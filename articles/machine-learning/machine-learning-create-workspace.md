---
title: "aaaCreate рабочей области машинного обучения | Документы Microsoft"
description: "Как toocreate в рабочую область для студии машинного обучения Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="54309-103">Создание рабочей области машинного обучения Azure и предоставление к ней общего доступа</span><span class="sxs-lookup"><span data-stu-id="54309-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="54309-104">Это меню связывает tootopics, которые описывают возможности tooset копирование hello различных средах обработки и анализа данных по использованию hello процесса Cortana аналитика (CAP).</span><span class="sxs-lookup"><span data-stu-id="54309-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="54309-105">toouse студии машинного обучения Azure, необходимо toohave рабочей области машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="54309-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="54309-106">Эта рабочая область содержит hello средства toocreate, управлять и публиковать экспериментов.</span><span class="sxs-lookup"><span data-stu-id="54309-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="54309-107">toocreate рабочей области</span><span class="sxs-lookup"><span data-stu-id="54309-107">toocreate a workspace</span></span>
1. <span data-ttu-id="54309-108">Войдите в toohello [портал Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="54309-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="54309-109">toosign в и создать рабочую область, необходимо toobe администратора подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="54309-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="54309-110">Щелкните **+Создать**.</span><span class="sxs-lookup"><span data-stu-id="54309-110">Click **+New**</span></span>

3. <span data-ttu-id="54309-111">Выберите **Аналитика**, щелкните **Рабочая область машинного обучения**, а затем — **Создать**.</span><span class="sxs-lookup"><span data-stu-id="54309-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="54309-112">Введите сведения о рабочей области.</span><span class="sxs-lookup"><span data-stu-id="54309-112">Enter your workspace information</span></span>

    - <span data-ttu-id="54309-113">Hello *имя рабочей области* может быть активным too260 символов, не заканчивается пробелом.</span><span class="sxs-lookup"><span data-stu-id="54309-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="54309-114">Hello имя не может содержать следующие символы:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="54309-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="54309-115">Hello *веб-службы план* вы выберите (или создайте), вместе с hello связанные *ценовой категории* выберите, используется при развертывании веб-служб из этой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="54309-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Создание рабочей области](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="54309-117">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="54309-117">Click **Create**</span></span>

<span data-ttu-id="54309-118">После развертывания hello рабочей области, можно открыть его в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="54309-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="54309-119">Обзор tooMachine Studio обучения на [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="54309-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="54309-120">Выберите рабочую область в верхнем правом углу hello.</span><span class="sxs-lookup"><span data-stu-id="54309-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![Выбор рабочей области](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="54309-122">Щелкните **my experiments** (Мои эксперименты).</span><span class="sxs-lookup"><span data-stu-id="54309-122">Click **my experiments**.</span></span>

    ![Открытие экспериментов](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="54309-124">Сведения об управлении рабочей областью см. в статье [Управление рабочей областью машинного обучения Azure](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="54309-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="54309-125">Если возникли проблемы при создании рабочей области в разделе [руководство по устранению неполадок: создать и присоединить рабочей области машинного обучения tooa](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="54309-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="54309-126">Предоставление общего доступа к рабочей области машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="54309-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="54309-127">После создания рабочей области машинного обучения, вы можете пригласить пользователей tooyour рабочей tooshare доступа tooyour рабочей области и все его экспериментов, наборы данных, портативные компьютеры, и т. д. Вы можете добавлять пользователей со следующими ролями:</span><span class="sxs-lookup"><span data-stu-id="54309-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="54309-128">**Пользователь** -рабочей области пользователя можно создать, открывать, изменять и удалять экспериментов, наборы данных, т. д., в рабочей области hello.</span><span class="sxs-lookup"><span data-stu-id="54309-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="54309-129">**Владелец** - владельца можно пригласить и удаление пользователей в рабочей области hello в toowhat Добавление пользователя можно сделать.</span><span class="sxs-lookup"><span data-stu-id="54309-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="54309-130">Hello учетной записи администратора, который создает hello рабочей toohello рабочей области автоматически добавляется в качестве владельца рабочей области.</span><span class="sxs-lookup"><span data-stu-id="54309-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="54309-131">Тем не менее, другие Администраторы или пользователи в том, что подписки не являются автоматически предоставил доступ рабочей toohello: требуется tooinvite их явно.</span><span class="sxs-lookup"><span data-stu-id="54309-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="54309-132">tooshare рабочей области</span><span class="sxs-lookup"><span data-stu-id="54309-132">tooshare a workspace</span></span>

1. <span data-ttu-id="54309-133">Войдите в tooMachine Studio обучения на [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="54309-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="54309-134">Hello левой панели щелкните **параметры**</span><span class="sxs-lookup"><span data-stu-id="54309-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="54309-135">Нажмите кнопку hello **пользователей** вкладка</span><span class="sxs-lookup"><span data-stu-id="54309-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="54309-136">Нажмите кнопку **ПРИГЛАШЕНИЯ более пользователей** hello нижней части страницы приветствия</span><span class="sxs-lookup"><span data-stu-id="54309-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Параметры Студии](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="54309-138">Укажите один или несколько адресов электронной почты.</span><span class="sxs-lookup"><span data-stu-id="54309-138">Enter one or more email addresses.</span></span> <span data-ttu-id="54309-139">Hello пользователям требуется допустимую учетную запись Майкрософт или учетная запись организации (из Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="54309-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="54309-140">Выберите пользователей hello tooadd владельцем или пользователя.</span><span class="sxs-lookup"><span data-stu-id="54309-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="54309-141">Нажмите кнопку hello **ОК** кнопку с галочкой.</span><span class="sxs-lookup"><span data-stu-id="54309-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="54309-142">Каждый пользователь получит сообщение электронной почты с инструкциями совместным использованием toosign в toohello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="54309-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="54309-143">Для возможности toodeploy toobe пользователей или управления веб-службами в этой рабочей области, они должны быть участника или администратора в hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="54309-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



