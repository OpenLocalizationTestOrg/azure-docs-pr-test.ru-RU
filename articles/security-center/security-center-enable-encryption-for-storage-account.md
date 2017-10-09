---
title: "шифрование aaaEnable для учетной записи хранилища в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить шифрование для Azure хранилища учетной записи **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="eb134-103">Включение шифрования данных для учетной записи хранения Azure в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="eb134-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="eb134-104">Центр безопасности Azure может рекомендовать включить шифрование службы хранилища Azure для неактивных данных.</span><span class="sxs-lookup"><span data-stu-id="eb134-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="eb134-105">Шифрование службы хранилища (SSE) осуществляется посредством шифрования данных hello записи tooAzure хранилища и расшифровки данных hello до извлечения.</span><span class="sxs-lookup"><span data-stu-id="eb134-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="eb134-106">SSE в настоящее время доступна только для hello службы больших двоичных объектов и может использоваться для больших двоичных объектов, страничные большие двоичные объекты и добавление BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="eb134-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="eb134-107">toolearn более, в разделе [шифрование службы хранилища для статических данных](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="eb134-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="eb134-108">После включения шифрования зашифровываются только новые данные.</span><span class="sxs-lookup"><span data-stu-id="eb134-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="eb134-109">Остальные существующие большие двоичные объекты в учетной записи хранения остаются незашифрованными.</span><span class="sxs-lookup"><span data-stu-id="eb134-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="eb134-110">существующие и большие двоичные объекты tooencrypt, в разделе hello [хранилища службы шифрования часто задаваемые вопросы о](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="eb134-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="eb134-111">Шифрование службы хранилища поддерживается только для учетных записей хранения Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="eb134-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="eb134-112">Классические учетные записи хранения в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="eb134-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="eb134-113">toounderstand hello классический и модели развертывания диспетчера ресурсов, в разделе [моделях развертывания Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="eb134-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="eb134-114">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="eb134-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="eb134-115">Этот документ не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="eb134-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="eb134-116">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="eb134-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="eb134-117">В hello **рекомендации** колонке выберите **включить шифрование для учетной записи хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="eb134-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="eb134-118">![Включение шифрования для учетной записи хранения][1]</span><span class="sxs-lookup"><span data-stu-id="eb134-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="eb134-119">Hello **включить шифрование хранилища** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="eb134-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="eb134-120">Эта колонка список учетных записей хранилища Azure hello, где отключен шифрование хранилища.</span><span class="sxs-lookup"><span data-stu-id="eb134-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="eb134-121">В этом примере выберем учетную запись **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="eb134-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="eb134-122">![Включение шифрования хранилища][2]</span><span class="sxs-lookup"><span data-stu-id="eb134-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="eb134-123">Hello **шифрования** колонке **storageacct1** открывается.</span><span class="sxs-lookup"><span data-stu-id="eb134-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="eb134-124">Щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="eb134-124">Select **Enabled**.</span></span>
   <span data-ttu-id="eb134-125">![Колонка "Шифрование"][3]</span><span class="sxs-lookup"><span data-stu-id="eb134-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="eb134-126">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="eb134-126">Select **Save**.</span></span>

<span data-ttu-id="eb134-127">Вы включили шифрование хранилища для учетной записи **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="eb134-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="eb134-128">См. также</span><span class="sxs-lookup"><span data-stu-id="eb134-128">See also</span></span>
<span data-ttu-id="eb134-129">В этом документе показано, как tooimplement hello центра обеспечения безопасности рекомендация «включить шифрование для учетной записи хранилища Azure».</span><span class="sxs-lookup"><span data-stu-id="eb134-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="eb134-130">toolearn Дополнительные сведения о шифрование службы хранилища Azure, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="eb134-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="eb134-131">Шифрование службы хранилища Azure для неактивных данных (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="eb134-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="eb134-132">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="eb134-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="eb134-133">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) -Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eb134-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="eb134-134">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) -Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="eb134-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="eb134-135">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) -Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="eb134-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="eb134-136">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md). Узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="eb134-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="eb134-137">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) -часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="eb134-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="eb134-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) (Блог по безопасности Azure). Публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="eb134-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
