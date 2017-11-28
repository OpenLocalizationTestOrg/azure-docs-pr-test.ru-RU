---
title: "исчерпывающий обзор планы службы приложений aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="2b259-104">Подробный обзор планов службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="2b259-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="2b259-105">Планы служб приложений представляют коллекцию hello toohost физические ресурсы, используемые приложения.</span><span class="sxs-lookup"><span data-stu-id="2b259-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="2b259-106">Планы службы приложений определяют такие компоненты:</span><span class="sxs-lookup"><span data-stu-id="2b259-106">App Service plans define:</span></span>

- <span data-ttu-id="2b259-107">регион ("Западная часть США", "Восточная часть США" и т. д.);</span><span class="sxs-lookup"><span data-stu-id="2b259-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="2b259-108">уровень масштабирования (один, два, три экземпляра и т. д.);</span><span class="sxs-lookup"><span data-stu-id="2b259-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="2b259-109">размер экземпляра (небольшой, средний, крупный);</span><span class="sxs-lookup"><span data-stu-id="2b259-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="2b259-110">SKU ("Бесплатный", "Общий", "Базовый", "Стандартный", "Премиум").</span><span class="sxs-lookup"><span data-stu-id="2b259-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="2b259-111">В рамках плана службы приложений Azure доступны все веб-приложения, мобильные приложения, приложения API и приложения-функции (или "Функции"), входящие в состав [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="2b259-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="2b259-112">Приложения в hello ту же подписку и регион могут совместно использовать план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="2b259-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="2b259-113">Все приложения назначенный tooan **план служб приложений** общий доступ к ресурсам hello, определяемое.</span><span class="sxs-lookup"><span data-stu-id="2b259-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="2b259-114">Поэтому, разместив несколько приложений в одном плане службы приложений, вы сможете сэкономить.</span><span class="sxs-lookup"><span data-stu-id="2b259-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="2b259-115">Ваш **план служб приложений** можно масштабировать от **Free** и **Shared** SKU слишком**основные**, **Стандартная**, и **Premium** SKU, предоставляя доступ к toomore ресурсы и компоненты вдоль hello способом.</span><span class="sxs-lookup"><span data-stu-id="2b259-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="2b259-116">Если план служб приложений задано слишком**основные** SKU или более поздней версии, а затем можно управлять hello **размер** и масштабировать количество hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="2b259-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="2b259-117">Например ваш план равен «small» экземпляров настроенного toouse два уровня службы standard hello, все приложения, которые связаны с этим планом, запустите на обоих экземплярах.</span><span class="sxs-lookup"><span data-stu-id="2b259-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="2b259-118">Приложения также имеют доступа к функциям уровня службы standard toohello.</span><span class="sxs-lookup"><span data-stu-id="2b259-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="2b259-119">Экземпляры плана, на которых выполняются приложения, являются полностью управляемыми и высокодоступными.</span><span class="sxs-lookup"><span data-stu-id="2b259-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b259-120">Hello **SKU** и **шкалы** hello службы приложений план определяет hello затрат и не hello число приложений, размещенных в нем.</span><span class="sxs-lookup"><span data-stu-id="2b259-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="2b259-121">В этой статье исследуются hello ключевые характеристики, например уровень масштаба план службы приложений и как их следует учитывать при управлении приложений.</span><span class="sxs-lookup"><span data-stu-id="2b259-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="2b259-122">Приложения и планы службы приложений</span><span class="sxs-lookup"><span data-stu-id="2b259-122">Apps and App Service plans</span></span>

<span data-ttu-id="2b259-123">Приложение службы приложений в конкретный момент времени может быть сопоставлено лишь с одним планом службы приложений.</span><span class="sxs-lookup"><span data-stu-id="2b259-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="2b259-124">Как приложения, так и планы находятся в **группе ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="2b259-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="2b259-125">Группа ресурсов выступает в качестве границ hello жизненного цикла для каждого ресурса, который находится в пределах его.</span><span class="sxs-lookup"><span data-stu-id="2b259-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="2b259-126">Можно использовать toomanage группы ресурсов всех компонентов приложения hello вместе.</span><span class="sxs-lookup"><span data-stu-id="2b259-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="2b259-127">Поскольку единой группы ресурсов может быть несколько планов служб приложений, можно выделить различные приложения toodifferent физических ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2b259-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="2b259-128">Например, можно разделить ресурсы между средами разработки, тестирования и производства.</span><span class="sxs-lookup"><span data-stu-id="2b259-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="2b259-129">Наличие отдельных сред для выполнения рабочих процессов, а также процессов разработки и тестирования позволяет изолировать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2b259-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="2b259-130">Таким образом, нагрузочное тестирование выполняется для новой версии приложения не конкурируют за hello же ресурсов, сколько приложений производства, которые должны работать с обычными пользователями.</span><span class="sxs-lookup"><span data-stu-id="2b259-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="2b259-131">Наличие нескольких планов в одной группе ресурсов позволяет создавать приложения, которые охватывают несколько географических регионов.</span><span class="sxs-lookup"><span data-stu-id="2b259-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="2b259-132">Например, высокодоступное приложение, запущенное в двух регионах, будет включать по крайней мере два плана — по одному для каждого региона, при этом каждый план будет сопоставлен с одним приложением.</span><span class="sxs-lookup"><span data-stu-id="2b259-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="2b259-133">В таком случае все копии hello приложение hello затем содержатся в единой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2b259-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="2b259-134">Наличие группы ресурсов с несколькими планами и нескольких приложений делает его легко toomanage, управления и представление работоспособности hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2b259-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="2b259-135">Создание плана службы приложений или использование имеющегося</span><span class="sxs-lookup"><span data-stu-id="2b259-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="2b259-136">При создании приложения мы рекомендуем создавать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2b259-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="2b259-137">На hello другой стороны, если это приложение — это компонент для более крупного приложения, создайте его в группе ресурсов hello, выделенный для этого приложения большего размера.</span><span class="sxs-lookup"><span data-stu-id="2b259-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="2b259-138">Является ли приложение hello полностью нового приложения или частью большой, вы можете toouse существующего плана toohost его или создать новую.</span><span class="sxs-lookup"><span data-stu-id="2b259-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="2b259-139">Это решение, скорее, вопрос емкости и ожидаемой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2b259-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="2b259-140">Мы рекомендуем изолировать приложение посредством нового плана службы приложений в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="2b259-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="2b259-141">Приложение является ресурсоемким.</span><span class="sxs-lookup"><span data-stu-id="2b259-141">App is resource-intensive.</span></span>
- <span data-ttu-id="2b259-142">Приложение имеет разные коэффициенты масштабирования из hello другие приложения, размещенные в существующий план.</span><span class="sxs-lookup"><span data-stu-id="2b259-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="2b259-143">Приложению требуется ресурс из другого географического региона.</span><span class="sxs-lookup"><span data-stu-id="2b259-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="2b259-144">Таким образом можно выделить новый набор ресурсов для приложения и усилить контроль над своими приложениями.</span><span class="sxs-lookup"><span data-stu-id="2b259-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="2b259-145">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="2b259-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="2b259-146">При наличии среды службы приложений можно просмотреть hello документации конкретного tooApp среды службы здесь: [создать план служб приложений в среде службы приложений](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="2b259-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="2b259-147">Можно создать пустой план служб приложений из hello интерфейс плана служб приложений или как часть создания приложения.</span><span class="sxs-lookup"><span data-stu-id="2b259-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="2b259-148">В hello [портал Azure](https://portal.azure.com), нажмите кнопку **New** > **Интернет + мобильные устройства**и выберите **веб-приложение** или в другом типе приложений служб приложений.</span><span class="sxs-lookup"><span data-stu-id="2b259-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Создайте приложение в hello портал Azure.][createWebApp]

<span data-ttu-id="2b259-150">Затем можно выбрать или создать план служб приложений для нового приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="2b259-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![Создание плана службы приложений.][createASP]

<span data-ttu-id="2b259-152">Щелкните toocreate план служб приложений **[+] создать новые**, тип hello **план служб приложений** имя, а затем выберите соответствующий **расположение**.</span><span class="sxs-lookup"><span data-stu-id="2b259-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="2b259-153">Нажмите кнопку **Ценовая категория**, а затем выберите соответствующий ценовую категорию для службы hello.</span><span class="sxs-lookup"><span data-stu-id="2b259-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="2b259-154">Выберите **просмотреть все** tooview более цены параметры, такие как **Free** и **Shared**.</span><span class="sxs-lookup"><span data-stu-id="2b259-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="2b259-155">После того как выбрана hello ценовой категории, нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="2b259-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="2b259-156">Переместить в другой план служб приложений приложения tooa</span><span class="sxs-lookup"><span data-stu-id="2b259-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="2b259-157">Перемещении другой план служб приложений приложения tooa hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b259-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2b259-158">Приложения можно перемещать между планы, при условии, что hello планов находятся в hello же группу ресурсов и географического региона.</span><span class="sxs-lookup"><span data-stu-id="2b259-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="2b259-159">toomove план tooanother приложения:</span><span class="sxs-lookup"><span data-stu-id="2b259-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="2b259-160">Перейдите toohello приложение, которое следует toomove.</span><span class="sxs-lookup"><span data-stu-id="2b259-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="2b259-161">В hello **меню**, найдите hello **план служб приложений** раздела.</span><span class="sxs-lookup"><span data-stu-id="2b259-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="2b259-162">Выберите **план служб приложений изменение** toostart hello процесса.</span><span class="sxs-lookup"><span data-stu-id="2b259-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="2b259-163">**Изменить план служб приложений** hello откроется **план служб приложений** селектора.</span><span class="sxs-lookup"><span data-stu-id="2b259-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="2b259-164">На этом этапе можно выбрать существующий план toomove в это приложение.</span><span class="sxs-lookup"><span data-stu-id="2b259-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b259-165">Выберите план служб приложений пользовательского интерфейса Hello фильтруется по hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="2b259-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="2b259-166">Существует в пределах hello же группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="2b259-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="2b259-167">Существует hello же географического региона</span><span class="sxs-lookup"><span data-stu-id="2b259-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="2b259-168">Существует в пределах hello же веб-пространство</span><span class="sxs-lookup"><span data-stu-id="2b259-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="2b259-169">Веб-пространство — это логическая конструкция внутри службы приложений, которая определяет группирование ресурсов сервера.</span><span class="sxs-lookup"><span data-stu-id="2b259-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="2b259-170">Географический регион (например, Запад США) содержит множество веб-пространств в порядке tooallocate клиентов, использующих службы приложений.</span><span class="sxs-lookup"><span data-stu-id="2b259-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="2b259-171">В настоящее время ресурсы службы приложений не может toobe, перемещать между веб-пространства.</span><span class="sxs-lookup"><span data-stu-id="2b259-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![Селектор планов службы приложений.][change]

<span data-ttu-id="2b259-173">Каждый план имеет свою ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="2b259-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="2b259-174">Например перемещение сайта из уровня Standard tooa бесплатный уровень, включает все приложения, назначенные tooit toouse hello компоненты и ресурсы уровня Standard hello.</span><span class="sxs-lookup"><span data-stu-id="2b259-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="2b259-175">Клонирование другой план служб приложений приложения tooa</span><span class="sxs-lookup"><span data-stu-id="2b259-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="2b259-176">Если требуется другой регион приложения hello tooa toomove, один из вариантов — приложение клонирования.</span><span class="sxs-lookup"><span data-stu-id="2b259-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="2b259-177">Клонирование позволяет создавать копии приложения в новом или имеющемся плане служб приложений в любом регионе.</span><span class="sxs-lookup"><span data-stu-id="2b259-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="2b259-178">Можно найти **клонирование приложений** в hello **средства разработки** части меню hello.</span><span class="sxs-lookup"><span data-stu-id="2b259-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b259-179">Клонирование имеет некоторые ограничения, о которых можно узнать из статьи [Клонирование приложений службы приложений Azure с помощью портала Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2b259-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="2b259-180">Масштабирование плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="2b259-180">Scale an App Service plan</span></span>

<span data-ttu-id="2b259-181">Существует три способа tooscale план.</span><span class="sxs-lookup"><span data-stu-id="2b259-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="2b259-182">**Изменение плана hello в ценовой категории**.</span><span class="sxs-lookup"><span data-stu-id="2b259-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="2b259-183">Все приложения назначенный tooit toouse hello функции уровня Standard hello плана в базовый уровень hello может быть преобразованный tooStandard</span><span class="sxs-lookup"><span data-stu-id="2b259-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="2b259-184">**Измените размер экземпляра плана hello**.</span><span class="sxs-lookup"><span data-stu-id="2b259-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="2b259-185">Например план на уровне Basic hello, который используется небольшого экземпляров может быть измененные toouse больших экземпляров.</span><span class="sxs-lookup"><span data-stu-id="2b259-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="2b259-186">Все приложения, которые связаны с этим планом, теперь можно использовать hello дополнительной памяти и ресурсов ЦП, hello большего размера предложения размер экземпляра.</span><span class="sxs-lookup"><span data-stu-id="2b259-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="2b259-187">**Измените число экземпляров плана hello**.</span><span class="sxs-lookup"><span data-stu-id="2b259-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="2b259-188">Например план Standard, масштабировать toothree экземпляров может быть масштабированный too10 экземпляров.</span><span class="sxs-lookup"><span data-stu-id="2b259-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="2b259-189">План "премиум" допускает масштабирование экземпляров too20 (tooavailability субъекта).</span><span class="sxs-lookup"><span data-stu-id="2b259-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="2b259-190">Все приложения, которые связаны с этим планом, теперь можно использовать hello дополнительной памяти и ресурсов ЦП, hello большего размера предложения экземпляр счетчика.</span><span class="sxs-lookup"><span data-stu-id="2b259-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="2b259-191">Вы можете изменить ценовой уровень и экземпляр размера, щелкнув hello hello **масштабирования вверх** элемента с настройками для приложение hello или hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="2b259-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="2b259-192">Изменения применяются toohello план служб приложений и влияют на все приложения, размещенными на нем.</span><span class="sxs-lookup"><span data-stu-id="2b259-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![Задайте значения tooscale копии приложения.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="2b259-194">Удаление плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="2b259-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b259-195">**Планы служб приложений** , имеющие не toothem приложений, связанных взиматься плата, так как они по-прежнему tooreserve hello вычислительная мощность.</span><span class="sxs-lookup"><span data-stu-id="2b259-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="2b259-196">tooavoid Непредвиденная накладных расходов при удалении hello последнего приложения, размещенного в план служб приложений hello полученный пустой план служб приложений, также будет удален.</span><span class="sxs-lookup"><span data-stu-id="2b259-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="2b259-197">Сводка</span><span class="sxs-lookup"><span data-stu-id="2b259-197">Summary</span></span>

<span data-ttu-id="2b259-198">Планы службы приложений представляют собой набор компонентов и возможностей, которые доступны всем приложениям.</span><span class="sxs-lookup"><span data-stu-id="2b259-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="2b259-199">Службы приложений планов Подождите hello гибкость tooallocate конкретных приложений tooa набор ресурсов и дополнительно оптимизировать использование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="2b259-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="2b259-200">Таким образом, если требуется toosave денег на тестовой среды, можно предоставить план для нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="2b259-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="2b259-201">Можно также увеличить пропускную способность для рабочей среды путем ее масштабирования в рамках нескольких регионов и планов.</span><span class="sxs-lookup"><span data-stu-id="2b259-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="2b259-202">Изменения</span><span class="sxs-lookup"><span data-stu-id="2b259-202">What's changed</span></span>

- <span data-ttu-id="2b259-203">Руководство по toohello изменений из tooApp веб-сайтов службы, см.: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="2b259-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
