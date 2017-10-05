---
title: "Преобразование данных XML с помощью преобразований в Azure Logic Apps | Документация Майкрософт"
description: "Создание преобразования или сопоставления для преобразования данных XML в разные форматы в приложениях логики с помощью пакета SDK для интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: fb6027769377b3527b11f7831dab3bb8d7061c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="f327d-103">Интеграция Enterprise с преобразованием данных XML</span><span class="sxs-lookup"><span data-stu-id="f327d-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="f327d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f327d-104">Overview</span></span>
<span data-ttu-id="f327d-105">В интеграции Enterprise используются соединитель преобразования, который позволяет преобразовывать данные из одного формата в другой.</span><span class="sxs-lookup"><span data-stu-id="f327d-105">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="f327d-106">Например, вы получили входящее сообщение, содержащее текущую дату в формате "ГодМесяцДень".</span><span class="sxs-lookup"><span data-stu-id="f327d-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="f327d-107">Вы хотите преобразовать эту дату в формат "МесяцДеньГод" с помощью преобразования.</span><span class="sxs-lookup"><span data-stu-id="f327d-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="f327d-108">Что делает преобразование?</span><span class="sxs-lookup"><span data-stu-id="f327d-108">What does a transform do?</span></span>
<span data-ttu-id="f327d-109">Преобразование, или сопоставление, состоит из исходной схемы XML (входных данных) и целевой схемы XML (выходных данных).</span><span class="sxs-lookup"><span data-stu-id="f327d-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="f327d-110">Вы можете использовать разные встроенные функции, помогающие работать с данными и управлять ими, включая действия со строками, условные назначения, арифметические выражения, модули форматирования даты и времени и даже циклические конструкции.</span><span class="sxs-lookup"><span data-stu-id="f327d-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="f327d-111">Как создать преобразование?</span><span class="sxs-lookup"><span data-stu-id="f327d-111">How to create a transform?</span></span>
<span data-ttu-id="f327d-112">Преобразование или карту можно создать с помощью [пакета SDK интеграции Enterprise](https://aka.ms/vsmapsandschemas)для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f327d-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="f327d-113">После создания и тестирования преобразования его можно передать в свою учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="f327d-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="f327d-114">Как использовать преобразование</span><span class="sxs-lookup"><span data-stu-id="f327d-114">How to use a transform</span></span>
<span data-ttu-id="f327d-115">После передачи преобразования или сопоставления в учетную запись интеграции их можно использовать для создания приложения логики.</span><span class="sxs-lookup"><span data-stu-id="f327d-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="f327d-116">Приложение логики выполняет преобразование всякий раз, когда оно активируется (и существует входное содержимое, которое необходимо преобразовать).</span><span class="sxs-lookup"><span data-stu-id="f327d-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="f327d-117">**Ниже приведены указания по использованию преобразования**.</span><span class="sxs-lookup"><span data-stu-id="f327d-117">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f327d-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f327d-118">Prerequisites</span></span>

* <span data-ttu-id="f327d-119">Создание учетной записи интеграции и добавление карты в нее</span><span class="sxs-lookup"><span data-stu-id="f327d-119">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="f327d-120">Теперь, когда предварительные требования выполнены, пора создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="f327d-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="f327d-121">Создайте приложение логики и [свяжите его с учетной записью интеграции](../logic-apps/logic-apps-enterprise-integration-accounts.md "Узнайте, как связать учетную запись интеграции с приложением логики"), содержащей карту.</span><span class="sxs-lookup"><span data-stu-id="f327d-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="f327d-122">Добавление триггера **запроса** в приложение логики</span><span class="sxs-lookup"><span data-stu-id="f327d-122">Add a **Request** trigger to your Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="f327d-123">Добавьте действие **Преобразовать XML**, щелкнув **Добавить действие** .</span><span class="sxs-lookup"><span data-stu-id="f327d-123">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="f327d-124">Введите слово *transform* в поле поиска, чтобы отфильтровать все действия и оставить только то, которое необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="f327d-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="f327d-125">Выберите действие **Преобразовать XML**.</span><span class="sxs-lookup"><span data-stu-id="f327d-125">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="f327d-126">Добавьте **содержимое** XML, которое будет преобразовано.</span><span class="sxs-lookup"><span data-stu-id="f327d-126">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="f327d-127">В качестве **содержимого** можно использовать любые данные XML, получаемые в HTTP-запросе.</span><span class="sxs-lookup"><span data-stu-id="f327d-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="f327d-128">В этом примере выберите текст HTTP-запроса, активировавшего приложение логики.</span><span class="sxs-lookup"><span data-stu-id="f327d-128">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>
7. <span data-ttu-id="f327d-129">Выберите имя **карты** , которую вы хотите использовать для преобразования.</span><span class="sxs-lookup"><span data-stu-id="f327d-129">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="f327d-130">Эта карта должна находиться в вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="f327d-130">The map must already be in your integration account.</span></span> <span data-ttu-id="f327d-131">На предыдущем шаге вы уже предоставили приложению логики доступ к своей учетной записи интеграции, содержащей карту.</span><span class="sxs-lookup"><span data-stu-id="f327d-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="f327d-132">Сохраните результаты своих действий.</span><span class="sxs-lookup"><span data-stu-id="f327d-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="f327d-133">На этом настройка карты завершена.</span><span class="sxs-lookup"><span data-stu-id="f327d-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="f327d-134">В случае реального приложения может потребоваться сохранить преобразованные данные в бизнес-приложении, например Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f327d-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="f327d-135">Можно легко добавить действие для отправки выходных данных преобразования в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f327d-135">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="f327d-136">Теперь можно проверить преобразование, выполнив запрос к конечной точке HTTP.</span><span class="sxs-lookup"><span data-stu-id="f327d-136">You can now test your transform by making a request to the HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="f327d-137">Функции и варианты использования</span><span class="sxs-lookup"><span data-stu-id="f327d-137">Features and use cases</span></span>
* <span data-ttu-id="f327d-138">Преобразование, создаваемое в сопоставлении, может быть простым, таким как копирование имени и адреса из одного документа в другой.</span><span class="sxs-lookup"><span data-stu-id="f327d-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="f327d-139">Но вы также можете создавать и более сложные преобразования с помощью встроенных операций сопоставления.</span><span class="sxs-lookup"><span data-stu-id="f327d-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="f327d-140">Многие операции или функции сопоставления легко доступны, включая строки, функции даты-времени и пр.</span><span class="sxs-lookup"><span data-stu-id="f327d-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="f327d-141">Можно выполнять прямое копирование данных между схемами.</span><span class="sxs-lookup"><span data-stu-id="f327d-141">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="f327d-142">В модуле сопоставления из пакета SDK сделать это так же просто, как нарисовать линию, соединяющую элементы в исходной схеме с соответствующими элементами в целевой схеме.</span><span class="sxs-lookup"><span data-stu-id="f327d-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="f327d-143">При создании сопоставления отображается его графическое представление, включая все созданные вами отношения и связи.</span><span class="sxs-lookup"><span data-stu-id="f327d-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="f327d-144">Используйте функцию тестирования сопоставления, чтобы добавить пример XML-сообщения.</span><span class="sxs-lookup"><span data-stu-id="f327d-144">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="f327d-145">Тогда одним щелчком вы сможете протестировать созданное сопоставление и увидеть полученный результат.</span><span class="sxs-lookup"><span data-stu-id="f327d-145">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="f327d-146">Передача существующих карт</span><span class="sxs-lookup"><span data-stu-id="f327d-146">Upload existing maps</span></span>  
* <span data-ttu-id="f327d-147">Включена поддержка формата XML.</span><span class="sxs-lookup"><span data-stu-id="f327d-147">Includes support for the XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="f327d-148">Подробнее</span><span class="sxs-lookup"><span data-stu-id="f327d-148">Learn more</span></span>
* [<span data-ttu-id="f327d-149">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="f327d-149">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise")  
* [<span data-ttu-id="f327d-150">Узнайте больше о картах</span><span class="sxs-lookup"><span data-stu-id="f327d-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Узнайте о картах интеграции Enterprise")  

