---
title: "aaaRegister стек Azure | Документы Microsoft"
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
ms.openlocfilehash: 3a3c8e82bec3e1e26ecfe591ecc27b2b91f6f91e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a><span data-ttu-id="9484a-103">Регистрация стек Azure с подпиской Azure</span><span class="sxs-lookup"><span data-stu-id="9484a-103">Register Azure Stack with your Azure Subscription</span></span>

<span data-ttu-id="9484a-104">Для развертываний Azure Active Directory с Azure toodownload элементы marketplace из Azure и tooset commerce данные обратно reporting tooMicrosoft можно зарегистрировать стек Azure.</span><span class="sxs-lookup"><span data-stu-id="9484a-104">For Azure Active Directory deployments, you can register Azure Stack with Azure toodownload marketplace items from Azure and tooset up commerce data reporting back tooMicrosoft.</span></span> 

> [!NOTE]
><span data-ttu-id="9484a-105">Регистрация рекомендуется, так как он позволяет tootest важные стек Azure функциональных возможностей, таких как синдикации marketplace и отчеты об использовании.</span><span class="sxs-lookup"><span data-stu-id="9484a-105">Registration is recommended because it enables you tootest important Azure Stack functionality, like marketplace syndication and usage reporting.</span></span> <span data-ttu-id="9484a-106">После регистрации Azure стека вариантом применения является commerce tooAzure отчета.</span><span class="sxs-lookup"><span data-stu-id="9484a-106">After you register Azure Stack, usage is reported tooAzure commerce.</span></span> <span data-ttu-id="9484a-107">Его можно просматривать в подписке hello, использованный для регистрации.</span><span class="sxs-lookup"><span data-stu-id="9484a-107">You can see it under hello subscription you used for registration.</span></span> <span data-ttu-id="9484a-108">Пользователей Azure стека пакет средств разработки, не будете платить за все они сообщают об использовании.</span><span class="sxs-lookup"><span data-stu-id="9484a-108">Azure Stack Development Kit users will not be charged for any usage they report.</span></span>
>


## <a name="get-azure-subscription"></a><span data-ttu-id="9484a-109">Получить подписку Azure</span><span class="sxs-lookup"><span data-stu-id="9484a-109">Get Azure subscription</span></span>

<span data-ttu-id="9484a-110">Перед регистрацией стек Azure с помощью Azure, необходимо иметь:</span><span class="sxs-lookup"><span data-stu-id="9484a-110">Before registering Azure Stack with Azure, you must have:</span></span>

- <span data-ttu-id="9484a-111">Идентификатор подписки Hello для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="9484a-111">hello subscription ID for an Azure subscription.</span></span> <span data-ttu-id="9484a-112">Идентификатор hello tooget, вход tooAzure, нажмите кнопку **дополнительные службы** > **подписки**, щелкните подписку hello требуется toouse и в разделе **Essentials** вы можете найти hello **идентификатор подписки**.</span><span class="sxs-lookup"><span data-stu-id="9484a-112">tooget hello ID, sign in tooAzure, click **More services** > **Subscriptions**, click hello subscription you want toouse, and under **Essentials** you can find hello **Subscription ID**.</span></span> <span data-ttu-id="9484a-113">Китай, Германии и нам облака государственных подписок в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9484a-113">China, Germany, and US government cloud subscriptions are not currently supported.</span></span>
- <span data-ttu-id="9484a-114">Здравствуйте, имя пользователя и пароль учетной записи, которая является владельцем подписки hello (поддерживаются учетные записи MSA/2FA)</span><span class="sxs-lookup"><span data-stu-id="9484a-114">hello username and password for an account that is an owner for hello subscription (MSA/2FA accounts are supported)</span></span>
- <span data-ttu-id="9484a-115">Hello Azure Active Directory для hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="9484a-115">hello Azure Active Directory for hello Azure subscription.</span></span> <span data-ttu-id="9484a-116">Наведя аватара в верхнем правом углу hello hello портал Azure можно найти этот каталог в Azure.</span><span class="sxs-lookup"><span data-stu-id="9484a-116">You can find this directory in Azure by hovering over your avatar at hello top right corner of hello Azure portal.</span></span> 
- <span data-ttu-id="9484a-117">Зарегистрированные hello поставщика ресурсов Azure стека (hello в разделе **Регистрация поставщика ресурсов Azure стека** ниже, в разделе подробные сведения)</span><span class="sxs-lookup"><span data-stu-id="9484a-117">Registered hello Azure Stack resource provider (see hello **Register Azure Stack Resource Provider** section below for details)</span></span>

<span data-ttu-id="9484a-118">Если нет подписки Azure, удовлетворяющее этим требованиям, вы можете [создать бесплатную учетную запись Azure здесь](https://azure.microsoft.com/en-us/free/?b=17.06).</span><span class="sxs-lookup"><span data-stu-id="9484a-118">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06).</span></span> <span data-ttu-id="9484a-119">Регистрация стек Azure влечет за собой без затрат на подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="9484a-119">Registering Azure Stack incurs no cost on your Azure subscription.</span></span>



## <a name="register-azure-stack-resource-provider-in-azure"></a><span data-ttu-id="9484a-120">Регистрация поставщика ресурсов Azure стека в Azure</span><span class="sxs-lookup"><span data-stu-id="9484a-120">Register Azure Stack resource provider in Azure</span></span>
> [!NOTE] 
> <span data-ttu-id="9484a-121">Этот шаг требуется только один раз выполнить в среде Azure стека toobe.</span><span class="sxs-lookup"><span data-stu-id="9484a-121">This step only needs toobe completed once in an Azure Stack environment.</span></span>
>

1. <span data-ttu-id="9484a-122">Запуск интегрированной среды Сценариев Powershell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="9484a-122">Start Powershell ISE as an administrator.</span></span>
2. <span data-ttu-id="9484a-123">Вход toohello учетная запись Azure, который является владельцем hello подписки Azure с параметром - EnvironmentName значение слишком «Облачной».</span><span class="sxs-lookup"><span data-stu-id="9484a-123">Log in toohello Azure account that is an owner of hello Azure subscription with -EnvironmentName parameter set too"AzureCloud".</span></span>
3. <span data-ttu-id="9484a-124">Регистрация поставщика ресурсов Azure hello «Microsoft.AzureStack».</span><span class="sxs-lookup"><span data-stu-id="9484a-124">Register hello Azure resource provider "Microsoft.AzureStack".</span></span>

<span data-ttu-id="9484a-125">Пример:</span><span class="sxs-lookup"><span data-stu-id="9484a-125">Example:</span></span> 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a><span data-ttu-id="9484a-126">Зарегистрировать стек Azure в Azure</span><span class="sxs-lookup"><span data-stu-id="9484a-126">Register Azure Stack with Azure</span></span>

> [!NOTE]
><span data-ttu-id="9484a-127">На главном компьютере hello необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9484a-127">All these steps must be completed on hello host computer.</span></span>
>

1. <span data-ttu-id="9484a-128">[Установите PowerShell для Azure стека](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="9484a-128">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
2. <span data-ttu-id="9484a-129">Копировать hello [RegisterWithAzure.ps1 сценарий](https://go.microsoft.com/fwlink/?linkid=842959) tooa папку (например, C:\Temp).</span><span class="sxs-lookup"><span data-stu-id="9484a-129">Copy hello [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) tooa folder (such as C:\Temp).</span></span>
3. <span data-ttu-id="9484a-130">Запуск интегрированной среды Сценариев PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="9484a-130">Start PowerShell ISE as an administrator.</span></span>    
4. <span data-ttu-id="9484a-131">Запустите сценарий RegisterWithAzure.ps1 hello, заменив hello следующие местозаполнители:</span><span class="sxs-lookup"><span data-stu-id="9484a-131">Run hello RegisterWithAzure.ps1 script, replacing hello following placeholders:</span></span>
    - <span data-ttu-id="9484a-132">*YourAccountName* является владельцем hello hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="9484a-132">*YourAccountName* is hello owner of hello Azure subscription</span></span>
    - <span data-ttu-id="9484a-133">*YourID* — идентификатор подписки Azure hello, что требуется toouse tooregister стек Azure</span><span class="sxs-lookup"><span data-stu-id="9484a-133">*YourID* is hello Azure subscription ID that you want toouse tooregister Azure Stack</span></span>
    - <span data-ttu-id="9484a-134">*YourDirectory* — имя вашего клиента Azure Active Directory, ваша подписка Azure является частью hello.</span><span class="sxs-lookup"><span data-stu-id="9484a-134">*YourDirectory* is hello name of your Azure Active Directory tenant that your Azure subscription is a part of.</span></span>

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    <span data-ttu-id="9484a-135">Например:</span><span class="sxs-lookup"><span data-stu-id="9484a-135">For example:</span></span>
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. <span data-ttu-id="9484a-136">В hello два запроса нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="9484a-136">At hello two prompts, press Enter.</span></span>
6. <span data-ttu-id="9484a-137">В окне приветствия всплывающих входа введите учетные данные подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="9484a-137">In hello pop-up login window, enter your Azure subscription credentials.</span></span>

## <a name="verify-hello-registration"></a><span data-ttu-id="9484a-138">Проверка регистрации hello</span><span class="sxs-lookup"><span data-stu-id="9484a-138">Verify hello registration</span></span>

1. <span data-ttu-id="9484a-139">Войдите в портал администратора toohello (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="9484a-139">Sign in toohello administrator portal (https://adminportal.local.azurestack.external).</span></span>
2. <span data-ttu-id="9484a-140">Нажмите кнопку **дополнительные службы** > **управления Marketplace** > **добавьте из Azure**.</span><span class="sxs-lookup"><span data-stu-id="9484a-140">Click **More Services** > **Marketplace Management** > **Add from Azure**.</span></span>
3. <span data-ttu-id="9484a-141">Если отображается список элементов, доступный в Azure (таких как WordPress) активацию прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="9484a-141">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9484a-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9484a-142">Next steps</span></span>

[<span data-ttu-id="9484a-143">Подключение tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="9484a-143">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

