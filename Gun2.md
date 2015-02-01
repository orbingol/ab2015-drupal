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
