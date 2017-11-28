---
title: "Регистрация стек Azure | Документы Microsoft"
description: "Azure стеком регистров с подпиской Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: f71ec571fee8e59ea9061cd619914b81a5bf701a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a><span data-ttu-id="d1a6b-103">Регистрация стек Azure с подпиской Azure</span><span class="sxs-lookup"><span data-stu-id="d1a6b-103">Register Azure Stack with your Azure Subscription</span></span>

<span data-ttu-id="d1a6b-104">Для развертываний Azure Active Directory можно зарегистрировать Azure стек Azure для загрузки элементов marketplace из Azure и настроить commerce данные отчетов обратно в корпорацию Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-104">For Azure Active Directory deployments, you can register Azure Stack with Azure to download marketplace items from Azure and to set up commerce data reporting back to Microsoft.</span></span> 

> [!NOTE]
><span data-ttu-id="d1a6b-105">Регистрация рекомендуется, так как он позволяет тестировать важные функции Azure стека, например синдикации marketplace и отчеты об использовании.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-105">Registration is recommended because it enables you to test important Azure Stack functionality, like marketplace syndication and usage reporting.</span></span> <span data-ttu-id="d1a6b-106">После регистрации Azure стека для Azure commerce отчеты об использовании.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-106">After you register Azure Stack, usage is reported to Azure commerce.</span></span> <span data-ttu-id="d1a6b-107">Его можно просматривать в подписке, которая использовалась для регистрации.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-107">You can see it under the subscription you used for registration.</span></span> <span data-ttu-id="d1a6b-108">Пользователей Azure стека пакет средств разработки, не будете платить за все они сообщают об использовании.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-108">Azure Stack Development Kit users will not be charged for any usage they report.</span></span>
>


## <a name="get-azure-subscription"></a><span data-ttu-id="d1a6b-109">Получить подписку Azure</span><span class="sxs-lookup"><span data-stu-id="d1a6b-109">Get Azure subscription</span></span>

<span data-ttu-id="d1a6b-110">Перед регистрацией стек Azure с помощью Azure, необходимо иметь:</span><span class="sxs-lookup"><span data-stu-id="d1a6b-110">Before registering Azure Stack with Azure, you must have:</span></span>

- <span data-ttu-id="d1a6b-111">Идентификатор подписки для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-111">The subscription ID for an Azure subscription.</span></span> <span data-ttu-id="d1a6b-112">Для получения идентификатора, выполните вход в Azure, нажмите кнопку **дополнительные службы** > **подписки**, щелкните подписку, которую нужно использовать, а затем в разделе **Essentials** можно найти **Идентификатор подписки**.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-112">To get the ID, sign in to Azure, click **More services** > **Subscriptions**, click the subscription you want to use, and under **Essentials** you can find the **Subscription ID**.</span></span> <span data-ttu-id="d1a6b-113">Китай, Германии и нам облака государственных подписок в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-113">China, Germany, and US government cloud subscriptions are not currently supported.</span></span>
- <span data-ttu-id="d1a6b-114">Имя пользователя и пароль учетной записи, которая является владельцем подписки (поддерживаются учетные записи MSA/2FA)</span><span class="sxs-lookup"><span data-stu-id="d1a6b-114">The username and password for an account that is an owner for the subscription (MSA/2FA accounts are supported)</span></span>
- <span data-ttu-id="d1a6b-115">Azure Active Directory для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-115">The Azure Active Directory for the Azure subscription.</span></span> <span data-ttu-id="d1a6b-116">Этот каталог можно найти в Azure, наведя на аватара в правом верхнем углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-116">You can find this directory in Azure by hovering over your avatar at the top right corner of the Azure portal.</span></span> 
- <span data-ttu-id="d1a6b-117">Регистрации поставщика ресурсов Azure стека (в разделе **Регистрация поставщика ресурсов Azure стека** ниже, в разделе Подробности)</span><span class="sxs-lookup"><span data-stu-id="d1a6b-117">Registered the Azure Stack resource provider (see the **Register Azure Stack Resource Provider** section below for details)</span></span>

<span data-ttu-id="d1a6b-118">Если нет подписки Azure, удовлетворяющее этим требованиям, вы можете [создать бесплатную учетную запись Azure здесь](https://azure.microsoft.com/en-us/free/?b=17.06).</span><span class="sxs-lookup"><span data-stu-id="d1a6b-118">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06).</span></span> <span data-ttu-id="d1a6b-119">Регистрация стек Azure влечет за собой без затрат на подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-119">Registering Azure Stack incurs no cost on your Azure subscription.</span></span>



## <a name="register-azure-stack-resource-provider-in-azure"></a><span data-ttu-id="d1a6b-120">Регистрация поставщика ресурсов Azure стека в Azure</span><span class="sxs-lookup"><span data-stu-id="d1a6b-120">Register Azure Stack resource provider in Azure</span></span>
> [!NOTE] 
> <span data-ttu-id="d1a6b-121">Этот шаг должен выполняться один раз в среде Azure стека.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-121">This step only needs to be completed once in an Azure Stack environment.</span></span>
>

1. <span data-ttu-id="d1a6b-122">Запуск интегрированной среды Сценариев Powershell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-122">Start Powershell ISE as an administrator.</span></span>
2. <span data-ttu-id="d1a6b-123">Выполните вход с учетной записью Azure, которая является владельцем подписки Azure с параметром - EnvironmentName в «Облачной».</span><span class="sxs-lookup"><span data-stu-id="d1a6b-123">Log in to the Azure account that is an owner of the Azure subscription with -EnvironmentName parameter set to "AzureCloud".</span></span>
3. <span data-ttu-id="d1a6b-124">Регистрация поставщика ресурсов Azure «Microsoft.AzureStack».</span><span class="sxs-lookup"><span data-stu-id="d1a6b-124">Register the Azure resource provider "Microsoft.AzureStack".</span></span>

<span data-ttu-id="d1a6b-125">Пример:</span><span class="sxs-lookup"><span data-stu-id="d1a6b-125">Example:</span></span> 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a><span data-ttu-id="d1a6b-126">Зарегистрировать стек Azure в Azure</span><span class="sxs-lookup"><span data-stu-id="d1a6b-126">Register Azure Stack with Azure</span></span>

> [!NOTE]
><span data-ttu-id="d1a6b-127">На главном компьютере необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-127">All these steps must be completed on the host computer.</span></span>
>

1. <span data-ttu-id="d1a6b-128">[Установите PowerShell для Azure стека](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="d1a6b-128">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
2. <span data-ttu-id="d1a6b-129">Копировать [RegisterWithAzure.ps1 сценарий](https://go.microsoft.com/fwlink/?linkid=842959) папку (например, C:\Temp).</span><span class="sxs-lookup"><span data-stu-id="d1a6b-129">Copy the [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) to a folder (such as C:\Temp).</span></span>
3. <span data-ttu-id="d1a6b-130">Запуск интегрированной среды Сценариев PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-130">Start PowerShell ISE as an administrator.</span></span>    
4. <span data-ttu-id="d1a6b-131">Запустите сценарий RegisterWithAzure.ps1, заменив следующие имена:</span><span class="sxs-lookup"><span data-stu-id="d1a6b-131">Run the RegisterWithAzure.ps1 script, replacing the following placeholders:</span></span>
    - <span data-ttu-id="d1a6b-132">*YourAccountName* является владельцем подписки Azure</span><span class="sxs-lookup"><span data-stu-id="d1a6b-132">*YourAccountName* is the owner of the Azure subscription</span></span>
    - <span data-ttu-id="d1a6b-133">*YourID* идентификатор подписки Azure, которую требуется использовать для регистрации стек Azure</span><span class="sxs-lookup"><span data-stu-id="d1a6b-133">*YourID* is the Azure subscription ID that you want to use to register Azure Stack</span></span>
    - <span data-ttu-id="d1a6b-134">*YourDirectory* — имя вашего клиента Azure Active Directory, ваша подписка Azure является частью.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-134">*YourDirectory* is the name of your Azure Active Directory tenant that your Azure subscription is a part of.</span></span>

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    <span data-ttu-id="d1a6b-135">Например:</span><span class="sxs-lookup"><span data-stu-id="d1a6b-135">For example:</span></span>
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. <span data-ttu-id="d1a6b-136">В двух запросов нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-136">At the two prompts, press Enter.</span></span>
6. <span data-ttu-id="d1a6b-137">В окне всплывающего входа введите учетные данные подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-137">In the pop-up login window, enter your Azure subscription credentials.</span></span>

## <a name="verify-the-registration"></a><span data-ttu-id="d1a6b-138">Проверьте регистрацию</span><span class="sxs-lookup"><span data-stu-id="d1a6b-138">Verify the registration</span></span>

1. <span data-ttu-id="d1a6b-139">Войдите в портал администратора (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="d1a6b-139">Sign in to the administrator portal (https://adminportal.local.azurestack.external).</span></span>
2. <span data-ttu-id="d1a6b-140">Нажмите кнопку **дополнительные службы** > **управления Marketplace** > **добавьте из Azure**.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-140">Click **More Services** > **Marketplace Management** > **Add from Azure**.</span></span>
3. <span data-ttu-id="d1a6b-141">Если отображается список элементов, доступный в Azure (таких как WordPress) активацию прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="d1a6b-141">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1a6b-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d1a6b-142">Next steps</span></span>

[<span data-ttu-id="d1a6b-143">Подключение к Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d1a6b-143">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

