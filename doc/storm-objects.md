
### JSONObject in Storm

This is the new proposal which is to switch **value** from

java.lang.Long to java.lang.Double

to support the new math simulator and the ability
for our customers to send in decimal values.

|                 | Java Type                 |
| --------------- |:-------------------------:|
| account_id      | java.lang.Long            |
| project_id      | java.lang.Long            |
| dimension       | java.lang.String          |
| key             | java.lang.String          |
| value           | java.lang.Double          |
| created_at      | java.lang.String          |
| calculation     | org.json.simple.JSONArray |
| interval        | org.json.simple.JSONArray |
| dbnumber        | java.lang.Long            |


### Old JSONObject

This is the default parsing when the tuple is taken off of RabbitMQ and cast as a JSONObject:

```
"account_id" -> "java.lang.Long"
"project_id" -> "java.lang.Long"
"dimension" -> "java.lang.String"
"key" -> "java.lang.String"
"value" -> "java.lang.Long"
"created_at" -> "java.lang.String"
"calculation" -> "org.json.simple.JSONArray"
"interval" -> "org.json.simple.JSONArray"
"dbnumber" -> "java.lang.Long"
```
