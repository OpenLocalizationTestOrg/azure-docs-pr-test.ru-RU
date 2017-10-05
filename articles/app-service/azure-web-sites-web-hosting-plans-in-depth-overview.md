---
title: "Подробный обзор планов службы приложений Azure | Документация Майкрософт"
description: "Узнайте, как работают планы службы приложений Azure и чем они удобны для вашей среды управления."
keywords: "служба приложений, служба приложений azure, масштабировать, масштабируемый, план службы приложений, стоимость службы приложений"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="5a365-104">Подробный обзор планов службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="5a365-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="5a365-105">Планы службы приложений представляют собой коллекцию физических ресурсов, используемых для размещения приложений.</span><span class="sxs-lookup"><span data-stu-id="5a365-105">App Service plans represent the collection of physical resources used to host your apps.</span></span>

<span data-ttu-id="5a365-106">Планы службы приложений определяют такие компоненты:</span><span class="sxs-lookup"><span data-stu-id="5a365-106">App Service plans define:</span></span>

- <span data-ttu-id="5a365-107">регион ("Западная часть США", "Восточная часть США" и т. д.);</span><span class="sxs-lookup"><span data-stu-id="5a365-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="5a365-108">уровень масштабирования (один, два, три экземпляра и т. д.);</span><span class="sxs-lookup"><span data-stu-id="5a365-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="5a365-109">размер экземпляра (небольшой, средний, крупный);</span><span class="sxs-lookup"><span data-stu-id="5a365-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="5a365-110">SKU ("Бесплатный", "Общий", "Базовый", "Стандартный", "Премиум").</span><span class="sxs-lookup"><span data-stu-id="5a365-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="5a365-111">В рамках плана службы приложений Azure доступны все веб-приложения, мобильные приложения, приложения API и приложения-функции (или "Функции"), входящие в состав [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="5a365-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="5a365-112">Приложения в одной подписке и регионе могут совместно использовать план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5a365-112">Apps in the same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="5a365-113">Все приложения, назначенные **плану службы приложений**, совместно используют ресурсы, определенные в нем.</span><span class="sxs-lookup"><span data-stu-id="5a365-113">All applications assigned to an **App Service plan** share the resources defined by it.</span></span> <span data-ttu-id="5a365-114">Поэтому, разместив несколько приложений в одном плане службы приложений, вы сможете сэкономить.</span><span class="sxs-lookup"><span data-stu-id="5a365-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="5a365-115">Ваши **планы службы приложения** предусматривают масштабирование от номеров SKU **Бесплатный** и **Общий** до **Базовый**, **Стандартный** и **Премиум**, обеспечивая доступ к дополнительным ресурсам и функциям во время работы.</span><span class="sxs-lookup"><span data-stu-id="5a365-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span></span>

<span data-ttu-id="5a365-116">Если для вашего плана службы приложений задан SKU **Базовый** или выше, то вы можете контролировать **размер** и уровень масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a365-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span></span>

<span data-ttu-id="5a365-117">Например, если план настроен для использования двух небольших экземпляров уровня "Стандартный", то все приложения, связанные с этим планом, выполняются на обоих экземплярах.</span><span class="sxs-lookup"><span data-stu-id="5a365-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="5a365-118">Приложения также имеют доступ к функциям уровня служб "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="5a365-118">Apps also have access to the standard service tier features.</span></span> <span data-ttu-id="5a365-119">Экземпляры плана, на которых выполняются приложения, являются полностью управляемыми и высокодоступными.</span><span class="sxs-lookup"><span data-stu-id="5a365-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a365-120">**Номер SKU** и **масштаб** плана службы приложений определяют стоимость, а не число приложений, размещенных в нем.</span><span class="sxs-lookup"><span data-stu-id="5a365-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span></span>

<span data-ttu-id="5a365-121">В этой статье рассматриваются ключевые характеристики плана службы приложений, такие как ценовая категория и масштаб, а также их роль в управлении вашими приложениями.</span><span class="sxs-lookup"><span data-stu-id="5a365-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="5a365-122">Приложения и планы службы приложений</span><span class="sxs-lookup"><span data-stu-id="5a365-122">Apps and App Service plans</span></span>

<span data-ttu-id="5a365-123">Приложение службы приложений в конкретный момент времени может быть сопоставлено лишь с одним планом службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5a365-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="5a365-124">Как приложения, так и планы находятся в **группе ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="5a365-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="5a365-125">Группа ресурсов определяет пределы жизненного цикла для каждого содержащегося в ней ресурса.</span><span class="sxs-lookup"><span data-stu-id="5a365-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="5a365-126">Группы ресурсов помогают управлять всеми частями приложения в комплексе.</span><span class="sxs-lookup"><span data-stu-id="5a365-126">You can use resource groups to manage all the pieces of an application together.</span></span>

<span data-ttu-id="5a365-127">Так как одна группа ресурсов могут включать несколько планов службы приложений, вы можете назначать разным приложениям разные физические ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5a365-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span></span>

<span data-ttu-id="5a365-128">Например, можно разделить ресурсы между средами разработки, тестирования и производства.</span><span class="sxs-lookup"><span data-stu-id="5a365-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="5a365-129">Наличие отдельных сред для выполнения рабочих процессов, а также процессов разработки и тестирования позволяет изолировать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5a365-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="5a365-130">В таком случае нагрузочное тестирование новой версии вашего приложения не будет конкурировать за одни и те же ресурсы с рабочим приложением, которое отвечает за обслуживание реальных клиентов.</span><span class="sxs-lookup"><span data-stu-id="5a365-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="5a365-131">Наличие нескольких планов в одной группе ресурсов позволяет создавать приложения, которые охватывают несколько географических регионов.</span><span class="sxs-lookup"><span data-stu-id="5a365-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="5a365-132">Например, высокодоступное приложение, запущенное в двух регионах, будет включать по крайней мере два плана — по одному для каждого региона, при этом каждый план будет сопоставлен с одним приложением.</span><span class="sxs-lookup"><span data-stu-id="5a365-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="5a365-133">В этом случае все копии приложения будут находиться в одной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a365-133">In such a situation, all the copies of the app are then contained in a single resource group.</span></span> <span data-ttu-id="5a365-134">Наличие группы ресурсов с несколькими планами и несколькими приложениями облегчает проверку и просмотр состояния приложения, а также управление им.</span><span class="sxs-lookup"><span data-stu-id="5a365-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="5a365-135">Создание плана службы приложений или использование имеющегося</span><span class="sxs-lookup"><span data-stu-id="5a365-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="5a365-136">При создании приложения мы рекомендуем создавать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a365-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="5a365-137">С другой стороны, если приложение будет компонентом более крупного решения, создайте его в группе ресурсов, которая выделена для крупного приложения.</span><span class="sxs-lookup"><span data-stu-id="5a365-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="5a365-138">Приложение может быть как независимым решением, так и частью более крупного приложения. Важно то, что для его размещения вы можете выбрать существующий план или создать новый.</span><span class="sxs-lookup"><span data-stu-id="5a365-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span></span> <span data-ttu-id="5a365-139">Это решение, скорее, вопрос емкости и ожидаемой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5a365-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="5a365-140">Мы рекомендуем изолировать приложение посредством нового плана службы приложений в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="5a365-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="5a365-141">Приложение является ресурсоемким.</span><span class="sxs-lookup"><span data-stu-id="5a365-141">App is resource-intensive.</span></span>
- <span data-ttu-id="5a365-142">Масштабирование приложения зависит от других приложений, размещенных в существующем плане.</span><span class="sxs-lookup"><span data-stu-id="5a365-142">App has different scaling factors from the other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="5a365-143">Приложению требуется ресурс из другого географического региона.</span><span class="sxs-lookup"><span data-stu-id="5a365-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="5a365-144">Таким образом можно выделить новый набор ресурсов для приложения и усилить контроль над своими приложениями.</span><span class="sxs-lookup"><span data-stu-id="5a365-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="5a365-145">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5a365-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="5a365-146">Документацию по определенной среде службы приложений см. в разделе [Создание плана службы приложений](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan).</span><span class="sxs-lookup"><span data-stu-id="5a365-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="5a365-147">План службы приложений можно создать отдельно с помощью средства просмотра плана службы приложений или же при создании приложения.</span><span class="sxs-lookup"><span data-stu-id="5a365-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="5a365-148">На [портале Azure](https://portal.azure.com) щелкните **Создать** > **Интернет+мобильные устройства**, выберите **Веб-приложение** или другое приложение службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5a365-148">In the [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Создание приложения на портале Azure.][createWebApp]

<span data-ttu-id="5a365-150">Затем можно выбрать или создать план службы приложений для нового приложения.</span><span class="sxs-lookup"><span data-stu-id="5a365-150">You can then select or create the App Service plan for the new app.</span></span>

 ![Создание плана службы приложений.][createASP]

<span data-ttu-id="5a365-152">Чтобы создать план службы приложений, щелкните **+Создать**, введите имя в поле **План службы приложений** и выберите соответствующее **расположение**.</span><span class="sxs-lookup"><span data-stu-id="5a365-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="5a365-153">Щелкните **Ценовая категория**и выберите для службы соответствующую категорию.</span><span class="sxs-lookup"><span data-stu-id="5a365-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="5a365-154">Щелкните **Просмотреть все**, чтобы просмотреть другие варианты тарификации, например **Бесплатный** и **Общий**.</span><span class="sxs-lookup"><span data-stu-id="5a365-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="5a365-155">После выбора ценовой категории нажмите кнопку **Выбрать** .</span><span class="sxs-lookup"><span data-stu-id="5a365-155">After you have selected the pricing tier, click the **Select** button.</span></span>

## <a name="move-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="5a365-156">Перемещение приложения в другой план службы приложений</span><span class="sxs-lookup"><span data-stu-id="5a365-156">Move an app to a different App Service plan</span></span>

<span data-ttu-id="5a365-157">Приложения можно переместить в другой план службы приложений на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a365-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5a365-158">Приложения можно перемещать между планами, если планы находятся в одной группе ресурсов и в одном географическом регионе.</span><span class="sxs-lookup"><span data-stu-id="5a365-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span></span>

<span data-ttu-id="5a365-159">Чтобы переместить приложение в другой план, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5a365-159">To move an app to another plan:</span></span>

- <span data-ttu-id="5a365-160">Перейдите к приложению, которое требуется переместить.</span><span class="sxs-lookup"><span data-stu-id="5a365-160">Navigate to the app that you want to move.</span></span>
- <span data-ttu-id="5a365-161">В **меню** найдите раздел **План службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="5a365-161">In the **Menu**, look for the **App Service Plan** section.</span></span>
- <span data-ttu-id="5a365-162">Чтобы начать процесс, выберите **Изменить план служб приложений**.</span><span class="sxs-lookup"><span data-stu-id="5a365-162">Select **Change App Service plan** to start the process.</span></span>

<span data-ttu-id="5a365-163">Щелкнув **Изменить план служб приложений**, вы откроете средство выбора **План службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="5a365-163">**Change App Service plan** opens the **App Service plan** selector.</span></span> <span data-ttu-id="5a365-164">На этом этапе можно выбрать существующий план, в который следует переместить приложение.</span><span class="sxs-lookup"><span data-stu-id="5a365-164">At this point, you can pick an existing plan to move this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a365-165">Пользовательский интерфейса выбора плана службы приложений фильтруется по следующим критериям:</span><span class="sxs-lookup"><span data-stu-id="5a365-165">The select App Service plan UI is filtered by the following criteria:</span></span>
> - <span data-ttu-id="5a365-166">Существует в той же группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="5a365-166">Exists within the same Resource Group</span></span>
> - <span data-ttu-id="5a365-167">Существует в том же географическом регионе</span><span class="sxs-lookup"><span data-stu-id="5a365-167">Exists in the same Geographical Region</span></span>
> - <span data-ttu-id="5a365-168">Существует в том же веб-пространстве</span><span class="sxs-lookup"><span data-stu-id="5a365-168">Exists within the same Webspace</span></span>
>
> <span data-ttu-id="5a365-169">Веб-пространство — это логическая конструкция внутри службы приложений, которая определяет группирование ресурсов сервера.</span><span class="sxs-lookup"><span data-stu-id="5a365-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="5a365-170">Географический регион (например западная часть США) содержит много веб-пространств для выделения клиентов с помощью службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5a365-170">A Geographical region (such as West US) contains many Webspaces in order to allocate customers using App Service.</span></span> <span data-ttu-id="5a365-171">В настоящее время ресурсы службы приложений не могут перемещаться между веб-пространствами.</span><span class="sxs-lookup"><span data-stu-id="5a365-171">Currently, App Service resources aren’t able to be moved between Webspaces.</span></span>
>

![Селектор планов службы приложений.][change]

<span data-ttu-id="5a365-173">Каждый план имеет свою ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="5a365-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="5a365-174">Например, при изменении уровня сайта с "Бесплатный" на "Стандартный" все назначенные ему приложения получат доступ к функциям и ресурсам уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="5a365-174">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span></span>

## <a name="clone-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="5a365-175">Клонирование приложения в другой план служб приложений</span><span class="sxs-lookup"><span data-stu-id="5a365-175">Clone an app to a different App Service plan</span></span>

<span data-ttu-id="5a365-176">Если вы хотите переместить приложение в другой регион, один из вариантов — клонировать его.</span><span class="sxs-lookup"><span data-stu-id="5a365-176">If you want to move the app to a different region, one alternative is app cloning.</span></span> <span data-ttu-id="5a365-177">Клонирование позволяет создавать копии приложения в новом или имеющемся плане служб приложений в любом регионе.</span><span class="sxs-lookup"><span data-stu-id="5a365-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="5a365-178">Команда **Клонировать приложение** находится в разделе **Средства разработки** меню.</span><span class="sxs-lookup"><span data-stu-id="5a365-178">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a365-179">Клонирование имеет некоторые ограничения, о которых можно узнать из статьи [Клонирование приложений службы приложений Azure с помощью портала Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a365-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="5a365-180">Масштабирование плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5a365-180">Scale an App Service plan</span></span>

<span data-ttu-id="5a365-181">Существует три способа масштабирования плана.</span><span class="sxs-lookup"><span data-stu-id="5a365-181">There are three ways to scale a plan:</span></span>

- <span data-ttu-id="5a365-182">**Изменение ценовой категории плана.**</span><span class="sxs-lookup"><span data-stu-id="5a365-182">**Change the plan’s pricing tier**.</span></span> <span data-ttu-id="5a365-183">План на уровне "Базовый" можно преобразовывать в план уровня "Стандартный", и все приложения, назначенные ему, получат доступ к функциям уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="5a365-183">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span></span>
- <span data-ttu-id="5a365-184">**Изменение размера экземпляров плана**.</span><span class="sxs-lookup"><span data-stu-id="5a365-184">**Change the plan’s instance size**.</span></span> <span data-ttu-id="5a365-185">Например, для плана уровня "Базовый", в рамках которого используются небольшие экземпляры, можно настроить использование крупных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="5a365-185">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span></span> <span data-ttu-id="5a365-186">Все приложения, связанные с этим планом, смогут использовать дополнительные ресурсы ЦП и памяти, предоставляемые более крупными экземплярами.</span><span class="sxs-lookup"><span data-stu-id="5a365-186">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span></span>
- <span data-ttu-id="5a365-187">**Изменение числа экземпляров плана**.</span><span class="sxs-lookup"><span data-stu-id="5a365-187">**Change the plan’s instance count**.</span></span> <span data-ttu-id="5a365-188">Например, масштабированный до трех экземпляров план уровня "Стандартный" можно масштабировать до десяти экземпляров.</span><span class="sxs-lookup"><span data-stu-id="5a365-188">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span></span> <span data-ttu-id="5a365-189">План категории "Премиум" можно масштабировать до 20 экземпляров (при условии доступности).</span><span class="sxs-lookup"><span data-stu-id="5a365-189">A Premium plan can be scaled out to 20 instances (subject to availability).</span></span> <span data-ttu-id="5a365-190">Все приложения, связанные с этим планом, смогут использовать дополнительные ресурсы ЦП и памяти, предоставляемые большему количеству экземпляров.</span><span class="sxs-lookup"><span data-stu-id="5a365-190">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span></span>

<span data-ttu-id="5a365-191">Вы можете изменить ценовую категорию и размер экземпляров, щелкнув элемент **Увеличить масштаб** в разделе параметров приложения или плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5a365-191">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span></span> <span data-ttu-id="5a365-192">Изменения будут применены к плану службы приложений и повлияют на все размещенные в нем приложения.</span><span class="sxs-lookup"><span data-stu-id="5a365-192">Changes apply to the App Service plan and affect all apps that it hosts.</span></span>

 ![Установка значений для увеличения масштаба приложения.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="5a365-194">Удаление плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5a365-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a365-195">За **планы службы приложений**, с которыми не связаны приложения, по-прежнему взимается плата, так как они продолжают резервировать вычислительную мощность.</span><span class="sxs-lookup"><span data-stu-id="5a365-195">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span></span>

<span data-ttu-id="5a365-196">Чтобы избежать непредвиденных расходов, после удаления последнего приложения, размещенного в плане службы приложений, также удаляется и пустой план.</span><span class="sxs-lookup"><span data-stu-id="5a365-196">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="5a365-197">Сводка</span><span class="sxs-lookup"><span data-stu-id="5a365-197">Summary</span></span>

<span data-ttu-id="5a365-198">Планы службы приложений представляют собой набор компонентов и возможностей, которые доступны всем приложениям.</span><span class="sxs-lookup"><span data-stu-id="5a365-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="5a365-199">Планы службы приложений позволяют гибко выделять наборы ресурсов для отдельных приложений, оптимизируя использование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5a365-199">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="5a365-200">Например, чтобы снизить затраты на тестовую среду, вы можете использовать один план для нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="5a365-200">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="5a365-201">Можно также увеличить пропускную способность для рабочей среды путем ее масштабирования в рамках нескольких регионов и планов.</span><span class="sxs-lookup"><span data-stu-id="5a365-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="5a365-202">Изменения</span><span class="sxs-lookup"><span data-stu-id="5a365-202">What's changed</span></span>

- <span data-ttu-id="5a365-203">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="5a365-203">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
