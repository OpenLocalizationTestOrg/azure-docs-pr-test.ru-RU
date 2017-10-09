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
# <a name="use-azure-key-vault-from-a-web-application"></a>Использование хранилища ключей Azure из веб-приложения
## <a name="introduction"></a>Введение
С помощью этого учебника toohelp, вы узнаете, как toouse Azure ключ хранилища из веб-приложения в Azure. Помогает выполнить процесс hello доступа к секрета из хранилища ключей Azure, чтобы он может использоваться в веб-приложении.

**Предполагаемое время toocomplete:** 15 минут

Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника необходимо иметь следующие hello:

* Секрет tooa URI в хранилище ключей Azure
* Идентификатор клиента и секрет клиента для веб-приложения, зарегистрированные с Azure Active Directory, имеющую доступ tooyour хранилища ключей
* Веб-приложение. Мы будет отображаться hello шаги для приложения ASP.NET MVC, развернутых в Azure в качестве веб-приложения.

> [!NOTE]
> Очень важно, что завершили hello действия, приведенные в [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md) для этого учебника, чтобы получить hello секрет tooa URI и hello идентификатор клиента и секрет клиента для веб-приложения.
> 
> 

веб-приложения Hello, будут получать доступ к hello хранилище ключей — hello один, зарегистрированный в Azure Active Directory, который предоставил доступ tooyour хранилища ключей. Если это не так hello, вернитесь tooRegister приложения hello учебника приступить к работе и повторите перечисленные шаги hello.

Этот учебник предназначен для веб-разработчиков, которые понимают hello основные принципы создания веб-приложений в Azure. Дополнительные сведения о веб-приложениях Azure см. в статье [Обзор веб-приложений](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Добавление пакетов NuGet
Существует два пакета, необходимые для веб-приложения toohave установлен.

* Библиотека проверки подлинности Active Directory содержит методы для взаимодействия с Azure Active Directory и управления удостоверениями пользователей.
* Библиотека хранилища ключей Azure содержит методы для взаимодействия с хранилищем ключей Azure.

Оба этих пакетов можно установить с помощью консоли диспетчера пакетов с помощью команды hello Install-Package hello.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Изменение файла Web.Config
Существует три параметра приложения, которым требуется файл web.config добавлена toohello toobe следующим образом.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Если вы не собираетесь toohost приложения как веб-приложение Azure, следует добавить hello фактическое ClientId, секрет клиента и секрет URI значения toohello web.config. В противном случае оставьте эти пустые значения, так как мы будем добавлять фактическими значениями hello в hello портала Azure для создания дополнительного уровня безопасности.

## <a id="gettoken"></a>Добавьте метод tooGet токена доступа
В порядке toouse hello API хранилища ключей требуется маркер доступа. Ключ хранилища клиента Hello обрабатывает вызовы, toohello API хранилища ключей, но требуется toosupply в функцию, которая получает маркер доступа hello.  

Ниже приведен код hello tooget маркера доступа из Azure Active Directory. Этот код можно расположить в любом месте приложения. Мне нравится tooadd Utils или EncryptionHelper класса.  

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
> С помощью идентификатора клиента и секрет клиента — hello простым способом tooauthenticate приложения Azure AD. Его использование в веб-приложении обеспечивает разделение обязанностей и больший контроль над вашим управлением ключами. Но он полагаться на размещение hello секрет клиента в параметрах конфигурации, в которых для некоторых как рискованно, как и добавлять hello секрет, которые должны tooprotect в параметры конфигурации. Обсуждение hello как toouse идентификатор клиента и сертификат вместо tooauthenticate идентификатор клиента и секрет клиента приложения Azure AD см. ниже.
> 
> 

## <a id="appstart"></a>Извлечь секрет hello на запуск приложения
Теперь нам нужна кода hello toocall API хранилища ключей и извлечь секрет hello. Hello следующий код можно поместить в любом месте при условии, что он вызывается, прежде чем выполнить toouse его. Я поместил этот код в событие запустить приложение hello в hello Global.asax, чтобы он запускается один раз при запуске и делает hello секрет для приложения hello.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Добавить параметры приложения в hello портал Azure (необязательно)
Если у вас есть веб-приложение Azure теперь можно добавить hello фактические значения для hello AppSettings в hello портала Azure. Таким образом, фактические значения hello в файле web.config hello не будет, но защищен с помощью портала при наличии возможности управления доступом отдельных hello. Эти значения будут заменены значениями hello, указанными в файл web.config. Убедитесь, что имена hello hello таким же.

![Параметры приложения на портале Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Проверка подлинности с помощью сертификата вместо секрета клиента
Другой способ tooauthenticate приложения Azure AD — с помощью идентификатора клиента и сертификат, а не идентификатор клиента и секрет клиента. Следующие являются hello toouse действия сертификата в веб-приложение Azure:

1. Получите или создайте сертификат
2. Связать hello сертификат с помощью приложения Azure AD
3. Добавить код tooyour веб-приложение toouse hello сертификата
4. Добавление сертификата tooyour веб-приложения

**Получение или создание сертификата** Для наших целей будет создан тестовый сертификат. Ниже приведено несколько команд, которые используются в toocreate Командная строка разработчика сертификат. Изменить каталог toowhere, нужно создать файлы cert hello.  Кроме того для hello открывающая и закрывающая дату hello сертификата, используйте hello текущую дату плюс 1 год.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Запишите дату окончания hello и hello пароль для PFX-файл hello (в этом примере: 07/31/2016 и test123). Они вам потребуются позднее.

Дополнительные сведения о создании тестового сертификата см. в [этом практическом руководстве](https://msdn.microsoft.com/library/ff699202.aspx).

**Свяжите hello сертификат с помощью приложения Azure AD** имеется сертификат, необходимо tooassociate его с помощью приложения Azure AD. В настоящее время hello портала Azure не поддерживает этот рабочий процесс; Это можно сделать с помощью PowerShell. Выполните следующие команды tooassoicate hello сертификат с hello Azure AD приложения hello.

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

После выполнения этих команд можно увидеть приложения hello в Azure AD. При поиске, убедитесь, что выбран «Приложений, которыми владеет Моя компания» вместо «Приложений использует Моя компания» в диалоговом окне поиска hello.

в разделе toolearn Дополнительные сведения о Azure AD и объекты приложений субъекта-службы, [участника-службы и объекты приложений](../active-directory/active-directory-application-objects.md)

**Добавить код tooyour веб-приложение toouse hello сертификат** теперь мы добавим код tooyour веб-приложение tooaccess hello сертификатов и использовать его для проверки подлинности.

Во-первых, есть cert hello tooaccess кода.

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


Обратите внимание, что hello StoreLocation — CurrentUser вместо LocalMachine. И что мы указали 'false' toohello найти метод, так как мы используем тестовым сертификатом.

Далее следует код, который использует hello CertificateHelper и создает ClientAssertionCertificate, которая используется для проверки подлинности.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Вот hello новый код tooget hello маркер доступа. Эта процедура заменяет описанный выше метод GetToken hello. Для удобства я задал другое имя.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

Я поместил весь этот код в класс Utils проекта веб-приложения для удобства использования.

Последнее изменение кода Hello находится в hello метода Application_Start. Сначала нужно hello toocall GetCert() метод tooload hello ClientAssertionCertificate. И мы измените метод обратного вызова hello, предоставляемый нами при создании нового KeyVaultClient. Обратите внимание, что этот параметр заменяет hello код, который мы должны были выше.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Добавление сертификата tooyour веб-приложения через портал Azure hello** Добавление tooyour сертификат веб-приложения — это простой двухэтапный процесс. Сначала перейдите toohello портала Azure и перейдите tooyour веб-приложения. В колонке hello параметры веб-приложения, щелкните запись hello для «пользовательские домены и SSL». На hello колонку, вы быть hello может tooupload сертификат, созданный выше KVWebApp.pfx, убедитесь, что следует помнить hello пароль для hello pfx.

![Добавление сертификата tooa веб-приложения в hello портала Azure][2]

Hello последнее, что необходимые toodo это tooadd tooyour параметр приложения веб-приложения с веб-сайте приветствия имен\_НАГРУЗКИ\_СЕРТИФИКАТЫ и значение *. Это позволит гарантировать загрузку всех сертификатов. Если требуется, только hello tooload сертификаты, которые вы отправили, а затем можно ввести список разделенных запятыми их отпечаткам.

toolearn Дополнительные сведения о добавлении tooa сертификат веб-приложения в разделе [с помощью сертификатов в приложениях веб-сайтов Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Добавьте сертификат tooKey хранилище в качестве секрета** вместо отправки вашего сертификата toohello службы веб-приложения напрямую, можно сохранить его в хранилище ключей как секрет и развернуть ее оттуда. Это в два этапа, описанных в следующие записи блога hello [развертывание Azure сертификат веб-приложения через хранилище ключей](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Дальнейшие действия
Справочные материалы по программированию см. в [справочнике по API клиента C# для хранилища ключей Azure](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
