---
title: "aaaCreate плана в стек Azure | Документы Microsoft"
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
ms.openlocfilehash: 3665bae5d212002da43316e62ce73686b4c66eea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="d37e1-103">Создание плана в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d37e1-103">Create a plan in Azure Stack</span></span>
<span data-ttu-id="d37e1-104">[Планы](azure-stack-key-features.md) — это группы, содержащие одну или несколько служб.</span><span class="sxs-lookup"><span data-stu-id="d37e1-104">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="d37e1-105">В качестве поставщика можно создавать планы toooffer tooyour клиентов.</span><span class="sxs-lookup"><span data-stu-id="d37e1-105">As a provider, you can create plans toooffer tooyour tenants.</span></span> <span data-ttu-id="d37e1-106">В свою очередь клиентам подписываться tooyour предложения toouse hello планы и службы, которые они включают.</span><span class="sxs-lookup"><span data-stu-id="d37e1-106">In turn, your tenants subscribe tooyour offers toouse hello plans and services they include.</span></span> <span data-ttu-id="d37e1-107">В этом примере показано, как toocreate план, который включает в себя hello поставщики ресурсов вычисления, сети и хранилища.</span><span class="sxs-lookup"><span data-stu-id="d37e1-107">This example shows you how toocreate a plan that includes hello compute, network, and storage resource providers.</span></span> <span data-ttu-id="d37e1-108">Этот план дает подписчиков hello возможность tooprovision виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d37e1-108">This plan gives subscribers hello ability tooprovision virtual machines.</span></span>

1. <span data-ttu-id="d37e1-109">Войдите в систему toohello портала администратора Azure стека (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="d37e1-109">Sign in toohello Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="d37e1-110">Введите учетные данные hello hello учетной записи, созданной на шаге 5 hello [скрипт PowerShell hello](azure-stack-run-powershell-script.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="d37e1-110">Enter hello credentials for hello account that you created during step 5 of hello [Run hello PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="d37e1-111">Щелкните toocreate плана и предложения, который клиенты могут подписываться на, **New** > **клиента предлагает + планы** > **плана**.</span><span class="sxs-lookup"><span data-stu-id="d37e1-111">toocreate a plan and offer that tenants can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="d37e1-112">В hello **создать план** колонки, заполните **отображаемое имя** и **имя ресурса**.</span><span class="sxs-lookup"><span data-stu-id="d37e1-112">In hello **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="d37e1-113">Hello отображаемое имя — hello плана понятное имя, которое будет отображаться для клиентов.</span><span class="sxs-lookup"><span data-stu-id="d37e1-113">hello Display Name is hello plan's friendly name that tenants see.</span></span> <span data-ttu-id="d37e1-114">Только администратор hello можно увидеть hello имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="d37e1-114">Only hello admin can see hello Resource Name.</span></span> <span data-ttu-id="d37e1-115">Он является hello имя, "Администраторы" использовать toowork с планом hello в качестве ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d37e1-115">It's hello name that admins use toowork with hello plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="d37e1-116">Создайте новый **группы ресурсов**, или выберите существующий как контейнер для плана hello.</span><span class="sxs-lookup"><span data-stu-id="d37e1-116">Create a new **Resource Group**, or select an existing one, as a container for hello plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="d37e1-117">Нажмите кнопку **службы**выберите **Microsoft.Compute**, **Microsoft.Network**, и **хранилища Майкрософт**, а затем нажмите кнопку **Выберите**.</span><span class="sxs-lookup"><span data-stu-id="d37e1-117">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="d37e1-118">Нажмите кнопку **квоты**, нажмите кнопку **хранилища Майкрософт (local)**и затем либо выберите hello Квота по умолчанию или нажмите кнопку **Создание новой квоте** toocustomize hello квоты.</span><span class="sxs-lookup"><span data-stu-id="d37e1-118">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="d37e1-119">При создании новой квоте, введите имя для квоты hello > задать значения квоты hello > щелкните **ОК** > щелкните имя новой квоте hello hello.</span><span class="sxs-lookup"><span data-stu-id="d37e1-119">If you're creating a new quota, enter a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="d37e1-120">Нажмите кнопку **Microsoft.Network (local)**и затем либо выберите hello Квота по умолчанию или нажмите кнопку **Создание новой квоте** toocustomize hello квоты.</span><span class="sxs-lookup"><span data-stu-id="d37e1-120">Click **Microsoft.Network (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="d37e1-121">При создании новой квоте, введите имя для квоты hello > задать значения квоты hello > щелкните **ОК** > щелкните имя новой квоте hello hello.</span><span class="sxs-lookup"><span data-stu-id="d37e1-121">If you're creating a new quota, type a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="d37e1-122">Нажмите кнопку **Microsoft.Compute (local)**и затем либо выберите hello Квота по умолчанию или нажмите кнопку **Создание новой квоте** toocustomize hello квоты.</span><span class="sxs-lookup"><span data-stu-id="d37e1-122">Click **Microsoft.Compute (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="d37e1-123">При создании новой квоте, введите имя для квоты hello > задать значения квоты hello > щелкните **ОК** > щелкните имя новой квоте hello hello.</span><span class="sxs-lookup"><span data-stu-id="d37e1-123">If you're creating a new quota, type a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="d37e1-124">В hello **квоты** колонке нажмите кнопку **ОК**и затем в hello **новый план** колонке нажмите кнопку **создать** toocreate hello плана.</span><span class="sxs-lookup"><span data-stu-id="d37e1-124">In hello **Quotas** blade, click **OK**, and then in hello **New Plan** blade, click **Create** toocreate hello plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="d37e1-125">toosee новый план, нажмите кнопку **все ресурсы**, а затем найдите hello план и щелкните ее имя.</span><span class="sxs-lookup"><span data-stu-id="d37e1-125">toosee your new plan, click **All resources**, then search for hello plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="d37e1-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d37e1-126">Next steps</span></span>
[<span data-ttu-id="d37e1-127">Создание предложения</span><span class="sxs-lookup"><span data-stu-id="d37e1-127">Create an offer</span></span>](azure-stack-create-offer.md)
