---
title: "устройств, присоединенных к aaaHow tooconfigure гибридной Azure Active Directory | Документы Microsoft"
description: "Узнайте, как tooconfigure гибридной Azure Active Directory устройств, присоединенных к."
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
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: f97ea436eca2833d8a9843acd19e5c633bc0fc07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-hybrid-azure-active-directory-joined-devices"></a><span data-ttu-id="98787-103">Как tooconfigure гибридной Azure Active Directory устройств, присоединенных к</span><span class="sxs-lookup"><span data-stu-id="98787-103">How tooconfigure hybrid Azure Active Directory joined devices</span></span>

<span data-ttu-id="98787-104">Благодаря управлению устройствами в Azure Active Directory (Azure AD) ваши пользователи получают доступ к ресурсам с устройств, которые соответствуют стандартам безопасности и нормативным требованиям.</span><span class="sxs-lookup"><span data-stu-id="98787-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> <span data-ttu-id="98787-105">Дополнительные сведения см. в разделе [управления toodevice введение в Azure Active Directory](device-management-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="98787-105">For more details, see [Introduction toodevice management in Azure Active Directory](device-management-introduction.md).</span></span>

<span data-ttu-id="98787-106">Если в локальной среде Active Directory, и требуется toojoin tooAzure вашего устройства, присоединенные к домену AD, это можно сделать путем настройки устройства гибридной Azure AD, которые присоединены.</span><span class="sxs-lookup"><span data-stu-id="98787-106">If you have an on-premises Active Directory environment and you want toojoin your domain-joined devices tooAzure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span></span> <span data-ttu-id="98787-107">раздел Hello содержит hello связанные действия.</span><span class="sxs-lookup"><span data-stu-id="98787-107">hello topic provides you with hello related steps.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="98787-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="98787-108">Before you begin</span></span>

<span data-ttu-id="98787-109">Перед началом настройки Azure AD гибридных устройств, присоединенных к в вашей среде, следует ознакомиться с ограничениями hello и сценариях hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="98787-109">Before you start configuring hybrid Azure AD joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="98787-110">удобочитаемость hello tooimprove описаний hello, в этом разделе используются следующие термин hello.</span><span class="sxs-lookup"><span data-stu-id="98787-110">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="98787-111">**Текущий устройств Windows** -этот термин обозначает toodomain устройств под управлением Windows 10 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="98787-111">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="98787-112">**Устройства Windows низкого уровня** -этот термин обозначает tooall **поддерживается** присоединенных к домену устройств Windows, которые не являются запущенной Windows 10 и Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="98787-112">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="98787-113">Текущие устройства Windows</span><span class="sxs-lookup"><span data-stu-id="98787-113">Windows current devices</span></span>

- <span data-ttu-id="98787-114">Для устройств под управлением операционной системы hello Windows, мы рекомендуем использовать обновления окончания действия (версии 1607) для Windows 10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="98787-114">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="98787-115">Здравствуйте, регистрации текущего устройств Windows **—** поддерживается в средах, не относящихся к федерации, таких как конфигурации синхронизации хеша пароля.</span><span class="sxs-lookup"><span data-stu-id="98787-115">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="98787-116">Устройства Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="98787-116">Windows down-level devices</span></span>

- <span data-ttu-id="98787-117">поддерживаются следующие устройства нижнего уровня Windows Hello:</span><span class="sxs-lookup"><span data-stu-id="98787-117">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="98787-118">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="98787-118">Windows 8.1</span></span>
    - <span data-ttu-id="98787-119">Windows 7</span><span class="sxs-lookup"><span data-stu-id="98787-119">Windows 7</span></span>
    - <span data-ttu-id="98787-120">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="98787-120">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="98787-121">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="98787-121">Windows Server 2012</span></span>
    - <span data-ttu-id="98787-122">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="98787-122">Windows Server 2008 R2</span></span>
- <span data-ttu-id="98787-123">Здравствуйте, регистрации устройств Windows низкого уровня **—** поддерживается в нефедеративных сред с помощью комплексной Single Sign On [Azure Active Directory прозрачную единого входа](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="98787-123">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="98787-124">Здравствуйте, регистрации устройств Windows низкого уровня **не** поддерживается для устройств с помощью перемещаемых профилей.</span><span class="sxs-lookup"><span data-stu-id="98787-124">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="98787-125">Если вам требуются перемещаемые профили или параметры, используйте только Windows 10.</span><span class="sxs-lookup"><span data-stu-id="98787-125">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="98787-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="98787-126">Prerequisites</span></span>

<span data-ttu-id="98787-127">Прежде чем начать включение гибридного Azure AD объединить устройств в вашей организации, необходимо toomake, что используется последняя версия Azure AD подключения.</span><span class="sxs-lookup"><span data-stu-id="98787-127">Before you start enabling hybrid Azure AD joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="98787-128">Azure AD Connect выполняет следующие функции:</span><span class="sxs-lookup"><span data-stu-id="98787-128">Azure AD Connect:</span></span>

- <span data-ttu-id="98787-129">Сохраняет hello связь между hello учетной записи компьютера в вашей локальной Active Directory (AD) и hello объекта устройства в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98787-129">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="98787-130">Поддерживает другие функции, связанные с устройствами, например Windows Hello для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="98787-130">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="98787-131">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="98787-131">Configuration steps</span></span>

<span data-ttu-id="98787-132">Гибридные устройства, присоединенные к Azure AD, можно настроить для различных типов платформ устройств Windows.</span><span class="sxs-lookup"><span data-stu-id="98787-132">You can configure hybrid Azure AD joined devices for various types of Windows device platforms.</span></span> <span data-ttu-id="98787-133">Этот раздел содержит hello необходимые действия для всех сценариев стандартной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="98787-133">This topic includes hello required steps for all typical configuration scenarios.</span></span>  

<span data-ttu-id="98787-134">Используйте следующие таблицы tooget hello этапы, необходимые для вашего сценария hello.</span><span class="sxs-lookup"><span data-stu-id="98787-134">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="98787-135">Действия</span><span class="sxs-lookup"><span data-stu-id="98787-135">Steps</span></span>                                      | <span data-ttu-id="98787-136">Текущие устройства Windows и синхронизация хэша паролей</span><span class="sxs-lookup"><span data-stu-id="98787-136">Windows current and password hash sync</span></span> | <span data-ttu-id="98787-137">Текущие устройства Windows и федерация</span><span class="sxs-lookup"><span data-stu-id="98787-137">Windows current and federation</span></span> | <span data-ttu-id="98787-138">Устройства Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="98787-138">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="98787-139">Шаг 1. Настройка точки подключения службы</span><span class="sxs-lookup"><span data-stu-id="98787-139">Step 1: Configure service connection point</span></span> | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |
| <span data-ttu-id="98787-143">Шаг 2. Настройка выдачи утверждений</span><span class="sxs-lookup"><span data-stu-id="98787-143">Step 2: Setup issuance of claims</span></span>           |                                        | ![Проверка][1]                    | ![Проверка][1]        |
| <span data-ttu-id="98787-146">Шаг 3. Включение поддержки устройств с ОС, отличными от Windows 10</span><span class="sxs-lookup"><span data-stu-id="98787-146">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Проверка][1]        |
| <span data-ttu-id="98787-148">Шаг 4. Контроль развертывания</span><span class="sxs-lookup"><span data-stu-id="98787-148">Step 4: Control deployment and rollout</span></span>     | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |
| <span data-ttu-id="98787-152">Шаг 5. Проверка присоединенных устройств</span><span class="sxs-lookup"><span data-stu-id="98787-152">Step 5: Verify joined devices</span></span>          | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="98787-156">Шаг 1. Настройка точки подключения службы</span><span class="sxs-lookup"><span data-stu-id="98787-156">Step 1: Configure service connection point</span></span>

<span data-ttu-id="98787-157">объект точки (SCP) для подключения служб Hello используется устройствами во время регистрации hello toodiscover информацию о клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98787-157">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="98787-158">В вашей локальной Active Directory (AD) объект hello SCP для устройств Azure AD объединить гибридного hello должен существовать в раздел конфигурации именования hello контекст компьютера hello леса.</span><span class="sxs-lookup"><span data-stu-id="98787-158">In your on-premises Active Directory (AD), hello SCP object for hello hybrid Azure AD joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="98787-159">В каждом лесу существует только один контекст именования конфигурации.</span><span class="sxs-lookup"><span data-stu-id="98787-159">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="98787-160">В конфигурации с несколькими лесами Active Directory точка подключения службы hello должны находиться во всех лесах, содержащих компьютеров, присоединенных к домену.</span><span class="sxs-lookup"><span data-stu-id="98787-160">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="98787-161">Можно использовать hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) командлет tooretrieve hello контекст именования конфигурации своего леса.</span><span class="sxs-lookup"><span data-stu-id="98787-161">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="98787-162">Для леса с именем домена Active Directory hello *fabrikam.com*, контекст именования конфигурации hello:</span><span class="sxs-lookup"><span data-stu-id="98787-162">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="98787-163">В вашем лесу hello SCP объекта для автоматической регистрации hello устройств, присоединенных к домену в каталоге:</span><span class="sxs-lookup"><span data-stu-id="98787-163">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="98787-164">В зависимости от того, как вы развернули Azure AD Connect hello объекта точки подключения службы может быть уже настроен.</span><span class="sxs-lookup"><span data-stu-id="98787-164">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="98787-165">Можно проверить существование hello объекта hello и извлечь значения обнаружения hello, с помощью hello следующий сценарий Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="98787-165">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="98787-166">Hello **$scp. Ключевые слова** выходные данные показывают сведения о клиенте hello Azure AD, например:</span><span class="sxs-lookup"><span data-stu-id="98787-166">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="98787-167">Если точка подключения службы hello не существует, то можно создать, запустив hello `Initialize-ADSyncDomainJoinedComputerSync` командлета на сервере Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="98787-167">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="98787-168">Учетные данные администратора предприятия является обязательным toorun этого командлета.</span><span class="sxs-lookup"><span data-stu-id="98787-168">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="98787-169">Hello командлета:</span><span class="sxs-lookup"><span data-stu-id="98787-169">hello cmdlet:</span></span>

- <span data-ttu-id="98787-170">Создает точку подключения службы hello в лесу Active Directory hello подключения Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="98787-170">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="98787-171">Требует toospecify hello `AdConnectorAccount` параметра.</span><span class="sxs-lookup"><span data-stu-id="98787-171">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="98787-172">Это учетная запись hello, настроенный как Active Directory, подключение соединителя учетной записи в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98787-172">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="98787-173">Hello следующий скрипт показывает пример использования командлета hello.</span><span class="sxs-lookup"><span data-stu-id="98787-173">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="98787-174">В этом сценарии `$aadAdminCred = Get-Credential` требует tootype имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98787-174">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="98787-175">Требуется имя пользователя tooprovide hello в формате имени участника (UPN) пользователя hello (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="98787-175">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="98787-176">Hello `Initialize-ADSyncDomainJoinedComputerSync` командлета:</span><span class="sxs-lookup"><span data-stu-id="98787-176">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="98787-177">Использует модуль Active Directory PowerShell hello, которое зависит от веб-службы Active Directory, на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="98787-177">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="98787-178">Поддержку веб-служб Active Directory выполняют контроллеры домена под управлением Windows Server 2008 R2 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="98787-178">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="98787-179">Поддерживается только hello **MSOnline PowerShell версии модуля 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="98787-179">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="98787-180">toodownload этот модуль используется [ссылку](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="98787-180">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="98787-181">Для контроллеров домена под управлением Windows Server 2008 или более ранних версий используйте ниже точка подключения службы hello toocreate сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="98787-181">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="98787-182">В конфигурации с несколькими лесами необходимо использовать hello Следующая точка подключения службы hello toocreate скрипта в каждом лесу, где компьютеры находятся:</span><span class="sxs-lookup"><span data-stu-id="98787-182">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="98787-183">Шаг 2. Настройка выдачи утверждений</span><span class="sxs-lookup"><span data-stu-id="98787-183">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="98787-184">В федеративной Azure конфигурации AD устройства зависят от служб федерации Active Directory (AD FS) или сторонний локальной tooAzure tooauthenticate службы федерации AD.</span><span class="sxs-lookup"><span data-stu-id="98787-184">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="98787-185">Устройства проходят проверку подлинности tooget tooregister токена доступа от hello Azure Active Directory службы регистрации устройств (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="98787-185">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="98787-186">Windows текущего устройства проходят проверку подлинности с помощью встроенной проверки подлинности Windows tooan active WS-Trust конечной точки (версии 1.3 или 2005) размещенной службой федерации hello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="98787-186">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="98787-187">При использовании AD необходимо включить **adfs/services/trust/13/windowstransport** или **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="98787-187">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="98787-188">При использовании веб-проверки подлинности прокси hello также убедиться, что эта конечная точка публикуется через прокси-сервер hello.</span><span class="sxs-lookup"><span data-stu-id="98787-188">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="98787-189">Можно увидеть, какие конечные точки включаются с помощью консоли управления AD FS hello под **службы > конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="98787-189">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="98787-190">При отсутствии в вашей локальной службой федерации AD FS, следуйте инструкциям hello из вашего поставщика toomake том, что они поддерживают WS-Trust 1.3 или 2005 конечных точек и что они публикуются с помощью hello файл обмена метаданными (MEX).</span><span class="sxs-lookup"><span data-stu-id="98787-190">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="98787-191">Hello следующие утверждения должен существовать в токен hello полученных Azure DRS для toocomplete регистрации устройства.</span><span class="sxs-lookup"><span data-stu-id="98787-191">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="98787-192">В Azure AD с некоторые из этих сведений, который затем используется объектом Azure AD Connect tooassociate hello вновь созданные устройства с hello компьютера учетная запись локальной Azure DRS создаст объект устройства.</span><span class="sxs-lookup"><span data-stu-id="98787-192">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="98787-193">Если имеется более одного проверенное имя домена, необходимо tooprovide hello после утверждения для компьютеров:</span><span class="sxs-lookup"><span data-stu-id="98787-193">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="98787-194">Если вы выдаете уже утверждение ImmutableID (например, альтернативного идентификатора входа) необходимо tooprovide одного соответствующего утверждения для компьютеров.</span><span class="sxs-lookup"><span data-stu-id="98787-194">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="98787-195">В следующих разделах hello можно найти сведения о:</span><span class="sxs-lookup"><span data-stu-id="98787-195">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="98787-196">Hello значения должны иметь каждое утверждение</span><span class="sxs-lookup"><span data-stu-id="98787-196">hello values each claim should have</span></span>
- <span data-ttu-id="98787-197">как выглядит определение в AD FS.</span><span class="sxs-lookup"><span data-stu-id="98787-197">How a definition would look like in AD FS</span></span>

<span data-ttu-id="98787-198">Определение Hello помогает tooverify присутствуют ли значения hello, или если требуется toocreate их.</span><span class="sxs-lookup"><span data-stu-id="98787-198">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="98787-199">Если вы не используете службы федерации Active Directory для локального сервера федерации, выполните к поставщику инструкции toocreate hello соответствующей конфигурации tooissue эти утверждения.</span><span class="sxs-lookup"><span data-stu-id="98787-199">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="98787-200">Выдача утверждений для типа учетной записи</span><span class="sxs-lookup"><span data-stu-id="98787-200">Issue account type claim</span></span>

<span data-ttu-id="98787-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**— Это утверждение должно содержать значение **DJ**, который идентифицирует hello устройства как компьютер к домену.</span><span class="sxs-lookup"><span data-stu-id="98787-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="98787-202">В AD FS вы можете добавить правила преобразования выдачи, например такие:</span><span class="sxs-lookup"><span data-stu-id="98787-202">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="98787-203">Проблема objectGUID hello компьютера учетная запись локальных</span><span class="sxs-lookup"><span data-stu-id="98787-203">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="98787-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**— Это утверждение должно содержать hello **objectGUID** значение hello локальной учетной записи компьютера.</span><span class="sxs-lookup"><span data-stu-id="98787-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="98787-205">В AD FS вы можете добавить правила преобразования выдачи, например такие:</span><span class="sxs-lookup"><span data-stu-id="98787-205">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="98787-206">Проблема objectSID hello компьютера учетная запись локальных</span><span class="sxs-lookup"><span data-stu-id="98787-206">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="98787-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**— Это утверждение должно содержать hello hello **objectSid** значение hello локальной учетной записи компьютера.</span><span class="sxs-lookup"><span data-stu-id="98787-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="98787-208">В AD FS вы можете добавить правила преобразования выдачи, например такие:</span><span class="sxs-lookup"><span data-stu-id="98787-208">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="98787-209">Выдача issuerID для компьютера при наличии нескольких проверенных доменных имен в Azure AD</span><span class="sxs-lookup"><span data-stu-id="98787-209">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="98787-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**— Это утверждение должно содержать hello, универсальный код ресурса (URI) любого hello проверить доменных имен, которые подключаются с hello локальный маркер выдающий hello федерации службы (AD FS или третьих сторон).</span><span class="sxs-lookup"><span data-stu-id="98787-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="98787-211">В AD FS можно добавить правила преобразования выдачи, выглядят hello те ниже в этом определенном порядке после hello те выше.</span><span class="sxs-lookup"><span data-stu-id="98787-211">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="98787-212">Обратите правила hello одно правило tooexplicitly проблемы для пользователей не требуется.</span><span class="sxs-lookup"><span data-stu-id="98787-212">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="98787-213">В правилах hello ниже добавляется первого правила идентификации пользователя и проверки подлинности компьютера.</span><span class="sxs-lookup"><span data-stu-id="98787-213">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

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


<span data-ttu-id="98787-214">В приведенном выше утверждений hello</span><span class="sxs-lookup"><span data-stu-id="98787-214">In hello claim above,</span></span>

- <span data-ttu-id="98787-215">`$<domain>`URL-адрес службы hello AD FS</span><span class="sxs-lookup"><span data-stu-id="98787-215">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="98787-216">`<verified-domain-name>`— Это, необходимо tooreplace с одним из имен проверенного домена в Azure AD</span><span class="sxs-lookup"><span data-stu-id="98787-216">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="98787-217">Дополнительные сведения об именах проверенных доменов см. в разделе [добавить tooAzure имя пользовательского домена Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="98787-217">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="98787-218">tooget список доменов проверенных компании, можно использовать hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) командлета.</span><span class="sxs-lookup"><span data-stu-id="98787-218">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="98787-220">Выдача ImmutableID для компьютера, если он уже существует для пользователей (например, в качестве альтернативного имени для входа)</span><span class="sxs-lookup"><span data-stu-id="98787-220">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="98787-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**. Это утверждение должно содержать допустимое значение для компьютеров.</span><span class="sxs-lookup"><span data-stu-id="98787-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="98787-222">В AD FS можно создать такие правила преобразования выдачи:</span><span class="sxs-lookup"><span data-stu-id="98787-222">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="98787-223">Вспомогательный hello AD toocreate сценария FS правил преобразования выдачи</span><span class="sxs-lookup"><span data-stu-id="98787-223">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="98787-224">Hello следующий сценарий поможет вам с созданием hello выдачи hello преобразования правила, описанные выше.</span><span class="sxs-lookup"><span data-stu-id="98787-224">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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

### <a name="remarks"></a><span data-ttu-id="98787-225">Примечания</span><span class="sxs-lookup"><span data-stu-id="98787-225">Remarks</span></span> 

- <span data-ttu-id="98787-226">Этот сценарий добавляет hello правила toohello существующие правила.</span><span class="sxs-lookup"><span data-stu-id="98787-226">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="98787-227">Сценарий hello не выполняются дважды поскольку hello набор правил следует добавить в два раза.</span><span class="sxs-lookup"><span data-stu-id="98787-227">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="98787-228">Убедитесь, что существует нет соответствующего правила для утверждения (при соответствующих условиях hello) перед повторным запуском сценария hello.</span><span class="sxs-lookup"><span data-stu-id="98787-228">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="98787-229">Если имеется несколько проверенных имен доменов (как показано на портале hello Azure AD или с помощью командлета Get-MsolDomains hello), задайте значение hello **$multipleVerifiedDomainNames** в hello скрипт слишком**$true**.</span><span class="sxs-lookup"><span data-stu-id="98787-229">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="98787-230">Также не забудьте удалить все существующие утверждения issuerid, которые могли создаваться в Azure AD Connect или другими средствами.</span><span class="sxs-lookup"><span data-stu-id="98787-230">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="98787-231">Вот пример для этого правила:</span><span class="sxs-lookup"><span data-stu-id="98787-231">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="98787-232">Если уже была выполнена **ImmutableID** утверждения для учетных записей пользователей, задайте значение hello **$immutableIDAlreadyIssuedforUsers** в hello скрипт слишком**$true**.</span><span class="sxs-lookup"><span data-stu-id="98787-232">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="98787-233">Шаг 3. Устройства Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="98787-233">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="98787-234">Если некоторые из присоединенных к домену устройств являются устройствами Windows нижнего уровня, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="98787-234">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="98787-235">Задайте политику в Azure AD tooenable tooregister устройствах пользователей.</span><span class="sxs-lookup"><span data-stu-id="98787-235">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="98787-236">Настройка утверждений вашей локальной службы федерации tooissue toosupport **встроенной проверки подлинности Windows (IWA)** для регистрации устройств.</span><span class="sxs-lookup"><span data-stu-id="98787-236">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="98787-237">Добавьте hello Azure AD устройства проверки подлинности конечной точки toohello локальной интрасети зоны, запрашивает сертификат tooavoid при проверке подлинности устройства hello.</span><span class="sxs-lookup"><span data-stu-id="98787-237">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="98787-238">Настройте политику в Azure AD tooenable tooregister устройствах пользователей</span><span class="sxs-lookup"><span data-stu-id="98787-238">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="98787-239">tooregister Windows низкого уровня устройства, вы должны toomake правильность установки, hello задание пользователей tooallow tooregister устройств в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98787-239">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="98787-240">В hello портал Azure можно найти этот параметр в разделе:</span><span class="sxs-lookup"><span data-stu-id="98787-240">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="98787-241">Hello следующие политика должна быть установлена слишком**все**: **пользователи могут регистрировать свои устройства в Azure AD**</span><span class="sxs-lookup"><span data-stu-id="98787-241">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Регистрация устройств](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="98787-243">Настройка локальной службы федерации</span><span class="sxs-lookup"><span data-stu-id="98787-243">Configure on-premises federation service</span></span> 

<span data-ttu-id="98787-244">Локальные службы федерации должен поддерживать выдающий hello **authenticationmehod** и **wiaormultiauthn** утверждений при получении проверку подлинности запроса с проверяющей стороной toohello Azure AD resouce_params параметр с закодированное значение, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="98787-244">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="98787-245">Когда такой запрос поступает, hello локальной службе федерации должен пройти проверку подлинности пользователя hello, используя встроенную проверку подлинности Windows и после успешного выполнения, следует учесть следующие два утверждения hello:</span><span class="sxs-lookup"><span data-stu-id="98787-245">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="98787-246">В AD FS необходимо добавить правил преобразования выдачи, метод проверки подлинности через передает hello.</span><span class="sxs-lookup"><span data-stu-id="98787-246">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="98787-247">**tooadd этого правила:**</span><span class="sxs-lookup"><span data-stu-id="98787-247">**tooadd this rule:**</span></span>

1. <span data-ttu-id="98787-248">В консоли управления hello AD FS, перейдите слишком`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="98787-248">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="98787-249">Щелкните правой кнопкой мыши объект доверия проверяющей стороны hello платформой удостоверений Microsoft Office 365, а затем выберите **изменение правил для утверждений**.</span><span class="sxs-lookup"><span data-stu-id="98787-249">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="98787-250">На hello **правила преобразования выдачи** выберите **добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="98787-250">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="98787-251">В hello **правило для утверждений** список шаблонов, выберите **Отправка утверждений с помощью настраиваемого правила**.</span><span class="sxs-lookup"><span data-stu-id="98787-251">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="98787-252">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="98787-252">Select **Next**.</span></span>
6. <span data-ttu-id="98787-253">В hello **имени правила утверждения** введите **Auth Method Claim Rule**.</span><span class="sxs-lookup"><span data-stu-id="98787-253">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="98787-254">В hello **правило для утверждений** поле, тип hello следующие правила:</span><span class="sxs-lookup"><span data-stu-id="98787-254">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="98787-255">На сервере федерации, введите указанную ниже команду PowerShell hello после замены  **\<RPObjectName\>**  с hello имя объекта проверяющей стороны для объекта отношений доверия проверяющей стороны Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98787-255">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="98787-256">Как правило, этот объект называется **платформой удостоверений Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="98787-256">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="98787-257">Добавьте hello Azure AD устройства проверки подлинности конечной точки toohello Местная интрасеть зоны</span><span class="sxs-lookup"><span data-stu-id="98787-257">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="98787-258">сертификат tooavoid запрос при tooAzure AD, можно отправить политики tooyour устройств, присоединенных к домену tooadd hello следующий URL-адрес toohello местной интрасети в Internet Explorer, проверка подлинности пользователей в регистрации устройств:</span><span class="sxs-lookup"><span data-stu-id="98787-258">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="98787-259">Шаг 4. Контроль развертывания</span><span class="sxs-lookup"><span data-stu-id="98787-259">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="98787-260">После завершения шагов требуется hello, присоединенных к домену устройства, готовы tooautomatically соединения Azure AD:</span><span class="sxs-lookup"><span data-stu-id="98787-260">When you have completed hello required steps, domain-joined devices are ready tooautomatically join Azure AD:</span></span>

- <span data-ttu-id="98787-261">Все присоединенные к домену устройства под управлением юбилейного обновления Windows 10 и Windows Server 2016 будут выполнять автоматическую регистрацию в Azure AD при перезагрузке устройства и при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="98787-261">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> 

- <span data-ttu-id="98787-262">Зарегистрировать новые устройства при перезагрузке устройства hello после завершения операции присоединения домена hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98787-262">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

- <span data-ttu-id="98787-263">Зарегистрированные устройства, которые были ранее Azure AD (например, Windows Intune) слишком переход»*, присоединенных к домену, зарегистрировано в AAD*«, однако он займет некоторое время для этого процесса toocomplete на всех устройствах из-за toohello обычного потока действие, домена и пользователя.</span><span class="sxs-lookup"><span data-stu-id="98787-263">Devices that were previously Azure AD registered (for example, for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="98787-264">Примечания</span><span class="sxs-lookup"><span data-stu-id="98787-264">Remarks</span></span>

- <span data-ttu-id="98787-265">Можно использовать объект групповой политики toocontrol hello развертывания автоматической регистрации Windows 10 и компьютеров, присоединенных к домену Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="98787-265">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="98787-266">Windows 10 ноября 2015 г. обновление автоматически соединяется с Azure AD **только** Если hello объекта групповой политики развертывания.</span><span class="sxs-lookup"><span data-stu-id="98787-266">Windows 10 November 2015 Update automatically joins with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="98787-267">toorollout компьютеров нижнего уровня Windows, вы можете развернуть [пакет установщика Windows](#windows-installer-packages-for-non-windows-10-computers) toocomputers, который выбран.</span><span class="sxs-lookup"><span data-stu-id="98787-267">toorollout of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="98787-268">При отправке hello групповой политики объект tooWindows 8.1 к домену устройства выполняется попытка соединения; Однако рекомендуется использовать hello [пакет установщика Windows](#windows-installer-packages-for-non-windows-10-computers) toojoin все устройства Windows низкого уровня.</span><span class="sxs-lookup"><span data-stu-id="98787-268">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, a join is attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toojoin all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="98787-269">Создание объекта групповой политики</span><span class="sxs-lookup"><span data-stu-id="98787-269">Create a Group Policy object</span></span> 

<span data-ttu-id="98787-270">Выделение hello toocontrol текущего компьютеров Windows, следует развернуть hello **регистрации присоединенных к домену компьютеров в качестве устройства** устройств toohello объекта групповой политики, необходимо tooregister.</span><span class="sxs-lookup"><span data-stu-id="98787-270">toocontrol hello rollout of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="98787-271">Например можно развернуть hello политики tooan подразделение или группу безопасности tooa.</span><span class="sxs-lookup"><span data-stu-id="98787-271">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="98787-272">**политика hello tooset:**</span><span class="sxs-lookup"><span data-stu-id="98787-272">**tooset hello policy:**</span></span>

1. <span data-ttu-id="98787-273">Откройте **диспетчера сервера**, а затем перейдите слишком`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="98787-273">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="98787-274">Перейдите toohello домена узел, соответствующий toohello домена, где tooactivate функции автоматической регистрации текущего компьютеров Windows.</span><span class="sxs-lookup"><span data-stu-id="98787-274">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="98787-275">Щелкните правой кнопкой мыши **Объекты групповой политики**, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="98787-275">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="98787-276">Введите имя объекта групповой политики.</span><span class="sxs-lookup"><span data-stu-id="98787-276">Type a name for your Group Policy object.</span></span> <span data-ttu-id="98787-277">Например, *Гибридное присоединение к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98787-277">For example, *Hybrid Azure AD join.</span></span> 
5. <span data-ttu-id="98787-278">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="98787-278">Click **OK**.</span></span>
6. <span data-ttu-id="98787-279">Щелкните новый объект групповой политики правой кнопкой мыши, а затем выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="98787-279">Right-click your new Group Policy object, and then select **Edit**.</span></span>
7. <span data-ttu-id="98787-280">Go слишком**Конфигурация компьютера** > **политики** > **административные шаблоны** > **Windows Компоненты** > **регистрацию устройств**.</span><span class="sxs-lookup"><span data-stu-id="98787-280">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> 
8. <span data-ttu-id="98787-281">Щелкните правой кнопкой мыши пункт **Зарегистрировать подключенные к домену компьютеры в качестве устройств** и выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="98787-281">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="98787-282">Этот шаблон групповой политики был переименован из более ранних версий hello консоли управления групповыми политиками.</span><span class="sxs-lookup"><span data-stu-id="98787-282">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="98787-283">При использовании более ранней версии консоли hello go слишком`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="98787-283">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="98787-284">Выберите параметр **Включено**, а затем — **Применить**.</span><span class="sxs-lookup"><span data-stu-id="98787-284">Select **Enabled**, and then click **Apply**.</span></span>
8. <span data-ttu-id="98787-285">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="98787-285">Click **OK**.</span></span>
9. <span data-ttu-id="98787-286">Здравствуйте, ссылка выбранное расположение tooa объекта групповой политики.</span><span class="sxs-lookup"><span data-stu-id="98787-286">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="98787-287">Например ее можно связать tooa конкретного подразделения.</span><span class="sxs-lookup"><span data-stu-id="98787-287">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="98787-288">Можно также связать его tooa определенной группе безопасности компьютеров, которые автоматически присоединяется к сообществу Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98787-288">You also could link it tooa specific security group of computers that automatically join with Azure AD.</span></span> <span data-ttu-id="98787-289">tooset эту политику для всех присоединенных к домену Windows 10 и Windows Server 2016 компьютеров в вашей организации ссылку hello Групповая политика объекта toohello домен.</span><span class="sxs-lookup"><span data-stu-id="98787-289">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="98787-290">Пакеты установщика Windows для компьютеров, не работающих на базе Windows 10</span><span class="sxs-lookup"><span data-stu-id="98787-290">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="98787-291">присоединенных к домену компьютеров нижнего уровня Windows toojoin в федеративной среде, можно загрузить и установить эти пакет установщика Windows (.msi) из центра загрузки Майкрософт на hello [присоединения к рабочему месту Майкрософт для компьютеров Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554)страницы.</span><span class="sxs-lookup"><span data-stu-id="98787-291">toojoin domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="98787-292">С помощью системы распространения программного обеспечения, такие как System Center Configuration Manager, можно развернуть пакет hello.</span><span class="sxs-lookup"><span data-stu-id="98787-292">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="98787-293">Hello пакет поддерживает hello стандартные параметры автоматической установки с hello *тихий* параметра.</span><span class="sxs-lookup"><span data-stu-id="98787-293">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="98787-294">Текущей ветви System Center Configuration Manager предлагает дополнительные преимущества от более ранней версии, такие как hello возможность tootrack завершения регистрации.</span><span class="sxs-lookup"><span data-stu-id="98787-294">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="98787-295">Дополнительные сведения см. на странице [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="98787-295">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="98787-296">Hello установщик создает запланированные задачи hello системе, которая выполняется в контексте пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98787-296">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="98787-297">При входе пользователя hello tooWindows, запускается задание Hello.</span><span class="sxs-lookup"><span data-stu-id="98787-297">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="98787-298">задачу Hello автоматически соединяет hello устройство в Azure AD с учетными данными пользователя hello после проверки подлинности с помощью встроенной проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="98787-298">hello task silently joins hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="98787-299">toosee hello запланированное задание, в устройстве hello go слишком**Microsoft** > **к рабочему месту**, и затем перейти toohello Библиотека планировщика заданий.</span><span class="sxs-lookup"><span data-stu-id="98787-299">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-joined-devices"></a><span data-ttu-id="98787-300">Шаг 5. Проверка присоединенных устройств</span><span class="sxs-lookup"><span data-stu-id="98787-300">Step 5: Verify joined devices</span></span>

<span data-ttu-id="98787-301">Можно проверить успешно присоединены к домену устройств в вашей организации с помощью hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) командлета в hello [модуля Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="98787-301">You can check successful joined devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="98787-302">выходные данные командлета Hello показывает устройства, которые зарегистрированы и соединить с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98787-302">hello output of this cmdlet shows devices that are registered and joined with Azure AD.</span></span> <span data-ttu-id="98787-303">tooget все устройства используют hello **-все** параметра, а затем фильтр их с помощью hello **deviceTrustType** свойство.</span><span class="sxs-lookup"><span data-stu-id="98787-303">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="98787-304">У присоединенных к домену устройств оно имеет значение **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="98787-304">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98787-305">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98787-305">Next steps</span></span>

* [<span data-ttu-id="98787-306">Управление toodevice введение в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98787-306">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
