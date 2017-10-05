---
title: "Создание рабочей области машинного обучения | Документация Майкрософт"
description: "Создание рабочей области для Студии машинного обучения Azure"
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
ms.openlocfilehash: 182a34822e71d63f4d7229548ae3f59d9f195337
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="aa248-103">Создание рабочей области машинного обучения Azure и предоставление к ней общего доступа</span><span class="sxs-lookup"><span data-stu-id="aa248-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="aa248-104">Это меню содержит ссылки на разделы, описывающие настройку различных сред обработки и анализа данных, используемых процессом Cortana Analytics (CAP).</span><span class="sxs-lookup"><span data-stu-id="aa248-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="aa248-105">Для использования Студии машинного обучения Azure требуется рабочая область машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="aa248-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span></span> <span data-ttu-id="aa248-106">Такая рабочая область содержит инструменты, необходимые для создания, публикации экспериментов и управления ими.</span><span class="sxs-lookup"><span data-stu-id="aa248-106">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="to-create-a-workspace"></a><span data-ttu-id="aa248-107">Создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="aa248-107">To create a workspace</span></span>
1. <span data-ttu-id="aa248-108">Войдите на [портал Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="aa248-108">Sign in to the [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="aa248-109">Чтобы войти и создать рабочую область, требуются права администратора подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="aa248-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="aa248-110">Щелкните **+Создать**.</span><span class="sxs-lookup"><span data-stu-id="aa248-110">Click **+New**</span></span>

3. <span data-ttu-id="aa248-111">Выберите **Аналитика**, щелкните **Рабочая область машинного обучения**, а затем — **Создать**.</span><span class="sxs-lookup"><span data-stu-id="aa248-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="aa248-112">Введите сведения о рабочей области.</span><span class="sxs-lookup"><span data-stu-id="aa248-112">Enter your workspace information</span></span>

    - <span data-ttu-id="aa248-113">*Имя рабочей области* может содержать до 260 символов и не должно заканчиваться пробелом.</span><span class="sxs-lookup"><span data-stu-id="aa248-113">The *workspace name* may be up to 260 characters, not ending in a space.</span></span> <span data-ttu-id="aa248-114">Оно не может содержать следующие символы: `< > * % & : \ ? + /`.</span><span class="sxs-lookup"><span data-stu-id="aa248-114">The name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="aa248-115">Выбранный (или созданный) *план веб-службы* и связанная *ценовая категория* используются при развертывании веб-служб из этой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="aa248-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Создание рабочей области](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="aa248-117">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="aa248-117">Click **Create**</span></span>

<span data-ttu-id="aa248-118">После развертывания рабочей области вы можете открыть Студию машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="aa248-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="aa248-119">Перейдите в Студию машинного обучения, щелкнув ссылку [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="aa248-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="aa248-120">В правом верхнем углу выберите рабочую область.</span><span class="sxs-lookup"><span data-stu-id="aa248-120">Select your workspace in the upper-right-hand corner.</span></span>

    ![Выбор рабочей области](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="aa248-122">Щелкните **my experiments** (Мои эксперименты).</span><span class="sxs-lookup"><span data-stu-id="aa248-122">Click **my experiments**.</span></span>

    ![Открытие экспериментов](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="aa248-124">Сведения об управлении рабочей областью см. в статье [Управление рабочей областью машинного обучения Azure](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="aa248-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="aa248-125">Если при создании рабочей области возникли какие-либо проблемы, см. сведения в [руководстве по устранению неполадок, связанных с созданием рабочей области машинного обучения и подключением к ней](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="aa248-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="aa248-126">Предоставление общего доступа к рабочей области машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="aa248-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="aa248-127">После создания рабочей области машинного обучения вы можете приглашать в нее пользователей, предоставляя общий доступ к области и всем ее экспериментам, наборам данных, записным книжкам и т. д. Вы можете добавлять пользователей со следующими ролями:</span><span class="sxs-lookup"><span data-stu-id="aa248-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="aa248-128">**Пользователь.** Пользователь рабочей области может создавать, открывать, изменять и удалять наборы данных, эксперименты и т. д. в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="aa248-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span></span>
* <span data-ttu-id="aa248-129">**Владелец.** Владелец может приглашать и удалять пользователей рабочей области, а также управлять доступными пользователям действиями.</span><span class="sxs-lookup"><span data-stu-id="aa248-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="aa248-130">Учетная запись администратора, создающего рабочую область, автоматически добавляется в качестве владельца.</span><span class="sxs-lookup"><span data-stu-id="aa248-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span></span> <span data-ttu-id="aa248-131">Но другим администраторам или пользователям в этой подписке автоматически не предоставляется доступ к рабочей области. Их необходимо пригласить явным образом.</span><span class="sxs-lookup"><span data-stu-id="aa248-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span></span>
> 
> 

### <a name="to-share-a-workspace"></a><span data-ttu-id="aa248-132">Предоставление общего доступа к рабочей области</span><span class="sxs-lookup"><span data-stu-id="aa248-132">To share a workspace</span></span>

1. <span data-ttu-id="aa248-133">Войдите в Студию машинного обучения, щелкнув ссылку [https://studio.azureml.net/Home](https://studio.azureml.net/Home).</span><span class="sxs-lookup"><span data-stu-id="aa248-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="aa248-134">На панели слева щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="aa248-134">In the left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="aa248-135">Откройте вкладку **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="aa248-135">Click the **USERS** tab</span></span>

4. <span data-ttu-id="aa248-136">В нижней части страницы щелкните **Invite more users** (Пригласить больше пользователей).</span><span class="sxs-lookup"><span data-stu-id="aa248-136">Click **INVITE MORE USERS** at the bottom of the page</span></span>

    ![Параметры Студии](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="aa248-138">Укажите один или несколько адресов электронной почты.</span><span class="sxs-lookup"><span data-stu-id="aa248-138">Enter one or more email addresses.</span></span> <span data-ttu-id="aa248-139">У пользователя должна быть действующая учетная запись Майкрософт или учетная запись организации (из Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="aa248-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="aa248-140">Выберите, с какими правами вы хотите добавить пользователей: владельца или пользователя.</span><span class="sxs-lookup"><span data-stu-id="aa248-140">Select whether you want to add the users as Owner or User.</span></span>

7. <span data-ttu-id="aa248-141">Щелкните значок флажка **ОК**.</span><span class="sxs-lookup"><span data-stu-id="aa248-141">Click the **OK** checkmark button.</span></span>

<span data-ttu-id="aa248-142">Каждый добавленный пользователь получит сообщение по электронной почте с инструкциями по входу в общую рабочую область.</span><span class="sxs-lookup"><span data-stu-id="aa248-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="aa248-143">Чтобы пользователи могли развертывать веб-службы и управлять ими в этой рабочей области, они должны быть участниками или администраторами подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="aa248-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span></span> 



