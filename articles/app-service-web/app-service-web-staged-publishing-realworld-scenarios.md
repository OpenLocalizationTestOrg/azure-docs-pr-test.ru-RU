---
title: "сред DevOps aaaUse эффективно для веб-приложения | Документы Microsoft"
description: "Узнайте, как слоты развертывания toouse tooset вверх и управление ими несколько сред разработки приложения"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>Эффективное использование сред разработки и операций для веб-приложений
В этой статье показано, как tooset и управление ею развертывания веб-приложений, несколько версий приложения, которые в средах разработки, промежуточной, контроль качества (QA) и производства. Каждая версия приложения может рассматриваться как среда разработки для конкретной цели hello процесс развертывания. Например разработчики могут использовать hello QA tootest среды hello качество приложения hello, прежде чем они push tooproduction изменения hello.
Несколько сред разработки может быть сложной задачей, так как требуется код tootrack управления ресурсами (вычислений, веб-приложения, базы данных, кэша, т. д.) и развернуть код во всех средах.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Настройка непроизводственной среды (для подготовки, разработки, контроля качества)
После работы рабочего веб-приложения hello следующим шагом является toocreate нерабочей среде. toouse слотов развертывания, убедитесь в том, что выполняется в режиме плана Standard или Premium службы приложений Azure hello. Слоты развертывания являются динамическими веб-приложениями с собственными именами узлов. Приложение веб-содержимого и конфигурации элементов можно переключать между двумя слотами развертывания, включая производственный слот hello. При развертывании слот развертывания tooa вашего приложения вы получаете hello следующие преимущества:

- Вы можете проверить изменения tooa веб-приложения в промежуточном слоте развертывания до замены приложение hello hello производственный слот.
- При развертывании сначала слот tooa web app и переключить его в рабочую среду, все экземпляры hello слот активированию перед идет переключение в рабочую среду. Это сокращает время простоя при развертывании веб-приложения. Hello перенаправление трафика не вызывает затруднений, а запросы не теряются из-за tooswap операций. tooautomate всего рабочего процесса, настройте [автоматическое переключение](web-sites-staged-publishing.md#configure-auto-swap) при предварительной swap проверку не требуется.
- После переключения слота hello, теперь имеет hello ранее промежуточная веб-приложение имеет hello предыдущего рабочего веб-приложения. Если изменения hello в производственный слот hello не соответствуют ожидаемым вы, вы можете выполнить hello же замены немедленно tooget вашей «последнего хорошо известных» назад web app.

tooset копирование промежуточном слоте развертывания, в разделе [Настройка промежуточных сред для веб-приложений в службе приложений Azure](web-sites-staged-publishing.md). Каждая среда должна включать собственный набор ресурсов. Например, если веб-приложение использует базу данных, рабочая и промежуточная версии веб-приложения должны использовать разные базы данных. Добавление промежуточных ресурсы среды разработки, такие как базы данных хранилища или кэш tooset промежуточной среды разработки.

## <a name="examples-of-using-multiple-development-environments"></a>Примеры использования нескольких сред разработки
Все проекты разработки необходимо вести в рамках системы управления исходным кодом как минимум с двумя средами (средой разработки и рабочей). При использовании системы управления содержимым (средах CMS), исполняющие среды, т. д., приложение hello могут не поддерживать этот сценарий без настройки. Для некоторых из наиболее популярных платформ hello, которые рассматриваются в следующих разделах hello верно этой возможности. Большое количество вопросов поступать toomind при работе с CMS-платформы, такие как:

- Как вы разбивает содержимое hello в разных средах?
- Какие файлы можно менять, не опасаясь, что изменение потребует обновления версии платформы?
- Как управлять конфигурацией каждой среды?
- Как управлять версии обновлений для модулей, подключаемые модули и hello core framework?

Существует много способов tooset несколько среды для проекта. Hello следующих примерах один метод для каждого из соответствующих приложений.

### <a name="wordpress"></a>WordPress
В этом разделе вы узнаете, как tooset копирование рабочего процесса развертывания с помощью слотов для WordPress. WordPress, как и большинство решений для управления контентом, по умолчанию не поддерживает работу с несколькими средами без настройки. компонент веб-приложения Hello службе приложений Azure имеет ряд возможностей, которые позволяют легко toostore параметры конфигурации извне вашего кода.

1. Прежде чем создать промежуточный слот, настройте код вашего приложения toosupport несколько сред. toosupport нескольких средах в WordPress, необходим tooedit `wp-config.php` на локальной разработки веб-приложения и добавьте следующий код в начало файла с hello hello hello. Этот процесс позволит toopick hello правильный конфигурации приложения в зависимости от выбранной среды hello.

    ```
    // Support multiple environments
    // set hello config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. Создайте папку в корне приложения web вызывается `config`и добавить hello `wp-config.azure.php` и `wp-config.local.php` файлы, которые представляют среды Azure и локальной среде соответственно.

3. Скопируйте следующие hello в `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    Установка hello ключей безопасности, как показано в предыдущем примере кода hello можно помощь tooprevent веб-приложения в вредоносной атаки на время, поэтому желательно использовать уникальные значения. Если требуется строка hello toogenerate для ключей безопасности, упомянутые в коде hello, вы можете [автоматического генератор перейдите toohello](https://api.wordpress.org/secret-key/1.1/salt) toocreate новые пары ключей и значений.

4. Копирования hello следующий код в `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a>Использование относительных путей
Один последний самое tooconfigure в приложение hello WordPress — относительные пути. WordPress хранит сведения о URL-адрес в базе данных hello. Это хранилище усложняет перемещения содержимого из одной среды tooanother. Необходимо настроить базу данных tooupdate hello, при переходе из локального toostage или при определенных условиях tooproduction рабочей области. риск hello tooreduce проблем, вызвавших с развертывание базы данных каждый раз при развертывании из одной среды tooanother, используйте hello [относительный корневой ссылки подключаемого модуля](https://wordpress.org/plugins/root-relative-urls/), которую можно установить с помощью администратора WordPress hello панель мониторинга.

Добавить следующие записи tooyour hello `wp-config.php` файла перед hello `That's all, stop editing!` комментария:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Активировать подключаемого модуля hello через hello `Plugins` меню в панели мониторинга администратора WordPress. Сохраните постоянную ссылку на приложение WordPress.

#### <a name="hello-final-wp-configphp-file"></a>Окончательный Hello `wp-config.php` файла
Никакие основные обновления WordPress не будут оказывать влияния на файлы `wp-config.php`, `wp-config.azure.php` и `wp-config.local.php`. Вот как окончательная версия hello `wp-config.php` файла:

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>Настройка промежуточной среды
1. Если уже имеется WordPress веб-приложения, запущенного на подписки Azure, выполнить вход в toohello [портал Azure](http://portal.azure.com), и перейдите на веб-приложение tooyour WordPress. Если у вас нет веб-приложения WordPress, можно создать из hello Azure Marketplace. toolearn более, в разделе [создать WordPress веб-приложения в службе приложений Azure](web-sites-php-web-site-gallery.md).
Нажмите кнопку **параметры** > **слоты развертывания** > **добавить** toocreate слота развертывания с именем hello *этапа*. Слот развертывания имеет другое веб-приложение, общие папки hello ресурсы hello первичного веб-приложения, который вы создали ранее.

    ![Создание промежуточного слота развертывания](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Добавить другую базу данных MySQL, например `wordpress-stage-db`, tooyour группы ресурсов, `wordpressapp-group`.

    ![Добавить группу tooresource базы данных MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Обновление строк соединения hello этап развертывания слот toopoint toohello новой базы данных, `wordpress-stage-db`. Веб-приложения рабочей `wordpressprodapp`и промежуточных веб-приложения `wordpressprodapp-stage`, базы данных должен toodifferent точки.

#### <a name="configure-environment-specific-app-settings"></a>Настройка параметров приложения с учетом конкретной среды
Разработчики могут хранить пары ключ значение строки в Azure как часть сведений о конфигурации hello, вызывается **параметры приложения**, связанную с веб-приложения. Во время выполнения веб-приложения автоматически получать эти значения и сделать их доступными toocode, который выполняется в веб-приложения. Это дает положительный побочный эффект с точки зрения безопасности, так как конфиденциальная информация, например строки подключения к базам данных и пароли, никогда не отображается в виде открытого текста в таких файлах, как `wp-config.php`.

Этот процесс, который описан в следующих абзацах hello, полезно, поскольку он включает изменения в файле и изменения базы данных для приложения hello WordPress:

* обновление версии WordPress;
* добавление, изменение или обновление подключаемых модулей;
* добавление, изменение или обновление тем.

Настройка параметров приложения:

* сведения о базе данных;
* включение и выключение ведения журнала для WordPress.
* параметры безопасности WordPress.

![Параметры приложения для веб-приложения WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Убедитесь, что добавить следующие параметры приложения для гнезда приложения и этап web производственного hello. Обратите внимание, что hello рабочего веб-приложения и промежуточного веб-приложения используют другой базы данных.

1. Очистить hello **параметр слот** флажок для всех параметров настройки hello, за исключением WP_ENV. Этот процесс поменяет hello конфигурации для веб-приложения, содержимое файла и базы данных. Если **параметр слот** — флажок установлен, параметры приложения hello веб-приложения и конфигурации строки соединения будут *не* переместить во всех средах, при выполнении **замены** операции. поэтому любые изменения базы данных не приведут к сбою рабочего веб-приложения.

2. Развертывание с помощью WebMatrix или средств по своему усмотрению, таких как FTP, Git или PhpMyAdmin hello локальной разработки среды web app toohello этап веб-приложения и базы данных.

    ![Диалоговое окно публикации веб-приложения WordPress в WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Перейдите к веб-приложению в промежуточной среде и протестируйте его. Учитывая сценарии, где тема hello hello веб-приложения — toobe обновлен Вот hello промежуточных веб-приложения.

    ![Просмотр промежуточных веб-приложений до переключения слотов](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Если все в порядке, нажмите кнопку hello **замены** кнопку на вашей промежуточного приложения toomove web содержимого toohello рабочую среду. В этом случае замены hello веб-приложения и базы данных hello во всех средах во время каждого **Swap** операции.

    ![Просмотр изменений при переключении для WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Если ваш сценарий должен tooonly принудительной файлы (без обновления базы данных), затем проверьте **параметр слот** для всех hello относящиеся к базе данных *параметры приложения* и *Параметрыстрокиподключения*в hello **параметры веб-приложения** колонки в hello портал Azure, прежде чем сделать hello **замены**. В этом случае параметры DB_NAME, DB_HOST, DB_PASSWORD, DB_USER и строка подключения по умолчанию не должны отображаться при предварительном просмотре изменений перед **переключением**. В настоящее время при заполнении hello **замены** операции hello WordPress веб-приложения будет иметь hello обновляет только файлы.
    >
    >

    Прежде чем делать **замены**, вот hello рабочего WordPress веб-приложения.
    ![Рабочее веб-приложение перед переключением слотов](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    После hello **замены** операции темы hello была обновлена на производственных веб-приложения.

    ![Рабочее веб-приложение после переключения слотов](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. При необходимости обратно tooroll можно перейти web toohello рабочей **параметры приложения**и нажмите кнопку hello **замены** tooswap hello веб-приложения и базы данных из рабочего слота toostaging, нажмите кнопку. Следует помнить, что, если изменения в базе данных входят в состав **замены** операции, а затем развернуть tooyour промежуточных веб-приложения, при очередном hello необходимо toodeploy hello базы данных изменения toohello текущей базы данных для размещения веб-приложения. Hello текущей базы данных может быть hello предыдущей рабочей базы данных или базы данных рабочей области hello.

#### <a name="summary"></a>Сводка
Ниже приведен общий процесс для любого приложения с базой данных:

1. Установите приложение hello в локальной среде.
2. Выбор конфигурации в зависимости от конкретной среды (локальное приложение и веб-приложение Azure).
3. Настройка промежуточной и рабочей сред для веб-приложений.
4. При наличии рабочего приложения, уже работающие в Azure синхронизации рабочей содержимого (файлы или код базы данных) toolocal и промежуточной сред и.
5. Разработка приложения в локальной среде.
6. Поместите производственного веб-приложения или заблокированный режим и синхронизировать содержимое базы данных из рабочих средах toostaging и разработки.
7. Развертывание toohello промежуточной среды и тестирования.
8. Развертывание среды tooproduction.
9. Повтор шагов 4–6.

### <a name="umbraco"></a>Umbraco
В этом разделе вы узнаете, как hello Umbraco CMS использует toodeploy пользовательский модуль в нескольких средах DevOps. В этом примере представлен toomanaging другой подход несколько сред разработки.

[Umbraco CMS](http://umbraco.com/) — это популярное среди разработчиков CMS-решение на основе .NET, Он предоставляет hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy модуль tooproduction сред разработки toostaging. Вы можете легко создать локальную среду разработки для веб-приложения Umbraco CMS с помощью Visual Studio или WebMatrix.

- [Создание веб-приложения Umbraco с помощью Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Создание веб-приложения Umbraco с помощью WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Не забывайте tooremove hello `install` папку приложения и никогда не отправлять toostage или рабочей веб-приложений. В этом руководстве используется WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Настройка промежуточной среды
1. Создайте слот развертывания, как упоминалось ранее, для hello Umbraco CMS веб-приложения, при условии, что уже имеется веб-приложение Umbraco CMS и работает. Если этого не сделать, можно создать один из hello Marketplace.
2. Обновление строки подключения hello для вашей рабочей области развертывания слот toopoint toohello новый **umbraco рабочей области db** базы данных. Ваш рабочего веб-приложения (umbraositecms-1) и промежуточный веб-приложения (этап umbracositecms 1) *должен* toodifferent точки баз данных.

    ![Обновление строки подключения для промежуточного веб-приложения с новой промежуточной базой данных](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Нажмите кнопку **параметры получения публикации** для слота развертывания hello **этап**. Этот процесс будет загрузить файл параметров публикации, в которой хранятся все сведения о hello, что Visual Studio или в WebMatrix требует toopublish приложения hello локальная разработка web app toohello веб-приложение Azure.

    ![Получение публикации равным hello промежуточных веб-приложения](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Откройте веб-приложение в локальной среде разработки WebMatrix или Visual Studio. В этом руководстве используется WebMatrix. Во-первых, требуется tooimport hello параметры публикации для размещения веб-приложения.

    ![Импорт параметров публикации в Umbraco с помощью Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Проверьте изменения в диалоговое окно «hello» и развернуть локальный веб-приложения tooyour Azure web приложение, *umbracositecms 1 рабочей области*. При развертывании файлов напрямую промежуточной tooyour веб-приложения, исключаются файлы в hello `~/app_data/TEMP/` папку, так как эти файлы будут созданы заново, при первом веб-приложения hello этапа работы. Также следует опустить hello `~/app_data/umbraco.config` файл, который будет также создан повторно.

    ![Просмотр изменений публикации в WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. После успешной публикации hello Umbraco локального web app toohello промежуточной веб-приложения, Обзор tooyour промежуточного веб-приложения и запустить несколько тестов toorule проблемы.

#### <a name="set-up-hello-courier2-deployment-module"></a>Настройка модуля развертывания Courier2 hello
С hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) модуль, можно просто щелкнуть toopush содержимого, стилей и разработки модулей из промежуточного web app tooa рабочего веб-приложения. При этом уменьшается hello риска нарушения производственного веб-приложения при развертывании обновления.
Приобрести лицензию для Courier2 hello `*.azurewebsites.net` домен и личный домен (например http://abc.com). После приобретения лицензии hello hello месте загруженные лицензии (. Файл: лицензионное соглашение) в hello `bin` папки.

![Перенос файла лицензии в папку bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Загрузить пакет hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Вход tooyour этап веб-приложения, например http://umbracocms-site-stage.azurewebsites.net/umbraco щелкните hello **разработчика** меню, а затем нажмите **пакетов** > **установки локального пакета**.

    ![Установщик пакета Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Отправьте пакет hello Courier2 с помощью установщика hello.

    ![Загрузка пакета модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. пакет tooconfigure hello, требуется файл courier.config hello tooupdate под hello **Config** папки веб-приложения.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. В разделе `<repositories>`, введите hello производственного сайта URL-адрес и сведения о пользователях.
    При использовании поставщика членства Umbraco по умолчанию hello, затем добавьте идентификатор пользователя администрирования hello hello в hello &lt;пользователя&gt; раздела.
    При использовании пользовательского поставщика членства Umbraco используйте `<login>`,`<password>` в hello Courier2 модуль tooconnect toohello рабочего сайта.
    Дополнительные сведения [документации hello hello Courier2 модуль](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Аналогичным образом установить модуль Courier2 hello на на рабочем сайте и настройте его toopoint toohello этап веб-приложения в своем файле соответствующих courier.config, как показано ниже.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Нажмите кнопку hello **Courier2** вкладке hello Umbraco CMS панели мониторинга приложения и нажмите кнопку **расположения**. Вы увидите имя репозитория hello, как упоминалось в `courier.config`. Сделайте это в веб-приложениях в рабочей и промежуточной среде.

    ![Просмотр целевого репозитория веб-приложения](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. содержимое toodeploy из промежуточного сайта toohello рабочего сайта, hello go слишком**содержимого**и выберите существующую страницу или создать новую страницу. Можно будет выбрать существующую страницу из Мое веб-приложение, где hello заголовок страницы приветствия **начало работы — новый**, а затем нажмите кнопку **сохранить и опубликовать**.

    ![Изменение заголовка страницы и публикация](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Щелкните правой кнопкой мыши hello изменить страницы tooview все параметры hello. Нажмите кнопку **Courier** tooopen hello **развертывания** диалоговое окно. Нажмите кнопку **развернуть** tooinitiate развертывания.

    ![Диалоговое окно развертывания модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Просмотрите изменения hello и нажмите кнопку **Продолжить**.

    ![Просмотр изменений в диалоговом окне развертывания модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    Журнал развертывания Hello показывает успешность развертывания hello.

     ![Просмотр журналов развертывания из модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Обзор toosee приложения web вашей рабочей среде, если hello изменения будут отражены.

     ![Переход к рабочему веб-приложению](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

Дополнительные сведения о как toouse курьера, просмотрите hello документации toolearn.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>Как tooupgrade hello версии Umbraco CMS
Будет Courier не помогающие выполнить обновление из одной версии tooanother Umbraco CMS. При обновлении версии Umbraco CMS, необходимо отслеживать проблемы совместимости с пользовательские модули или модули из партнеров, hello Umbraco основных библиотек. Ниже приведены рекомендации.

* Всегда создавайте резервную копию веб-приложения и базы данных перед обновлением. На веб-приложений в Azure можно настроить автоматическое создание резервных копий для веб-сайтов с помощью функции резервного копирования hello и восстановить сайт, при необходимости с помощью функции восстановления hello. Дополнительные сведения см. в разделе [как tooback копирование веб-приложения](web-sites-backup.md) и [как toorestore веб-приложения](web-sites-restore.md).
* Проверьте совместим с версией hello, которые вы осуществили обновление для пакетов от партнеров. Страница загрузки пакета hello, просмотрите hello совместимость проекта с версией Umbraco CMS.

Дополнительные сведения о том, как tooupgrade веб-приложения локально, [см. руководство по обновлению общие hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

После обновления локальных сайтов публикации toohello изменения hello промежуточных веб-приложения. Протестируйте приложение. Если все в порядке, используйте hello **замены** кнопку tooswap промежуточного сайта toohello производственного веб-приложения. При использовании hello **замены** операции, можно просмотреть изменения hello, которые будут затронуты в конфигурации веб-приложения. Это **замены** операции меняет hello веб-приложений и баз данных. После hello **замены**hello производственного веб-приложения будет toohello точки umbraco рабочей области базы данных база данных и hello промежуточного веб-приложение будет tooumbraco точки одной рабочей базы данных база данных.

![Предварительный просмотр перед операцией перемещения при развертывании Umbraco CMS](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Ниже приведены преимущества обмен hello веб-приложения и базы данных hello.

* Можно выполнить откат предыдущей версии веб-приложения с другим toohello **замены** при наличии проблемы с приложением.
* Для обновления требуется toodeploy файлов и баз данных из промежуточных web app toohello рабочего веб-приложения hello и базы данных. Развертывание файлов и базы данных связано с большим количеством рисков. С помощью hello **замены** функция слотов, можно сократить время простоя во время обновления и уменьшить риск hello сбоев, которые могут возникнуть при развертывании изменений.
* Можно сделать **A / B-тестирования** с помощью hello [тестирования в рабочей среде](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) компонентов.

В этом примере представлены hello гибкость hello платформы, где можно создать пользовательские модули аналогичные tooUmbraco Courier модуля toomanage развертывания в средах.

## <a name="references"></a>Ссылки
[Гибкая разработка программного обеспечения с помощью службы приложений Azure.](app-service-agile-software-development.md)

[Настройка промежуточных сред для веб-приложений в службе приложений Azure](web-sites-staged-publishing.md)

[Как tooblock веб-доступа к рабочей toonon слоты развертывания](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
