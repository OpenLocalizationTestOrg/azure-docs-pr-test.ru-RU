---
title: "Приступая к работе AD Cordova aaaAzure | Документы Microsoft"
description: "Как toobuild приложения Cordova, интегрируется с Azure AD для входа в систему и вызывает Azure API, защищенные AD с помощью OAuth."
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
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="ba81e-103">Интеграция Azure AD с приложением Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="ba81e-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ba81e-104">Можно использовать Apache Cordova toodevelop HTML5 и JavaScript приложения, работающие на мобильных устройствах, как полноценные собственного приложения.</span><span class="sxs-lookup"><span data-stu-id="ba81e-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="ba81e-105">В Azure Active Directory (Azure AD) можно добавить приложений Cordova tooyour возможности проверки подлинности корпоративного уровня.</span><span class="sxs-lookup"><span data-stu-id="ba81e-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="ba81e-106">Подключаемый модуль Cordova использует собственные пакеты SDK Azure AD для приложений iOS, Android, Магазина Windows и Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="ba81e-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="ba81e-107">С помощью подключаемого модуля, можно усилить приложения toosupport вход в систему с учетными записями пользователей Windows Server Active Directory, получить доступ tooOffice 365 и API-интерфейсов Azure и даже защитить вызовы tooyour собственные пользовательские веб-API.</span><span class="sxs-lookup"><span data-stu-id="ba81e-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="ba81e-108">В этом учебнике мы будем использовать hello подключаемых модулей Apache Cordova для библиотеки проверки подлинности Active Directory (ADAL) tooimprove простое приложение, добавив hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="ba81e-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="ba81e-109">реализация проверки подлинности пользователя и получения маркера путем добавления всего нескольких строк кода;</span><span class="sxs-lookup"><span data-stu-id="ba81e-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="ba81e-110">Использовать этот токен tooinvoke hello Graph API tooquery этого каталога и отображения результатов hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="ba81e-111">Проверка подлинности toominimize ADAL кэша маркера hello запрашивает пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="ba81e-112">toomake этих усовершенствований, необходимо:</span><span class="sxs-lookup"><span data-stu-id="ba81e-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="ba81e-113">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ba81e-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="ba81e-114">Добавьте код tooyour приложения toorequest маркеры.</span><span class="sxs-lookup"><span data-stu-id="ba81e-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="ba81e-115">Добавление токена hello toouse код для выполнения запросов к Graph API hello и отображения результатов.</span><span class="sxs-lookup"><span data-stu-id="ba81e-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="ba81e-116">Создать проект развертывания hello Cordova со всех платформ hello требуется tootarget, добавить hello Cordova ADAL подключаемого модуля и тестирование решения hello в эмуляторах.</span><span class="sxs-lookup"><span data-stu-id="ba81e-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba81e-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ba81e-117">Prerequisites</span></span>
<span data-ttu-id="ba81e-118">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="ba81e-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="ba81e-119">Клиент Azure AD с учетной записью с правами на разработку приложений.</span><span class="sxs-lookup"><span data-stu-id="ba81e-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="ba81e-120">Среда разработки, которая настроена toouse Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ba81e-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="ba81e-121">Если оба уже установлено, перейдите непосредственно toostep 1.</span><span class="sxs-lookup"><span data-stu-id="ba81e-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="ba81e-122">Если у вас нет клиента Azure AD, используйте hello [инструкции tooget один](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ba81e-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="ba81e-123">Если у вас нет Apache Cordova на компьютере, установите hello следующее:</span><span class="sxs-lookup"><span data-stu-id="ba81e-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="ba81e-124">Git.</span><span class="sxs-lookup"><span data-stu-id="ba81e-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="ba81e-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="ba81e-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="ba81e-126">[Cordova CLI](https://cordova.apache.org/) (можно легко установить через диспетчер пакетов NPM: `npm install -g cordova`).</span><span class="sxs-lookup"><span data-stu-id="ba81e-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="ba81e-127">Hello предыдущих установок должен работать на hello ПК и hello Mac.</span><span class="sxs-lookup"><span data-stu-id="ba81e-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="ba81e-128">У каждой целевой платформы свои требования.</span><span class="sxs-lookup"><span data-stu-id="ba81e-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="ba81e-129">toobuild и запуска приложения для Планшетных Windows или Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="ba81e-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="ba81e-130">Установите [Visual Studio 2013 для Windows с обновлением 2 или более поздней версии](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express или другая версия) или [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="ba81e-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="ba81e-131">toobuild и запустите приложение для iOS:</span><span class="sxs-lookup"><span data-stu-id="ba81e-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="ba81e-132">Установите Xcode 6.x или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ba81e-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="ba81e-133">Загрузите его из hello [сайта разработчика Apple](http://developer.apple.com/downloads) или hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="ba81e-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="ba81e-134">Установите [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="ba81e-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="ba81e-135">Он используется toostart приложений iOS в симуляторе iOS с hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="ba81e-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="ba81e-136">(Его можно легко установить через hello терминалов: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="ba81e-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="ba81e-137">toobuild и запуска приложения для Android:</span><span class="sxs-lookup"><span data-stu-id="ba81e-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="ba81e-138">Установить [пакет средств разработки Java (JDK) версии 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) или более поздней.</span><span class="sxs-lookup"><span data-stu-id="ba81e-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="ba81e-139">Убедитесь, что `JAVA_HOME` (переменной среды) правильно установлен в соответствии с путь установки JDK toohello (например, C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="ba81e-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="ba81e-140">Установка [пакета SDK для Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) и добавить hello `<android-sdk-location>\tools` tooyour расположение (например, C:\tools\Android\android-sdk\tools) `PATH` переменной среды.</span><span class="sxs-lookup"><span data-stu-id="ba81e-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="ba81e-141">Откройте диспетчер Android SDK Manager (например, через hello терминалов: `android`) и установить:</span><span class="sxs-lookup"><span data-stu-id="ba81e-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="ba81e-142">*Android 5.0.1 (API уровня 21)* ;</span><span class="sxs-lookup"><span data-stu-id="ba81e-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="ba81e-143">*Android SDK Build Tools* версии 19.1.0 или более поздней;</span><span class="sxs-lookup"><span data-stu-id="ba81e-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="ba81e-144">*Android Support Repository* (дополнительно).</span><span class="sxs-lookup"><span data-stu-id="ba81e-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="ba81e-145">любой экземпляр эмулятора по умолчанию не предоставляет возможность Hello пакета SDK для Android.</span><span class="sxs-lookup"><span data-stu-id="ba81e-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="ba81e-146">Сделать это с `android avd` из hello терминалов и затем выбрав **создать**, если требуется, чтобы приложение Android toorun hello в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="ba81e-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="ba81e-147">Рекомендуемый уровень API — 19 или выше.</span><span class="sxs-lookup"><span data-stu-id="ba81e-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="ba81e-148">Дополнительные сведения о hello Android эмулятора и параметрами создания см. в разделе [диспетчер AVD](http://developer.android.com/tools/help/avd-manager.html) на сайте Android hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="ba81e-149">Шаг 1. Регистрация приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba81e-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="ba81e-150">Этот шаг не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="ba81e-150">This step is optional.</span></span> <span data-ttu-id="ba81e-151">Этот учебник предоставляет предварительную подготовку значения, которые можно использовать toosee образец hello без выполнения любой инициализации своим собственным клиентом.</span><span class="sxs-lookup"><span data-stu-id="ba81e-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="ba81e-152">Тем не менее рекомендуется выполнить этот шаг и ближе познакомиться с hello процесса, так как он понадобится, при создании собственных приложений.</span><span class="sxs-lookup"><span data-stu-id="ba81e-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="ba81e-153">Azure AD выдает токены tooonly известные приложений.</span><span class="sxs-lookup"><span data-stu-id="ba81e-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="ba81e-154">Прежде чем использовать Azure AD из приложения, необходимо toocreate запись для него в клиенте.</span><span class="sxs-lookup"><span data-stu-id="ba81e-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="ba81e-155">tooregister новое приложение в клиенте:</span><span class="sxs-lookup"><span data-stu-id="ba81e-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="ba81e-156">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba81e-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ba81e-157">На верхней панели hello выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ba81e-157">On hello top bar, click your account.</span></span> <span data-ttu-id="ba81e-158">В hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="ba81e-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="ba81e-159">Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ba81e-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ba81e-160">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ba81e-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="ba81e-161">Следуйте инструкциям hello и создать **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="ba81e-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="ba81e-162">(Хотя приложения Cordova основаны на HTML, мы создаем собственное клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="ba81e-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="ba81e-163">Hello **собственное клиентское приложение** должен быть выбран вариант, или не будет работать приложение hello.)</span><span class="sxs-lookup"><span data-stu-id="ba81e-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="ba81e-164">**Имя** описывает toousers вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ba81e-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="ba81e-165">**URI перенаправления** — hello URI, который использовал tooreturn маркеры tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="ba81e-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="ba81e-166">Введите **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="ba81e-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="ba81e-167">После завершения регистрации Azure AD присваивает значение приложении tooyour приложения уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ba81e-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="ba81e-168">Вам потребуется это значение в последующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="ba81e-169">Его можно найти на вкладке приложения hello созданного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="ba81e-170">toorun `DirSearchClient Sample`, предоставьте hello hello созданного приложения разрешение tooquery API Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="ba81e-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="ba81e-171">Из hello **параметры** выберите **требуемые разрешения**, а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="ba81e-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="ba81e-172">Hello приложения Azure Active Directory, выберите **Microsoft Graph** как hello API и добавьте hello **доступ к каталогу hello как пользователя, выполнившего вход hello** разрешение в списке **полномочные Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="ba81e-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="ba81e-173">Это позволяет вашей hello tooquery приложения Graph API для пользователей.</span><span class="sxs-lookup"><span data-stu-id="ba81e-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="ba81e-174">Шаг 2: Клонирование репозитория приложения образец hello</span><span class="sxs-lookup"><span data-stu-id="ba81e-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="ba81e-175">Оболочки или командной строки введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ba81e-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="ba81e-176">Шаг 3: Создание приложения Cordova hello</span><span class="sxs-lookup"><span data-stu-id="ba81e-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="ba81e-177">Существует несколько способов toocreate Cordova приложения.</span><span class="sxs-lookup"><span data-stu-id="ba81e-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="ba81e-178">В этом учебнике мы будем использовать hello Cordova интерфейс командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="ba81e-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="ba81e-179">Оболочки или командной строки введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ba81e-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="ba81e-180">Эта команда создает структуру папок hello и формирование шаблонов для проекта Cordova hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="ba81e-181">Переместите новую папку DirSearchClient toohello:</span><span class="sxs-lookup"><span data-stu-id="ba81e-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="ba81e-182">Скопируйте содержимое hello hello начального проекта во вложенной папке hello www с помощью диспетчера файлов или следующую команду в оболочка hello:</span><span class="sxs-lookup"><span data-stu-id="ba81e-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="ba81e-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="ba81e-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="ba81e-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="ba81e-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="ba81e-185">Добавьте белого списка hello подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="ba81e-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="ba81e-186">Это требуется для вызова Graph API hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="ba81e-187">Добавьте все платформы hello, что требуется toosupport.</span><span class="sxs-lookup"><span data-stu-id="ba81e-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="ba81e-188">toohave рабочий образец, необходимо tooexecute по крайней мере один из следующих команд hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="ba81e-189">Обратите внимание, что не быть может tooemulate iOS в Windows или эмулировать Windows на компьютере Mac.</span><span class="sxs-lookup"><span data-stu-id="ba81e-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="ba81e-190">Добавьте hello ADAL для проекта tooyour подключаемого модуля Cordova:</span><span class="sxs-lookup"><span data-stu-id="ba81e-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="ba81e-191">Шаг 4: Добавление кода tooauthenticate пользователей и получать токены из Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba81e-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="ba81e-192">приложение Hello, которое вы разрабатываете в этом учебнике будет предоставляют возможность поиска каталог с простым.</span><span class="sxs-lookup"><span data-stu-id="ba81e-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="ba81e-193">Hello пользователя можно введите псевдоним hello любого пользователя в каталоге hello и визуализировать некоторые основные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="ba81e-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="ba81e-194">Hello начальный проект содержит определение hello hello основной пользовательский интерфейс приложения hello (в www/index.html) и формирование шаблонов hello, настраивающий событий базовое приложение циклов привязки интерфейса пользователя и результаты логики отображения (в www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="ba81e-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="ba81e-195">Hello только слева для вас останется tooadd hello логику, которая реализует идентификаторов задач.</span><span class="sxs-lookup"><span data-stu-id="ba81e-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="ba81e-196">Hello прежде всего необходимо toodo в коде является вводит значения протокола hello, используемые для идентификации приложения Azure AD и hello ресурсы, предназначенные.</span><span class="sxs-lookup"><span data-stu-id="ba81e-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="ba81e-197">Эти значения будут запросы маркеров используется tooconstruct hello позже.</span><span class="sxs-lookup"><span data-stu-id="ba81e-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="ba81e-198">Вставьте следующий фрагмент кода hello верхней части файла index.js hello hello:</span><span class="sxs-lookup"><span data-stu-id="ba81e-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="ba81e-199">Hello `redirectUri` и `clientId` значения должны совпадать hello значения, которые описывают приложение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba81e-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="ba81e-200">Можно найти соответствующие hello **Настройка** вкладке hello портал Azure, как описано в шаге 1 ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ba81e-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="ba81e-201">Если вы выбрали для вашего собственного клиента не Регистрация нового приложения, можно просто вставить hello заранее настроенные значения как есть.</span><span class="sxs-lookup"><span data-stu-id="ba81e-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="ba81e-202">Можно просматривать выполняется образец hello, хотя рекомендуется всегда создавать записи для приложения, предназначенные для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="ba81e-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="ba81e-203">Добавьте код запроса маркера hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-203">Next, add hello token request code.</span></span> <span data-ttu-id="ba81e-204">Вставьте следующий фрагмент кода между hello hello `search` и `renderData` определения:</span><span class="sxs-lookup"><span data-stu-id="ba81e-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="ba81e-205">Рассмотрим эту функцию, разбив ее на две основные части.</span><span class="sxs-lookup"><span data-stu-id="ba81e-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="ba81e-206">В этом примере является спроектированный toowork с любым клиентом как противоположность toobeing привязан tooa одну из них.</span><span class="sxs-lookup"><span data-stu-id="ba81e-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="ba81e-207">Она использует hello конечную «/ Общие», которая позволяет любой учетной записи пользователя tooenter hello во время проверки подлинности и направляет клиента toohello hello запроса, к которой он принадлежит.</span><span class="sxs-lookup"><span data-stu-id="ba81e-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="ba81e-208">Эта часть hello метод проверяет toosee кэш ADAL hello, если токен уже хранится.</span><span class="sxs-lookup"><span data-stu-id="ba81e-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="ba81e-209">В этом случае hello способе клиентов hello токен hello происхождения для повторной инициализации ADAL.</span><span class="sxs-lookup"><span data-stu-id="ba81e-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="ba81e-210">Это — tooavoid необходимые дополнительные запросы, поскольку использование hello объекта «/ общие» всегда приводит попросить пользователя tooenter hello новую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ba81e-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="ba81e-211">во второй части Hello hello метод выполняет hello правильный запрос маркера.</span><span class="sxs-lookup"><span data-stu-id="ba81e-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="ba81e-212">Hello `acquireTokenSilentAsync` метод запрашивает ADAL tooreturn маркер hello указанного ресурса без отображения любой UI.</span><span class="sxs-lookup"><span data-stu-id="ba81e-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="ba81e-213">Что может произойти, если hello кэша уже есть подходящий описателя хранения, или если токен обновления можно использовать tooget новый маркер доступа без отображения предупреждений.</span><span class="sxs-lookup"><span data-stu-id="ba81e-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="ba81e-214">В случае неудачной попытки, мы прибегнуть к `acquireTokenAsync`--наглядно будет предложено hello tooauthenticate пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba81e-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="ba81e-215">Теперь, когда у нас есть токен hello, мы наконец вызова Graph API hello и hello поискового запроса, который необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="ba81e-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="ba81e-216">Вставьте следующий фрагмент кода ниже hello hello `authenticate` определение:</span><span class="sxs-lookup"><span data-stu-id="ba81e-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
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
<span data-ttu-id="ba81e-217">файлы начального приветствия предоставлен простой UX для ввода псевдонима пользователя в текстовом поле.</span><span class="sxs-lookup"><span data-stu-id="ba81e-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="ba81e-218">Этот метод используется, значение tooconstruct запрос, использовать ее в сочетании с маркером доступа hello, отправить его tooMicrosoft Graph и проанализировать результаты hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="ba81e-219">Hello `renderData` берет на себя метод, уже присутствует в файле начального приветствия, наглядно представить результаты hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="ba81e-220">Шаг 5: Запуск приложения hello</span><span class="sxs-lookup"><span data-stu-id="ba81e-220">Step 5: Run hello app</span></span>
<span data-ttu-id="ba81e-221">Приложение будет toorun все готово.</span><span class="sxs-lookup"><span data-stu-id="ba81e-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="ba81e-222">Его работы является простым: при запуске приложение hello, введите псевдоним hello hello пользователя необходимо toolook, а затем нажмите кнопку hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="ba81e-223">Будет предложено ввести учетные данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ba81e-223">You're prompted for authentication.</span></span> <span data-ttu-id="ba81e-224">После успешной проверки подлинности и успешного поиска отображаются атрибуты hello hello поиск пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba81e-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="ba81e-225">Последующие запуски выполнит поиск hello без отображения предупреждений, благодаря использованию toohello наличие hello ранее получены маркера в кэше.</span><span class="sxs-lookup"><span data-stu-id="ba81e-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="ba81e-226">Hello конкретные действия для запуска приложения hello зависят от платформы.</span><span class="sxs-lookup"><span data-stu-id="ba81e-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="ba81e-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="ba81e-227">Windows 10</span></span>
   <span data-ttu-id="ba81e-228">Планшет или ПК: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="ba81e-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="ba81e-229">Мобильных устройств (требуется tooa подключенное устройство Windows 10 Mobile PC):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="ba81e-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="ba81e-230">Во время первого запуска hello вас попросят toosign в лицензию разработчика.</span><span class="sxs-lookup"><span data-stu-id="ba81e-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="ba81e-231">Дополнительные сведения см. в статье [Получение лицензии разработчика](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba81e-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="ba81e-232">Планшеты или компьютеры с Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ba81e-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="ba81e-233">Во время первого запуска hello вас попросят toosign в лицензию разработчика.</span><span class="sxs-lookup"><span data-stu-id="ba81e-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="ba81e-234">Дополнительные сведения см. в статье [Получение лицензии разработчика](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba81e-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="ba81e-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="ba81e-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="ba81e-236">toorun на подключенном устройстве:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="ba81e-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="ba81e-237">toorun на эмулятор по умолчанию hello:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="ba81e-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="ba81e-238">Используйте `cordova run windows --list -- --phone` toosee все доступные целевые объекты и `cordova run windows --target=<target_name> -- --phone` toorun приложения hello на конкретном устройстве или эмуляторе (например, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="ba81e-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="ba81e-239">Android</span><span class="sxs-lookup"><span data-stu-id="ba81e-239">Android</span></span>
   <span data-ttu-id="ba81e-240">toorun на подключенном устройстве:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="ba81e-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="ba81e-241">toorun на эмулятор по умолчанию hello:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="ba81e-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="ba81e-242">Убедитесь, что вы создали экземпляр эмулятор из диспетчера AVD, как описано ранее в подразделе «Необходимые условия» hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="ba81e-243">Используйте `cordova run android --list` toosee все доступные целевые объекты и `cordova run android --target=<target_name>` toorun приложения hello на конкретном устройстве или эмуляторе (например, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="ba81e-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="ba81e-244">iOS</span><span class="sxs-lookup"><span data-stu-id="ba81e-244">iOS</span></span>
   <span data-ttu-id="ba81e-245">toorun на подключенном устройстве:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="ba81e-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="ba81e-246">toorun на эмулятор по умолчанию hello:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="ba81e-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="ba81e-247">Убедитесь, что у вас есть hello `ios-sim` toorun установлен пакет на эмуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="ba81e-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="ba81e-248">Дополнительные сведения см. в разделе hello «необходимые условия» раздела.</span><span class="sxs-lookup"><span data-stu-id="ba81e-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="ba81e-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba81e-249">Next steps</span></span>
<span data-ttu-id="ba81e-250">Для ссылки, пример hello завершена (без настройки) доступен в [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="ba81e-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="ba81e-251">Вы можете теперь сценарии перемещения на toomore advanced (и другие интересные).</span><span class="sxs-lookup"><span data-stu-id="ba81e-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="ba81e-252">Может потребоваться tootry: [защитить веб-API Node.js в Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ba81e-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
