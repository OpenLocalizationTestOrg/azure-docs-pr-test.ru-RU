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
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="1b796-103">Как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b796-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="1b796-104">toouse [условного доступа на основе устройств Azure Active Directory](active-directory-conditional-access-azure-portal.md), компьютеры должны быть зарегистрированы в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b796-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="1b796-105">Можно получить список устройств, зарегистрированных в вашей организации с помощью hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) командлета в hello [модуля Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="1b796-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="1b796-106">В этой статье предоставляет hello шаги по настройке hello автоматической регистрации присоединенных к домену устройств Windows с помощью Azure AD в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="1b796-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="1b796-107">Ознакомьтесь также с информацией по смежным темам:</span><span class="sxs-lookup"><span data-stu-id="1b796-107">For more information about:</span></span>

- <span data-ttu-id="1b796-108">Условный доступ описан в статье [Условный доступ в Azure Active Directory — предварительная версия](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1b796-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="1b796-109">Устройства Windows 10 в рабочей области hello и опыт hello усиленной при регистрации в Azure AD см. [Windows 10 для предприятия hello: использование устройств для работы](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b796-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="1b796-110">Windows 10 корпоративный E3 в CSP, в разделе hello [Windows 10 корпоративный E3 в обзоре CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="1b796-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="1b796-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1b796-111">Before you begin</span></span>

<span data-ttu-id="1b796-112">Перед началом настройки hello автоматической регистрации присоединенных к домену устройств Windows в вашей среде, следует ознакомиться с ограничениями hello и сценариях hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1b796-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="1b796-113">удобочитаемость hello tooimprove описаний hello, в этом разделе используются следующие термин hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="1b796-114">**Текущий устройств Windows** -этот термин обозначает toodomain устройств под управлением Windows 10 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="1b796-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="1b796-115">**Устройства Windows низкого уровня** -этот термин обозначает tooall **поддерживается** присоединенных к домену устройств Windows, которые не являются запущенной Windows 10 и Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="1b796-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="1b796-116">Текущие устройства Windows</span><span class="sxs-lookup"><span data-stu-id="1b796-116">Windows current devices</span></span>

- <span data-ttu-id="1b796-117">Для устройств под управлением операционной системы hello Windows, мы рекомендуем использовать обновления окончания действия (версии 1607) для Windows 10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1b796-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="1b796-118">Здравствуйте, регистрации текущего устройств Windows **—** поддерживается в средах, не относящихся к федерации, таких как конфигурации синхронизации хеша пароля.</span><span class="sxs-lookup"><span data-stu-id="1b796-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="1b796-119">Устройства Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="1b796-119">Windows down-level devices</span></span>

- <span data-ttu-id="1b796-120">поддерживаются следующие устройства нижнего уровня Windows Hello:</span><span class="sxs-lookup"><span data-stu-id="1b796-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="1b796-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="1b796-121">Windows 8.1</span></span>
    - <span data-ttu-id="1b796-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="1b796-122">Windows 7</span></span>
    - <span data-ttu-id="1b796-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1b796-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="1b796-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="1b796-124">Windows Server 2012</span></span>
    - <span data-ttu-id="1b796-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="1b796-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="1b796-126">Здравствуйте, регистрации устройств Windows низкого уровня **—** поддерживается в нефедеративных сред с помощью комплексной Single Sign On [Azure Active Directory прозрачную единого входа](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="1b796-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="1b796-127">Здравствуйте, регистрации устройств Windows низкого уровня **не** поддерживается для устройств с помощью перемещаемых профилей.</span><span class="sxs-lookup"><span data-stu-id="1b796-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="1b796-128">Если вам требуются перемещаемые профили или параметры, используйте только Windows 10.</span><span class="sxs-lookup"><span data-stu-id="1b796-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="1b796-129">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1b796-129">Prerequisites</span></span>

<span data-ttu-id="1b796-130">Прежде чем начать включение hello функции автоматической регистрации присоединенных к домену устройств в вашей организации, необходимо toomake, что используется последняя версия Azure AD подключения.</span><span class="sxs-lookup"><span data-stu-id="1b796-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="1b796-131">Azure AD Connect выполняет следующие функции:</span><span class="sxs-lookup"><span data-stu-id="1b796-131">Azure AD Connect:</span></span>

- <span data-ttu-id="1b796-132">Сохраняет hello связь между hello учетной записи компьютера в вашей локальной Active Directory (AD) и hello объекта устройства в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="1b796-133">Поддерживает другие функции, связанные с устройствами, например Windows Hello для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="1b796-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="1b796-134">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="1b796-134">Configuration steps</span></span>

<span data-ttu-id="1b796-135">Этот раздел содержит hello необходимые действия для всех сценариев стандартной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1b796-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="1b796-136">Используйте следующие таблицы tooget hello этапы, необходимые для вашего сценария hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="1b796-137">Действия</span><span class="sxs-lookup"><span data-stu-id="1b796-137">Steps</span></span>                                      | <span data-ttu-id="1b796-138">Текущие устройства Windows и синхронизация хэша паролей</span><span class="sxs-lookup"><span data-stu-id="1b796-138">Windows current and password hash sync</span></span> | <span data-ttu-id="1b796-139">Текущие устройства Windows и федерация</span><span class="sxs-lookup"><span data-stu-id="1b796-139">Windows current and federation</span></span> | <span data-ttu-id="1b796-140">Устройства Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="1b796-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="1b796-141">Шаг 1. Настройка точки подключения службы</span><span class="sxs-lookup"><span data-stu-id="1b796-141">Step 1: Configure service connection point</span></span> | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |
| <span data-ttu-id="1b796-145">Шаг 2. Настройка выдачи утверждений</span><span class="sxs-lookup"><span data-stu-id="1b796-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Проверка][1]                    | ![Проверка][1]        |
| <span data-ttu-id="1b796-148">Шаг 3. Включение поддержки устройств с ОС, отличными от Windows 10</span><span class="sxs-lookup"><span data-stu-id="1b796-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Проверка][1]        |
| <span data-ttu-id="1b796-150">Шаг 4. Контроль развертывания</span><span class="sxs-lookup"><span data-stu-id="1b796-150">Step 4: Control deployment and rollout</span></span>     | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |
| <span data-ttu-id="1b796-154">Шаг 5. Проверка зарегистрированных устройств</span><span class="sxs-lookup"><span data-stu-id="1b796-154">Step 5: Verify registered devices</span></span>          | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="1b796-158">Шаг 1. Настройка точки подключения службы</span><span class="sxs-lookup"><span data-stu-id="1b796-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="1b796-159">объект точки (SCP) для подключения служб Hello используется устройствами во время регистрации hello toodiscover информацию о клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="1b796-160">В вашей локальной Active Directory (AD) hello объекта точки подключения службы для hello функции автоматической регистрации присоединенных к домену устройств должен существовать в раздел конфигурации именования hello контекст компьютера hello леса.</span><span class="sxs-lookup"><span data-stu-id="1b796-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="1b796-161">В каждом лесу существует только один контекст именования конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1b796-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="1b796-162">В конфигурации с несколькими лесами Active Directory точка подключения службы hello должны находиться во всех лесах, содержащих компьютеров, присоединенных к домену.</span><span class="sxs-lookup"><span data-stu-id="1b796-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="1b796-163">Можно использовать hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) командлет tooretrieve hello контекст именования конфигурации своего леса.</span><span class="sxs-lookup"><span data-stu-id="1b796-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="1b796-164">Для леса с именем домена Active Directory hello *fabrikam.com*, контекст именования конфигурации hello:</span><span class="sxs-lookup"><span data-stu-id="1b796-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="1b796-165">В вашем лесу hello SCP объекта для автоматической регистрации hello устройств, присоединенных к домену в каталоге:</span><span class="sxs-lookup"><span data-stu-id="1b796-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="1b796-166">В зависимости от того, как вы развернули Azure AD Connect hello объекта точки подключения службы может быть уже настроен.</span><span class="sxs-lookup"><span data-stu-id="1b796-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="1b796-167">Можно проверить существование hello объекта hello и извлечь значения обнаружения hello, с помощью hello следующий сценарий Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1b796-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="1b796-168">Hello **$scp. Ключевые слова** выходные данные показывают сведения о клиенте hello Azure AD, например:</span><span class="sxs-lookup"><span data-stu-id="1b796-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="1b796-169">Если точка подключения службы hello не существует, то можно создать, запустив hello `Initialize-ADSyncDomainJoinedComputerSync` командлета на сервере Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1b796-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="1b796-170">Учетные данные администратора предприятия является обязательным toorun этого командлета.</span><span class="sxs-lookup"><span data-stu-id="1b796-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="1b796-171">Hello командлета:</span><span class="sxs-lookup"><span data-stu-id="1b796-171">hello cmdlet:</span></span>

- <span data-ttu-id="1b796-172">Создает точку подключения службы hello в лесу Active Directory hello подключения Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1b796-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="1b796-173">Требует toospecify hello `AdConnectorAccount` параметра.</span><span class="sxs-lookup"><span data-stu-id="1b796-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="1b796-174">Это учетная запись hello, настроенный как Active Directory, подключение соединителя учетной записи в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="1b796-175">Hello следующий скрипт показывает пример использования командлета hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="1b796-176">В этом сценарии `$aadAdminCred = Get-Credential` требует tootype имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b796-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="1b796-177">Требуется имя пользователя tooprovide hello в формате имени участника (UPN) пользователя hello (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="1b796-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="1b796-178">Hello `Initialize-ADSyncDomainJoinedComputerSync` командлета:</span><span class="sxs-lookup"><span data-stu-id="1b796-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="1b796-179">Использует модуль Active Directory PowerShell hello, которое зависит от веб-службы Active Directory, на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="1b796-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="1b796-180">Поддержку веб-служб Active Directory выполняют контроллеры домена под управлением Windows Server 2008 R2 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1b796-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="1b796-181">Поддерживается только hello **MSOnline PowerShell версии модуля 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="1b796-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="1b796-182">toodownload этот модуль используется [ссылку](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="1b796-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="1b796-183">Для контроллеров домена под управлением Windows Server 2008 или более ранних версий используйте ниже точка подключения службы hello toocreate сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="1b796-184">В конфигурации с несколькими лесами необходимо использовать hello Следующая точка подключения службы hello toocreate скрипта в каждом лесу, где компьютеры находятся:</span><span class="sxs-lookup"><span data-stu-id="1b796-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="1b796-185">Шаг 2. Настройка выдачи утверждений</span><span class="sxs-lookup"><span data-stu-id="1b796-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="1b796-186">В федеративной Azure конфигурации AD устройства зависят от служб федерации Active Directory (AD FS) или сторонний локальной tooAzure tooauthenticate службы федерации AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="1b796-187">Устройства проходят проверку подлинности tooget tooregister токена доступа от hello Azure Active Directory службы регистрации устройств (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="1b796-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="1b796-188">Windows текущего устройства проходят проверку подлинности с помощью встроенной проверки подлинности Windows tooan active WS-Trust конечной точки (версии 1.3 или 2005) размещенной службой федерации hello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="1b796-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="1b796-189">При использовании AD необходимо включить **adfs/services/trust/13/windowstransport** или **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="1b796-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="1b796-190">При использовании веб-проверки подлинности прокси hello также убедиться, что эта конечная точка публикуется через прокси-сервер hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="1b796-191">Можно увидеть, какие конечные точки включаются с помощью консоли управления AD FS hello под **службы > конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="1b796-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="1b796-192">При отсутствии в вашей локальной службой федерации AD FS, следуйте инструкциям hello из вашего поставщика toomake том, что они поддерживают WS-Trust 1.3 или 2005 конечных точек и что они публикуются с помощью hello файл обмена метаданными (MEX).</span><span class="sxs-lookup"><span data-stu-id="1b796-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="1b796-193">Hello следующие утверждения должен существовать в токен hello полученных Azure DRS для toocomplete регистрации устройства.</span><span class="sxs-lookup"><span data-stu-id="1b796-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="1b796-194">В Azure AD с некоторые из этих сведений, который затем используется объектом Azure AD Connect tooassociate hello вновь созданные устройства с hello компьютера учетная запись локальной Azure DRS создаст объект устройства.</span><span class="sxs-lookup"><span data-stu-id="1b796-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="1b796-195">Если имеется более одного проверенное имя домена, необходимо tooprovide hello после утверждения для компьютеров:</span><span class="sxs-lookup"><span data-stu-id="1b796-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="1b796-196">Если вы выдаете уже утверждение ImmutableID (например, альтернативного идентификатора входа) необходимо tooprovide одного соответствующего утверждения для компьютеров.</span><span class="sxs-lookup"><span data-stu-id="1b796-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="1b796-197">В следующих разделах hello можно найти сведения о:</span><span class="sxs-lookup"><span data-stu-id="1b796-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="1b796-198">Hello значения должны иметь каждое утверждение</span><span class="sxs-lookup"><span data-stu-id="1b796-198">hello values each claim should have</span></span>
- <span data-ttu-id="1b796-199">как выглядит определение в AD FS.</span><span class="sxs-lookup"><span data-stu-id="1b796-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="1b796-200">Определение Hello помогает tooverify присутствуют ли значения hello, или если требуется toocreate их.</span><span class="sxs-lookup"><span data-stu-id="1b796-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="1b796-201">Если вы не используете службы федерации Active Directory для локального сервера федерации, выполните к поставщику инструкции toocreate hello соответствующей конфигурации tooissue эти утверждения.</span><span class="sxs-lookup"><span data-stu-id="1b796-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="1b796-202">Выдача утверждений для типа учетной записи</span><span class="sxs-lookup"><span data-stu-id="1b796-202">Issue account type claim</span></span>

<span data-ttu-id="1b796-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**— Это утверждение должно содержать значение **DJ**, который идентифицирует hello устройства как компьютер к домену.</span><span class="sxs-lookup"><span data-stu-id="1b796-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="1b796-204">В AD FS вы можете добавить правила преобразования выдачи, например такие:</span><span class="sxs-lookup"><span data-stu-id="1b796-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="1b796-205">Проблема objectGUID hello компьютера учетная запись локальных</span><span class="sxs-lookup"><span data-stu-id="1b796-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="1b796-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**— Это утверждение должно содержать hello **objectGUID** значение hello локальной учетной записи компьютера.</span><span class="sxs-lookup"><span data-stu-id="1b796-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="1b796-207">В AD FS вы можете добавить правила преобразования выдачи, например такие:</span><span class="sxs-lookup"><span data-stu-id="1b796-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="1b796-208">Проблема objectSID hello компьютера учетная запись локальных</span><span class="sxs-lookup"><span data-stu-id="1b796-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="1b796-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**— Это утверждение должно содержать hello hello **objectSid** значение hello локальной учетной записи компьютера.</span><span class="sxs-lookup"><span data-stu-id="1b796-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="1b796-210">В AD FS вы можете добавить правила преобразования выдачи, например такие:</span><span class="sxs-lookup"><span data-stu-id="1b796-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="1b796-211">Выдача issuerID для компьютера при наличии нескольких проверенных доменных имен в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b796-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="1b796-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**— Это утверждение должно содержать hello, универсальный код ресурса (URI) любого hello проверить доменных имен, которые подключаются с hello локальный маркер выдающий hello федерации службы (AD FS или третьих сторон).</span><span class="sxs-lookup"><span data-stu-id="1b796-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="1b796-213">В AD FS можно добавить правила преобразования выдачи, выглядят hello те ниже в этом определенном порядке после hello те выше.</span><span class="sxs-lookup"><span data-stu-id="1b796-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="1b796-214">Обратите правила hello одно правило tooexplicitly проблемы для пользователей не требуется.</span><span class="sxs-lookup"><span data-stu-id="1b796-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="1b796-215">В правилах hello ниже добавляется первого правила идентификации пользователя и проверки подлинности компьютера.</span><span class="sxs-lookup"><span data-stu-id="1b796-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

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


<span data-ttu-id="1b796-216">В приведенном выше утверждений hello</span><span class="sxs-lookup"><span data-stu-id="1b796-216">In hello claim above,</span></span>

- <span data-ttu-id="1b796-217">`$<domain>`URL-адрес службы hello AD FS</span><span class="sxs-lookup"><span data-stu-id="1b796-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="1b796-218">`<verified-domain-name>`— Это, необходимо tooreplace с одним из имен проверенного домена в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b796-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="1b796-219">Дополнительные сведения об именах проверенных доменов см. в разделе [добавить tooAzure имя пользовательского домена Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="1b796-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="1b796-220">tooget список доменов проверенных компании, можно использовать hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) командлета.</span><span class="sxs-lookup"><span data-stu-id="1b796-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="1b796-222">Выдача ImmutableID для компьютера, если он уже существует для пользователей (например, в качестве альтернативного имени для входа)</span><span class="sxs-lookup"><span data-stu-id="1b796-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="1b796-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**. Это утверждение должно содержать допустимое значение для компьютеров.</span><span class="sxs-lookup"><span data-stu-id="1b796-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="1b796-224">В AD FS можно создать такие правила преобразования выдачи:</span><span class="sxs-lookup"><span data-stu-id="1b796-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="1b796-225">Вспомогательный hello AD toocreate сценария FS правил преобразования выдачи</span><span class="sxs-lookup"><span data-stu-id="1b796-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="1b796-226">Hello следующий сценарий поможет вам с созданием hello выдачи hello преобразования правила, описанные выше.</span><span class="sxs-lookup"><span data-stu-id="1b796-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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

### <a name="remarks"></a><span data-ttu-id="1b796-227">Примечания</span><span class="sxs-lookup"><span data-stu-id="1b796-227">Remarks</span></span> 

- <span data-ttu-id="1b796-228">Этот сценарий добавляет hello правила toohello существующие правила.</span><span class="sxs-lookup"><span data-stu-id="1b796-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="1b796-229">Сценарий hello не выполняются дважды поскольку hello набор правил следует добавить в два раза.</span><span class="sxs-lookup"><span data-stu-id="1b796-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="1b796-230">Убедитесь, что существует нет соответствующего правила для утверждения (при соответствующих условиях hello) перед повторным запуском сценария hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="1b796-231">Если имеется несколько проверенных имен доменов (как показано на портале hello Azure AD или с помощью командлета Get-MsolDomains hello), задайте значение hello **$multipleVerifiedDomainNames** в hello скрипт слишком**$true**.</span><span class="sxs-lookup"><span data-stu-id="1b796-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="1b796-232">Также не забудьте удалить все существующие утверждения issuerid, которые могли создаваться в Azure AD Connect или другими средствами.</span><span class="sxs-lookup"><span data-stu-id="1b796-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="1b796-233">Вот пример для этого правила:</span><span class="sxs-lookup"><span data-stu-id="1b796-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="1b796-234">Если уже была выполнена **ImmutableID** утверждения для учетных записей пользователей, задайте значение hello **$immutableIDAlreadyIssuedforUsers** в hello скрипт слишком**$true**.</span><span class="sxs-lookup"><span data-stu-id="1b796-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="1b796-235">Шаг 3. Устройства Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="1b796-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="1b796-236">Если некоторые из присоединенных к домену устройств являются устройствами Windows нижнего уровня, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1b796-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="1b796-237">Задайте политику в Azure AD tooenable tooregister устройствах пользователей.</span><span class="sxs-lookup"><span data-stu-id="1b796-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="1b796-238">Настройка утверждений вашей локальной службы федерации tooissue toosupport **встроенной проверки подлинности Windows (IWA)** для регистрации устройств.</span><span class="sxs-lookup"><span data-stu-id="1b796-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="1b796-239">Добавьте hello Azure AD устройства проверки подлинности конечной точки toohello локальной интрасети зоны, запрашивает сертификат tooavoid при проверке подлинности устройства hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="1b796-240">Настройте политику в Azure AD tooenable tooregister устройствах пользователей</span><span class="sxs-lookup"><span data-stu-id="1b796-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="1b796-241">tooregister Windows низкого уровня устройства, вы должны toomake правильность установки, hello задание пользователей tooallow tooregister устройств в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="1b796-242">В hello портал Azure можно найти этот параметр в разделе:</span><span class="sxs-lookup"><span data-stu-id="1b796-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="1b796-243">Hello следующие политика должна быть установлена слишком**все**: **пользователи могут регистрировать свои устройства в Azure AD**</span><span class="sxs-lookup"><span data-stu-id="1b796-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Регистрация устройств](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="1b796-245">Настройка локальной службы федерации</span><span class="sxs-lookup"><span data-stu-id="1b796-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="1b796-246">Локальные службы федерации должен поддерживать выдающий hello **authenticationmehod** и **wiaormultiauthn** утверждений при получении проверку подлинности запроса с проверяющей стороной toohello Azure AD resouce_params параметр с закодированное значение, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="1b796-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="1b796-247">Когда такой запрос поступает, hello локальной службе федерации должен пройти проверку подлинности пользователя hello, используя встроенную проверку подлинности Windows и после успешного выполнения, следует учесть следующие два утверждения hello:</span><span class="sxs-lookup"><span data-stu-id="1b796-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="1b796-248">В AD FS необходимо добавить правил преобразования выдачи, метод проверки подлинности через передает hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="1b796-249">**tooadd этого правила:**</span><span class="sxs-lookup"><span data-stu-id="1b796-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="1b796-250">В консоли управления hello AD FS, перейдите слишком`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="1b796-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="1b796-251">Щелкните правой кнопкой мыши объект доверия проверяющей стороны hello платформой удостоверений Microsoft Office 365, а затем выберите **изменение правил для утверждений**.</span><span class="sxs-lookup"><span data-stu-id="1b796-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="1b796-252">На hello **правила преобразования выдачи** выберите **добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="1b796-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="1b796-253">В hello **правило для утверждений** список шаблонов, выберите **Отправка утверждений с помощью настраиваемого правила**.</span><span class="sxs-lookup"><span data-stu-id="1b796-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="1b796-254">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1b796-254">Select **Next**.</span></span>
6. <span data-ttu-id="1b796-255">В hello **имени правила утверждения** введите **Auth Method Claim Rule**.</span><span class="sxs-lookup"><span data-stu-id="1b796-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="1b796-256">В hello **правило для утверждений** поле, тип hello следующие правила:</span><span class="sxs-lookup"><span data-stu-id="1b796-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="1b796-257">На сервере федерации, введите указанную ниже команду PowerShell hello после замены  **\<RPObjectName\>**  с hello имя объекта проверяющей стороны для объекта отношений доверия проверяющей стороны Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="1b796-258">Как правило, этот объект называется **платформой удостоверений Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="1b796-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="1b796-259">Добавьте hello Azure AD устройства проверки подлинности конечной точки toohello Местная интрасеть зоны</span><span class="sxs-lookup"><span data-stu-id="1b796-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="1b796-260">сертификат tooavoid запрос при tooAzure AD, можно отправить политики tooyour устройств, присоединенных к домену tooadd hello следующий URL-адрес toohello местной интрасети в Internet Explorer, проверка подлинности пользователей в регистрации устройств:</span><span class="sxs-lookup"><span data-stu-id="1b796-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="1b796-261">Шаг 4. Контроль развертывания</span><span class="sxs-lookup"><span data-stu-id="1b796-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="1b796-262">После завершения шагов требуется hello, присоединенных к домену устройства, готовы tooautomatically регистрацию в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="1b796-263">Все присоединенные к домену устройства под управлением юбилейного обновления Windows 10 и Windows Server 2016 будут выполнять автоматическую регистрацию в Azure AD при перезагрузке устройства и при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b796-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="1b796-264">Зарегистрировать новые устройства при перезагрузке устройства hello после завершения операции присоединения домена hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="1b796-265">Устройствах, которые были ранее присоединено к рабочему месту tooAzure AD (например, для Windows Intune) перехода слишком»*, присоединенных к домену, зарегистрировано в AAD*«, однако он займет некоторое время для этого процесса toocomplete на всех устройствах из-за toohello обычный поток операций домена и пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b796-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="1b796-266">Примечания</span><span class="sxs-lookup"><span data-stu-id="1b796-266">Remarks</span></span>

- <span data-ttu-id="1b796-267">Можно использовать объект групповой политики toocontrol hello развертывания автоматической регистрации Windows 10 и компьютеров, присоединенных к домену Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="1b796-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="1b796-268">Windows 10 ноября 2015 г. Автоматическое обновление регистров с помощью Azure AD **только** Если hello объекта групповой политики развертывания.</span><span class="sxs-lookup"><span data-stu-id="1b796-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="1b796-269">Автоматическая регистрация toorollout hello компьютеров нижнего уровня Windows, вы можете развернуть [пакет установщика Windows](#windows-installer-packages-for-non-windows-10-computers) toocomputers, который выбран.</span><span class="sxs-lookup"><span data-stu-id="1b796-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="1b796-270">При отправке hello групповой политики объект tooWindows 8.1 к домену устройства будет предпринята попытка регистрации; Однако рекомендуется использовать hello [пакет установщика Windows](#windows-installer-packages-for-non-windows-10-computers) tooregister все устройства Windows низкого уровня.</span><span class="sxs-lookup"><span data-stu-id="1b796-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="1b796-271">Создание объекта групповой политики</span><span class="sxs-lookup"><span data-stu-id="1b796-271">Create a Group Policy object</span></span> 

<span data-ttu-id="1b796-272">Выделение hello toocontrol Автоматическая регистрация текущей компьютеров Windows, следует развернуть hello **регистрации присоединенных к домену компьютеров в качестве устройства** устройств toohello объекта групповой политики, необходимо tooregister.</span><span class="sxs-lookup"><span data-stu-id="1b796-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="1b796-273">Например можно развернуть hello политики tooan подразделение или группу безопасности tooa.</span><span class="sxs-lookup"><span data-stu-id="1b796-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="1b796-274">**политика hello tooset:**</span><span class="sxs-lookup"><span data-stu-id="1b796-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="1b796-275">Откройте **диспетчера сервера**, а затем перейдите слишком`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="1b796-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="1b796-276">Перейдите toohello домена узел, соответствующий toohello домена, где tooactivate функции автоматической регистрации текущего компьютеров Windows.</span><span class="sxs-lookup"><span data-stu-id="1b796-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="1b796-277">Щелкните правой кнопкой мыши **Объекты групповой политики**, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1b796-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="1b796-278">Введите имя объекта групповой политики.</span><span class="sxs-lookup"><span data-stu-id="1b796-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="1b796-279">Например *tooAzure Автоматическая регистрация AD*.</span><span class="sxs-lookup"><span data-stu-id="1b796-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="1b796-280">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1b796-280">Select **OK**.</span></span>
5. <span data-ttu-id="1b796-281">Щелкните новый объект групповой политики правой кнопкой мыши, а затем выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="1b796-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="1b796-282">Go слишком**Конфигурация компьютера** > **политики** > **административные шаблоны** > **Windows Компоненты** > **регистрацию устройств**.</span><span class="sxs-lookup"><span data-stu-id="1b796-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="1b796-283">Щелкните правой кнопкой мыши пункт **Зарегистрировать подключенные к домену компьютеры в качестве устройств** и выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="1b796-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1b796-284">Этот шаблон групповой политики был переименован из более ранних версий hello консоли управления групповыми политиками.</span><span class="sxs-lookup"><span data-stu-id="1b796-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="1b796-285">При использовании более ранней версии консоли hello go слишком`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="1b796-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="1b796-286">Выберите параметр **Включено**, а затем — **Применить**.</span><span class="sxs-lookup"><span data-stu-id="1b796-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="1b796-287">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1b796-287">Select **OK**.</span></span>
9. <span data-ttu-id="1b796-288">Здравствуйте, ссылка выбранное расположение tooa объекта групповой политики.</span><span class="sxs-lookup"><span data-stu-id="1b796-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="1b796-289">Например ее можно связать tooa конкретного подразделения.</span><span class="sxs-lookup"><span data-stu-id="1b796-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="1b796-290">Можно также связать его tooa определенной группе безопасности компьютеров, которые автоматически зарегистрированы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="1b796-291">tooset эту политику для всех присоединенных к домену Windows 10 и Windows Server 2016 компьютеров в вашей организации ссылку hello Групповая политика объекта toohello домен.</span><span class="sxs-lookup"><span data-stu-id="1b796-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="1b796-292">Пакеты установщика Windows для компьютеров, не работающих на базе Windows 10</span><span class="sxs-lookup"><span data-stu-id="1b796-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="1b796-293">присоединенных к домену компьютеров нижнего уровня Windows tooregister в федеративной среде, можно загрузить и установить эти пакет установщика Windows (.msi) из центра загрузки Майкрософт на hello [Майкрософт для компьютеров Windows 10крабочемуместу](https://www.microsoft.com/en-us/download/details.aspx?id=53554) страницы.</span><span class="sxs-lookup"><span data-stu-id="1b796-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="1b796-294">С помощью системы распространения программного обеспечения, такие как System Center Configuration Manager, можно развернуть пакет hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="1b796-295">Hello пакет поддерживает hello стандартные параметры автоматической установки с hello *тихий* параметра.</span><span class="sxs-lookup"><span data-stu-id="1b796-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="1b796-296">Текущей ветви System Center Configuration Manager предлагает дополнительные преимущества от более ранней версии, такие как hello возможность tootrack завершения регистрации.</span><span class="sxs-lookup"><span data-stu-id="1b796-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="1b796-297">Дополнительные сведения см. на странице [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="1b796-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="1b796-298">Hello установщик создает запланированные задачи hello системе, которая выполняется в контексте пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="1b796-299">При входе пользователя hello tooWindows, запускается задание Hello.</span><span class="sxs-lookup"><span data-stu-id="1b796-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="1b796-300">задачу Hello автоматически регистрирует устройство hello Azure AD с учетными данными пользователя hello после проверки подлинности с помощью встроенной проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="1b796-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="1b796-301">toosee hello запланированное задание, в устройстве hello go слишком**Microsoft** > **к рабочему месту**, и затем перейти toohello Библиотека планировщика заданий.</span><span class="sxs-lookup"><span data-stu-id="1b796-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="1b796-302">Шаг 5. Проверка зарегистрированных устройств</span><span class="sxs-lookup"><span data-stu-id="1b796-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="1b796-303">Можно проверить успешно зарегистрированные устройства в вашей организации с помощью hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) командлета в hello [модуля Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="1b796-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="1b796-304">выходные данные командлета Hello показывает устройства, зарегистрированные в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b796-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="1b796-305">tooget все устройства используют hello **-все** параметра, а затем фильтр их с помощью hello **deviceTrustType** свойство.</span><span class="sxs-lookup"><span data-stu-id="1b796-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="1b796-306">У присоединенных к домену устройств оно имеет значение **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="1b796-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b796-307">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b796-307">Next steps</span></span>

* <span data-ttu-id="1b796-308">[Azure Active Directory automatic device registration FAQ](active-directory-device-registration-faq.md) (Часто задаваемые вопросы об автоматической регистрации устройств)</span><span class="sxs-lookup"><span data-stu-id="1b796-308">[Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span>
* [<span data-ttu-id="1b796-309">Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD – Windows 10 и Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="1b796-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="1b796-310">Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD – Windows 10</span><span class="sxs-lookup"><span data-stu-id="1b796-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="1b796-311">Условный доступ в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b796-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
