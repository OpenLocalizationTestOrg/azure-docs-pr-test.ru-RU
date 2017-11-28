---
title: "Моделирование данных документов для базы данных NoSQL | Документы Майкрософт"
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
ms.openlocfilehash: 16c387fe574243544cf54cf283c7713ddcaa1942
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="c98a4-104">Моделирование данных документов для базы данных NoSQL</span><span class="sxs-lookup"><span data-stu-id="c98a4-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="c98a4-105">Хотя базы данных без схем, такие как Azure Cosmos DB, существенно упрощают внесение изменений в модель данных, вам все равно следует уделить время анализу ситуации с данными.</span><span class="sxs-lookup"><span data-stu-id="c98a4-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="c98a4-106">Как данные будут храниться?</span><span class="sxs-lookup"><span data-stu-id="c98a4-106">How is data going to be stored?</span></span> <span data-ttu-id="c98a4-107">Как приложение будет получать данные и выполнять запросы по ним?</span><span class="sxs-lookup"><span data-stu-id="c98a4-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="c98a4-108">Ориентировано ли ваше приложение на запись или на чтение?</span><span class="sxs-lookup"><span data-stu-id="c98a4-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="c98a4-109">После прочтения этой статьи вы сможете ответить на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="c98a4-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="c98a4-110">Как следует представлять документ в базе данных?</span><span class="sxs-lookup"><span data-stu-id="c98a4-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="c98a4-111">Что такое моделирование данных и почему оно так важно?</span><span class="sxs-lookup"><span data-stu-id="c98a4-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="c98a4-112">Чем различается моделирование данных в базе данных документов и в реляционной базе данных?</span><span class="sxs-lookup"><span data-stu-id="c98a4-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="c98a4-113">Как выразить связи данных в нереляционной базе данных?</span><span class="sxs-lookup"><span data-stu-id="c98a4-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="c98a4-114">Когда следует внедрять данные, а когда — связывать?</span><span class="sxs-lookup"><span data-stu-id="c98a4-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="c98a4-115">Внедрение данных</span><span class="sxs-lookup"><span data-stu-id="c98a4-115">Embedding data</span></span>
<span data-ttu-id="c98a4-116">Когда вы начинаете моделировать данные в хранилище документов, таком как Azure Cosmos DB, попробуйте обрабатывать свои сущности как **самодостаточные документы**, представленные в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="c98a4-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="c98a4-117">Прежде чем углубляться в подробности, давайте вернемся немного назад и рассмотрим, как можно смоделировать что-либо в реляционной базе данных, ведь многим из нас уже знакома эта тема.</span><span class="sxs-lookup"><span data-stu-id="c98a4-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="c98a4-118">В следующем примере показано, как можно сохранить в реляционной базе данных человека.</span><span class="sxs-lookup"><span data-stu-id="c98a4-118">The following example shows how a person might be stored in a relational database.</span></span> 

![Модель реляционной базы данных](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="c98a4-120">При работе с реляционными базами данных мы в течение многих лет учимся одному — нормализовать, нормализовать, нормализовать.</span><span class="sxs-lookup"><span data-stu-id="c98a4-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="c98a4-121">Нормализация данных обычно заключается в том, чтобы взять сущность, например человека, и разбить ее на отдельные элементы данных.</span><span class="sxs-lookup"><span data-stu-id="c98a4-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="c98a4-122">В приведенном выше примере человек может иметь несколько записей со сведениями о контактах, а также несколько записей с адресом.</span><span class="sxs-lookup"><span data-stu-id="c98a4-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="c98a4-123">Мы пойдем еще дальше и разобьем сведения о контактах, извлекая общие поля, такие как тип.</span><span class="sxs-lookup"><span data-stu-id="c98a4-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="c98a4-124">Аналогично и для адреса — здесь каждая запись имеет тип, такой как *Home* или *Business*.</span><span class="sxs-lookup"><span data-stu-id="c98a4-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="c98a4-125">Руководящий принцип при нормализации данных заключается в том, чтобы **избегать хранения избыточных данных** в каждой записи и использовать только ссылки на эти данные.</span><span class="sxs-lookup"><span data-stu-id="c98a4-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="c98a4-126">Чтобы в данном примере считать данные о человеке со всеми его сведениями контактах и адресами, необходимо использовать операторы JOIN для эффективной агрегации данных во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c98a4-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="c98a4-127">Чтобы обновить сведения о контактах и адреса для отдельного человека, требуется выполнить операции записи для множества отдельных таблиц.</span><span class="sxs-lookup"><span data-stu-id="c98a4-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="c98a4-128">А сейчас давайте рассмотрим, как смоделировать аналогичные данные в виде самодостаточной сущности в базе данных документов.</span><span class="sxs-lookup"><span data-stu-id="c98a4-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="c98a4-129">Согласно описанному выше подходу, мы выполнили **денормализацию** записи человека, куда была **внедрена** такая информация, как сведения о контактах и адреса, получив отдельный документ JSON.</span><span class="sxs-lookup"><span data-stu-id="c98a4-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="c98a4-130">Кроме того, отсутствие привязки к фиксированной схеме повышает гибкость работы, например, мы можем использовать сведения о контактах в самых разных формах.</span><span class="sxs-lookup"><span data-stu-id="c98a4-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="c98a4-131">Получение всей записи человека из базы данных теперь обеспечивается одной операцией чтения, выполняемой для одной коллекции и отдельного документа.</span><span class="sxs-lookup"><span data-stu-id="c98a4-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="c98a4-132">Обновление сведений о контактах и адресов в записи человека также обеспечивается одной операцией записи, выполняемой для одного документа.</span><span class="sxs-lookup"><span data-stu-id="c98a4-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="c98a4-133">Благодаря денормализации данных ваше приложение может использовать меньше запросов и обновлений для выполнения распространенных операций.</span><span class="sxs-lookup"><span data-stu-id="c98a4-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="c98a4-134">Когда следует использовать внедрение</span><span class="sxs-lookup"><span data-stu-id="c98a4-134">When to embed</span></span>
<span data-ttu-id="c98a4-135">В общем случае модели внедренных данных следует использовать в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="c98a4-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="c98a4-136">между сущностями существуют связи **contains** ;</span><span class="sxs-lookup"><span data-stu-id="c98a4-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="c98a4-137">между сущностями существуют связи **один к нескольким** ;</span><span class="sxs-lookup"><span data-stu-id="c98a4-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="c98a4-138">имеются внедренные данные, которые **редко изменяются**;</span><span class="sxs-lookup"><span data-stu-id="c98a4-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="c98a4-139">имеются внедренные данные, которые не разрастаются **неограниченно**;</span><span class="sxs-lookup"><span data-stu-id="c98a4-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="c98a4-140">имеются внедренные данные, которые составляют **целое** с данными в документе.</span><span class="sxs-lookup"><span data-stu-id="c98a4-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="c98a4-141">Обычно модели денормализованных данных обеспечивают повышенную производительность при **чтении** .</span><span class="sxs-lookup"><span data-stu-id="c98a4-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="c98a4-142">Когда внедрение использовать не следует</span><span class="sxs-lookup"><span data-stu-id="c98a4-142">When not to embed</span></span>
<span data-ttu-id="c98a4-143">Хотя основной подход для базы данных документов заключается в том, чтобы выполнить денормализацию всех элементов и внедрить все данные в один документ, это может привести к некоторым нежелательным ситуациям.</span><span class="sxs-lookup"><span data-stu-id="c98a4-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="c98a4-144">Рассмотрим этот фрагмент кода JSON.</span><span class="sxs-lookup"><span data-stu-id="c98a4-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="c98a4-145">Так могла бы выглядеть сущность публикации с внедренными комментариями, если бы мы моделировали обычный блог или систему CMS.</span><span class="sxs-lookup"><span data-stu-id="c98a4-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="c98a4-146">Проблема с данным примером заключается в том, что массив комментариев является **неограниченным**, то есть не существует (фактического) предела для количества комментариев, которое может иметь отдельная публикация.</span><span class="sxs-lookup"><span data-stu-id="c98a4-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="c98a4-147">Это станет источником проблем, так как размер документа может значительно вырасти.</span><span class="sxs-lookup"><span data-stu-id="c98a4-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="c98a4-148">По мере роста размера документа пропорционально ухудшается возможность передачи данных, а также чтения и обновления документа.</span><span class="sxs-lookup"><span data-stu-id="c98a4-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="c98a4-149">В этом случае лучше рассмотреть следующую модель.</span><span class="sxs-lookup"><span data-stu-id="c98a4-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
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

<span data-ttu-id="c98a4-150">В этом модели три последних комментария внедрены в саму публикацию, которая здесь представлена массивом фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="c98a4-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="c98a4-151">Другие комментарии сгруппированы в пакеты по 100 штук и сохранены в отдельных документах.</span><span class="sxs-lookup"><span data-stu-id="c98a4-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="c98a4-152">Размер пакета был выбран равным 100, поскольку наше условное приложение позволяет пользователю отправить 100 комментариев за один раз.</span><span class="sxs-lookup"><span data-stu-id="c98a4-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="c98a4-153">Кроме того внедрение данных нельзя назвать удачным решением там, где эти данные часто используются в разных документах и постоянно изменяются.</span><span class="sxs-lookup"><span data-stu-id="c98a4-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="c98a4-154">Рассмотрим этот фрагмент кода JSON.</span><span class="sxs-lookup"><span data-stu-id="c98a4-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="c98a4-155">Этот код может представлять биржевой портфель человека.</span><span class="sxs-lookup"><span data-stu-id="c98a4-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="c98a4-156">Мы решили внедрить информацию об акциях в каждый документ портфеля.</span><span class="sxs-lookup"><span data-stu-id="c98a4-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="c98a4-157">В среде, где связанные данные регулярно изменяются, например, в приложении биржевых торгов, внедрение часто изменяемых данных означает, что вы постоянно обновляете каждый документ портфеля при выполнении торговой операции с каждой акцией.</span><span class="sxs-lookup"><span data-stu-id="c98a4-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="c98a4-158">В течение дня акции *zaza* могут покупать и продавать сотни раз, и *zaza* могут входить в портфели тысяч пользователей.</span><span class="sxs-lookup"><span data-stu-id="c98a4-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="c98a4-159">В случае использования описанной выше модели данных нам пришлось бы обновлять многие тысячи документов портфелей каждый день, что затруднило бы масштабирование системы.</span><span class="sxs-lookup"><span data-stu-id="c98a4-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <span data-ttu-id="c98a4-160"><a id="Refer"></a>Использование ссылок на данные</span><span class="sxs-lookup"><span data-stu-id="c98a4-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="c98a4-161">Таким образом, внедрение данных отлично подходит для многих ситуаций, однако совершенно ясно, что существуют сценарии, в которых денормализация данных вызовет больше проблем, чем поможет решить.</span><span class="sxs-lookup"><span data-stu-id="c98a4-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="c98a4-162">Что же нам делать теперь?</span><span class="sxs-lookup"><span data-stu-id="c98a4-162">So what do we do now?</span></span> 

<span data-ttu-id="c98a4-163">Связи между сущностями можно задавать не только в реляционных базах данных.</span><span class="sxs-lookup"><span data-stu-id="c98a4-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="c98a4-164">В базе данных документов можно поместить в один документ сведения, которые ссылаются на данные в других документах.</span><span class="sxs-lookup"><span data-stu-id="c98a4-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="c98a4-165">Я не спорю, что мы создаем системы, которые лучше подходят для реляционной базы данных в Azure Cosmos DB или любой другой базы данных документов, однако простые связи легко реализуются и могут оказаться очень удобны в работе.</span><span class="sxs-lookup"><span data-stu-id="c98a4-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="c98a4-166">В приведенном ниже коде JSON мы решили использовать использованный ранее пример биржевого портфеля, однако здесь мы не внедряем элемент акции в портфеле, а ссылаемся на него.</span><span class="sxs-lookup"><span data-stu-id="c98a4-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="c98a4-167">Если элемент акции часто изменяется в течение дня, то обновлять требуется единственный документ акции.</span><span class="sxs-lookup"><span data-stu-id="c98a4-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

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


<span data-ttu-id="c98a4-168">Недостаток такого подхода проявляется, когда приложению нужно отобразить информацию о каждой имеющейся акции в портфеле человека; в этом случае потребуется выполнить множество обращений к базе данных, чтобы загрузить информацию для каждого документа акции.</span><span class="sxs-lookup"><span data-stu-id="c98a4-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="c98a4-169">Здесь мы приняли решение повысить эффективность операций записи, которые часто выполняются в течение дня, однако это затруднило выполнение операций чтения, которые оказывают меньшее влияние на производительность всей данной системы.</span><span class="sxs-lookup"><span data-stu-id="c98a4-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="c98a4-170">Модели нормализованных данных **могут потребовать больше круговых путей** к серверу.</span><span class="sxs-lookup"><span data-stu-id="c98a4-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="c98a4-171">Сведения о внешнем ключе</span><span class="sxs-lookup"><span data-stu-id="c98a4-171">What about foreign keys?</span></span>
<span data-ttu-id="c98a4-172">Поскольку в настоящий момент концепция ограничения, основанная на внешнем ключе или чем-либо другом, отсутствует, все связи между документами представляют собой "слабые звенья" и не проверяются базой данных.</span><span class="sxs-lookup"><span data-stu-id="c98a4-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="c98a4-173">Если вы хотите убедиться, что данные, на которые ссылается документ, действительно существуют, это нужно сделать в приложении либо с помощью триггеров на стороне сервера или хранимых процедур в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c98a4-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="c98a4-174">Когда следует использовать ссылки</span><span class="sxs-lookup"><span data-stu-id="c98a4-174">When to reference</span></span>
<span data-ttu-id="c98a4-175">В общем случае модели нормализованных данных следует использовать в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="c98a4-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="c98a4-176">Осуществляется представление связей **один ко многим** .</span><span class="sxs-lookup"><span data-stu-id="c98a4-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="c98a4-177">Осуществляется представление связей **многие ко многим** .</span><span class="sxs-lookup"><span data-stu-id="c98a4-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="c98a4-178">Связанные данные **часто изменяются**.</span><span class="sxs-lookup"><span data-stu-id="c98a4-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="c98a4-179">Данные, на которые указывает ссылка, могут быть **неограниченными**.</span><span class="sxs-lookup"><span data-stu-id="c98a4-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="c98a4-180">Обычно нормализация обеспечивает повышенную производительность при **записи** .</span><span class="sxs-lookup"><span data-stu-id="c98a4-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="c98a4-181">Куда следует поместить связь</span><span class="sxs-lookup"><span data-stu-id="c98a4-181">Where do I put the relationship?</span></span>
<span data-ttu-id="c98a4-182">Рост связи поможет определить, в каком документе следует сохранить ссылку.</span><span class="sxs-lookup"><span data-stu-id="c98a4-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="c98a4-183">Давайте рассмотрим следующий код JSON, моделирующий издателей и книги.</span><span class="sxs-lookup"><span data-stu-id="c98a4-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="c98a4-184">Если на издателя приходится небольшое число книг, а рост ограничен, то может оказаться удобным хранить ссылку на книгу в документе издателя.</span><span class="sxs-lookup"><span data-stu-id="c98a4-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="c98a4-185">Однако если число книг на издателя не имеет ограничений, эта модель данных приведет к изменяемым и разрастающимся массивам, как в приведенном выше примере с документом издателя.</span><span class="sxs-lookup"><span data-stu-id="c98a4-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="c98a4-186">Небольшая доработка помогает получить модель, которая все еще представляет те же данные, однако избавляется от крупных изменяемых коллекций.</span><span class="sxs-lookup"><span data-stu-id="c98a4-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="c98a4-187">В приведенном выше примере мы помещали неограниченную коллекцию в документ издателя.</span><span class="sxs-lookup"><span data-stu-id="c98a4-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="c98a4-188">Вместо этого мы просто воспользуемся ссылкой на издателя в каждом документе книги.</span><span class="sxs-lookup"><span data-stu-id="c98a4-188">Instead we just have a a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="c98a4-189">Как моделировать связи "многие ко многим"</span><span class="sxs-lookup"><span data-stu-id="c98a4-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="c98a4-190">В реляционной базе данных связи *многие ко многим* часто моделируются с помощью таблиц JOIN, которые просто соединяют вместе записи из других таблиц.</span><span class="sxs-lookup"><span data-stu-id="c98a4-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Объединенные таблицы](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="c98a4-192">У вас может возникнуть желание реплицировать это с помощью документов и создать модель данных, аналогичную приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="c98a4-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="c98a4-193">Такой подход будет работать.</span><span class="sxs-lookup"><span data-stu-id="c98a4-193">This would work.</span></span> <span data-ttu-id="c98a4-194">Однако при загрузке автора вместе с его книгами или книги вместе с ее автором всегда потребуется отправлять два дополнительных запроса в базу данных.</span><span class="sxs-lookup"><span data-stu-id="c98a4-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="c98a4-195">Один запрос отправляется в документ присоединения, а другой — для получения самого присоединяемого документа.</span><span class="sxs-lookup"><span data-stu-id="c98a4-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="c98a4-196">Если эта таблица JOIN всего лишь соединяет два элемента данных, почему бы просто не отказаться от нее?</span><span class="sxs-lookup"><span data-stu-id="c98a4-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="c98a4-197">Давайте рассмотрим следующее.</span><span class="sxs-lookup"><span data-stu-id="c98a4-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="c98a4-198">Если у меня есть автор, я сразу же узнаю, какие книги он написал, и наоборот, если у меня загружен документ книги, я получу сведения об авторе.</span><span class="sxs-lookup"><span data-stu-id="c98a4-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="c98a4-199">Это позволяет отказаться от промежуточного запроса к таблице JOIN и сократить количество круговых путей для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="c98a4-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <span data-ttu-id="c98a4-200"><a id="WrapUp"></a>Гибридные модели данных</span><span class="sxs-lookup"><span data-stu-id="c98a4-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="c98a4-201">Мы рассмотрели внедрение данных (или денормализацию) и использование ссылок на данные (или нормализацию), а также преимущества и недостатки этих подходов.</span><span class="sxs-lookup"><span data-stu-id="c98a4-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="c98a4-202">Однако далеко не всегда следует придерживаться лишь одного из подходов, можно попробовать совместить их.</span><span class="sxs-lookup"><span data-stu-id="c98a4-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="c98a4-203">Учитывая применяемые в приложении схемы использования и рабочие нагрузки, в некоторых случаях совмещение внедрения и ссылок может иметь смысл и позволяет упростить логическую схему приложения, сократить число круговых путей к серверу и при этом сохранить высокий уровень производительности.</span><span class="sxs-lookup"><span data-stu-id="c98a4-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="c98a4-204">Давайте рассмотрим следующий код JSON.</span><span class="sxs-lookup"><span data-stu-id="c98a4-204">Consider the following JSON.</span></span> 

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

<span data-ttu-id="c98a4-205">Здесь мы в большей степени придерживались модели внедрения, где данные из других сущностей внедряются в документ верхнего уровня, однако для остальных данных используются ссылки.</span><span class="sxs-lookup"><span data-stu-id="c98a4-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="c98a4-206">Если взглянуть на документ книги, можно заметить несколько интересных полей в массиве авторов.</span><span class="sxs-lookup"><span data-stu-id="c98a4-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="c98a4-207">Существует поле *id*, которое используется для обратной ссылки на документ автора, что является стандартным решением в модели нормализации, однако также присутствуют поля *name* и *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="c98a4-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="c98a4-208">Мы могли бы ограничиться полем *id* и заставить приложение получать всю необходимую информацию из соответствующего документа автора с использованием "ссылки", но поскольку наше приложение выводит имя автора и эскиз для каждой отображаемой книги, мы можем сэкономить по одному круговому пути к серверу на каждую книгу в списке, выполнив денормализацию **некоторых** данных об авторе.</span><span class="sxs-lookup"><span data-stu-id="c98a4-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="c98a4-209">Естественно, в случае изменения имени автора или обновления его фотографии нам пришлось бы обновить каждую опубликованную им книгу, однако в нашем приложении такое решение вполне уместно, поскольку авторы довольно редко меняют свои имена.</span><span class="sxs-lookup"><span data-stu-id="c98a4-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="c98a4-210">В примере используются значения **предварительно вычисленных статистических выражений** , чтобы сэкономить вычислительные ресурсы на операции чтения.</span><span class="sxs-lookup"><span data-stu-id="c98a4-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="c98a4-211">В данном примере некоторые данные, внедренные в документ автора, вычисляются во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c98a4-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="c98a4-212">Каждый раз при публикации новой книги создается документ книги, **и** для поля countOfBooks задается вычисленное значение, зависящее от числа существующих для данного автора документов книги.</span><span class="sxs-lookup"><span data-stu-id="c98a4-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="c98a4-213">Такая оптимизация хорошо подходит для систем с большим количеством операций чтения, где можно выполнять вычисления в операциях записи для повышения производительности операций чтения.</span><span class="sxs-lookup"><span data-stu-id="c98a4-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="c98a4-214">Использование модели с предварительно вычисленными значениями в полях стало возможным благодаря тому, что Azure Cosmos DB поддерживает **транзакции с несколькими документами**.</span><span class="sxs-lookup"><span data-stu-id="c98a4-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="c98a4-215">Многие хранилища NoSQL не позволяют выполнять транзакции между документами, что вынуждает слепо следовать правилу "всегда внедряйте все, что можно".</span><span class="sxs-lookup"><span data-stu-id="c98a4-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="c98a4-216">В Azure Cosmos DB вы можете использовать триггеры на стороне сервера или хранимые процедуры, которые вставляют книги и обновляют авторов в рамках транзакции ACID.</span><span class="sxs-lookup"><span data-stu-id="c98a4-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="c98a4-217">Теперь вам не **обязательно** внедрять все в один документ просто для того, чтобы обеспечить согласованность данных.</span><span class="sxs-lookup"><span data-stu-id="c98a4-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <span data-ttu-id="c98a4-218"><a name="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c98a4-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="c98a4-219">Основная идея этой статьи заключается в том, что моделирование данных без фиксированных схем не теряет своей актуальности.</span><span class="sxs-lookup"><span data-stu-id="c98a4-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="c98a4-220">Как не существует единственного способа представить элемент данных на экране, нет такого способа и для моделирования данных.</span><span class="sxs-lookup"><span data-stu-id="c98a4-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="c98a4-221">Необходимо разобраться в принципах работы приложения, его механизмах формирования, использования и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="c98a4-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="c98a4-222">После этого с помощью представленных здесь рекомендаций вы можете приступить к созданию модели, которая оптимально соответствует основным потребностям вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="c98a4-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="c98a4-223">Благодаря отсутствию схемы в базе данных вы можете оперативно вносить изменения в приложения и легко корректировать модель данных соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="c98a4-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="c98a4-224">Дополнительные сведения об Azure Cosmos DB см. на странице [документации](https://azure.microsoft.com/documentation/services/cosmos-db/) по этой службе.</span><span class="sxs-lookup"><span data-stu-id="c98a4-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="c98a4-225">Чтобы понять, как сегментировать данные по нескольким разделам, ознакомьтесь со статьей [Секционирование, ключи секции и масштабирование в DocumentDB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="c98a4-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
