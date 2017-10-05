---
title: "Разрешить Многопользовательские приложения в Azure стек | Документы Microsoft"
description: "Узнайте, как для поддержки нескольких каталогов Azure Active Directory в стек Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: ed1d9d20c06ea0478a439775020fd35941b3d640
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="enable-multi-tenancy-in-azure-stack"></a><span data-ttu-id="ca92c-103">Разрешить Многопользовательские приложения в стек Azure</span><span class="sxs-lookup"><span data-stu-id="ca92c-103">Enable multi-tenancy in Azure Stack</span></span>

<span data-ttu-id="ca92c-104">Вы можете настроить стек Azure для поддержки пользователей из нескольких клиентов Azure Active Directory (Azure AD) для использования служб в Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ca92c-104">You can configure Azure Stack to support users from multiple Azure Active Directory (Azure AD) tenants to use services in Azure Stack.</span></span> <span data-ttu-id="ca92c-105">Например рассмотрим следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="ca92c-105">As an example, consider the following scenario:</span></span>

 - <span data-ttu-id="ca92c-106">Вы являетесь администратором службы из contoso.onmicrosoft.com, установленным Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ca92c-106">You are the Service Administrator of contoso.onmicrosoft.com, where Azure Stack is installed.</span></span>
 - <span data-ttu-id="ca92c-107">Мэри является администратором каталога fabrikam.onmicrosoft.com, где расположены гостевых пользователей.</span><span class="sxs-lookup"><span data-stu-id="ca92c-107">Mary is the Directory Administrator of fabrikam.onmicrosoft.com, where guest users are located.</span></span> 
 - <span data-ttu-id="ca92c-108">Мэри компании получает служб IaaS и PaaS из компании и необходимо разрешить пользователям из каталога гостя (fabrikam.onmicrosoft.com) войти и использовать ресурсы Azure стека в contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="ca92c-108">Mary's company receives IaaS and PaaS services from your company, and needs to allow users from the guest directory (fabrikam.onmicrosoft.com) to sign in and use Azure Stack resources in contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="ca92c-109">Здесь приведены шаги, в контексте этого сценария для настройки Многопользовательские приложения Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ca92c-109">This guide provides the steps required, in the context of this scenario, to configure multi-tenancy in Azure Stack.</span></span>  <span data-ttu-id="ca92c-110">В этом случае вы и Мэри необходимо выполнить действия, чтобы разрешить пользователям из компании Fabrikam, выполнить вход и использовать службы из развертывания Azure стека в компании Contoso.</span><span class="sxs-lookup"><span data-stu-id="ca92c-110">In this scenario, you and Mary must complete steps to enable users from Fabrikam to sign in and consume services from the Azure Stack deployment in Contoso.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="ca92c-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ca92c-111">Before you begin</span></span>
<span data-ttu-id="ca92c-112">Существует несколько необходимых компонентов для учета перед настройкой Многопользовательские приложения Azure стека:</span><span class="sxs-lookup"><span data-stu-id="ca92c-112">There are a few pre-requisites to account for before you configure multi-tenancy in Azure Stack:</span></span>
  
 - <span data-ttu-id="ca92c-113">Вы и Мэри необходимо координировать административные действия в каталог, который в (Contoso), устанавливается стек Azure и каталог гостя (Fabrikam).</span><span class="sxs-lookup"><span data-stu-id="ca92c-113">You and Mary must coordinate administrative steps across both the directory Azure Stack is installed in (Contoso), and the guest directory (Fabrikam).</span></span>  
 - <span data-ttu-id="ca92c-114">Убедитесь, что вы уже [установлен](azure-stack-powershell-install.md) и [настроен](azure-stack-powershell-configure-admin.md) PowerShell для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ca92c-114">Make sure you've [installed](azure-stack-powershell-install.md) and [configured](azure-stack-powershell-configure-admin.md) PowerShell for Azure Stack.</span></span>
 - <span data-ttu-id="ca92c-115">[Загрузите средства Azure стека](azure-stack-powershell-download.md)и импортируйте модули Connect и удостоверений:</span><span class="sxs-lookup"><span data-stu-id="ca92c-115">[Download the Azure Stack Tools](azure-stack-powershell-download.md), and import the Connect and Identity modules:</span></span>

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - <span data-ttu-id="ca92c-116">Потребуется Mary [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) доступ к Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ca92c-116">Mary will require [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) access to Azure Stack.</span></span> 

## <a name="configure-azure-stack-directory"></a><span data-ttu-id="ca92c-117">Настроить каталог стек Azure</span><span class="sxs-lookup"><span data-stu-id="ca92c-117">Configure Azure Stack directory</span></span>
<span data-ttu-id="ca92c-118">В этом разделе Настройте стек Azure позволяет войти в систему от клиентов directory Fabrikam Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca92c-118">In this section, you configure Azure Stack to allow sign-ins from Fabrikam Azure AD directory tenants.</span></span>

### <a name="onboard-guest-directory-tenant"></a><span data-ttu-id="ca92c-119">Встроенный гостевой каталог клиента</span><span class="sxs-lookup"><span data-stu-id="ca92c-119">Onboard guest directory tenant</span></span>
<span data-ttu-id="ca92c-120">Далее, встроенный клиент каталога гостя (Fabrikam) в стек Azure.</span><span class="sxs-lookup"><span data-stu-id="ca92c-120">Next, onboard the Guest Directory Tenant (Fabrikam) to Azure Stack.</span></span>  <span data-ttu-id="ca92c-121">Этот шаг позволяет настроить Azure Resource Manager для принятия пользователи и участники службы из клиента каталога гостя.</span><span class="sxs-lookup"><span data-stu-id="ca92c-121">This step configures Azure Resource Manager to accept users and service principals from the guest directory tenant.</span></span>

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace the value below with the Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a><span data-ttu-id="ca92c-122">Настройка каталога гостя</span><span class="sxs-lookup"><span data-stu-id="ca92c-122">Configure guest directory</span></span>
<span data-ttu-id="ca92c-123">После выполнения шагов в каталоге Azure стека, Мэри необходимо дать согласие на доступ к каталогу гостевой стек Azure и Azure стеком регистров с каталогом гостевой.</span><span class="sxs-lookup"><span data-stu-id="ca92c-123">After you complete steps in the Azure Stack directory, Mary must provide consent to Azure Stack accessing the guest directory and register Azure Stack with the guest directory.</span></span> 

### <a name="registering-azure-stack-with-the-guest-directory"></a><span data-ttu-id="ca92c-124">Регистрация в каталоге гостевой стек Azure</span><span class="sxs-lookup"><span data-stu-id="ca92c-124">Registering Azure Stack with the guest directory</span></span>
<span data-ttu-id="ca92c-125">После гостевой directory администратор предоставил разрешения для стека Azure для доступа к каталогу компании Fabrikam, их необходимо зарегистрировать Azure стека клиента каталога компании Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="ca92c-125">Once the guest directory administrator has provided consent for Azure Stack to access Fabrikam's directory, they must register Azure Stack with Fabrikam's directory tenant.</span></span>

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName ` 
 -Verbose 
````
## <a name="direct-users-to-sign-in"></a><span data-ttu-id="ca92c-126">Предоставить пользователям вход</span><span class="sxs-lookup"><span data-stu-id="ca92c-126">Direct users to sign in</span></span>
<span data-ttu-id="ca92c-127">Теперь, когда вы и Мэри шаги по встроенным Мэри каталог, Мэри могут направлять пользователей Fabrikam вход.</span><span class="sxs-lookup"><span data-stu-id="ca92c-127">Now that you and Mary have completed the steps to onboard Mary's directory, Mary can direct Fabrikam users to sign in.</span></span>  <span data-ttu-id="ca92c-128">Вход пользователей Fabrikam (то есть, пользователи с суффиксом fabrikam.onmicrosoft.com), перейдя по адресу https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="ca92c-128">Fabrikam users (that is, users with the fabrikam.onmicrosoft.com suffix) sign in by visiting https://portal.local.azurestack.external.</span></span>  

<span data-ttu-id="ca92c-129">Мария будет направлять все [внешних участников](../active-directory/active-directory-understanding-resource-access.md) в каталоге компании Fabrikam (то есть, пользователи в каталоге Fabrikam без суффикса fabrikam.onmicrosoft.com) выполнить вход с использованием https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  Если они не используют этот URL-адрес, они отправляются их каталог по умолчанию (Fabrikam) и происходит ошибка, о том, что не согласился своему администратору.</span><span class="sxs-lookup"><span data-stu-id="ca92c-129">Mary will direct any [foreign principals](../active-directory/active-directory-understanding-resource-access.md) in the Fabrikam directory (that is, users in the Fabrikam directory without the suffix of fabrikam.onmicrosoft.com) to sign in using https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  If they do not use this URL, they are sent to their default directory (Fabrikam) and receive an error that says their admin has not consented.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca92c-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca92c-130">Next Steps</span></span>

- [<span data-ttu-id="ca92c-131">Управление поставщиками делегированные</span><span class="sxs-lookup"><span data-stu-id="ca92c-131">Manage delegated providers</span></span>](azure-stack-delegated-provider.md)
- [<span data-ttu-id="ca92c-132">Основные понятия Azure стека</span><span class="sxs-lookup"><span data-stu-id="ca92c-132">Azure Stack key concepts</span></span>](azure-stack-key-features.md)
