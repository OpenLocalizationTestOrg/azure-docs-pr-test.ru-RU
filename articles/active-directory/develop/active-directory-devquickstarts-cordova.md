---
title: "Приступая к работе с Azure AD для Cordova | Документация Майкрософт"
description: "Практическое руководство по созданию приложения Cordova, которое интегрируется с Azure AD для входа в систему и вызывает программные интерфейсы приложения, защищенные Azure AD, по протоколу OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: d9f53148787729d29a0a89cce1b8b2b83ba228f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="e9af8-103">Интеграция Azure AD с приложением Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="e9af8-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="e9af8-104">Вы можете использовать Apache Cordova для разработки приложений на HTML5 и JavaScript, которые могут работать на мобильных устройствах как полноценные приложения.</span><span class="sxs-lookup"><span data-stu-id="e9af8-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="e9af8-105">Azure Active Directory (Azure AD) позволяет добавлять в приложения Cordova возможности проверки подлинности уровня предприятия.</span><span class="sxs-lookup"><span data-stu-id="e9af8-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="e9af8-106">Подключаемый модуль Cordova использует собственные пакеты SDK Azure AD для приложений iOS, Android, Магазина Windows и Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e9af8-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="e9af8-107">Этот подключаемый модуль позволяет расширить функции приложения, обеспечивая реализацию входа пользователей с учетными записями Windows Server Active Directory, получение доступа к Office 365 и API Azure, а также защиту вызовов пользовательского веб-API.</span><span class="sxs-lookup"><span data-stu-id="e9af8-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="e9af8-108">В данном руководстве подключаемый модуль Apache Cordova будет использоваться для библиотеки аутентификации Active Directory (ADAL), чтобы добавить в простое приложение следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="e9af8-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="e9af8-109">реализация проверки подлинности пользователя и получения маркера путем добавления всего нескольких строк кода;</span><span class="sxs-lookup"><span data-stu-id="e9af8-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="e9af8-110">вызов API Graph для запроса сведений из каталога и отображения результатов с использованием этого маркера;</span><span class="sxs-lookup"><span data-stu-id="e9af8-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="e9af8-111">минимизация количества запросов пользователя на ввод данных для проверки подлинности за счет использования кэша маркера библиотеки ADAL.</span><span class="sxs-lookup"><span data-stu-id="e9af8-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="e9af8-112">Чтобы получить эти возможности, необходимо:</span><span class="sxs-lookup"><span data-stu-id="e9af8-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="e9af8-113">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e9af8-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="e9af8-114">Добавить в приложение код для запроса маркеров.</span><span class="sxs-lookup"><span data-stu-id="e9af8-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="e9af8-115">Добавить код, использующий маркер для запросов Graph API и отображения результатов.</span><span class="sxs-lookup"><span data-stu-id="e9af8-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="e9af8-116">Создать проект развертывания Cordova на всех целевых платформах, добавить подключаемый модуль Cordova ADAL и протестировать решение в эмуляторах.</span><span class="sxs-lookup"><span data-stu-id="e9af8-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9af8-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e9af8-117">Prerequisites</span></span>
<span data-ttu-id="e9af8-118">Для работы с этим учебником необходимы указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="e9af8-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="e9af8-119">Клиент Azure AD с учетной записью с правами на разработку приложений.</span><span class="sxs-lookup"><span data-stu-id="e9af8-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="e9af8-120">Среда разработки, настроенная для использования Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="e9af8-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="e9af8-121">При наличии этих компонентов вы можете приступить непосредственно к выполнению этапа 1.</span><span class="sxs-lookup"><span data-stu-id="e9af8-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="e9af8-122">Если у вас еще нет клиента Azure AD, узнайте, [как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e9af8-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="e9af8-123">Если на компьютере не установлена платформа Apache Cordova, установите следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="e9af8-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="e9af8-124">Git.</span><span class="sxs-lookup"><span data-stu-id="e9af8-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="e9af8-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="e9af8-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="e9af8-126">[Cordova CLI](https://cordova.apache.org/) (можно легко установить через диспетчер пакетов NPM: `npm install -g cordova`).</span><span class="sxs-lookup"><span data-stu-id="e9af8-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="e9af8-127">Компоненты, описанные выше, должны работать как на ПК, так и на компьютере Mac.</span><span class="sxs-lookup"><span data-stu-id="e9af8-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="e9af8-128">У каждой целевой платформы свои требования.</span><span class="sxs-lookup"><span data-stu-id="e9af8-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="e9af8-129">Чтобы создать и запустить приложение для планшетов и компьютеров с Windows или Windows Phone, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="e9af8-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="e9af8-130">Установите [Visual Studio 2013 для Windows с обновлением 2 или более поздней версии](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express или другая версия) или [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="e9af8-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="e9af8-131">Чтобы создать и запустить приложение для iOS, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="e9af8-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="e9af8-132">Установите Xcode 6.x или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e9af8-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="e9af8-133">Вы можете ее скачать на [сайте Apple Developer](http://developer.apple.com/downloads) или из [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="e9af8-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="e9af8-134">Установите [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="e9af8-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="e9af8-135">Его можно использовать для запуска приложений iOS в эмуляторе iOS из командной строки.</span><span class="sxs-lookup"><span data-stu-id="e9af8-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="e9af8-136">(Для быстрой установки приложения используйте терминал `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="e9af8-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="e9af8-137">Чтобы создать и запустить приложение для Android, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="e9af8-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="e9af8-138">Установить [пакет средств разработки Java (JDK) версии 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e9af8-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="e9af8-139">Убедитесь, что `JAVA_HOME` (переменная среды) указывает путь установки JDK (например, C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="e9af8-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="e9af8-140">Установите [пакет SDK для Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) и добавьте `<android-sdk-location>\tools`расположение (например, C:\tools\Android\android-sdk\tools) в переменную среды `PATH`.</span><span class="sxs-lookup"><span data-stu-id="e9af8-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="e9af8-141">Откройте диспетчер пакетов SDK для Android (например, через терминал `android`) и установите:</span><span class="sxs-lookup"><span data-stu-id="e9af8-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="e9af8-142">*Android 5.0.1 (API уровня 21)* ;</span><span class="sxs-lookup"><span data-stu-id="e9af8-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="e9af8-143">*Android SDK Build Tools* версии 19.1.0 или более поздней;</span><span class="sxs-lookup"><span data-stu-id="e9af8-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="e9af8-144">*Android Support Repository* (дополнительно).</span><span class="sxs-lookup"><span data-stu-id="e9af8-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="e9af8-145">Пакет SDK для Android по умолчанию не содержит эмулятор.</span><span class="sxs-lookup"><span data-stu-id="e9af8-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="e9af8-146">Чтобы запустить приложение Android в эмуляторе, необходимо создать эмулятор, выполнив команду `android avd` из терминала, а затем выбрав **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="e9af8-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="e9af8-147">Рекомендуемый уровень API — 19 или выше.</span><span class="sxs-lookup"><span data-stu-id="e9af8-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="e9af8-148">Дополнительные сведения об эмуляторе Android и параметрах его создания см. в документе [Create and Manage Virtual Devices](http://developer.android.com/tools/help/avd-manager.html) (Создание и управление виртуальными устройствами) на сайте Android.</span><span class="sxs-lookup"><span data-stu-id="e9af8-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="e9af8-149">Шаг 1. Регистрация приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9af8-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="e9af8-150">Этот шаг не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="e9af8-150">This step is optional.</span></span> <span data-ttu-id="e9af8-151">В руководстве представлены заранее подготовленные значения, позволяющие наблюдать пример в действии без какой-либо подготовки вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="e9af8-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="e9af8-152">Однако мы все же рекомендуем пройти данный этап и ознакомиться с процессом, так как это потребуется вам при создании собственных приложений.</span><span class="sxs-lookup"><span data-stu-id="e9af8-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="e9af8-153">Azure AD выдает маркеры только для знакомых приложений.</span><span class="sxs-lookup"><span data-stu-id="e9af8-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="e9af8-154">Прежде чем использовать службу Azure AD из приложения, вы должны создать для него запись в собственном клиенте.</span><span class="sxs-lookup"><span data-stu-id="e9af8-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="e9af8-155">Чтобы зарегистрировать новое приложение в клиенте:</span><span class="sxs-lookup"><span data-stu-id="e9af8-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="e9af8-156">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9af8-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e9af8-157">На верхней панели щелкните свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="e9af8-157">On the top bar, click your account.</span></span> <span data-ttu-id="e9af8-158">В списке **Каталог** выберите клиент Azure AD, в котором будет зарегистрировано приложение.</span><span class="sxs-lookup"><span data-stu-id="e9af8-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="e9af8-159">В области слева щелкните **Больше служб** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9af8-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e9af8-160">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e9af8-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e9af8-161">Следуя инструкциям, создайте **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="e9af8-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="e9af8-162">(Хотя приложения Cordova основаны на HTML, мы создаем собственное клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="e9af8-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="e9af8-163">Чтобы оно работало, должен быть выбран параметр **Собственное клиентское приложение**.)</span><span class="sxs-lookup"><span data-stu-id="e9af8-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="e9af8-164">**Имя** приложения является его описанием для пользователей.</span><span class="sxs-lookup"><span data-stu-id="e9af8-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="e9af8-165">**URI перенаправления** — это универсальный код ресурса (URI), используемый для возврата маркеров приложению.</span><span class="sxs-lookup"><span data-stu-id="e9af8-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="e9af8-166">Введите **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="e9af8-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="e9af8-167">Когда вы завершите регистрацию, Azure AD присвоит приложению уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="e9af8-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="e9af8-168">Это значение понадобится вам в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="e9af8-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="e9af8-169">Его можно найти на вкладке только что созданного приложения.</span><span class="sxs-lookup"><span data-stu-id="e9af8-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="e9af8-170">Для запуска `DirSearchClient Sample` предоставьте созданному приложению разрешение на запрос API Graph Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9af8-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="e9af8-171">На странице **Параметры** выберите **Необходимые разрешения** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e9af8-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="e9af8-172">Для приложения Azure Active Directory выберите в качестве интерфейса API **Microsoft Graph** и добавьте разрешение **Access the directory as the signed-in user** (Доступ к каталогу в качестве пользователя, выполнившего вход) в списке **Делегированные разрешения**.</span><span class="sxs-lookup"><span data-stu-id="e9af8-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="e9af8-173">Это позволит приложению запрашивать API Graph для пользователей.</span><span class="sxs-lookup"><span data-stu-id="e9af8-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="e9af8-174">Шаг 2. Клонирование примера репозитория приложений</span><span class="sxs-lookup"><span data-stu-id="e9af8-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="e9af8-175">Введите следующую команду из оболочки или командной строки:</span><span class="sxs-lookup"><span data-stu-id="e9af8-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="e9af8-176">Шаг 3. Создание приложения Cordova</span><span class="sxs-lookup"><span data-stu-id="e9af8-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="e9af8-177">Существует несколько способов создания приложений Cordova.</span><span class="sxs-lookup"><span data-stu-id="e9af8-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="e9af8-178">В данном руководстве используется интерфейс командной строки (CLI) Cordova.</span><span class="sxs-lookup"><span data-stu-id="e9af8-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="e9af8-179">Введите следующую команду из оболочки или командной строки:</span><span class="sxs-lookup"><span data-stu-id="e9af8-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="e9af8-180">Эта команда создаст структуру папок и шаблон для проекта Cordova.</span><span class="sxs-lookup"><span data-stu-id="e9af8-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="e9af8-181">Перейдите в новую папку DirSearchClient.</span><span class="sxs-lookup"><span data-stu-id="e9af8-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="e9af8-182">Скопируйте содержимое начального проекта во вложенную папку www с помощью диспетчера файлов или следующей команды из оболочки:</span><span class="sxs-lookup"><span data-stu-id="e9af8-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="e9af8-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="e9af8-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="e9af8-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="e9af8-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="e9af8-185">Добавьте разрешенный подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="e9af8-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="e9af8-186">Это необходимо для вызова API Graph.</span><span class="sxs-lookup"><span data-stu-id="e9af8-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="e9af8-187">Добавьте все платформы, которые необходимо поддерживать.</span><span class="sxs-lookup"><span data-stu-id="e9af8-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="e9af8-188">Чтобы получить работающий пример, необходимо выполнить хотя бы одну из приведенных ниже команд.</span><span class="sxs-lookup"><span data-stu-id="e9af8-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="e9af8-189">Имейте в виду, что вы не сможете выполнить эмуляцию iOS в Windows или эмуляцию Windows в Mac.</span><span class="sxs-lookup"><span data-stu-id="e9af8-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="e9af8-190">Добавьте в проект библиотеку ADAL для подключаемого модуля Cordova.</span><span class="sxs-lookup"><span data-stu-id="e9af8-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="e9af8-191">Шаг 4. Добавление кода аутентификации пользователей и получение маркеров из Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9af8-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="e9af8-192">Приложение, которое разрабатывается в данном руководстве, предоставляет базовую функцию поиска в каталоге.</span><span class="sxs-lookup"><span data-stu-id="e9af8-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="e9af8-193">Пользователь может ввести псевдоним любого пользователя в каталоге и просмотреть некоторые основные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="e9af8-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="e9af8-194">Начальный проект содержит определение базового пользовательского интерфейса приложения (в файле www/index.html) и шаблона, который реализует циклы обработки основных событий приложения, привязку интерфейса пользователя и логику отображения результатов (в файле www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="e9af8-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="e9af8-195">Вам остается только добавить логику, реализующую задачи по работе с удостоверениями.</span><span class="sxs-lookup"><span data-stu-id="e9af8-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="e9af8-196">Первое, что необходимо сделать — это вставить в код значения протокола, используемые Azure AD для идентификации вашего приложения и целевых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e9af8-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="e9af8-197">Позже эти значения будут использоваться для создания запросов маркеров.</span><span class="sxs-lookup"><span data-stu-id="e9af8-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="e9af8-198">Вставьте следующий фрагмент в самое начала файла index.js.</span><span class="sxs-lookup"><span data-stu-id="e9af8-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="e9af8-199">Значения `redirectUri` и `clientId` должны совпадать со значениями, описывающими приложение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9af8-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="e9af8-200">Их можно найти на вкладке **Настройка** на портале Azure, как описано на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="e9af8-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="e9af8-201">Если вы решили не регистрировать новое приложение в собственном клиенте, вы можете просто вставить предварительно настроенные значения "как есть".</span><span class="sxs-lookup"><span data-stu-id="e9af8-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="e9af8-202">Это позволит вам увидеть работу примера, но вам всегда придется указывать собственные значения для рабочих приложений.</span><span class="sxs-lookup"><span data-stu-id="e9af8-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="e9af8-203">Далее добавьте код запроса маркера.</span><span class="sxs-lookup"><span data-stu-id="e9af8-203">Next, add the token request code.</span></span> <span data-ttu-id="e9af8-204">Вставьте следующий фрагмент кода между определениями `search` и `renderData`.</span><span class="sxs-lookup"><span data-stu-id="e9af8-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="e9af8-205">Рассмотрим эту функцию, разбив ее на две основные части.</span><span class="sxs-lookup"><span data-stu-id="e9af8-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="e9af8-206">Данный пример предназначен для работы с любым клиентом, а не определенным.</span><span class="sxs-lookup"><span data-stu-id="e9af8-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="e9af8-207">Он использует конечную точку "/common", которая позволяет пользователю ввести данные любой учетной записи во время проверки подлинности и направляет запрос соответствующему клиенту.</span><span class="sxs-lookup"><span data-stu-id="e9af8-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="e9af8-208">Первая часть метода проверяет кэш ADAL на наличие хранимых маркеров.</span><span class="sxs-lookup"><span data-stu-id="e9af8-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="e9af8-209">Если таковые имеются, то метод использует клиент, от которого поступил данный маркер, для повторной инициализации ADAL.</span><span class="sxs-lookup"><span data-stu-id="e9af8-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="e9af8-210">Необходимо избегать дополнительных запросов, так как использование конечной точки "/common" всегда приводит к просьбе пользователю ввести новые данные учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e9af8-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="e9af8-211">Вторая часть метода выполняет непосредственно запрос маркера.</span><span class="sxs-lookup"><span data-stu-id="e9af8-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="e9af8-212">Метод `acquireTokenSilentAsync` запрашивает ADAL вернуть маркер для указанного ресурса без отображения диалогового окна ввода учетных данных.</span><span class="sxs-lookup"><span data-stu-id="e9af8-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="e9af8-213">Диалоговое окно не отображается, если в кэше уже имеется подходящий хранимый маркер доступа или если существует маркер обновления, используемый для получения нового токена доступа без запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9af8-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="e9af8-214">Если получить действительный маркер не удается, будет вызвана функция `acquireTokenAsync`, которая через диалоговое окно запросит у пользователя данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e9af8-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="e9af8-215">Теперь, когда у нас есть маркер, мы можем, наконец, вызвать API Graph и выполнить требуемую операцию поиска.</span><span class="sxs-lookup"><span data-stu-id="e9af8-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="e9af8-216">Вставьте следующий фрагмент сразу под определением `authenticate`.</span><span class="sxs-lookup"><span data-stu-id="e9af8-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="e9af8-217">Файлы начальной точки содержат соответствующую поддержку для ввода псевдонима пользователя в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="e9af8-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="e9af8-218">Данный метод использует значение псевдонима для создания запроса, сочетания его с маркером доступа, отправки в Microsoft Graph и анализа результатов.</span><span class="sxs-lookup"><span data-stu-id="e9af8-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="e9af8-219">Метод `renderData`, который уже присутствует в файле начальной точки, отвечает за отображение результатов.</span><span class="sxs-lookup"><span data-stu-id="e9af8-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="e9af8-220">Шаг 5. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="e9af8-220">Step 5: Run the app</span></span>
<span data-ttu-id="e9af8-221">Теперь вы можете запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="e9af8-221">Your app is finally ready to run.</span></span> <span data-ttu-id="e9af8-222">Процесс работы прост: после запуска приложения введите псевдоним нужного пользователя, а затем нажмите кнопку.</span><span class="sxs-lookup"><span data-stu-id="e9af8-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="e9af8-223">Будет предложено ввести учетные данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e9af8-223">You're prompted for authentication.</span></span> <span data-ttu-id="e9af8-224">После ее завершения и успешного поиска будут отображены атрибуты нужного пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9af8-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="e9af8-225">Последующие запуски будут выполнять поиск без отображения запроса благодаря присутствию в кэше маркера, полученного ранее.</span><span class="sxs-lookup"><span data-stu-id="e9af8-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="e9af8-226">Конкретные этапы запуска приложения зависят от платформы.</span><span class="sxs-lookup"><span data-stu-id="e9af8-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="e9af8-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="e9af8-227">Windows 10</span></span>
   <span data-ttu-id="e9af8-228">Планшет или ПК: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="e9af8-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="e9af8-229">Мобильное устройство (требуется мобильное устройство с Windows 10, подключенное к компьютеру): `cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="e9af8-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="e9af8-230">Во время первого запуска может потребоваться выполнить вход для предоставления системе лицензии разработчика.</span><span class="sxs-lookup"><span data-stu-id="e9af8-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="e9af8-231">Дополнительные сведения см. в статье [Получение лицензии разработчика](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9af8-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="e9af8-232">Планшеты или компьютеры с Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="e9af8-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="e9af8-233">Во время первого запуска может потребоваться выполнить вход для предоставления системе лицензии разработчика.</span><span class="sxs-lookup"><span data-stu-id="e9af8-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="e9af8-234">Дополнительные сведения см. в статье [Получение лицензии разработчика](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9af8-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="e9af8-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="e9af8-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="e9af8-236">Запустить приложение на подключенном устройстве: `cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="e9af8-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="e9af8-237">Запустить приложение в эмуляторе по умолчанию: `cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="e9af8-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="e9af8-238">Используйте `cordova run windows --list -- --phone` для просмотра всех доступных целевых объектов и `cordova run windows --target=<target_name> -- --phone` —для запуска приложения на конкретном устройстве или эмуляторе (например, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="e9af8-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="e9af8-239">Android</span><span class="sxs-lookup"><span data-stu-id="e9af8-239">Android</span></span>
   <span data-ttu-id="e9af8-240">Запустить приложение на подключенном устройстве: `cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="e9af8-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="e9af8-241">Запустить приложение в эмуляторе по умолчанию: `cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="e9af8-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="e9af8-242">Убедитесь, что экземпляр эмулятора создан, использовав диспетчер AVD, как описано в разделе "Предварительные требования".</span><span class="sxs-lookup"><span data-stu-id="e9af8-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="e9af8-243">Используйте `cordova run android --list` для просмотра всех доступных целевых объектов и `cordova run android --target=<target_name>` —для запуска приложения на конкретном устройстве или эмуляторе (например, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="e9af8-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="e9af8-244">iOS</span><span class="sxs-lookup"><span data-stu-id="e9af8-244">iOS</span></span>
   <span data-ttu-id="e9af8-245">Запустить приложение на подключенном устройстве: `cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="e9af8-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="e9af8-246">Запустить приложение в эмуляторе по умолчанию: `cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="e9af8-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="e9af8-247">Убедитесь, что пакет `ios-sim` установлен для запуска в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="e9af8-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="e9af8-248">Дополнительные сведения см. в разделе "Предварительные требования".</span><span class="sxs-lookup"><span data-stu-id="e9af8-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="e9af8-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e9af8-249">Next steps</span></span>
<span data-ttu-id="e9af8-250">Готовый пример (для которого лишь осталось задать конфигурацию) можно найти в [репозитории GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="e9af8-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="e9af8-251">Теперь вы можете приступить к более сложным и содержательным сценариям.</span><span class="sxs-lookup"><span data-stu-id="e9af8-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="e9af8-252">Дополнительные сведения см. в статье [Приступая к работе с веб-интерфейсом API для узла](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e9af8-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
