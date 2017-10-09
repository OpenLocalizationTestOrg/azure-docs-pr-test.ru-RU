---
title: "Azure Active Directory B2C: Использование hello Graph API | Документы Microsoft"
description: "Как toocall hello Graph API для клиента B2C с помощью процесса hello tooautomate удостоверения приложения."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="d379c-103">Azure AD B2C: Использовать Graph API hello</span><span class="sxs-lookup"><span data-stu-id="d379c-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="d379c-104">Клиенты Azure Active Directory (Azure AD) B2C обычно toobe очень большой.</span><span class="sxs-lookup"><span data-stu-id="d379c-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="d379c-105">Это означает, что многие распространенные задачи управления клиента должны toobe выполнены программно.</span><span class="sxs-lookup"><span data-stu-id="d379c-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="d379c-106">Основным примером может служить управление пользователями.</span><span class="sxs-lookup"><span data-stu-id="d379c-106">A primary example is user management.</span></span> <span data-ttu-id="d379c-107">Может потребоваться toomigrate существующий клиент B2C tooa хранилища пользователя.</span><span class="sxs-lookup"><span data-stu-id="d379c-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="d379c-108">Можно toohost регистрации пользователей на веб-узле и создать учетные записи пользователей в вашем каталоге Azure AD B2C фоновом hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="d379c-109">Эти типы задач требуется возможность toocreate hello, чтение, обновление и удаление учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="d379c-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="d379c-110">Эти задачи можно сделать с помощью API Azure AD Graph hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="d379c-111">Для клиентов B2C существует два основного режима взаимодействия с Graph API hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="d379c-112">Для интерактивного, однократного запуска задачи должен работать от имени учетной записи администратора в клиенте B2C hello при выполнении задач hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="d379c-113">Этот режим требует toosign администратора с использованием учетных данных, перед выполнением этого администратору toohello все вызовы Graph API.</span><span class="sxs-lookup"><span data-stu-id="d379c-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="d379c-114">Для автоматических, непрерывные задачи следует использовать некоторый тип учетной записи службы, который предоставляется с задачами управления tooperform hello необходимые права.</span><span class="sxs-lookup"><span data-stu-id="d379c-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="d379c-115">В Azure AD это можно сделать путем регистрации приложения и проверка подлинности tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="d379c-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="d379c-116">Это делается с помощью **идентификатор приложения** , использующий hello [предоставления учетных данных клиента OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="d379c-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="d379c-117">В этом случае приложение hello выступает в качестве себя, а не как пользователь, toocall hello Graph API.</span><span class="sxs-lookup"><span data-stu-id="d379c-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="d379c-118">В этой статье мы обсудим, как tooperform hello вариант автоматического использования.</span><span class="sxs-lookup"><span data-stu-id="d379c-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="d379c-119">toodemonstrate, мы выполним сборку .NET 4.5 `B2CGraphClient` , выполняющего пользователя создания, чтения, обновления и удаления (CRUD).</span><span class="sxs-lookup"><span data-stu-id="d379c-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="d379c-120">Hello будут у клиента Windows интерфейс командной строки (CLI) позволяет вам tooinvoke различные методы.</span><span class="sxs-lookup"><span data-stu-id="d379c-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="d379c-121">Однако hello код toobehave в неинтерактивной, автоматические виде.</span><span class="sxs-lookup"><span data-stu-id="d379c-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="d379c-122">Получение клиента Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d379c-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="d379c-123">До создания приложений или пользователей или вообще взаимодействовать с Azure AD, потребуется клиент Azure AD B2C и учетную запись глобального администратора в клиенте hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="d379c-124">Если у вас нет клиента, создайте его, следуя инструкциям в статье [Предварительная версия Azure Active Directory B2C: создание клиента Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d379c-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="d379c-125">Регистрация приложения в клиенте</span><span class="sxs-lookup"><span data-stu-id="d379c-125">Register your application in your tenant</span></span>
<span data-ttu-id="d379c-126">После того как вы клиента B2C, необходимо tooregister к приложению через hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d379c-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d379c-127">API Graph hello toouse с вашим клиентом B2C, вам потребуется tooregister выделенных приложений с помощью универсального hello *регистрации приложения* колонки в hello портала Azure **не** Azure AD B2C  *Приложения* колонку.</span><span class="sxs-lookup"><span data-stu-id="d379c-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="d379c-128">Нельзя повторно использовать hello существующие B2C приложений, которые зарегистрированы в Azure AD B2C hello *приложений* колонку.</span><span class="sxs-lookup"><span data-stu-id="d379c-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="d379c-129">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d379c-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d379c-130">Выберите клиент Azure AD B2C, выбрав вашей учетной записи в верхнем правом углу hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="d379c-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="d379c-131">Hello левой панели навигации, выберите **более служб**, нажмите кнопку **регистрации приложения**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="d379c-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="d379c-132">Следуйте инструкциям hello и создайте новое приложение.</span><span class="sxs-lookup"><span data-stu-id="d379c-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="d379c-133">Выберите **веб-приложения и API** как тип приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="d379c-134">Укажите **любой URI перенаправления** (например, https://B2CGraphAPI), так как он неважен в этом примере.</span><span class="sxs-lookup"><span data-stu-id="d379c-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="d379c-135">Hello приложение будет показано вверх в списке hello приложений, щелкните ее tooobtain hello **идентификатор приложения** (также известный как идентификатор клиента).</span><span class="sxs-lookup"><span data-stu-id="d379c-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="d379c-136">Скопируйте его, так как он потребуется вам в одном из следующих разделов.</span><span class="sxs-lookup"><span data-stu-id="d379c-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="d379c-137">В колонке параметров hello щелкните **ключей** и добавьте новый раздел (также известный как секрет клиента).</span><span class="sxs-lookup"><span data-stu-id="d379c-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="d379c-138">Также скопируйте его для использования в одном из следующих разделов.</span><span class="sxs-lookup"><span data-stu-id="d379c-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="d379c-139">Настройка разрешений на создание, чтение и обновление для приложения</span><span class="sxs-lookup"><span data-stu-id="d379c-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="d379c-140">Теперь необходимо tooconfigure вашей tooget приложения, которые hello все необходимые разрешения toocreate, чтение, обновление и удаление пользователей.</span><span class="sxs-lookup"><span data-stu-id="d379c-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="d379c-141">Продолжить в Здравствуйте колонке регистрации приложения портала Azure, выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="d379c-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="d379c-142">В колонке параметров hello щелкните **требуемые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="d379c-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="d379c-143">В колонке hello необходимые разрешения, нажмите кнопку **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d379c-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="d379c-144">В колонке hello разрешить доступ, выберите hello **чтение и запись данных каталога** разрешений у **разрешения приложения** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d379c-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="d379c-145">Наконец, в колонке hello необходимые разрешения, щелкните hello **GRANT, предоставление разрешений** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d379c-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="d379c-146">Теперь у вас есть приложение, имеющее разрешения toocreate, чтение и обновление пользователей из вашего клиента B2C.</span><span class="sxs-lookup"><span data-stu-id="d379c-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="d379c-147">Настройка разрешений на удаление для приложения</span><span class="sxs-lookup"><span data-stu-id="d379c-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="d379c-148">В настоящее время hello *чтение и запись данных каталога* разрешение **не** включают возможность toodo hello удалений, например, удаление пользователей.</span><span class="sxs-lookup"><span data-stu-id="d379c-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="d379c-149">Если требуется toogive пользователей toodelete возможности приложения hello, необходим toodo эти дополнительные действия, которые включают PowerShell, в противном случае toohello Далее раздел можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="d379c-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="d379c-150">Во-первых, загрузите и установите hello [Microsoft Online Services помощник по входу](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="d379c-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="d379c-151">Затем загрузите и установите hello [64-разрядного модуля Azure Active Directory для Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="d379c-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="d379c-152">После установки модуля PowerShell hello, откройте PowerShell и подключения клиента tooyour B2C.</span><span class="sxs-lookup"><span data-stu-id="d379c-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="d379c-153">После запуска `Get-Credential`, то предложит ввести имя пользователя и пароль, введите имя пользователя hello и пароль учетной записи администратора клиента B2C.</span><span class="sxs-lookup"><span data-stu-id="d379c-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d379c-154">Требуется toouse B2C учетную запись администратора, **локального** toohello B2C клиента.</span><span class="sxs-lookup"><span data-stu-id="d379c-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="d379c-155">Эти учетные записи выглядят следующим образом: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d379c-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="d379c-156">Теперь мы будем использовать hello **идентификатор приложения** в скрипте hello ниже tooassign hello приложения hello роли учетной записи пользователя администратор которого оно toodelete пользователям разрешается.</span><span class="sxs-lookup"><span data-stu-id="d379c-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="d379c-157">Эти роли имеют хорошо известные идентификаторы, поэтому все, что нужно toodo является входным вашей **идентификатор приложения** в hello приведенный ниже сценарий.</span><span class="sxs-lookup"><span data-stu-id="d379c-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="d379c-158">Приложение теперь также имеет разрешения toodelete пользователей из вашего клиента B2C.</span><span class="sxs-lookup"><span data-stu-id="d379c-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="d379c-159">Загрузить, настройки и создания кода образца hello</span><span class="sxs-lookup"><span data-stu-id="d379c-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="d379c-160">Во-первых Загрузите образец кода hello и его запуска.</span><span class="sxs-lookup"><span data-stu-id="d379c-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="d379c-161">После этого мы сможем рассмотреть его подробнее.</span><span class="sxs-lookup"><span data-stu-id="d379c-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="d379c-162">Вы можете [загрузить пример кода hello как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="d379c-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="d379c-163">Его можно клонировать в необходимый каталог.</span><span class="sxs-lookup"><span data-stu-id="d379c-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="d379c-164">Откройте hello `B2CGraphClient\B2CGraphClient.sln` решения Visual Studio в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d379c-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="d379c-165">В hello `B2CGraphClient` проекта, откройте hello файл `App.config`.</span><span class="sxs-lookup"><span data-stu-id="d379c-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="d379c-166">Замените параметры три приложения hello собственные значения.</span><span class="sxs-lookup"><span data-stu-id="d379c-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="d379c-167">После этого щелкните правой кнопкой мыши на hello `B2CGraphClient` решение и постройте образец hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="d379c-168">Если вам удастся выполнить это действие, в каталоге `B2CGraphClient\bin\Debug` появится исполняемый файл `B2C.exe`.</span><span class="sxs-lookup"><span data-stu-id="d379c-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="d379c-169">Создавать пользовательские операции CRUD с помощью hello Graph API</span><span class="sxs-lookup"><span data-stu-id="d379c-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="d379c-170">Откройте hello toouse B2CGraphClient, `cmd` Windows команд запроса и изменить ваш каталог toohello `Debug` каталога.</span><span class="sxs-lookup"><span data-stu-id="d379c-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="d379c-171">Затем запустите hello `B2C Help` команды.</span><span class="sxs-lookup"><span data-stu-id="d379c-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="d379c-172">Появится краткое описание каждой команды.</span><span class="sxs-lookup"><span data-stu-id="d379c-172">This will display a brief description of each command.</span></span> <span data-ttu-id="d379c-173">Каждый раз при вызове одной из этих команд `B2CGraphClient` делает запрос toohello API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="d379c-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="d379c-174">Получение маркера доступа</span><span class="sxs-lookup"><span data-stu-id="d379c-174">Get an access token</span></span>
<span data-ttu-id="d379c-175">Любой запрос toohello Graph API требуется маркер доступа для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d379c-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="d379c-176">`B2CGraphClient`Открытая библиотеку проверки подлинности Active Directory (ADAL) использует hello toohelp получения маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="d379c-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="d379c-177">ADAL упрощает получение маркеров, так как предоставляет простой API и выполняет некоторые важные действия, такие как кэширование маркеров доступа.</span><span class="sxs-lookup"><span data-stu-id="d379c-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="d379c-178">У вас нет токенов ADAL tooget toouse, хотя.</span><span class="sxs-lookup"><span data-stu-id="d379c-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="d379c-179">Их можно получать, составляя HTTP-запросы вручную.</span><span class="sxs-lookup"><span data-stu-id="d379c-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="d379c-180">Этот пример кода использует ADAL v2 в порядке toocommunicate с hello Graph API.</span><span class="sxs-lookup"><span data-stu-id="d379c-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="d379c-181">Необходимо использовать ADAL версии 2 или 3 в маркеров доступа tooget заказа, которые можно использовать с hello API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="d379c-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="d379c-182">Когда `B2CGraphClient` запускается, он создает экземпляр hello `B2CGraphClient` класса.</span><span class="sxs-lookup"><span data-stu-id="d379c-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="d379c-183">Устанавливает Hello конструктор для этого класса проверки подлинности ADAL формирование шаблонов:</span><span class="sxs-lookup"><span data-stu-id="d379c-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="d379c-184">Мы будем использовать hello `B2C Get-User` команду в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d379c-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="d379c-185">Когда `B2C Get-User` вызывается без дополнительные входные данные, hello hello вызовов CLI `B2CGraphClient.GetAllUsers(...)` метод.</span><span class="sxs-lookup"><span data-stu-id="d379c-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="d379c-186">Этот метод вызывает метод `B2CGraphClient.SendGraphGetRequest(...)`, который отправляет Graph API toohello запрос HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="d379c-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="d379c-187">Прежде чем `B2CGraphClient.SendGraphGetRequest(...)` отправляет Здравствуйте запрос GET, он сначала получает токен доступа с помощью ADAL:</span><span class="sxs-lookup"><span data-stu-id="d379c-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="d379c-188">Вы может получить маркер доступа для hello Graph API, вызывающему Привет ADAL `AuthenticationContext.AcquireToken(...)` метод.</span><span class="sxs-lookup"><span data-stu-id="d379c-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="d379c-189">ADAL возвращает `access_token` , представляющий удостоверение приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="d379c-190">Чтение пользователей</span><span class="sxs-lookup"><span data-stu-id="d379c-190">Read users</span></span>
<span data-ttu-id="d379c-191">При необходимости tooget список пользователей или получить конкретного пользователя из hello Graph API можно отправлять HTTP- `GET` запроса toohello `/users` конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d379c-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="d379c-192">Запрос для всех пользователей hello в клиенте выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d379c-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="d379c-193">toosee этот запрос запуска:</span><span class="sxs-lookup"><span data-stu-id="d379c-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="d379c-194">Существует два toonote важных событий.</span><span class="sxs-lookup"><span data-stu-id="d379c-194">There are two important things toonote:</span></span>

* <span data-ttu-id="d379c-195">Hello токена доступа, полученного через ADAL добавляется toohello `Authorization` заголовок с помощью hello `Bearer` схемы.</span><span class="sxs-lookup"><span data-stu-id="d379c-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="d379c-196">Для клиентов B2C, необходимо использовать параметр запроса hello `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d379c-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="d379c-197">Оба эти данные обрабатываются в hello `B2CGraphClient.SendGraphGetRequest(...)` метод:</span><span class="sxs-lookup"><span data-stu-id="d379c-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="d379c-198">Создание учетных записей пользователей-клиентов</span><span class="sxs-lookup"><span data-stu-id="d379c-198">Create consumer user accounts</span></span>
<span data-ttu-id="d379c-199">При создании учетных записей пользователей в клиенте B2C можно отправлять HTTP- `POST` запроса toohello `/users` конечной точки:</span><span class="sxs-lookup"><span data-stu-id="d379c-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="d379c-200">Большая часть этих свойств в данном запросе являются необходимые toocreate пользователей клиента.</span><span class="sxs-lookup"><span data-stu-id="d379c-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="d379c-201">toolearn, щелкните пункт [здесь](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="d379c-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="d379c-202">Обратите внимание, что hello `//` комментарии были включены для иллюстрации.</span><span class="sxs-lookup"><span data-stu-id="d379c-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="d379c-203">Их не нужно добавлять в запрос.</span><span class="sxs-lookup"><span data-stu-id="d379c-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="d379c-204">toosee запрос hello, выполните одну из следующих команд hello:</span><span class="sxs-lookup"><span data-stu-id="d379c-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="d379c-205">Hello `Create-User` команда принимает JSON-файл в качестве входного параметра.</span><span class="sxs-lookup"><span data-stu-id="d379c-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="d379c-206">Он содержит представление JSON объекта пользователя.</span><span class="sxs-lookup"><span data-stu-id="d379c-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="d379c-207">Существуют два файла .json образец в примере кода hello: `usertemplate-email.json` и `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="d379c-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="d379c-208">Вы можете изменить эти файлы toosuit вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="d379c-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="d379c-209">В дополнение к этому toohello обязательные поля выше, несколько дополнительных полей, которые можно использовать, включаются в эти файлы.</span><span class="sxs-lookup"><span data-stu-id="d379c-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="d379c-210">Сведения о необязательных полей hello можно найти в hello [Справочник по API Azure AD Graph сущности](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="d379c-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="d379c-211">Можно увидеть, как создается запрос POST hello в `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="d379c-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="d379c-212">Он присоединяет toohello токена доступа `Authorization` заголовок запроса hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="d379c-213">Затем задается параметр `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d379c-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="d379c-214">Он включает hello объекта пользователя JSON в тексте hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="d379c-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="d379c-215">Hello учетные записи, следует ли toomigrate из существующего хранилища пользователя имеет нижней стойкость пароля, чем hello [стойкость надежный пароль, обеспечиваемая Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), вы можете отключить hello надежного пароля с помощью hello `DisableStrongPassword`значение в hello `passwordPolicies` свойство.</span><span class="sxs-lookup"><span data-stu-id="d379c-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="d379c-216">Например, можно изменить hello создайте пользовательский запрос, приведенный выше, следующим образом: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="d379c-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="d379c-217">Обновление учетных записей пользователей-клиентов</span><span class="sxs-lookup"><span data-stu-id="d379c-217">Update consumer user accounts</span></span>
<span data-ttu-id="d379c-218">При обновлении пользовательские объекты, процесс hello — примерно toohello один использовать toocreate пользовательские объекты.</span><span class="sxs-lookup"><span data-stu-id="d379c-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="d379c-219">Однако этот процесс использует hello HTTP `PATCH` метод:</span><span class="sxs-lookup"><span data-stu-id="d379c-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="d379c-220">Попробуйте tooupdate пользователя, обновив файлы JSON с новыми данными.</span><span class="sxs-lookup"><span data-stu-id="d379c-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="d379c-221">Затем можно использовать `B2CGraphClient` toorun одной из этих команд:</span><span class="sxs-lookup"><span data-stu-id="d379c-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="d379c-222">Проверять hello `B2CGraphClient.SendGraphPatchRequest(...)` метод подробные сведения о том, как toosend этого запроса.</span><span class="sxs-lookup"><span data-stu-id="d379c-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="d379c-223">Поиск пользователей</span><span class="sxs-lookup"><span data-stu-id="d379c-223">Search users</span></span>
<span data-ttu-id="d379c-224">Искать пользователей в клиенте B2C можно разными способами.</span><span class="sxs-lookup"><span data-stu-id="d379c-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="d379c-225">Один с помощью hello пользователя идентификатор объекта или две, используя идентификатор входа пользователя hello (т. е. hello `signInNames` свойство).</span><span class="sxs-lookup"><span data-stu-id="d379c-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="d379c-226">Выполните одну из следующих hello команд toosearch для конкретного пользователя:</span><span class="sxs-lookup"><span data-stu-id="d379c-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="d379c-227">Вот несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="d379c-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="d379c-228">Удаление пользователей</span><span class="sxs-lookup"><span data-stu-id="d379c-228">Delete users</span></span>
<span data-ttu-id="d379c-229">Hello процесс удаления пользователя достаточно прост.</span><span class="sxs-lookup"><span data-stu-id="d379c-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="d379c-230">Используйте hello HTTP `DELETE` метода и конструкции hello URL-адрес с hello исправьте идентификатор объекта:</span><span class="sxs-lookup"><span data-stu-id="d379c-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="d379c-231">toosee пример, введите этот команды и представление hello запроса delete, печатной toohello консоли:</span><span class="sxs-lookup"><span data-stu-id="d379c-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="d379c-232">Проверять hello `B2CGraphClient.SendGraphDeleteRequest(...)` метод подробные сведения о том, как toosend этого запроса.</span><span class="sxs-lookup"><span data-stu-id="d379c-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="d379c-233">Можно выполнять многие другие действия с hello API Azure AD Graph в toouser управления сложения.</span><span class="sxs-lookup"><span data-stu-id="d379c-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="d379c-234">Дополнительные сведения о каждом действии и примеры запросов см. в [справочнике по API Graph для Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="d379c-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="d379c-235">Использование настраиваемых атрибутов</span><span class="sxs-lookup"><span data-stu-id="d379c-235">Use custom attributes</span></span>
<span data-ttu-id="d379c-236">Большинство приложения-потребители должны toostore своего рода пользовательские сведения профиля.</span><span class="sxs-lookup"><span data-stu-id="d379c-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="d379c-237">Это можно сделать одним из способов является toodefine настраиваемого атрибута в клиенте B2C.</span><span class="sxs-lookup"><span data-stu-id="d379c-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="d379c-238">Затем можно считать этот атрибут hello так же, как обрабатывать любые другие свойства в объекте пользователя.</span><span class="sxs-lookup"><span data-stu-id="d379c-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="d379c-239">Можно обновить атрибут hello атрибут hello delete, запрос по атрибуту hello, отправка hello атрибут в качестве утверждения в маркеры входа в систему и многое другое.</span><span class="sxs-lookup"><span data-stu-id="d379c-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="d379c-240">toodefine настраиваемого атрибута в клиенте B2C см hello [ссылку настраиваемого атрибута B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="d379c-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="d379c-241">Можно просмотреть hello настраиваемых атрибутов, определенных в B2C клиента с помощью `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="d379c-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="d379c-242">Hello вывода этих функций показывает hello сведения каждого пользовательского атрибута, такие как:</span><span class="sxs-lookup"><span data-stu-id="d379c-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="d379c-243">Можно использовать полное имя, например hello `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, как свойство объектов-пользователей.</span><span class="sxs-lookup"><span data-stu-id="d379c-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="d379c-244">Добавьте в файл .json hello новое свойство и значение для свойства hello, а затем запустите:</span><span class="sxs-lookup"><span data-stu-id="d379c-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="d379c-245">Использование `B2CGraphClient`позволяет получить приложение-службу, которое обеспечивает управление пользователями клиента B2C программным путем.</span><span class="sxs-lookup"><span data-stu-id="d379c-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="d379c-246">`B2CGraphClient`использует собственный toohello tooauthenticate удостоверение приложения Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="d379c-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="d379c-247">Кроме того, B2CGraphClient получает маркеры, используя секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="d379c-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="d379c-248">Добавляя эту функцию в свое приложение, учитывайте некоторые ключевые особенности приложений B2C.</span><span class="sxs-lookup"><span data-stu-id="d379c-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="d379c-249">Необходимо toogrant hello приложения hello соответствующие разрешения в клиенте hello.</span><span class="sxs-lookup"><span data-stu-id="d379c-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="d379c-250">На данном этапе необходимо токены доступа tooget toouse ADAL (не MSAL).</span><span class="sxs-lookup"><span data-stu-id="d379c-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="d379c-251">(Кроме того, сообщения протокола можно отправлять напрямую, не используя библиотеку.)</span><span class="sxs-lookup"><span data-stu-id="d379c-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="d379c-252">При вызове Graph API hello использовать `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d379c-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="d379c-253">При создании и обновлении пользователей-клиентов требуются некоторые свойства, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="d379c-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="d379c-254">Если у вас есть вопросы или запросы для действия, которые вы хотите tooperform с помощью Graph API hello на клиенте B2C комментарий в этой статье или файл проблему в репозитории примеров кода hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="d379c-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>

