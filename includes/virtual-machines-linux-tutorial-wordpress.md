## <a name="install-wordpress"></a>Установка WordPress

Если требуется tootry комплекта, установите образец приложения. Например, hello следующие шаги установки Привет открыть источник [WordPress](https://wordpress.org/) платформы toocreate веб-сайты и блоги. Включить другие рабочие нагрузки tootry [Drupal](http://www.drupal.org) и [Moodle](https://moodle.org/). 

Эта программа установки WordPress предназначена для подтверждения концепции. Дополнительные сведения и параметры для установки в рабочей среде см. в разделе hello [документации WordPress](https://codex.wordpress.org/Main_Page). 



### <a name="install-hello-wordpress-package"></a>Установка пакета WordPress hello

Выполните следующую команду hello.

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>Настройка WordPress

Настройте WordPress toouse MySQL и PHP. Запустите следующие команды tooopen hello текстовый редактор, по вашему выбору и создайте файл hello `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
Копировать hello следующие строки toohello файл, указав пароль базы данных для *yourPassword* (оставить другие значения без изменений). Затем сохраните файл hello.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

В рабочем каталоге, создайте текстовый файл `wordpress.sql` tooconfigure hello WordPress, базы данных: 

```bash
sudo sensible-editor wordpress.sql
```

Добавить hello следующие команды, указав пароль базы данных для *yourPassword* (оставить другие значения без изменений). Затем сохраните файл hello.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


Выполните hello, следующая команда toocreate hello, базы данных:

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

После завершения команды hello, удалите файл hello `wordpress.sql`.

Переместите hello WordPress установки toohello корень веб-сервера документа:

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

Теперь можно завершить настройку WordPress hello и опубликовать на платформе hello. Откройте браузер и перейдите в слишком`http://yourPublicIPAddress/wordpress`. Замените hello общедоступный IP-адрес виртуальной Машины. Он должен выглядеть примерно toothis изображения.

![Страница установки WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)