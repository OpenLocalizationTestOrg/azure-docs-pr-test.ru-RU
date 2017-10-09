---
title: "aaaManage логику приложений в Visual Studio — приложения логики Azure | Документы Microsoft"
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
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="d683a-103">Управление приложениями логики с помощью Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="d683a-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="d683a-104">Несмотря на то что hello [портал Azure](https://portal.azure.com/) предлагает отличный способ для вас toodesign и управлять Azure логику приложения, Visual Studio Cloud Explorer можно использовать для управления много ресурсов Azure, включая логику приложения.</span><span class="sxs-lookup"><span data-stu-id="d683a-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="d683a-105">Visual Studio Cloud Explorer позволяет просматривать, изменять и скачивать опубликованные приложения логики, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="d683a-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="d683a-106">К задачам управления относятся включение, отключение и просмотр журнала выполнения.</span><span class="sxs-lookup"><span data-stu-id="d683a-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="d683a-107">Чтобы иметь доступ к приложениям логики в Visual Studio и управлять ими, установите и настройте перечисленные ниже инструменты Visual Studio для Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="d683a-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d683a-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d683a-108">Prerequisites</span></span>

* <span data-ttu-id="d683a-109">[Visual Studio 2015 или Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="d683a-109">[Visual Studio 2015 or Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="d683a-110">[пакет Azure SDK последней версии](https://azure.microsoft.com/downloads/) (версия 2.9.1 или выше);</span><span class="sxs-lookup"><span data-stu-id="d683a-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="d683a-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="d683a-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="d683a-112">Web toohello доступ при использовании конструктора внедренные hello</span><span class="sxs-lookup"><span data-stu-id="d683a-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="d683a-113">Установка инструментов Visual Studio для приложений логики</span><span class="sxs-lookup"><span data-stu-id="d683a-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="d683a-114">После установки необходимых компонентов hello, загрузите и установите логику приложения hello Azure Tools для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d683a-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="d683a-115">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d683a-115">Open Visual Studio.</span></span> <span data-ttu-id="d683a-116">На hello **средства** последовательно выберите пункты **расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="d683a-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="d683a-117">Разверните hello **Online** категории, можно найти в Интернете в hello коллекции Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d683a-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="d683a-118">Найдите **средства Azure Logic Apps Tools для Visual Studio**. Если потребуется, выполните поиск по названию **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="d683a-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="d683a-119">toodownload и расширение hello установки, нажмите кнопку **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="d683a-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="d683a-120">После установки перезапустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d683a-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="d683a-121">hello toodownload инструментов приложения логики Azure для Visual Studio перейдите непосредственно, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="d683a-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="d683a-122">Поиск приложений логики в Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="d683a-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="d683a-123">tooopen Cloud Explorer на hello **представление** меню, выберите **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d683a-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="d683a-124">Найдите приложение логики, используя поиск по группе ресурсов или типу ресурса.</span><span class="sxs-lookup"><span data-stu-id="d683a-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="d683a-125">Если перейти от типа ресурса, выберите подписку Azure, разверните hello **Logic Apps** и выберите логику приложения.</span><span class="sxs-lookup"><span data-stu-id="d683a-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="d683a-126">Если перейти по группе ресурсов, разверните группу ресурсов hello, имеет логику приложения и выберите логику приложения.</span><span class="sxs-lookup"><span data-stu-id="d683a-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="d683a-127">команды tooview логику приложения, либо щелкните правой кнопкой мыши логику приложения или внизу hello Cloud Explorer, выберите пункт hello **действия** меню.</span><span class="sxs-lookup"><span data-stu-id="d683a-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![Поиск приложения логики](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="d683a-129">Изменение приложения логики с помощью конструктора приложений логики</span><span class="sxs-lookup"><span data-stu-id="d683a-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="d683a-130">Из Cloud Explorer можно открыть приложение развернутой логики в hello одного конструктора, используемого в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d683a-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="d683a-131">tooedit логику приложения, в Cloud Explorer, щелкните правой кнопкой мыши логику приложения и выберите **открыть с помощью редактора логику приложения**.</span><span class="sxs-lookup"><span data-stu-id="d683a-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="d683a-132">toopublish облако вашей toohello обновления, выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="d683a-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="d683a-133">Выберите новое выполнение toostart **запуска триггера**.</span><span class="sxs-lookup"><span data-stu-id="d683a-133">toostart a new run, choose **Run Trigger**.</span></span>

![Конструктор Logic Apps](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="d683a-135">В конструкторе hello, вы можете также **загрузки** приложения логики.</span><span class="sxs-lookup"><span data-stu-id="d683a-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="d683a-136">Это действие автоматически параметризует определение приложения логики hello и сохраняет определение hello в качестве шаблона развертывания диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d683a-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="d683a-137">Можно добавить этот проект группы ресурсов Azure tooyour шаблона развертывания.</span><span class="sxs-lookup"><span data-stu-id="d683a-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="d683a-138">Просмотр журнала выполнения приложения логики</span><span class="sxs-lookup"><span data-stu-id="d683a-138">Browse your logic app run history</span></span>

<span data-ttu-id="d683a-139">журнал приложения логики выполнения hello tooview логику приложения и выберите **открыть журнал выполнения**.</span><span class="sxs-lookup"><span data-stu-id="d683a-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="d683a-140">tooreorder историю выполнения на основе любого из заголовка столбца hello свойства отображается, выберите hello.</span><span class="sxs-lookup"><span data-stu-id="d683a-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![Журнал выполнения](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="d683a-142">журнал для экземпляра выполнения, что можно просмотреть результаты, включая hello входы и выходы на каждом этапе выполнения hello hello tooshow дважды щелкните одну из hello запуска экземпляров.</span><span class="sxs-lookup"><span data-stu-id="d683a-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![Результаты в журнале выполнения, входные и выходные данные по шагам](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="d683a-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d683a-144">Next steps</span></span>

* [<span data-ttu-id="d683a-145">Создание приложения логики</span><span class="sxs-lookup"><span data-stu-id="d683a-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* <span data-ttu-id="d683a-146">[Создание и развертывание приложений логики Azure в Visual Studio](logic-apps-deploy-from-vs.md).</span><span class="sxs-lookup"><span data-stu-id="d683a-146">[Design, build, and deploy logic apps in Visual Studio](logic-apps-deploy-from-vs.md)</span></span>
* [<span data-ttu-id="d683a-147">Примеры приложений логики и распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="d683a-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="d683a-148">Видео. Автоматизация бизнес-процессов с помощью Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d683a-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="d683a-149">Видео. Интеграция систем с Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d683a-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
