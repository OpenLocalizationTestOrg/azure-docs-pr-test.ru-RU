---
title: "Запросы на увеличение квоты ядер Azure Resource Manager | Документация Майкрософт"
description: "Запросы на увеличение квоты ядер Azure Resource Manager."
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="de674-103">Запросы на увеличение квоты ядер Resource Manager</span><span class="sxs-lookup"><span data-stu-id="de674-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="de674-104">Квоты ядер Resource Manager применяются на уровне региона и семейства SKU.</span><span class="sxs-lookup"><span data-stu-id="de674-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="de674-105">Дополнительные сведения о применении квот доступны на странице [Подписка Azure, границы, квоты и ограничения службы](http://aka.ms/quotalimits).</span><span class="sxs-lookup"><span data-stu-id="de674-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="de674-106">Чтобы узнать больше о семействах SKU, вы можете сравнить затраты и производительность на странице [Цены на виртуальные машины Windows](http://aka.ms/pricingcompute).</span><span class="sxs-lookup"><span data-stu-id="de674-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="de674-107">Чтобы запросить увеличение квоты ядер, отправьте соответствующее обращение в службу поддержки на портале Azure: [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de674-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="de674-108">Узнайте, как [создать запрос на поддержку](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="de674-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="de674-109">На странице создания запроса на поддержку выберите тип проблемы "Квота" и тип квоты как "Ядра".</span><span class="sxs-lookup"><span data-stu-id="de674-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![Колонка "Основные" для квоты](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="de674-111">Выберите модель развертывания "Resource Manager" и укажите расположение.</span><span class="sxs-lookup"><span data-stu-id="de674-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Колонка "Проблема" для квоты](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="de674-113">Выберите семейства SKU, которые требуют увеличения квоты.</span><span class="sxs-lookup"><span data-stu-id="de674-113">Select the SKU Families that require an increase.</span></span>

    ![Выбранные семейства SKU](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="de674-115">Введите желаемые ограничения для подписки.</span><span class="sxs-lookup"><span data-stu-id="de674-115">Enter the new limits you would like on the subscription.</span></span>

    ![Новый запрос квоты для SKU](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="de674-117">Чтобы удалить строку, снимите флажок SKU в раскрывающемся списке семейства SKU или щелкните значок отмены "x".</span><span class="sxs-lookup"><span data-stu-id="de674-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="de674-118">После ввода требуемой квоты для каждого семейства SKU нажмите кнопку "Далее" на странице "Проблема", чтобы продолжить создание запроса на поддержку.</span><span class="sxs-lookup"><span data-stu-id="de674-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
