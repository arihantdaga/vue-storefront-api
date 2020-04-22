Same like from the documentation

#### Step 1
calling start.sh 
```
docker-compose -f docker-compose.yml -f docker-compose.nodejs.yml up -d
docker-compose -f docker-compose.magento.yml up -d
```

#### Step 2 (Temporary data)
```
docker exec -it vue-storefront-api_app_1 yarn restore
docker exec -it vue-storefront-api_app_1 yarn migrate
```

### Setting Up Magento on Lightsail 
- Lightsail create Magento app+os -> It can take upto 5 Mins. 
- Default admin credentials - user, for password do in ~ directory of the new instance - cat  bitnami_application_password . (ex. IEIebFUpB6XR) 
- Magento marketplace credentials 
```
username: "9891718dcb3d1333af392fb8d90b1655"
password: "44a3114353871afc25edc8c2da7560b4"
```
- Install Magento native module - https://github.com/DivanteLtd/magento2-vsbridge-indexer
```
sudo composer config repositories.divante vcs https://github.com/DivanteLtd/magento2-vsbridge-indexer
sudo composer require divante/magento2-vsbridge-indexer:dev-master
```



### Setting Up Magento
- docker-compose-up the image. 
- Install Sample Data
```
cd /opt/bitnami/magento/htdocs
sudo -u daemon php -d memory_limit=4G bin/magento sampledata:deploy // Note that we are allowing 4gb memort for this process, otherwise it throws some error. 
// Seems like this command also throws error in the end due to some permissions issue - hence we also have to run this
// However, i am not sure how safe they are. https://community.magento.com/t5/Magento-2-x-Technical-Issues/Extension-installation-failed-using-web-Setup-Wizard/td-p/114553
//
//sudo find var pub/static pub/media -type f -exec chmod g+w {} \; 
//sudo find var pub/static pub/media -type d -exec chmod g+ws {} \;
//sudo find ./pub/media -type d -exec chmod 777 {} \;
//sudo find ./pub/static -type d -exec chmod 777 {} \;

// This will however prompt for username and password - which are publick and private keys from magento developer account. 
// I think we can also just add these credentials in this file - /opt/bitnami/magento/htdocs/var/composer_home/auth.json
```
