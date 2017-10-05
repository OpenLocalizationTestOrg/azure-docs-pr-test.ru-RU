---
title: "Преобразование сайта WordPress в мультисайт с помощью службы приложений Azure"
description: "Узнайте, как преобразовать существующее веб-приложение WordPress, созданное с помощью коллекции в Azure, в мультисайт WordPress"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a><span data-ttu-id="83e9d-103">Преобразование сайта WordPress в мультисайт с помощью службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="83e9d-103">Convert WordPress to Multisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="83e9d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="83e9d-104">Overview</span></span>
<span data-ttu-id="83e9d-105">*Автор [Бен Лобо (Ben Lobaugh)][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="83e9d-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="83e9d-106">В этом учебнике описано, как преобразовать существующее веб-приложение WordPress, созданное с помощью коллекции в Azure, в мультисайт WordPress.</span><span class="sxs-lookup"><span data-stu-id="83e9d-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="83e9d-107">Кроме того вы узнаете, как назначить пользовательский домен каждому из дочерних сайтов в установке.</span><span class="sxs-lookup"><span data-stu-id="83e9d-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span></span>

<span data-ttu-id="83e9d-108">Предполагается наличие существующей установки WordPress.</span><span class="sxs-lookup"><span data-stu-id="83e9d-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="83e9d-109">В противном случае следуйте инструкциям раздела [Создание веб-приложения из Azure Marketplace][website-from-gallery].</span><span class="sxs-lookup"><span data-stu-id="83e9d-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="83e9d-110">Преобразование существующего отдельного сайта WordPress выполнить достаточно просто, и многие из перечисленных здесь начальных действий взяты непосредственно со страницы [Create A Network][wordpress-codex-create-a-network] (Создание сети) в [кодексе WordPress](http://codex.wordpress.org).</span><span class="sxs-lookup"><span data-stu-id="83e9d-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="83e9d-111">Давайте приступим.</span><span class="sxs-lookup"><span data-stu-id="83e9d-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="83e9d-112">Включение функциональности мультисайта</span><span class="sxs-lookup"><span data-stu-id="83e9d-112">Allow Multisite</span></span>
<span data-ttu-id="83e9d-113">Сначала необходимо активировать функциональность Мультисайт с помощью файла `wp-config.php` с константой **WP\_ALLOW\_MULTISITE**.</span><span class="sxs-lookup"><span data-stu-id="83e9d-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="83e9d-114">Существует два способа изменить файлы веб-приложения: по протоколу FTP и через Git.</span><span class="sxs-lookup"><span data-stu-id="83e9d-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span></span> <span data-ttu-id="83e9d-115">Если вы не знаете, как настроить хотя бы один из этих способов, вы можете обратиться к одному из следующих учебных курсов:</span><span class="sxs-lookup"><span data-stu-id="83e9d-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span></span>

* <span data-ttu-id="83e9d-116">[Веб-сайт PHP с MySQL и FTP][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="83e9d-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="83e9d-117">[Веб-сайт PHP с MySQL и Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="83e9d-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="83e9d-118">Откройте в выбранном редакторе файл `wp-config.php` и в строку `/* That's all, stop editing! Happy blogging. */` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="83e9d-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="83e9d-119">Не забудьте сохранить файл и загрузить его на сервер!</span><span class="sxs-lookup"><span data-stu-id="83e9d-119">Be sure to save the file and upload it back to the server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="83e9d-120">Настройка сети</span><span class="sxs-lookup"><span data-stu-id="83e9d-120">Network Setup</span></span>
<span data-ttu-id="83e9d-121">Войдите в область веб-сайта *wp-admin*, где в меню **Сервис** вы увидите новый элемент **Настройка сети**.</span><span class="sxs-lookup"><span data-stu-id="83e9d-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="83e9d-122">Нажмите кнопку **Настройка сети** и введите сведения о своей сети.</span><span class="sxs-lookup"><span data-stu-id="83e9d-122">Click **Network Setup** and fill in the details of your network.</span></span>

![Экран настройки сети][wordpress-network-setup]

<span data-ttu-id="83e9d-124">В этом руководстве используется схема сайта *Sub-directories*, так как она должна работать при любых обстоятельствах. Позже мы настроим личные домены для каждого дочернего сайта.</span><span class="sxs-lookup"><span data-stu-id="83e9d-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span></span> <span data-ttu-id="83e9d-125">Однако должна быть возможность настроить поддомен, если вы сопоставляете домен через [портал Azure](https://portal.azure.com) и правильно настраиваете DNS с подстановочными знаками.</span><span class="sxs-lookup"><span data-stu-id="83e9d-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="83e9d-126">Дополнительные сведения о сравнении поддоменов с подкаталогами см. в статье [Types of multisite network][wordpress-codex-types-of-networks] (Типы многосайтовых сетей) в кодексе WordPress.</span><span class="sxs-lookup"><span data-stu-id="83e9d-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span></span>

## <a name="enable-the-network"></a><span data-ttu-id="83e9d-127">Включение сети</span><span class="sxs-lookup"><span data-stu-id="83e9d-127">Enable the Network</span></span>
<span data-ttu-id="83e9d-128">Теперь сеть настроена в базе данных, но для включения функций сети осталось выполнить еще один шаг.</span><span class="sxs-lookup"><span data-stu-id="83e9d-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span></span> <span data-ttu-id="83e9d-129">Завершите настройку параметров `wp-config.php` и убедитесь, что файл `web.config` правильно направляет все веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="83e9d-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="83e9d-130">После нажатия кнопки **Установить** на странице *Настройка сети* WordPress предпримет попытку обновить файлы `wp-config.php` и `web.config`.</span><span class="sxs-lookup"><span data-stu-id="83e9d-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="83e9d-131">Тем не менее, всегда следует выполнять проверку файлов, чтобы убедиться, что обновление выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="83e9d-131">However, you should always check the files to ensure the updates were successful.</span></span> <span data-ttu-id="83e9d-132">В противном случае на этом экране будут отображаться необходимые обновления.</span><span class="sxs-lookup"><span data-stu-id="83e9d-132">If not, this screen will present you with the necessary updates.</span></span> <span data-ttu-id="83e9d-133">Измените и сохраните файлы.</span><span class="sxs-lookup"><span data-stu-id="83e9d-133">Edit and save the files.</span></span>

<span data-ttu-id="83e9d-134">После выполнения этих обновлений вам необходимо выйти с панели мониторинга wp-admin и войти в нее снова.</span><span class="sxs-lookup"><span data-stu-id="83e9d-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span></span>

<span data-ttu-id="83e9d-135">На панели администратора должно появиться дополнительное меню с именем **Мои сайты**.</span><span class="sxs-lookup"><span data-stu-id="83e9d-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span></span> <span data-ttu-id="83e9d-136">Это меню позволяет управлять новой сетью на панели мониторинга **Администратор сети** .</span><span class="sxs-lookup"><span data-stu-id="83e9d-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="83e9d-137">Добавление пользовательских доменов</span><span class="sxs-lookup"><span data-stu-id="83e9d-137">Adding custom domains</span></span>
<span data-ttu-id="83e9d-138">Подключаемый модуль [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] делает добавление пользовательских доменов для любого сайта в сети очень простым.</span><span class="sxs-lookup"><span data-stu-id="83e9d-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span></span> <span data-ttu-id="83e9d-139">Для обеспечения правильной работы этого подключаемого модуля необходимо выполнить дополнительную настройку на портале, а также в регистраторе доменов.</span><span class="sxs-lookup"><span data-stu-id="83e9d-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-to-the-web-app"></a><span data-ttu-id="83e9d-140">Включение сопоставления доменов с веб-приложением</span><span class="sxs-lookup"><span data-stu-id="83e9d-140">Enable domain mapping to the web app</span></span>
<span data-ttu-id="83e9d-141">В плане обслуживания **Бесплатный** [службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714) не поддерживается добавление в веб-приложение пользовательских доменов.</span><span class="sxs-lookup"><span data-stu-id="83e9d-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span></span> <span data-ttu-id="83e9d-142">Потребуется переключиться в режим **Общий** или **Стандартный**.</span><span class="sxs-lookup"><span data-stu-id="83e9d-142">You will need to switch to **Shared** or **Standard** mode.</span></span> <span data-ttu-id="83e9d-143">Для этого:</span><span class="sxs-lookup"><span data-stu-id="83e9d-143">To do this:</span></span>

* <span data-ttu-id="83e9d-144">Войдите на портал Azure и найдите свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="83e9d-144">Log in to the Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="83e9d-145">Откройте вкладку **Масштабирование** в разделе **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="83e9d-145">Click on the **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="83e9d-146">В разделе **Общие** выберите *Общий* или *Стандартный*.</span><span class="sxs-lookup"><span data-stu-id="83e9d-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="83e9d-147">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="83e9d-147">Click **Save**</span></span>

<span data-ttu-id="83e9d-148">Может появиться сообщение с просьбой проверить изменения и подтвердить, что за это веб-приложение начнет взиматься плата в зависимости от использования и других настроек.</span><span class="sxs-lookup"><span data-stu-id="83e9d-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span></span>

<span data-ttu-id="83e9d-149">Обработка новых параметров займет несколько минут, поэтому сейчас самое время приступить к настройке домена.</span><span class="sxs-lookup"><span data-stu-id="83e9d-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="83e9d-150">Проверка домена</span><span class="sxs-lookup"><span data-stu-id="83e9d-150">Verify your domain</span></span>
<span data-ttu-id="83e9d-151">Чтобы веб-приложения Azure позволили сопоставить домен с сайтом, вам необходима авторизация для сопоставления домена.</span><span class="sxs-lookup"><span data-stu-id="83e9d-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span></span> <span data-ttu-id="83e9d-152">Для этого необходимо добавить в запись DNS новую запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="83e9d-152">To do so, you must add a new CNAME record to your DNS entry.</span></span>

* <span data-ttu-id="83e9d-153">Выполните вход в диспетчер DNS домена.</span><span class="sxs-lookup"><span data-stu-id="83e9d-153">Log in to your domain's DNS manager</span></span>
* <span data-ttu-id="83e9d-154">Создайте новую запись CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="83e9d-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="83e9d-155">Укажите в *awverify* путь *awverify.ВАШ_ДОМЕН.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="83e9d-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="83e9d-156">Для полного вступления в силу внесенных изменений DNS может потребоваться некоторое время, так что если перечисленные ниже действия не получается выполнить сразу, выпейте чашку кофе, а затем повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="83e9d-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-the-domain-to-the-web-app"></a><span data-ttu-id="83e9d-157">Добавление домена в веб-приложение</span><span class="sxs-lookup"><span data-stu-id="83e9d-157">Add the domain to the web app</span></span>
<span data-ttu-id="83e9d-158">Вернитесь в свое веб-приложение на портале Azure, откройте меню **Параметры** и щелкните **Пользовательские домены и SSL**.</span><span class="sxs-lookup"><span data-stu-id="83e9d-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="83e9d-159">Когда отобразятся *Параметры SSL* , вы увидите поля для ввода всех доменов, которые вы хотите назначить своему веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="83e9d-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span></span> <span data-ttu-id="83e9d-160">Если домен отсутствует в списке, он будет недоступен для сопоставления в WordPress независимо от настроек DNS домена.</span><span class="sxs-lookup"><span data-stu-id="83e9d-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span></span>

![Диалоговое окно "Управление пользовательскими доменами"][wordpress-manage-domains]

<span data-ttu-id="83e9d-162">После ввода своего домена в текстовом поле в Azure будет проверена созданная ранее запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="83e9d-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span></span> <span data-ttu-id="83e9d-163">Если распространение DNS не завершено, будет отображаться красный индикатор.</span><span class="sxs-lookup"><span data-stu-id="83e9d-163">If the DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="83e9d-164">Если все успешно выполнено, появится зеленый флажок.</span><span class="sxs-lookup"><span data-stu-id="83e9d-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="83e9d-165">Запишите IP-адреса, перечисленные в нижней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="83e9d-165">Take note of the IP Address listed at the bottom of the dialog.</span></span> <span data-ttu-id="83e9d-166">Они потребуются для установки A-записи для домена.</span><span class="sxs-lookup"><span data-stu-id="83e9d-166">You will need this to setup the A record for your domain.</span></span>

## <a name="setup-the-domain-a-record"></a><span data-ttu-id="83e9d-167">Настройка A-записи домена</span><span class="sxs-lookup"><span data-stu-id="83e9d-167">Setup the domain A record</span></span>
<span data-ttu-id="83e9d-168">Если предыдущие шаги выполнены успешно, теперь вы можете назначить домен веб-приложению Azure через запись A DNS.</span><span class="sxs-lookup"><span data-stu-id="83e9d-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="83e9d-169">Важно отметить, что веб-приложения Azure принимают как CNAME, так и записи A, но для правильного сопоставления домена *следует* использовать запись A.</span><span class="sxs-lookup"><span data-stu-id="83e9d-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span></span> <span data-ttu-id="83e9d-170">CNAME нельзя передать в другую CNAME, созданную в Azure с использованием ссылки "ВАШ_ДОМЕН.azurewebsites.net".</span><span class="sxs-lookup"><span data-stu-id="83e9d-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="83e9d-171">При помощи IP-адреса из предыдущего шага вернитесь в диспетчер DNS и настройте A-запись таким образом, чтобы она указывала на данный IP.</span><span class="sxs-lookup"><span data-stu-id="83e9d-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span></span>

## <a name="install-and-setup-the-plugin"></a><span data-ttu-id="83e9d-172">Установка и настройка подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="83e9d-172">Install and setup the plugin</span></span>
<span data-ttu-id="83e9d-173">В функциональности мультисайтов WordPress в настоящее время отсутствует встроенный метод сопоставления пользовательских доменов.</span><span class="sxs-lookup"><span data-stu-id="83e9d-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span></span> <span data-ttu-id="83e9d-174">Однако есть подключаемый модуль [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping], который добавляет эти функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="83e9d-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span></span> <span data-ttu-id="83e9d-175">Войдите в среду администрирования сайта и установите подключаемый модуль **Сопоставление доменов WordPress MU** .</span><span class="sxs-lookup"><span data-stu-id="83e9d-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="83e9d-176">После установки и активации подключаемого модуля выберите команды **Параметры** > **Сопоставление доменов** , чтобы настроить этот подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="83e9d-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span></span> <span data-ttu-id="83e9d-177">В первом текстовом поле *IP-адрес сервера*введите IP-адрес, который использовался при настройке A-записи для домена.</span><span class="sxs-lookup"><span data-stu-id="83e9d-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span></span> <span data-ttu-id="83e9d-178">Задайте нужные *параметры домена* (значения по умолчанию часто являются оптимальными) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="83e9d-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span></span>

## <a name="map-the-domain"></a><span data-ttu-id="83e9d-179">Сопоставление домена</span><span class="sxs-lookup"><span data-stu-id="83e9d-179">Map the domain</span></span>
<span data-ttu-id="83e9d-180">Перейдите на **Панель мониторинга** сайта, с которым требуется сопоставить домен.</span><span class="sxs-lookup"><span data-stu-id="83e9d-180">Visit the **Dashboard** for the site you wish to map the domain to.</span></span> <span data-ttu-id="83e9d-181">Щелкните **Сервис** > **Domain Mapping** (Сопоставление доменов), введите новый домен в текстовом поле и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83e9d-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span></span>

<span data-ttu-id="83e9d-182">По умолчанию новый домен перезапишет автоматически созданный домен сайта.</span><span class="sxs-lookup"><span data-stu-id="83e9d-182">By default, the new domain will be rewritten to the autogenerated site domain.</span></span> <span data-ttu-id="83e9d-183">Если требуется, чтобы весь трафик отправлялся в новый домен, перед сохранением установите флажок *Основной домен для этого блога* .</span><span class="sxs-lookup"><span data-stu-id="83e9d-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="83e9d-184">Для сайта можно добавить неограниченное количество доменов, но только один будет основным.</span><span class="sxs-lookup"><span data-stu-id="83e9d-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="83e9d-185">Повторение процедуры</span><span class="sxs-lookup"><span data-stu-id="83e9d-185">Do it again</span></span>
<span data-ttu-id="83e9d-186">Веб-приложения Azure позволяют добавить для веб-приложения неограниченное число доменов.</span><span class="sxs-lookup"><span data-stu-id="83e9d-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span></span> <span data-ttu-id="83e9d-187">Чтобы добавить другой домен, необходимо будет выполнить инструкции в разделах **Проверка домена** и **Настройка A-записи домена** для каждого домена.</span><span class="sxs-lookup"><span data-stu-id="83e9d-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="83e9d-188">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="83e9d-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="83e9d-189">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="83e9d-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="83e9d-190">Изменения</span><span class="sxs-lookup"><span data-stu-id="83e9d-190">What's changed</span></span>
* <span data-ttu-id="83e9d-191">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="83e9d-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


