---
title: "Создать план в стек Azure | Документы Microsoft"
description: "Как администратор облака создайте план, который позволяет подписчикам подготовки виртуальных машин."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: 30759dca746fd7fd02653556cb105f419f5bf854
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="ffaa8-103">Создание плана в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ffaa8-103">Create a plan in Azure Stack</span></span>

<span data-ttu-id="ffaa8-104">*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*</span><span class="sxs-lookup"><span data-stu-id="ffaa8-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="ffaa8-105">[Планы](azure-stack-key-features.md) — это группы, содержащие одну или несколько служб.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-105">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="ffaa8-106">В качестве поставщика можно создать планах можно предложить пользователям.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-106">As a provider, you can create plans to offer to your users.</span></span> <span data-ttu-id="ffaa8-107">В свою очередь пользователи подписываться на вашего предложения для использования планы и службы, которые они включают.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-107">In turn, your users subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="ffaa8-108">В этом примере показано, как создать план, который содержит вычисления, сети и поставщики ресурсов хранилища.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-108">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span></span> <span data-ttu-id="ffaa8-109">Этот план позволяет подписчикам для подготовки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-109">This plan gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="ffaa8-110">Войдите в портал администратора Azure стека (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="ffaa8-110">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="ffaa8-111">Введите учетные данные для учетной записи, созданной на шаге 5 [запустить сценарий PowerShell](azure-stack-run-powershell-script.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-111">Enter the credentials for the account that you created during step 5 of the [Run the PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="ffaa8-112">Чтобы создать план и пользователи смогут подписаться на предложение, щелкните **New** > **клиента предлагает + планы** > **плана**.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-112">To create a plan and offer that users can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="ffaa8-113">В **создать план** колонки, заполните **отображаемое имя** и **имя ресурса**.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-113">In the **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="ffaa8-114">Отображаемое имя — плана понятное имя, которое будет отображаться для пользователей.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-114">The Display Name is the plan's friendly name that users see.</span></span> <span data-ttu-id="ffaa8-115">Только администратор может видеть имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-115">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="ffaa8-116">Это имя, которое администраторы используют для работы с планом в качестве ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-116">It's the name that admins use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="ffaa8-117">Создайте новый **группы ресурсов**, или выберите существующий как контейнер для плана.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-117">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="ffaa8-118">Нажмите кнопку **службы**выберите **Microsoft.Compute**, **Microsoft.Network**, и **хранилища Майкрософт**, а затем нажмите кнопку **Выберите**.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-118">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="ffaa8-119">Нажмите кнопку **квоты**, нажмите кнопку **хранилища Майкрософт (local)**и затем выберите Квота по умолчанию или нажмите кнопку **Создание новой квоте** для настройки квоты.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-119">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="ffaa8-120">При создании новой квоте, введите имя для квоты > задать значения квот > щелкните **ОК** > щелкните имя новой квоте.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-120">If you're creating a new quota, enter a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="ffaa8-121">Нажмите кнопку **Microsoft.Network (local)**и затем выберите Квота по умолчанию или нажмите кнопку **Создание новой квоте** для настройки квоты.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-121">Click **Microsoft.Network (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="ffaa8-122">При создании новой квоте, введите имя для квоты > задать значения квот > щелкните **ОК** > щелкните имя новой квоте.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-122">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="ffaa8-123">Нажмите кнопку **Microsoft.Compute (local)**и затем выберите Квота по умолчанию или нажмите кнопку **Создание новой квоте** для настройки квоты.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-123">Click **Microsoft.Compute (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="ffaa8-124">При создании новой квоте, введите имя для квоты > задать значения квот > щелкните **ОК** > щелкните имя новой квоте.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-124">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="ffaa8-125">В **квоты** колонке нажмите кнопку **ОК**, а затем в **новый план** колонке нажмите кнопку **создать** для создания плана.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-125">In the **Quotas** blade, click **OK**, and then in the **New Plan** blade, click **Create** to create the plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="ffaa8-126">Для просмотра нового плана, нажмите кнопку **все ресурсы**, а затем найдите план и щелкните ее имя.</span><span class="sxs-lookup"><span data-stu-id="ffaa8-126">To see your new plan, click **All resources**, then search for the plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="ffaa8-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ffaa8-127">Next steps</span></span>
[<span data-ttu-id="ffaa8-128">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="ffaa8-128">Create an offer</span></span>](azure-stack-create-offer.md)
