參考 : [https://superuser.com/questions/648163/recursively-chown-all-files-that-are-owned-by-a-specific-user](https://superuser.com/questions/648163/recursively-chown-all-files-that-are-owned-by-a-specific-user)

改檔案修改權 

chmod 

改檔案用戶與群組

chown

大量調整檔案

`find . -type d -iname '???' -user old_user -exec chown -R new_user:new_group {} \;`

測試情境

`find . -type d -iname 'zh_TW' -user tiptop -exec chown -R tiptop:tiptop {} \;`

> 找出目錄名稱為 zh_TW 用戶為 tiptop 執行更改此目錄全部檔案
> 
> 
> 用戶 tiptop 群組 tiptop
> 

權限

root 以外用戶使用 su 切換用戶被擋住

![image](https://user-images.githubusercontent.com/96226780/217994624-b9cb761f-2532-4616-b9a0-ef1c59a4efb2.png)

參考 :

- [https://cloud.tencent.com/developer/article/1020334](https://cloud.tencent.com/developer/article/1020334)
- [https://unix.stackexchange.com/questions/61876/su-permission-denied-despite-correct-password](https://unix.stackexchange.com/questions/61876/su-permission-denied-despite-correct-password)
- [https://blog.csdn.net/master336/article/details/121972302](https://blog.csdn.net/master336/article/details/121972302)
- [http://iamnotpg.blogspot.com/2015/11/crontab-e.html](http://iamnotpg.blogspot.com/2015/11/crontab-e.html)
- [https://support.oneidentity.com/safeguard-authentication-services/kb/4271211/user-unable-to-run-crontab-command-due-to-error-you-username-are-not-allowed-to-access-to-crontab-because-of-pam-configuration](https://support.oneidentity.com/safeguard-authentication-services/kb/4271211/user-unable-to-run-crontab-command-due-to-error-you-username-are-not-allowed-to-access-to-crontab-because-of-pam-configuration)

檢查是不是沒有 setuid

![image](https://user-images.githubusercontent.com/96226780/217994663-65bd271e-53a0-4649-87bf-abc9b061bc08.png)

chmod u+s /bin/su

![image](https://user-images.githubusercontent.com/96226780/217994699-bebd1dbe-5e7b-4e0e-b852-c5af40b54ce3.png)

測試用戶可以切換

![image](https://user-images.githubusercontent.com/96226780/217994725-beb32ff9-9f5a-4652-a35f-2aa4246ddd5b.png)

如還是被擋住

檢查 /etc/pam.d/su

預設 wheel 群組是管理用

可以把該段註解

![image](https://user-images.githubusercontent.com/96226780/217994782-9b3a7e80-a843-4b42-9f7d-6fe9c0ec4240.png)

用戶查看排程

![image](https://user-images.githubusercontent.com/96226780/217994826-e42b5a2d-0808-45c9-90c1-ef7e61f787fe.png)

![image](https://user-images.githubusercontent.com/96226780/217994848-5fc3e1e4-ea6c-4c7a-aa24-74ec1f7502db.png)

也需要給權限

chmod u+s /bin/crontab

如缺少 /etc/cron.deny 也會不能執行

可以給一個空檔案

![image](https://user-images.githubusercontent.com/96226780/217994876-6212ef33-a657-466b-83ae-c1aaf00c02ef.png)
