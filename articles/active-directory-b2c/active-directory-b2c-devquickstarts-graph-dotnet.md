---
title: "Azure Active Directory B2C: использование API Graph | Документация Майкрософт"
description: "Сведения о том, как вызвать API Graph для клиента B2C, используя удостоверение приложения для автоматизации процесса."
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
ms.openlocfilehash: c838fcad21875c4f813159ad78d4c87129a40a86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="483c2-103">Azure AD B2C: использование API Graph</span><span class="sxs-lookup"><span data-stu-id="483c2-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="483c2-104">Как правило, клиенты Azure AD B2C (Azure AD) отличаются очень большими размерами.</span><span class="sxs-lookup"><span data-stu-id="483c2-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="483c2-105">Это значит, что многие распространенные задачи управления клиентами необходимо решать программным путем.</span><span class="sxs-lookup"><span data-stu-id="483c2-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="483c2-106">Основным примером может служить управление пользователями.</span><span class="sxs-lookup"><span data-stu-id="483c2-106">A primary example is user management.</span></span> <span data-ttu-id="483c2-107">Возможно, вам потребуется перенести существующее хранилище пользователя в клиент B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="483c2-108">Кроме того, может потребоваться разместить регистрацию пользователей на своей странице и создавать учетные записи пользователей каталога Azure AD B2C в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="483c2-108">You may want to host user registration on your own page and create user accounts in your Azure AD B2C directory behind the scenes.</span></span> <span data-ttu-id="483c2-109">Для выполнения задач такого типа требуется возможность создавать, читать, обновлять и удалять учетные записи пользователей.</span><span class="sxs-lookup"><span data-stu-id="483c2-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="483c2-110">Такую возможность предоставляет API Graph Azure AD.</span><span class="sxs-lookup"><span data-stu-id="483c2-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="483c2-111">Для клиентов B2C используются в основном два режима обмена данными с API Graph.</span><span class="sxs-lookup"><span data-stu-id="483c2-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="483c2-112">Если речь идет об интерактивных разовых задачах, то их следует выполнять под учетной записью администратора клиента B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="483c2-113">Для этого прежде чем выполнять вызовы в API Graph, администратор должен войти в систему со своими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="483c2-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="483c2-114">Для выполнения автоматизированных непрерывно выполняемых задач управления следует использовать тип учетной записи службы, которой предоставлены необходимые привилегии.</span><span class="sxs-lookup"><span data-stu-id="483c2-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="483c2-115">В Azure AD это можно сделать путем регистрации приложения и выполнения проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="483c2-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="483c2-116">Для этого нужен **идентификатор приложения** , который использует [предоставление учетных данных клиента OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="483c2-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="483c2-117">В этом случае приложение вызывает API Graph, действуя само по себе, а не под именем конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="483c2-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="483c2-118">В этой статье мы рассмотрим автоматизированный вариант использования.</span><span class="sxs-lookup"><span data-stu-id="483c2-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="483c2-119">Для примера создадим в .NET 4.5 `B2CGraphClient` , который выполняет операции пользователя: создание, чтение, обновление и удаление (CRUD).</span><span class="sxs-lookup"><span data-stu-id="483c2-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="483c2-120">В клиенте предусмотрен интерфейс командной строки Windows, позволяющий вызывать различные методы.</span><span class="sxs-lookup"><span data-stu-id="483c2-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="483c2-121">При этом код записывается как для неинтерактивной автоматизированной задачи.</span><span class="sxs-lookup"><span data-stu-id="483c2-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="483c2-122">Получение клиента Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="483c2-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="483c2-123">Для создания приложения или пользователей, а также для работы с Azure AD в целом требуется клиент с поддержкой B2C и учетная запись глобального администратора для этого клиента.</span><span class="sxs-lookup"><span data-stu-id="483c2-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="483c2-124">Если у вас нет клиента, создайте его, следуя инструкциям в статье [Предварительная версия Azure Active Directory B2C: создание клиента Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="483c2-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="483c2-125">Регистрация приложения в клиенте</span><span class="sxs-lookup"><span data-stu-id="483c2-125">Register your application in your tenant</span></span>
<span data-ttu-id="483c2-126">После создания клиента B2C необходимо зарегистрировать в нем приложение на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="483c2-126">After you have a B2C tenant, you need to register your application via the [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="483c2-127">Чтобы использовать API Graph с клиентом B2C, необходимо зарегистрировать выделенное приложение с помощью универсальной колонки *Регистрация приложений* на портале Azure, а **не** с помощью колонки *Приложения* Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-127">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using the generic *App Registrations* blade in the Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="483c2-128">Вам не удастся повторно использовать уже существующие приложения B2C, зарегистрированные в колонке *приложений* Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-128">You can't reuse the already-existing B2C applications that you registered in the Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="483c2-129">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="483c2-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="483c2-130">Выберите клиент Azure AD B2C, щелкнув имя своей учетной записи в правом верхнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="483c2-130">Choose your Azure AD B2C tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="483c2-131">На панели навигации слева выберите **Другие службы**, щелкните **Регистрация приложений**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="483c2-131">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="483c2-132">Следуйте инструкциям на экране, а затем создайте новое приложение.</span><span class="sxs-lookup"><span data-stu-id="483c2-132">Follow the prompts and create a new application.</span></span> 
    1. <span data-ttu-id="483c2-133">Выберите в качестве типа приложения **Веб-приложение или API**.</span><span class="sxs-lookup"><span data-stu-id="483c2-133">Select **Web App / API** as the Application Type.</span></span>    
    2. <span data-ttu-id="483c2-134">Укажите **любой URI перенаправления** (например, https://B2CGraphAPI), так как он неважен в этом примере.</span><span class="sxs-lookup"><span data-stu-id="483c2-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="483c2-135">Теперь приложение появится в списке приложений. Щелкните его, чтобы получить **идентификатор приложения** (также известный как идентификатор клиента).</span><span class="sxs-lookup"><span data-stu-id="483c2-135">The application will now show up in the list of applications, click on it to obtain the **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="483c2-136">Скопируйте его, так как он потребуется вам в одном из следующих разделов.</span><span class="sxs-lookup"><span data-stu-id="483c2-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="483c2-137">В колонке "Параметры" щелкните **Ключи** и добавьте новый ключ (также известный как секрет клиента).</span><span class="sxs-lookup"><span data-stu-id="483c2-137">In the Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="483c2-138">Также скопируйте его для использования в одном из следующих разделов.</span><span class="sxs-lookup"><span data-stu-id="483c2-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="483c2-139">Настройка разрешений на создание, чтение и обновление для приложения</span><span class="sxs-lookup"><span data-stu-id="483c2-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="483c2-140">Теперь необходимо настроить для приложения все необходимые разрешения на создание, чтение, обновление и удаление пользователей.</span><span class="sxs-lookup"><span data-stu-id="483c2-140">Now you need to configure your application to get all the required permissions to create, read, update and delete users.</span></span>

1. <span data-ttu-id="483c2-141">В колонке "Регистрация приложений" на портале Azure выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="483c2-141">Continuing in the Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="483c2-142">В колонке "Параметры" щелкните **Необходимые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="483c2-142">In the Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="483c2-143">В колонке "Необходимые разрешения" щелкните **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="483c2-143">In the Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="483c2-144">В колонке "Разрешить доступ" выберите разрешение **Чтение и запись данных каталога** из списка **разрешений приложений** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="483c2-144">In the Enable Access  blade, select the **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="483c2-145">Наконец, в колонке "Необходимые разрешения" нажмите кнопку **Предоставить разрешения**.</span><span class="sxs-lookup"><span data-stu-id="483c2-145">Finally, back in the Required permissions blade, click on the **Grant Permissions** button.</span></span>

<span data-ttu-id="483c2-146">Теперь у вас есть приложение с разрешением на создание, чтение и обновление пользователей из клиента B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-146">You now have an application that has permission to create, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="483c2-147">Настройка разрешений на удаление для приложения</span><span class="sxs-lookup"><span data-stu-id="483c2-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="483c2-148">В настоящее время разрешения на *чтение и запись данных каталога* **не** предусматривают возможность выполнять удаление, например удаление пользователей.</span><span class="sxs-lookup"><span data-stu-id="483c2-148">Currently, the *Read and write directory data* permission does **NOT** include the ability to do any deletions such as deleting users.</span></span> <span data-ttu-id="483c2-149">Если вы хотите предоставить приложению возможность удалять пользователей, необходимо выполнить следующие дополнительные действия, требующие использования PowerShell. В противном случае перейдите к следующему разделу.</span><span class="sxs-lookup"><span data-stu-id="483c2-149">If you want to give your application the ability to delete users, you'll need to do these extra steps that involve PowerShell, otherwise, you can skip to the next section.</span></span>

<span data-ttu-id="483c2-150">Для начала скачайте и установите [помощник по входу в Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="483c2-150">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="483c2-151">Затем скачайте и установите [64-разрядный модуль Azure Active Directory для Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="483c2-151">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="483c2-152">Установив модуль Powershell, откройте Powershell и подключитесь к клиенту B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-152">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="483c2-153">После запуска команды `Get-Credential` отобразится запрос на ввод имени пользователя и пароля. Введите имя пользователя и пароль учетной записи администратора клиента B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="483c2-154">Необходимо использовать учетную запись администратора клиента B2C, которая является **локальной** по отношению к клиенту B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-154">You need to use a B2C tenant administrator account that is **local** to the B2C tenant.</span></span> <span data-ttu-id="483c2-155">Эти учетные записи выглядят следующим образом: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="483c2-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="483c2-156">Теперь мы используем **идентификатор приложения** в приведенном ниже сценарии, чтобы назначить приложению роль администратора учетных записей пользователей, которая позволяет удалять пользователей.</span><span class="sxs-lookup"><span data-stu-id="483c2-156">Now we'll use the **Application ID** in the script below to assign the application the user account administrator role which will allow it to delete users.</span></span> <span data-ttu-id="483c2-157">Идентификаторы этих ролей известны, поэтому можно просто ввести **идентификатор приложения** в приведенный ниже скрипт.</span><span class="sxs-lookup"><span data-stu-id="483c2-157">These roles have well-known identifiers, so all you need to do is input your **Application ID** in the script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="483c2-158">Теперь приложение имеет разрешение на удаление пользователей из клиента B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-158">Your application now also has permissions to delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="483c2-159">Скачивание, настройка и создание примера кода</span><span class="sxs-lookup"><span data-stu-id="483c2-159">Download, configure, and build the sample code</span></span>
<span data-ttu-id="483c2-160">Сначала скачайте и запустите пример кода.</span><span class="sxs-lookup"><span data-stu-id="483c2-160">First, download the sample code and get it running.</span></span> <span data-ttu-id="483c2-161">После этого мы сможем рассмотреть его подробнее.</span><span class="sxs-lookup"><span data-stu-id="483c2-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="483c2-162">Вы можете [скачать пример кода в виде ZIP-файла](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="483c2-162">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="483c2-163">Его можно клонировать в необходимый каталог.</span><span class="sxs-lookup"><span data-stu-id="483c2-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="483c2-164">Откройте решение Visual Studio `B2CGraphClient\B2CGraphClient.sln` в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="483c2-164">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="483c2-165">В проекте `B2CGraphClient` откройте файл `App.config`.</span><span class="sxs-lookup"><span data-stu-id="483c2-165">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="483c2-166">Замените три параметра приложения собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="483c2-166">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="483c2-167">Затем щелкните решение `B2CGraphClient` правой кнопкой мыши и еще раз создайте пример кода.</span><span class="sxs-lookup"><span data-stu-id="483c2-167">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="483c2-168">Если вам удастся выполнить это действие, в каталоге `B2CGraphClient\bin\Debug` появится исполняемый файл `B2C.exe`.</span><span class="sxs-lookup"><span data-stu-id="483c2-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="483c2-169">Создание операций CRUD пользователя с помощью API Graph</span><span class="sxs-lookup"><span data-stu-id="483c2-169">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="483c2-170">Чтобы использовать B2CGraphClient, откройте командную строку Windows (`cmd`) и замените свой каталог каталогом `Debug`.</span><span class="sxs-lookup"><span data-stu-id="483c2-170">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="483c2-171">Затем выполните команду `B2C Help` .</span><span class="sxs-lookup"><span data-stu-id="483c2-171">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="483c2-172">Появится краткое описание каждой команды.</span><span class="sxs-lookup"><span data-stu-id="483c2-172">This will display a brief description of each command.</span></span> <span data-ttu-id="483c2-173">Каждый раз, когда вы вызываете одну из этих команд, клиент `B2CGraphClient` создает запрос к службе API Graph Azure AD.</span><span class="sxs-lookup"><span data-stu-id="483c2-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="483c2-174">Получение маркера доступа</span><span class="sxs-lookup"><span data-stu-id="483c2-174">Get an access token</span></span>
<span data-ttu-id="483c2-175">При любом запросе к API Graph требуется маркер доступа для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="483c2-175">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="483c2-176">`B2CGraphClient` использует библиотеку проверки подлинности Active Directory (ADAL) с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="483c2-176">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="483c2-177">ADAL упрощает получение маркеров, так как предоставляет простой API и выполняет некоторые важные действия, такие как кэширование маркеров доступа.</span><span class="sxs-lookup"><span data-stu-id="483c2-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="483c2-178">Использовать ADAL для получения маркеров необязательно.</span><span class="sxs-lookup"><span data-stu-id="483c2-178">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="483c2-179">Их можно получать, составляя HTTP-запросы вручную.</span><span class="sxs-lookup"><span data-stu-id="483c2-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="483c2-180">В этом примере кода используется ADAL версии 2 для связи с API Graph.</span><span class="sxs-lookup"><span data-stu-id="483c2-180">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="483c2-181">Для получения маркеров доступа, которые могут использоваться с API Graph Azure AD, необходимо использовать ADAL версии 2 или 3.</span><span class="sxs-lookup"><span data-stu-id="483c2-181">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="483c2-182">После запуска `B2CGraphClient` создает экземпляр класса `B2CGraphClient`.</span><span class="sxs-lookup"><span data-stu-id="483c2-182">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="483c2-183">Конструктор для этого класса настраивает формирование шаблонов проверки подлинности ADAL.</span><span class="sxs-lookup"><span data-stu-id="483c2-183">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="483c2-184">Для примера используем команду `B2C Get-User` .</span><span class="sxs-lookup"><span data-stu-id="483c2-184">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="483c2-185">При вызове `B2C Get-User` без дополнительных входных данных CLI вызывает метод `B2CGraphClient.GetAllUsers(...)`.</span><span class="sxs-lookup"><span data-stu-id="483c2-185">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="483c2-186">А тот, в свою очередь, вызывает метод `B2CGraphClient.SendGraphGetRequest(...)`, который отправляет HTTP-запрос GET в API Graph.</span><span class="sxs-lookup"><span data-stu-id="483c2-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="483c2-187">Прежде чем отправить запрос GET, `B2CGraphClient.SendGraphGetRequest(...)` получает маркер доступа, используя ADAL.</span><span class="sxs-lookup"><span data-stu-id="483c2-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="483c2-188">Чтобы получить маркер доступа для API Graph, вызовите метод ADAL `AuthenticationContext.AcquireToken(...)` .</span><span class="sxs-lookup"><span data-stu-id="483c2-188">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="483c2-189">ADAL возвращает `access_token` , представляющий удостоверение приложения.</span><span class="sxs-lookup"><span data-stu-id="483c2-189">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="483c2-190">Чтение пользователей</span><span class="sxs-lookup"><span data-stu-id="483c2-190">Read users</span></span>
<span data-ttu-id="483c2-191">Чтобы извлечь список пользователей или получить определенного пользователя из API Graph, отправьте HTTP-запрос `GET` в конечную точку `/users`.</span><span class="sxs-lookup"><span data-stu-id="483c2-191">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="483c2-192">Для всех пользователей клиента запрос будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="483c2-192">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="483c2-193">Чтобы увидеть, как работает этот запрос, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="483c2-193">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="483c2-194">При этом необходимо обратить внимание на два важных момента.</span><span class="sxs-lookup"><span data-stu-id="483c2-194">There are two important things to note:</span></span>

* <span data-ttu-id="483c2-195">Маркер доступа, полученный из ADAL, добавлен в заголовок `Authorization` с помощью схемы `Bearer`.</span><span class="sxs-lookup"><span data-stu-id="483c2-195">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="483c2-196">Для клиентов B2C необходимо использовать параметр запроса `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="483c2-196">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="483c2-197">Оба фрагмента сведений обрабатываются в методе `B2CGraphClient.SendGraphGetRequest(...)` .</span><span class="sxs-lookup"><span data-stu-id="483c2-197">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="483c2-198">Создание учетных записей пользователей-клиентов</span><span class="sxs-lookup"><span data-stu-id="483c2-198">Create consumer user accounts</span></span>
<span data-ttu-id="483c2-199">При создании учетных записей пользователей в клиенте B2C можно отправить HTTP-запрос `POST` в конечную точку `/users`.</span><span class="sxs-lookup"><span data-stu-id="483c2-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="483c2-200">Для создания пользователей-потребителей требуется большинство свойств в этом запросе.</span><span class="sxs-lookup"><span data-stu-id="483c2-200">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="483c2-201">Для получения дополнительных сведений щелкните [здесь](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="483c2-201">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="483c2-202">Обратите внимание, что комментарии `//` добавлены для наглядности.</span><span class="sxs-lookup"><span data-stu-id="483c2-202">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="483c2-203">Их не нужно добавлять в запрос.</span><span class="sxs-lookup"><span data-stu-id="483c2-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="483c2-204">Чтобы просмотреть запрос, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="483c2-204">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="483c2-205">Команда `Create-User` принимает JSON-файл в качестве входного параметра.</span><span class="sxs-lookup"><span data-stu-id="483c2-205">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="483c2-206">Он содержит представление JSON объекта пользователя.</span><span class="sxs-lookup"><span data-stu-id="483c2-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="483c2-207">Пример кода содержит два примера JSON-файла: `usertemplate-email.json` и `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="483c2-207">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="483c2-208">Вы можете изменить эти файлы с учетом своих требований.</span><span class="sxs-lookup"><span data-stu-id="483c2-208">You can modify these files to suit your needs.</span></span> <span data-ttu-id="483c2-209">Помимо указанных выше можно использовать и другие поля, включенные в эти файлы.</span><span class="sxs-lookup"><span data-stu-id="483c2-209">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="483c2-210">Дополнительные сведения о других необязательных полях см. в [справочнике по сущностям API Graph Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="483c2-210">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="483c2-211">Процесс формирования запроса POST можно увидеть в методе `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="483c2-211">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="483c2-212">Сначала добавляется маркер доступа в заголовок `Authorization` запроса.</span><span class="sxs-lookup"><span data-stu-id="483c2-212">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="483c2-213">Затем задается параметр `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="483c2-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="483c2-214">После чего добавляется объект пользователя JSON в текст запроса.</span><span class="sxs-lookup"><span data-stu-id="483c2-214">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="483c2-215">Если у учетных записей, переносимых из существующего хранилища пользователей, надежность пароля ниже, чем [высокая надежность пароля, обеспечиваемая Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), можно отключить требование надежного пароля с помощью значения `DisableStrongPassword` свойства `passwordPolicies`.</span><span class="sxs-lookup"><span data-stu-id="483c2-215">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="483c2-216">Например, можно изменить запрос создания пользователя, приведенный выше, следующим образом: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="483c2-216">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="483c2-217">Обновление учетных записей пользователей-клиентов</span><span class="sxs-lookup"><span data-stu-id="483c2-217">Update consumer user accounts</span></span>
<span data-ttu-id="483c2-218">Обновление объектов пользователей аналогично процессу их создания,</span><span class="sxs-lookup"><span data-stu-id="483c2-218">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="483c2-219">за исключением того, что при обновлении используется метод HTTP `PATCH`.</span><span class="sxs-lookup"><span data-stu-id="483c2-219">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="483c2-220">Для обновления пользователя можно добавить в JSON-файлы новые данные.</span><span class="sxs-lookup"><span data-stu-id="483c2-220">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="483c2-221">Можно использовать `B2CGraphClient`, чтобы выполнить одну из следующих команд:</span><span class="sxs-lookup"><span data-stu-id="483c2-221">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="483c2-222">Сведения о том, как отправить этот запрос, см. в методе `B2CGraphClient.SendGraphPatchRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="483c2-222">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="483c2-223">Поиск пользователей</span><span class="sxs-lookup"><span data-stu-id="483c2-223">Search users</span></span>
<span data-ttu-id="483c2-224">Искать пользователей в клиенте B2C можно разными способами.</span><span class="sxs-lookup"><span data-stu-id="483c2-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="483c2-225">Можно использовать идентификатор объекта пользователя или идентификатор входа пользователя (т. е. свойство `signInNames`).</span><span class="sxs-lookup"><span data-stu-id="483c2-225">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="483c2-226">Выполните одну из следующих команд для поиска конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="483c2-226">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="483c2-227">Вот несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="483c2-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="483c2-228">Удаление пользователей</span><span class="sxs-lookup"><span data-stu-id="483c2-228">Delete users</span></span>
<span data-ttu-id="483c2-229">Удаление пользователей выполняется очень просто.</span><span class="sxs-lookup"><span data-stu-id="483c2-229">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="483c2-230">Воспользуйтесь методом HTTP `DELETE` и составьте URL-адрес с правильным идентификатором объекта.</span><span class="sxs-lookup"><span data-stu-id="483c2-230">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="483c2-231">Чтобы увидеть пример, выполните следующую команду и просмотрите запрос delete, который будет выведен на консоль.</span><span class="sxs-lookup"><span data-stu-id="483c2-231">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="483c2-232">Сведения о том, как отправить этот запрос, см. в методе `B2CGraphClient.SendGraphDeleteRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="483c2-232">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="483c2-233">Наряду с управлением пользователями API Graph позволяет выполнять и многие другие действия.</span><span class="sxs-lookup"><span data-stu-id="483c2-233">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="483c2-234">Дополнительные сведения о каждом действии и примеры запросов см. в [справочнике по API Graph для Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="483c2-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="483c2-235">Использование настраиваемых атрибутов</span><span class="sxs-lookup"><span data-stu-id="483c2-235">Use custom attributes</span></span>
<span data-ttu-id="483c2-236">В большинстве клиентских приложений необходимо сохранять те или иные данные профилей пользователей-клиентов.</span><span class="sxs-lookup"><span data-stu-id="483c2-236">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="483c2-237">Один из способов решения данной задачи — настройка пользовательского атрибута в клиенте B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-237">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="483c2-238">Этот атрибут можно использовать как и любое другое свойство объекта пользователя.</span><span class="sxs-lookup"><span data-stu-id="483c2-238">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="483c2-239">Атрибут можно обновить, удалить, использовать для запроса, отправить как утверждение в маркере входа и т. д.</span><span class="sxs-lookup"><span data-stu-id="483c2-239">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="483c2-240">Инструкции по указанию настраиваемых атрибутов клиента B2C см. в [справочнике по настраиваемым атрибутам B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="483c2-240">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="483c2-241">Для просмотра пользовательских атрибутов, определенных в клиенте B2C, можно использовать `B2CGraphClient`.</span><span class="sxs-lookup"><span data-stu-id="483c2-241">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="483c2-242">Выходные данные этих функций содержат сведения о каждом пользовательском атрибуте, например:</span><span class="sxs-lookup"><span data-stu-id="483c2-242">The output of these functions reveals the details of each custom attribute, such as:</span></span>

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

<span data-ttu-id="483c2-243">Полное имя, например `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, можно использовать как свойство объектов пользователей.</span><span class="sxs-lookup"><span data-stu-id="483c2-243">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="483c2-244">Для этого достаточно добавить в JSON-файл новое свойство, указать значение для него и запустить указанный ниже код.</span><span class="sxs-lookup"><span data-stu-id="483c2-244">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="483c2-245">Использование `B2CGraphClient`позволяет получить приложение-службу, которое обеспечивает управление пользователями клиента B2C программным путем.</span><span class="sxs-lookup"><span data-stu-id="483c2-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="483c2-246">`B2CGraphClient` проходит аутентификацию в API Graph Azure AD по собственному удостоверению приложения.</span><span class="sxs-lookup"><span data-stu-id="483c2-246">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="483c2-247">Кроме того, B2CGraphClient получает маркеры, используя секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="483c2-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="483c2-248">Добавляя эту функцию в свое приложение, учитывайте некоторые ключевые особенности приложений B2C.</span><span class="sxs-lookup"><span data-stu-id="483c2-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="483c2-249">Приложению необходимо предоставить соответствующие разрешения в клиенте.</span><span class="sxs-lookup"><span data-stu-id="483c2-249">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="483c2-250">На данном этапе для получения токенов доступа необходимо использовать ADAL (не MSAL).</span><span class="sxs-lookup"><span data-stu-id="483c2-250">For now, you need to use ADAL (not MSAL) to get access tokens.</span></span> <span data-ttu-id="483c2-251">(Кроме того, сообщения протокола можно отправлять напрямую, не используя библиотеку.)</span><span class="sxs-lookup"><span data-stu-id="483c2-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="483c2-252">При вызове API Graph укажите `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="483c2-252">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="483c2-253">При создании и обновлении пользователей-клиентов требуются некоторые свойства, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="483c2-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="483c2-254">Если у вас есть вопросы о действиях, которые вы хотели бы выполнить с помощью API Graph для клиента B2C, оставьте комментарий к статье или отправьте заявку в репозиторий примеров кода GitHub.</span><span class="sxs-lookup"><span data-stu-id="483c2-254">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>

