SQL injection vulnerability exists in tongda oa v2017

version:2017

Route: general/hr/manage/staff_relatives/delete.php

There is an injected parameter: $RELATIVES_ID

The code here is neat, concatenating parameters directly into the SQL statement when $RELATIVES_ID is not empty. There is a bypass because of the parenthesis closure.

![WPS图片(1)](https://github.com/RCEraser/cve/assets/131632691/71670d34-ca27-4d73-a803-97bb2243669c)

We can use Cartesian product blind injection, the following payload can determine that the first character of the database name is t, because it was successfully delayed at 116. ascii 116 also corresponds to the lowercase letter t. In this way, the database name and any database information can be obtained through blind injection.

POC
```
1)%20and%20(substr(DATABASE(),1,1))=char(116)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)%20and(1)=(1
```
![WPS图片(2)](https://github.com/RCEraser/cve/assets/131632691/af257358-ab7b-4cd9-b114-333f9dbcc493)
