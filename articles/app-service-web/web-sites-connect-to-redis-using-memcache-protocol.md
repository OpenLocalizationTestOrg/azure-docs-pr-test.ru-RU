---
title: "aaaConnect tooRedis приложения web службы приложений, через протокол Memcache - Azure hello | Документы Microsoft"
description: "Подключение веб-приложения в приложение Azure службы tooRedis кэша с помощью протокола Memcache hello"
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Подключение веб-приложения в службе приложений Azure tooRedis кэша через протокол Memcache hello
В этой статье вы узнаете, как приложение в веб-tooconnect WordPress [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) слишком[кэш Azure Redis] [ 12] с помощью hello [Memcache] [ 13] протокола. При наличии существующего веб-приложения, которая использует сервер Memcached для кэша в памяти, можно перенести tooAzure службы приложений и использовать hello основном кэширования решение в Microsoft Azure с незначительной или нулевой изменение tooyour кода приложения. Кроме того можно использовать существующие Memcache опыт toocreate масштабируемых, распределенные приложения в службе приложений Azure с помощью кэша Redis для Azure для кэширования в памяти, при использовании популярных платформ приложений, таких как .NET, PHP, Node.js, Java и Python.  

Службы приложений веб-приложения поддерживает такие сценарии приложений с оболочке Memcache приложения Web hello, являющийся локального сервера Memcached, который выступает в качестве прокси-сервера Memcache для кэширования вызовы tooAzure кэша Redis. Это позволяет любому приложению, которое взаимодействует с помощью протокола toocache hello Memcache данных с кэшем Redis. Прокладку Memcache работает на уровне протокола hello, поэтому он может использоваться любым приложения или платформы приложения до тех пор, пока он взаимодействует с помощью протокола Memcache hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Предварительные требования
оболочке Memcache Web приложения Hello может использоваться с любым приложением, предоставляемых обменивается данными с помощью протокола Memcache hello. Для этого конкретного примера приложения hello ссылка является масштабируемой WordPress сайт, который может предоставляться из hello Azure Marketplace.

Выполните шаги hello, описанные в следующих статьях:

* [Подготовка экземпляра hello служба кэша Redis Azure][0]
* [Развертывание масштабируемого сайта WordPress в Azure][1]

После развертывания сайта WordPress масштабируемой hello и подготовить экземпляр кэша Redis будет готов tooproceed с включением оболочке Memcache hello в веб-приложениях службы приложений Azure.

## Включить оболочке Memcache Web приложения hello
В оболочке Memcache tooconfigure заказ необходимо создать три параметра приложения. Это можно сделать с помощью различных методов, включая hello [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715), hello [классический портал][3], hello [командлеты PowerShell Azure] [ 5] или hello [интерфейса командной строки Azure][5]. Hello целях эту запись, я буду toouse hello [портала Azure] [ 4] tooset параметры приложения hello. Hello следующие значения могут быть получены из **параметры** колонке экземпляра кэша Redis.

![Колонка параметров кэша Redis для Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### Добавление параметра приложения REDIS_HOST
Здравствуйте, первый параметр приложения, необходимо toocreate — hello **REDIS\_узла** параметра приложения. Этот параметр задает hello toowhich hello оболочки пересылает hello кэша данные о месте назначения. Здравствуйте, значение является обязательным для параметра приложения hello REDIS_HOST могут быть получены из hello **свойства** колонке экземпляра кэша Redis.

![Имя хоста кэша Redis для Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Набор hello ключ установки приложения hello слишком**REDIS\_узла** и значение hello toohello параметр приложения hello **hostname** hello экземпляра кэша Redis.

![Параметр веб-приложения REDIS_HOST](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### Добавление параметра приложения REDIS_KEY
Здравствуйте, второй параметр приложения, необходимо toocreate — hello **REDIS\_ключ** параметра приложения. Данный параметр предоставляет кэш Redis hello проверки подлинности маркеров требуется toosecurely доступ hello экземпляра. Можно получить значение hello, необходимые для параметра приложения hello REDIS_KEY из hello **ключи доступа** колонку кэша Redis экземпляра hello.

![Первичный ключ кэша Redis для Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Ключ набора hello установки приложения hello слишком**REDIS\_ключ** и значение hello toohello параметр приложения hello **первичный ключ** hello экземпляра кэша Redis.

![Параметр веб-приложения REDIS_KEY](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### Добавление параметра приложения MEMCACHESHIM_REDIS_ENABLE
Последний параметр приложения Hello — используется tooenable hello оболочке Memcache в веб-приложения, использующего hello REDIS_HOST и REDIS_KEY toohello tooconnect кэша Redis для Azure и прямой hello вызовов кэша. Ключ набора hello установки приложения hello слишком**MEMCACHESHIM\_REDIS\_ВКЛЮЧИТЬ** и hello значение слишком**true**.

![Параметр веб-приложения MEMCACHESHIM_REDIS_ENABLE](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

После завершения добавления параметров приложения hello трех (3), нажмите кнопку **Сохранить**.

## Включение расширения Memcache для PHP
Чтобы hello toospeak приложения hello протокол Memcache при необходимости tooinstall hello Memcache расширения tooPHP--hello языковой платформе для сайта WordPress.

### Загрузить php_memcache hello расширения
Обзор слишком[нагрузка PECL][6]. В разделе hello кэширование категории, нажмите кнопку [memcache][7]. В разделе загрузок hello столбца по ссылке hello DLL.

![Веб-сайт PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

Загрузите hello потока не безопасном (Обновить) x86 ссылку для hello версии включены в веб-приложений PHP. (по умолчанию это PHP 5.4).

![Пакет Memcache веб-сайта PHP PECL](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### Включить расширение php_memcache hello
После загрузки файла hello, распаковка и отправить hello **php\_memcache.dll** в hello **d:\\домашней\\сайта\\wwwroot\\bin\\ext\\**  каталога. После передачи hello php_memcache.dll в веб-приложения hello необходимо tooenable hello расширения toohello среды выполнения PHP. hello tooenable расширение Memcache в портале Azure, откройте hello hello **параметры приложения** колонку для веб-приложения hello, затем добавьте новый параметр приложения с ключом hello **PHP\_расширения** и hello значение **bin\\ext\\php_memcache.dll**.

> [!NOTE]
> Если веб-приложение hello должен tooload несколько расширений PHP, значение hello PHP_EXTENSIONS должен быть список с разделителями запятыми файлы tooDLL относительные пути.
> 
> 

![Параметр веб-приложения PHP_EXTENSIONS](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

По завершении щелкните **Сохранить**.

## Установка подключаемого модуля Memcache WordPress
> [!NOTE]
> Можно также загрузить hello [подключаемый модуль кэша объекта Memcached](https://wordpress.org/plugins/memcached/) из WordPress.org.
> 
> 

На странице приветствия WordPress подключаемых модулей щелкните **добавить новое**.

![Страница подключаемого модуля WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

Введите в поле поиска hello **memcached** и нажмите клавишу **ввод**.

![Добавление нового подключаемого модуля WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

Найти **кэш объектов Memcached** hello списка, а затем нажмите кнопку **установить сейчас**.

![Установка подключаемого модуля Memcache для WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Включить hello подключаемого модуля Memcache WordPress
> [!NOTE]
> Следуйте инструкциям hello в этом блоге на [как расширение сайта в веб-приложениях tooenable] [ 8] tooinstall Visual Studio Team Services.
> 
> 

В hello `wp-config.php` файл, добавьте следующий код выше редактирования комментарий hello stop конце hello файл hello hello.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

После вставленных этот код Монако автоматически сохранит hello документа.

Hello следующим шагом является tooenable hello объекта кэша, подключаемый модуль. Это делается с помощью перетаскивания **объекта cache.php** из **wp-content/подключаемых модулей и memcached** toohello папки **wp-content** tooenable папку hello объекта Memcache Функции кэша.

![Найдите подключаемый модуль объекта cache.php memcache hello](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

Теперь этот hello **объекта cache.php** файл находится в hello **wp-content** папки кэша объектов Memcached включен hello.

![Включение подключаемого модуля объекта cache.php memcache hello](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Проверьте hello кэш объектов Memcache работы подключаемого модуля
Все оболочки совместимости приложений Memcache Web hello действия tooenable hello, теперь завершения. что осталось Hello — tooverify, что данные hello заполнения экземпляра кэша Redis.

### Включить поддержку порт не SSL hello в кэше Redis для Azure
> [!NOTE]
> Во время написания данной статьи hello hello Redis CLI не поддерживает SSL-подключение, таким образом hello процедуры ниже необходимы.
> 
> 

Откройте экземпляр кэша Redis toohello, созданный для этого веб-приложения в hello портала Azure. После открытия hello кэша щелкните hello **параметры** значок.

![Кнопка параметров кэша Redis для Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

Выберите **порты доступа** из списка hello.

![Порт доступа к кэшу Redis для Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

Щелкните **Нет** для параметра **Разрешить доступ только по SSL**.

![Порт доступа к кэшу Redis для Azure (только SSL)](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

Вы увидите hello порт SSL не настроена. Щелкните **Сохранить**.

![Портал доступа к кэшу Redis для Azure (без SSL)](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### Подключение из redis cli tooAzure кэша Redis
> [!NOTE]
> При выполнении этого действия предполагается, что программное обеспечение Redis установлено локально на компьютере, на котором проводится разработка. [Установите Redis локально, следуя этим указаниям][9].
> 
> 

Откройте консоль командной строки для hello выбора и введите следующую команду:

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Замените hello  **&lt;имя узла для redis кэша&gt;**  с именем узла фактическое xxxxx.redis.cache.windows.net hello и hello  **&lt;первичный ключ для redis кэша&gt;**  hello ключ доступа для кэша hello, затем нажмите клавишу **ввод**. После hello CLI подключенный экземпляр кэша Redis toohello, выполните любые команды redis. В приведенном далее снимке экрана приветствия я выбрал toolist hello ключей.

![Подключение из Redis CLI в терминале tooAzure кэша Redis](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

Hello вызовов toolist hello ключи должны возвращать значение. Если нет, навигация по toohello веб-приложение и повторите попытку.

## Заключение
Поздравляем! Теперь приложение Hello WordPress имеет tooaid централизованного кэша в памяти в увеличить пропускную способность. Обратите внимание, что hello оболочке Memcache Web приложений можно использовать с любой клиент Memcache, независимо от того, платформа приложения или языка программирования. tooprovide отзывы или tooask вопросы об оболочке Memcache Web приложения hello, учет слишком[форумы MSDN] [ 10] или [Stackoverflow][11].

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org
