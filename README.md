

Here is the model specification:

https://github.com/stormasm/spinnakr-generic-ds/blob/master/test05.json

The **interval** and the **calculation** are functions of **type** and **dimension**,
in other words **interval** and **calculation** are dependent upon **type** and **dimension**.

For type = visit, and dimension = uuid

```
interval = ["hours", "days"]
calculation = "sum", "average"
```

For type = visit, and dimension = useragent

key= ["mozilla", "firefox", "chrome"]

```
interval = ["weeks"]
calculation = ["sum", "average", "percentage"]
```

intervals can be

```
["seconds", "minutes", "hours", "days", "weeks", "months", "years"]
```
