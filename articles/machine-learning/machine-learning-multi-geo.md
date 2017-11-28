---
title: "Географическая aaaMulti справочной документации | Документы Microsoft"
description: "Узнайте, как toocreate рабочей области и публикации веб-службы в регион Azure отличается от hello Юг центральной США (SCUS) регионе Azure."
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
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="82170-103">Справка по размещению в различных регионах</span><span class="sxs-lookup"><span data-stu-id="82170-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="82170-104">В этой статье описывается создание рабочей области и публикация веб-службы в других регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="82170-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="82170-105">Hello [Azure продукты по области страницы](https://azure.microsoft.com/en-us/regions/services/) список регионов, где находится машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="82170-105">hello [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="82170-106">Создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="82170-106">Create a workspace</span></span>
1. <span data-ttu-id="82170-107">Войдите в toohello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="82170-107">Sign in toohello Azure Classic Portal.</span></span>
2. <span data-ttu-id="82170-108">Щелкните **+ Создать** > **Службы данных** > **Машинное обучение** > **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="82170-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="82170-109">В списке **Расположение** выберите другой регион, например **Юго-Восточная Азия**.</span><span class="sxs-lookup"><span data-stu-id="82170-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="82170-110">![Справка по размещению в различных регионах, изображение 1][1]</span><span class="sxs-lookup"><span data-stu-id="82170-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="82170-111">Выберите рабочую область hello и нажмите кнопку **входа tooML Studio**.</span><span class="sxs-lookup"><span data-stu-id="82170-111">Select hello workspace, and then click **Sign-in tooML Studio**.</span></span>
   <span data-ttu-id="82170-112">![Справка по размещению в различных регионах, изображение 2][2]</span><span class="sxs-lookup"><span data-stu-id="82170-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="82170-113">Вы создали рабочую область в другом регионе, которую можно использовать наряду с другими рабочими областями.</span><span class="sxs-lookup"><span data-stu-id="82170-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="82170-114">tooswitch между рабочими областями вид toohello правой верхней части экрана.</span><span class="sxs-lookup"><span data-stu-id="82170-114">tooswitch among your workspaces, look toohello upper right of your screen.</span></span> <span data-ttu-id="82170-115">Щелкните раскрывающийся список hello, выберите hello региона и рабочей области выберите hello.</span><span class="sxs-lookup"><span data-stu-id="82170-115">Click hello dropdown, select hello region, and then select hello workspace.</span></span> <span data-ttu-id="82170-116">Все уже toohello локальной рабочей области.</span><span class="sxs-lookup"><span data-stu-id="82170-116">Everything is local toohello workspace region.</span></span>  <span data-ttu-id="82170-117">Например все вашего веб-службы, созданные из рабочей области, будут в hello одной рабочей области hello, расположенный в.</span><span class="sxs-lookup"><span data-stu-id="82170-117">For example, all of your web services created from a workspace will be in hello same region hello workspace is located in.</span></span>
   <span data-ttu-id="82170-118">![Справка по размещению в различных регионах, изображение 3][3]</span><span class="sxs-lookup"><span data-stu-id="82170-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="82170-119">Доступ к эксперименту из коллекции</span><span class="sxs-lookup"><span data-stu-id="82170-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="82170-120">При открытии эксперимент из коллекции, можно выбрать область, которая требуется toocopy hello эксперимента.</span><span class="sxs-lookup"><span data-stu-id="82170-120">If you open an experiment from Gallery, you can also select which region you want toocopy hello experiment to.</span></span>

![Справка по размещению в различных регионах, изображение 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="82170-122">Управление веб-службой</span><span class="sxs-lookup"><span data-stu-id="82170-122">Web service management</span></span>
<span data-ttu-id="82170-123">tooprogrammatically управление веб-служб, таких как для переустановки, использовать адрес конкретного региона hello:</span><span class="sxs-lookup"><span data-stu-id="82170-123">tooprogrammatically manage web services, such as for retraining, use hello region-specific address:</span></span>

* <span data-ttu-id="82170-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="82170-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="82170-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="82170-125">https://europewest.management.azureml.net</span></span>

### <a name="things-toonote"></a><span data-ttu-id="82170-126">Toonote действия</span><span class="sxs-lookup"><span data-stu-id="82170-126">Things toonote</span></span>
1. <span data-ttu-id="82170-127">Можно копировать только экспериментов между рабочих областей, которые принадлежат toohello одного региона таким образом.</span><span class="sxs-lookup"><span data-stu-id="82170-127">You can only copy experiments between workspaces that belong toohello same region this way.</span></span> <span data-ttu-id="82170-128">Если вам требуется toocopy эксперимента между областями в разных регионах, можно использовать hello [PowerShell](http://aka.ms/amlps) командлетов для [ *копирования AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="82170-128">If you need toocopy experiment across workspaces in different regions, you can use hello [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish that.</span></span> <span data-ttu-id="82170-129">Другое решение — toopublish hello эксперимента в коллекцию в режиме, отсутствующие в списке, а затем открыть его в рабочей области hello из hello другой области.</span><span class="sxs-lookup"><span data-stu-id="82170-129">Another workaround is toopublish hello experiment into Gallery in unlisted mode, then open it in hello workspace from hello other region.</span></span>
2. <span data-ttu-id="82170-130">Селектор Hello области будут отображаться только рабочих областей для одного региона одновременно.</span><span class="sxs-lookup"><span data-stu-id="82170-130">hello region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="82170-131">Бесплатные или гостевые (анонимные) рабочие области создаются и размещаются в юго-центральном регионе США.</span><span class="sxs-lookup"><span data-stu-id="82170-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="82170-132">Веб-службы, развертываемые из рабочей области, расположенной в Юго-Восточной Азии, также будут размещены в Юго-Восточной Азии.</span><span class="sxs-lookup"><span data-stu-id="82170-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="82170-133">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="82170-133">More information</span></span>
<span data-ttu-id="82170-134">Задать вопрос о hello [форум машинного обучения Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="82170-134">Ask a question on hello [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
