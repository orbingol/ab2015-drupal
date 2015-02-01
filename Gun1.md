# Akademik Bilişim 2015 - Drupal Eğitimi

## Giriş

Akademik Bilişim 2015 kapsamında düzenlenen *Eğitim Kurumları için Drupal* kursunun ders notlarıdır.

## Eğitmenler

* [Onur Rauf Bingöl](http://onurraufbingol.com)
* [Murat Duman](https://www.muratduman.com)

## Geliştirme ortamının kurulumu

### Sistem paketlerinin kurulumu

```bash
~ $ sudo apt-get install apache2 php5 mysql-server phpmyadmin php5-gd
~ $ sudo apt-get install git
```

### Apache ayarlarının yapılması

Öncelikle `id` komutu çalıştırılır ve kullanıcı adı / grubu belirlenir.

```bash
~  $ id
uid=1000(drupal) gid=1000(drupal) ...
```

Buna göre,

* **Kullanıcı adı:** drupal
* **Kullanıcı grubu:** drupal

Bu noktada Apache'nin kendi kullanıcımız ve grubumuz ile çalışmasını sağlıyoruz.

```bash
~ $ nano /etc/apache2/envvars
```

ve aşağıdaki satırları bulup,

```bash
export APACHE_RUN_USER=www-data
export APACHE_RUN_GROUP=www-data
```

şu şekilde değiştiriyoruz:

```bash
export APACHE_RUN_USER=drupal
export APACHE_RUN_GROUP=drupal
```

Gerekli bazı eklentileri aktifleştiriyoruz.

```bash
~ $ sudo a2enmod rewrite
```

Apache varsayılan dizinini değiştiriyoruz.

```bash
~ $ sudo nano /etc/apache2/sites-available/000-default.conf
```

Bu dosya içinde aşağıdaki satırı bulup,

```
DocumentRoot /var/www/html
```

şu şekilde değiştiriyoruz:

```
DocumentRoot /home/drupal/public_html
```

Debian ve türevi Linux dağıtımları için PHP ayarlarında bazı değişiklikler yapmamız gerekiyor.

```bash
~ $ sudo nano /etc/apache2/mods-available/php5.conf
```

Bu dosyanın içinde aşağıdaki satırları bulup siliyoruz veya başına `#` işareti ekliyoruz.

```
<IfModule mod_userdir.c>
    <Directory /home/*/public_html>
        php_admin_flag engine Off
    </Directory>
</IfModule>
```

En son olarak, Apache için kullanacağımızı belirttiğimiz ev dizinini oluşturuyoruz.

```bash
~ $ mkdir public_html
```

ve ayarlarımızın çalışması için Apache'yi yeniden başlatıyoruz.

```bash
~ $ sudo service apache2 restart
```

### Drupal multi-site için ayarların yapılması

Yakında.

### Drush kurulması

Öncelikle sistemde kurulu Drush paketlerini kaldırmamız gerekiyor.

```bash
~ $ sudo apt-get purge drush
```

ve gerekli bir paketi kuruyoruz.

```bash
~ $ sudo apt-get install php-console-table
```

Drush git reposundan paketi indiriyoruz.

```bash
~ $ git clone https://github.com/drush-ops/drush.git
~ $ cd drush
~/drush $ git checkout 6.5.0
```

Bu kullanıcının erişebileceği her yerde çalışabilmesi için bir Bash alias tanımlıyoruz. Aşağıdaki komutu yazıyoruz.

```bash
~ $ nano ~/.bashrc
```

ve açılan dosyanın en altına aşağıdaki satırı ekliyoruz.

```bash
alias drush="$HOME/drush/drush"
```

Bir sonraki aşamada ise aşağıdaki komutu çalıştırıyoruz.

```bash
~ $ source ~/.bashrc
```

`source` komutunu çalıştırmak yerine terminal ekranını açıp kapatabilirsiniz. İkisi de aynı işe yarayacaktır.

## Veritabanı işlemleri

Veritabanı eklemek için [phpMyAdmin](http://www.phpmyadmin.net) kullanabilir veya [şu yazıyı](http://onurraufbingol.com/2015/01/29/komut-satirindan-mysql-ile-calismak-bolum2.html) referans alabilirsiniz.

## Drush

### Drupal kurulumu

```bash
~ $ cd public_html
~/public_html $ drush dl drupal
~/public_html $ mv drupal-7.34 drupal
~/public_html $ cd drupal
~/public_html/drupal $ drush si --db-url=mysql://dbuser:dbpass@localhost/drupaldb
```

### Drush geliştirme web sunucusu

```bash
~/public_html/drupal $ drush rs
```

### Türkçe dil ekleme

```bash
~/public_html/drupal $ drush en locale
~/public_html/drupal $ drush dl drush_language
~/public_html/drupal $ drush language-add tr
~/public_html/drupal $ drush language-default tr
```

### Türkçe dil paketini kurma

```bash
~/public_html/drupal $ drush dl l10n_update
~/public_html/drupal $ drush en l10n_update
~/public_html/drupal $ drush l10n-update
```
