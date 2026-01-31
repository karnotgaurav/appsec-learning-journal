
---

## 📄 `Day-03/juice-shop-authorization-review.md`

```md
# Day 03 – Juice Shop Authorization Review

## Objective
To analyze real authorization patterns in OWASP Juice Shop and distinguish secure and insecure implementations.

---

## Secure Endpoint Example

### Route
```ts
app.delete('/api/Addresss/:id',
  security.appendUserId(),
  address.delAddressById()
)
)

Handler Logic

AddressModel.destroy({
  where: {
    id: req.params.id,
    UserId: req.body.UserId
  }
})

Why This Is Secure

    User identity is derived from JWT

    Object ownership is enforced

    Deletion only occurs if both ID and UserId match

Route-Level Authorization Example

app.route('/api/Users/:id')
  .get(security.isAuthorized())
  .put(security.denyAll())
  .delete(security.denyAll())

Observations

    Route access is controlled

    Sensitive operations are denied globally

    Object-level checks are not applicable here

Key Lesson

Different resources require different authorization strategies:

    User-owned objects → object-level checks

    Sensitive system resources → route-level deny

    Public data → limited or no authorization