
### JSONObject in Storm

|                 | Java Type                 | 
| --------------- |:-------------------------:|
| account_id      | java.lang.Long            |
| calculation     | org.json.simple.JSONArray |
| interval        | org.json.simple.JSONArray |



This is the default parsing when the tuple

is taken off of RabbitMQ and cast as a JSONObject:

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
