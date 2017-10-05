---
title: "Регистрация запроса в службу поддержки с помощью диспетчера устройств StorSimple | Документация Майкрософт"
description: "В статье описываются возможности диагностики диспетчера устройств StorSimple и способы его использования для устранения неполадок в виртуальном массиве StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a0c394df-957b-49b3-a283-38824f8847fd
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 658afbc178814389fefd7941e2ca030741bd08e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-log-a-support-request-for-the-storsimple-virtual-array"></a><span data-ttu-id="09973-103">Использование службы диспетчера устройств StorSimple для регистрации запроса в службу поддержки для виртуального массива StorSimple</span><span class="sxs-lookup"><span data-stu-id="09973-103">Use the StorSimple Device Manager service to log a Support request for the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="09973-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="09973-104">Overview</span></span>

<span data-ttu-id="09973-105">Диспетчер устройств StorSimple предоставляет возможность **регистрации новых запросов в службу поддержки** в колонке сводных данных о службе.</span><span class="sxs-lookup"><span data-stu-id="09973-105">The StorSimple Device Manager provides the capability to **log a new support request** within the service summary blade.</span></span> <span data-ttu-id="09973-106">В этой статье объясняется, как зарегистрировать новый запрос и управлять его жизненным циклом на портале.</span><span class="sxs-lookup"><span data-stu-id="09973-106">This article explains how you can log a new support request and manage its lifecycle from within the portal.</span></span>

## <a name="new-support-request"></a><span data-ttu-id="09973-107">Новый запрос на техническую поддержку</span><span class="sxs-lookup"><span data-stu-id="09973-107">New support request</span></span>

<span data-ttu-id="09973-108">В зависимости от [плана поддержки](https://azure.microsoft.com/support/plans/) запросы в службу поддержки для решения проблем с виртуальным массивом StorSimple можно создать непосредственно в колонке сводных данных о службе диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="09973-108">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple Virtual array directly from the StorSimple Device Manager service summary blade.</span></span>

#### <a name="to-log-a-new-request"></a><span data-ttu-id="09973-109">Регистрация нового запроса</span><span class="sxs-lookup"><span data-stu-id="09973-109">To log a new request</span></span>

1. <span data-ttu-id="09973-110">Откройте службу диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="09973-110">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="09973-111">В настройках колонки сводных данных о службе перейдите в раздел **Поддержка и устранение неполадок** и щелкните **Новый запрос в службу поддержки**.</span><span class="sxs-lookup"><span data-stu-id="09973-111">In the service summary blade settings, go to **SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
   
    ![Новый запрос на техническую поддержку](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket1.png)

2. <span data-ttu-id="09973-113">В колонке **Основное** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="09973-113">In the **Basics** blade, do the following:</span></span>

    1. <span data-ttu-id="09973-114">В раскрывающемся списке **Тип проблемы** выберите **Техническая**.</span><span class="sxs-lookup"><span data-stu-id="09973-114">From the **Issue type** dropdown list, select **Technical**.</span></span> 
    
    2. <span data-ttu-id="09973-115">Текущая **подписка**, тип **службы** и **ресурс** (служба диспетчера устройств StorSimple) выбираются автоматически.</span><span class="sxs-lookup"><span data-stu-id="09973-115">The current **Subscription**, **Service** type, and the **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 

    3. <span data-ttu-id="09973-116">Укажите одно или несколько устройств, зарегистрированных в службе, с которыми возникли проблемы.</span><span class="sxs-lookup"><span data-stu-id="09973-116">Specify one or more devices registered to your service that are experiencing issues.</span></span>

    4. <span data-ttu-id="09973-117">Выберите соответствующий **план поддержки** при наличии нескольких планов, связанных с подпиской.</span><span class="sxs-lookup"><span data-stu-id="09973-117">Choose an appropriate **support plan** if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="09973-118">Чтобы получить техническую поддержку, у вас должен быть платный план поддержки.</span><span class="sxs-lookup"><span data-stu-id="09973-118">You need a paid support plan to enable Technical Support.</span></span>

3. <span data-ttu-id="09973-119">На **шаге 2** выберите тип **серьезности** и укажите, с чем связана проблема: с массивом или со службой диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="09973-119">In **Step 2**, choose the **Severity** and specify if the issue is related to the array or the StorSimple Device Manager service.</span></span> <span data-ttu-id="09973-120">Кроме того, выберите **категорию** этой проблемы и предоставьте больше **сведений** о проблеме.</span><span class="sxs-lookup"><span data-stu-id="09973-120">Also, choose a **Category** for this issue and provide more **Details** about the issue.</span></span>
   
    ![Новый запрос на техническую поддержку](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket2.png)

4. <span data-ttu-id="09973-122">На **шаге 3** предоставьте свои контактные данные.</span><span class="sxs-lookup"><span data-stu-id="09973-122">In **Step 3**, provide your contact information.</span></span> <span data-ttu-id="09973-123">Служба технической поддержки Майкрософт будет использовать эту информацию, чтобы связаться с вами для получения дополнительных сведений, диагностики и устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="09973-123">Microsoft Support will use this information to reach out to you for further information, diagnosis, and resolution.</span></span>
   
    ![Новый запрос на техническую поддержку](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket3.png)

## <a name="manage-a-support-request"></a><span data-ttu-id="09973-125">Управление запросом в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="09973-125">Manage a support request</span></span>

<span data-ttu-id="09973-126">После создания запроса вы можете управлять его жизненным циклом, не покидая портал.</span><span class="sxs-lookup"><span data-stu-id="09973-126">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span>

#### <a name="to-manage-your-support-requests"></a><span data-ttu-id="09973-127">Управление запросами в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="09973-127">To manage your support requests</span></span>

<span data-ttu-id="09973-128">Чтобы открыть страницу справки и поддержки, последовательно щелкните **Обзор > Справка и поддержка**.</span><span class="sxs-lookup"><span data-stu-id="09973-128">To get to the help and support page, navigate to **Browse > Help + support**.</span></span>

![Управление запросами на поддержку](./media/storsimple-virtual-array-log-support-ticket/manage-support-tickets.png)

## <a name="next-steps"></a><span data-ttu-id="09973-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09973-130">Next steps</span></span>

<span data-ttu-id="09973-131">[Устранение неполадок виртуального массива StorSimple с помощью диспетчера устройств StorSimple](storsimple-virtual-array-diagnose-problems.md)</span><span class="sxs-lookup"><span data-stu-id="09973-131">Learn how to [diagnose and solve problems related to your StorSimple Virtual array](storsimple-virtual-array-diagnose-problems.md)</span></span>

