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
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a>Автоматически установить hello соединитель прокси приложения Azure AD
Вы хотите toobe может toosend установки скрипт toomultiple или серверов Server tooWindows, у которых нет пользовательского интерфейса включена. Этот раздел поможет вам создать сценарий Windows PowerShell, позволяющий выполнить автоматическую установку и регистрацию соединитель прокси приложения Azure AD.

Эта возможность полезна в тех случаях, когда требуется:

* Установите соединитель hello на компьютерах не слой пользовательского интерфейса, или если вы не можете машины toohello протокола удаленного рабочего СТОЛА.
* установить и зарегистрировать много соединителей одновременно;
* Интеграция hello соединителя установки и регистрации в другой процедуре.
* Создайте стандартный образ, содержащий hello соединителя bits, но не зарегистрирован.

Прокси-сервер приложений работает, установив тонкий службу Windows Server под названием hello соединителя в сети. Для toowork соединитель прокси приложения hello имеет toobe, зарегистрированных в каталоге Azure AD с помощью глобального администратора и пароль. Обычно эти сведения вводятся во всплывающем окне во время установки соединителя. Тем не менее можно использовать Windows PowerShell toocreate tooenter объекта учетных данных сведений о регистрации. Или можно создать собственную токен и использовать его tooenter регистрационную информацию.

## <a name="install-hello-connector"></a>Установка соединителя hello
Установка MSI соединителя hello без регистрации hello соединителя следующим образом:

1. Откройте окно командной строки.
2. Запустите следующую команду, в которой hello/q означает установки в автоматическом режиме hello - hello установки не предлагает tooaccept hello лицензионное соглашение.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a>Регистрация соединителя hello в Azure AD
Можно использовать соединитель hello tooregister двумя способами.

* Зарегистрировать соединитель hello, с помощью объекта учетных данных Windows PowerShell
* Регистрация с помощью маркера, созданных при автономной работе соединителя hello

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a>Зарегистрировать соединитель hello, с помощью объекта учетных данных Windows PowerShell
1. Создайте объект учетных данных Windows PowerShell hello, запустив следующую команду. Замените  *\<username\>*  и  *\<пароль\>*  hello имя пользователя и пароль для вашего каталога:
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Go слишком**соединителя AAD прокси-сервера приложений для C:\Program Files\Microsoft** и запустите сценарий hello hello PowerShell с помощью учетных данных созданный объект. Замените *$cred* с именем hello hello PowerShell учетные данные созданном объекте:
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a>Регистрация с помощью маркера, созданных при автономной работе соединителя hello
1. Создание маркера вне сети, с помощью класса AuthenticationContext hello значениями hello в фрагменте кода hello:

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


2. Получив токен hello, создайте SecureString, с помощью токена hello:

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Выполнения hello следующую команду Windows PowerShell, заменив \<клиента GUID\> с Идентификатором каталога:

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Дальнейшие действия 
* [Публикация приложений с помощью доменного имени](active-directory-application-proxy-custom-domains.md)
* [Включение единого входа](active-directory-application-proxy-sso-using-kcd.md)
* [Устранение неполадок с прокси приложения](active-directory-application-proxy-troubleshoot.md)


