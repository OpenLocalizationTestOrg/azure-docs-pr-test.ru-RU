---
title: "Загрузить элементы marketplace из Azure | Документы Microsoft"
description: "Мои развертывание стека Azure можно загрузить элементы marketplace из Azure."
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
ms.openlocfilehash: 4d7c335a3c68cc9bb8cb0c823883716a3dd6620a
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="download-marketplace-items-from-azure-to-azure-stack"></a><span data-ttu-id="4f708-103">Загрузить элементы marketplace из Azure в стек Azure</span><span class="sxs-lookup"><span data-stu-id="4f708-103">Download marketplace items from Azure to Azure Stack</span></span>

<span data-ttu-id="4f708-104">*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*</span><span class="sxs-lookup"><span data-stu-id="4f708-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="4f708-105">Как вы решите, какое содержимое для включения в ваш стек Azure marketplace, рассмотрите возможность содержимое из Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="4f708-105">As you decide what content to include in your Azure Stack marketplace, you should consider the content available from the Azure marketplace.</span></span> <span data-ttu-id="4f708-106">Можно загрузить из списка проверенного Azure marketplace элементов, которые были заранее протестированных для запуска на Azure стека.</span><span class="sxs-lookup"><span data-stu-id="4f708-106">You can download from a curated list of Azure marketplace items that have been pre-tested to run on Azure Stack.</span></span> <span data-ttu-id="4f708-107">Часто новые элементы добавляются в этот список, поэтому убедитесь, что следите за новым содержимым.</span><span class="sxs-lookup"><span data-stu-id="4f708-107">New items are frequently added to this list, so make sure check back for new content.</span></span>

<span data-ttu-id="4f708-108">Чтобы загрузить элементы marketplace, сначала необходимо выполнить [Azure стеком регистров с помощью Azure](azure-stack-register.md).</span><span class="sxs-lookup"><span data-stu-id="4f708-108">To download marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span></span> 

## <a name="download"></a><span data-ttu-id="4f708-109">Загрузить</span><span class="sxs-lookup"><span data-stu-id="4f708-109">Download</span></span>
1. <span data-ttu-id="4f708-110">Войдите в портал администратора Azure стека (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="4f708-110">Sign in to the Azure Stack administrator portal (https://portal.local.azurestack.external).</span></span>
2. <span data-ttu-id="4f708-111">Некоторые элементы marketplace может быть очень большим.</span><span class="sxs-lookup"><span data-stu-id="4f708-111">Some marketplace items can be very large.</span></span>  <span data-ttu-id="4f708-112">Убедитесь, что имеется достаточно места на компьютере, щелкнув **поставщиков ресурсов** > **хранения**.</span><span class="sxs-lookup"><span data-stu-id="4f708-112">Check to make sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. <span data-ttu-id="4f708-113">Нажмите кнопку **дополнительные службы** > **управления Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="4f708-113">Click **More Services** > **Marketplace Management**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. <span data-ttu-id="4f708-114">Нажмите кнопку **добавить из Azure** для просмотра списка элементов, доступных для загрузки.</span><span class="sxs-lookup"><span data-stu-id="4f708-114">Click **Add from Azure** to see a list of items available for download.</span></span> <span data-ttu-id="4f708-115">Можно щелкнуть каждый элемент в списке, чтобы просмотреть ее описание и размер загружаемого файла.</span><span class="sxs-lookup"><span data-stu-id="4f708-115">You can click on each item in the list to view its description and download size.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. <span data-ttu-id="4f708-116">Выберите элемент в списке и нажмите кнопку **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="4f708-116">Select the item you want in the list and then click **Download**.</span></span> <span data-ttu-id="4f708-117">Запустится загрузка образа виртуальной Машины для выбранного элемента.</span><span class="sxs-lookup"><span data-stu-id="4f708-117">This starts downloading the VM image for the item you selected.</span></span> <span data-ttu-id="4f708-118">Время загрузки различаются.</span><span class="sxs-lookup"><span data-stu-id="4f708-118">Download times vary.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. <span data-ttu-id="4f708-119">После завершения загрузки, можно развернуть новый элемент marketplace как оператор стек Azure или пользователя.</span><span class="sxs-lookup"><span data-stu-id="4f708-119">After the download completes, you can deploy your new marketplace item as either an Azure Stack operator or user.</span></span> <span data-ttu-id="4f708-120">Нажмите кнопку **+ создать**, поиск среди категории для нового элемента marketplace, а затем выберите элемент.</span><span class="sxs-lookup"><span data-stu-id="4f708-120">Click **+New**, search among the categories for the new marketplace item, and then select the item.</span></span>
7. <span data-ttu-id="4f708-121">Нажмите кнопку **создать** открывая процесс создания для вновь загруженного элемента.</span><span class="sxs-lookup"><span data-stu-id="4f708-121">Click **Create** to open up the creation experience for the newly downloaded item.</span></span> <span data-ttu-id="4f708-122">Выполните пошаговые инструкции для развертывания вашего элемента.</span><span class="sxs-lookup"><span data-stu-id="4f708-122">Follow the step-by-step instructions to deploy your item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f708-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f708-123">Next steps</span></span>

[<span data-ttu-id="4f708-124">Создание и публикация элемента Marketplace</span><span class="sxs-lookup"><span data-stu-id="4f708-124">Create and publish a Marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)
