---
title: "Эффективное использование сред DevOps для веб-приложений | Документация Майкрософт"
description: "Узнайте, как использовать слоты развертывания для настройки нескольких сред разработки приложения и управления ими"
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
ms.openlocfilehash: 25248411659f6c7b2e386e310428c365c44ea2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="a3fc9-103">Эффективное использование сред разработки и операций для веб-приложений</span><span class="sxs-lookup"><span data-stu-id="a3fc9-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="a3fc9-104">В этой статье показано, как настроить развертывание разных версий веб-приложений в разных средах, например в среде разработки, промежуточной среде, среде для проверки качества и рабочей среде, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="a3fc9-105">Каждая версия приложения может рассматриваться как среда разработки для конкретной цели в рамках процесса развертывания.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span></span> <span data-ttu-id="a3fc9-106">Например, разработчики могут использовать среду для проверки качества для тестирования перед переносом изменений в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span></span>
<span data-ttu-id="a3fc9-107">Работа с несколькими средами разработки может вызывать затруднения, так как необходимо отслеживать код, управлять ресурсами (вычислительные ресурсы, веб-приложения, базы данных, кэш и т. д.) и развертывать код в этих средах.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="a3fc9-108">Настройка непроизводственной среды (для подготовки, разработки, контроля качества)</span><span class="sxs-lookup"><span data-stu-id="a3fc9-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="a3fc9-109">После того как вы создадите и настроите рабочую версию веб-приложения, необходимо создать непроизводственную среду.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-109">After a production web app is up and running, the next step is to create a non-production environment.</span></span> <span data-ttu-id="a3fc9-110">Для использования слотов развертывания убедитесь, что вы работаете в рамках плана службы приложений Azure "Стандартный" или "Премиум".</span><span class="sxs-lookup"><span data-stu-id="a3fc9-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="a3fc9-111">Слоты развертывания являются динамическими веб-приложениями с собственными именами узлов.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="a3fc9-112">Содержимое веб-приложений и элементы конфигурации можно переключать между двумя слотами развертывания (включая рабочий).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="a3fc9-113">Развертывание приложения в области развертывания дает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-113">When you deploy your application to a deployment slot, you get the following benefits:</span></span>

- <span data-ttu-id="a3fc9-114">В промежуточном слоте развертывания можно проверить изменения в веб-приложении до того, как они будут отправлены в рабочий слот.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span></span>
- <span data-ttu-id="a3fc9-115">Развертывание веб-приложения в промежуточном слоте и последующее перемещение в производственный позволяет подготовить все экземпляры слота до того, как они будут перемещены в производственную среду.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="a3fc9-116">Это сокращает время простоя при развертывании веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="a3fc9-117">Перенаправление трафика не вызывает затруднений, а запросы не теряются из-за операций переключения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span></span> <span data-ttu-id="a3fc9-118">Чтобы автоматизировать весь этот рабочий процесс, настройте функцию [автоматического переноса](web-sites-staged-publishing.md#configure-auto-swap), когда проверка перед переносом не требуется.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="a3fc9-119">После переноса в слоте промежуточного развертывания окажется предыдущее производственное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span></span> <span data-ttu-id="a3fc9-120">Если изменения в рабочем слоте не соответствуют вашим ожиданиям, вы можете мгновенно выполнить откат к последнему удачному веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span></span>

<span data-ttu-id="a3fc9-121">Сведения о настройке промежуточного слота развертывания см. в статье [Настройка промежуточных сред для веб-приложений в службе приложений Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="a3fc9-122">Каждая среда должна включать собственный набор ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="a3fc9-123">Например, если веб-приложение использует базу данных, рабочая и промежуточная версии веб-приложения должны использовать разные базы данных.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="a3fc9-124">Чтобы настроить промежуточную среду развертывания, добавьте для нее такие ресурсы, как база данных, хранилище и кэш.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="a3fc9-125">Примеры использования нескольких сред разработки</span><span class="sxs-lookup"><span data-stu-id="a3fc9-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="a3fc9-126">Все проекты разработки необходимо вести в рамках системы управления исходным кодом как минимум с двумя средами (средой разработки и рабочей).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="a3fc9-127">Но при использовании систем управления контентом, платформ приложений и т. п. можно столкнуться с ситуацией, когда приложение не поддерживает по умолчанию тот или иной сценарий.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span></span> <span data-ttu-id="a3fc9-128">Это справедливо для некоторых популярных платформ, рассмотренных в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span></span> <span data-ttu-id="a3fc9-129">При работе с CMS и платформами возникает множество вопросов:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="a3fc9-130">Как разделить содержимое между средами?</span><span class="sxs-lookup"><span data-stu-id="a3fc9-130">How do you break the content out into different environments?</span></span>
- <span data-ttu-id="a3fc9-131">Какие файлы можно менять, не опасаясь, что изменение потребует обновления версии платформы?</span><span class="sxs-lookup"><span data-stu-id="a3fc9-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="a3fc9-132">Как управлять конфигурацией каждой среды?</span><span class="sxs-lookup"><span data-stu-id="a3fc9-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="a3fc9-133">Как управлять обновлением модулей, подключаемых модулей или базовой платформы?</span><span class="sxs-lookup"><span data-stu-id="a3fc9-133">How do you manage version updates for modules, plugins, and the core framework?</span></span>

<span data-ttu-id="a3fc9-134">В проекте есть много способов настройки сред.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-134">There are many ways to set up multiple environments for your project.</span></span> <span data-ttu-id="a3fc9-135">Ниже приведены примеры, соответствующие рассматриваемым типам приложений.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-135">The following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="a3fc9-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="a3fc9-136">WordPress</span></span>
<span data-ttu-id="a3fc9-137">Из этого раздела вы узнаете, как настроить рабочий процесс развертывания, используя слоты для WordPress.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="a3fc9-138">WordPress, как и большинство решений для управления контентом, по умолчанию не поддерживает работу с несколькими средами без настройки.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="a3fc9-139">Веб-приложения службы приложений Azure предоставляют несколько функций, облегчающих хранение параметров конфигурации вне кода.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span></span>

1. <span data-ttu-id="a3fc9-140">Прежде чем создавать промежуточный слот развертывания, настройте поддержку нескольких сред кодом приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-140">Before you create a staging slot, set up your application code to support multiple environments.</span></span> <span data-ttu-id="a3fc9-141">Для этого добавьте в начало файла `wp-config.php` в веб-приложении в локальной среде разработки следующий код.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span></span> <span data-ttu-id="a3fc9-142">Это позволит приложению использовать конфигурацию в зависимости от выбранной среды.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-142">This process will enable your application to pick the correct configuration based on the selected environment.</span></span>

    ```
    // Support multiple environments
    // set the config file based on current environment
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
    // include the config file if it exists, otherwise WP is going to fail
    require_once $path. $config_file;
    ```

2. <span data-ttu-id="a3fc9-143">Создайте в корне веб-приложения папку `config` и добавьте в нее файлы `wp-config.azure.php` и `wp-config.local.php` (для среды Azure и локальной среды).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="a3fc9-144">Скопируйте в файл `wp-config.local.php` следующий код:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-144">Copy the following in `wp-config.local.php`:</span></span>

    ```
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this to true to enable the display of notices during development.
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

    <span data-ttu-id="a3fc9-145">Настройка ключей безопасности, продемонстрированная в предыдущем коде, помогает предотвратить взлом веб-приложения, поэтому используйте уникальные значения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="a3fc9-146">Если вы хотите создать строку для ключей безопасности (пары "ключ-значение"), указанных в коде, [перейдите к автоматическому генератору](https://api.wordpress.org/secret-key/1.1/salt).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span></span>

4. <span data-ttu-id="a3fc9-147">Скопируйте в файл `wp-config.azure.php`следующий код:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-147">Copy the following code in `wp-config.azure.php`:</span></span>

    ```    
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

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
    * Change this to true to enable the display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging to investigate issues without displaying to end user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on the page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need to generate the string for security keys mentioned above, you can go the automatic generator to create new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
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

#### <a name="use-relative-paths"></a><span data-ttu-id="a3fc9-148">Использование относительных путей</span><span class="sxs-lookup"><span data-stu-id="a3fc9-148">Use relative paths</span></span>
<span data-ttu-id="a3fc9-149">В завершение следует настроить в приложении WordPress относительные пути.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-149">One last thing to configure in the WordPress app is relative paths.</span></span> <span data-ttu-id="a3fc9-150">WordPress хранит сведения об URL-адресах в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-150">WordPress stores URL information in the database.</span></span> <span data-ttu-id="a3fc9-151">Использование абсолютных путей усложняет перемещение из одной среды в другую,</span><span class="sxs-lookup"><span data-stu-id="a3fc9-151">This storage makes moving content from one environment to another more difficult.</span></span> <span data-ttu-id="a3fc9-152">так как базу данных необходимо обновлять при каждом перемещении из локальной среды в промежуточную и из промежуточной в рабочую.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-152">You need to update the database every time you move from local to stage or stage to production environments.</span></span> <span data-ttu-id="a3fc9-153">Чтобы снизить вероятность возникновения проблем, вызванных обновлением базы данных при каждом переносе ресурсов из одной среды в другую, используйте [подключаемый модуль для создания путей относительно корневого элемента](https://wordpress.org/plugins/root-relative-urls/), который можно установить с помощью панели мониторинга администратора WordPress.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span></span>

<span data-ttu-id="a3fc9-154">Добавьте следующие записи в файл `wp-config.php` перед комментарием `That's all, stop editing!`:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="a3fc9-155">Активируйте подключаемый модуль, используя меню `Plugins` на панели мониторинга администратора WordPress.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="a3fc9-156">Сохраните постоянную ссылку на приложение WordPress.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="the-final-wp-configphp-file"></a><span data-ttu-id="a3fc9-157">Итоговая версия файла `wp-config.php`</span><span class="sxs-lookup"><span data-stu-id="a3fc9-157">The final `wp-config.php` file</span></span>
<span data-ttu-id="a3fc9-158">Никакие основные обновления WordPress не будут оказывать влияния на файлы `wp-config.php`, `wp-config.azure.php` и `wp-config.local.php`.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="a3fc9-159">Ниже приведен окончательный вариант файла `wp-config.php`:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-159">Here's a final version of the `wp-config.php` file:</span></span>

```
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web web app, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// Support multiple environments
// set the config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include the config file if it exists, otherwise WP is going to fail
  require_once $path. $config_file;
}

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="a3fc9-160">Настройка промежуточной среды</span><span class="sxs-lookup"><span data-stu-id="a3fc9-160">Set up a staging environment</span></span>
1. <span data-ttu-id="a3fc9-161">Если у вас уже есть веб-приложение WordPress, развернутое в подписке Azure, войдите на [портал Azure](http://portal.azure.com) и перейдите к веб-приложению WordPress.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span></span> <span data-ttu-id="a3fc9-162">Если у вас нет веб-приложения WordPress, его можно создать в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span></span> <span data-ttu-id="a3fc9-163">Дополнительные сведения см. в статье [Создание веб-приложения WordPress в службе приложений Azure](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="a3fc9-164">Чтобы создать слот развертывания с именем *stage*, выберите **Параметры** > **Слоты развертывания** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span></span> <span data-ttu-id="a3fc9-165">Слот развертывания — это другое веб-приложение, которое использует те же ресурсы, что и основное веб-приложение, созданное ранее.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span></span>

    ![Создание промежуточного слота развертывания](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="a3fc9-167">Добавьте другую базу данных MySQL, например `wordpress-stage-db`, в группу ресурсов `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span></span>

    ![Добавление базы данных MySQL в группу ресурсов](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="a3fc9-169">Обновите строки подключения для промежуточного слота развертывания, указав в них новую базу данных `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="a3fc9-170">Рабочее веб-приложение `wordpressprodapp` и промежуточное веб-приложение `wordpressprodapp-stage` должны указывать на разные базы данных.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="a3fc9-171">Настройка параметров приложения с учетом конкретной среды</span><span class="sxs-lookup"><span data-stu-id="a3fc9-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="a3fc9-172">Разработчики могут хранить пары "ключ-значение" в Azure в разделе **Параметры приложения** сведений о конфигурации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="a3fc9-173">В среде выполнения веб-приложения автоматически получают эти значения и делают их доступными коду, выполняемому в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span></span> <span data-ttu-id="a3fc9-174">Это дает положительный побочный эффект с точки зрения безопасности, так как конфиденциальная информация, например строки подключения к базам данных и пароли, никогда не отображается в виде открытого текста в таких файлах, как `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="a3fc9-175">Процесс, описанный в следующих разделах, объединяет изменения как файлов, так и базы данных для приложения WordPress:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span></span>

* <span data-ttu-id="a3fc9-176">обновление версии WordPress;</span><span class="sxs-lookup"><span data-stu-id="a3fc9-176">WordPress version upgrade</span></span>
* <span data-ttu-id="a3fc9-177">добавление, изменение или обновление подключаемых модулей;</span><span class="sxs-lookup"><span data-stu-id="a3fc9-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="a3fc9-178">добавление, изменение или обновление тем.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="a3fc9-179">Настройка параметров приложения:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-179">Configure app settings for:</span></span>

* <span data-ttu-id="a3fc9-180">сведения о базе данных;</span><span class="sxs-lookup"><span data-stu-id="a3fc9-180">Database information</span></span>
* <span data-ttu-id="a3fc9-181">включение и выключение ведения журнала для WordPress.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="a3fc9-182">параметры безопасности WordPress.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-182">WordPress security settings</span></span>

![Параметры приложения для веб-приложения WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="a3fc9-184">Убедитесь, что вы добавили следующие параметры приложения для рабочего веб-приложения и промежуточного слота.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-184">Make sure that you add the following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="a3fc9-185">Обратите внимание, что рабочая и промежуточная версии веб-приложения должны использовать разные базы данных.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-185">Note that the production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="a3fc9-186">Снимите флажок **Параметр слота** для всех параметров, кроме WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span></span> <span data-ttu-id="a3fc9-187">Этот процесс отвечает за смену конфигурации вашего веб-приложения, а также содержимого файлов и базы данных.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-187">This process will swap the configuration for your web app, file content, and database.</span></span> <span data-ttu-id="a3fc9-188">Если флажок **Параметр слота** установлен, параметры веб-приложения и строки подключения *не* будут перемещаться из одной среды в другую во время **переключения**,</span><span class="sxs-lookup"><span data-stu-id="a3fc9-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="a3fc9-189">поэтому любые изменения базы данных не приведут к сбою рабочего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="a3fc9-190">Разверните веб-приложение в локальной среде разработки, чтобы затем переместить его и базу данных в промежуточную среду с помощью WebMatrix или других средств, таких как FTP, Git или PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Диалоговое окно публикации веб-приложения WordPress в WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="a3fc9-192">Перейдите к веб-приложению в промежуточной среде и протестируйте его.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-192">Browse and test your staging web app.</span></span> <span data-ttu-id="a3fc9-193">Рассмотрим сценарий, в котором нужно обновить тему веб-приложения. Промежуточная версия выглядит так:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span></span>

    ![Просмотр промежуточных веб-приложений до переключения слотов](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="a3fc9-195">Если ничего менять не требуется, щелкните **Переключить** в параметрах промежуточного веб-приложения, чтобы переместить его содержимое в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span></span> <span data-ttu-id="a3fc9-196">В нашем примере каждая операция **переключения** приводит к переключению веб-приложения и базы данных между средами.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span></span>

    ![Просмотр изменений при переключении для WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="a3fc9-198">Если в вашем сценарии требуется только передача файлов (без обновления базы данных), то перед выполнением операции **переключения** установите флажок **Параметр слота** для всех *параметров приложения* и *параметров строки подключения*, связанных с базой данных, в колонке **параметров веб-приложения** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span></span> <span data-ttu-id="a3fc9-199">В этом случае параметры DB_NAME, DB_HOST, DB_PASSWORD, DB_USER и строка подключения по умолчанию не должны отображаться при предварительном просмотре изменений перед **переключением**.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="a3fc9-200">После **переключения** в веб-приложении WordPress будут только обновленные файлы.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span></span>
    >
    >

    <span data-ttu-id="a3fc9-201">Перед выполнением операции **переключения** рабочее приложение WordPress выглядит так:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-201">Before doing a **Swap**, here is the production WordPress web app.</span></span>
    <span data-ttu-id="a3fc9-202">![Рабочее веб-приложение перед переключением слотов](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="a3fc9-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="a3fc9-203">После операции **переключения** тема в рабочем веб-приложении будет обновлена.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-203">After the **Swap** operation, the theme has been updated on your production web app.</span></span>

    ![Рабочее веб-приложение после переключения слотов](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="a3fc9-205">Если вам необходимо выполнить **откат**, перейдите к параметрам рабочего веб-приложения и нажмите кнопку **Переключить**, чтобы переключить веб-приложение и базу данных из рабочего слота на промежуточный.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span></span> <span data-ttu-id="a3fc9-206">Имейте в виду, что если в операцию **переключения** включены изменения базы данных, то при следующем повторном развертывании промежуточного веб-приложения потребуется развернуть изменения базы данных в текущей базе данных для промежуточного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span></span> <span data-ttu-id="a3fc9-207">Это может быть как предыдущая рабочая, так и промежуточная база данных.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-207">The current database might be the previous production database or the stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="a3fc9-208">Сводка</span><span class="sxs-lookup"><span data-stu-id="a3fc9-208">Summary</span></span>
<span data-ttu-id="a3fc9-209">Ниже приведен общий процесс для любого приложения с базой данных:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="a3fc9-210">Установка приложения в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-210">Install the application on your local environment.</span></span>
2. <span data-ttu-id="a3fc9-211">Выбор конфигурации в зависимости от конкретной среды (локальное приложение и веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="a3fc9-212">Настройка промежуточной и рабочей сред для веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="a3fc9-213">Синхронизация содержимого рабочей среды (файлы, код и база данных) с локальной и промежуточной средами (если ваше рабочее приложение уже выполняется в Azure).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span></span>
5. <span data-ttu-id="a3fc9-214">Разработка приложения в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="a3fc9-215">Перевод рабочего веб-приложения в режим обслуживания или блокировки для синхронизации содержимого базы данных в рабочей среде с промежуточной средой и средой разработки.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span></span>
7. <span data-ttu-id="a3fc9-216">Развертывание в промежуточной среде и тестирование.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-216">Deploy to the staging environment and test.</span></span>
8. <span data-ttu-id="a3fc9-217">Развертывание в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-217">Deploy to production environment.</span></span>
9. <span data-ttu-id="a3fc9-218">Повтор шагов 4–6.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="a3fc9-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="a3fc9-219">Umbraco</span></span>
<span data-ttu-id="a3fc9-220">Из этого раздела вы узнаете, как использовать пользовательские модули в системе CMS Umbraco для развертывания в нескольких средах разработки и операций.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span></span> <span data-ttu-id="a3fc9-221">В этом примере представлен другой подход к управлению развертыванием в нескольких средах разработки.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-221">This example provides a different approach to managing multiple development environments.</span></span>

<span data-ttu-id="a3fc9-222">[Umbraco CMS](http://umbraco.com/) — это популярное среди разработчиков CMS-решение на основе .NET,</span><span class="sxs-lookup"><span data-stu-id="a3fc9-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="a3fc9-223">предоставляющее модуль [Courier2](http://umbraco.com/products/more-add-ons/courier-2) для переноса содержимого из среды разработки в промежуточную, а затем и в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span></span> <span data-ttu-id="a3fc9-224">Вы можете легко создать локальную среду разработки для веб-приложения Umbraco CMS с помощью Visual Studio или WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="a3fc9-225">Создание веб-приложения Umbraco с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3fc9-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="a3fc9-226">Создание веб-приложения Umbraco с помощью WebMatrix</span><span class="sxs-lookup"><span data-stu-id="a3fc9-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="a3fc9-227">Не забывайте удалять папку `install` приложения и никогда не переносите ее в промежуточную или рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span></span> <span data-ttu-id="a3fc9-228">В этом руководстве используется WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="a3fc9-229">Настройка промежуточной среды</span><span class="sxs-lookup"><span data-stu-id="a3fc9-229">Set up a staging environment</span></span>
1. <span data-ttu-id="a3fc9-230">Предположим, у вас уже есть готовое веб-приложение Umbraco CMS. Создайте слот развертывания для веб-приложения Umbraco CMS в соответствии с приведенными выше инструкциями.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="a3fc9-231">Если приложения нет, вы можете создать его в магазине.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-231">If you do not, you can create one from the Marketplace.</span></span>
2. <span data-ttu-id="a3fc9-232">Обновите строки подключения для промежуточного слота развертывания, указав в них новую базу данных **umbraco-stage-db**.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span></span> <span data-ttu-id="a3fc9-233">Ваше рабочее веб-приложение (umbraositecms-1) и промежуточное веб-приложение (umbracositecms-1-stage) *должны* указывать на разные базы данных.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span></span>

    ![Обновление строки подключения для промежуточного веб-приложения с новой промежуточной базой данных](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="a3fc9-235">Щелкните **Get Publish settings** (Получить параметры публикации) для **промежуточного** слота развертывания.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-235">Click **Get Publish settings** for the deployment slot **stage**.</span></span> <span data-ttu-id="a3fc9-236">Будет загружен файл параметров публикации, в котором хранятся сведения, необходимые Visual Studio или WebMatrix для публикации приложения из локальной среды разработки в веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span></span>

    ![Получение параметров публикации для промежуточного веб-приложения](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="a3fc9-238">Откройте веб-приложение в локальной среде разработки WebMatrix или Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="a3fc9-239">В этом руководстве используется WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="a3fc9-240">Сначала нам необходимо импортировать файл параметров публикации для промежуточного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-240">First, you need to import the publish settings file for your staging web app.</span></span>

    ![Импорт параметров публикации в Umbraco с помощью Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="a3fc9-242">Просмотрите изменения в диалоговом окне и разверните локальное веб-приложение в веб-приложение Azure *umbracositecms-1-stage*.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="a3fc9-243">При развертывании файлов непосредственно в промежуточное веб-приложение исключаются файлы в папке `~/app_data/TEMP/`, так как они будут повторно созданы при первом запуске промежуточного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span></span> <span data-ttu-id="a3fc9-244">Следует также пропустить файл `~/app_data/umbraco.config`, так как он тоже будет создан заново.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Просмотр изменений публикации в WebMatrix](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="a3fc9-246">После успешной публикации локального веб-приложения Umbraco в промежуточное веб-приложение перейдите к промежуточному веб-приложению и выполните несколько тестов, чтобы исключить возможные проблемы.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span></span>

#### <a name="set-up-the-courier2-deployment-module"></a><span data-ttu-id="a3fc9-247">Настройка модуля развертывания Courier2</span><span class="sxs-lookup"><span data-stu-id="a3fc9-247">Set up the Courier2 deployment module</span></span>
<span data-ttu-id="a3fc9-248">Используя модуль [Courier2](http://umbraco.com/products/more-add-ons/courier-2), вы можете щелчком правой кнопки мыши передавать содержимое, таблицы стилей и модули разработки из промежуточного веб-приложения в рабочее.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span></span> <span data-ttu-id="a3fc9-249">Это снижает риск возникновения сбоев рабочего веб-приложения при развертывании обновлений.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-249">This process reduces the risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="a3fc9-250">Приобретите лицензию на Courier2 для домена `*.azurewebsites.net` и пользовательского домена (например, http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="a3fc9-251">После этого поместите скачанный файл лицензии (LIC-файл) в папку `bin`.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span></span>

![Перенос файла лицензии в папку bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="a3fc9-253">[Скачайте пакет Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="a3fc9-254">Войдите в промежуточное веб-приложение, например http://umbracocms-site-stage.azurewebsites.net/umbraco, и в меню **Разработчик** щелкните **Пакеты** > **Install local package** (Установить локальный пакет).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Установщик пакета Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="a3fc9-256">Передайте пакет Сourier2 с помощью установщика.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-256">Upload the Courier2 package by using the installer.</span></span>

    ![Загрузка пакета модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="a3fc9-258">Для настройки пакета необходимо обновить файл courier.config в папке **Config** вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span></span>

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. <span data-ttu-id="a3fc9-259">В `<repositories>` введите URL-адрес рабочего сайта и сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-259">Under `<repositories>`, enter the production site URL and user information.</span></span>
    <span data-ttu-id="a3fc9-260">Если используется поставщик членства Umbraco по умолчанию, следует добавить соответствующий идентификатор для пользователя-администратора в разделе &lt;user&gt;.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span></span>
    <span data-ttu-id="a3fc9-261">Если используется собственный поставщик членства Umbraco, укажите `<login>`, `<password>`, с которыми модуль Courier2 должен подключаться к рабочему сайту.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span></span>
    <span data-ttu-id="a3fc9-262">Дополнительные сведения см. в [документации по модулю Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="a3fc9-263">Аналогичным образом установите модуль Courier2 на рабочий сайт и настройте его на размещенное веб-приложение в соответствующем файле courier.config, как показано здесь.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span></span>

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. <span data-ttu-id="a3fc9-264">Откройте вкладку **Courier2** в панели мониторинга веб-приложений Umbraco CMS и щелкните **Расположения**.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="a3fc9-265">Вы увидите имя репозитория, используемое в `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-265">You should see the repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="a3fc9-266">Сделайте это в веб-приложениях в рабочей и промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-266">Do this process on both your production and staging web apps.</span></span>

    ![Просмотр целевого репозитория веб-приложения](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="a3fc9-268">Для развертывания содержимого промежуточного сайта в рабочей среде перейдите в раздел **Содержимое** и выберите существующую страницу или создайте ее.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="a3fc9-269">Выберем существующую страницу в разделе "Мое веб-приложение" с заголовком **Приступая к работе — новый**, после чего нажмем кнопку **Сохранить и опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Изменение заголовка страницы и публикация](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="a3fc9-271">Щелкните измененную страницу правой кнопкой мыши, чтобы просмотреть все параметры.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-271">Right-click the modified page to view all the options.</span></span> <span data-ttu-id="a3fc9-272">Щелкните **Courier**, чтобы открыть диалоговое окно **Развертывание**.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-272">Click **Courier** to open the **Deployment** dialog box.</span></span> <span data-ttu-id="a3fc9-273">Щелкните **Развернуть**, чтобы инициировать развертывание.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-273">Click **Deploy** to initiate deployment.</span></span>

    ![Диалоговое окно развертывания модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="a3fc9-275">Просмотрите изменения и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-275">Review the changes, and then click **Continue**.</span></span>

    ![Просмотр изменений в диалоговом окне развертывания модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="a3fc9-277">Информация о результатах развертывания отображается в журнале развертывания.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-277">The deployment log shows if the deployment was successful.</span></span>

     ![Просмотр журналов развертывания из модуля Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="a3fc9-279">Перейдите к рабочему веб-приложению, чтобы проверить, отражены ли изменения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-279">Browse your production web app to see if the changes are reflected.</span></span>

     ![Переход к рабочему веб-приложению](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="a3fc9-281">Дополнительные сведения об использовании Courier см. в документации.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-281">To learn more about how to use Courier, review the documentation.</span></span>

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a><span data-ttu-id="a3fc9-282">Обновление Umbraco CMS</span><span class="sxs-lookup"><span data-stu-id="a3fc9-282">How to upgrade the Umbraco CMS version</span></span>
<span data-ttu-id="a3fc9-283">Пакеты Courier невозможно использовать при обновлении с одной версии CMS Umbraco до другой.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span></span> <span data-ttu-id="a3fc9-284">При обновлении версии Umbraco CMS необходимо проверить совместимость с пользовательскими модулями, партнерскими модулями и основными библиотеками Umbraco.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span></span> <span data-ttu-id="a3fc9-285">Ниже приведены рекомендации.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-285">Here are best practices:</span></span>

* <span data-ttu-id="a3fc9-286">Всегда создавайте резервную копию веб-приложения и базы данных перед обновлением.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="a3fc9-287">Для веб-приложений Azure можно настроить автоматическую архивацию компонентов веб-сайтов с помощью функции архивации. При необходимости веб-сайт можно восстановить с помощью функции восстановления.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span></span> <span data-ttu-id="a3fc9-288">Дополнительные сведения см. в статьях [Архивация приложения в Azure](web-sites-backup.md) и [Восстановление приложения в Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="a3fc9-289">Проверьте партнерские пакеты на совместимость с версией, до которой выполняется обновление.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-289">Check if packages from partners are compatible with the version you're upgrading to.</span></span> <span data-ttu-id="a3fc9-290">На странице скачивания пакета проверьте совместимость проекта с версией Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="a3fc9-291">Дополнительные сведения о локальном обновлении веб-приложения см. в [общих рекомендациях по обновлению](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="a3fc9-292">После обновления локального сайта опубликуйте изменения в промежуточное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-292">After your local development site is upgraded, publish the changes to the staging web app.</span></span> <span data-ttu-id="a3fc9-293">Протестируйте приложение.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-293">Test your application.</span></span> <span data-ttu-id="a3fc9-294">Если ничего менять не требуется, нажмите кнопку **Переключить**, чтобы переключить промежуточный сайт в рабочее веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span></span> <span data-ttu-id="a3fc9-295">При выполнении операции **переключения** можно просмотреть изменения, которые произойдут в конфигурации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="a3fc9-296">В рамках **переключения** происходит переключение веб-приложений и баз данных.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-296">This **Swap** operation swaps the web apps and databases.</span></span> <span data-ttu-id="a3fc9-297">После завершения **переключения** рабочее веб-приложение будет указывать на базу данных umbraco-stage-db, а промежуточное — на базу данных umbraco-prod-db.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span></span>

![Предварительный просмотр перед операцией перемещения при развертывании Umbraco CMS](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="a3fc9-299">Ниже представлены преимущества переключения веб-приложения и базы данных:</span><span class="sxs-lookup"><span data-stu-id="a3fc9-299">Here are advantages of swapping both the web app and the database:</span></span>

* <span data-ttu-id="a3fc9-300">При возникновении проблем с приложением это позволяет выполнить откат к предыдущей версии веб-приложения с помощью другой операции **переключения**.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="a3fc9-301">Для обновления необходимо выполнить развертывание файлов и базы данных из промежуточного веб-приложения в рабочие веб-приложение и базу данных.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span></span> <span data-ttu-id="a3fc9-302">Развертывание файлов и базы данных связано с большим количеством рисков.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="a3fc9-303">Используя функцию **переключения** между слотами, мы сокращаем время простоя при обновлении и снижаем риск сбоев, которые могут произойти при развертывании изменений.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="a3fc9-304">Вы можете выполнить **тестирование A/B** с помощью функции [тестирование в рабочей среде](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/).</span><span class="sxs-lookup"><span data-stu-id="a3fc9-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="a3fc9-305">Этот пример демонстрирует гибкость платформы: вы можете создавать пользовательские модули, аналогичные модулю Umbraco Courier, для управления развертыванием в разных средах.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="a3fc9-306">Ссылки</span><span class="sxs-lookup"><span data-stu-id="a3fc9-306">References</span></span>
[<span data-ttu-id="a3fc9-307">Гибкая разработка программного обеспечения с помощью службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fc9-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="a3fc9-308">Настройка промежуточных сред для веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a3fc9-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="a3fc9-309">Блокирование веб-доступа к непроизводственным областям развертывания</span><span class="sxs-lookup"><span data-stu-id="a3fc9-309">How to block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
