---
title: "Новые возможности в Машинном обучении Azure | Документация Майкрософт"
description: "Новые возможности в Машинном обучении Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: ddc716ed-2615-4806-bf27-6c9a5662a7f2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 551b977b90612ddbfa1514a9c2358ebf8179c385
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-azure-machine-learning"></a><span data-ttu-id="56818-103">Новые возможности Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="56818-103">What's New in Azure Machine Learning</span></span>

### <a name="the-march-2017-release-of-microsoft-azure-machine-learning-updates-provides-the-following-feature"></a><span data-ttu-id="56818-104">Обновления для Машинного обучения Microsoft Azure за март 2017 года обеспечивают следующее.</span><span class="sxs-lookup"><span data-stu-id="56818-104">The March 2017 release of Microsoft Azure Machine Learning updates provides the following feature:</span></span>



* <span data-ttu-id="56818-105">Выделенная емкость для заданий службы выполнения пакетов (BES) машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="56818-105">Dedicated Capacity for Azure Machine Learning BES Jobs</span></span>

    <span data-ttu-id="56818-106">Для обработки пул пакетной службы машинного обучения использует [пакетную службу Azure](../batch/batch-technical-overview.md), чтобы предоставить пользователям управление масштабированием службы выполнения пакетов машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="56818-106">Machine Learning Batch Pool processing uses the [Azure Batch](../batch/batch-technical-overview.md) service to provide customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="56818-107">Обработка в пуле пакетной службы дает возможность создавать пулы пакетной службы Azure, в которые можно отправлять пакетные задания и выполнять их предсказуемым образом.</span><span class="sxs-lookup"><span data-stu-id="56818-107">Batch Pool processing allows you to create Azure Batch pools on which you can submit batch jobs and have them execute in a predictable manner.</span></span>

    <span data-ttu-id="56818-108">Дополнительные сведения см. в разделе [Пакетные службы Azure для обработки заданий машинного обучения](machine-learning-dedicated-capacity-for-bes-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="56818-108">For more information, see [Azure Batch service for Machine Learning jobs](machine-learning-dedicated-capacity-for-bes-jobs.md).</span></span>


### <a name="the-august-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="56818-109">Обновления для машинного обучения Microsoft Azure за август 2016 года обеспечивают приведенные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="56818-109">The August 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="56818-110">Классическими веб-службами теперь можно управлять на новом портале [веб-служб машинного обучения Microsoft Azure](https://services.azureml.net/), который предоставляет возможность централизованно управлять всеми аспектами веб-службы.</span><span class="sxs-lookup"><span data-stu-id="56818-110">Classic Web services can now be managed in the new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>    
  * <span data-ttu-id="56818-111">На нем предоставляется [статистика использования](machine-learning-manage-new-webservice.md) веб-службы.</span><span class="sxs-lookup"><span data-stu-id="56818-111">Which provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
  * <span data-ttu-id="56818-112">Упрощается тестирование вызовов удаленных запросов машинного обучения Azure с использованием примеров данных.</span><span class="sxs-lookup"><span data-stu-id="56818-112">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
  * <span data-ttu-id="56818-113">Предоставляется новая страница тестирования службы пакетного выполнения, на которой можно использовать примеры данных и журнал отправки заданий.</span><span class="sxs-lookup"><span data-stu-id="56818-113">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>
  * <span data-ttu-id="56818-114">Обеспечивается более простое управление конечными точками.</span><span class="sxs-lookup"><span data-stu-id="56818-114">Provides easier endpoint management.</span></span>

### <a name="the-july-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="56818-115">Обновления для машинного обучения Microsoft Azure за июль 2016 года обеспечивают приведенные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="56818-115">The July 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="56818-116">Веб-службы теперь управляются как ресурсы Azure, с помощью интерфейсов [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) , что обеспечивает следующие усовершенствования:</span><span class="sxs-lookup"><span data-stu-id="56818-116">Web services are now managed as Azure resources managed through [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) interfaces, allowing for the following enhancements:</span></span>
  * <span data-ttu-id="56818-117">Добавлены новые [интерфейсы REST API](https://msdn.microsoft.com/library/azure/Dn950030.aspx) для развертывания веб-служб с помощью Resource Manager и управления ими.</span><span class="sxs-lookup"><span data-stu-id="56818-117">There are new [REST APIs](https://msdn.microsoft.com/library/azure/Dn950030.aspx) to deploy and manage your Resource Manager based Web services.</span></span>
  * <span data-ttu-id="56818-118">Доступен новый портал [веб-служб машинного обучения Microsoft Azure](https://services.azureml.net/), который позволяет централизованно управлять всеми аспектами веб-службы.</span><span class="sxs-lookup"><span data-stu-id="56818-118">There is a new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>
* <span data-ttu-id="56818-119">Добавлена новая модель развертывания веб-служб в нескольких регионах по подписке, в которой применяются интерфейсы API на основе Resource Manager, использующие поставщик ресурсов Resource Manager для веб-служб.</span><span class="sxs-lookup"><span data-stu-id="56818-119">Incorporates a new subscription-based, multi-region web service deployment model using Resource Manager based APIs leveraging the Resource Manager Resource Provider for Web Services.</span></span>
* <span data-ttu-id="56818-120">Добавлены новые [ценовые планы](https://azure.microsoft.com/pricing/details/machine-learning/) и возможности планирования управления, использующие новые функции поставщика ресурсов Resource Manager для выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="56818-120">Introduces new [pricing plans](https://azure.microsoft.com/pricing/details/machine-learning/) and plan management capabilities using the new Resource Manager RP for Billing.</span></span>
  * <span data-ttu-id="56818-121">Теперь можно [развернуть веб-службу в нескольких регионах](machine-learning-how-to-deploy-to-multiple-regions.md) без необходимости создавать новую подписку в каждом из них.</span><span class="sxs-lookup"><span data-stu-id="56818-121">You can now [deploy your web service to multiple regions](machine-learning-how-to-deploy-to-multiple-regions.md) without needing to create a subscription in each region.</span></span>
* <span data-ttu-id="56818-122">Предоставляется [статистика использования](machine-learning-manage-new-webservice.md)веб-службы.</span><span class="sxs-lookup"><span data-stu-id="56818-122">Provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
* <span data-ttu-id="56818-123">Упрощается тестирование вызовов удаленных запросов машинного обучения Azure с использованием примеров данных.</span><span class="sxs-lookup"><span data-stu-id="56818-123">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
* <span data-ttu-id="56818-124">Предоставляется новая страница тестирования службы пакетного выполнения, на которой можно использовать примеры данных и журнал отправки заданий.</span><span class="sxs-lookup"><span data-stu-id="56818-124">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>

<span data-ttu-id="56818-125">Кроме того, обновлена студия машинного обучения. Теперь вы можете развертывать веб-службы с помощью новой модели или продолжать использовать классическую модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="56818-125">In addition, the Machine Learning Studio has been updated to allow you to deploy to the new Web service model or continue to deploy to the classic Web service model.</span></span> 

