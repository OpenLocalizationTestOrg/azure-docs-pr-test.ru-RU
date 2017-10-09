---
title: "Реализация мобильного охвата aaaAzure для игр приложения"
description: "Игры tooimplement сценарий приложения Azure Mobile Engagement"
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
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="54ea4-103">Реализация Служб мобильного взаимодействия в игровом приложении</span><span class="sxs-lookup"><span data-stu-id="54ea4-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="54ea4-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="54ea4-104">Overview</span></span>
<span data-ttu-id="54ea4-105">Игровой стартап запустил новое игровое приложение про рыбалку на базе ролей/стратегии.</span><span class="sxs-lookup"><span data-stu-id="54ea4-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="54ea4-106">Игра Hello был запущен и работает за 6 месяцев.</span><span class="sxs-lookup"><span data-stu-id="54ea4-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="54ea4-107">Эта игра является огромным Успех и он имеет миллионы файлы для загрузки и хранения hello является очень высокая сравниваемых tooother при запуске игры приложений.</span><span class="sxs-lookup"><span data-stu-id="54ea4-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="54ea4-108">В hello квартальные собрание, заинтересованные лица соглашаюсь с тем, они должны tooincrease средний доход на пользователя (ARPU).</span><span class="sxs-lookup"><span data-stu-id="54ea4-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="54ea4-109">Премиум-пакеты в игре доступны как специальные предложения.</span><span class="sxs-lookup"><span data-stu-id="54ea4-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="54ea4-110">Эти игры пакеты позволяют пользователям tooupgrade hello, внешний вид и производительность их рыбалка строк и наживок или tackles в игре hello.</span><span class="sxs-lookup"><span data-stu-id="54ea4-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="54ea4-111">Однако продажи пакета очень низкие.</span><span class="sxs-lookup"><span data-stu-id="54ea4-111">However, package sales are very low.</span></span> <span data-ttu-id="54ea4-112">Чтобы члены команды принимают решение первый tooanalyze hello качества программного обеспечения с помощью средства аналитики, и затем toodevelop engagement программы tooincrease продаж с помощью расширенная сегментации.</span><span class="sxs-lookup"><span data-stu-id="54ea4-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="54ea4-113">В зависимости от hello [Azure Mobile Engagement - руководство по началу работы с рекомендациями](mobile-engagement-getting-started-best-practices.md) разработки стратегии обязательств.</span><span class="sxs-lookup"><span data-stu-id="54ea4-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="54ea4-114">Цели и ключевые показатели эффективности</span><span class="sxs-lookup"><span data-stu-id="54ea4-114">Objectives and KPIs</span></span>
<span data-ttu-id="54ea4-115">Соответствует ключевых заинтересованных лиц для hello игры.</span><span class="sxs-lookup"><span data-stu-id="54ea4-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="54ea4-116">Согласовать один основной целью - tooincrease premium пакета продажи по 15%.</span><span class="sxs-lookup"><span data-stu-id="54ea4-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="54ea4-117">Они создают toomeasure бизнеса ключевые показатели эффективности (KPI) и диск этой цели</span><span class="sxs-lookup"><span data-stu-id="54ea4-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="54ea4-118">На каком уровне игры hello приобретаемые эти пакеты?</span><span class="sxs-lookup"><span data-stu-id="54ea4-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="54ea4-119">Что такое hello доход на пользователя, сеанса, раз в неделю и месяц?</span><span class="sxs-lookup"><span data-stu-id="54ea4-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="54ea4-120">Что такое типы hello избранные покупки?</span><span class="sxs-lookup"><span data-stu-id="54ea4-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="54ea4-121">Часть 1 из hello [руководство по началу работы](mobile-engagement-getting-started-best-practices.md) объясняет, как toodefine hello целями и ключевые показатели эффективности.</span><span class="sxs-lookup"><span data-stu-id="54ea4-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="54ea4-122">С hello, теперь заданных ключевых показателей эффективности организации hello Mobile продукта Manager создает ключевые показатели эффективности Engagement toodetermine новый пользователь тенденции и хранения.</span><span class="sxs-lookup"><span data-stu-id="54ea4-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="54ea4-123">Мониторинг хранения и использовать в Привет следующие интервалы: ежедневно, каждые 2 дня, еженедельно, ежемесячно и каждые 3 месяца</span><span class="sxs-lookup"><span data-stu-id="54ea4-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="54ea4-124">Количество активных пользователей</span><span class="sxs-lookup"><span data-stu-id="54ea4-124">Active user counts</span></span>
* <span data-ttu-id="54ea4-125">Рейтинг приложения Hello в hello хранения</span><span class="sxs-lookup"><span data-stu-id="54ea4-125">hello app rating in hello store</span></span>

<span data-ttu-id="54ea4-126">На основе рекомендаций из hello ИТ-отдела, следующие технические ключевые показатели эффективности hello были добавлены hello tooanswer следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="54ea4-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="54ea4-127">путь пользователя (посещаемая страница, количество времени, которые пользователи тратят на ее просмотр);</span><span class="sxs-lookup"><span data-stu-id="54ea4-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="54ea4-128">количество сбоев или ошибок на сеанс;</span><span class="sxs-lookup"><span data-stu-id="54ea4-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="54ea4-129">версии операционных систем, используемые пользователями;</span><span class="sxs-lookup"><span data-stu-id="54ea4-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="54ea4-130">Что такое hello Средний размер экрана для моих пользователей?</span><span class="sxs-lookup"><span data-stu-id="54ea4-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="54ea4-131">тип подключения к Интернету, используемый пользователями.</span><span class="sxs-lookup"><span data-stu-id="54ea4-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="54ea4-132">Для каждого ключевого индикатора Производительности hello диспетчера продукта мобильных указывает данные hello ей и где он находится в ее репертуара.</span><span class="sxs-lookup"><span data-stu-id="54ea4-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="54ea4-133">Программа привлечения и интеграция</span><span class="sxs-lookup"><span data-stu-id="54ea4-133">Engagement program and integration</span></span>
<span data-ttu-id="54ea4-134">Перед построением программе дополнительные участия, hello директору проекта Mobile, ответственный за hello проекта должны иметь глубокого понимания потребляемых как и когда пользователи hello продуктов.</span><span class="sxs-lookup"><span data-stu-id="54ea4-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="54ea4-135">После 3 месяца hello директору проекта Mobile собрал tooenhance недостаточно данных его продаж уведомлений push в приложении.</span><span class="sxs-lookup"><span data-stu-id="54ea4-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="54ea4-136">Он узнал, что:</span><span class="sxs-lookup"><span data-stu-id="54ea4-136">He learns that:</span></span>

* <span data-ttu-id="54ea4-137">Hello первой покупки, обычно происходит на уровне hello 14.</span><span class="sxs-lookup"><span data-stu-id="54ea4-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="54ea4-138">90% из таких случаев покупки hello называется новый легендарного оружие для $3.</span><span class="sxs-lookup"><span data-stu-id="54ea4-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="54ea4-139">В 80% этих вариантов пользователей, которые были внесены покупку, продолжите hello продукта и делать покупки.</span><span class="sxs-lookup"><span data-stu-id="54ea4-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="54ea4-140">Пользователи, которые прошли hello уровень 20, запустите toospend более 10 долларов в неделю.</span><span class="sxs-lookup"><span data-stu-id="54ea4-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="54ea4-141">Пользователи, как правило, пакеты toobuy premium на уровне 16, 24 и 32.</span><span class="sxs-lookup"><span data-stu-id="54ea4-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="54ea4-142">Благодарим вас toothis анализа hello директору проекта Mobile решает tooincrease последовательности toocreate определенных извещающих уведомлений приложения продаж.</span><span class="sxs-lookup"><span data-stu-id="54ea4-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="54ea4-143">Он создает три серии push-уведомлений, которые он называет: "Программа приветствия", "Программа продаж" и "Программа неактивности".</span><span class="sxs-lookup"><span data-stu-id="54ea4-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="54ea4-144">Дополнительные сведения см. в разделе toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="54ea4-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
