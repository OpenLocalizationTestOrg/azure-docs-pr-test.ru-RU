---
title: "элементы marketplace aaaDownload из Azure | Документы Microsoft"
description: "Элементы marketplace можно загрузить из Azure toomy развертывания Azure стека."
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
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: erikje
ms.openlocfilehash: 734470fbacc09617908a2f6db9107ffa9c39e51d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-marketplace-items-from-azure-tooazure-stack"></a><span data-ttu-id="cd77b-103">Загрузить элементы marketplace из Azure tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="cd77b-103">Download marketplace items from Azure tooAzure Stack</span></span>

<span data-ttu-id="cd77b-104">Как вы решите какие tooinclude содержимого в вашей стек Azure marketplace, рассмотрите возможность hello содержимого, доступного из hello Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="cd77b-104">As you decide what content tooinclude in your Azure Stack marketplace, you should consider hello content available from hello Azure marketplace.</span></span> <span data-ttu-id="cd77b-105">Можно загрузить из проверенного список элементов Azure marketplace, которые были заранее протестированных toorun стек Azure.</span><span class="sxs-lookup"><span data-stu-id="cd77b-105">You can download from a curated list of Azure marketplace items that have been pre-tested toorun on Azure Stack.</span></span> <span data-ttu-id="cd77b-106">Список toothis часто добавляются новые элементы, поэтому убедитесь, что следите за новым содержимым.</span><span class="sxs-lookup"><span data-stu-id="cd77b-106">New items are frequently added toothis list, so make sure check back for new content.</span></span>

<span data-ttu-id="cd77b-107">элементы marketplace toodownload, сначала необходимо выполнить [Azure стеком регистров с помощью Azure](azure-stack-register.md).</span><span class="sxs-lookup"><span data-stu-id="cd77b-107">toodownload marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span></span> 

## <a name="download"></a><span data-ttu-id="cd77b-108">Загрузить</span><span class="sxs-lookup"><span data-stu-id="cd77b-108">Download</span></span>
1. <span data-ttu-id="cd77b-109">Войдите в систему toohello портала администратора Azure стека (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="cd77b-109">Sign in toohello Azure Stack administrator portal (https://portal.local.azurestack.external).</span></span>
2. <span data-ttu-id="cd77b-110">Некоторые элементы marketplace может быть очень большим.</span><span class="sxs-lookup"><span data-stu-id="cd77b-110">Some marketplace items can be very large.</span></span>  <span data-ttu-id="cd77b-111">Проверьте toomake убедиться, что имеется достаточно места на компьютере, щелкнув **поставщиков ресурсов** > **хранения**.</span><span class="sxs-lookup"><span data-stu-id="cd77b-111">Check toomake sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. <span data-ttu-id="cd77b-112">Нажмите кнопку **дополнительные службы** > **управления Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="cd77b-112">Click **More Services** > **Marketplace Management**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. <span data-ttu-id="cd77b-113">Нажмите кнопку **добавить из Azure** toosee список элементов, доступных для загрузки.</span><span class="sxs-lookup"><span data-stu-id="cd77b-113">Click **Add from Azure** toosee a list of items available for download.</span></span> <span data-ttu-id="cd77b-114">Можно щелкнуть ее описание каждого элемента в списке tooview hello и размер загружаемого файла.</span><span class="sxs-lookup"><span data-stu-id="cd77b-114">You can click on each item in hello list tooview its description and download size.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. <span data-ttu-id="cd77b-115">Элемент SELECT hello hello списка и нажмите кнопку **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="cd77b-115">Select hello item you want in hello list and then click **Download**.</span></span> <span data-ttu-id="cd77b-116">Запустится загрузка образа виртуальной Машины hello для выбранного элемента hello.</span><span class="sxs-lookup"><span data-stu-id="cd77b-116">This starts downloading hello VM image for hello item you selected.</span></span> <span data-ttu-id="cd77b-117">Время загрузки различаются.</span><span class="sxs-lookup"><span data-stu-id="cd77b-117">Download times vary.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. <span data-ttu-id="cd77b-118">После завершения загрузки hello, вы можете развернуть новый элемент marketplace как оператор облака или пользователь клиента.</span><span class="sxs-lookup"><span data-stu-id="cd77b-118">After hello download completes, you can deploy your new marketplace item as either a cloud operator or tenant user.</span></span> <span data-ttu-id="cd77b-119">Нажмите кнопку **+ создать**, поиск среди hello категории для hello создать элемент marketplace, а затем выберите элемент hello.</span><span class="sxs-lookup"><span data-stu-id="cd77b-119">Click **+New**, search among hello categories for hello new marketplace item, and then select hello item.</span></span>
7. <span data-ttu-id="cd77b-120">Нажмите кнопку **создать** tooopen копирование hello возможности создания для hello вновь загружена элемента.</span><span class="sxs-lookup"><span data-stu-id="cd77b-120">Click **Create** tooopen up hello creation experience for hello newly downloaded item.</span></span> <span data-ttu-id="cd77b-121">Выполните пошаговые инструкции toodeploy hello ваш элемент.</span><span class="sxs-lookup"><span data-stu-id="cd77b-121">Follow hello step-by-step instructions toodeploy your item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd77b-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd77b-122">Next steps</span></span>

[<span data-ttu-id="cd77b-123">Создание и публикация элемента Marketplace</span><span class="sxs-lookup"><span data-stu-id="cd77b-123">Create and publish a Marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)
