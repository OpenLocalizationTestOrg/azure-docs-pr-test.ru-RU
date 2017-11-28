---
title: "Применение пользовательского кода в Azure Logic Apps с помощью Функций Azure | Документация Майкрософт"
description: "Узнайте, как создавать и выполнять пользовательский код для Azure Logic Apps с помощью Функций Azure."
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18442c87b049200fac5ed41cc7034ba7a848b8d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="f6e4a-103">Добавление и выполнение пользовательского кода для приложений логики с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="f6e4a-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="f6e4a-104">Для выполнения пользовательских фрагментов кода C# или Node.js в приложениях логики можно с помощью Функций Azure создать пользовательские функции.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="f6e4a-105">[Функции Azure](../azure-functions/functions-overview.md) позволяют производить в Microsoft Azure вычисления без использования серверов. Они полезны для выполнения следующих задач:</span><span class="sxs-lookup"><span data-stu-id="f6e4a-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="f6e4a-106">Расширенные функции форматирования или вычисления полей в приложениях логики.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="f6e4a-107">Выполнение вычислений в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="f6e4a-108">Расширение функциональных возможностей приложения логики с помощью функций, поддерживаемых в C# или Node.js.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-108">Extend the logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="f6e4a-109">Создание пользовательских функций для приложений логики</span><span class="sxs-lookup"><span data-stu-id="f6e4a-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="f6e4a-110">Мы рекомендуем создавать новые функции на портале функций Azure с помощью шаблона **Generic Webhook - Node** или **Generic Webhook - C#**.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="f6e4a-111">В результате создается автоматически заполняемый шаблон, который принимает `application/json` из приложения логики.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="f6e4a-112">Функции, которые создаются из этих шаблонов, обнаруживаются автоматически и отображаются в конструкторе приложений логики в разделе **Azure Functions in my region** (Функции Azure в моем регионе).</span><span class="sxs-lookup"><span data-stu-id="f6e4a-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="f6e4a-113">На портале Azure в области **Интегрировать** функции для шаблона должен отображаться **Режим** **Веб-перехватчик**, а **Тип webhook** — **Generic JSON** (Универсальный JSON).</span><span class="sxs-lookup"><span data-stu-id="f6e4a-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span></span> 

<span data-ttu-id="f6e4a-114">Функции веб-перехватчика принимают запрос и передают его методу в виде переменной `data` .</span><span class="sxs-lookup"><span data-stu-id="f6e4a-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span></span> <span data-ttu-id="f6e4a-115">Для доступа к свойствам рабочей нагрузки можно использовать запись с точками типа `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="f6e4a-116">Вот пример простой функции JavaScript, которая преобразует значение DateTime в строку даты:</span><span class="sxs-lookup"><span data-stu-id="f6e4a-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="f6e4a-117">Вызов Функций Azure из приложений логики</span><span class="sxs-lookup"><span data-stu-id="f6e4a-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="f6e4a-118">Для перечисления контейнеров в подписке и выбора функции, которую необходимо вызвать, в конструкторе приложений логики щелкните меню **Действия** и выберите функцию из списка **Azure Functions in my Region** (Функции Azure в моем регионе).</span><span class="sxs-lookup"><span data-stu-id="f6e4a-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="f6e4a-119">После выбора функции вам будет предложено указать объект входных данных.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-119">After you select the function, you are asked to specify an input payload object.</span></span> <span data-ttu-id="f6e4a-120">Этот объект — сообщение, которое приложение логики передает функции и которое должно быть объектом в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-120">This object is the message that the logic app sends to the function and must be a JSON object.</span></span> <span data-ttu-id="f6e4a-121">Например, если вы хотите передать **дату последнего изменения** из триггера Salesforce, то полезные данные функции могут выглядеть как в этом примере:</span><span class="sxs-lookup"><span data-stu-id="f6e4a-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span></span>

![Дата последнего изменения][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="f6e4a-123">Запуск приложения логики из функции</span><span class="sxs-lookup"><span data-stu-id="f6e4a-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="f6e4a-124">Приложение логики можно запустить из функции.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="f6e4a-125">Ознакомьтесь со статьей [Приложения логики как вызываемые конечные точки](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="f6e4a-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="f6e4a-126">Создайте приложение логики с ручным триггером. Затем из функции создайте HTTP-запрос POST к URL-адресу ручного триггера, включающий полезные данные, которые нужно отправить в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="f6e4a-127">Создание функции из конструктора приложений логики</span><span class="sxs-lookup"><span data-stu-id="f6e4a-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="f6e4a-128">Функцию webhook node.js можно также создать из конструктора.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-128">You can also create a node.js webhook function from the designer.</span></span> <span data-ttu-id="f6e4a-129">Для начала выберите раздел **Функции Azure в моем регионе** , а затем контейнер для своей функции.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="f6e4a-130">Если у вас еще нет контейнера, его необходимо создать на [портале функций Azure](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="f6e4a-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="f6e4a-131">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-131">Then select **Create New**.</span></span>  

<span data-ttu-id="f6e4a-132">Чтобы создать шаблон на основе данных для вычисления, укажите объект контекста, который будет передан в функцию.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span></span> <span data-ttu-id="f6e4a-133">Это должен быть объект JSON.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-133">This object must be a JSON object.</span></span> <span data-ttu-id="f6e4a-134">Например, если передать содержимое файла из действия FTP, то полезные данные контекста будут выглядеть как в этом примере:</span><span class="sxs-lookup"><span data-stu-id="f6e4a-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span></span>

![Полезные данные контекста][2]

> [!NOTE]
> <span data-ttu-id="f6e4a-136">Поскольку для объекта не выполнялось приведение к строковому типу, содержимое добавляется непосредственно в полезные данные JSON.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span></span> <span data-ttu-id="f6e4a-137">Но если объект не является маркером JSON (т. е. строкой, объектом или массивом JSON), то возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="f6e4a-138">Чтобы преобразовать объект в строку, заключите его в кавычки, как показано на первом рисунке в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span></span>
> 

<span data-ttu-id="f6e4a-139">Затем конструктор создаст шаблон функции, который позволит создавать встроенные функции.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-139">The designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="f6e4a-140">Переменные создаются заранее в зависимости от содержимого, которое вы планируете передать в функцию.</span><span class="sxs-lookup"><span data-stu-id="f6e4a-140">Variables are pre-created based on the context that you plan to pass into the function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
