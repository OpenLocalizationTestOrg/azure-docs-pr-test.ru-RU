## <a name="install-wordpress"></a><span data-ttu-id="db857-101">Установка WordPress</span><span class="sxs-lookup"><span data-stu-id="db857-101">Install WordPress</span></span>

<span data-ttu-id="db857-102">Чтобы проверить работу стека, установите пример приложения.</span><span class="sxs-lookup"><span data-stu-id="db857-102">If you want to try your stack, install a sample app.</span></span> <span data-ttu-id="db857-103">Например, выполните приведенные ниже шаги, чтобы установить платформу [WordPress](https://wordpress.org/) с открытым кодом для создания веб-сайтов и блогов.</span><span class="sxs-lookup"><span data-stu-id="db857-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span></span> <span data-ttu-id="db857-104">Для других рабочих нагрузок потребуется установка платформ [Drupal](http://www.drupal.org) и [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="db857-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="db857-105">Эта программа установки WordPress предназначена для подтверждения концепции.</span><span class="sxs-lookup"><span data-stu-id="db857-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="db857-106">Дополнительные сведения об установке в рабочей среде и параметры см. в [документации WordPress](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="db857-106">For more information and settings for production installation, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-the-wordpress-package"></a><span data-ttu-id="db857-107">Установка пакета WordPress</span><span class="sxs-lookup"><span data-stu-id="db857-107">Install the WordPress package</span></span>

<span data-ttu-id="db857-108">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="db857-108">Run the following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="db857-109">Настройка WordPress</span><span class="sxs-lookup"><span data-stu-id="db857-109">Configure WordPress</span></span>

<span data-ttu-id="db857-110">Настройте WordPress, чтобы использовать MySQL и PHP.</span><span class="sxs-lookup"><span data-stu-id="db857-110">Configure WordPress to use MySQL and PHP.</span></span> <span data-ttu-id="db857-111">Чтобы открыть необходимый текстовый редактор и создать файл `/etc/wordpress/config-localhost.php`, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="db857-111">Run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="db857-112">Скопируйте следующие строки в файл, заменив пароль базы данных на *свой_пароль*. Другие значения оставьте без изменений.</span><span class="sxs-lookup"><span data-stu-id="db857-112">Copy the following lines to the file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="db857-113">Затем сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="db857-113">Then save the file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="db857-114">В рабочей папке создайте текстовый файл `wordpress.sql`, чтобы настроить базу данных WordPress.</span><span class="sxs-lookup"><span data-stu-id="db857-114">In a working directory, create a text file `wordpress.sql` to configure the WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="db857-115">Добавьте следующие команды, заменив пароль базы данных на *свой_пароль*. Другие значения оставьте без изменений.</span><span class="sxs-lookup"><span data-stu-id="db857-115">Add the following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="db857-116">Затем сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="db857-116">Then save the file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="db857-117">Выполните следующую команду для создания базы данных.</span><span class="sxs-lookup"><span data-stu-id="db857-117">Run the following command to create the database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="db857-118">После выполнения команды удалите файл `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="db857-118">After the command completes, delete the file `wordpress.sql`.</span></span>

<span data-ttu-id="db857-119">Переместите файлы установки WordPress в корневой каталог документов на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="db857-119">Move the WordPress installation to the web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="db857-120">Теперь можно завершить настройку WordPress и выполнить публикацию на платформе.</span><span class="sxs-lookup"><span data-stu-id="db857-120">Now you can complete the WordPress setup and publish on the platform.</span></span> <span data-ttu-id="db857-121">Откройте браузер и перейдите на страницу `http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="db857-121">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="db857-122">Замените общедоступный IP-адрес своей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="db857-122">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="db857-123">Она должна выглядеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="db857-123">It should look similar to this image.</span></span>

![Страница установки WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)