## <a name="install-wordpress"></a><span data-ttu-id="7329b-101">Установка WordPress</span><span class="sxs-lookup"><span data-stu-id="7329b-101">Install WordPress</span></span>

<span data-ttu-id="7329b-102">Если требуется tootry комплекта, установите образец приложения.</span><span class="sxs-lookup"><span data-stu-id="7329b-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="7329b-103">Например, hello следующие шаги установки Привет открыть источник [WordPress](https://wordpress.org/) платформы toocreate веб-сайты и блоги.</span><span class="sxs-lookup"><span data-stu-id="7329b-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="7329b-104">Включить другие рабочие нагрузки tootry [Drupal](http://www.drupal.org) и [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="7329b-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="7329b-105">Эта программа установки WordPress предназначена для подтверждения концепции.</span><span class="sxs-lookup"><span data-stu-id="7329b-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="7329b-106">Дополнительные сведения и параметры для установки в рабочей среде см. в разделе hello [документации WordPress](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="7329b-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="7329b-107">Установка пакета WordPress hello</span><span class="sxs-lookup"><span data-stu-id="7329b-107">Install hello WordPress package</span></span>

<span data-ttu-id="7329b-108">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="7329b-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="7329b-109">Настройка WordPress</span><span class="sxs-lookup"><span data-stu-id="7329b-109">Configure WordPress</span></span>

<span data-ttu-id="7329b-110">Настройте WordPress toouse MySQL и PHP.</span><span class="sxs-lookup"><span data-stu-id="7329b-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="7329b-111">Запустите следующие команды tooopen hello текстовый редактор, по вашему выбору и создайте файл hello `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="7329b-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="7329b-112">Копировать hello следующие строки toohello файл, указав пароль базы данных для *yourPassword* (оставить другие значения без изменений).</span><span class="sxs-lookup"><span data-stu-id="7329b-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="7329b-113">Затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="7329b-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="7329b-114">В рабочем каталоге, создайте текстовый файл `wordpress.sql` tooconfigure hello WordPress, базы данных:</span><span class="sxs-lookup"><span data-stu-id="7329b-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="7329b-115">Добавить hello следующие команды, указав пароль базы данных для *yourPassword* (оставить другие значения без изменений).</span><span class="sxs-lookup"><span data-stu-id="7329b-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="7329b-116">Затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="7329b-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="7329b-117">Выполните hello, следующая команда toocreate hello, базы данных:</span><span class="sxs-lookup"><span data-stu-id="7329b-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="7329b-118">После завершения команды hello, удалите файл hello `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="7329b-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="7329b-119">Переместите hello WordPress установки toohello корень веб-сервера документа:</span><span class="sxs-lookup"><span data-stu-id="7329b-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="7329b-120">Теперь можно завершить настройку WordPress hello и опубликовать на платформе hello.</span><span class="sxs-lookup"><span data-stu-id="7329b-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="7329b-121">Откройте браузер и перейдите в слишком`http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="7329b-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="7329b-122">Замените hello общедоступный IP-адрес виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7329b-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="7329b-123">Он должен выглядеть примерно toothis изображения.</span><span class="sxs-lookup"><span data-stu-id="7329b-123">It should look similar toothis image.</span></span>

![Страница установки WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)