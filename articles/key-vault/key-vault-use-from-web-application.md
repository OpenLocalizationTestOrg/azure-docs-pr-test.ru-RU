---
title: "Хранилище ключей Azure из веб-приложения aaaUse | Документы Microsoft"
description: "С помощью этого учебника toohelp, вы узнаете, как toouse Azure ключ хранилища из веб-приложения."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="7adf9-103">Использование хранилища ключей Azure из веб-приложения</span><span class="sxs-lookup"><span data-stu-id="7adf9-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="7adf9-104">Введение</span><span class="sxs-lookup"><span data-stu-id="7adf9-104">Introduction</span></span>
<span data-ttu-id="7adf9-105">С помощью этого учебника toohelp, вы узнаете, как toouse Azure ключ хранилища из веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="7adf9-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="7adf9-106">Помогает выполнить процесс hello доступа к секрета из хранилища ключей Azure, чтобы он может использоваться в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="7adf9-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="7adf9-107">**Предполагаемое время toocomplete:** 15 минут</span><span class="sxs-lookup"><span data-stu-id="7adf9-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="7adf9-108">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="7adf9-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7adf9-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7adf9-109">Prerequisites</span></span>
<span data-ttu-id="7adf9-110">toocomplete этого учебника необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="7adf9-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="7adf9-111">Секрет tooa URI в хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="7adf9-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="7adf9-112">Идентификатор клиента и секрет клиента для веб-приложения, зарегистрированные с Azure Active Directory, имеющую доступ tooyour хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="7adf9-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="7adf9-113">Веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="7adf9-113">A web application.</span></span> <span data-ttu-id="7adf9-114">Мы будет отображаться hello шаги для приложения ASP.NET MVC, развернутых в Azure в качестве веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7adf9-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="7adf9-115">Очень важно, что завершили hello действия, приведенные в [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md) для этого учебника, чтобы получить hello секрет tooa URI и hello идентификатор клиента и секрет клиента для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7adf9-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="7adf9-116">веб-приложения Hello, будут получать доступ к hello хранилище ключей — hello один, зарегистрированный в Azure Active Directory, который предоставил доступ tooyour хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="7adf9-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="7adf9-117">Если это не так hello, вернитесь tooRegister приложения hello учебника приступить к работе и повторите перечисленные шаги hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="7adf9-118">Этот учебник предназначен для веб-разработчиков, которые понимают hello основные принципы создания веб-приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="7adf9-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="7adf9-119">Дополнительные сведения о веб-приложениях Azure см. в статье [Обзор веб-приложений](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7adf9-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="7adf9-120"><a id="packages"></a>Добавление пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="7adf9-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="7adf9-121">Существует два пакета, необходимые для веб-приложения toohave установлен.</span><span class="sxs-lookup"><span data-stu-id="7adf9-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="7adf9-122">Библиотека проверки подлинности Active Directory содержит методы для взаимодействия с Azure Active Directory и управления удостоверениями пользователей.</span><span class="sxs-lookup"><span data-stu-id="7adf9-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="7adf9-123">Библиотека хранилища ключей Azure содержит методы для взаимодействия с хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="7adf9-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="7adf9-124">Оба этих пакетов можно установить с помощью консоли диспетчера пакетов с помощью команды hello Install-Package hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="7adf9-125"><a id="webconfig"></a>Изменение файла Web.Config</span><span class="sxs-lookup"><span data-stu-id="7adf9-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="7adf9-126">Существует три параметра приложения, которым требуется файл web.config добавлена toohello toobe следующим образом.</span><span class="sxs-lookup"><span data-stu-id="7adf9-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="7adf9-127">Если вы не собираетесь toohost приложения как веб-приложение Azure, следует добавить hello фактическое ClientId, секрет клиента и секрет URI значения toohello web.config. В противном случае оставьте эти пустые значения, так как мы будем добавлять фактическими значениями hello в hello портала Azure для создания дополнительного уровня безопасности.</span><span class="sxs-lookup"><span data-stu-id="7adf9-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="7adf9-128"><a id="gettoken"></a>Добавьте метод tooGet токена доступа</span><span class="sxs-lookup"><span data-stu-id="7adf9-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="7adf9-129">В порядке toouse hello API хранилища ключей требуется маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="7adf9-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="7adf9-130">Ключ хранилища клиента Hello обрабатывает вызовы, toohello API хранилища ключей, но требуется toosupply в функцию, которая получает маркер доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="7adf9-131">Ниже приведен код hello tooget маркера доступа из Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7adf9-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="7adf9-132">Этот код можно расположить в любом месте приложения.</span><span class="sxs-lookup"><span data-stu-id="7adf9-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="7adf9-133">Мне нравится tooadd Utils или EncryptionHelper класса.</span><span class="sxs-lookup"><span data-stu-id="7adf9-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="7adf9-134">С помощью идентификатора клиента и секрет клиента — hello простым способом tooauthenticate приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7adf9-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="7adf9-135">Его использование в веб-приложении обеспечивает разделение обязанностей и больший контроль над вашим управлением ключами.</span><span class="sxs-lookup"><span data-stu-id="7adf9-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="7adf9-136">Но он полагаться на размещение hello секрет клиента в параметрах конфигурации, в которых для некоторых как рискованно, как и добавлять hello секрет, которые должны tooprotect в параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7adf9-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="7adf9-137">Обсуждение hello как toouse идентификатор клиента и сертификат вместо tooauthenticate идентификатор клиента и секрет клиента приложения Azure AD см. ниже.</span><span class="sxs-lookup"><span data-stu-id="7adf9-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="7adf9-138"><a id="appstart"></a>Извлечь секрет hello на запуск приложения</span><span class="sxs-lookup"><span data-stu-id="7adf9-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="7adf9-139">Теперь нам нужна кода hello toocall API хранилища ключей и извлечь секрет hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="7adf9-140">Hello следующий код можно поместить в любом месте при условии, что он вызывается, прежде чем выполнить toouse его.</span><span class="sxs-lookup"><span data-stu-id="7adf9-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="7adf9-141">Я поместил этот код в событие запустить приложение hello в hello Global.asax, чтобы он запускается один раз при запуске и делает hello секрет для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="7adf9-142"><a id="portalsettings"></a>Добавить параметры приложения в hello портал Azure (необязательно)</span><span class="sxs-lookup"><span data-stu-id="7adf9-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="7adf9-143">Если у вас есть веб-приложение Azure теперь можно добавить hello фактические значения для hello AppSettings в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7adf9-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="7adf9-144">Таким образом, фактические значения hello в файле web.config hello не будет, но защищен с помощью портала при наличии возможности управления доступом отдельных hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="7adf9-145">Эти значения будут заменены значениями hello, указанными в файл web.config. Убедитесь, что имена hello hello таким же.</span><span class="sxs-lookup"><span data-stu-id="7adf9-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Параметры приложения на портале Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="7adf9-147">Проверка подлинности с помощью сертификата вместо секрета клиента</span><span class="sxs-lookup"><span data-stu-id="7adf9-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="7adf9-148">Другой способ tooauthenticate приложения Azure AD — с помощью идентификатора клиента и сертификат, а не идентификатор клиента и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="7adf9-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="7adf9-149">Следующие являются hello toouse действия сертификата в веб-приложение Azure:</span><span class="sxs-lookup"><span data-stu-id="7adf9-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="7adf9-150">Получите или создайте сертификат</span><span class="sxs-lookup"><span data-stu-id="7adf9-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="7adf9-151">Связать hello сертификат с помощью приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="7adf9-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="7adf9-152">Добавить код tooyour веб-приложение toouse hello сертификата</span><span class="sxs-lookup"><span data-stu-id="7adf9-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="7adf9-153">Добавление сертификата tooyour веб-приложения</span><span class="sxs-lookup"><span data-stu-id="7adf9-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="7adf9-154">**Получение или создание сертификата** Для наших целей будет создан тестовый сертификат.</span><span class="sxs-lookup"><span data-stu-id="7adf9-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="7adf9-155">Ниже приведено несколько команд, которые используются в toocreate Командная строка разработчика сертификат.</span><span class="sxs-lookup"><span data-stu-id="7adf9-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="7adf9-156">Изменить каталог toowhere, нужно создать файлы cert hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="7adf9-157">Кроме того для hello открывающая и закрывающая дату hello сертификата, используйте hello текущую дату плюс 1 год.</span><span class="sxs-lookup"><span data-stu-id="7adf9-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="7adf9-158">Запишите дату окончания hello и hello пароль для PFX-файл hello (в этом примере: 07/31/2016 и test123).</span><span class="sxs-lookup"><span data-stu-id="7adf9-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="7adf9-159">Они вам потребуются позднее.</span><span class="sxs-lookup"><span data-stu-id="7adf9-159">You will need them below.</span></span>

<span data-ttu-id="7adf9-160">Дополнительные сведения о создании тестового сертификата см. в [этом практическом руководстве](https://msdn.microsoft.com/library/ff699202.aspx).</span><span class="sxs-lookup"><span data-stu-id="7adf9-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="7adf9-161">**Свяжите hello сертификат с помощью приложения Azure AD** имеется сертификат, необходимо tooassociate его с помощью приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7adf9-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="7adf9-162">В настоящее время hello портала Azure не поддерживает этот рабочий процесс; Это можно сделать с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7adf9-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="7adf9-163">Выполните следующие команды tooassoicate hello сертификат с hello Azure AD приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="7adf9-164">После выполнения этих команд можно увидеть приложения hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7adf9-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="7adf9-165">При поиске, убедитесь, что выбран «Приложений, которыми владеет Моя компания» вместо «Приложений использует Моя компания» в диалоговом окне поиска hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="7adf9-166">в разделе toolearn Дополнительные сведения о Azure AD и объекты приложений субъекта-службы, [участника-службы и объекты приложений](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="7adf9-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="7adf9-167">**Добавить код tooyour веб-приложение toouse hello сертификат** теперь мы добавим код tooyour веб-приложение tooaccess hello сертификатов и использовать его для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7adf9-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="7adf9-168">Во-первых, есть cert hello tooaccess кода.</span><span class="sxs-lookup"><span data-stu-id="7adf9-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="7adf9-169">Обратите внимание, что hello StoreLocation — CurrentUser вместо LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="7adf9-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="7adf9-170">И что мы указали 'false' toohello найти метод, так как мы используем тестовым сертификатом.</span><span class="sxs-lookup"><span data-stu-id="7adf9-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="7adf9-171">Далее следует код, который использует hello CertificateHelper и создает ClientAssertionCertificate, которая используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7adf9-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="7adf9-172">Вот hello новый код tooget hello маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="7adf9-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="7adf9-173">Эта процедура заменяет описанный выше метод GetToken hello.</span><span class="sxs-lookup"><span data-stu-id="7adf9-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="7adf9-174">Для удобства я задал другое имя.</span><span class="sxs-lookup"><span data-stu-id="7adf9-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="7adf9-175">Я поместил весь этот код в класс Utils проекта веб-приложения для удобства использования.</span><span class="sxs-lookup"><span data-stu-id="7adf9-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="7adf9-176">Последнее изменение кода Hello находится в hello метода Application_Start.</span><span class="sxs-lookup"><span data-stu-id="7adf9-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="7adf9-177">Сначала нужно hello toocall GetCert() метод tooload hello ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="7adf9-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="7adf9-178">И мы измените метод обратного вызова hello, предоставляемый нами при создании нового KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="7adf9-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="7adf9-179">Обратите внимание, что этот параметр заменяет hello код, который мы должны были выше.</span><span class="sxs-lookup"><span data-stu-id="7adf9-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="7adf9-180">**Добавление сертификата tooyour веб-приложения через портал Azure hello** Добавление tooyour сертификат веб-приложения — это простой двухэтапный процесс.</span><span class="sxs-lookup"><span data-stu-id="7adf9-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="7adf9-181">Сначала перейдите toohello портала Azure и перейдите tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7adf9-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="7adf9-182">В колонке hello параметры веб-приложения, щелкните запись hello для «пользовательские домены и SSL».</span><span class="sxs-lookup"><span data-stu-id="7adf9-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="7adf9-183">На hello колонку, вы быть hello может tooupload сертификат, созданный выше KVWebApp.pfx, убедитесь, что следует помнить hello пароль для hello pfx.</span><span class="sxs-lookup"><span data-stu-id="7adf9-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![Добавление сертификата tooa веб-приложения в hello портала Azure][2]

<span data-ttu-id="7adf9-185">Hello последнее, что необходимые toodo это tooadd tooyour параметр приложения веб-приложения с веб-сайте приветствия имен\_НАГРУЗКИ\_СЕРТИФИКАТЫ и значение *.</span><span class="sxs-lookup"><span data-stu-id="7adf9-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="7adf9-186">Это позволит гарантировать загрузку всех сертификатов.</span><span class="sxs-lookup"><span data-stu-id="7adf9-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="7adf9-187">Если требуется, только hello tooload сертификаты, которые вы отправили, а затем можно ввести список разделенных запятыми их отпечаткам.</span><span class="sxs-lookup"><span data-stu-id="7adf9-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="7adf9-188">toolearn Дополнительные сведения о добавлении tooa сертификат веб-приложения в разделе [с помощью сертификатов в приложениях веб-сайтов Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="7adf9-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="7adf9-189">**Добавьте сертификат tooKey хранилище в качестве секрета** вместо отправки вашего сертификата toohello службы веб-приложения напрямую, можно сохранить его в хранилище ключей как секрет и развернуть ее оттуда.</span><span class="sxs-lookup"><span data-stu-id="7adf9-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="7adf9-190">Это в два этапа, описанных в следующие записи блога hello [развертывание Azure сертификат веб-приложения через хранилище ключей](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="7adf9-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="7adf9-191"><a id="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7adf9-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="7adf9-192">Справочные материалы по программированию см. в [справочнике по API клиента C# для хранилища ключей Azure](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="7adf9-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
