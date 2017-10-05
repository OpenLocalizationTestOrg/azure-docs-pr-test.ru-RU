---
title: "Использование хранилища ключей Azure из веб-приложения | Документация Майкрософт"
description: "В этом учебнике показано, как использовать хранилище ключей Azure из веб-приложения."
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
ms.openlocfilehash: d095bcfe37baefa90cf79bb48bff3f703ce1dad7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="e1e23-103">Использование хранилища ключей Azure из веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e1e23-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="e1e23-104">Введение</span><span class="sxs-lookup"><span data-stu-id="e1e23-104">Introduction</span></span>
<span data-ttu-id="e1e23-105">В этом учебнике показано, как использовать хранилище ключей Azure из веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e23-105">Use this tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="e1e23-106">В нем рассматривается процесс доступа к секрету в хранилище ключей Azure для его использования в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="e1e23-106">It walks you through the process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="e1e23-107">**Предполагаемое время выполнения:** 15 минут.</span><span class="sxs-lookup"><span data-stu-id="e1e23-107">**Estimated time to complete:** 15 minutes</span></span>

<span data-ttu-id="e1e23-108">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="e1e23-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1e23-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e1e23-109">Prerequisites</span></span>
<span data-ttu-id="e1e23-110">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="e1e23-110">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="e1e23-111">URI для секрета кода в хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="e1e23-111">A URI to a secret in an Azure Key Vault</span></span>
* <span data-ttu-id="e1e23-112">Идентификатор клиента и секрет клиента для веб-приложения, зарегистрированного в Azure Active Directory, которое имеет доступ к вашему хранилищу ключей</span><span class="sxs-lookup"><span data-stu-id="e1e23-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access to your Key Vault</span></span>
* <span data-ttu-id="e1e23-113">Веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="e1e23-113">A web application.</span></span> <span data-ttu-id="e1e23-114">Мы покажем действия для приложения ASP.NET MVC, развернутого в Azure в качестве веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e1e23-114">We will be showing the steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="e1e23-115">Необходимо выполнить действия, описанные в разделе [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md) , чтобы получить URI секрета, идентификатор клиента и секрет клиента для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e1e23-115">It is essential that you have completed the steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have the URI to a secret and the Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="e1e23-116">Доступ к хранилищу ключей будет получать веб-приложение, зарегистрированное в Azure Active Directory и получившее права доступа к хранилищу ключей.</span><span class="sxs-lookup"><span data-stu-id="e1e23-116">The web application that will be accessing the Key Vault is the one that is registered in Azure Active Directory and has been given access to your Key Vault.</span></span> <span data-ttu-id="e1e23-117">Если это не так, вернитесь к разделу "Регистрация приложения" в учебнике "Приступая к работе" и повторите перечисленные шаги.</span><span class="sxs-lookup"><span data-stu-id="e1e23-117">If this is not the case, go back to Register an Application in the Get Started tutorial and repeat the steps listed.</span></span>

<span data-ttu-id="e1e23-118">Этот учебник поможет веб-разработчикам понять принципы создания веб-приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e23-118">This tutorial is designed for web developers that understand the basics of creating web applications on Azure.</span></span> <span data-ttu-id="e1e23-119">Дополнительные сведения о веб-приложениях Azure см. в статье [Обзор веб-приложений](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1e23-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="e1e23-120"><a id="packages"></a>Добавление пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="e1e23-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="e1e23-121">Существует два пакета, которые необходимо установить для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e1e23-121">There are two packages that your web application needs to have installed.</span></span>

* <span data-ttu-id="e1e23-122">Библиотека проверки подлинности Active Directory содержит методы для взаимодействия с Azure Active Directory и управления удостоверениями пользователей.</span><span class="sxs-lookup"><span data-stu-id="e1e23-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="e1e23-123">Библиотека хранилища ключей Azure содержит методы для взаимодействия с хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e23-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="e1e23-124">Оба пакета можно установить с помощью консоли диспетчера пакетов, используя команду Install-Package.</span><span class="sxs-lookup"><span data-stu-id="e1e23-124">Both of these packages can be installed using the Package Manager Console using the Install-Package command.</span></span>

    // this is currently the latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="e1e23-125"><a id="webconfig"></a>Изменение файла Web.Config</span><span class="sxs-lookup"><span data-stu-id="e1e23-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="e1e23-126">Существует три параметра приложения, которые необходимо добавить в файл web.config следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e1e23-126">There are three application settings that need to be added to the web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer to the web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is the URI for the secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="e1e23-127">Если вы не собираетесь размещать приложения как веб-приложения Azure, добавьте фактические значения идентификатора клиента, секрета клиента и URI секрета в файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="e1e23-127">If you are not going to host your application as an Azure Web App, then you should add the actual ClientId, Client Secret, and Secret URI values to the web.config.</span></span> <span data-ttu-id="e1e23-128">В противном случае оставьте значения-заполнители, так как мы добавим фактические значения на портале Azure, чтобы получить дополнительный уровень безопасности.</span><span class="sxs-lookup"><span data-stu-id="e1e23-128">Otherwise leave these dummy values because we will be adding the actual values in the Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="e1e23-129"><a id="gettoken"></a>Добавление метода для получения маркера доступа</span><span class="sxs-lookup"><span data-stu-id="e1e23-129"><a id="gettoken"></a>Add Method to Get an Access Token</span></span>
<span data-ttu-id="e1e23-130">Для использования API хранилища ключей требуется маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="e1e23-130">In order to use the Key Vault API you need an access token.</span></span> <span data-ttu-id="e1e23-131">Клиент хранилища ключей обрабатывает вызовы API хранилища ключей, но вам необходимо предоставить ему функцию, которая возвращает маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="e1e23-131">The Key Vault Client handles calls to the Key Vault API but you need to supply it with a function that gets the access token.</span></span>  

<span data-ttu-id="e1e23-132">Ниже приведен код для получения маркера доступа из Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1e23-132">Following is the code to get an access token from Azure Active Directory.</span></span> <span data-ttu-id="e1e23-133">Этот код можно расположить в любом месте приложения.</span><span class="sxs-lookup"><span data-stu-id="e1e23-133">This code can go anywhere in your application.</span></span> <span data-ttu-id="e1e23-134">Я добавлю его в класс Utils или EncryptionHelper.</span><span class="sxs-lookup"><span data-stu-id="e1e23-134">I like to add a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property to hold the secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //the method that will be provided to the KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed to obtain the JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="e1e23-135">Использование идентификатора клиента и секрета клиента — это самый простой способ выполнить проверку подлинности для приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1e23-135">Using a Client ID and Client Secret is the easiest way to authenticate an Azure AD application.</span></span> <span data-ttu-id="e1e23-136">Его использование в веб-приложении обеспечивает разделение обязанностей и больший контроль над вашим управлением ключами.</span><span class="sxs-lookup"><span data-stu-id="e1e23-136">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="e1e23-137">Но ему требуется размещение секрета клиента в параметрах конфигурации, что в некоторых ситуациях может быть так же рискованно, как размещение секрета, который необходимо защитить, в параметрах конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e1e23-137">But it does rely on putting the Client Secret in your configuration settings which for some can be as risky as putting the secret that you want to protect in your configuration settings.</span></span> <span data-ttu-id="e1e23-138">Ниже приведены сведения о том, как использовать идентификатор клиента и сертификат вместо идентификатора и секрета клиента для проверки подлинности приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1e23-138">See below for a discussion on how to use a Client ID and Certificate instead of Client ID and Client Secret to authenticate the Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="e1e23-139"><a id="appstart"></a>Получение секрета при запуске приложения</span><span class="sxs-lookup"><span data-stu-id="e1e23-139"><a id="appstart"></a>Retrieve the secret on Application Start</span></span>
<span data-ttu-id="e1e23-140">Теперь нам требуется, чтобы код вызвал API хранилища ключей и получил секрет.</span><span class="sxs-lookup"><span data-stu-id="e1e23-140">Now we need code to call the Key Vault API and retrieve the secret.</span></span> <span data-ttu-id="e1e23-141">Следующий фрагмент кода можно поместить в любом месте, при условии что он вызывается перед тем, как его необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="e1e23-141">The following code can be put anywhere as long as it is called before you need to use it.</span></span> <span data-ttu-id="e1e23-142">Я поместил код в событии запуска приложения в файле Global.asax, чтобы он выполнялся один раз при запуске, а секрет становился доступным для приложения.</span><span class="sxs-lookup"><span data-stu-id="e1e23-142">I have put this code in the Application Start event in the Global.asax so that it runs once on start and makes the secret available for the application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class to hold the secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="e1e23-143"><a id="portalsettings"></a>Добавление параметров приложения на портале Azure (необязательно)</span><span class="sxs-lookup"><span data-stu-id="e1e23-143"><a id="portalsettings"></a>Add App Settings in the Azure Portal (optional)</span></span>
<span data-ttu-id="e1e23-144">Если у вас есть веб-приложение Azure, теперь вы можете добавить фактические значения параметров приложений на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e23-144">If you have an Azure Web App you can now add the actual values for the AppSettings in the Azure Portal.</span></span> <span data-ttu-id="e1e23-145">При этом фактические значения не будут размещены в файле web.config, а будут защищены с помощью портала, где предоставляются отдельные возможности управления доступом.</span><span class="sxs-lookup"><span data-stu-id="e1e23-145">By doing this, the actual values will not be in the web.config but protected via the Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="e1e23-146">Эти значения будут заменены на значения, введенные в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="e1e23-146">These values will be substituted for the values that you entered in your web.config.</span></span> <span data-ttu-id="e1e23-147">Убедитесь, что имена совпадают.</span><span class="sxs-lookup"><span data-stu-id="e1e23-147">Make sure that the names are the same.</span></span>

![Параметры приложения на портале Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="e1e23-149">Проверка подлинности с помощью сертификата вместо секрета клиента</span><span class="sxs-lookup"><span data-stu-id="e1e23-149">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="e1e23-150">Еще один способ проверки подлинности приложения Azure AD состоит в использовании идентификатора клиента и сертификата вместо идентификатора и секрета клиента.</span><span class="sxs-lookup"><span data-stu-id="e1e23-150">Another way to authenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="e1e23-151">Ниже приведены действия по использованию сертификата в веб-приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e23-151">Following are the steps to use a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="e1e23-152">Получите или создайте сертификат</span><span class="sxs-lookup"><span data-stu-id="e1e23-152">Get or Create a Certificate</span></span>
2. <span data-ttu-id="e1e23-153">Свяжите сертификат с приложением Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1e23-153">Associate the Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="e1e23-154">Добавьте код в веб-приложение, чтобы использовать сертификат</span><span class="sxs-lookup"><span data-stu-id="e1e23-154">Add code to your Web App to use the Certificate</span></span>
4. <span data-ttu-id="e1e23-155">Добавьте сертификат в веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1e23-155">Add a Certificate to your Web App</span></span>

<span data-ttu-id="e1e23-156">**Получение или создание сертификата** Для наших целей будет создан тестовый сертификат.</span><span class="sxs-lookup"><span data-stu-id="e1e23-156">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="e1e23-157">Вот несколько команд, которые можно использовать в командной строке разработчика для создания сертификата.</span><span class="sxs-lookup"><span data-stu-id="e1e23-157">Here are a couple of commands that you can use in a Developer Command Prompt to create a certificate.</span></span> <span data-ttu-id="e1e23-158">Измените каталог, в котором будут созданы файлы сертификата.</span><span class="sxs-lookup"><span data-stu-id="e1e23-158">Change directory to where you want the cert files created.</span></span>  <span data-ttu-id="e1e23-159">Кроме того, для начальной и конечной даты сертификата используется текущая дата плюс один год.</span><span class="sxs-lookup"><span data-stu-id="e1e23-159">Also, for the beginning and ending date of the certificate, use the current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="e1e23-160">Запишите дату окончания и пароль для PFX-файла (в этом примере: 07/31/2016 и test123).</span><span class="sxs-lookup"><span data-stu-id="e1e23-160">Make note of the end date and the password for the .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="e1e23-161">Они вам потребуются позднее.</span><span class="sxs-lookup"><span data-stu-id="e1e23-161">You will need them below.</span></span>

<span data-ttu-id="e1e23-162">Дополнительные сведения о создании тестового сертификата см. в [этом практическом руководстве](https://msdn.microsoft.com/library/ff699202.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1e23-162">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="e1e23-163">**Свяжите сертификат с приложением Azure AD** Теперь, когда у вас есть сертификат, необходимо связать его с приложением Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1e23-163">**Associate the Certificate with an Azure AD application** Now that you have a certificate, you need to associate it with an Azure AD application.</span></span> <span data-ttu-id="e1e23-164">В настоящее время портал Azure не поддерживает этот рабочий процесс. Однако это можно сделать с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1e23-164">Presently, the Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="e1e23-165">Чтобы связать сертификат с приложением Azure AD, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e1e23-165">Run the following commands to assoicate the certificate with the Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get the thumbprint to use in your app settings
    $x509.Thumbprint

<span data-ttu-id="e1e23-166">После выполнения этих команд приложение можно будет увидеть в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1e23-166">After you have run these commands, you can see the application in Azure AD.</span></span> <span data-ttu-id="e1e23-167">Во время поиска в диалогом окне поиска выберите "Приложения, которыми владеет моя компания", а не "Приложения, которые использует моя компания".</span><span class="sxs-lookup"><span data-stu-id="e1e23-167">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in the search dialog.</span></span>

<span data-ttu-id="e1e23-168">Дополнительные сведения об объектах приложения Azure AD и ServicePrincipal см. в статье [Объекты приложения и субъекта-службы в Azure Active Directory](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="e1e23-168">To learn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="e1e23-169">**Добавление кода для веб-приложения, чтобы использовать сертификат** Теперь в веб-приложение будет добавлен код для доступа к сертификату и его использования для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e1e23-169">**Add code to your Web App to use the Certificate** Now we will add code to your Web App to access the cert and use it for authentication.</span></span>

<span data-ttu-id="e1e23-170">Во-первых, есть код для доступа к сертификату.</span><span class="sxs-lookup"><span data-stu-id="e1e23-170">First there is code to access the cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since the test root isn't installed.
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


<span data-ttu-id="e1e23-171">Обратите внимание, что StoreLocation является CurrentUser вместо LocalMachine</span><span class="sxs-lookup"><span data-stu-id="e1e23-171">Note that the StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="e1e23-172">и что мы указали false для метода Find, поскольку мы используем тестовый сертификат.</span><span class="sxs-lookup"><span data-stu-id="e1e23-172">And that we are supplying 'false' to the Find method because we are using a test cert.</span></span>

<span data-ttu-id="e1e23-173">Далее следует код, который с помощью CertificateHelper и создает ClientAssertionCertificate, необходимый для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e1e23-173">Next is code that uses the CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="e1e23-174">Здесь представлен новый код для получения токена доступа.</span><span class="sxs-lookup"><span data-stu-id="e1e23-174">Here is the new code to get the access token.</span></span> <span data-ttu-id="e1e23-175">Этот параметр заменяет метод GetToken выше.</span><span class="sxs-lookup"><span data-stu-id="e1e23-175">This replaces the GetToken method above.</span></span> <span data-ttu-id="e1e23-176">Для удобства я задал другое имя.</span><span class="sxs-lookup"><span data-stu-id="e1e23-176">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="e1e23-177">Я поместил весь этот код в класс Utils проекта веб-приложения для удобства использования.</span><span class="sxs-lookup"><span data-stu-id="e1e23-177">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="e1e23-178">Последнее изменение кода находится в методе Application_Start.</span><span class="sxs-lookup"><span data-stu-id="e1e23-178">The last code change is in the Application_Start method.</span></span> <span data-ttu-id="e1e23-179">Сначала необходимо вызвать метод GetCert() для загрузки ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="e1e23-179">First we need to call the GetCert() method to load the ClientAssertionCertificate.</span></span> <span data-ttu-id="e1e23-180">А затем мы изменяем метод обратного вызова, который использовался при создании нового KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="e1e23-180">And then we change the callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="e1e23-181">Обратите внимание, что этот параметр заменяет имевшийся ранее код.</span><span class="sxs-lookup"><span data-stu-id="e1e23-181">Note that this replaces the code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="e1e23-182">**Добавление сертификата в веб-приложение на портале Azure** Добавление сертификата в веб-приложение — это простой двухэтапный процесс.</span><span class="sxs-lookup"><span data-stu-id="e1e23-182">**Add a Certificate to your Web App through the Azure Portal** Adding a Certificate to your Web App is a simple two-step process.</span></span> <span data-ttu-id="e1e23-183">Сначала войдите на портал управления Azure и перейдите к своему веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="e1e23-183">First, go to the Azure Portal and navigate to your Web App.</span></span> <span data-ttu-id="e1e23-184">В колонке "Параметры" веб-приложения щелкните запись "Пользовательские домены и SSL".</span><span class="sxs-lookup"><span data-stu-id="e1e23-184">On the Settings blade for your Web App, click on the entry for "Custom domains and SSL".</span></span> <span data-ttu-id="e1e23-185">В открывшейся колонке вы сможете загрузить ранее созданный сертификат KVWebApp.pfx. Убедитесь, что вы помните пароль для PFX.</span><span class="sxs-lookup"><span data-stu-id="e1e23-185">On the blade that opens you will be able to upload the Certificate that you created above, KVWebApp.pfx, make sure that you remember the password for the pfx.</span></span>

![Добавление сертификата в веб-приложение на портале Azure][2]

<span data-ttu-id="e1e23-187">Последнее, что требуется выполнить, — добавить в веб-приложение параметр с именем WEBSITE\_LOAD\_CERTIFICATES и значением "*".</span><span class="sxs-lookup"><span data-stu-id="e1e23-187">The last thing that you need to do is to add an Application Setting to your Web App that has the name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="e1e23-188">Это позволит гарантировать загрузку всех сертификатов.</span><span class="sxs-lookup"><span data-stu-id="e1e23-188">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="e1e23-189">Если требуется загрузить только переданные сертификаты, можно ввести разделенный запятыми список их отпечатков.</span><span class="sxs-lookup"><span data-stu-id="e1e23-189">If you wanted to load only the Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="e1e23-190">Дополнительные сведения о добавлении сертификата в веб-приложение см. в статье [Использование сертификатов в приложениях веб-сайтов Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/).</span><span class="sxs-lookup"><span data-stu-id="e1e23-190">To learn more about adding a Certificate to a Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="e1e23-191">**Добавление сертификата в хранилище ключей в качестве секрета** Вместо отправки сертификата непосредственно в службу веб-приложения вы можете сохранить его в хранилище ключей в секрете, а затем развернуть его оттуда.</span><span class="sxs-lookup"><span data-stu-id="e1e23-191">**Add a Certificate to Key Vault as a secret** Instead of uploading your certificate to the Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="e1e23-192">Этот двухэтапный процесс описан в записи блога, посвященной [развертыванию сертификата веб-приложения Azure из хранилища ключей](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="e1e23-192">This is a two-step process that is outlined in the following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="e1e23-193"><a id="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1e23-193"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="e1e23-194">Справочные материалы по программированию см. в [справочнике по API клиента C# для хранилища ключей Azure](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1e23-194">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
