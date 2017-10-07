---
title: "Многопользовательские приложения aaaEnable в стек Azure | Документы Microsoft"
description: "Узнайте, как toosupport нескольких каталогов Azure Active Directory в стек Azure"
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
ms.openlocfilehash: d7e404894a65f6786c42c5c27f76d46f353cb8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-multi-tenancy-in-azure-stack"></a><span data-ttu-id="85fe0-103">Разрешить Многопользовательские приложения в стек Azure</span><span class="sxs-lookup"><span data-stu-id="85fe0-103">Enable multi-tenancy in Azure Stack</span></span>

<span data-ttu-id="85fe0-104">Стек Azure toosupport пользователей из нескольких служб toouse клиентов Azure Active Directory (Azure AD) можно настроить в стек Azure.</span><span class="sxs-lookup"><span data-stu-id="85fe0-104">You can configure Azure Stack toosupport users from multiple Azure Active Directory (Azure AD) tenants toouse services in Azure Stack.</span></span> <span data-ttu-id="85fe0-105">Например рассмотрим следующие сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="85fe0-105">As an example, consider hello following scenario:</span></span>

 - <span data-ttu-id="85fe0-106">Есть hello администратора службы из contoso.onmicrosoft.com, где установлена стек Azure.</span><span class="sxs-lookup"><span data-stu-id="85fe0-106">You are hello Service Administrator of contoso.onmicrosoft.com, where Azure Stack is installed.</span></span>
 - <span data-ttu-id="85fe0-107">Мария — hello администратор каталога fabrikam.onmicrosoft.com, где расположены гостевых пользователей.</span><span class="sxs-lookup"><span data-stu-id="85fe0-107">Mary is hello Directory Administrator of fabrikam.onmicrosoft.com, where guest users are located.</span></span> 
 - <span data-ttu-id="85fe0-108">Мэри компании получает служб IaaS и PaaS из вашей организации и требуется tooallow пользователям toosign каталога (fabrikam.onmicrosoft.com) гостевой hello в и использовать ресурсы Azure стека в contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="85fe0-108">Mary's company receives IaaS and PaaS services from your company, and needs tooallow users from hello guest directory (fabrikam.onmicrosoft.com) toosign in and use Azure Stack resources in contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="85fe0-109">Это руководство предоставляет hello действия требуются в контексте hello этого сценария tooconfigure Многопользовательские приложения в Azure стека.</span><span class="sxs-lookup"><span data-stu-id="85fe0-109">This guide provides hello steps required, in hello context of this scenario, tooconfigure multi-tenancy in Azure Stack.</span></span>  <span data-ttu-id="85fe0-110">В этом сценарии вы и Мария выполните действия tooenable пользователи из компании Fabrikam toosign в и использовать службы из hello развертывания Azure стека в компании Contoso.</span><span class="sxs-lookup"><span data-stu-id="85fe0-110">In this scenario, you and Mary must complete steps tooenable users from Fabrikam toosign in and consume services from hello Azure Stack deployment in Contoso.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="85fe0-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="85fe0-111">Before you begin</span></span>
<span data-ttu-id="85fe0-112">Существует несколько tooaccount предварительных требований для перед настройкой Многопользовательские приложения Azure стека:</span><span class="sxs-lookup"><span data-stu-id="85fe0-112">There are a few pre-requisites tooaccount for before you configure multi-tenancy in Azure Stack:</span></span>
  
 - <span data-ttu-id="85fe0-113">Вы Мэри необходимо координировать административные действия между обоих стек Azure установлен в (Contoso) каталог hello и hello каталога гостя (Fabrikam).</span><span class="sxs-lookup"><span data-stu-id="85fe0-113">You and Mary must coordinate administrative steps across both hello directory Azure Stack is installed in (Contoso), and hello guest directory (Fabrikam).</span></span>  
 - <span data-ttu-id="85fe0-114">Убедитесь, что вы уже [установлен](azure-stack-powershell-install.md) и [настроен](azure-stack-powershell-configure-admin.md) PowerShell для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="85fe0-114">Make sure you've [installed](azure-stack-powershell-install.md) and [configured](azure-stack-powershell-configure-admin.md) PowerShell for Azure Stack.</span></span>
 - <span data-ttu-id="85fe0-115">[Загрузить средства стека hello Azure](azure-stack-powershell-download.md)и импортируйте модули hello Connect и удостоверений:</span><span class="sxs-lookup"><span data-stu-id="85fe0-115">[Download hello Azure Stack Tools](azure-stack-powershell-download.md), and import hello Connect and Identity modules:</span></span>

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - <span data-ttu-id="85fe0-116">Потребуется Mary [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) доступ к tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="85fe0-116">Mary will require [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) access tooAzure Stack.</span></span> 

## <a name="configure-azure-stack-directory"></a><span data-ttu-id="85fe0-117">Настроить каталог стек Azure</span><span class="sxs-lookup"><span data-stu-id="85fe0-117">Configure Azure Stack directory</span></span>
<span data-ttu-id="85fe0-118">В этом разделе Настройте стек Azure tooallow входа в систему от клиентов directory Fabrikam Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85fe0-118">In this section, you configure Azure Stack tooallow sign-ins from Fabrikam Azure AD directory tenants.</span></span>

### <a name="onboard-guest-directory-tenant"></a><span data-ttu-id="85fe0-119">Встроенный гостевой каталог клиента</span><span class="sxs-lookup"><span data-stu-id="85fe0-119">Onboard guest directory tenant</span></span>
<span data-ttu-id="85fe0-120">Далее, встроенный hello tooAzure клиента каталога гостя (Fabrikam) стека.</span><span class="sxs-lookup"><span data-stu-id="85fe0-120">Next, onboard hello Guest Directory Tenant (Fabrikam) tooAzure Stack.</span></span>  <span data-ttu-id="85fe0-121">Этот шаг позволяет настроить диспетчера ресурсов Azure tooaccept пользователи и участники службы из клиента каталога гостя hello.</span><span class="sxs-lookup"><span data-stu-id="85fe0-121">This step configures Azure Resource Manager tooaccept users and service principals from hello guest directory tenant.</span></span>

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace hello value below with hello Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a><span data-ttu-id="85fe0-122">Настройка каталога гостя</span><span class="sxs-lookup"><span data-stu-id="85fe0-122">Configure guest directory</span></span>
<span data-ttu-id="85fe0-123">После выполнения шагов в каталоге Azure стека hello, Мэри необходимо указать согласия tooAzure стека доступ к hello гостевой directory и Azure стеком регистров с каталогом гостевой hello.</span><span class="sxs-lookup"><span data-stu-id="85fe0-123">After you complete steps in hello Azure Stack directory, Mary must provide consent tooAzure Stack accessing hello guest directory and register Azure Stack with hello guest directory.</span></span> 

### <a name="registering-azure-stack-with-hello-guest-directory"></a><span data-ttu-id="85fe0-124">Регистрация стек Azure directory гостевой hello</span><span class="sxs-lookup"><span data-stu-id="85fe0-124">Registering Azure Stack with hello guest directory</span></span>
<span data-ttu-id="85fe0-125">После hello гостевой directory администратор предоставил согласие для каталога Azure стека tooaccess Fabrikam, их необходимо зарегистрировать Azure стека клиента каталога компании Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="85fe0-125">Once hello guest directory administrator has provided consent for Azure Stack tooaccess Fabrikam's directory, they must register Azure Stack with Fabrikam's directory tenant.</span></span>

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName ` 
 -Verbose 
````
## <a name="direct-users-toosign-in"></a><span data-ttu-id="85fe0-126">Предоставить пользователям toosign в</span><span class="sxs-lookup"><span data-stu-id="85fe0-126">Direct users toosign in</span></span>
<span data-ttu-id="85fe0-127">Вы и Мэри после завершения hello действия tooonboard Мэри каталога, Мэри можно направить toosign пользователей Fabrikam в.</span><span class="sxs-lookup"><span data-stu-id="85fe0-127">Now that you and Mary have completed hello steps tooonboard Mary's directory, Mary can direct Fabrikam users toosign in.</span></span>  <span data-ttu-id="85fe0-128">Fabrikam пользователей (то есть с суффиксом hello fabrikam.onmicrosoft.com), перейдя по адресу https://portal.local.azurestack.external вход.</span><span class="sxs-lookup"><span data-stu-id="85fe0-128">Fabrikam users (that is, users with hello fabrikam.onmicrosoft.com suffix) sign in by visiting https://portal.local.azurestack.external.</span></span>  

<span data-ttu-id="85fe0-129">Мария будет направлять все [внешних участников](../active-directory/active-directory-understanding-resource-access.md) в toosign каталога (то есть пользователей в каталог Fabrikam hello без суффикса hello fabrikam.onmicrosoft.com) Fabrikam hello в с помощью https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  Если они не используют этот URL-адрес, они отправляются tootheir каталог по умолчанию (Fabrikam) и происходит ошибка, о том, что не согласился своему администратору.</span><span class="sxs-lookup"><span data-stu-id="85fe0-129">Mary will direct any [foreign principals](../active-directory/active-directory-understanding-resource-access.md) in hello Fabrikam directory (that is, users in hello Fabrikam directory without hello suffix of fabrikam.onmicrosoft.com) toosign in using https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  If they do not use this URL, they are sent tootheir default directory (Fabrikam) and receive an error that says their admin has not consented.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85fe0-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="85fe0-130">Next Steps</span></span>

- [<span data-ttu-id="85fe0-131">Управление поставщиками делегированные</span><span class="sxs-lookup"><span data-stu-id="85fe0-131">Manage delegated providers</span></span>](azure-stack-delegated-provider.md)
- [<span data-ttu-id="85fe0-132">Основные понятия Azure стека</span><span class="sxs-lookup"><span data-stu-id="85fe0-132">Azure Stack key concepts</span></span>](azure-stack-key-features.md)
