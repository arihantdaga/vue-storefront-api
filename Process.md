Same like from the documentation

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
