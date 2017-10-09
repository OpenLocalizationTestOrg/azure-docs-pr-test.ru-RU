---
title: "Класс aaaEnterprise WordPress в Azure | Документы Microsoft"
description: "Узнайте, как toohost WordPress корпоративного уровня сайта в службе приложений Azure"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>WordPress корпоративного класса в Azure
Служба приложений Azure предоставляет масштабируемую, безопасную и простую в использовании среду для критически важных, крупномасштабных сайтов [WordPress][wordpress]. Майкрософт, сама выполняет сайтов корпоративного уровня, например hello [Office] [ officeblog] и [Bing] [ bingblog] блоги. В этой статье показано, как toouse hello веб-приложений функции tooestablish службу приложений Microsoft Azure и поддерживать корпоративного уровня, облачного сайта WordPress, который может обрабатывать большое количество посетителей.

## <a name="architecture-and-planning"></a>Архитектура и планирование
К базовой установке WordPress предъявляются только два требования:

* **База данных MySQL**: это требование доступна через [ClearDB в hello Azure Marketplace][cdbnstore]. Вы также можете управлять собственной установленной системой MySQL в виртуальных машинах Azure с использованием [Windows][mysqlwindows] или [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB обеспечивает несколько конфигураций MySQL, каждая из которых имеет разные характеристики производительности. В разделе hello [хранилища Azure] [ cdbnstore] сведения о предложениях, которые предоставляются через магазин Azure hello или напрямую, как показано на hello [веб-сайте ClearDB](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 или более поздней версии** — служба приложений Azure в настоящее время предоставляет версии [PHP 5.4, 5.5 и 5.6][phpwebsite].

  > [!NOTE]
  > Что вы всегда выполнения hello последняя версия PHP, рекомендуется, чтобы получить последние исправления безопасности hello.
  >
  >

### <a name="basic-deployment"></a>Базовое развертывание
При использовании только hello базовые требования, можно создать базовое решение внутри региона Azure.

![Веб-приложение Azure и база данных MySQL в одном регионе Azure][basic-diagram]

Несмотря на то, что это позволяет создать несколько экземпляров веб-приложения hello tooscale сайта, приложения, все, что размещается в центрах обработки данных hello в определенном географическом регионе. Посетители вне этой области может появиться увеличенное время ответа при использовании сайта hello. Если hello центрах обработки данных в этом регионе вышли из строя, поэтому не приложения.

### <a name="multi-region-deployment"></a>Развертывание в нескольких регионах
С помощью Azure [диспетчера трафика][trafficmanager], можно масштабировать сайт WordPress в нескольких географических регионов и предоставить hello же URL-адрес для всех посетителей. Всех посетителей поставляются в через диспетчер трафика и затем перенаправленное tooa область, которая основана на hello конфигурации балансировки нагрузки.

![Веб-приложение Azure, размещенной в нескольких регионах с помощью tooMySQL tooroute CDBR высокий уровень доступности маршрутизатора по регионам][multi-region-diagram]

В каждом регионе hello сайта WordPress по-прежнему будет масштабироваться по нескольким экземплярам веб-приложений, но это масштабирование — конкретных tooa область. Масштабирование регионов с высоким трафиком отличается от масштабирования в регионах с низким трафиком.

tooreplicate и маршрутизации трафика toomultiple базы данных MySQL, можно использовать [маршрутизаторов ClearDB высокого уровня доступности (CDBRs)] [ cleardbscale] (показано слева) или [MySQL кластера перевозчика уровень выпуска (CGE)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Развертывание с хранилищем мультимедиа и кэшированием в нескольких регионах
Если сайт hello принимает передачи или файлы мультимедиа узлов, используйте хранилище больших двоичных объектов Azure. Если вам требуется кэширование, рассмотрите возможность [кэша Redis][rediscache], [Memcache облачных](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), или один из hello другими предложениями кэширования в hello [Хранилища azure](http://azure.microsoft.com/gallery/store/).

![Веб-приложение Azure, размещенное в нескольких регионах с помощью маршрутизатора высокой доступности CDBR для MySQL, с управляемой службой кэша, хранилищем BLOB-объектов и сетью доставки содержимого][performance-diagram]

Хранилище больших двоичных объектов географически распределенных по регионам, по умолчанию, поэтому tooworry о репликации файлов на всех сайтах не нужно. Можно также включить hello Azure [сети доставки содержимого] [ cdn] для хранения больших двоичных объектов, которая распределяет узлы tooend файлы, которые ближе tooyour посетителей.

### <a name="planning"></a>Планирование
#### <a name="additional-requirements"></a>Дополнительные требования
| toodo это... | Используйте это... |
| --- | --- |
| **Отправка или хранение больших файлов** |[Подключаемый модуль WordPress для использования хранилища BLOB-объектов][storageplugin] |
| **Отправка электронной почты** |[SendGrid] [ storesendgrid] и hello [подключаемого модуля WordPress с помощью SendGrid][sendgridplugin] |
| **Личные доменные имена** |[Сопоставление имени личного домена с приложением Azure][customdomain] |
| **HTTPS** |[Защита личного домена приложения с помощью протокола HTTPS][httpscustomdomain] |
| **Предварительная проверка** |[Настройка промежуточных сред для веб-приложений в службе приложений Azure][staging] <p>При перемещении веб-приложения из промежуточной tooproduction также перемещать hello WordPress конфигурации. Убедитесь, что все параметры обновленные toohello требования для производственного приложения перед перемещением tooproduction hello промежуточное приложение.</p> |
| **Мониторинг и устранение неполадок** |[Включение ведения журнала диагностики для веб-приложений в службе приложений Azure][log] и [Мониторинг приложений в службе приложений Azure][monitor] |
| **Развертывание сайта** |[Развертывание приложения в службе приложений Azure][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Доступность и аварийное восстановление
| toodo это... | Используйте это... |
| --- | --- |
| **Сайты балансировки нагрузки** или **геораспределенные сайты** |[Что такое диспетчер трафика][trafficmanager] |
| **Архивация и восстановление** |[Архивация приложения в Azure][backup] и [Восстановление приложения в Azure][restore] |

#### <a name="performance"></a>Производительность
Производительность в облаке hello достигается в основном через кэширование и масштабирования. Тем не менее следует рассматривать hello памяти, пропускной способности и другие атрибуты размещения веб-приложений.

| toodo это... | Используйте это... |
| --- | --- |
| **Общая информация о возможностях экземпляра службы приложений** |[Информация о ценах, в том числе о возможностях уровней служб приложений][websitepricing] |
| **Ресурсы кэша** |[Кэш redis][rediscache], [Memcache облачных](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), или один из hello другими предложениями кэширования в hello [хранилища Azure](/gallery/store/) |
| **Масштабирование приложения** |[Масштабируйте веб-приложение в службе приложений Azure][websitescale] и [используйте высокодоступную маршрутизацию ClearDB][cleardbscale]. Если выбрать toohost и управления установкой MySQL, следует рассмотреть [CGE кластер MySQL] [ cge] для масштабного развертывания. |

#### <a name="migration"></a>Миграция
Существует два метода toomigrate существующего сайта WordPress tooAzure службы приложений:

* **[Экспорт WordPress][export]**: этот метод экспортирует содержимое hello блога. Затем можно импортировать hello содержимого tooa нового WordPress сайта в службе приложений Azure с помощью hello [подключаемого модуля WordPress импортера][import].

  > [!NOTE]
  > Хотя этот процесс позволяет переносить содержимое, но подключаемые модули, темы или другие настройки не переносятся. Необходимо установить эти компоненты повторно вручную.
  >
  >
* **Перенос параметров вручную**: [резервное копирование сайта] [ wordpressbackup] и [базы данных][wordpressdbbackup]и затем восстановить его вручную tooa веб-приложения в Azure Службы приложений и связанная база данных MySQL. Этот метод является полезным toomigrate большой объем настроек сайтов, так как позволяет избежать трудоемкость hello установки подключаемых модулей, темы и другие настройки вручную.

## <a name="step-by-step-instructions"></a>Пошаговые инструкции
### <a name="create-a-wordpress-site"></a>Создание сайта WordPress
1. Используйте hello [Azure Marketplace] [ cdbnstore] toocreate базы данных MySQL размера hello, определенных в hello [архитектуры и планирование](#planning) раздела hello области или области где будет размещаться веб-узла.
2. Следуйте указаниям hello [создать WordPress веб-приложения в службе приложений Azure] [ createwordpress] toocreate WordPress веб-приложения. При создании веб-приложения hello, выберите **использовать существующую базу данных MySQL**, а затем выберите hello базы данных, созданный на шаге 1.

Если вы выполняете миграцию существующего сайта WordPress, см. раздел [перенести существующие tooAzure сайта WordPress](#Migrate-an-existing-WordPress-site-to-Azure) после создания нового веб-приложения.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>Миграция существующих tooAzure сайта WordPress
Как упоминалось в hello [архитектуры и планирование](#planning) статьи, существует два способа toomigrate сайта WordPress:

* **Экспорта и импорта** для сайтов, не имеющими много настройки или просто место toomove hello содержимого.
* **Используйте резервное копирование и восстановление** для сайтов с большим настройки место toomove все данные.

Используйте один из следующих разделов toomigrate hello веб-узла.

#### <a name="hello-export-and-import-method"></a>Здравствуйте, экспорта и импорта
1. Используйте [Экспорт WordPress] [ export] tooexport существующего сайта.
2. Создание веб-приложения с помощью действия hello в hello [создать сайт WordPress](#Create-a-new-WordPress-site) раздела.
3. Войдите на сайт WordPress tooyour на hello [портал Azure][mgmtportal]и нажмите кнопку **подключаемые модули** > **добавить новое**. Поиск и установка hello **импорта WordPress** подключаемого модуля.
4. После установки hello подключаемого модуля WordPress импорта, нажмите кнопку **средства** > **импорта**, а затем нажмите кнопку **WordPress** toouse hello подключаемого модуля WordPress импорта.
5. На hello **импорта WordPress** щелкните **выбрать файл**. Найдите файл WXR hello, который был экспортирован из существующего сайта WordPress и щелкните **передача файла и импорт**.
6. Нажмите кнопку **Submit**(Отправить). Появится запрос, hello Импорт успешно выполнен.
7. После выполнения этих действий перезапустить сайт из его **службы приложений** колонки в hello [портал Azure][mgmtportal].

После импорта узла hello, может потребоваться hello tooperform следующие параметры tooenable действия, которые не находятся в файле импорта hello.

| Если вы использовали... | Процедура |
| --- | --- |
| **Постоянные ссылки** |Hello WordPress мониторинга hello нового узла, щелкните **параметры** > **постоянных**и затем обновить структуру постоянных hello. |
| **Ссылки на изображения и мультимедиа** |tooupdate ссылки toohello новое расположение, используйте hello [Velvet синего обновить URL-адреса, подключаемый модуль][velvet], поиска и замены инструмент, либо вручную обновить ссылки hello в базе данных. |
| **Темы** |Go слишком**внешний вид** > **темы**и при необходимости обновите темы сайта hello. |
| **Меню** |Тема поддерживает меню, ссылки tooyour Домашняя страница может еще hello старого подкаталог, в которых. Go слишком**внешний вид** > **меню**, а затем обновлять их. |

#### <a name="hello-backup-and-restore-method"></a>Здравствуйте, резервного копирования и восстановления
1. Создайте резервную копию вашей существующей WordPress сайта, используя сведения о hello в [резервные копии WordPress][wordpressbackup].
2. Резервное копирование существующей базы данных, используя сведения о hello в [резервную копию базы данных][wordpressdbbackup].
3. Создать базу данных и восстановить hello.

   1. Приобрести новую базу данных из hello [Azure Marketplace][cdbnstore], или настроить базу данных MySQL на [Windows] [ mysqlwindows] или [Linux ] [ mysqllinux] виртуальной машины.
   2. Использование клиента MySQL как [MySQL Workbench] [ workbench] tooconnect toohello новые базы данных и импорт WordPress базы данных.
   3. Обновить hello базы данных toochange hello домена записи tooyour новые службы приложений Azure домен, например, mywordpress.azurewebsites.net. Используйте hello [для поиска и замены для скрипта базы данных WordPress] [ searchandreplace] toosafely изменение всех экземпляров.
4. Создание веб-приложения в hello портал Azure и публикация резервного копирования WordPress hello.

   1. веб-приложения с базы данных, в hello toocreate [портал Azure][mgmtportal], нажмите кнопку **New** > **Интернет + мобильные устройства**  >  **Azure Marketplace** > **веб-приложений** > **веб-приложение + SQL** (или **веб-приложение + MySQL**) > **Создания**. Настройте параметры toocreate все необходимые hello пустой веб-приложение.
   2. В резервную копию WordPress, найдите hello **wp-config.php** и откройте его в редакторе. Замените следующие операции с hello сведения для новой базы данных MySQL hello:

      * **Db_name**: hello имя пользователя базы данных hello.
      * **DB_USER**: hello пользователя имя, используемое tooaccess hello базы данных.
      * **DB_PASSWORD**: hello пароль пользователя.

        После изменения этих записей, сохраните и закройте hello **wp-config.php** файл.
   3. Используйте hello [развертывание веб-приложения в службе приложений Azure] [ deploy] сведения tooenable hello метода для развертывания требуется toouse и затем развернуть WordPress tooyour резервного копирования веб-приложение в службе приложений Azure.
5. После развертывания сайта WordPress hello должен быть новый сайт будет tooaccess hello (как веб-приложение служб приложений) с помощью hello *. azurewebsite.net URL-адрес сайта hello.

### <a name="configure-your-site"></a>Настройка сайта
После создания или миграции сайта WordPress hello используйте следующие сведения о производительности tooimprove hello или включить дополнительные функции.

| toodo это... | Используйте это... |
| --- | --- |
| **Установка режима плана службы приложений, размера и включение масштабирования** |[Увеличение масштаба приложения в Azure][websitescale] |
| **Включение постоянных подключений базы данных** |По умолчанию WordPress не использует постоянного подключения к базе данных которых может привести к регулированию после нескольких подключений вашей базы данных toobecome соединения toohello. tooenable постоянные подключения, установить hello [подключаемый модуль адаптера постоянные подключения](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Повышение производительности** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Отключить hello ARR cookie</a>, который может повысить производительность при запуске WordPress на нескольких экземплярах веб-приложений.</p></li><li><p>Включите кэширование. Можно использовать <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">кэша Redis</a> (preview) hello <a href="https://wordpress.org/plugins/redis-object-cache/">подключаемого модуля WordPress объекта кэша Redis</a>, или можно использовать один из hello другими предложениями кэширования из hello <a href="/gallery/store/">хранилища Azure</a>.</p></li><li><p>[Ускорение работы WordPress с помощью Wincache.](https://wordpress.org/plugins/w3-total-cache/) Wincache по умолчанию включен для веб-приложений. При совместном использовании WinCache и динамического кэша, отключить кэш файлов WinCache, но оставьте пользователя hello и кэш сеанса включен. tooturn файл кэширования, в файл .ini системного уровня, установите hello следующие значения:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Масштабируйте веб-приложение в службе приложений Azure][websitescale] и используйте <a href="http://www.cleardb.com/developers/cdbr/introduction">маршрутизацию высокой доступности ClearDB</a> или <a href="http://www.mysql.com/products/cluster/">MySQL Cluster CGE</a>.</p></li></ul> |
| **Использование больших двоичных объектов для хранения данных** |<ol><li><p>[Создайте учетную запись хранения Azure](../storage/common/storage-create-storage-account.md).</p></li><li><p>Узнайте, каким образом слишком[используйте hello сеть распространения содержимого](../cdn/cdn-create-new-endpoint.md) toogeo-распределение данных, хранящихся в больших двоичных объектов.</p></li><li><p>Установка и настройка hello <a href="https://wordpress.org/plugins/windows-azure-storage/">хранилища Azure для подключаемого модуля WordPress</a>.</p><p>Подробные сведения установке и настройке для hello подключаемого модуля, в разделе hello <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">руководство пользователя по</a>.</p> </li></ol> |
| **Включение электронной почты** |Включить <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> с использованием hello хранилища Azure. Установка hello <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">SendGrid подключаемый модуль</a> для WordPress. |
| **Настройка пользовательского имени домена** |[Сопоставление имени личного домена с приложением Azure][customdomain]. |
| **Включение HTTPS для личного доменного имени** |[Защита личного домена приложения с помощью протокола HTTPS][httpscustomdomain]. |
| **Распределение нагрузки или географическое распределение сайта** |[Что такое диспетчер трафика][trafficmanager]. Если вы используете пользовательский домен, см. раздел [настроить пользовательское доменное имя в службе приложений Azure] [ customdomain] сведения о том, как toouse диспетчера трафика с помощью пользовательских доменных имен. |
| **Включение автоматически создаваемых резервных копий** |[Архивация приложения в Azure][backup] |
| **Включение ведения журналов диагностики** |[Включение ведения журнала диагностики для веб-приложений в службе приложений Azure][log] |

## <a name="next-steps"></a>Дальнейшие действия
* [Оптимизация WordPress](http://codex.wordpress.org/WordPress_Optimization)
* [Преобразовать toomultisite WordPress в службе приложений Azure](web-sites-php-convert-wordpress-multisite.md)
* [Мастер обновления ClearDB для Azure](http://www.cleardb.com/store/azure/upgrade)
* [Размещение WordPress в подпапке веб-приложения в службе приложений Azure](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Step-By-Step: Create a WordPress Site using Windows Azure](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx) (Пошаговое руководство. Создание сайта WordPress с помощью Azure)
* [Размещение существующего блога WordPress в Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Включение постоянных ссылок в WordPress](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Как toomigrate и запустите блога WordPress на службе приложений Azure](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Как toorun WordPress в службе приложений Azure для освобождения](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress on Windows Azure in 2 Minutes or Less](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/) (WordPress в Azure за 2 минуты или меньше)
* [Перемещение tooAzure WordPress блога — часть 1: создание блог WordPress в Azure](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Перемещение tooAzure WordPress блога — часть 2: передача содержимого](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Перемещение tooAzure WordPress блога — часть 3: Настройка пользовательского домена](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Перемещение tooAzure WordPress блога — часть 4: довольно постоянных и правил переопределения URL-адресов](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Перемещение tooAzure WordPress блога — часть 5: перемещение из корневого элемента toohello вложенной папки](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Как tooset копирование WordPress веб-приложения в учетной записи Azure](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Поддержка WordPress в Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Советы по WordPress в Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Tooget к работе со службой приложения Azure, прежде чем выполнить вход для учетной записи Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Не требуется никаких кредитных карт и обязательств.
>
>

## <a name="whats-changed"></a>Изменения
Руководство по toohello изменений из tooApp веб-сайтов службы, см. [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
