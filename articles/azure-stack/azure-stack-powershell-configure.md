---
title: "Настройка для использования со стеком Azure PowerShell | Документы Microsoft"
description: "Подробные сведения о настройке PowerShell для Azure стека."
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
ms.openlocfilehash: 3c6fc6af0588ae2e796d50f2d7bfdafaea81e2a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="configure-powershell-for-use-with-azure-stack"></a><span data-ttu-id="ac295-103">Настройка PowerShell для использования с стек Azure</span><span class="sxs-lookup"><span data-stu-id="ac295-103">Configure PowerShell for use with Azure Stack</span></span> 

<span data-ttu-id="ac295-104">В этой статье описаны шаги, необходимые для подключения к экземпляру пакет средств разработки Azure стека с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac295-104">This article describes the steps required to connect to an Azure Stack Development Kit instance by using PowerShell.</span></span> <span data-ttu-id="ac295-105">После подключения вы доступ к порталу и развертывать ресурсы с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac295-105">After you connect, you can access the portal and deploy resources through PowerShell.</span></span> <span data-ttu-id="ac295-106">Можно использовать действия, описанные в этой статье из пакета средств разработки, либо от внешнего клиента на основе Windows при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="ac295-106">You can use the steps described in this article either from the development kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="ac295-107">В этой статье содержатся подробные инструкции по настройке PowerShell для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ac295-107">This article has detailed instructions to configure PowerShell for Azure Stack.</span></span> <span data-ttu-id="ac295-108">Тем не менее, если вы хотите быстро установить и настроить PowerShell, можно использовать сценарий, приведенный в [приступить к работе с PowerShell](azure-stack-powershell-configure-quickstart.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="ac295-108">However, if you want to quickly install and configure PowerShell, you can use the script provided in the [Get up and running with PowerShell](azure-stack-powershell-configure-quickstart.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ac295-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ac295-109">Prerequisites</span></span>
* <span data-ttu-id="ac295-110">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="ac295-110">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="ac295-111">Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="ac295-111">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

## <a name="import-the-connect-powershell-module"></a><span data-ttu-id="ac295-112">Импортируйте модуль PowerShell для подключения</span><span class="sxs-lookup"><span data-stu-id="ac295-112">Import the Connect PowerShell module</span></span>

<span data-ttu-id="ac295-113">После загрузки необходимых средств, перейдите в папку загруженные и импортировать **Connect** модуля PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac295-113">After you download the required tools, navigate to the downloaded folder and import the **Connect** PowerShell module.</span></span> <span data-ttu-id="ac295-114">Чтобы импортировать модуль Connect, выполните следующую команду в сеансе PowerShell с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="ac295-114">To import the Connect module, run the following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-the-powershell-environment"></a><span data-ttu-id="ac295-115">Настройка среды PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac295-115">Configure the PowerShell environment</span></span>

<span data-ttu-id="ac295-116">Чтобы настроить среду стека Azure, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="ac295-116">To configure your Azure Stack environment, do the following:</span></span>

1. <span data-ttu-id="ac295-117">Зарегистрируйте AzureRM среду, которая обращается экземпляр стек Azure с помощью одного из следующих командлетов:</span><span class="sxs-lookup"><span data-stu-id="ac295-117">Register an AzureRM environment that targets your Azure Stack instance by using one of the following cmdlets:</span></span>

   * <span data-ttu-id="ac295-118">**Облачной среде администрирования**</span><span class="sxs-lookup"><span data-stu-id="ac295-118">**Cloud administrative environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackAdmin" `
         -ArmEndpoint "https://adminmanagement.local.azurestack.external"
       ```

   * <span data-ttu-id="ac295-119">**Среды пользователя**</span><span class="sxs-lookup"><span data-stu-id="ac295-119">**User environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackUser" `
         -ArmEndpoint "https://management.local.azurestack.external" 
       ```
   
   <span data-ttu-id="ac295-120">После зарегистрировались AzureRM среды, можно использовать все командлеты AzureRM в вашей среде Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ac295-120">After you've registered the AzureRM environment, you can use all the AzureRM cmdlets in your Azure Stack environment.</span></span> <span data-ttu-id="ac295-121">На следующем снимке экрана показан результат предыдущего выполнения командлета:</span><span class="sxs-lookup"><span data-stu-id="ac295-121">The output of the previous cmdlet is shown in the following screenshot:</span></span>

   ![Получение сведений о среде](media/azure-stack-powershell-configure/getenvdetails.png)

2. <span data-ttu-id="ac295-123">Установите значение GraphEndpointResourceId с помощью одного из следующих командлетов:</span><span class="sxs-lookup"><span data-stu-id="ac295-123">Set the GraphEndpointResourceId value by using one of the following cmdlets:</span></span>
   
   * <span data-ttu-id="ac295-124">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="ac295-124">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="ac295-125">Для **облачной среде администрирования**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-125">For the **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * <span data-ttu-id="ac295-126">Для **среды пользователя**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-126">For the **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * <span data-ttu-id="ac295-127">**Службы федерации Active Directory**</span><span class="sxs-lookup"><span data-stu-id="ac295-127">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="ac295-128">Для **облачной среде администрирования**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-128">For the **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * <span data-ttu-id="ac295-129">Для **среды пользователя**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-129">For the **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. <span data-ttu-id="ac295-130">Получите значение идентификатора GUID для клиента Active Directory, который используется для развертывания Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ac295-130">Get the GUID value of the Active Directory tenant that is used to deploy Azure Stack.</span></span> <span data-ttu-id="ac295-131">Если среду стека Azure развертывается с помощью:</span><span class="sxs-lookup"><span data-stu-id="ac295-131">If your Azure Stack environment is deployed by using:</span></span>  

   * <span data-ttu-id="ac295-132">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="ac295-132">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="ac295-133">Чтобы получить доступ к **облачной среде администрирования**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-133">To access the **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="ac295-134">Чтобы получить доступ к **среды пользователя**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-134">To access the **user environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * <span data-ttu-id="ac295-135">**Службы федерации Active Directory**</span><span class="sxs-lookup"><span data-stu-id="ac295-135">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="ac295-136">Чтобы получить доступ к **облачной среде администрирования**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-136">To access the **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="ac295-137">Чтобы получить доступ к **среды пользователя**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-137">To access the **user environment**, use:</span></span>
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-to-azure-stack"></a><span data-ttu-id="ac295-138">Войдите в стек Azure</span><span class="sxs-lookup"><span data-stu-id="ac295-138">Sign in to Azure Stack</span></span>

<span data-ttu-id="ac295-139">Войдите в среду Azure стека с помощью одного из двух следующих командлетов:</span><span class="sxs-lookup"><span data-stu-id="ac295-139">Sign in to the Azure Stack environment by using one of the following two cmdlets:</span></span>

   * <span data-ttu-id="ac295-140">Для входа в **административный портал**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-140">To sign in to the **administrative portal**, use:</span></span>
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * <span data-ttu-id="ac295-141">Для входа в **пользовательского портала**, используйте:</span><span class="sxs-lookup"><span data-stu-id="ac295-141">To sign in to the **user portal**, use:</span></span>

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a><span data-ttu-id="ac295-142">Регистрация поставщиков ресурсов</span><span class="sxs-lookup"><span data-stu-id="ac295-142">Register resource providers</span></span>

<span data-ttu-id="ac295-143">После входа на портал администратора или пользователя, можно выполнять операции с зарегистрированных поставщиков.</span><span class="sxs-lookup"><span data-stu-id="ac295-143">After you sign in to the administrator or user portal, you can issue operations against the registered resource providers.</span></span> <span data-ttu-id="ac295-144">По умолчанию все поставщики ресурсов фундаментальные регистрируются в подписки поставщика по умолчанию (администратору облака подписка).</span><span class="sxs-lookup"><span data-stu-id="ac295-144">By default, all the foundational resource providers are registered in the Default Provider Subscription (the cloud administrator's subscription).</span></span>

<span data-ttu-id="ac295-145">При работе с только что созданного пользователя подписки, при которой не содержит все ресурсы, развертываемые на портале, автоматически не зарегистрированы поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ac295-145">When you operate on a newly created user subscription, which doesn’t have any resources deployed through the portal, the resource providers aren't automatically registered.</span></span> <span data-ttu-id="ac295-146">Следует явно регистрировать поставщики ресурсов с помощью следующего сценария:</span><span class="sxs-lookup"><span data-stu-id="ac295-146">You should explicitly register the resource providers by using the following script:</span></span>

```powershell

foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```


## <a name="next-steps"></a><span data-ttu-id="ac295-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac295-147">Next steps</span></span>
* [<span data-ttu-id="ac295-148">Разработка шаблонов для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ac295-148">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="ac295-149">Развертывание шаблонов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac295-149">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
