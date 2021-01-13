centos7 certbot

## 安裝 Certbot

安裝 Certbot
```
yum install -y certbot
```

安裝 Python2-certbot-apache
```
yum install -y python2-certbot-apache
```

安裝 Apache mod_ssl，安裝好 mod_ssl 後, 系統會自動建立 Apache 的 ssl 設定檔, 位置在 /etc/httpd/conf.d/ssl.conf
```
yum install mod_ssl
```

## 使用 Certbot 申請 SSL 金鑰

> 依需求自行修改
> - certonly：僅申請憑證，不編輯 httpd.conf
> - --apache：表示使用apache作為伺服器軟體
> - -w：網域所在的根目錄路徑
> - -d：連續請求的功能
> - --mail：SSL金鑰到期前寄送過期通知

```
certbot certonly --apache -w /var/www/html/ -d www.yourwebsite.com --email account@email.com
```

金鑰存放路徑
/etc/letsencrypt/live/www.yourwebsite.com/

如果有使用 certonly ，請自行修改 httpd-vhosts.conf 和 httpd-vhosts-le-ssl.conf 的內容，然後重啟apache
```
systemctl restart httpd
```

## 選擇 domain name 編號申請 SSL 金鑰

1. 進入申請SSL流程
```
certbot --apache
```
2. 選擇要申請SSL的網站代號
3. [1]為繼續使用過去的SSL，但是重新設定vhost； [2]為建立新的SSL金鑰，並且重新設定vhost

## certbot 常用指令

列出所有憑證及到期日
```
certbot certificates
```

測試是否能更新
```
certbot renew --dry-run
```

手動立即更新SSL憑證
```
certbot renew
```

## 參考資料
https://www.digit-seed.com/centos7-certbot-lets_encrypt_ssl/
<br>
https://linuxhostsupport.com/blog/how-to-install-lets-encrypt-on-centos-7-with-apache/