---
title: "aaaCreate, сборка и развертывание приложений логики в Visual Studio — приложения логики Azure | Документы Microsoft"
description: "Узнайте, как создавать проекты Visual Studio для проектирования, создания и развертывания приложений логики с помощью Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="71ec4-103">Проектирование, создание и развертывание приложений логики Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71ec4-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="71ec4-104">Несмотря на то что hello [портал Azure](https://portal.azure.com/) предлагает отличный способ для вас toocreate и управлять приложения логики Azure, можно использовать Visual Studio для проектирования, создания и развертывания приложений логики.</span><span class="sxs-lookup"><span data-stu-id="71ec4-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="71ec4-105">Visual Studio предоставляет широкие возможности средств, таких как hello конструктор логику приложения для вас toocreate логику приложения и настроить шаблоны развертывания и автоматизации развертывания tooany среды.</span><span class="sxs-lookup"><span data-stu-id="71ec4-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="71ec4-106">tooget работы с приложениями логики Azure, узнайте [как toocreate своего первого приложения логики в hello портал Azure](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="71ec4-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="71ec4-107">Шаги установки</span><span class="sxs-lookup"><span data-stu-id="71ec4-107">Installation steps</span></span>

<span data-ttu-id="71ec4-108">tooinstall и настройка средств Visual Studio для приложения логики Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="71ec4-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="71ec4-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="71ec4-109">Prerequisites</span></span>

* <span data-ttu-id="71ec4-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="71ec4-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="71ec4-111">[пакет Azure SDK последней версии](https://azure.microsoft.com/downloads/) (версия 2.9.1 или выше);</span><span class="sxs-lookup"><span data-stu-id="71ec4-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="71ec4-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="71ec4-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="71ec4-113">Web toohello доступ при использовании конструктора внедренные hello</span><span class="sxs-lookup"><span data-stu-id="71ec4-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="71ec4-114">Установка средств Visual Studio для Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="71ec4-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="71ec4-115">После установки необходимых компонентов hello:</span><span class="sxs-lookup"><span data-stu-id="71ec4-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="71ec4-116">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71ec4-116">Open Visual Studio.</span></span> <span data-ttu-id="71ec4-117">На hello **средства** последовательно выберите пункты **расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="71ec4-118">Разверните hello **Online** категории, можно найти в Интернете.</span><span class="sxs-lookup"><span data-stu-id="71ec4-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="71ec4-119">Найдите **средства Azure Logic Apps Tools для Visual Studio**. Если потребуется, выполните поиск по названию **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="71ec4-120">toodownload и расширение hello установки, нажмите кнопку **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="71ec4-121">После установки перезапустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71ec4-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="71ec4-122">Можно также загрузить [инструментов приложения логики Azure для Visual Studio 2017 г](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) и hello [инструментов приложения логики Azure для Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) непосредственно из Visual Studio Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="71ec4-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="71ec4-123">После завершения установки можно использовать hello проекта группы ресурсов Azure с помощью конструктора логики приложения.</span><span class="sxs-lookup"><span data-stu-id="71ec4-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="71ec4-124">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="71ec4-124">Create your project</span></span>

1. <span data-ttu-id="71ec4-125">На hello **файл** меню перейдите слишком**New**и выберите **проекта**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="71ec4-126">Или tooadd tooan вашего проекта, существующие решения go слишком**добавить**и выберите **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![Меню «Файл»](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="71ec4-128">В hello **новый проект** окна, найдите **облака**и выберите **группы ресурсов Azure**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="71ec4-129">Присвойте проекту имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-129">Name your project, and click **OK**.</span></span>

    ![Добавление нового проекта](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="71ec4-131">Выберите hello **приложения логики** шаблона, который создает шаблон развертывания приложения пустое логику для вас toouse.</span><span class="sxs-lookup"><span data-stu-id="71ec4-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="71ec4-132">Выбрав нужный шаблон, нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-132">After you select your template, click **OK**.</span></span>

    ![Выбор шаблона Logic App](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="71ec4-134">Теперь вы добавили решения tooyour логику приложения проекта.</span><span class="sxs-lookup"><span data-stu-id="71ec4-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="71ec4-135">В hello обозреватель решений файл развертывания должен отображаться.</span><span class="sxs-lookup"><span data-stu-id="71ec4-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![Файл развертывания](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="71ec4-137">Создание приложения логики с помощью конструктора приложений логики</span><span class="sxs-lookup"><span data-stu-id="71ec4-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="71ec4-138">При наличии проекта группы ресурсов Azure, содержащий приложение логики, можно открыть конструктор логику приложения hello в Visual Studio toocreate рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="71ec4-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="71ec4-139">Конструктор Hello требуется подключение к Интернету запроса слишком соединители для доступных свойств и данных.</span><span class="sxs-lookup"><span data-stu-id="71ec4-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="71ec4-140">Например при использовании соединитель Dynamics CRM Online hello hello конструктор запрашивает настраиваемый доступных tooshow экземпляра CRM и свойства по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="71ec4-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="71ec4-141">Щелкните правой кнопкой мыши файл `<template>.json` и выберите пункт **Открыть в конструкторе Logic App**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="71ec4-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="71ec4-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="71ec4-143">Выберите подписку Azure, группу ресурсов и расположение шаблона развертывания.</span><span class="sxs-lookup"><span data-stu-id="71ec4-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71ec4-144">При проектировании приложения логики будут создаваться ресурсы для подключения к API, которые используются для получения свойств.</span><span class="sxs-lookup"><span data-stu-id="71ec4-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="71ec4-145">Visual Studio использует эти подключения вашей toocreate группы выбранного ресурса во время разработки.</span><span class="sxs-lookup"><span data-stu-id="71ec4-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="71ec4-146">tooview или изменить любые соединения API, перейти toohello портал Azure и поиск **подключений API**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![Средство выбора подписки](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="71ec4-148">Конструктор Hello использует определения hello в hello `<template>.json` файл для подготовки к просмотру.</span><span class="sxs-lookup"><span data-stu-id="71ec4-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="71ec4-149">Создайте и подготовьте приложение логики.</span><span class="sxs-lookup"><span data-stu-id="71ec4-149">Create and design your logic app.</span></span> <span data-ttu-id="71ec4-150">Шаблон развертывания обновляется в соответствии со всеми вносимыми изменениями.</span><span class="sxs-lookup"><span data-stu-id="71ec4-150">Your deployment template is updated with your changes.</span></span>

    ![Конструктор Logic App в Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="71ec4-152">Visual Studio добавляет `Microsoft.Web/connections` слишком ресурс файла ресурсов для любых соединений логику приложению toofunction.</span><span class="sxs-lookup"><span data-stu-id="71ec4-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="71ec4-153">Эти свойства соединения можно задавать при развертывании и управлять после развертывания в **подключений API** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="71ec4-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="71ec4-154">Переключение tooJSON в представлении кода</span><span class="sxs-lookup"><span data-stu-id="71ec4-154">Switch tooJSON code view</span></span>

<span data-ttu-id="71ec4-155">hello tooshow JSON-представление для логики приложения, выберите hello **в представлении кода** вкладку внизу hello hello конструктора.</span><span class="sxs-lookup"><span data-stu-id="71ec4-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="71ec4-156">tooswitch обратно toohello ресурсов JSON, щелкните правой кнопкой мыши hello `<template>.json` правой кнопкой мыши и выберите **откройте**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="71ec4-157">Добавьте ссылки на зависимые ресурсы tooVisual Studio развертывания шаблонов</span><span class="sxs-lookup"><span data-stu-id="71ec4-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="71ec4-158">При необходимости вашего приложения логики tooreference зависимые ресурсы, можно использовать [функции шаблона Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) в шаблон развертывания логику приложения.</span><span class="sxs-lookup"><span data-stu-id="71ec4-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="71ec4-159">Например может потребоваться вашей tooreference приложения логики Azure функции или интеграции учетной записью, которую toodeploy вместе с логикой приложения.</span><span class="sxs-lookup"><span data-stu-id="71ec4-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="71ec4-160">Необходимо помнить о подготовке правильно toouse параметры в шаблон развертывания, который hello конструктор логику приложения.</span><span class="sxs-lookup"><span data-stu-id="71ec4-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="71ec4-161">Параметры приложений логики можно использовать в следующих типах триггеров и действий.</span><span class="sxs-lookup"><span data-stu-id="71ec4-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="71ec4-162">Дочерний рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="71ec4-162">Child workflow</span></span>
*   <span data-ttu-id="71ec4-163">Приложение-функция</span><span class="sxs-lookup"><span data-stu-id="71ec4-163">Function app</span></span>
*   <span data-ttu-id="71ec4-164">Вызов APIM</span><span class="sxs-lookup"><span data-stu-id="71ec4-164">APIM call</span></span>
*   <span data-ttu-id="71ec4-165">URL-адрес API среды выполнения</span><span class="sxs-lookup"><span data-stu-id="71ec4-165">API connection runtime URL</span></span>
*   <span data-ttu-id="71ec4-166">Путь для подключения к API.</span><span class="sxs-lookup"><span data-stu-id="71ec4-166">API connection path</span></span>

<span data-ttu-id="71ec4-167">Вы также можете использовать функции шаблонов: parameters, variables, resourceId, concat и т. п. Например Вот как можно заменить идентификатор ресурса Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="71ec4-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="71ec4-168">А так вы можете использовать параметры:</span><span class="sxs-lookup"><span data-stu-id="71ec4-168">And where you would use parameters:</span></span>

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
<span data-ttu-id="71ec4-169">В качестве другого примера можно параметризовать hello сообщение операции отправки служебной шины:</span><span class="sxs-lookup"><span data-stu-id="71ec4-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> <span data-ttu-id="71ec4-170">Параметр host.runtimeUrl является необязательным, его можно удалить из шаблона.</span><span class="sxs-lookup"><span data-stu-id="71ec4-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="71ec4-171">Для toowork конструктор логику приложения hello при использовании параметров, необходимо предоставить значения по умолчанию, например:</span><span class="sxs-lookup"><span data-stu-id="71ec4-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="71ec4-172">Сохранение приложения логики</span><span class="sxs-lookup"><span data-stu-id="71ec4-172">Save your logic app</span></span>

<span data-ttu-id="71ec4-173">go логику приложения в любое время, toosave слишком**файл** > **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="71ec4-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="71ec4-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="71ec4-175">Если логика приложения все ошибки при сохранении свое приложение, они отображаются в Visual Studio hello **выходов** окна.</span><span class="sxs-lookup"><span data-stu-id="71ec4-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="71ec4-176">Развертывание приложения логики из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71ec4-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="71ec4-177">Когда настройка приложения логики будет завершена, вы можете развернуть его, выполнив несколько простых действий напрямую из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71ec4-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="71ec4-178">В обозревателе решений щелкните правой кнопкой мыши проект и перейдите в слишком**развернуть** > **новое развертывание...**</span><span class="sxs-lookup"><span data-stu-id="71ec4-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![Новое развертывание](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="71ec4-180">Если появится запрос, может входить в tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="71ec4-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="71ec4-181">Теперь необходимо выбрать hello сведений для группы ресурсов hello место toodeploy логику приложения.</span><span class="sxs-lookup"><span data-stu-id="71ec4-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="71ec4-182">Закончив, щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71ec4-183">Убедитесь, что выбран правильный шаблон hello и файл параметров для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="71ec4-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="71ec4-184">Например toodeploy tooa рабочей среде следует выберите файл параметров рабочей hello.</span><span class="sxs-lookup"><span data-stu-id="71ec4-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![Развертывание группы tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="71ec4-186">отображается состояние развертывания Hello hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="71ec4-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="71ec4-187">Возможно, tooselect **подготовки Azure** в hello **Показать выходные данные от** списка.</span><span class="sxs-lookup"><span data-stu-id="71ec4-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![Вывод информации о состоянии развертывания](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="71ec4-189">В будущем hello можно изменить логику приложения в системе управления версиями и использовать Visual Studio toodeploy новых версий.</span><span class="sxs-lookup"><span data-stu-id="71ec4-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="71ec4-190">Если непосредственно изменить определение hello в hello портал Azure, эти изменения будут перезаписаны при развертывании из Visual Studio следующий раз.</span><span class="sxs-lookup"><span data-stu-id="71ec4-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="71ec4-191">Добавьте существующий проект группы ресурсов логику приложения tooan</span><span class="sxs-lookup"><span data-stu-id="71ec4-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="71ec4-192">При наличии существующего проекта группы ресурсов, можно добавить в окне структуры JSON hello проекта toothat логику приложения.</span><span class="sxs-lookup"><span data-stu-id="71ec4-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="71ec4-193">Можно также добавить другое приложение логики, наряду с приложение hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="71ec4-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="71ec4-194">Откройте hello `<template>.json` файла.</span><span class="sxs-lookup"><span data-stu-id="71ec4-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="71ec4-195">hello tooopen окно структуры JSON go слишком**представление** > **другие окна** > **структуры JSON**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="71ec4-196">Щелкните файл шаблона ресурсов toohello tooadd **добавить ресурс** hello верхней части окна hello структуры JSON.</span><span class="sxs-lookup"><span data-stu-id="71ec4-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="71ec4-197">Или щелкните правой кнопкой мыши в окне структуры JSON hello **ресурсов**и выберите **добавить новый ресурс**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Окно "Структура JSON"](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="71ec4-199">В hello **добавить ресурс** диалоговое окно, найдите и выберите **приложения логики**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="71ec4-200">Присвойте имя приложению логики и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="71ec4-200">Name your logic app, and choose **Add**.</span></span>

    ![Добавление ресурса](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="71ec4-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="71ec4-202">Next Steps</span></span>

* [<span data-ttu-id="71ec4-203">Управление Logic Apps с помощью Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="71ec4-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="71ec4-204">Примеры приложений логики и распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="71ec4-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="71ec4-205">Узнайте, как tooautomate business обрабатывает с приложениями логики Azure</span><span class="sxs-lookup"><span data-stu-id="71ec4-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="71ec4-206">Узнайте, как toointegrate системах с логикой приложения Azure</span><span class="sxs-lookup"><span data-stu-id="71ec4-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
