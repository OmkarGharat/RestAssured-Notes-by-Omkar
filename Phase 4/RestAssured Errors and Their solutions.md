# RestAssured Errors and Their solutions

1. \<u>java.net.ConnectException\</u>: Connection refused: connect

missing baseURI in the code

***

1. java.lang.IllegalStateException: Target host is null

BaseURI is blank or empty

***

1. \<u>org.json.JSONException\</u>: A JSONObject text must begin with '{' at 1 \[character 2 line 1]

you are using response.toString()

use response.asString()

***

