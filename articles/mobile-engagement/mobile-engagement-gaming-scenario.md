---
title: "Реализация Служб мобильного взаимодействия Azure в игровом приложении"
description: "Сценарий для реализации Служб мобильного взаимодействия Azure в игровом приложении."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0ca35a3d634db8eb5c63afacba046a35b8a3e7ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="ff9a7-103">Реализация Служб мобильного взаимодействия в игровом приложении</span><span class="sxs-lookup"><span data-stu-id="ff9a7-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="ff9a7-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ff9a7-104">Overview</span></span>
<span data-ttu-id="ff9a7-105">Игровой стартап запустил новое игровое приложение про рыбалку на базе ролей/стратегии.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="ff9a7-106">Игра работает в течение 6 месяцев.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="ff9a7-107">Она имеет невероятный успех и миллионы скачиваний, а также высокий период удержания по сравнению с другими приложениями игровых стартапов.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="ff9a7-108">На квартальном собрании акционеры согласились, что им нужно увеличить средний доход на пользователя (ARPU).</span><span class="sxs-lookup"><span data-stu-id="ff9a7-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="ff9a7-109">Премиум-пакеты в игре доступны как специальные предложения.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="ff9a7-110">Эти игровые пакеты позволяют обновлять внешний вид и эффективность лески и наживки или снастей в игре.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="ff9a7-111">Однако продажи пакета очень низкие.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-111">However, package sales are very low.</span></span> <span data-ttu-id="ff9a7-112">Поэтому акционеры принимают решение сначала проанализировать впечатления пользователей с помощью средства аналитики и затем разработать программу привлечения для увеличения продаж с помощью расширенной сегментации.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="ff9a7-113">На базе статьи [Службы мобильного взаимодействия Azure. Руководство по началу работы и рекомендации](mobile-engagement-getting-started-best-practices.md) они создали стратегию привлечения.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="ff9a7-114">Цели и ключевые показатели эффективности</span><span class="sxs-lookup"><span data-stu-id="ff9a7-114">Objectives and KPIs</span></span>
<span data-ttu-id="ff9a7-115">Встречаются основные акционеры игры.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="ff9a7-116">Все собравшиеся пришли к согласию относительно основной цели: увеличить уровень продаж премиум-пакета на 15 %.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="ff9a7-117">Кроме этого, на совещании обсудили ключевые показатели эффективности бизнеса, которые позволяют определить коэффициент эффективности и стимулировать достижение цели:</span><span class="sxs-lookup"><span data-stu-id="ff9a7-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="ff9a7-118">На каком уровне игры приобретаются эти пакеты?</span><span class="sxs-lookup"><span data-stu-id="ff9a7-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="ff9a7-119">Каков доход с одного пользователя за сеанс, за неделю и за месяц?</span><span class="sxs-lookup"><span data-stu-id="ff9a7-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="ff9a7-120">Какие типы покупок предпочитают пользователи?</span><span class="sxs-lookup"><span data-stu-id="ff9a7-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="ff9a7-121">Часть 1 из [руководства по началу работы](mobile-engagement-getting-started-best-practices.md) объясняет, как определить цели и ключевые показатели эффективности.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="ff9a7-122">После определения ключевых показателей эффективности организации менеджер по продуктам для мобильных устройств создает ключевые показатели эффективности привлечения для определения тенденций новых пользователей и методов удержания.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="ff9a7-123">Отслеживайте период удержания и используйте через следующие интервалы: ежедневно, каждые 2 дня, еженедельно, ежемесячно и каждые 3 месяца</span><span class="sxs-lookup"><span data-stu-id="ff9a7-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="ff9a7-124">Количество активных пользователей</span><span class="sxs-lookup"><span data-stu-id="ff9a7-124">Active user counts</span></span>
* <span data-ttu-id="ff9a7-125">Оценка приложения в магазине приложений</span><span class="sxs-lookup"><span data-stu-id="ff9a7-125">The app rating in the store</span></span>

<span data-ttu-id="ff9a7-126">Следуя рекомендациям ИТ-отдела, были добавлены следующие технические ключевые показатели эффективности:</span><span class="sxs-lookup"><span data-stu-id="ff9a7-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="ff9a7-127">путь пользователя (посещаемая страница, количество времени, которые пользователи тратят на ее просмотр);</span><span class="sxs-lookup"><span data-stu-id="ff9a7-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="ff9a7-128">количество сбоев или ошибок на сеанс;</span><span class="sxs-lookup"><span data-stu-id="ff9a7-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="ff9a7-129">версии операционных систем, используемые пользователями;</span><span class="sxs-lookup"><span data-stu-id="ff9a7-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="ff9a7-130">средний размер экрана пользователей;</span><span class="sxs-lookup"><span data-stu-id="ff9a7-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="ff9a7-131">тип подключения к Интернету, используемый пользователями.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="ff9a7-132">Для каждого ключевого показателя эффективности менеджер по продуктам для мобильных устройств указывает необходимые данные и их расположение в сборнике тренировочных заданий.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="ff9a7-133">Программа привлечения и интеграция</span><span class="sxs-lookup"><span data-stu-id="ff9a7-133">Engagement program and integration</span></span>
<span data-ttu-id="ff9a7-134">Перед созданием программы расширенного привлечения ответственный за проект руководитель проектов для мобильных устройств должен иметь глубокое понимание того, как и когда продукты используются пользователями.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="ff9a7-135">Через 3 месяца руководитель проектов для мобильных устройств собрал достаточно данных, чтобы улучшить продажи push-уведомлений в приложении.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="ff9a7-136">Он узнал, что:</span><span class="sxs-lookup"><span data-stu-id="ff9a7-136">He learns that:</span></span>

* <span data-ttu-id="ff9a7-137">первая покупка обычно происходит на уровне 14;</span><span class="sxs-lookup"><span data-stu-id="ff9a7-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="ff9a7-138">в 90 % таких случаях приобретается новое легендарное оружие за 3 доллара;</span><span class="sxs-lookup"><span data-stu-id="ff9a7-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="ff9a7-139">в 80 % таких случаев пользователи, сделавшие покупку, продолжают использовать продукт и делать покупки;</span><span class="sxs-lookup"><span data-stu-id="ff9a7-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="ff9a7-140">пользователи, которые прошли уровень 20, начинают тратить более 10 долларов в неделю;</span><span class="sxs-lookup"><span data-stu-id="ff9a7-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="ff9a7-141">пользователи склонны приобретать премиум-пакеты на уровнях 16, 24 и 32.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="ff9a7-142">Благодаря анализу руководитель проектов для мобильных устройств решает создать специальную серию push-уведомлений для увеличения продаж в приложении.</span><span class="sxs-lookup"><span data-stu-id="ff9a7-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="ff9a7-143">Он создает три серии push-уведомлений, которые он называет: "Программа приветствия", "Программа продаж" и "Программа неактивности".</span><span class="sxs-lookup"><span data-stu-id="ff9a7-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="ff9a7-144">Дополнительные сведения см. в [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="ff9a7-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
