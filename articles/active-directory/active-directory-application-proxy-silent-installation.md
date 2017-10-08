---
title: "aaaSilent установить соединитель прокси приложения Azure AD | Документы Microsoft"
description: "Рассматриваются как tooperform автоматической установки tooyour безопасный удаленный доступ соединитель прокси приложения Azure AD tooprovide локальных приложений."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="703f7-103">Автоматически установить hello соединитель прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="703f7-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="703f7-104">Вы хотите toobe может toosend установки скрипт toomultiple или серверов Server tooWindows, у которых нет пользовательского интерфейса включена.</span><span class="sxs-lookup"><span data-stu-id="703f7-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="703f7-105">Этот раздел поможет вам создать сценарий Windows PowerShell, позволяющий выполнить автоматическую установку и регистрацию соединитель прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="703f7-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="703f7-106">Эта возможность полезна в тех случаях, когда требуется:</span><span class="sxs-lookup"><span data-stu-id="703f7-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="703f7-107">Установите соединитель hello на компьютерах не слой пользовательского интерфейса, или если вы не можете машины toohello протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="703f7-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="703f7-108">установить и зарегистрировать много соединителей одновременно;</span><span class="sxs-lookup"><span data-stu-id="703f7-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="703f7-109">Интеграция hello соединителя установки и регистрации в другой процедуре.</span><span class="sxs-lookup"><span data-stu-id="703f7-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="703f7-110">Создайте стандартный образ, содержащий hello соединителя bits, но не зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="703f7-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="703f7-111">Прокси-сервер приложений работает, установив тонкий службу Windows Server под названием hello соединителя в сети.</span><span class="sxs-lookup"><span data-stu-id="703f7-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="703f7-112">Для toowork соединитель прокси приложения hello имеет toobe, зарегистрированных в каталоге Azure AD с помощью глобального администратора и пароль.</span><span class="sxs-lookup"><span data-stu-id="703f7-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="703f7-113">Обычно эти сведения вводятся во всплывающем окне во время установки соединителя.</span><span class="sxs-lookup"><span data-stu-id="703f7-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="703f7-114">Тем не менее можно использовать Windows PowerShell toocreate tooenter объекта учетных данных сведений о регистрации.</span><span class="sxs-lookup"><span data-stu-id="703f7-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="703f7-115">Или можно создать собственную токен и использовать его tooenter регистрационную информацию.</span><span class="sxs-lookup"><span data-stu-id="703f7-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="703f7-116">Установка соединителя hello</span><span class="sxs-lookup"><span data-stu-id="703f7-116">Install hello connector</span></span>
<span data-ttu-id="703f7-117">Установка MSI соединителя hello без регистрации hello соединителя следующим образом:</span><span class="sxs-lookup"><span data-stu-id="703f7-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="703f7-118">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="703f7-118">Open a command prompt.</span></span>
2. <span data-ttu-id="703f7-119">Запустите следующую команду, в которой hello/q означает установки в автоматическом режиме hello - hello установки не предлагает tooaccept hello лицензионное соглашение.</span><span class="sxs-lookup"><span data-stu-id="703f7-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="703f7-120">Регистрация соединителя hello в Azure AD</span><span class="sxs-lookup"><span data-stu-id="703f7-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="703f7-121">Можно использовать соединитель hello tooregister двумя способами.</span><span class="sxs-lookup"><span data-stu-id="703f7-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="703f7-122">Зарегистрировать соединитель hello, с помощью объекта учетных данных Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="703f7-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="703f7-123">Регистрация с помощью маркера, созданных при автономной работе соединителя hello</span><span class="sxs-lookup"><span data-stu-id="703f7-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="703f7-124">Зарегистрировать соединитель hello, с помощью объекта учетных данных Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="703f7-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="703f7-125">Создайте объект учетных данных Windows PowerShell hello, запустив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="703f7-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="703f7-126">Замените  *\<username\>*  и  *\<пароль\>*  hello имя пользователя и пароль для вашего каталога:</span><span class="sxs-lookup"><span data-stu-id="703f7-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="703f7-127">Go слишком**соединителя AAD прокси-сервера приложений для C:\Program Files\Microsoft** и запустите сценарий hello hello PowerShell с помощью учетных данных созданный объект.</span><span class="sxs-lookup"><span data-stu-id="703f7-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="703f7-128">Замените *$cred* с именем hello hello PowerShell учетные данные созданном объекте:</span><span class="sxs-lookup"><span data-stu-id="703f7-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="703f7-129">Регистрация с помощью маркера, созданных при автономной работе соединителя hello</span><span class="sxs-lookup"><span data-stu-id="703f7-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="703f7-130">Создание маркера вне сети, с помощью класса AuthenticationContext hello значениями hello в фрагменте кода hello:</span><span class="sxs-lookup"><span data-stu-id="703f7-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. <span data-ttu-id="703f7-131">Получив токен hello, создайте SecureString, с помощью токена hello:</span><span class="sxs-lookup"><span data-stu-id="703f7-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="703f7-132">Выполнения hello следующую команду Windows PowerShell, заменив \<клиента GUID\> с Идентификатором каталога:</span><span class="sxs-lookup"><span data-stu-id="703f7-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="703f7-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="703f7-133">Next steps</span></span> 
* [<span data-ttu-id="703f7-134">Публикация приложений с помощью доменного имени</span><span class="sxs-lookup"><span data-stu-id="703f7-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="703f7-135">Включение единого входа</span><span class="sxs-lookup"><span data-stu-id="703f7-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="703f7-136">Устранение неполадок с прокси приложения</span><span class="sxs-lookup"><span data-stu-id="703f7-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


