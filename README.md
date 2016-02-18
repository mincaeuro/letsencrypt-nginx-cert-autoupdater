# letsencrypt-nginx-cert-autoupdater


1. use steps from official guide:
https://community.letsencrypt.org/t/quick-start-guide/1631

```
 cd /home/<user>/
  git clone https://github.com/letsencrypt/letsencrypt
  cd letsencrypt
  ./letsencrypt-auto
```
2. create script file with:
```
  vim my_cert_script.sh
```
- paste:
```
  #! /bin/shecho "stoping Nginx...";
  sudo service nginx stop;
  
  cd /home/<user>/letsencrypt/;
  sudo -H ./letsencrypt-auto --domain yourdomain.com --domain www.yourdomain.com --server https://acme-v01.api.letsencrypt.org/directory auth;
  
  echo "Starting Nginx...";
  
  sudo service nginx start;
```

3. save it
 ```
chmod +x my_cert_script.sh
```
4. setup Crjob (as root)
```  
crontab -e
```
5. paste
	```
1 0 12 2,5,8,11 * /home/<user>/my_cert_script.sh >> /home/<user>/cert.log 2>&1
```
- you've to set it every 3 moths, you can't add in cronjob simply 90 days...in my exaple 12th Feb/May/Aug/Nov
6. save
