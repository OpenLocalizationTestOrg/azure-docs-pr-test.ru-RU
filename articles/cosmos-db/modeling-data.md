---
title: "данные документа aaaModeling базы данных NoSQL | Документы Microsoft"
description: "Подробно о моделировании данных для баз данных NoSQL"
keywords: "моделирование данных"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="5e216-104">Моделирование данных документов для базы данных NoSQL</span><span class="sxs-lookup"><span data-stu-id="5e216-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="5e216-105">Пока без схемы базах данных, таких как Azure Cosmos DB, легко super tooembrace изменения tooyour используемой модели данных по-прежнему необходимо потратить некоторое время думать о данных.</span><span class="sxs-lookup"><span data-stu-id="5e216-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="5e216-106">Как происходит toobe хранимых данных?</span><span class="sxs-lookup"><span data-stu-id="5e216-106">How is data going toobe stored?</span></span> <span data-ttu-id="5e216-107">Как обеспечивается непрерывная tooretrieve и запроса данных приложения?</span><span class="sxs-lookup"><span data-stu-id="5e216-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="5e216-108">Ориентировано ли ваше приложение на запись или на чтение?</span><span class="sxs-lookup"><span data-stu-id="5e216-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="5e216-109">После считывания в этой статье, можно будет tooanswer hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="5e216-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="5e216-110">Как следует представлять документ в базе данных?</span><span class="sxs-lookup"><span data-stu-id="5e216-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="5e216-111">Что такое моделирование данных и почему оно так важно?</span><span class="sxs-lookup"><span data-stu-id="5e216-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="5e216-112">Как обеспечивается моделирования данных документа базы данных другой tooa реляционной базы данных?</span><span class="sxs-lookup"><span data-stu-id="5e216-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="5e216-113">Как выразить связи данных в нереляционной базе данных?</span><span class="sxs-lookup"><span data-stu-id="5e216-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="5e216-114">При внедрении данных и если связать toodata?</span><span class="sxs-lookup"><span data-stu-id="5e216-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="5e216-115">Внедрение данных</span><span class="sxs-lookup"><span data-stu-id="5e216-115">Embedding data</span></span>
<span data-ttu-id="5e216-116">При запуске моделирования данных в хранилище документа, например Azure Cosmos DB, попробуйте tootreat объекты в виде **самодостаточным документы** представлены в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="5e216-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="5e216-117">Прежде чем углубляться в подробности, давайте вернемся немного назад и рассмотрим, как можно смоделировать что-либо в реляционной базе данных, ведь многим из нас уже знакома эта тема.</span><span class="sxs-lookup"><span data-stu-id="5e216-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="5e216-118">Hello следующем примере показано, как пользователь может сохранить в реляционной базе данных.</span><span class="sxs-lookup"><span data-stu-id="5e216-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![Модель реляционной базы данных](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="5e216-120">При работе с реляционными базами данных, мы были при изучении для toonormalize лет нормализации, нормализации.</span><span class="sxs-lookup"><span data-stu-id="5e216-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="5e216-121">Нормализация данных обычно подразумевает создание сущности, такие как лицо и распределением в toodiscrete части данных.</span><span class="sxs-lookup"><span data-stu-id="5e216-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="5e216-122">В приведенном выше примере hello пользователь может иметь несколько записей контактной информации, а также несколько записей адресов.</span><span class="sxs-lookup"><span data-stu-id="5e216-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="5e216-123">Мы пойдем еще дальше и разобьем сведения о контактах, извлекая общие поля, такие как тип.</span><span class="sxs-lookup"><span data-stu-id="5e216-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="5e216-124">Аналогично и для адреса — здесь каждая запись имеет тип, такой как *Home* или *Business*.</span><span class="sxs-lookup"><span data-stu-id="5e216-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="5e216-125">Привет, руководствуясь локальных при нормализации данных слишком**избежать хранения избыточных данных** на каждой записи и вместо ссылки toodata.</span><span class="sxs-lookup"><span data-stu-id="5e216-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="5e216-126">В этом примере tooread обладающий все контактные сведения и адреса, необходимо toouse СОЕДИНЕНИЯ tooeffectively статистических данных во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="5e216-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="5e216-127">Чтобы обновить сведения о контактах и адреса для отдельного человека, требуется выполнить операции записи для множества отдельных таблиц.</span><span class="sxs-lookup"><span data-stu-id="5e216-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="5e216-128">Теперь давайте же Здравствуйте, взгляните на том, как мы модели данных как автономная сущность в базе данных документа.</span><span class="sxs-lookup"><span data-stu-id="5e216-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

<span data-ttu-id="5e216-129">Использование hello выше у нас есть теперь **денормализованные** hello записи лица где мы **внедренные** Здравствуйте, все сведения, касающиеся toothis пользователями, например свои контактные сведения и адреса, в одном tooa Документ JSON.</span><span class="sxs-lookup"><span data-stu-id="5e216-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="5e216-130">Кроме того так как мы не будете ограничены tooa фиксированную схему, мы hello гибкость toodo таких вещей, как полностью наличие контактные сведения различные формы.</span><span class="sxs-lookup"><span data-stu-id="5e216-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="5e216-131">Получение записи полный человек из базы данных hello теперь является отдельной операции в одной коллекции, а для одного документа чтения.</span><span class="sxs-lookup"><span data-stu-id="5e216-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="5e216-132">Обновление сведений о контактах и адресов в записи человека также обеспечивается одной операцией записи, выполняемой для одного документа.</span><span class="sxs-lookup"><span data-stu-id="5e216-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="5e216-133">По Денормализация данных, приложение должно tooissue меньшее число запросов и обновлений toocomplete распространенных операций.</span><span class="sxs-lookup"><span data-stu-id="5e216-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="5e216-134">Когда tooembed</span><span class="sxs-lookup"><span data-stu-id="5e216-134">When tooembed</span></span>
<span data-ttu-id="5e216-135">В общем случае модели внедренных данных следует использовать в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="5e216-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="5e216-136">между сущностями существуют связи **contains** ;</span><span class="sxs-lookup"><span data-stu-id="5e216-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="5e216-137">между сущностями существуют связи **один к нескольким** ;</span><span class="sxs-lookup"><span data-stu-id="5e216-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="5e216-138">имеются внедренные данные, которые **редко изменяются**;</span><span class="sxs-lookup"><span data-stu-id="5e216-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="5e216-139">имеются внедренные данные, которые не разрастаются **неограниченно**;</span><span class="sxs-lookup"><span data-stu-id="5e216-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="5e216-140">Внедренные данные, **целый** toodata в документе.</span><span class="sxs-lookup"><span data-stu-id="5e216-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="5e216-141">Обычно модели денормализованных данных обеспечивают повышенную производительность при **чтении** .</span><span class="sxs-lookup"><span data-stu-id="5e216-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="5e216-142">Если не tooembed</span><span class="sxs-lookup"><span data-stu-id="5e216-142">When not tooembed</span></span>
<span data-ttu-id="5e216-143">Хотя hello правило в базе данных документа является toodenormalize все, что и внедрить все данные в одном документе tooa, это может привести toosome ситуациях, в которых следует избегать.</span><span class="sxs-lookup"><span data-stu-id="5e216-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="5e216-144">Рассмотрим этот фрагмент кода JSON.</span><span class="sxs-lookup"><span data-stu-id="5e216-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="5e216-145">Так могла бы выглядеть сущность публикации с внедренными комментариями, если бы мы моделировали обычный блог или систему CMS.</span><span class="sxs-lookup"><span data-stu-id="5e216-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="5e216-146">Hello проблема с этим примером является, hello комментарии массив **unbounded**, это означает, что отсутствует номер toohello (практического) ограничения комментариев, может иметь любую одну публикацию.</span><span class="sxs-lookup"><span data-stu-id="5e216-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="5e216-147">Станет проблемы как размер hello hello документа может значительно расти.</span><span class="sxs-lookup"><span data-stu-id="5e216-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="5e216-148">Как размер hello hello документа увеличивается hello возможность tootransmit hello данных по линии связи hello, а также чтение и обновление hello в документе шкалы, будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="5e216-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="5e216-149">В этом случае было бы лучше hello tooconsider модели.</span><span class="sxs-lookup"><span data-stu-id="5e216-149">In this case it would be better tooconsider hello following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

<span data-ttu-id="5e216-150">Эта модель имеет hello трех последних комментарии на hello учет себя, который является массивом с фиксированной границей времени.</span><span class="sxs-lookup"><span data-stu-id="5e216-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="5e216-151">Hello других комментариев группируются в toobatches 100 комментариев и хранятся в виде отдельных документов.</span><span class="sxs-lookup"><span data-stu-id="5e216-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="5e216-152">Hello размер пакета hello был выбран как 100, потому что наши вымышленные приложения позволяет hello комментарии 100 tooload пользователей одновременно.</span><span class="sxs-lookup"><span data-stu-id="5e216-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="5e216-153">Другой случай, когда внедренные данные не рекомендуется при hello внедренных данных часто используются в документах и часто изменяются.</span><span class="sxs-lookup"><span data-stu-id="5e216-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="5e216-154">Рассмотрим этот фрагмент кода JSON.</span><span class="sxs-lookup"><span data-stu-id="5e216-154">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

<span data-ttu-id="5e216-155">Этот код может представлять биржевой портфель человека.</span><span class="sxs-lookup"><span data-stu-id="5e216-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="5e216-156">Мы выбрали tooembed hello биржевых данных в документе tooeach портфеля.</span><span class="sxs-lookup"><span data-stu-id="5e216-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="5e216-157">В среде, где связанные данные изменяется часто, как биржевая, торговых приложения внедрение часто изменяемых данных будет toomean, что каждый раз был продан stock постоянно обновляется каждый документ портфеля.</span><span class="sxs-lookup"><span data-stu-id="5e216-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="5e216-158">В течение дня акции *zaza* могут покупать и продавать сотни раз, и *zaza* могут входить в портфели тысяч пользователей.</span><span class="sxs-lookup"><span data-stu-id="5e216-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="5e216-159">С моделью данных, таких как hello выше мы бы tooupdate нескольких тысяч документов портфеля много раз каждый день ведущая tooa, не очень хорошо масштабируются.</span><span class="sxs-lookup"><span data-stu-id="5e216-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="5e216-160"><a id="Refer"></a>Использование ссылок на данные</span><span class="sxs-lookup"><span data-stu-id="5e216-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="5e216-161">Таким образом, внедрение данных отлично подходит для многих ситуаций, однако совершенно ясно, что существуют сценарии, в которых денормализация данных вызовет больше проблем, чем поможет решить.</span><span class="sxs-lookup"><span data-stu-id="5e216-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="5e216-162">Что же нам делать теперь?</span><span class="sxs-lookup"><span data-stu-id="5e216-162">So what do we do now?</span></span> 

<span data-ttu-id="5e216-163">Реляционные базы данных не являются hello единственное место, где можно создавать связи между сущностями.</span><span class="sxs-lookup"><span data-stu-id="5e216-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="5e216-164">В базе данных документов могут иметь сведения в одном документе, который фактически связывает toodata в других документах.</span><span class="sxs-lookup"><span data-stu-id="5e216-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="5e216-165">Теперь я хочу не рекомендуют даже одну минуту мы создаем системы, которые были бы лучше подходит tooa или реляционную базу данных в базе данных Azure Cosmos любая другая база данных документа, но простые отношения допустимы и может быть очень полезно.</span><span class="sxs-lookup"><span data-stu-id="5e216-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="5e216-166">В hello JSON ниже мы выбрали пример hello toouse портфеля акций из ранее но в этот раз мы называем элемент склада toohello по портфелю hello вместо его внедрения.</span><span class="sxs-lookup"><span data-stu-id="5e216-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="5e216-167">Таким образом, элемент склада hello часто изменяются на протяжении hello день hello только документ, который требуется обновить toobe при биржевых однооконный hello.</span><span class="sxs-lookup"><span data-stu-id="5e216-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


<span data-ttu-id="5e216-168">Подход toothis немедленно недостаток хотя является ли приложение tooshow необходимые сведения о каждой из них, который проводится при отображении портфолио человека; в этом случае потребуется toomake несколько приема-передачи toohello tooload hello сведения о базе данных для каждого документа акций.</span><span class="sxs-lookup"><span data-stu-id="5e216-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="5e216-169">Здесь мы сделали решение tooimprove hello эффективность операций записи, которые происходить часто в hello дня, но в свою очередь компрометации на hello операций чтения, потенциально оказывает меньшее влияние на производительность hello этой конкретной системы.</span><span class="sxs-lookup"><span data-stu-id="5e216-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="5e216-170">Нормализованных моделей данных **может потребоваться несколько циклов приема-передачи** toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="5e216-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="5e216-171">Сведения о внешнем ключе</span><span class="sxs-lookup"><span data-stu-id="5e216-171">What about foreign keys?</span></span>
<span data-ttu-id="5e216-172">Так как в настоящее время не используется понятие ограничения, внешнего ключа или в противном случае — все связи между документов, имеющих в документах фактически являются «слабой ссылки» и не будут проверены по самой базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="5e216-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="5e216-173">Если требуется, чтобы tooensure, hello данных, который ссылается документ tooactually существует, то потребуется toodo в приложении, или с помощью hello серверных триггеров или хранимых процедур в базе данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5e216-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="5e216-174">Когда tooreference</span><span class="sxs-lookup"><span data-stu-id="5e216-174">When tooreference</span></span>
<span data-ttu-id="5e216-175">В общем случае модели нормализованных данных следует использовать в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="5e216-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="5e216-176">Осуществляется представление связей **один ко многим** .</span><span class="sxs-lookup"><span data-stu-id="5e216-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="5e216-177">Осуществляется представление связей **многие ко многим** .</span><span class="sxs-lookup"><span data-stu-id="5e216-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="5e216-178">Связанные данные **часто изменяются**.</span><span class="sxs-lookup"><span data-stu-id="5e216-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="5e216-179">Данные, на которые указывает ссылка, могут быть **неограниченными**.</span><span class="sxs-lookup"><span data-stu-id="5e216-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="5e216-180">Обычно нормализация обеспечивает повышенную производительность при **записи** .</span><span class="sxs-lookup"><span data-stu-id="5e216-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="5e216-181">Места размещения hello связи?</span><span class="sxs-lookup"><span data-stu-id="5e216-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="5e216-182">рост Hello отношения «hello» поможет определить, в которых документ toostore hello.</span><span class="sxs-lookup"><span data-stu-id="5e216-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="5e216-183">Если взглянуть на hello JSON ниже, моделирующее издателей и книг.</span><span class="sxs-lookup"><span data-stu-id="5e216-183">If we look at hello JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

<span data-ttu-id="5e216-184">При небольших с ограниченной роста hello количество книг hello по издателю последующее сохранение ссылки книги hello внутри документа hello издателя может пригодиться.</span><span class="sxs-lookup"><span data-stu-id="5e216-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="5e216-185">Однако если unbounded hello количество книг по издателю, эта модель данных приведет toomutable, растет массивы как документе издателю hello пример выше.</span><span class="sxs-lookup"><span data-stu-id="5e216-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="5e216-186">Переключение предметы немного бы результат в модели, но теперь hello и те же данные по-прежнему представляет позволяет избежать эти большие изменяемой коллекции.</span><span class="sxs-lookup"><span data-stu-id="5e216-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="5e216-187">В приведенном выше примере hello, мы удалили hello unbounded коллекции hello издателя документа.</span><span class="sxs-lookup"><span data-stu-id="5e216-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="5e216-188">Вместо этого мы просто у издателя toohello ссылку на каждом документе книги.</span><span class="sxs-lookup"><span data-stu-id="5e216-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="5e216-189">Как моделировать связи "многие ко многим"</span><span class="sxs-lookup"><span data-stu-id="5e216-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="5e216-190">В реляционной базе данных связи *многие ко многим* часто моделируются с помощью таблиц JOIN, которые просто соединяют вместе записи из других таблиц.</span><span class="sxs-lookup"><span data-stu-id="5e216-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Объединенные таблицы](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="5e216-192">Может быть удобным средством tooreplicate hello же результата с помощью документов и создания модели данных, которая выглядит примерно следующие toohello.</span><span class="sxs-lookup"><span data-stu-id="5e216-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="5e216-193">Такой подход будет работать.</span><span class="sxs-lookup"><span data-stu-id="5e216-193">This would work.</span></span> <span data-ttu-id="5e216-194">Тем не менее загрузка автора с их книг или Загрузка книги с его автор всегда потребуется по меньшей мере два дополнительных запросов к hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="5e216-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="5e216-195">Объединение документов и еще один запрос toofetch hello непосредственно документа присоединяемых toohello один запрос.</span><span class="sxs-lookup"><span data-stu-id="5e216-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="5e216-196">Если эта таблица JOIN всего лишь соединяет два элемента данных, почему бы просто не отказаться от нее?</span><span class="sxs-lookup"><span data-stu-id="5e216-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="5e216-197">Рассмотрим следующие hello.</span><span class="sxs-lookup"><span data-stu-id="5e216-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="5e216-198">Теперь если у меня автора, немедленно узнать, какие книги был разработан и и наоборот, если у меня возникли загруженного документа книги я знаю hello идентификаторы авторов hello.</span><span class="sxs-lookup"><span data-stu-id="5e216-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="5e216-199">Это экономит, промежуточный запрос к hello соединяемой таблице уменьшение числа hello server циклов приема-передачи приложение имеет toomake.</span><span class="sxs-lookup"><span data-stu-id="5e216-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="5e216-200"><a id="WrapUp"></a>Гибридные модели данных</span><span class="sxs-lookup"><span data-stu-id="5e216-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="5e216-201">Мы рассмотрели внедрение данных (или денормализацию) и использование ссылок на данные (или нормализацию), а также преимущества и недостатки этих подходов.</span><span class="sxs-lookup"><span data-stu-id="5e216-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="5e216-202">Он не всегда имеют toobe либо или, не быть сущности Испуганные toomix копирование немного.</span><span class="sxs-lookup"><span data-stu-id="5e216-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="5e216-203">На основе определенных шаблонов использования и рабочих нагрузок, которые могут быть случаи, где смешивание внедренные приложения и ссылочных данных имеет смысл удалось логику приложения toosimpler интереса с сервером меньшее число циклов приема-передачи отказываясь высокого уровня производительности .</span><span class="sxs-lookup"><span data-stu-id="5e216-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="5e216-204">Рассмотрим следующий JSON hello.</span><span class="sxs-lookup"><span data-stu-id="5e216-204">Consider hello following JSON.</span></span> 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

<span data-ttu-id="5e216-205">Здесь мы (обычно) выполнили hello внедренную модель, где внедренные данные из других сущностей в hello верхнего уровня документа, но упоминается других данных.</span><span class="sxs-lookup"><span data-stu-id="5e216-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="5e216-206">Если взглянуть на документе книги hello, мы видим, несколько интересных поля при рассмотрении массива hello авторов.</span><span class="sxs-lookup"><span data-stu-id="5e216-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="5e216-207">Отсутствует *идентификатор* поле, являющееся поле hello, мы используем toorefer задней tooan автор документа, стандартные рекомендации по Нормализованная модель, а затем мы также имеют *имя* и *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="5e216-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="5e216-208">Мы может просто использовали *идентификатор* левого tooget приложения hello дополнительную информацию, помогающую его из соответствующих автор документа hello, с помощью hello «связи», но, поскольку наше приложение отображает имя автора hello и a эскиз рисунка с каждой книги отображается мы можно сохранить сервере toohello кругового пути на книги в списке, денормализации **некоторые** данные автора hello.</span><span class="sxs-lookup"><span data-stu-id="5e216-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="5e216-209">Убедитесь, что, если изменено имя автора hello или было tooupdate их фотография будет toogo обновление всех книг они никогда не опубликована, но для нашего приложения, исходя из предположения hello авторы не изменяют очень часто, их имена это допустимого конструктора решение.</span><span class="sxs-lookup"><span data-stu-id="5e216-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="5e216-210">В примере hello **предварительно вычисляемых агрегатов** значения toosave ресурсов обработки на операции чтения.</span><span class="sxs-lookup"><span data-stu-id="5e216-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="5e216-211">В примере hello некоторые из данных hello, внедренных в hello автор документа является данных, вычисляемых во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="5e216-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="5e216-212">Создается каждый раз при публикации новой книги документа книги **и** hello countOfBooks задано значение tooa вычисляется на основании hello число документов в книге, существующих для определенной автора.</span><span class="sxs-lookup"><span data-stu-id="5e216-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="5e216-213">Эта оптимизация бы хорошо чтения больших систем, где может позволить вычислений toodo при записи в порядке toooptimize чтений.</span><span class="sxs-lookup"><span data-stu-id="5e216-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="5e216-214">Здравствуйте, toohave возможности модели с предварительно вычисляемыми полями стало возможным, так как Azure Cosmos DB поддерживает **транзакции с несколькими документами**.</span><span class="sxs-lookup"><span data-stu-id="5e216-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="5e216-215">Многих хранилищ NoSQL нельзя выполнить транзакции для документов и поэтому представление проектные решения, такие как «всегда встраивать все», из-за ограничений toothis.</span><span class="sxs-lookup"><span data-stu-id="5e216-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="5e216-216">В Azure Cosmos DB вы можете использовать триггеры на стороне сервера или хранимые процедуры, которые вставляют книги и обновляют авторов в рамках транзакции ACID.</span><span class="sxs-lookup"><span data-stu-id="5e216-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="5e216-217">Теперь вы не **имеют** tooembed tooone все содержимое документа просто toobe в том, что данные остаются неизменными.</span><span class="sxs-lookup"><span data-stu-id="5e216-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="5e216-218"><a name="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e216-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="5e216-219">Hello крупнейших общие выводы из этой статьи — toounderstand, что в мире без схемы моделирования данных будет столь же важно как никогда.</span><span class="sxs-lookup"><span data-stu-id="5e216-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="5e216-220">Так же, как есть не единый способ toorepresent фрагмента данных на экране, нет не единый способ toomodel данных.</span><span class="sxs-lookup"><span data-stu-id="5e216-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="5e216-221">Требуется toounderstand приложения и каким образом будут получены, получать и обрабатывать данные hello.</span><span class="sxs-lookup"><span data-stu-id="5e216-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="5e216-222">Затем применяя некоторые hello рекомендации, описанные ниже, вы можно задать о создании модели, учитывающие hello немедленным потребностям приложения.</span><span class="sxs-lookup"><span data-stu-id="5e216-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="5e216-223">Приложения должны toochange, позволяет эффективно использовать гибкость hello tooembrace без схемы базы данных, изменение и легко развить модели данных.</span><span class="sxs-lookup"><span data-stu-id="5e216-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="5e216-224">toolearn Дополнительные сведения о базе данных Azure Cosmos, см. Служба toohello [документации](https://azure.microsoft.com/documentation/services/cosmos-db/) страницы.</span><span class="sxs-lookup"><span data-stu-id="5e216-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="5e216-225">toounderstand как tooshard данные по нескольким секциям, см. слишком[секционирование данных в базе данных Azure Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="5e216-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
