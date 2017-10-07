---
title: "aaaConfigure PowerShell для использования со стеком Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure PowerShell для Azure стека."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: sngun
ms.openlocfilehash: bc40869abe453cef4854daaf11605efd94a66c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-powershell-for-use-with-azure-stack"></a><span data-ttu-id="d1f28-103">Настройка PowerShell для использования с стек Azure</span><span class="sxs-lookup"><span data-stu-id="d1f28-103">Configure PowerShell for use with Azure Stack</span></span> 

<span data-ttu-id="d1f28-104">Данная статья содержит hello действия требуется tooconnect tooan пакет средств разработки Azure стека экземпляра с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1f28-104">This article describes hello steps required tooconnect tooan Azure Stack Development Kit instance by using PowerShell.</span></span> <span data-ttu-id="d1f28-105">После подключения можно получить доступ к порталу hello и развертывать ресурсы с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1f28-105">After you connect, you can access hello portal and deploy resources through PowerShell.</span></span> <span data-ttu-id="d1f28-106">Можно использовать hello действия, описанные в этой статье из пакета средств разработки hello или из внешнего клиента на основе Windows, при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="d1f28-106">You can use hello steps described in this article either from hello development kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="d1f28-107">В этой статье содержатся подробные инструкции по tooconfigure PowerShell для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="d1f28-107">This article has detailed instructions tooconfigure PowerShell for Azure Stack.</span></span> <span data-ttu-id="d1f28-108">Тем не менее, если tooquickly установку и настройте PowerShell, можно использовать сценарий hello в hello [приступить к работе с PowerShell](azure-stack-powershell-configure-quickstart.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="d1f28-108">However, if you want tooquickly install and configure PowerShell, you can use hello script provided in hello [Get up and running with PowerShell](azure-stack-powershell-configure-quickstart.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d1f28-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d1f28-109">Prerequisites</span></span>
* <span data-ttu-id="d1f28-110">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="d1f28-110">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="d1f28-111">Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="d1f28-111">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

## <a name="import-hello-connect-powershell-module"></a><span data-ttu-id="d1f28-112">Модуль Connect PowerShell hello импорта</span><span class="sxs-lookup"><span data-stu-id="d1f28-112">Import hello Connect PowerShell module</span></span>

<span data-ttu-id="d1f28-113">После загрузки hello необходимые средства, перейдите в папку toohello загрузить и импортировать hello **Connect** модуля PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1f28-113">After you download hello required tools, navigate toohello downloaded folder and import hello **Connect** PowerShell module.</span></span> <span data-ttu-id="d1f28-114">tooimport hello модуля Connect, запустите следующую команду в сеансе PowerShell с повышенными привилегиями hello:</span><span class="sxs-lookup"><span data-stu-id="d1f28-114">tooimport hello Connect module, run hello following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-hello-powershell-environment"></a><span data-ttu-id="d1f28-115">Настройка среды PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="d1f28-115">Configure hello PowerShell environment</span></span>

<span data-ttu-id="d1f28-116">tooconfigure среды стека Azure hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d1f28-116">tooconfigure your Azure Stack environment, do hello following:</span></span>

1. <span data-ttu-id="d1f28-117">Зарегистрируйте AzureRM среду, которая обращается экземпляр стек Azure с помощью одного из следующих командлетов hello:</span><span class="sxs-lookup"><span data-stu-id="d1f28-117">Register an AzureRM environment that targets your Azure Stack instance by using one of hello following cmdlets:</span></span>

   * <span data-ttu-id="d1f28-118">**Облачной среде администрирования**</span><span class="sxs-lookup"><span data-stu-id="d1f28-118">**Cloud administrative environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackAdmin" `
         -ArmEndpoint "https://adminmanagement.local.azurestack.external"
       ```

   * <span data-ttu-id="d1f28-119">**Среды пользователя**</span><span class="sxs-lookup"><span data-stu-id="d1f28-119">**User environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackUser" `
         -ArmEndpoint "https://management.local.azurestack.external" 
       ```
   
   <span data-ttu-id="d1f28-120">После зарегистрировались среды AzureRM hello, можно использовать все командлеты AzureRM hello в вашей среде Azure стека.</span><span class="sxs-lookup"><span data-stu-id="d1f28-120">After you've registered hello AzureRM environment, you can use all hello AzureRM cmdlets in your Azure Stack environment.</span></span> <span data-ttu-id="d1f28-121">выходные данные Hello Предыдущий командлет hello показан следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="d1f28-121">hello output of hello previous cmdlet is shown in hello following screenshot:</span></span>

   ![Получение сведений о среде](media/azure-stack-powershell-configure/getenvdetails.png)

2. <span data-ttu-id="d1f28-123">Установите значение hello GraphEndpointResourceId с помощью одного из следующих командлетов hello:</span><span class="sxs-lookup"><span data-stu-id="d1f28-123">Set hello GraphEndpointResourceId value by using one of hello following cmdlets:</span></span>
   
   * <span data-ttu-id="d1f28-124">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="d1f28-124">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="d1f28-125">Для hello **облачной среде администрирования**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-125">For hello **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * <span data-ttu-id="d1f28-126">Для hello **среды пользователя**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-126">For hello **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * <span data-ttu-id="d1f28-127">**Службы федерации Active Directory**</span><span class="sxs-lookup"><span data-stu-id="d1f28-127">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="d1f28-128">Для hello **облачной среде администрирования**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-128">For hello **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * <span data-ttu-id="d1f28-129">Для hello **среды пользователя**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-129">For hello **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. <span data-ttu-id="d1f28-130">Получает значение идентификатора GUID hello hello клиента Active Directory, используемые toodeploy стека Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f28-130">Get hello GUID value of hello Active Directory tenant that is used toodeploy Azure Stack.</span></span> <span data-ttu-id="d1f28-131">Если среду стека Azure развертывается с помощью:</span><span class="sxs-lookup"><span data-stu-id="d1f28-131">If your Azure Stack environment is deployed by using:</span></span>  

   * <span data-ttu-id="d1f28-132">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="d1f28-132">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="d1f28-133">tooaccess hello **облачной среде администрирования**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-133">tooaccess hello **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="d1f28-134">tooaccess hello **среды пользователя**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-134">tooaccess hello **user environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * <span data-ttu-id="d1f28-135">**Службы федерации Active Directory**</span><span class="sxs-lookup"><span data-stu-id="d1f28-135">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="d1f28-136">tooaccess hello **облачной среде администрирования**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-136">tooaccess hello **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="d1f28-137">tooaccess hello **среды пользователя**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-137">tooaccess hello **user environment**, use:</span></span>
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-tooazure-stack"></a><span data-ttu-id="d1f28-138">Войдите в tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="d1f28-138">Sign in tooAzure Stack</span></span>

<span data-ttu-id="d1f28-139">Войдите в toohello среду стека Azure с помощью одного из следующих двух командлетов hello:</span><span class="sxs-lookup"><span data-stu-id="d1f28-139">Sign in toohello Azure Stack environment by using one of hello following two cmdlets:</span></span>

   * <span data-ttu-id="d1f28-140">toosign в toohello **административный портал**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-140">toosign in toohello **administrative portal**, use:</span></span>
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * <span data-ttu-id="d1f28-141">toosign в toohello **пользовательского портала**, используйте:</span><span class="sxs-lookup"><span data-stu-id="d1f28-141">toosign in toohello **user portal**, use:</span></span>

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a><span data-ttu-id="d1f28-142">Регистрация поставщиков ресурсов</span><span class="sxs-lookup"><span data-stu-id="d1f28-142">Register resource providers</span></span>

<span data-ttu-id="d1f28-143">После входа в toohello портал администратора или пользователя, можно выполнять операции с hello зарегистрированных поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d1f28-143">After you sign in toohello administrator or user portal, you can issue operations against hello registered resource providers.</span></span> <span data-ttu-id="d1f28-144">По умолчанию все поставщики ресурсов фундаментальные hello регистрируются в hello подписки поставщика по умолчанию (администратор облака hello подписка).</span><span class="sxs-lookup"><span data-stu-id="d1f28-144">By default, all hello foundational resource providers are registered in hello Default Provider Subscription (hello cloud administrator's subscription).</span></span>

<span data-ttu-id="d1f28-145">При работе с только что созданного пользователя подписки, при которой не содержит все ресурсы, развертываемые через портал hello, автоматически не зарегистрированы hello поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d1f28-145">When you operate on a newly created user subscription, which doesn’t have any resources deployed through hello portal, hello resource providers aren't automatically registered.</span></span> <span data-ttu-id="d1f28-146">Следует явно регистрировать hello поставщиков ресурсов с помощью hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="d1f28-146">You should explicitly register hello resource providers by using hello following script:</span></span>

```powershell

foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```


## <a name="next-steps"></a><span data-ttu-id="d1f28-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d1f28-147">Next steps</span></span>
* [<span data-ttu-id="d1f28-148">Разработка шаблонов для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d1f28-148">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="d1f28-149">Развертывание шаблонов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1f28-149">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
