---
title: "aaaCustom код для приложения логики Azure с помощью функций Azure | Документы Microsoft"
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
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="70427-103">Добавление и выполнение пользовательского кода для приложений логики с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="70427-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="70427-104">фрагменты toorun C# или node.js в приложениях для логики, можно создать пользовательские функции с помощью функций Azure.</span><span class="sxs-lookup"><span data-stu-id="70427-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="70427-105">[Функции Azure](../azure-functions/functions-overview.md) позволяют производить в Microsoft Azure вычисления без использования серверов. Они полезны для выполнения следующих задач:</span><span class="sxs-lookup"><span data-stu-id="70427-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="70427-106">Расширенные функции форматирования или вычисления полей в приложениях логики.</span><span class="sxs-lookup"><span data-stu-id="70427-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="70427-107">Выполнение вычислений в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="70427-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="70427-108">Расширения функциональности приложения hello логики с функциями, которые поддерживаются в C# или node.js.</span><span class="sxs-lookup"><span data-stu-id="70427-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="70427-109">Создание пользовательских функций для приложений логики</span><span class="sxs-lookup"><span data-stu-id="70427-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="70427-110">Рекомендуется создать функцию на портале Azure функции hello из hello **универсального веб-перехватчика - узел** или **универсального веб-перехватчика - C#** шаблонов.</span><span class="sxs-lookup"><span data-stu-id="70427-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="70427-111">результат Hello создает заполняется автоматически шаблон, который принимает `application/json` из логики приложения.</span><span class="sxs-lookup"><span data-stu-id="70427-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="70427-112">Функции, создаваемые на основе этих шаблонов обнаруживаются автоматически и отображаются в hello конструктора логики приложения под **функции Azure в моем регионе.**</span><span class="sxs-lookup"><span data-stu-id="70427-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="70427-113">В hello в hello портала Azure **Интеграция** область функции шаблона должно отображаться **режим** значение слишком**веб-перехватчика** и **тип веб-перехватчика** задано слишком**универсального JSON**.</span><span class="sxs-lookup"><span data-stu-id="70427-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="70427-114">Функции веб-перехватчика принять запрос и передайте его в метод hello через `data` переменной.</span><span class="sxs-lookup"><span data-stu-id="70427-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="70427-115">Можно обратиться к свойствам hello объема полезных данных с помощью точечной нотации как `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="70427-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="70427-116">Например простую функцию JavaScript, которая преобразует значения даты и времени в строку даты выглядит как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="70427-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="70427-117">Вызов Функций Azure из приложений логики</span><span class="sxs-lookup"><span data-stu-id="70427-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="70427-118">контейнеры hello toolist из своей подписки и выберите hello функции, которые должны toocall в конструкторе логики приложения, нажмите кнопку hello **действия** меню и выберите его в **функции Azure в моем регионе**.</span><span class="sxs-lookup"><span data-stu-id="70427-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="70427-119">После выбора функции hello, задаваемые toospecify полезные данные входного объекта.</span><span class="sxs-lookup"><span data-stu-id="70427-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="70427-120">Этот объект является приветственное сообщение, отправляет toohello логику приложения функции hello и должен быть объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="70427-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="70427-121">Например, если вы хотите toopass в hello **последнее изменение** даты из триггера Salesforce полезные данные функции hello может выглядеть как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="70427-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![Дата последнего изменения][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="70427-123">Запуск приложения логики из функции</span><span class="sxs-lookup"><span data-stu-id="70427-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="70427-124">Приложение логики можно запустить из функции.</span><span class="sxs-lookup"><span data-stu-id="70427-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="70427-125">Ознакомьтесь со статьей [Приложения логики как вызываемые конечные точки](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="70427-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="70427-126">Создания логики приложения, которое содержит триггер вручную, а затем внутри функции, создать HTTP POST toohello триггер запуска вручную URL-адрес с полезными данными hello, будет отправлено toohello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="70427-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="70427-127">Создание функции из конструктора приложений логики</span><span class="sxs-lookup"><span data-stu-id="70427-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="70427-128">Также можно создать веб-перехватчика node.js функции из конструктора hello.</span><span class="sxs-lookup"><span data-stu-id="70427-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="70427-129">Для начала выберите раздел **Функции Azure в моем регионе** , а затем контейнер для своей функции.</span><span class="sxs-lookup"><span data-stu-id="70427-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="70427-130">Если у вас еще нет контейнер, необходимо toocreate один из hello [портала Azure функции](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="70427-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="70427-131">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="70427-131">Then select **Create New**.</span></span>  

<span data-ttu-id="70427-132">toogenerate шаблона, основанного на hello данных, что toocompute, укажите объект контекста hello планируется toopass в функцию.</span><span class="sxs-lookup"><span data-stu-id="70427-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="70427-133">Это должен быть объект JSON.</span><span class="sxs-lookup"><span data-stu-id="70427-133">This object must be a JSON object.</span></span> <span data-ttu-id="70427-134">Например если передать содержимое файла hello из операции FTP, полезные данные контекста hello выглядит следующим образом в этом примере.</span><span class="sxs-lookup"><span data-stu-id="70427-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![Полезные данные контекста][2]

> [!NOTE]
> <span data-ttu-id="70427-136">Так как этот объект не был приведен как строка, содержимое hello добавляется непосредственно toohello полезные данные JSON.</span><span class="sxs-lookup"><span data-stu-id="70427-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="70427-137">Тем не менее если объект hello не является маркер JSON (то есть, строка или JSON объект или массив) возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="70427-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="70427-138">toocast hello объекта в виде строки, добавляет кавычки, как показано на первом рисунке hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="70427-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="70427-139">Конструктор Hello затем приводит к возникновению ошибки, можно создавать встроенные функции-шаблона.</span><span class="sxs-lookup"><span data-stu-id="70427-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="70427-140">Переменные предварительно создаются на основе контекста hello планируется toopass в функции hello.</span><span class="sxs-lookup"><span data-stu-id="70427-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
