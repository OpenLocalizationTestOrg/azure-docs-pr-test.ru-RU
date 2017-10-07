---
title: "aaaAzure Воронкообразные диаграммы аналитики приложений"
description: "Дополнительные сведения об использовании toodiscover Воронкообразные диаграммы как клиенты взаимодействуют с приложением."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 2a6125cf596570cfaee30bb3ff757916e90d7676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="27cd2-103">Узнайте, как пользователи используют приложения с hello Воронкообразные диаграммы аналитики приложений</span><span class="sxs-lookup"><span data-stu-id="27cd2-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="27cd2-104">Основные сведения о качества — бизнес-tooyour первостепенное значение hello.</span><span class="sxs-lookup"><span data-stu-id="27cd2-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="27cd2-105">Если приложение состоит из нескольких этапов, потребуется tooknow, если большинство пользователей продвигается через весь процесс hello, или если они завершение процесса hello в определенный момент.</span><span class="sxs-lookup"><span data-stu-id="27cd2-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="27cd2-106">Hello продвижения через ряд шагов для веб-приложения, называется «Воронка».</span><span class="sxs-lookup"><span data-stu-id="27cd2-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="27cd2-107">Можно использовать hello анализа toogain Воронкообразные диаграммы аналитики приложений пользователей и пошаговые курсами монитора.</span><span class="sxs-lookup"><span data-stu-id="27cd2-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="27cd2-108">Приступая к работе с колонке hello Воронкообразные диаграммы</span><span class="sxs-lookup"><span data-stu-id="27cd2-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="27cd2-109">toolearn простым способом Hello о Воронкообразные диаграммы — toowalk на то, что пример.</span><span class="sxs-lookup"><span data-stu-id="27cd2-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="27cd2-110">Hello рисунках ниже описываются шаги владельцев hello для бизнеса электронной коммерции может потребоваться toolearn как своим клиентам взаимодействовать с веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="27cd2-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="27cd2-111">Создание воронки</span><span class="sxs-lookup"><span data-stu-id="27cd2-111">Create your funnel</span></span>
<span data-ttu-id="27cd2-112">Перед созданием вашей воронкообразной необходимо toodecide на hello вопрос будет tooanswer.</span><span class="sxs-lookup"><span data-stu-id="27cd2-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="27cd2-113">Например может потребоваться tooknow количество клиентов, просмотр на домашней странице нажмите на оповещение.</span><span class="sxs-lookup"><span data-stu-id="27cd2-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="27cd2-114">В этом примере hello владельцев hello компании Fabrikam Fiber требуется tooknow hello процент клиентов, которые совершить покупку после добавления элементов tootheir Корзина для покупок во время hello прошлый месяц.</span><span class="sxs-lookup"><span data-stu-id="27cd2-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="27cd2-115">Ниже приведены шаги hello, они принимают toocreate их воронки.</span><span class="sxs-lookup"><span data-stu-id="27cd2-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="27cd2-116">Нажмите кнопку Новый hello в колонке hello Воронкообразные диаграммы.</span><span class="sxs-lookup"><span data-stu-id="27cd2-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="27cd2-117">Выберите диапазон времени hello «За последний месяц» hello **диапазон времени** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="27cd2-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="27cd2-118">Выберите hello **страницу продукта** события из hello **шаг 1** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="27cd2-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="27cd2-119">Выберите hello **покупок добавить tooshopping** события из hello **шаг 2** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="27cd2-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="27cd2-120">Выберите hello **щелкните Покупка** события из hello **шаг 3** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="27cd2-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="27cd2-121">Добавить Воронка toohello имя и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="27cd2-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="27cd2-122">Hello следующей иллюстрации демонстрируется hello данных hello Воронкообразные диаграммы колонку приводит к возникновению ошибки.</span><span class="sxs-lookup"><span data-stu-id="27cd2-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="27cd2-123">Из здесь hello Fabrikam владельцев можно увидеть, что во время hello прошлой неделе 22.7 спецификации % от своих клиентов, которые добавлены tootheir элементов списка покупок корзину завершенного hello покупки.</span><span class="sxs-lookup"><span data-stu-id="27cd2-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="27cd2-124">Также они могут видеть 1% клиентов hello перед посетите страницу продукта hello и 20% от своих клиентов Выход после завершения покупки выделить объявления.</span><span class="sxs-lookup"><span data-stu-id="27cd2-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Колонка "Воронки" с данными](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="27cd2-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27cd2-126">Next steps</span></span>
  * [<span data-ttu-id="27cd2-127">Общие сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="27cd2-127">Usage overview</span></span>](app-insights-usage-overview.md)
  * [<span data-ttu-id="27cd2-128">Анализ пользователей, сеансов и событий в Application Insights</span><span class="sxs-lookup"><span data-stu-id="27cd2-128">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
  * [<span data-ttu-id="27cd2-129">Сохранение</span><span class="sxs-lookup"><span data-stu-id="27cd2-129">Retention</span></span>](app-insights-usage-retention.md)
  * [<span data-ttu-id="27cd2-130">Книги</span><span class="sxs-lookup"><span data-stu-id="27cd2-130">Workbooks</span></span>](app-insights-usage-workbooks.md)
  * [<span data-ttu-id="27cd2-131">Добавление контекста пользователей</span><span class="sxs-lookup"><span data-stu-id="27cd2-131">Add user context</span></span>](app-insights-usage-send-user-context.md)
