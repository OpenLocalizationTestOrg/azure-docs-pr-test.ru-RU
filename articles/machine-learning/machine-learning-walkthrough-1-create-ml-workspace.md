---
title: "Шаг 1. Создание рабочей области машинного обучения | Документация Майкрософт"
description: "Шаг 1 из hello разработка прогнозирующего решения Пошаговое руководство: Узнайте, как tooset копирование новую рабочую область студии машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="f903f-103">Шаг 1. Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="f903f-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="f903f-104">Это первый шаг hello hello пошагового руководства, [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="f903f-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="f903f-105">**Создание рабочей области машинного обучения**</span><span class="sxs-lookup"><span data-stu-id="f903f-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="f903f-106">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="f903f-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="f903f-107">Создание нового эксперимента</span><span class="sxs-lookup"><span data-stu-id="f903f-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="f903f-108">Обучать и оценивать модели hello</span><span class="sxs-lookup"><span data-stu-id="f903f-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="f903f-109">Развернуть веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="f903f-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="f903f-110">Доступ к веб-службе hello</span><span class="sxs-lookup"><span data-stu-id="f903f-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="f903f-111">toouse студии машинного обучения, необходимо toohave рабочей области машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f903f-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="f903f-112">Эта рабочая область содержит hello средства toocreate, управлять и публиковать экспериментов.</span><span class="sxs-lookup"><span data-stu-id="f903f-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="f903f-113">Здравствуйте, администратор вашей подписки Azure требуется рабочая область toocreate hello и добавить вас в качестве владельца или участника.</span><span class="sxs-lookup"><span data-stu-id="f903f-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="f903f-114">Подробные сведения см. в статье [Создание рабочей области машинного обучения Azure и предоставление к ней общего доступа](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f903f-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="f903f-115">Создав рабочую область, откройте Студию машинного обучения ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="f903f-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="f903f-116">При наличии более чем одной рабочей области, можно выбрать hello рабочей области в панели инструментов hello в правом верхнем углу hello окна hello.</span><span class="sxs-lookup"><span data-stu-id="f903f-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Выбор рабочей области в Студии][2]

> [!TIP]
> <span data-ttu-id="f903f-118">Если были внесены владельца рабочей области hello, вы можете совместно использовать hello экспериментов, над которыми вы работаете с приглашение других пользователей toohello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f903f-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="f903f-119">Это можно сделать в студии машинного обучения на hello **параметры** страницы.</span><span class="sxs-lookup"><span data-stu-id="f903f-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="f903f-120">Необходимо просто hello учетную запись Майкрософт или организации для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="f903f-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="f903f-121">На hello **параметры** щелкните **пользователей**, нажмите кнопку **ПРИГЛАШЕНИЯ более пользователей** hello нижней части окна hello.</span><span class="sxs-lookup"><span data-stu-id="f903f-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="f903f-122">**Далее:[ отправка имеющихся данных](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="f903f-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
