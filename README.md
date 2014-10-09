

Here is the model specification:

https://github.com/stormasm/spinnakr-generic-ds/blob/master/test06.json

For dimension = visit-useragent

```
keys= ["mozilla", "firefox", "chrome"]
```

For dimension = visit-uuid

keys are uuids

For dimension = job-skills

```
keys = ["ios", "android", "java", "ruby", "python"]
```

calculations can be

```
["count", "sum", "average", "standard_deviation", "linear_regression"]
```

intervals can be

```
["seconds", "minutes", "hours", "days", "weeks", "months", "years"]
```
