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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="3a560-103">Эффективное использование сред разработки и операций для веб-приложений</span><span class="sxs-lookup"><span data-stu-id="3a560-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="3a560-104">В этой статье показано, как tooset и управление ею развертывания веб-приложений, несколько версий приложения, которые в средах разработки, промежуточной, контроль качества (QA) и производства.</span><span class="sxs-lookup"><span data-stu-id="3a560-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="3a560-105">Каждая версия приложения может рассматриваться как среда разработки для конкретной цели hello процесс развертывания.</span><span class="sxs-lookup"><span data-stu-id="3a560-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="3a560-106">Например разработчики могут использовать hello QA tootest среды hello качество приложения hello, прежде чем они push tooproduction изменения hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="3a560-107">Несколько сред разработки может быть сложной задачей, так как требуется код tootrack управления ресурсами (вычислений, веб-приложения, базы данных, кэша, т. д.) и развернуть код во всех средах.</span><span class="sxs-lookup"><span data-stu-id="3a560-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="3a560-108">Настройка непроизводственной среды (для подготовки, разработки, контроля качества)</span><span class="sxs-lookup"><span data-stu-id="3a560-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="3a560-109">После работы рабочего веб-приложения hello следующим шагом является toocreate нерабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3a560-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="3a560-110">toouse слотов развертывания, убедитесь в том, что выполняется в режиме плана Standard или Premium службы приложений Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="3a560-111">Слоты развертывания являются динамическими веб-приложениями с собственными именами узлов.</span><span class="sxs-lookup"><span data-stu-id="3a560-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="3a560-112">Приложение веб-содержимого и конфигурации элементов можно переключать между двумя слотами развертывания, включая производственный слот hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="3a560-113">При развертывании слот развертывания tooa вашего приложения вы получаете hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3a560-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="3a560-114">Вы можете проверить изменения tooa веб-приложения в промежуточном слоте развертывания до замены приложение hello hello производственный слот.</span><span class="sxs-lookup"><span data-stu-id="3a560-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="3a560-115">При развертывании сначала слот tooa web app и переключить его в рабочую среду, все экземпляры hello слот активированию перед идет переключение в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="3a560-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="3a560-116">Это сокращает время простоя при развертывании веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="3a560-117">Hello перенаправление трафика не вызывает затруднений, а запросы не теряются из-за tooswap операций.</span><span class="sxs-lookup"><span data-stu-id="3a560-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="3a560-118">tooautomate всего рабочего процесса, настройте [автоматическое переключение](web-sites-staged-publishing.md#configure-auto-swap) при предварительной swap проверку не требуется.</span><span class="sxs-lookup"><span data-stu-id="3a560-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="3a560-119">После переключения слота hello, теперь имеет hello ранее промежуточная веб-приложение имеет hello предыдущего рабочего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="3a560-120">Если изменения hello в производственный слот hello не соответствуют ожидаемым вы, вы можете выполнить hello же замены немедленно tooget вашей «последнего хорошо известных» назад web app.</span><span class="sxs-lookup"><span data-stu-id="3a560-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="3a560-121">tooset копирование промежуточном слоте развертывания, в разделе [Настройка промежуточных сред для веб-приложений в службе приложений Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3a560-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="3a560-122">Каждая среда должна включать собственный набор ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3a560-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="3a560-123">Например, если веб-приложение использует базу данных, рабочая и промежуточная версии веб-приложения должны использовать разные базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a560-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="3a560-124">Добавление промежуточных ресурсы среды разработки, такие как базы данных хранилища или кэш tooset промежуточной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="3a560-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="3a560-125">Примеры использования нескольких сред разработки</span><span class="sxs-lookup"><span data-stu-id="3a560-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="3a560-126">Все проекты разработки необходимо вести в рамках системы управления исходным кодом как минимум с двумя средами (средой разработки и рабочей).</span><span class="sxs-lookup"><span data-stu-id="3a560-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="3a560-127">При использовании системы управления содержимым (средах CMS), исполняющие среды, т. д., приложение hello могут не поддерживать этот сценарий без настройки.</span><span class="sxs-lookup"><span data-stu-id="3a560-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="3a560-128">Для некоторых из наиболее популярных платформ hello, которые рассматриваются в следующих разделах hello верно этой возможности.</span><span class="sxs-lookup"><span data-stu-id="3a560-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="3a560-129">Большое количество вопросов поступать toomind при работе с CMS-платформы, такие как:</span><span class="sxs-lookup"><span data-stu-id="3a560-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="3a560-130">Как вы разбивает содержимое hello в разных средах?</span><span class="sxs-lookup"><span data-stu-id="3a560-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="3a560-131">Какие файлы можно менять, не опасаясь, что изменение потребует обновления версии платформы?</span><span class="sxs-lookup"><span data-stu-id="3a560-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="3a560-132">Как управлять конфигурацией каждой среды?</span><span class="sxs-lookup"><span data-stu-id="3a560-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="3a560-133">Как управлять версии обновлений для модулей, подключаемые модули и hello core framework?</span><span class="sxs-lookup"><span data-stu-id="3a560-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="3a560-134">Существует много способов tooset несколько среды для проекта.</span><span class="sxs-lookup"><span data-stu-id="3a560-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="3a560-135">Hello следующих примерах один метод для каждого из соответствующих приложений.</span><span class="sxs-lookup"><span data-stu-id="3a560-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="3a560-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="3a560-136">WordPress</span></span>
<span data-ttu-id="3a560-137">В этом разделе вы узнаете, как tooset копирование рабочего процесса развертывания с помощью слотов для WordPress.</span><span class="sxs-lookup"><span data-stu-id="3a560-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="3a560-138">WordPress, как и большинство решений для управления контентом, по умолчанию не поддерживает работу с несколькими средами без настройки.</span><span class="sxs-lookup"><span data-stu-id="3a560-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="3a560-139">компонент веб-приложения Hello службе приложений Azure имеет ряд возможностей, которые позволяют легко toostore параметры конфигурации извне вашего кода.</span><span class="sxs-lookup"><span data-stu-id="3a560-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="3a560-140">Прежде чем создать промежуточный слот, настройте код вашего приложения toosupport несколько сред.</span><span class="sxs-lookup"><span data-stu-id="3a560-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="3a560-141">toosupport нескольких средах в WordPress, необходим tooedit `wp-config.php` на локальной разработки веб-приложения и добавьте следующий код в начало файла с hello hello hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="3a560-142">Этот процесс позволит toopick hello правильный конфигурации приложения в зависимости от выбранной среды hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

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

2. <span data-ttu-id="3a560-143">Создайте папку в корне приложения web вызывается `config`и добавить hello `wp-config.azure.php` и `wp-config.local.php` файлы, которые представляют среды Azure и локальной среде соответственно.</span><span class="sxs-lookup"><span data-stu-id="3a560-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="3a560-144">Скопируйте следующие hello в `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="3a560-144">Copy hello following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="3a560-145">Установка hello ключей безопасности, как показано в предыдущем примере кода hello можно помощь tooprevent веб-приложения в вредоносной атаки на время, поэтому желательно использовать уникальные значения.</span><span class="sxs-lookup"><span data-stu-id="3a560-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="3a560-146">Если требуется строка hello toogenerate для ключей безопасности, упомянутые в коде hello, вы можете [автоматического генератор перейдите toohello](https://api.wordpress.org/secret-key/1.1/salt) toocreate новые пары ключей и значений.</span><span class="sxs-lookup"><span data-stu-id="3a560-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="3a560-147">Копирования hello следующий код в `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="3a560-147">Copy hello following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="3a560-148">Использование относительных путей</span><span class="sxs-lookup"><span data-stu-id="3a560-148">Use relative paths</span></span>
<span data-ttu-id="3a560-149">Один последний самое tooconfigure в приложение hello WordPress — относительные пути.</span><span class="sxs-lookup"><span data-stu-id="3a560-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="3a560-150">WordPress хранит сведения о URL-адрес в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="3a560-151">Это хранилище усложняет перемещения содержимого из одной среды tooanother.</span><span class="sxs-lookup"><span data-stu-id="3a560-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="3a560-152">Необходимо настроить базу данных tooupdate hello, при переходе из локального toostage или при определенных условиях tooproduction рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3a560-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="3a560-153">риск hello tooreduce проблем, вызвавших с развертывание базы данных каждый раз при развертывании из одной среды tooanother, используйте hello [относительный корневой ссылки подключаемого модуля](https://wordpress.org/plugins/root-relative-urls/), которую можно установить с помощью администратора WordPress hello панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="3a560-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="3a560-154">Добавить следующие записи tooyour hello `wp-config.php` файла перед hello `That's all, stop editing!` комментария:</span><span class="sxs-lookup"><span data-stu-id="3a560-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="3a560-155">Активировать подключаемого модуля hello через hello `Plugins` меню в панели мониторинга администратора WordPress.</span><span class="sxs-lookup"><span data-stu-id="3a560-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="3a560-156">Сохраните постоянную ссылку на приложение WordPress.</span><span class="sxs-lookup"><span data-stu-id="3a560-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="3a560-157">Окончательный Hello `wp-config.php` файла</span><span class="sxs-lookup"><span data-stu-id="3a560-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="3a560-158">Никакие основные обновления WordPress не будут оказывать влияния на файлы `wp-config.php`, `wp-config.azure.php` и `wp-config.local.php`.</span><span class="sxs-lookup"><span data-stu-id="3a560-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="3a560-159">Вот как окончательная версия hello `wp-config.php` файла:</span><span class="sxs-lookup"><span data-stu-id="3a560-159">Here's a final version of hello `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="3a560-160">Настройка промежуточной среды</span><span class="sxs-lookup"><span data-stu-id="3a560-160">Set up a staging environment</span></span>
1. <span data-ttu-id="3a560-161">Если уже имеется WordPress веб-приложения, запущенного на подписки Azure, выполнить вход в toohello [портал Azure](http://portal.azure.com), и перейдите на веб-приложение tooyour WordPress.</span><span class="sxs-lookup"><span data-stu-id="3a560-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="3a560-162">Если у вас нет веб-приложения WordPress, можно создать из hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3a560-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="3a560-163">toolearn более, в разделе [создать WordPress веб-приложения в службе приложений Azure](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="3a560-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="3a560-164">Нажмите кнопку **параметры** > **слоты развертывания** > **добавить** toocreate слота развертывания с именем hello *этапа*.</span><span class="sxs-lookup"><span data-stu-id="3a560-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="3a560-165">Слот развертывания имеет другое веб-приложение, общие папки hello ресурсы hello первичного веб-приложения, который вы создали ранее.</span><span class="sxs-lookup"><span data-stu-id="3a560-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![Создание промежуточного слота развертывания](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="3a560-167">Добавить другую базу данных MySQL, например `wordpress-stage-db`, tooyour группы ресурсов, `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="3a560-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![Добавить группу tooresource базы данных MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="3a560-169">Обновление строк соединения hello этап развертывания слот toopoint toohello новой базы данных, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="3a560-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="3a560-170">Веб-приложения рабочей `wordpressprodapp`и промежуточных веб-приложения `wordpressprodapp-stage`, базы данных должен toodifferent точки.</span><span class="sxs-lookup"><span data-stu-id="3a560-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="3a560-171">Настройка параметров приложения с учетом конкретной среды</span><span class="sxs-lookup"><span data-stu-id="3a560-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="3a560-172">Разработчики могут хранить пары ключ значение строки в Azure как часть сведений о конфигурации hello, вызывается **параметры приложения**, связанную с веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="3a560-173">Во время выполнения веб-приложения автоматически получать эти значения и сделать их доступными toocode, который выполняется в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="3a560-174">Это дает положительный побочный эффект с точки зрения безопасности, так как конфиденциальная информация, например строки подключения к базам данных и пароли, никогда не отображается в виде открытого текста в таких файлах, как `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="3a560-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="3a560-175">Этот процесс, который описан в следующих абзацах hello, полезно, поскольку он включает изменения в файле и изменения базы данных для приложения hello WordPress:</span><span class="sxs-lookup"><span data-stu-id="3a560-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="3a560-176">обновление версии WordPress;</span><span class="sxs-lookup"><span data-stu-id="3a560-176">WordPress version upgrade</span></span>
* <span data-ttu-id="3a560-177">добавление, изменение или обновление подключаемых модулей;</span><span class="sxs-lookup"><span data-stu-id="3a560-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="3a560-178">добавление, изменение или обновление тем.</span><span class="sxs-lookup"><span data-stu-id="3a560-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="3a560-179">Настройка параметров приложения:</span><span class="sxs-lookup"><span data-stu-id="3a560-179">Configure app settings for:</span></span>

* <span data-ttu-id="3a560-180">сведения о базе данных;</span><span class="sxs-lookup"><span data-stu-id="3a560-180">Database information</span></span>
* <span data-ttu-id="3a560-181">включение и выключение ведения журнала для WordPress.</span><span class="sxs-lookup"><span data-stu-id="3a560-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="3a560-182">параметры безопасности WordPress.</span><span class="sxs-lookup"><span data-stu-id="3a560-182">WordPress security settings</span></span>

![Параметры приложения для веб-приложения WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="3a560-184">Убедитесь, что добавить следующие параметры приложения для гнезда приложения и этап web производственного hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="3a560-185">Обратите внимание, что hello рабочего веб-приложения и промежуточного веб-приложения используют другой базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a560-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="3a560-186">Очистить hello **параметр слот** флажок для всех параметров настройки hello, за исключением WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="3a560-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="3a560-187">Этот процесс поменяет hello конфигурации для веб-приложения, содержимое файла и базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a560-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="3a560-188">Если **параметр слот** — флажок установлен, параметры приложения hello веб-приложения и конфигурации строки соединения будут *не* переместить во всех средах, при выполнении **замены** операции.</span><span class="sxs-lookup"><span data-stu-id="3a560-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="3a560-189">поэтому любые изменения базы данных не приведут к сбою рабочего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="3a560-190">Развертывание с помощью WebMatrix или средств по своему усмотрению, таких как FTP, Git или PhpMyAdmin hello локальной разработки среды web app toohello этап веб-приложения и базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a560-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Диалоговое окно публикации веб-приложения WordPress в WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="3a560-192">Перейдите к веб-приложению в промежуточной среде и протестируйте его.</span><span class="sxs-lookup"><span data-stu-id="3a560-192">Browse and test your staging web app.</span></span> <span data-ttu-id="3a560-193">Учитывая сценарии, где тема hello hello веб-приложения — toobe обновлен Вот hello промежуточных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![Просмотр промежуточных веб-приложений до переключения слотов](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="3a560-195">Если все в порядке, нажмите кнопку hello **замены** кнопку на вашей промежуточного приложения toomove web содержимого toohello рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="3a560-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="3a560-196">В этом случае замены hello веб-приложения и базы данных hello во всех средах во время каждого **Swap** операции.</span><span class="sxs-lookup"><span data-stu-id="3a560-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![Просмотр изменений при переключении для WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="3a560-198">Если ваш сценарий должен tooonly принудительной файлы (без обновления базы данных), затем проверьте **параметр слот** для всех hello относящиеся к базе данных *параметры приложения* и *Параметрыстрокиподключения*в hello **параметры веб-приложения** колонки в hello портал Azure, прежде чем сделать hello **замены**.</span><span class="sxs-lookup"><span data-stu-id="3a560-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="3a560-199">В этом случае параметры DB_NAME, DB_HOST, DB_PASSWORD, DB_USER и строка подключения по умолчанию не должны отображаться при предварительном просмотре изменений перед **переключением**.</span><span class="sxs-lookup"><span data-stu-id="3a560-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="3a560-200">В настоящее время при заполнении hello **замены** операции hello WordPress веб-приложения будет иметь hello обновляет только файлы.</span><span class="sxs-lookup"><span data-stu-id="3a560-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="3a560-201">Прежде чем делать **замены**, вот hello рабочего WordPress веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="3a560-202">![Рабочее веб-приложение перед переключением слотов](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="3a560-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="3a560-203">После hello **замены** операции темы hello была обновлена на производственных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![Рабочее веб-приложение после переключения слотов](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="3a560-205">При необходимости обратно tooroll можно перейти web toohello рабочей **параметры приложения**и нажмите кнопку hello **замены** tooswap hello веб-приложения и базы данных из рабочего слота toostaging, нажмите кнопку.</span><span class="sxs-lookup"><span data-stu-id="3a560-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="3a560-206">Следует помнить, что, если изменения в базе данных входят в состав **замены** операции, а затем развернуть tooyour промежуточных веб-приложения, при очередном hello необходимо toodeploy hello базы данных изменения toohello текущей базы данных для размещения веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="3a560-207">Hello текущей базы данных может быть hello предыдущей рабочей базы данных или базы данных рабочей области hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="3a560-208">Сводка</span><span class="sxs-lookup"><span data-stu-id="3a560-208">Summary</span></span>
<span data-ttu-id="3a560-209">Ниже приведен общий процесс для любого приложения с базой данных:</span><span class="sxs-lookup"><span data-stu-id="3a560-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="3a560-210">Установите приложение hello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="3a560-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="3a560-211">Выбор конфигурации в зависимости от конкретной среды (локальное приложение и веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="3a560-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="3a560-212">Настройка промежуточной и рабочей сред для веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="3a560-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="3a560-213">При наличии рабочего приложения, уже работающие в Azure синхронизации рабочей содержимого (файлы или код базы данных) toolocal и промежуточной сред и.</span><span class="sxs-lookup"><span data-stu-id="3a560-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="3a560-214">Разработка приложения в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="3a560-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="3a560-215">Поместите производственного веб-приложения или заблокированный режим и синхронизировать содержимое базы данных из рабочих средах toostaging и разработки.</span><span class="sxs-lookup"><span data-stu-id="3a560-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="3a560-216">Развертывание toohello промежуточной среды и тестирования.</span><span class="sxs-lookup"><span data-stu-id="3a560-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="3a560-217">Развертывание среды tooproduction.</span><span class="sxs-lookup"><span data-stu-id="3a560-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="3a560-218">Повтор шагов 4–6.</span><span class="sxs-lookup"><span data-stu-id="3a560-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="3a560-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="3a560-219">Umbraco</span></span>
<span data-ttu-id="3a560-220">В этом разделе вы узнаете, как hello Umbraco CMS использует toodeploy пользовательский модуль в нескольких средах DevOps.</span><span class="sxs-lookup"><span data-stu-id="3a560-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="3a560-221">В этом примере представлен toomanaging другой подход несколько сред разработки.</span><span class="sxs-lookup"><span data-stu-id="3a560-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="3a560-222">[Umbraco CMS](http://umbraco.com/) — это популярное среди разработчиков CMS-решение на основе .NET,</span><span class="sxs-lookup"><span data-stu-id="3a560-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="3a560-223">Он предоставляет hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy модуль tooproduction сред разработки toostaging.</span><span class="sxs-lookup"><span data-stu-id="3a560-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="3a560-224">Вы можете легко создать локальную среду разработки для веб-приложения Umbraco CMS с помощью Visual Studio или WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="3a560-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="3a560-225">Создание веб-приложения Umbraco с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3a560-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="3a560-226">Создание веб-приложения Umbraco с помощью WebMatrix</span><span class="sxs-lookup"><span data-stu-id="3a560-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="3a560-227">Не забывайте tooremove hello `install` папку приложения и никогда не отправлять toostage или рабочей веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="3a560-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="3a560-228">В этом руководстве используется WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="3a560-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="3a560-229">Настройка промежуточной среды</span><span class="sxs-lookup"><span data-stu-id="3a560-229">Set up a staging environment</span></span>
1. <span data-ttu-id="3a560-230">Создайте слот развертывания, как упоминалось ранее, для hello Umbraco CMS веб-приложения, при условии, что уже имеется веб-приложение Umbraco CMS и работает.</span><span class="sxs-lookup"><span data-stu-id="3a560-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="3a560-231">Если этого не сделать, можно создать один из hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3a560-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="3a560-232">Обновление строки подключения hello для вашей рабочей области развертывания слот toopoint toohello новый **umbraco рабочей области db** базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a560-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="3a560-233">Ваш рабочего веб-приложения (umbraositecms-1) и промежуточный веб-приложения (этап umbracositecms 1) *должен* toodifferent точки баз данных.</span><span class="sxs-lookup"><span data-stu-id="3a560-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![Обновление строки подключения для промежуточного веб-приложения с новой промежуточной базой данных](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="3a560-235">Нажмите кнопку **параметры получения публикации** для слота развертывания hello **этап**.</span><span class="sxs-lookup"><span data-stu-id="3a560-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="3a560-236">Этот процесс будет загрузить файл параметров публикации, в которой хранятся все сведения о hello, что Visual Studio или в WebMatrix требует toopublish приложения hello локальная разработка web app toohello веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="3a560-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Получение публикации равным hello промежуточных веб-приложения](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="3a560-238">Откройте веб-приложение в локальной среде разработки WebMatrix или Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a560-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="3a560-239">В этом руководстве используется WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="3a560-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="3a560-240">Во-первых, требуется tooimport hello параметры публикации для размещения веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Импорт параметров публикации в Umbraco с помощью Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="3a560-242">Проверьте изменения в диалоговое окно «hello» и развернуть локальный веб-приложения tooyour Azure web приложение, *umbracositecms 1 рабочей области*.</span><span class="sxs-lookup"><span data-stu-id="3a560-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="3a560-243">При развертывании файлов напрямую промежуточной tooyour веб-приложения, исключаются файлы в hello `~/app_data/TEMP/` папку, так как эти файлы будут созданы заново, при первом веб-приложения hello этапа работы.</span><span class="sxs-lookup"><span data-stu-id="3a560-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="3a560-244">Также следует опустить hello `~/app_data/umbraco.config` файл, который будет также создан повторно.</span><span class="sxs-lookup"><span data-stu-id="3a560-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Просмотр изменений публикации в WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="3a560-246">После успешной публикации hello Umbraco локального web app toohello промежуточной веб-приложения, Обзор tooyour промежуточного веб-приложения и запустить несколько тестов toorule проблемы.</span><span class="sxs-lookup"><span data-stu-id="3a560-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="3a560-247">Настройка модуля развертывания Courier2 hello</span><span class="sxs-lookup"><span data-stu-id="3a560-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="3a560-248">С hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) модуль, можно просто щелкнуть toopush содержимого, стилей и разработки модулей из промежуточного web app tooa рабочего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="3a560-249">При этом уменьшается hello риска нарушения производственного веб-приложения при развертывании обновления.</span><span class="sxs-lookup"><span data-stu-id="3a560-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="3a560-250">Приобрести лицензию для Courier2 hello `*.azurewebsites.net` домен и личный домен (например http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="3a560-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="3a560-251">После приобретения лицензии hello hello месте загруженные лицензии (. Файл: лицензионное соглашение) в hello `bin` папки.</span><span class="sxs-lookup"><span data-stu-id="3a560-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![Перенос файла лицензии в папку bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="3a560-253">[Загрузить пакет hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="3a560-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="3a560-254">Вход tooyour этап веб-приложения, например http://umbracocms-site-stage.azurewebsites.net/umbraco щелкните hello **разработчика** меню, а затем нажмите **пакетов** > **установки локального пакета**.</span><span class="sxs-lookup"><span data-stu-id="3a560-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Установщик пакета Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="3a560-256">Отправьте пакет hello Courier2 с помощью установщика hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Загрузка пакета модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="3a560-258">пакет tooconfigure hello, требуется файл courier.config hello tooupdate под hello **Config** папки веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="3a560-259">В разделе `<repositories>`, введите hello производственного сайта URL-адрес и сведения о пользователях.</span><span class="sxs-lookup"><span data-stu-id="3a560-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="3a560-260">При использовании поставщика членства Umbraco по умолчанию hello, затем добавьте идентификатор пользователя администрирования hello hello в hello &lt;пользователя&gt; раздела.</span><span class="sxs-lookup"><span data-stu-id="3a560-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="3a560-261">При использовании пользовательского поставщика членства Umbraco используйте `<login>`,`<password>` в hello Courier2 модуль tooconnect toohello рабочего сайта.</span><span class="sxs-lookup"><span data-stu-id="3a560-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="3a560-262">Дополнительные сведения [документации hello hello Courier2 модуль](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="3a560-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="3a560-263">Аналогичным образом установить модуль Courier2 hello на на рабочем сайте и настройте его toopoint toohello этап веб-приложения в своем файле соответствующих courier.config, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3a560-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="3a560-264">Нажмите кнопку hello **Courier2** вкладке hello Umbraco CMS панели мониторинга приложения и нажмите кнопку **расположения**.</span><span class="sxs-lookup"><span data-stu-id="3a560-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="3a560-265">Вы увидите имя репозитория hello, как упоминалось в `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="3a560-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="3a560-266">Сделайте это в веб-приложениях в рабочей и промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="3a560-266">Do this process on both your production and staging web apps.</span></span>

    ![Просмотр целевого репозитория веб-приложения](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="3a560-268">содержимое toodeploy из промежуточного сайта toohello рабочего сайта, hello go слишком**содержимого**и выберите существующую страницу или создать новую страницу.</span><span class="sxs-lookup"><span data-stu-id="3a560-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="3a560-269">Можно будет выбрать существующую страницу из Мое веб-приложение, где hello заголовок страницы приветствия **начало работы — новый**, а затем нажмите кнопку **сохранить и опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="3a560-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Изменение заголовка страницы и публикация](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="3a560-271">Щелкните правой кнопкой мыши hello изменить страницы tooview все параметры hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="3a560-272">Нажмите кнопку **Courier** tooopen hello **развертывания** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="3a560-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="3a560-273">Нажмите кнопку **развернуть** tooinitiate развертывания.</span><span class="sxs-lookup"><span data-stu-id="3a560-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Диалоговое окно развертывания модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="3a560-275">Просмотрите изменения hello и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="3a560-275">Review hello changes, and then click **Continue**.</span></span>

    ![Просмотр изменений в диалоговом окне развертывания модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="3a560-277">Журнал развертывания Hello показывает успешность развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Просмотр журналов развертывания из модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="3a560-279">Обзор toosee приложения web вашей рабочей среде, если hello изменения будут отражены.</span><span class="sxs-lookup"><span data-stu-id="3a560-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![Переход к рабочему веб-приложению](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="3a560-281">Дополнительные сведения о как toouse курьера, просмотрите hello документации toolearn.</span><span class="sxs-lookup"><span data-stu-id="3a560-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="3a560-282">Как tooupgrade hello версии Umbraco CMS</span><span class="sxs-lookup"><span data-stu-id="3a560-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="3a560-283">Будет Courier не помогающие выполнить обновление из одной версии tooanother Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="3a560-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="3a560-284">При обновлении версии Umbraco CMS, необходимо отслеживать проблемы совместимости с пользовательские модули или модули из партнеров, hello Umbraco основных библиотек.</span><span class="sxs-lookup"><span data-stu-id="3a560-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="3a560-285">Ниже приведены рекомендации.</span><span class="sxs-lookup"><span data-stu-id="3a560-285">Here are best practices:</span></span>

* <span data-ttu-id="3a560-286">Всегда создавайте резервную копию веб-приложения и базы данных перед обновлением.</span><span class="sxs-lookup"><span data-stu-id="3a560-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="3a560-287">На веб-приложений в Azure можно настроить автоматическое создание резервных копий для веб-сайтов с помощью функции резервного копирования hello и восстановить сайт, при необходимости с помощью функции восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="3a560-288">Дополнительные сведения см. в разделе [как tooback копирование веб-приложения](web-sites-backup.md) и [как toorestore веб-приложения](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="3a560-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="3a560-289">Проверьте совместим с версией hello, которые вы осуществили обновление для пакетов от партнеров.</span><span class="sxs-lookup"><span data-stu-id="3a560-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="3a560-290">Страница загрузки пакета hello, просмотрите hello совместимость проекта с версией Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="3a560-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="3a560-291">Дополнительные сведения о том, как tooupgrade веб-приложения локально, [см. руководство по обновлению общие hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="3a560-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="3a560-292">После обновления локальных сайтов публикации toohello изменения hello промежуточных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="3a560-293">Протестируйте приложение.</span><span class="sxs-lookup"><span data-stu-id="3a560-293">Test your application.</span></span> <span data-ttu-id="3a560-294">Если все в порядке, используйте hello **замены** кнопку tooswap промежуточного сайта toohello производственного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="3a560-295">При использовании hello **замены** операции, можно просмотреть изменения hello, которые будут затронуты в конфигурации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3a560-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="3a560-296">Это **замены** операции меняет hello веб-приложений и баз данных.</span><span class="sxs-lookup"><span data-stu-id="3a560-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="3a560-297">После hello **замены**hello производственного веб-приложения будет toohello точки umbraco рабочей области базы данных база данных и hello промежуточного веб-приложение будет tooumbraco точки одной рабочей базы данных база данных.</span><span class="sxs-lookup"><span data-stu-id="3a560-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Предварительный просмотр перед операцией перемещения при развертывании Umbraco CMS](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="3a560-299">Ниже приведены преимущества обмен hello веб-приложения и базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="3a560-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="3a560-300">Можно выполнить откат предыдущей версии веб-приложения с другим toohello **замены** при наличии проблемы с приложением.</span><span class="sxs-lookup"><span data-stu-id="3a560-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="3a560-301">Для обновления требуется toodeploy файлов и баз данных из промежуточных web app toohello рабочего веб-приложения hello и базы данных.</span><span class="sxs-lookup"><span data-stu-id="3a560-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="3a560-302">Развертывание файлов и базы данных связано с большим количеством рисков.</span><span class="sxs-lookup"><span data-stu-id="3a560-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="3a560-303">С помощью hello **замены** функция слотов, можно сократить время простоя во время обновления и уменьшить риск hello сбоев, которые могут возникнуть при развертывании изменений.</span><span class="sxs-lookup"><span data-stu-id="3a560-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="3a560-304">Можно сделать **A / B-тестирования** с помощью hello [тестирования в рабочей среде](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) компонентов.</span><span class="sxs-lookup"><span data-stu-id="3a560-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="3a560-305">В этом примере представлены hello гибкость hello платформы, где можно создать пользовательские модули аналогичные tooUmbraco Courier модуля toomanage развертывания в средах.</span><span class="sxs-lookup"><span data-stu-id="3a560-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="3a560-306">Ссылки</span><span class="sxs-lookup"><span data-stu-id="3a560-306">References</span></span>
[<span data-ttu-id="3a560-307">Гибкая разработка программного обеспечения с помощью службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="3a560-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="3a560-308">Настройка промежуточных сред для веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="3a560-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="3a560-309">Как tooblock веб-доступа к рабочей toonon слоты развертывания</span><span class="sxs-lookup"><span data-stu-id="3a560-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
