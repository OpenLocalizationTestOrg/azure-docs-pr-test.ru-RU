---
title: "Как настроить автоматическую регистрацию присоединенных к домену устройств Windows в Azure Active Directory | Документация Майкрософт"
description: "Настройте автоматическую регистрацию устройств Windows, присоединенных к домену, без предупреждений с помощью Azure Active Directory."
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
ms.openlocfilehash: dccd7df6a5f85df4179c7ea7cfc476cfb57f48c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="8b88e-103">Настройка автоматической регистрации присоединенных к домену устройств Windows в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b88e-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="8b88e-104">Для использования [условного доступа на основе устройств в Azure Active Directory](active-directory-conditional-access-azure-portal.md) необходимо зарегистрировать компьютеры в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b88e-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8b88e-105">Список устройств, зарегистрированных в организации, можно получить с помощью командлета [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) в [модуле PowerShell Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="8b88e-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="8b88e-106">В этой статье описана процедура настройки автоматической регистрации присоединенных к домену устройств Windows вашей организации в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b88e-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="8b88e-107">Ознакомьтесь также с информацией по смежным темам:</span><span class="sxs-lookup"><span data-stu-id="8b88e-107">For more information about:</span></span>

- <span data-ttu-id="8b88e-108">Условный доступ описан в статье [Условный доступ в Azure Active Directory — предварительная версия](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8b88e-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="8b88e-109">Сведения об устройствах Windows 10 в рабочей области и об улучшенной процедуре регистрации пользователей в Azure AD см. в статье [Windows 10 для предприятия: использование устройств для работы](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b88e-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="8b88e-110">Сведения о Windows 10 Корпоративная E3 в CSP см. в [этой статье](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="8b88e-110">Windows 10 Enterprise E3 in CSP, see the [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="8b88e-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="8b88e-111">Before you begin</span></span>

<span data-ttu-id="8b88e-112">Прежде чем настраивать в своей среде автоматическую регистрацию присоединенных к домену устройств Windows, ознакомьтесь с ограничениями и поддерживаемыми сценариями.</span><span class="sxs-lookup"><span data-stu-id="8b88e-112">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="8b88e-113">Чтобы упростить описания, в этой статье используются следующие термины.</span><span class="sxs-lookup"><span data-stu-id="8b88e-113">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="8b88e-114">**Текущие устройства Windows.** Это собирательное описание всех присоединенных к домену устройств под управлением Windows 10 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8b88e-114">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="8b88e-115">**Устройства Windows нижнего уровня.** Этот термин относится ко всем **поддерживаемым** устройствам Windows, присоединенным к домену, операционная система которых отлична от Windows 10 и Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8b88e-115">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="8b88e-116">Текущие устройства Windows</span><span class="sxs-lookup"><span data-stu-id="8b88e-116">Windows current devices</span></span>

- <span data-ttu-id="8b88e-117">Для настольных устройств под управлением ОС Windows мы рекомендуем использовать юбилейное обновление Windows 10 (версия 1607) или более позднюю версию.</span><span class="sxs-lookup"><span data-stu-id="8b88e-117">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="8b88e-118">Регистрация текущих устройств Windows **поддерживается** в средах, не являющихся федеративными, например в конфигурациях с синхронизацией хэша паролей.</span><span class="sxs-lookup"><span data-stu-id="8b88e-118">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="8b88e-119">Устройства Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="8b88e-119">Windows down-level devices</span></span>

- <span data-ttu-id="8b88e-120">Поддерживаются устройства Windows нижнего уровня со следующими системами:</span><span class="sxs-lookup"><span data-stu-id="8b88e-120">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="8b88e-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8b88e-121">Windows 8.1</span></span>
    - <span data-ttu-id="8b88e-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8b88e-122">Windows 7</span></span>
    - <span data-ttu-id="8b88e-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8b88e-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="8b88e-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8b88e-124">Windows Server 2012</span></span>
    - <span data-ttu-id="8b88e-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="8b88e-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="8b88e-126">Регистрация устройств Windows нижнего уровня **поддерживается** в средах, не являющихся федеративными, с помощью простого единого входа. [Простой единый вход Azure Active Directory](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="8b88e-126">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="8b88e-127">Регистрация устройств Windows нижнего уровня **не поддерживается** на устройствах с перемещаемыми профилями.</span><span class="sxs-lookup"><span data-stu-id="8b88e-127">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="8b88e-128">Если вам требуются перемещаемые профили или параметры, используйте только Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8b88e-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="8b88e-129">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8b88e-129">Prerequisites</span></span>

<span data-ttu-id="8b88e-130">Прежде чем настроить в организации автоматическую регистрацию присоединенных к домену устройств, обязательно убедитесь в том, что вы используете последнюю версию Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8b88e-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="8b88e-131">Azure AD Connect выполняет следующие функции:</span><span class="sxs-lookup"><span data-stu-id="8b88e-131">Azure AD Connect:</span></span>

- <span data-ttu-id="8b88e-132">Отслеживает связи между учетными записями на компьютерах в локальной среде Active Directory (AD) и объектами устройств в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b88e-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="8b88e-133">Поддерживает другие функции, связанные с устройствами, например Windows Hello для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="8b88e-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="8b88e-134">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="8b88e-134">Configuration steps</span></span>

<span data-ttu-id="8b88e-135">В этом разделе описаны обязательные действия для всех типичных сценариев настройки.</span><span class="sxs-lookup"><span data-stu-id="8b88e-135">This topic includes the required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="8b88e-136">Следующая таблица содержит обзор действий, необходимых для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="8b88e-136">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="8b88e-137">Действия</span><span class="sxs-lookup"><span data-stu-id="8b88e-137">Steps</span></span>                                      | <span data-ttu-id="8b88e-138">Текущие устройства Windows и синхронизация хэша паролей</span><span class="sxs-lookup"><span data-stu-id="8b88e-138">Windows current and password hash sync</span></span> | <span data-ttu-id="8b88e-139">Текущие устройства Windows и федерация</span><span class="sxs-lookup"><span data-stu-id="8b88e-139">Windows current and federation</span></span> | <span data-ttu-id="8b88e-140">Устройства Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="8b88e-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="8b88e-141">Шаг 1. Настройка точки подключения службы</span><span class="sxs-lookup"><span data-stu-id="8b88e-141">Step 1: Configure service connection point</span></span> | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |
| <span data-ttu-id="8b88e-145">Шаг 2. Настройка выдачи утверждений</span><span class="sxs-lookup"><span data-stu-id="8b88e-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Проверка][1]                    | ![Проверка][1]        |
| <span data-ttu-id="8b88e-148">Шаг 3. Включение поддержки устройств с ОС, отличными от Windows 10</span><span class="sxs-lookup"><span data-stu-id="8b88e-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Проверка][1]        |
| <span data-ttu-id="8b88e-150">Шаг 4. Контроль развертывания</span><span class="sxs-lookup"><span data-stu-id="8b88e-150">Step 4: Control deployment and rollout</span></span>     | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |
| <span data-ttu-id="8b88e-154">Шаг 5. Проверка зарегистрированных устройств</span><span class="sxs-lookup"><span data-stu-id="8b88e-154">Step 5: Verify registered devices</span></span>          | ![Проверка][1]                            | ![Проверка][1]                    | ![Проверка][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="8b88e-158">Шаг 1. Настройка точки подключения службы</span><span class="sxs-lookup"><span data-stu-id="8b88e-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="8b88e-159">Объект точки подключения службы (SCP) используется устройствами во время регистрации для получения сведений о клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b88e-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="8b88e-160">В локальной среде Active Directory (AD) должен существовать объект SCP для автоматической регистрации присоединенных к домену устройств, определенный в разделе контекста именования конфигурации в лесу компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8b88e-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="8b88e-161">В каждом лесу существует только один контекст именования конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8b88e-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="8b88e-162">В конфигурации Active Directory с несколькими лесами точка подключения службы должна существовать во всех лесах, содержащих присоединенные к домену компьютеры.</span><span class="sxs-lookup"><span data-stu-id="8b88e-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="8b88e-163">Для получения контекста именования конфигурации для леса можно использовать командлет [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b88e-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="8b88e-164">Для леса, в котором домен Active Directory имеет имя *example.com*, контекст именования конфигурации будет таким:</span><span class="sxs-lookup"><span data-stu-id="8b88e-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="8b88e-165">В лесу объект SCP для автоматической регистрации присоединенных к домену устройств имеет следующее расположение:</span><span class="sxs-lookup"><span data-stu-id="8b88e-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="8b88e-166">В зависимости от того, как выполнялось развертывание Azure AD Connect, объект SCP уже может быть настроен.</span><span class="sxs-lookup"><span data-stu-id="8b88e-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="8b88e-167">Чтобы проверить существование объекта и получить значения для обнаружения, используйте следующий сценарий Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8b88e-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="8b88e-168">В выходных данных **$scp.Keywords** указаны сведения о клиенте Azure AD, такие как показаны ниже:</span><span class="sxs-lookup"><span data-stu-id="8b88e-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="8b88e-169">Если точка подключения службы не существует, создайте ее, выполнив командлет `Initialize-ADSyncDomainJoinedComputerSync` на сервере Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8b88e-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="8b88e-170">Для выполнения этого командлета необходимы учетные данные администратора организации.</span><span class="sxs-lookup"><span data-stu-id="8b88e-170">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="8b88e-171">Этот командлет:</span><span class="sxs-lookup"><span data-stu-id="8b88e-171">The cmdlet:</span></span>

- <span data-ttu-id="8b88e-172">Создает точку подключения службы в лесу Active Directory, к которому подключена служба Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8b88e-172">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="8b88e-173">Требует указать обязательный параметр `AdConnectorAccount`,</span><span class="sxs-lookup"><span data-stu-id="8b88e-173">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="8b88e-174">который обозначает учетную запись, настроенную в Azure AD Connect в качестве учетной записи соединителя Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8b88e-174">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="8b88e-175">Следующий скрипт демонстрирует использование этого командлета.</span><span class="sxs-lookup"><span data-stu-id="8b88e-175">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="8b88e-176">В этом скрипте есть параметр `$aadAdminCred = Get-Credential`, который требует ввести имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="8b88e-176">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="8b88e-177">Имя пользователя следует вводить в формате имени участника-пользователя (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="8b88e-177">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="8b88e-178">Командлет `Initialize-ADSyncDomainJoinedComputerSync`:</span><span class="sxs-lookup"><span data-stu-id="8b88e-178">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="8b88e-179">В этом командлете используется модуль PowerShell для Active Directory, который использует веб-службы Active Directory в контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="8b88e-179">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="8b88e-180">Поддержку веб-служб Active Directory выполняют контроллеры домена под управлением Windows Server 2008 R2 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="8b88e-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="8b88e-181">Он поддерживается только **модулем MSOnline PowerShell версии 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-181">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="8b88e-182">Чтобы скачать этот модуль, используйте эту [ссылку](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="8b88e-182">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="8b88e-183">Если вы используете контроллер домена под управлением Windows Server 2008 или более ранних версий, для создания точки подключения службы используйте приведенный ниже скрипт.</span><span class="sxs-lookup"><span data-stu-id="8b88e-183">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="8b88e-184">В конфигурации с несколькими лесами следует использовать следующий сценарий, чтобы создать точку подключения службы в каждом лесу, где существуют компьютеры.</span><span class="sxs-lookup"><span data-stu-id="8b88e-184">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="8b88e-185">Шаг 2. Настройка выдачи утверждений</span><span class="sxs-lookup"><span data-stu-id="8b88e-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="8b88e-186">В федеративной конфигурации Azure AD устройства проходят проверку подлинности в Azure AD, используя службы федерации Active Directory или локальную службу федерации стороннего поставщика.</span><span class="sxs-lookup"><span data-stu-id="8b88e-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="8b88e-187">При проверке подлинности устройства получают маркер доступа для регистрации в службе регистрации устройств Azure Active Directory (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="8b88e-187">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="8b88e-188">Текущие устройства Windows с помощью встроенной проверки подлинности Windows проходят проверку подлинности в активной конечной точке WS-Trust (версии 1.3 или 2005), размещенной в локальной службе федерации.</span><span class="sxs-lookup"><span data-stu-id="8b88e-188">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="8b88e-189">При использовании AD необходимо включить **adfs/services/trust/13/windowstransport** или **adfs/services/trust/2005/windowstransport**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="8b88e-190">При использовании прокси-службы проверки подлинности через Интернет также убедитесь, что эта конечная точка публикуется через прокси-службу.</span><span class="sxs-lookup"><span data-stu-id="8b88e-190">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="8b88e-191">В разделе **Служба > Конечные точки** вы можете увидеть, какие конечные точки активированы в консоли управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="8b88e-191">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="8b88e-192">Если вы не используете AD FS в качестве локальной службы федерации, обратитесь к своему поставщику за инструкциями и убедитесь, что система поддерживает конечные точки WS-Trust 1.3 или 2005 и что эти конечные точки публикуются с использованием файла обмена метаданными (MEX-файла).</span><span class="sxs-lookup"><span data-stu-id="8b88e-192">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="8b88e-193">Чтобы регистрация устройства прошла успешно, в полученном с помощью DRS Azure маркере должны существовать следующие утверждения.</span><span class="sxs-lookup"><span data-stu-id="8b88e-193">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="8b88e-194">Azure DRS создаст в Azure AD объект устройства, который содержит часть этой информации. Azure AD Connect на ее основе сопоставит новый объект устройства с локальной учетной записью компьютера.</span><span class="sxs-lookup"><span data-stu-id="8b88e-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="8b88e-195">Если у вас есть несколько подтвержденных доменных имен, для компьютеров нужно предоставить следующее утверждение:</span><span class="sxs-lookup"><span data-stu-id="8b88e-195">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="8b88e-196">Если вы уже используете утверждение ImmutableID (например, в качестве альтернативного идентификатора для входа), предоставьте еще одно утверждение для компьютеров:</span><span class="sxs-lookup"><span data-stu-id="8b88e-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="8b88e-197">В следующих разделах вы найдете следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="8b88e-197">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="8b88e-198">какие значения должны входить в каждое утверждение;</span><span class="sxs-lookup"><span data-stu-id="8b88e-198">The values each claim should have</span></span>
- <span data-ttu-id="8b88e-199">как выглядит определение в AD FS.</span><span class="sxs-lookup"><span data-stu-id="8b88e-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="8b88e-200">Определение помогает проверить, существуют ли нужные значения, или их необходимо создать.</span><span class="sxs-lookup"><span data-stu-id="8b88e-200">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="8b88e-201">Если вы не используете AD FS в качестве локального сервера федерации, следуйте инструкциям поставщика, чтобы создать соответствующую конфигурацию для выдачи этих утверждений.</span><span class="sxs-lookup"><span data-stu-id="8b88e-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="8b88e-202">Выдача утверждений для типа учетной записи</span><span class="sxs-lookup"><span data-stu-id="8b88e-202">Issue account type claim</span></span>

<span data-ttu-id="8b88e-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**. Это утверждение должно содержать значение **DJ**, которое идентифицирует устройство как присоединенный к домену компьютер.</span><span class="sxs-lookup"><span data-stu-id="8b88e-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="8b88e-204">В AD FS вы можете добавить правила преобразования выдачи, например такие:</span><span class="sxs-lookup"><span data-stu-id="8b88e-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="8b88e-205">Выдача идентификатора objectGUID для локальной учетной записи компьютера</span><span class="sxs-lookup"><span data-stu-id="8b88e-205">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="8b88e-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**. Это утверждение должно содержать значение **objectGUID** для учетной записи локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="8b88e-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="8b88e-207">В AD FS вы можете добавить правила преобразования выдачи, например такие:</span><span class="sxs-lookup"><span data-stu-id="8b88e-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="8b88e-208">Выдача идентификатора objectSID для локальной учетной записи компьютера</span><span class="sxs-lookup"><span data-stu-id="8b88e-208">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="8b88e-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**. Это утверждение должно содержать значение **objectSID** для учетной записи локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="8b88e-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="8b88e-210">В AD FS вы можете добавить правила преобразования выдачи, например такие:</span><span class="sxs-lookup"><span data-stu-id="8b88e-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="8b88e-211">Выдача issuerID для компьютера при наличии нескольких проверенных доменных имен в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b88e-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="8b88e-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**. Это утверждение должно содержать универсальный идентификатор ресурса (URI) для любого проверенного доменного имени, которое подключается с использованием локальной службы федерации (AD FS или стороннего поставщика), выдающей маркер.</span><span class="sxs-lookup"><span data-stu-id="8b88e-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="8b88e-213">В AD FS вы можете добавить правила преобразования выдачи, похожие на представленные ниже, именно в таком порядке после указанных выше правил.</span><span class="sxs-lookup"><span data-stu-id="8b88e-213">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="8b88e-214">Обратите внимание, что для явной выдачи правил пользователям необходимо одно правило.</span><span class="sxs-lookup"><span data-stu-id="8b88e-214">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="8b88e-215">В указанных ниже правилах добавлено первое правило, различающее пользователей и компьютеры при проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="8b88e-215">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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


<span data-ttu-id="8b88e-216">В приведенном выше утверждении</span><span class="sxs-lookup"><span data-stu-id="8b88e-216">In the claim above,</span></span>

- <span data-ttu-id="8b88e-217">`$<domain>` — URL-адрес службы AD FS,</span><span class="sxs-lookup"><span data-stu-id="8b88e-217">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="8b88e-218">`<verified-domain-name>` — заполнитель, который необходимо заменить одним из проверенных доменных имен в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b88e-218">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="8b88e-219">Дополнительные сведения о проверенных доменных именах см. в статье [Добавление имени личного домена в Azure Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="8b88e-219">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="8b88e-220">Чтобы получить список проверенных доменов компании, можно использовать командлет [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="8b88e-220">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="8b88e-222">Выдача ImmutableID для компьютера, если он уже существует для пользователей (например, в качестве альтернативного имени для входа)</span><span class="sxs-lookup"><span data-stu-id="8b88e-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="8b88e-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**. Это утверждение должно содержать допустимое значение для компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8b88e-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="8b88e-224">В AD FS можно создать такие правила преобразования выдачи:</span><span class="sxs-lookup"><span data-stu-id="8b88e-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="8b88e-225">Вспомогательный скрипт для создания правила преобразования выдачи AD FS</span><span class="sxs-lookup"><span data-stu-id="8b88e-225">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="8b88e-226">Следующий скрипт поможет вам создавать описанные выше правила преобразования выдачи.</span><span class="sxs-lookup"><span data-stu-id="8b88e-226">The following script helps you with the creation of the issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="8b88e-227">Примечания</span><span class="sxs-lookup"><span data-stu-id="8b88e-227">Remarks</span></span> 

- <span data-ttu-id="8b88e-228">Этот скрипт добавляет правила к существующим правилам.</span><span class="sxs-lookup"><span data-stu-id="8b88e-228">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="8b88e-229">Не выполняйте этот скрипт дважды, иначе набор правил будет также добавлен дважды.</span><span class="sxs-lookup"><span data-stu-id="8b88e-229">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="8b88e-230">Перед повторным запуском скрипта убедитесь, что для этих утверждений не существует установленных правил (при соответствующих условиях).</span><span class="sxs-lookup"><span data-stu-id="8b88e-230">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="8b88e-231">Если у вас есть несколько проверенных доменных имен (это можно проверить на портале Azure AD или с помощью командлета Get-MsolDomains), в скрипте для переменной **$multipleVerifiedDomainNames** задайте значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-231">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="8b88e-232">Также не забудьте удалить все существующие утверждения issuerid, которые могли создаваться в Azure AD Connect или другими средствами.</span><span class="sxs-lookup"><span data-stu-id="8b88e-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="8b88e-233">Вот пример для этого правила:</span><span class="sxs-lookup"><span data-stu-id="8b88e-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="8b88e-234">Если утверждение **ImmutableID** для учетных записей пользователей уже выдано, задайте для **$immutableIDAlreadyIssuedforUsers** в сценарии значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-234">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="8b88e-235">Шаг 3. Устройства Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="8b88e-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="8b88e-236">Если некоторые из присоединенных к домену устройств являются устройствами Windows нижнего уровня, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8b88e-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="8b88e-237">Настройте в Azure AD политику, разрешающую пользователям регистрировать устройства.</span><span class="sxs-lookup"><span data-stu-id="8b88e-237">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="8b88e-238">Настройте локальную службу федерации, чтобы она выдавала утверждения **встроенной проверки подлинности Windows (IWA)**, необходимые для регистрации устройств.</span><span class="sxs-lookup"><span data-stu-id="8b88e-238">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="8b88e-239">В локальные зоны интрасети добавьте конечную точку проверки подлинности устройств в Azure AD, чтобы избежать запросов сертификатов при проверке подлинности устройств.</span><span class="sxs-lookup"><span data-stu-id="8b88e-239">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="8b88e-240">Настройка политики регистрации устройств в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b88e-240">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="8b88e-241">Чтобы поддерживать регистрацию устройств Windows нижнего уровня, необходимо установить параметр, разрешающий пользователям регистрировать устройства в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b88e-241">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="8b88e-242">Эти настройки можно найти на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="8b88e-242">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="8b88e-243">Следующая политика должна иметь значение **Все**: **Пользователи могут регистрировать устройства в Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-243">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Регистрация устройств](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="8b88e-245">Настройка локальной службы федерации</span><span class="sxs-lookup"><span data-stu-id="8b88e-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="8b88e-246">Локальная служба федерации должна поддерживать выдачу утверждений **authenticationmehod** и **wiaormultiauthn** при получении запросов на проверку подлинности к проверяющей стороне Azure AD, содержащих параметр resouce_params с закодированным значением, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="8b88e-246">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="8b88e-247">При поступлении такого запроса локальная служба федерации должна выполнить проверку подлинности пользователя, используя встроенную проверку подлинности Windows. При успешной проверке подлинности она должна выдать следующие два утверждения:</span><span class="sxs-lookup"><span data-stu-id="8b88e-247">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="8b88e-248">В AD FS следует добавить правило преобразования выдачи, пропускающее метод проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8b88e-248">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="8b88e-249">**Чтобы добавить это правило, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="8b88e-249">**To add this rule:**</span></span>

1. <span data-ttu-id="8b88e-250">В консоли управления AD FS откройте `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="8b88e-250">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="8b88e-251">Щелкните правой кнопкой мыши объект отношений доверия с проверяющей стороной платформы удостоверений Microsoft Office 365 и выберите **Edit Claim Rules** (Изменить правила для утверждений).</span><span class="sxs-lookup"><span data-stu-id="8b88e-251">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="8b88e-252">На вкладке **Правила преобразования выдачи** выберите **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-252">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="8b88e-253">Из списка шаблонов **Claim rule** (Правило для утверждений) выберите **Отправка утверждений с помощью настраиваемого правила**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-253">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="8b88e-254">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-254">Select **Next**.</span></span>
6. <span data-ttu-id="8b88e-255">В поле **Claim rule name** (Имя правила для утверждений метода проверки подлинности) введите **Auth Method Claim Rule** (Правило для утверждений метода проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="8b88e-255">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="8b88e-256">В поле **Claim rule** (Правило утверждения) введите такое правило:</span><span class="sxs-lookup"><span data-stu-id="8b88e-256">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="8b88e-257">На сервере федерации введите указанную ниже команду PowerShell, заменив в ней **\<RPObjectName\>** именем объекта проверяющей стороны, которое соответствует объекту доверия проверяющей стороны Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b88e-257">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="8b88e-258">Как правило, этот объект называется **платформой удостоверений Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="8b88e-259">Добавление конечной точки для проверки подлинности устройств Azure AD в локальные зоны интрасети</span><span class="sxs-lookup"><span data-stu-id="8b88e-259">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="8b88e-260">Чтобы избежать запросов сертификатов при проверке подлинности в Azure AD пользователей с зарегистрированных устройств, можно отправить политику на присоединенные к домену устройства, добавив следующий URL-адрес в зону локальной интрасети в Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="8b88e-260">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="8b88e-261">Шаг 4. Контроль развертывания</span><span class="sxs-lookup"><span data-stu-id="8b88e-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="8b88e-262">Когда вы выполните эти обязательные шаги, все будет готово для автоматической регистрации в Azure AD устройств, присоединенных к домену.</span><span class="sxs-lookup"><span data-stu-id="8b88e-262">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span></span> <span data-ttu-id="8b88e-263">Все присоединенные к домену устройства под управлением юбилейного обновления Windows 10 и Windows Server 2016 будут выполнять автоматическую регистрацию в Azure AD при перезагрузке устройства и при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="8b88e-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="8b88e-264">Новые устройства зарегистрируются в Azure AD, когда завершится перезагрузка после присоединения к домену.</span><span class="sxs-lookup"><span data-stu-id="8b88e-264">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

<span data-ttu-id="8b88e-265">Устройства, которые были ранее присоединены к рабочей области Azure AD (например, для Intune), перейдут в состояние *Присоединено к домену и Зарегистрировано в AAD*. Однако из-за обычного потока действий домена и пользователя, чтобы завершить этот процесс на всех устройствах понадобится некоторое время.</span><span class="sxs-lookup"><span data-stu-id="8b88e-265">Devices that were previously workplace-joined to Azure AD (for example for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="8b88e-266">Примечания</span><span class="sxs-lookup"><span data-stu-id="8b88e-266">Remarks</span></span>

- <span data-ttu-id="8b88e-267">Для управления развертыванием автоматической регистрации присоединенных к домену компьютеров Windows 10 и Windows Server 2016 можно использовать объект групповой политики.</span><span class="sxs-lookup"><span data-stu-id="8b88e-267">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="8b88e-268">Устройства с обновлением Windows 10 от ноября 2015 г. автоматически регистрируются в Azure AD **только** в том случае, если задан объект групповой политики развертывания.</span><span class="sxs-lookup"><span data-stu-id="8b88e-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="8b88e-269">Чтобы развернуть автоматическую регистрацию компьютеров Windows нижнего уровня, вы можете развернуть на выбранных компьютерах [пакет установщика Windows](#windows-installer-packages-for-non-windows-10-computers).</span><span class="sxs-lookup"><span data-stu-id="8b88e-269">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="8b88e-270">Когда вы отправляете объект групповой политики на присоединенные к домену устройства Windows 8.1, предпринимается попытка регистрации. Но мы рекомендуем использовать для регистрации всех устройств Windows нижнего уровня [пакет установщика Windows](#windows-installer-packages-for-non-windows-10-computers).</span><span class="sxs-lookup"><span data-stu-id="8b88e-270">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="8b88e-271">Создание объекта групповой политики</span><span class="sxs-lookup"><span data-stu-id="8b88e-271">Create a Group Policy object</span></span> 

<span data-ttu-id="8b88e-272">Чтобы управлять развертыванием автоматической регистрации текущих компьютеров Windows, следует развернуть на компьютерах, которые нужно зарегистрировать, объект групповой политики **Зарегистрировать подключенные к домену компьютеры в качестве устройств**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-272">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="8b88e-273">Например, можно развернуть политику в подразделении или группе безопасности.</span><span class="sxs-lookup"><span data-stu-id="8b88e-273">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="8b88e-274">**Чтобы задать политику, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="8b88e-274">**To set the policy:**</span></span>

1. <span data-ttu-id="8b88e-275">Откройте **диспетчер сервера** и перейдите к разделу `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="8b88e-275">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="8b88e-276">Перейдите к узлу домена, на котором нужно активировать автоматическую регистрацию текущих компьютеров Windows.</span><span class="sxs-lookup"><span data-stu-id="8b88e-276">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="8b88e-277">Щелкните правой кнопкой мыши **Объекты групповой политики**, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="8b88e-278">Введите имя объекта групповой политики.</span><span class="sxs-lookup"><span data-stu-id="8b88e-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="8b88e-279">Например, *автоматическая регистрация в Azure AD*.</span><span class="sxs-lookup"><span data-stu-id="8b88e-279">For example, *Automatic Registration to Azure AD*.</span></span> <span data-ttu-id="8b88e-280">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-280">Select **OK**.</span></span>
5. <span data-ttu-id="8b88e-281">Щелкните новый объект групповой политики правой кнопкой мыши, а затем выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="8b88e-282">Выберите **Конфигурация компьютера** > **Политики** > **Административные шаблоны** > **Компоненты Windows** > **Регистрация устройств**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-282">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="8b88e-283">Щелкните правой кнопкой мыши пункт **Зарегистрировать подключенные к домену компьютеры в качестве устройств** и выберите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8b88e-284">В более ранних версиях консоли управления групповыми политиками этот шаблон групповой политики назывался по-другому.</span><span class="sxs-lookup"><span data-stu-id="8b88e-284">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="8b88e-285">Если вы используете более раннюю версию консоли, перейдите к `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="8b88e-285">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="8b88e-286">Выберите параметр **Включено**, а затем — **Применить**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="8b88e-287">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-287">Select **OK**.</span></span>
9. <span data-ttu-id="8b88e-288">Свяжите объект групповой политики с выбранным расположением.</span><span class="sxs-lookup"><span data-stu-id="8b88e-288">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="8b88e-289">Например, его можно связать с определенным подразделением.</span><span class="sxs-lookup"><span data-stu-id="8b88e-289">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="8b88e-290">Его также можно связать с определенной группой безопасности компьютеров, которые регистрируются в Azure AD автоматически.</span><span class="sxs-lookup"><span data-stu-id="8b88e-290">You also could link it to a specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="8b88e-291">Чтобы задать эту политику для всех присоединенных к домену компьютеров Windows 10 и Windows Server 2016 в организации, свяжите объект групповой политики с доменом.</span><span class="sxs-lookup"><span data-stu-id="8b88e-291">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="8b88e-292">Пакеты установщика Windows для компьютеров, не работающих на базе Windows 10</span><span class="sxs-lookup"><span data-stu-id="8b88e-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="8b88e-293">Чтобы регистрировать в федеративной среде присоединенные к домену компьютеры Windows нижнего уровня, скачайте из Центра загрузки Майкрософт и установите пакет установщика Windows (MSI-файл), опубликованный на странице [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) (Microsoft Workplace Join для компьютеров под управлением ОС, отличной от Windows 10).</span><span class="sxs-lookup"><span data-stu-id="8b88e-293">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="8b88e-294">Для развертывания пакета используйте систему распространения программного обеспечения, например System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="8b88e-294">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="8b88e-295">Пакет поддерживает параметры стандартной автоматической установки с использованием параметра *quiet*.</span><span class="sxs-lookup"><span data-stu-id="8b88e-295">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="8b88e-296">В System Center Configuration Manager доступны дополнительные преимущества предыдущих версий, такие как возможность отслеживать ход выполнения регистрации.</span><span class="sxs-lookup"><span data-stu-id="8b88e-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="8b88e-297">Дополнительные сведения см. на странице [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="8b88e-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="8b88e-298">Установщик создает в системе запланированную задачу, которая выполняется в контексте пользователя.</span><span class="sxs-lookup"><span data-stu-id="8b88e-298">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="8b88e-299">Задача запускается в момент входа пользователя в систему Windows.</span><span class="sxs-lookup"><span data-stu-id="8b88e-299">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="8b88e-300">Эта задача автоматически регистрирует устройство в Azure AD, используя учетные данные пользователя, после проверки подлинности с использованием встроенной проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="8b88e-300">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="8b88e-301">Чтобы просмотреть запланированные задачи, выберите на устройстве **Microsoft** > **Присоединение к рабочей области** и перейдите к библиотеке планировщика задач.</span><span class="sxs-lookup"><span data-stu-id="8b88e-301">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="8b88e-302">Шаг 5. Проверка зарегистрированных устройств</span><span class="sxs-lookup"><span data-stu-id="8b88e-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="8b88e-303">Список успешно зарегистрированных корпоративных устройств вашей организации вы можете получить с помощью командлета [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice), входящего в [модуль PowerShell для Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="8b88e-303">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="8b88e-304">Выходные данные этого командлета содержат список устройств, зарегистрированных в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b88e-304">The output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="8b88e-305">Чтобы получить полный список устройств, используйте параметр **-All**. Устройства затем можно отфильтровать по свойству **deviceTrustType**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-305">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="8b88e-306">У присоединенных к домену устройств оно имеет значение **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="8b88e-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b88e-307">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b88e-307">Next steps</span></span>

* <span data-ttu-id="8b88e-308">[Azure Active Directory automatic device registration FAQ](active-directory-device-registration-faq.md) (Часто задаваемые вопросы об автоматической регистрации устройств)</span><span class="sxs-lookup"><span data-stu-id="8b88e-308">[Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span>
* <span data-ttu-id="8b88e-309">[Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md) (Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров под управлением Windows 10 и Windows Server 2016)</span><span class="sxs-lookup"><span data-stu-id="8b88e-309">[Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)</span></span>
* <span data-ttu-id="8b88e-310">[Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md) (Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров под управлением ОС, отличных от Windows 10)</span><span class="sxs-lookup"><span data-stu-id="8b88e-310">[Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10](active-directory-device-registration-troubleshoot-windows-legacy.md)</span></span>
* [<span data-ttu-id="8b88e-311">Условный доступ в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b88e-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
