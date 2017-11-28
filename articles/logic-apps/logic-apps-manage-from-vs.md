---
title: "Управление приложениями логики в Visual Studio с помощью Azure Logic Apps | Документация Майкрософт"
description: "Узнайте, как управлять приложениями логики и другими ресурсами Azure с помощью Visual Studio с помощью Visual Studio Cloud Explorer."
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: a5bf24de1a7a2b6d4c1ae6416c95d83ef7506da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="db382-103">Управление приложениями логики с помощью Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="db382-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="db382-104">Хотя [портал Azure](https://portal.azure.com/) предоставляет отличный способ проектирования приложений логики Azure Logic Apps и управления ими, вы также можете использовать Visual Studio Cloud Explorer для управления многими ресурсами Azure, включая приложения логики.</span><span class="sxs-lookup"><span data-stu-id="db382-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="db382-105">Visual Studio Cloud Explorer позволяет просматривать, изменять и скачивать опубликованные приложения логики, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="db382-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="db382-106">К задачам управления относятся включение, отключение и просмотр журнала выполнения.</span><span class="sxs-lookup"><span data-stu-id="db382-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="db382-107">Чтобы иметь доступ к приложениям логики в Visual Studio и управлять ими, установите и настройте перечисленные ниже инструменты Visual Studio для Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="db382-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="db382-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="db382-108">Prerequisites</span></span>

* <span data-ttu-id="db382-109">[Visual Studio 2015 или Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="db382-109">[Visual Studio 2015 or Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="db382-110">[пакет Azure SDK последней версии](https://azure.microsoft.com/downloads/) (версия 2.9.1 или выше);</span><span class="sxs-lookup"><span data-stu-id="db382-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="db382-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="db382-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="db382-112">доступ к Интернету при использовании внедренного конструктора.</span><span class="sxs-lookup"><span data-stu-id="db382-112">Access to the web when using the embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="db382-113">Установка инструментов Visual Studio для приложений логики</span><span class="sxs-lookup"><span data-stu-id="db382-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="db382-114">После установки необходимых компонентов скачайте и установите инструменты Azure Logic Apps для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db382-114">After you install the prerequisites, download and install the Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="db382-115">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db382-115">Open Visual Studio.</span></span> <span data-ttu-id="db382-116">Откройте меню **Средства** и выберите пункт **Расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="db382-116">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="db382-117">Разверните категорию **В сети**, чтобы можно было выполнять онлайн-поиск в коллекции Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db382-117">Expand the **Online** category so you can search online in the Visual Studio Gallery.</span></span>
3. <span data-ttu-id="db382-118">Найдите **средства Azure Logic Apps Tools для Visual Studio**. Если потребуется, выполните поиск по названию **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="db382-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="db382-119">Нажмите кнопку **Скачать**, чтобы скачать и установить это расширение.</span><span class="sxs-lookup"><span data-stu-id="db382-119">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="db382-120">После установки перезапустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db382-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="db382-121">Чтобы скачать инструменты Azure Logic Apps для Visual Studio напрямую, перейдите в [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="db382-121">To download the Azure Logic Apps Tools for Visual Studio directly, go to the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="db382-122">Поиск приложений логики в Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="db382-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="db382-123">Чтобы открыть Cloud Explorer, в меню **Вид** выберите **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="db382-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="db382-124">Найдите приложение логики, используя поиск по группе ресурсов или типу ресурса.</span><span class="sxs-lookup"><span data-stu-id="db382-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="db382-125">При поиске по типу ресурса выберите подписку Azure, разверните раздел **Приложения логики** и выберите свое приложение.</span><span class="sxs-lookup"><span data-stu-id="db382-125">If you browse by resource type, select your Azure subscription, expand the **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="db382-126">При поиске по группе ресурсов разверните группу ресурсов, которая содержит ваше приложение логики, и выберите это приложение.</span><span class="sxs-lookup"><span data-stu-id="db382-126">If you browse by resource group, expand the resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="db382-127">Чтобы просмотреть команды для приложения логики, щелкните это приложение правой кнопкой мыши или воспользуйтесь меню **Действия** в нижней части Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="db382-127">To view commands for your logic app, either right-click your logic app, or at the bottom of Cloud Explorer, choose from the **Actions** menu.</span></span>

    ![Поиск приложения логики](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="db382-129">Изменение приложения логики с помощью конструктора приложений логики</span><span class="sxs-lookup"><span data-stu-id="db382-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="db382-130">Из Cloud Explorer можно открыть развернутое приложение логики в том же конструкторе, что и на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="db382-130">From Cloud Explorer, you can open a currently deployed logic app in the same designer that you use in the Azure portal.</span></span> 

* <span data-ttu-id="db382-131">Чтобы изменить приложение логики, в Cloud Explorer щелкните это приложение правой кнопкой мыши и выберите команду **Открыть в редакторе приложений логики**.</span><span class="sxs-lookup"><span data-stu-id="db382-131">To edit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="db382-132">Для публикации обновлений в облаке выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="db382-132">To publish your updates to the cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="db382-133">Чтобы запустить новое выполнение, выберите **Запустить триггер**.</span><span class="sxs-lookup"><span data-stu-id="db382-133">To start a new run, choose **Run Trigger**.</span></span>

![Конструктор Logic Apps](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="db382-135">Из конструктора также можно **скачать** приложение логики.</span><span class="sxs-lookup"><span data-stu-id="db382-135">From the designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="db382-136">Это действие автоматически параметризует определение приложения логики и сохраняет его как шаблон развертывания Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="db382-136">This action automatically parameterizes the logic app definition, and saves the definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="db382-137">Этот шаблон развертывания можно добавить в проект группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="db382-137">You can add this deployment template to your Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="db382-138">Просмотр журнала выполнения приложения логики</span><span class="sxs-lookup"><span data-stu-id="db382-138">Browse your logic app run history</span></span>

<span data-ttu-id="db382-139">Чтобы просмотреть журнал выполнения приложения логики, щелкните это приложение правой кнопкой мыши и выберите команду **Открыть журнал запусков**.</span><span class="sxs-lookup"><span data-stu-id="db382-139">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="db382-140">Чтобы упорядочить журнал выполнения по одному из отображаемых свойств, выберите соответствующий заголовок столбца.</span><span class="sxs-lookup"><span data-stu-id="db382-140">To reorder your run history based on any of the properties shown, select the column header.</span></span>

![Журнал выполнения](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="db382-142">Дважды щелкните один из экземпляров выполнения, чтобы отобразился журнал выполнения для этого экземпляра, где можно просмотреть результаты выполнения, включая входные и выходные данные каждого шага.</span><span class="sxs-lookup"><span data-stu-id="db382-142">To show the run history for an instance so you can review the run results, including the inputs and outputs from each step, double-click one of the run instances.</span></span>

![Результаты в журнале выполнения, входные и выходные данные по шагам](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="db382-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="db382-144">Next steps</span></span>

* [<span data-ttu-id="db382-145">Создание приложения логики</span><span class="sxs-lookup"><span data-stu-id="db382-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* <span data-ttu-id="db382-146">[Создание и развертывание приложений логики Azure в Visual Studio](logic-apps-deploy-from-vs.md).</span><span class="sxs-lookup"><span data-stu-id="db382-146">[Design, build, and deploy logic apps in Visual Studio](logic-apps-deploy-from-vs.md)</span></span>
* [<span data-ttu-id="db382-147">Примеры приложений логики и распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="db382-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="db382-148">Видео. Автоматизация бизнес-процессов с помощью Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="db382-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="db382-149">Видео. Интеграция систем с Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="db382-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
