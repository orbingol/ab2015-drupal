# Drush Komutları (devamı)

## Drupal indirme ve dizin adı değiştirme

`drush dl drupal --drupal-project-rename`

## Drupal kurulumu (minimal profil)

`drush si minimal --db-url=mysql://drupal:drupal@localhost/drupal`

## Minimal kurulum sonrası aktifleştirilecek modüller

* Block (block) 
* Database logging (dblog) 
* Field (field)  
* Field SQL storage (field_sql_storage)
* Field UI (field_ui)
* File (file)
* Filter (filter) 
* Image (image)  
* List (list)  
* Locale (locale)  
* Menu (menu)  
* Node (node)
* Number (number)  
* Options (options) 
* Path (path)
* PHP filter (php)    
* System (system)   
* Taxonomy (taxonomy)   
* Text (text) 
* Toolbar (toolbar)    
* Update manager (update)    
* User (user) 

## *Corporate Clean* temasının kurulması ve aktifleştirilmesi

* `drush dl corporateclean`
* `drush en corporateclean`
* `drush vset theme_default corporateclean`

## *Rubik* admin temasının kurulması

* `drush dl tao, rubik`
* `drush en tao, rubik`
* `drush vset admin_theme rubik`

## Kullanıcı işlemleri

* *admin* kullanıcısı şifresinin *12345* şeklinde değiştirilmesi

```
drush user-password admin --password="12345"
```

* *admin* kullanıcısı için tek kullanımlık giriş linkinin oluşturulması

```
drush user-login
```

## Yanlış şifre girerseniz ve kullanıcı adımız bloklanırsa ne yapabiliriz?

**Yol 1:**

`drush user-login`

**Yol 2:**

`drush sql-query "TRUNCATE flood;"`

## Bugün üzerinde çalıştığımız modüller

* views
* calendar
* date
* panels

Drupal kapsamında oluşan bazı olaylar sonrasında işlem yapılmak istendiğinde ise aşağıdaki modüller denenebilir.

* trigger
* rules (oldukça kapsamlıdır)
