---
title: "aaaHow tooconfigure автоматической регистрации присоединенных к домену устройств Windows в Azure Active Directory | Документы Microsoft"
description: "Настройку вашей tooregister присоединенных к домену устройств Windows автоматически и без предупреждений с помощью Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a>Как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory

toouse [условного доступа на основе устройств Azure Active Directory](active-directory-conditional-access-azure-portal.md), компьютеры должны быть зарегистрированы в Azure Active Directory (Azure AD). Можно получить список устройств, зарегистрированных в вашей организации с помощью hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) командлета в hello [модуля Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0). 

В этой статье предоставляет hello шаги по настройке hello автоматической регистрации присоединенных к домену устройств Windows с помощью Azure AD в вашей организации.


Ознакомьтесь также с информацией по смежным темам:

- Условный доступ описан в статье [Условный доступ в Azure Active Directory — предварительная версия](active-directory-conditional-access-azure-portal.md). 
- Устройства Windows 10 в рабочей области hello и опыт hello усиленной при регистрации в Azure AD см. [Windows 10 для предприятия hello: использование устройств для работы](active-directory-azureadjoin-windows10-devices-overview.md).
- Windows 10 корпоративный E3 в CSP, в разделе hello [Windows 10 корпоративный E3 в обзоре CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).


## <a name="before-you-begin"></a>Перед началом работы

Перед началом настройки hello автоматической регистрации присоединенных к домену устройств Windows в вашей среде, следует ознакомиться с ограничениями hello и сценариях hello поддерживается.  

удобочитаемость hello tooimprove описаний hello, в этом разделе используются следующие термин hello. 

- **Текущий устройств Windows** -этот термин обозначает toodomain устройств под управлением Windows 10 или Windows Server 2016.
- **Устройства Windows низкого уровня** -этот термин обозначает tooall **поддерживается** присоединенных к домену устройств Windows, которые не являются запущенной Windows 10 и Windows Server 2016.  


### <a name="windows-current-devices"></a>Текущие устройства Windows

- Для устройств под управлением операционной системы hello Windows, мы рекомендуем использовать обновления окончания действия (версии 1607) для Windows 10 или более поздней версии. 
- Здравствуйте, регистрации текущего устройств Windows **—** поддерживается в средах, не относящихся к федерации, таких как конфигурации синхронизации хеша пароля.  


### <a name="windows-down-level-devices"></a>Устройства Windows нижнего уровня

- поддерживаются следующие устройства нижнего уровня Windows Hello:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- Здравствуйте, регистрации устройств Windows низкого уровня **—** поддерживается в нефедеративных сред с помощью комплексной Single Sign On [Azure Active Directory прозрачную единого входа](https://aka.ms/hybrid/sso).
- Здравствуйте, регистрации устройств Windows низкого уровня **не** поддерживается для устройств с помощью перемещаемых профилей. Если вам требуются перемещаемые профили или параметры, используйте только Windows 10.



## <a name="prerequisites"></a>Предварительные требования

Прежде чем начать включение hello функции автоматической регистрации присоединенных к домену устройств в вашей организации, необходимо toomake, что используется последняя версия Azure AD подключения.

Azure AD Connect выполняет следующие функции:

- Сохраняет hello связь между hello учетной записи компьютера в вашей локальной Active Directory (AD) и hello объекта устройства в Azure AD. 
- Поддерживает другие функции, связанные с устройствами, например Windows Hello для бизнеса.



## <a name="configuration-steps"></a>Этапы настройки

Этот раздел содержит hello необходимые действия для всех сценариев стандартной конфигурации.  
Используйте следующие таблицы tooget hello этапы, необходимые для вашего сценария hello.  



| Действия                                      | Текущие устройства Windows и синхронизация хэша паролей | Текущие устройства Windows и федерация | Устройства Windows нижнего уровня |
| :--                                        | :-:                                    | :-:                            | :-:                |
| Шаг 1. Настройка точки подключения службы | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |
| Шаг 2. Настройка выдачи утверждений           |                                        | ![Проверка][1]                    | ![Проверка][1]        |
| Шаг 3. Включение поддержки устройств с ОС, отличными от Windows 10      |                                        |                                | ![Проверка][1]        |
| Шаг 4. Контроль развертывания     | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |
| Шаг 5. Проверка зарегистрированных устройств          | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |



## <a name="step-1-configure-service-connection-point"></a>Шаг 1. Настройка точки подключения службы

объект точки (SCP) для подключения служб Hello используется устройствами во время регистрации hello toodiscover информацию о клиенте Azure AD. В вашей локальной Active Directory (AD) hello объекта точки подключения службы для hello функции автоматической регистрации присоединенных к домену устройств должен существовать в раздел конфигурации именования hello контекст компьютера hello леса. В каждом лесу существует только один контекст именования конфигурации. В конфигурации с несколькими лесами Active Directory точка подключения службы hello должны находиться во всех лесах, содержащих компьютеров, присоединенных к домену.

Можно использовать hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) командлет tooretrieve hello контекст именования конфигурации своего леса.  

Для леса с именем домена Active Directory hello *fabrikam.com*, контекст именования конфигурации hello:

`CN=Configuration,DC=fabrikam,DC=com`

В вашем лесу hello SCP объекта для автоматической регистрации hello устройств, присоединенных к домену в каталоге:  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

В зависимости от того, как вы развернули Azure AD Connect hello объекта точки подключения службы может быть уже настроен.
Можно проверить существование hello объекта hello и извлечь значения обнаружения hello, с помощью hello следующий сценарий Windows PowerShell: 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

Hello **$scp. Ключевые слова** выходные данные показывают сведения о клиенте hello Azure AD, например:

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Если точка подключения службы hello не существует, то можно создать, запустив hello `Initialize-ADSyncDomainJoinedComputerSync` командлета на сервере Azure AD Connect. Учетные данные администратора предприятия является обязательным toorun этого командлета.  
Hello командлета:

- Создает точку подключения службы hello в лесу Active Directory hello подключения Azure AD Connect. 
- Требует toospecify hello `AdConnectorAccount` параметра. Это учетная запись hello, настроенный как Active Directory, подключение соединителя учетной записи в Azure AD. 


Hello следующий скрипт показывает пример использования командлета hello. В этом сценарии `$aadAdminCred = Get-Credential` требует tootype имя пользователя. Требуется имя пользователя tooprovide hello в формате имени участника (UPN) пользователя hello (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

Hello `Initialize-ADSyncDomainJoinedComputerSync` командлета:

- Использует модуль Active Directory PowerShell hello, которое зависит от веб-службы Active Directory, на контроллере домена. Поддержку веб-служб Active Directory выполняют контроллеры домена под управлением Windows Server 2008 R2 и более поздних версий.
- Поддерживается только hello **MSOnline PowerShell версии модуля 1.1.166.0**. toodownload этот модуль используется [ссылку](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Для контроллеров домена под управлением Windows Server 2008 или более ранних версий используйте ниже точка подключения службы hello toocreate сценарий hello.

В конфигурации с несколькими лесами необходимо использовать hello Следующая точка подключения службы hello toocreate скрипта в каждом лесу, где компьютеры находятся:
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a>Шаг 2. Настройка выдачи утверждений

В федеративной Azure конфигурации AD устройства зависят от служб федерации Active Directory (AD FS) или сторонний локальной tooAzure tooauthenticate службы федерации AD. Устройства проходят проверку подлинности tooget tooregister токена доступа от hello Azure Active Directory службы регистрации устройств (Azure DRS).

Windows текущего устройства проходят проверку подлинности с помощью встроенной проверки подлинности Windows tooan active WS-Trust конечной точки (версии 1.3 или 2005) размещенной службой федерации hello в локальной среде.

> [!NOTE]
> При использовании AD необходимо включить **adfs/services/trust/13/windowstransport** или **adfs/services/trust/2005/windowstransport**. При использовании веб-проверки подлинности прокси hello также убедиться, что эта конечная точка публикуется через прокси-сервер hello. Можно увидеть, какие конечные точки включаются с помощью консоли управления AD FS hello под **службы > конечные точки**.
>
>При отсутствии в вашей локальной службой федерации AD FS, следуйте инструкциям hello из вашего поставщика toomake том, что они поддерживают WS-Trust 1.3 или 2005 конечных точек и что они публикуются с помощью hello файл обмена метаданными (MEX).

Hello следующие утверждения должен существовать в токен hello полученных Azure DRS для toocomplete регистрации устройства. В Azure AD с некоторые из этих сведений, который затем используется объектом Azure AD Connect tooassociate hello вновь созданные устройства с hello компьютера учетная запись локальной Azure DRS создаст объект устройства.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Если имеется более одного проверенное имя домена, необходимо tooprovide hello после утверждения для компьютеров:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Если вы выдаете уже утверждение ImmutableID (например, альтернативного идентификатора входа) необходимо tooprovide одного соответствующего утверждения для компьютеров.

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

В следующих разделах hello можно найти сведения о:
 
- Hello значения должны иметь каждое утверждение
- как выглядит определение в AD FS.

Определение Hello помогает tooverify присутствуют ли значения hello, или если требуется toocreate их.

> [!NOTE]
> Если вы не используете службы федерации Active Directory для локального сервера федерации, выполните к поставщику инструкции toocreate hello соответствующей конфигурации tooissue эти утверждения.

### <a name="issue-account-type-claim"></a>Выдача утверждений для типа учетной записи

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**— Это утверждение должно содержать значение **DJ**, который идентифицирует hello устройства как компьютер к домену. В AD FS вы можете добавить правила преобразования выдачи, например такие:

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>Проблема objectGUID hello компьютера учетная запись локальных

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**— Это утверждение должно содержать hello **objectGUID** значение hello локальной учетной записи компьютера. В AD FS вы можете добавить правила преобразования выдачи, например такие:

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>Проблема objectSID hello компьютера учетная запись локальных

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**— Это утверждение должно содержать hello hello **objectSid** значение hello локальной учетной записи компьютера. В AD FS вы можете добавить правила преобразования выдачи, например такие:

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>Выдача issuerID для компьютера при наличии нескольких проверенных доменных имен в Azure AD

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**— Это утверждение должно содержать hello, универсальный код ресурса (URI) любого hello проверить доменных имен, которые подключаются с hello локальный маркер выдающий hello федерации службы (AD FS или третьих сторон). В AD FS можно добавить правила преобразования выдачи, выглядят hello те ниже в этом определенном порядке после hello те выше. Обратите правила hello одно правило tooexplicitly проблемы для пользователей не требуется. В правилах hello ниже добавляется первого правила идентификации пользователя и проверки подлинности компьютера.

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


В приведенном выше утверждений hello

- `$<domain>`URL-адрес службы hello AD FS
- `<verified-domain-name>`— Это, необходимо tooreplace с одним из имен проверенного домена в Azure AD



Дополнительные сведения об именах проверенных доменов см. в разделе [добавить tooAzure имя пользовательского домена Active Directory](active-directory-add-domain.md).  
tooget список доменов проверенных компании, можно использовать hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) командлета. 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>Выдача ImmutableID для компьютера, если он уже существует для пользователей (например, в качестве альтернативного имени для входа)

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**. Это утверждение должно содержать допустимое значение для компьютеров. В AD FS можно создать такие правила преобразования выдачи:

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>Вспомогательный hello AD toocreate сценария FS правил преобразования выдачи

Hello следующий сценарий поможет вам с созданием hello выдачи hello преобразования правила, описанные выше.

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a>Примечания 

- Этот сценарий добавляет hello правила toohello существующие правила. Сценарий hello не выполняются дважды поскольку hello набор правил следует добавить в два раза. Убедитесь, что существует нет соответствующего правила для утверждения (при соответствующих условиях hello) перед повторным запуском сценария hello.

- Если имеется несколько проверенных имен доменов (как показано на портале hello Azure AD или с помощью командлета Get-MsolDomains hello), задайте значение hello **$multipleVerifiedDomainNames** в hello скрипт слишком**$true**. Также не забудьте удалить все существующие утверждения issuerid, которые могли создаваться в Azure AD Connect или другими средствами. Вот пример для этого правила:


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Если уже была выполнена **ImmutableID** утверждения для учетных записей пользователей, задайте значение hello **$immutableIDAlreadyIssuedforUsers** в hello скрипт слишком**$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Шаг 3. Устройства Windows нижнего уровня

Если некоторые из присоединенных к домену устройств являются устройствами Windows нижнего уровня, выполните следующие действия:

- Задайте политику в Azure AD tooenable tooregister устройствах пользователей.
 
- Настройка утверждений вашей локальной службы федерации tooissue toosupport **встроенной проверки подлинности Windows (IWA)** для регистрации устройств.
 
- Добавьте hello Azure AD устройства проверки подлинности конечной точки toohello локальной интрасети зоны, запрашивает сертификат tooavoid при проверке подлинности устройства hello.

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>Настройте политику в Azure AD tooenable tooregister устройствах пользователей

tooregister Windows низкого уровня устройства, вы должны toomake правильность установки, hello задание пользователей tooallow tooregister устройств в Azure AD. В hello портал Azure можно найти этот параметр в разделе:

`Azure Active Directory > Users and groups > Device settings`
    
Hello следующие политика должна быть установлена слишком**все**: **пользователи могут регистрировать свои устройства в Azure AD**

![Регистрация устройств](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Настройка локальной службы федерации 

Локальные службы федерации должен поддерживать выдающий hello **authenticationmehod** и **wiaormultiauthn** утверждений при получении проверку подлинности запроса с проверяющей стороной toohello Azure AD resouce_params параметр с закодированное значение, как показано ниже:

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Когда такой запрос поступает, hello локальной службе федерации должен пройти проверку подлинности пользователя hello, используя встроенную проверку подлинности Windows и после успешного выполнения, следует учесть следующие два утверждения hello:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

В AD FS необходимо добавить правил преобразования выдачи, метод проверки подлинности через передает hello.  

**tooadd этого правила:**

1. В консоли управления hello AD FS, перейдите слишком`AD FS > Trust Relationships > Relying Party Trusts`.
2. Щелкните правой кнопкой мыши объект доверия проверяющей стороны hello платформой удостоверений Microsoft Office 365, а затем выберите **изменение правил для утверждений**.
3. На hello **правила преобразования выдачи** выберите **добавить правило**.
4. В hello **правило для утверждений** список шаблонов, выберите **Отправка утверждений с помощью настраиваемого правила**.
5. Щелкните **Далее**.
6. В hello **имени правила утверждения** введите **Auth Method Claim Rule**.
7. В hello **правило для утверждений** поле, тип hello следующие правила:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. На сервере федерации, введите указанную ниже команду PowerShell hello после замены  **\<RPObjectName\>**  с hello имя объекта проверяющей стороны для объекта отношений доверия проверяющей стороны Azure AD. Как правило, этот объект называется **платформой удостоверений Microsoft Office 365**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>Добавьте hello Azure AD устройства проверки подлинности конечной точки toohello Местная интрасеть зоны

сертификат tooavoid запрос при tooAzure AD, можно отправить политики tooyour устройств, присоединенных к домену tooadd hello следующий URL-адрес toohello местной интрасети в Internet Explorer, проверка подлинности пользователей в регистрации устройств:

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Шаг 4. Контроль развертывания

После завершения шагов требуется hello, присоединенных к домену устройства, готовы tooautomatically регистрацию в Azure AD. Все присоединенные к домену устройства под управлением юбилейного обновления Windows 10 и Windows Server 2016 будут выполнять автоматическую регистрацию в Azure AD при перезагрузке устройства и при входе пользователя. Зарегистрировать новые устройства при перезагрузке устройства hello после завершения операции присоединения домена hello Azure AD.

Устройствах, которые были ранее присоединено к рабочему месту tooAzure AD (например, для Windows Intune) перехода слишком»*, присоединенных к домену, зарегистрировано в AAD*«, однако он займет некоторое время для этого процесса toocomplete на всех устройствах из-за toohello обычный поток операций домена и пользователя.

### <a name="remarks"></a>Примечания

- Можно использовать объект групповой политики toocontrol hello развертывания автоматической регистрации Windows 10 и компьютеров, присоединенных к домену Windows Server 2016.

- Windows 10 ноября 2015 г. Автоматическое обновление регистров с помощью Azure AD **только** Если hello объекта групповой политики развертывания.

- Автоматическая регистрация toorollout hello компьютеров нижнего уровня Windows, вы можете развернуть [пакет установщика Windows](#windows-installer-packages-for-non-windows-10-computers) toocomputers, который выбран.

- При отправке hello групповой политики объект tooWindows 8.1 к домену устройства будет предпринята попытка регистрации; Однако рекомендуется использовать hello [пакет установщика Windows](#windows-installer-packages-for-non-windows-10-computers) tooregister все устройства Windows низкого уровня. 

### <a name="create-a-group-policy-object"></a>Создание объекта групповой политики 

Выделение hello toocontrol Автоматическая регистрация текущей компьютеров Windows, следует развернуть hello **регистрации присоединенных к домену компьютеров в качестве устройства** устройств toohello объекта групповой политики, необходимо tooregister. Например можно развернуть hello политики tooan подразделение или группу безопасности tooa.

**политика hello tooset:**

1. Откройте **диспетчера сервера**, а затем перейдите слишком`Tools > Group Policy Management`.
2. Перейдите toohello домена узел, соответствующий toohello домена, где tooactivate функции автоматической регистрации текущего компьютеров Windows.
3. Щелкните правой кнопкой мыши **Объекты групповой политики**, а затем выберите **Создать**.
4. Введите имя объекта групповой политики. Например *tooAzure Автоматическая регистрация AD*. Нажмите кнопку **ОК**.
5. Щелкните новый объект групповой политики правой кнопкой мыши, а затем выберите **Изменить**.
6. Go слишком**Конфигурация компьютера** > **политики** > **административные шаблоны** > **Windows Компоненты** > **регистрацию устройств**. Щелкните правой кнопкой мыши пункт **Зарегистрировать подключенные к домену компьютеры в качестве устройств** и выберите **Изменить**.
   
   > [!NOTE]
   > Этот шаблон групповой политики был переименован из более ранних версий hello консоли управления групповыми политиками. При использовании более ранней версии консоли hello go слишком`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Выберите параметр **Включено**, а затем — **Применить**.
8. Нажмите кнопку **ОК**.
9. Здравствуйте, ссылка выбранное расположение tooa объекта групповой политики. Например ее можно связать tooa конкретного подразделения. Можно также связать его tooa определенной группе безопасности компьютеров, которые автоматически зарегистрированы в Azure AD. tooset эту политику для всех присоединенных к домену Windows 10 и Windows Server 2016 компьютеров в вашей организации ссылку hello Групповая политика объекта toohello домен.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Пакеты установщика Windows для компьютеров, не работающих на базе Windows 10

присоединенных к домену компьютеров нижнего уровня Windows tooregister в федеративной среде, можно загрузить и установить эти пакет установщика Windows (.msi) из центра загрузки Майкрософт на hello [Майкрософт для компьютеров Windows 10крабочемуместу](https://www.microsoft.com/en-us/download/details.aspx?id=53554) страницы.

С помощью системы распространения программного обеспечения, такие как System Center Configuration Manager, можно развернуть пакет hello. Hello пакет поддерживает hello стандартные параметры автоматической установки с hello *тихий* параметра. Текущей ветви System Center Configuration Manager предлагает дополнительные преимущества от более ранней версии, такие как hello возможность tootrack завершения регистрации. Дополнительные сведения см. на странице [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

Hello установщик создает запланированные задачи hello системе, которая выполняется в контексте пользователя hello. При входе пользователя hello tooWindows, запускается задание Hello. задачу Hello автоматически регистрирует устройство hello Azure AD с учетными данными пользователя hello после проверки подлинности с помощью встроенной проверки подлинности Windows. toosee hello запланированное задание, в устройстве hello go слишком**Microsoft** > **к рабочему месту**, и затем перейти toohello Библиотека планировщика заданий.

## <a name="step-5-verify-registered-devices"></a>Шаг 5. Проверка зарегистрированных устройств

Можно проверить успешно зарегистрированные устройства в вашей организации с помощью hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) командлета в hello [модуля Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

выходные данные командлета Hello показывает устройства, зарегистрированные в Azure AD. tooget все устройства используют hello **-все** параметра, а затем фильтр их с помощью hello **deviceTrustType** свойство. У присоединенных к домену устройств оно имеет значение **Domain Joined**.

## <a name="next-steps"></a>Дальнейшие действия

* [Azure Active Directory automatic device registration FAQ](active-directory-device-registration-faq.md) (Часто задаваемые вопросы об автоматической регистрации устройств)
* [Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD – Windows 10 и Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)
* [Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD – Windows 10](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [Условный доступ в Azure Active Directory](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
