### Spinnakr Calculation Spec

All of the calculation data will live in Redis. Account data is stored on unique DB numbers.

Below is a list the keys used in the Storm calculations:

#### Generic Persistence Keys

```
set:projects
```

A simple set of project ids on the selected database.

```
set:PROJECT:dimensions
```

A set of all dimensions declared in a project.

i.e., "visit-useragent", "visit-uuid", "job-skills", etc.

```
set:PROJECT:DIMENSION:keys
```

A set of all keys declared for a specific project-dimension.

Examples for project_ids {1,2}:

```
set:1:visit-useragent:keys
set:1:visit-uuid:keys

set:2:job-skills:keys
```

Contents of 
```
set:2:job-skills:keys
``` 
would contain:

```
1) "ruby"
2) "ios"
3) "java"
4) "python"
5) "android"
```

```
set:PROJECT:DIMENSION:KEY:calculations
```

A set of declared calculations to perform on a specific key.

Examples for project ids {2}:
```
set:2:job-skills:ruby:calculations
set:2:job-skills:python:calculations

```

Contents of 
```
set:2:job-skills:python:calculations
``` 
would contain:

```
1) "sum"
2) "standard_deviation"
3) "count"
4) "linear_regression"
5) "average"

```

```
set:PROJECT:DIMENSION:KEY:CALCULATION:intervals
```

A set of declared intervals for calculations.

Examples for project ids {2}:
```
set:2:job-skills:ruby:sum:intervals
set:2:job-skills:python:average:intervals

```
Contents of 
```
set:2:job-skills:python:average:intervals
``` 
would contain:

```
1) "months"
2) "weeks"
```

```
hash:PROJECT:DIMENSION:KEY:values
```

This is a hash that contains all the values for a declared dimension-key. All keys in the hashmap are timestamps. 

Examples for project ids {2}:

```
hash:2:job-skills:python:values
```

Contents would contain:

```
1) "2014-10-17 21:34:07 -0400"
2) "8"
3) "2014-10-08 06:57:22 -0400"
4) "5"
5) "2014-10-10 21:52:11 -0400"
6) "5"
7) "2014-10-13 21:26:07 -0400"
8) "2"
9) "2014-10-18 03:57:18 -0400"
10) "7"
11) "2014-10-11 11:30:45 -0400"
12) "10"
```

#### Calculation Hashmap

```
hash:PROJECT:DIMENSION:KEY:CALCULATION:INTERVAL
```

A hash that contains the calculated value for a given interval for a declared dimension-key.

i.e. 
```
hash:2:job-skills:python:count:months
```

##### Count & Sum

These calculations use timestamps formatted for their intervals (YYYY, YYYYMM, YYYYMMDD, etc) as their keys.

i.e. 
```
hash:2:job-skills:python:count:months
``` 
would contain this:

```
1) "2014-10"
2) "53"
3) "2014-11"
4) "29"
```
##### Average & Standard Deviation

These calculations just use their calculation name as the key. i.e. average & standard_devation.

The key 
```
hash:2:job-skills:python:average:months
``` 
would contain this:

```
1) "average"
2) "219.0"
```

##### Linear Regression

This calculation is has unique keys. They are "intercept", "slope", "ci_90", "ci_95", and "ci_99". The "ci_*" keys are short for confidence interval with associated alpha.

The key 
```
hash:2:job-skills:python:linear_regression:weeks
``` 
would contain the following:

```
1) "intercept"
2) "60.53333333333333"
3) "slope"
4) "5.6571428571428575"
5) "ci_99"
6) "22.79094188400575"
7) "ci_95"
8) "13.743808674832158"
9) "ci_90"
10) "10.552952873877196"
```

