---
title: "Воронки Azure Application Insights"
description: "Узнайте, как использовать воронки, чтобы узнать как клиенты взаимодействуют с вашим приложением."
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
ms.openlocfilehash: 59c4dfafc102b26e3b9873f433065715f4aec9ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="b27b0-103">Узнайте, как клиенты используют ваше приложение с помощью воронок Application Insights</span><span class="sxs-lookup"><span data-stu-id="b27b0-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="b27b0-104">Понимание потребностей клиента является важнейшим приоритетом для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="b27b0-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="b27b0-105">Если приложение состоит из нескольких шагов, необходимо узнать, проходит ли большинство клиентов весь процесс или же они прекращают его в какой-то момент.</span><span class="sxs-lookup"><span data-stu-id="b27b0-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="b27b0-106">Продвижение через ряд шагов в веб-приложении называется воронкой.</span><span class="sxs-lookup"><span data-stu-id="b27b0-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="b27b0-107">Воронки Application Insights можно использовать для получения ценной информации о пользователях и пошагового отслеживания коэффициента преобразования.</span><span class="sxs-lookup"><span data-stu-id="b27b0-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="b27b0-108">Начало работы с колонкой "Воронки"</span><span class="sxs-lookup"><span data-stu-id="b27b0-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="b27b0-109">Проще всего ознакомиться с воронками на примере.</span><span class="sxs-lookup"><span data-stu-id="b27b0-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="b27b0-110">На следующей иллюстрации показаны шаги, которые предпримут владельцы компании, занимающейся электронной коммерцией, чтобы узнать, как клиенты взаимодействуют с их веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="b27b0-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="b27b0-111">Создание воронки</span><span class="sxs-lookup"><span data-stu-id="b27b0-111">Create your funnel</span></span>
<span data-ttu-id="b27b0-112">Перед созданием воронки вам нужно решить, на какой вопрос необходимо ответить.</span><span class="sxs-lookup"><span data-stu-id="b27b0-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="b27b0-113">Например, необходимо узнать сколько клиентов, просматривавших вашу домашнюю страницу, щелкнули рекламу.</span><span class="sxs-lookup"><span data-stu-id="b27b0-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="b27b0-114">В этом примере владельцам компании Fabrikam Fiber необходимо узнать процент клиентов, которые совершили покупку после добавления элементов в корзину за последний месяц.</span><span class="sxs-lookup"><span data-stu-id="b27b0-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="b27b0-115">Ниже приведены шаги, которые они выполнили, чтобы создать воронку.</span><span class="sxs-lookup"><span data-stu-id="b27b0-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="b27b0-116">Щелкните "Создать" в колонке "Воронки".</span><span class="sxs-lookup"><span data-stu-id="b27b0-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="b27b0-117">Из раскрывающегося списка **Диапазон времени** выберите диапазон времени "За последний месяц".</span><span class="sxs-lookup"><span data-stu-id="b27b0-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="b27b0-118">В раскрывающемся списке **Step 1** (Шаг 1) выберите событие **Product page** (Страница продукта).</span><span class="sxs-lookup"><span data-stu-id="b27b0-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="b27b0-119">В раскрывающемся списке **Step 2** (Шаг 2) выберите событие **Add to shopping cart** (Добавление в корзину).</span><span class="sxs-lookup"><span data-stu-id="b27b0-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="b27b0-120">В раскрывающемся списке**Step 3** выберите событие **Click purchase** (Щелкнули "Купить").</span><span class="sxs-lookup"><span data-stu-id="b27b0-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="b27b0-121">Назовите воронку и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b27b0-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="b27b0-122">На следующей иллюстрации показаны данные, создаваемые колонкой "Воронки".</span><span class="sxs-lookup"><span data-stu-id="b27b0-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="b27b0-123">Отсюда владельцы Fabrikam могут увидеть, что на прошлой неделе 22,7 % клиентов, добавивших элемент в корзину, завершили покупку.</span><span class="sxs-lookup"><span data-stu-id="b27b0-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="b27b0-124">Кроме того, они видят, что 1 % клиентов щелкнул рекламу перед посещением страницы продукта и 20 % клиентов вышли после совершения покупки.</span><span class="sxs-lookup"><span data-stu-id="b27b0-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Колонка "Воронки" с данными](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="b27b0-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b27b0-126">Next steps</span></span>
  * [<span data-ttu-id="b27b0-127">Общие сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="b27b0-127">Usage overview</span></span>](app-insights-usage-overview.md)
  * [<span data-ttu-id="b27b0-128">Анализ пользователей, сеансов и событий в Application Insights</span><span class="sxs-lookup"><span data-stu-id="b27b0-128">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
  * [<span data-ttu-id="b27b0-129">Сохранение</span><span class="sxs-lookup"><span data-stu-id="b27b0-129">Retention</span></span>](app-insights-usage-retention.md)
  * [<span data-ttu-id="b27b0-130">Книги</span><span class="sxs-lookup"><span data-stu-id="b27b0-130">Workbooks</span></span>](app-insights-usage-workbooks.md)
  * [<span data-ttu-id="b27b0-131">Добавление контекста пользователей</span><span class="sxs-lookup"><span data-stu-id="b27b0-131">Add user context</span></span>](app-insights-usage-send-user-context.md)
