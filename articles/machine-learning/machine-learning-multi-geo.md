---
title: "Справка по размещению в различных регионах | Документация Майкрософт"
description: "Узнайте, как создать рабочую область и опубликовать веб-службу в регионе Azure, отличном от юго-центрального региона США."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="1ac62-103">Справка по размещению в различных регионах</span><span class="sxs-lookup"><span data-stu-id="1ac62-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="1ac62-104">В этой статье описывается создание рабочей области и публикация веб-службы в других регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="1ac62-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="1ac62-105">На [странице доступности продуктов Azure в разных регионах](https://azure.microsoft.com/en-us/regions/services/) содержится список регионов, в которых доступно Машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="1ac62-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="1ac62-106">Создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="1ac62-106">Create a workspace</span></span>
1. <span data-ttu-id="1ac62-107">Перейдите на классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1ac62-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="1ac62-108">Щелкните **+ Создать** > **Службы данных** > **Машинное обучение** > **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="1ac62-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="1ac62-109">В списке **Расположение** выберите другой регион, например **Юго-Восточная Азия**.</span><span class="sxs-lookup"><span data-stu-id="1ac62-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="1ac62-110">![Справка по размещению в различных регионах, изображение 1][1]</span><span class="sxs-lookup"><span data-stu-id="1ac62-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="1ac62-111">Выберите рабочую область и щелкните ссылку **Войти в Студию машинного обучения Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="1ac62-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="1ac62-112">![Справка по размещению в различных регионах, изображение 2][2]</span><span class="sxs-lookup"><span data-stu-id="1ac62-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="1ac62-113">Вы создали рабочую область в другом регионе, которую можно использовать наряду с другими рабочими областями.</span><span class="sxs-lookup"><span data-stu-id="1ac62-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="1ac62-114">Переключаться между рабочими областями можно с помощью элементов управления в правом верхнем углу экрана.</span><span class="sxs-lookup"><span data-stu-id="1ac62-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="1ac62-115">Щелкните раскрывающийся список, выберите регион, а затем выберите рабочую область.</span><span class="sxs-lookup"><span data-stu-id="1ac62-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="1ac62-116">Все ресурсы рабочей области относятся к одному региону.</span><span class="sxs-lookup"><span data-stu-id="1ac62-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="1ac62-117">Например, все веб-службы, созданные в рабочей области, будут размещены в том же регионе, что и рабочая область.</span><span class="sxs-lookup"><span data-stu-id="1ac62-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="1ac62-118">![Справка по размещению в различных регионах, изображение 3][3]</span><span class="sxs-lookup"><span data-stu-id="1ac62-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="1ac62-119">Доступ к эксперименту из коллекции</span><span class="sxs-lookup"><span data-stu-id="1ac62-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="1ac62-120">Открыв эксперимент из коллекции, вы сможете выбрать регион, в который нужно скопировать эксперимент.</span><span class="sxs-lookup"><span data-stu-id="1ac62-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Справка по размещению в различных регионах, изображение 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="1ac62-122">Управление веб-службой</span><span class="sxs-lookup"><span data-stu-id="1ac62-122">Web service management</span></span>
<span data-ttu-id="1ac62-123">Для программного управления веб-службами, например для повторного обучения, используйте адрес региона:</span><span class="sxs-lookup"><span data-stu-id="1ac62-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="1ac62-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="1ac62-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="1ac62-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="1ac62-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="1ac62-126">Примечания</span><span class="sxs-lookup"><span data-stu-id="1ac62-126">Things to note</span></span>
1. <span data-ttu-id="1ac62-127">Копировать эксперименты можно только между рабочими областями одного региона.</span><span class="sxs-lookup"><span data-stu-id="1ac62-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="1ac62-128">Если необходимо скопировать эксперимент между рабочими областями в разных регионах, то это можно сделать с помощью командлета [PowerShell](http://aka.ms/amlps) [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment).</span><span class="sxs-lookup"><span data-stu-id="1ac62-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="1ac62-129">Другим обходным решением является публикация эксперимента в коллекции в режиме без включения в список, а затем открытие его в рабочей области из другого региона.</span><span class="sxs-lookup"><span data-stu-id="1ac62-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="1ac62-130">В средстве выбора региона одновременно отображаются рабочие области только для одного региона.</span><span class="sxs-lookup"><span data-stu-id="1ac62-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="1ac62-131">Бесплатные или гостевые (анонимные) рабочие области создаются и размещаются в юго-центральном регионе США.</span><span class="sxs-lookup"><span data-stu-id="1ac62-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="1ac62-132">Веб-службы, развертываемые из рабочей области, расположенной в Юго-Восточной Азии, также будут размещены в Юго-Восточной Азии.</span><span class="sxs-lookup"><span data-stu-id="1ac62-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="1ac62-133">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="1ac62-133">More information</span></span>
<span data-ttu-id="1ac62-134">Задайте вопрос на [форуме по Машинному обучению Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="1ac62-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
