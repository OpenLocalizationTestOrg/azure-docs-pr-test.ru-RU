---
title: "aaaConvert XML-данных с преобразованиями - приложения логики Azure | Документы Microsoft"
description: "Создание преобразования или mapps tooconvert XML-данные между форматами в приложениях для логики с помощью hello SDK интеграции Enterprise"
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
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="a75f1-103">Интеграция Enterprise с преобразованием данных XML</span><span class="sxs-lookup"><span data-stu-id="a75f1-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="a75f1-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a75f1-104">Overview</span></span>
<span data-ttu-id="a75f1-105">Соединитель преобразования интеграции Enterprise Hello преобразует данные из одного формата tooanother формат.</span><span class="sxs-lookup"><span data-stu-id="a75f1-105">hello Enterprise integration Transform connector converts data from one format tooanother format.</span></span> <span data-ttu-id="a75f1-106">Например имеется входящее сообщение, которое содержит текущую дату в формате YearMonthDay hello hello.</span><span class="sxs-lookup"><span data-stu-id="a75f1-106">For example, you may have an incoming message that contains hello current date in hello YearMonthDay format.</span></span> <span data-ttu-id="a75f1-107">Можно использовать преобразование tooreformat hello даты toobe в формате MonthDayYear hello.</span><span class="sxs-lookup"><span data-stu-id="a75f1-107">You can use a transform tooreformat hello date toobe in hello MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="a75f1-108">Что делает преобразование?</span><span class="sxs-lookup"><span data-stu-id="a75f1-108">What does a transform do?</span></span>
<span data-ttu-id="a75f1-109">Преобразования, который также называется карты, состоит из источника XML-схемы (hello входных данных) и целевой XML-схемы (hello выходных данных).</span><span class="sxs-lookup"><span data-stu-id="a75f1-109">A Transform, which is also known as a map, consists of a Source XML schema (hello input) and a Target XML schema (hello output).</span></span> <span data-ttu-id="a75f1-110">Можно использовать различные встроенные функции toohelp управления или управления hello данных, включая обработку строк, условного назначения, арифметические выражения, модули форматирования даты времени и даже циклические конструкции.</span><span class="sxs-lookup"><span data-stu-id="a75f1-110">You can use different built-in functions toohelp manipulate or control hello data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-toocreate-a-transform"></a><span data-ttu-id="a75f1-111">Как toocreate преобразование?</span><span class="sxs-lookup"><span data-stu-id="a75f1-111">How toocreate a transform?</span></span>
<span data-ttu-id="a75f1-112">Преобразование или карты можно создать с помощью Visual Studio hello [SDK интеграции Enterprise](https://aka.ms/vsmapsandschemas).</span><span class="sxs-lookup"><span data-stu-id="a75f1-112">You can create a transform/map by using hello Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="a75f1-113">После завершения создания и тестирования hello преобразования, преобразования hello загрузки в вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="a75f1-113">When you are finished creating and testing hello transform, you upload hello transform into your integration account.</span></span> 

## <a name="how-toouse-a-transform"></a><span data-ttu-id="a75f1-114">Как toouse преобразования</span><span class="sxs-lookup"><span data-stu-id="a75f1-114">How toouse a transform</span></span>
<span data-ttu-id="a75f1-115">После преобразования hello/map передать в учетную запись интеграции, его можно использовать toocreate приложения логики.</span><span class="sxs-lookup"><span data-stu-id="a75f1-115">After you upload hello transform/map into your integration account, you can use it toocreate a Logic app.</span></span> <span data-ttu-id="a75f1-116">приложение Hello логика выполняет преобразования всякий раз, когда запускается приложение hello логики (существует входного содержимого, которое требуется преобразовать toobe).</span><span class="sxs-lookup"><span data-stu-id="a75f1-116">hello Logic app runs your transformations whenever hello Logic app is triggered (and there is input content that needs toobe transformed).</span></span>

<span data-ttu-id="a75f1-117">**Ниже приведены шаги toouse hello преобразования**:</span><span class="sxs-lookup"><span data-stu-id="a75f1-117">**Here are hello steps toouse a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a75f1-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a75f1-118">Prerequisites</span></span>

* <span data-ttu-id="a75f1-119">Создайте учетную запись интеграции и добавьте tooit карты</span><span class="sxs-lookup"><span data-stu-id="a75f1-119">Create an integration account and add a map tooit</span></span>  

<span data-ttu-id="a75f1-120">Теперь, когда вы занимается hello предварительные требования, это время toocreate логику приложения:</span><span class="sxs-lookup"><span data-stu-id="a75f1-120">Now that you've taken care of hello prerequisites, it's time toocreate your Logic app:</span></span>  

1. <span data-ttu-id="a75f1-121">Создание приложения логики и [связать его учетной записи интеграции tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md "узнать toolink tooa логики интеграции учетной записи приложения") , содержащий hello карты.</span><span class="sxs-lookup"><span data-stu-id="a75f1-121">Create a Logic app and [link it tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that contains hello map.</span></span>
2. <span data-ttu-id="a75f1-122">Добавить **запроса** приложения логики триггера tooyour</span><span class="sxs-lookup"><span data-stu-id="a75f1-122">Add a **Request** trigger tooyour Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="a75f1-123">Добавить hello **преобразование XML** действия путем выбора **добавить действие** </span><span class="sxs-lookup"><span data-stu-id="a75f1-123">Add hello **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="a75f1-124">Введите слово hello *преобразование* в toofilter поле поиска hello все hello один toohello действия, которые должны toouse</span><span class="sxs-lookup"><span data-stu-id="a75f1-124">Enter hello word *transform* in hello search box toofilter all hello actions toohello one that you want toouse</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="a75f1-125">Выберите hello **преобразование XML** действие</span><span class="sxs-lookup"><span data-stu-id="a75f1-125">Select hello **Transform XML** action</span></span>   
6. <span data-ttu-id="a75f1-126">Добавить hello XML **СОДЕРЖИМОГО** , необходимо преобразование.</span><span class="sxs-lookup"><span data-stu-id="a75f1-126">Add hello XML **CONTENT** that you transform.</span></span> <span data-ttu-id="a75f1-127">Можно использовать любой XML-данных, появляется в запросе hello HTTP как hello **СОДЕРЖИМОГО**.</span><span class="sxs-lookup"><span data-stu-id="a75f1-127">You can use any XML data you receive in hello HTTP request as hello **CONTENT**.</span></span> <span data-ttu-id="a75f1-128">В этом примере выберите текст hello hello HTTP-запроса, запустившего приложение hello логику.</span><span class="sxs-lookup"><span data-stu-id="a75f1-128">In this example, select hello body of hello HTTP request that triggered hello Logic app.</span></span>
7. <span data-ttu-id="a75f1-129">Выберите hello имя hello **КАРТЫ** нужных toouse tooperform hello преобразования.</span><span class="sxs-lookup"><span data-stu-id="a75f1-129">Select hello name of hello **MAP** that you want toouse tooperform hello transformation.</span></span> <span data-ttu-id="a75f1-130">карта Hello должен быть в вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="a75f1-130">hello map must already be in your integration account.</span></span> <span data-ttu-id="a75f1-131">На предыдущем шаге вы дали уже учетной интеграции tooyour доступа логики приложения, содержащий схему.</span><span class="sxs-lookup"><span data-stu-id="a75f1-131">In an earlier step, you already gave your Logic app access tooyour integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="a75f1-132">Сохраните результаты своих действий.</span><span class="sxs-lookup"><span data-stu-id="a75f1-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="a75f1-133">На этом настройка карты завершена.</span><span class="sxs-lookup"><span data-stu-id="a75f1-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="a75f1-134">В реальных приложениях вы можете toostore hello преобразования данных в бизнес-приложения, таких как SalesForce.</span><span class="sxs-lookup"><span data-stu-id="a75f1-134">In a real world application, you may want toostore hello transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="a75f1-135">Можно легко, как выходные данные hello toosend действие hello преобразовывать tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="a75f1-135">You can easily as an action toosend hello output of hello transform tooSalesforce.</span></span> 

<span data-ttu-id="a75f1-136">Теперь можно проверить преобразование, делая конечную точку HTTP toohello запроса.</span><span class="sxs-lookup"><span data-stu-id="a75f1-136">You can now test your transform by making a request toohello HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="a75f1-137">Функции и варианты использования</span><span class="sxs-lookup"><span data-stu-id="a75f1-137">Features and use cases</span></span>
* <span data-ttu-id="a75f1-138">Преобразование Hello, созданные на карте могут быть простыми, например для копирования из одного документа tooanother имя и адрес.</span><span class="sxs-lookup"><span data-stu-id="a75f1-138">hello transformation created in a map can be simple, such as copying a name and address from one document tooanother.</span></span> <span data-ttu-id="a75f1-139">Также можно создавать более сложные преобразования, использование операций сопоставления out of box hello.</span><span class="sxs-lookup"><span data-stu-id="a75f1-139">Or, you can create more complex transformations using hello out-of-the-box map operations.</span></span>  
* <span data-ttu-id="a75f1-140">Многие операции или функции сопоставления легко доступны, включая строки, функции даты-времени и пр.</span><span class="sxs-lookup"><span data-stu-id="a75f1-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="a75f1-141">Это можно сделать копию прямой данных между схемами hello.</span><span class="sxs-lookup"><span data-stu-id="a75f1-141">You can do a direct data copy between hello schemas.</span></span> <span data-ttu-id="a75f1-142">В hello сопоставления, включенный в пакет SDK для hello это просто рисования линии, соединяющей hello элементов в исходной схеме hello их аналогами в целевой схеме hello.</span><span class="sxs-lookup"><span data-stu-id="a75f1-142">In hello Mapper included in hello SDK, this is as simple as drawing a line that connects hello elements in hello source schema with their counterparts in hello destination schema.</span></span>  
* <span data-ttu-id="a75f1-143">При создании карты, можно просмотреть графическое представление hello карты, которая показывает все отношения hello и ссылки, создаваемые вами.</span><span class="sxs-lookup"><span data-stu-id="a75f1-143">When creating a map, you view a graphical representation of hello map, which shows all hello relationships and links you create.</span></span>
* <span data-ttu-id="a75f1-144">Используйте tooadd функции hello тестового сопоставления пример XML-сообщения.</span><span class="sxs-lookup"><span data-stu-id="a75f1-144">Use hello Test Map feature tooadd a sample XML message.</span></span> <span data-ttu-id="a75f1-145">С одним щелчком мыши можно проверить hello карты вы создали и увидеть результаты созданных hello.</span><span class="sxs-lookup"><span data-stu-id="a75f1-145">With a simple click, you can test hello map you created, and see hello generated output.</span></span>  
* <span data-ttu-id="a75f1-146">Передача существующих карт</span><span class="sxs-lookup"><span data-stu-id="a75f1-146">Upload existing maps</span></span>  
* <span data-ttu-id="a75f1-147">Включает поддержку hello XML-формате.</span><span class="sxs-lookup"><span data-stu-id="a75f1-147">Includes support for hello XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="a75f1-148">Подробнее</span><span class="sxs-lookup"><span data-stu-id="a75f1-148">Learn more</span></span>
* [<span data-ttu-id="a75f1-149">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="a75f1-149">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")  
* [<span data-ttu-id="a75f1-150">Узнайте больше о картах</span><span class="sxs-lookup"><span data-stu-id="a75f1-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Узнайте о картах интеграции Enterprise")  

