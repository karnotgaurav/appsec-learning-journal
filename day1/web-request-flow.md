Stage	Action	Security Responsibility
Browser	User inputs data.	None (Assume the browser is compromised).
Server Entry	Request received.	Identify Untrusted Input (Headers, Body, URL).
Logic	Code processes data.	Input Validation (Check type, length, format).
Database	Data storage/retrieval.	Parameterized Queries (Prevent SQL Injection).
Response	HTML/JSON generation.	Output Encoding (Prevent XSS).


Step 1: Browser (The Request)

    Action: User clicks "Submit".

    Data: The browser packs the comment into a JSON body inside a POST request.

    Security Reality: The browser cannot be trusted. An attacker can bypass any checks here.

Step 2: Server (The Entry)

    Action: The server receives the request packet.

    Data: The server parses the JSON body to find comment.

    Security Reality: This is where Untrusted Input enters the system.

Step 3: Logic (The Processing)

    Action: The code checks the input (e.g., "Is the comment too long?").

    Data: The code prepares the data for the database.

    Security Reality: Validation happens here (check type/length), but we generally don't change the data yet. We treat it as a string.

Step 4: Database (The Storage)

    Action: The logic sends the comment to the DB to be saved.

    Data: INSERT INTO comments VALUES ('<script>alert(1)</script>')

    Security Reality: We use Parameterized Queries here. This tells the DB: "Treat this input as just text, not as a command." The DB saves the script tags safely as plain text.

Step 5: Response (The Output)

    Action: Another user views the blog post. The server pulls the comment from the DB and puts it into the HTML.

    Data: The server converts < to &lt; and > to &gt;.

    Security Reality: This is Output Encoding. The browser receives &lt;script&gt;... and displays it harmlessly instead of running it.

In Short:

    Browser: Sends the threat.

    Server: Receives the threat.

    Logic: Validates the threat (length/type).

    DB: Stores the threat (safely).

    Response: Neutralizes the threat (Encoding) so it can't run.