---
title: "aaa.NET многоуровневого приложения с помощью Azure Service Bus | Документы Microsoft"
description: "Учебник .NET, в котором помогает разрабатывать приложения для многоуровневых приложений в Azure, которая использует toocommunicate очереди Service Bus между уровнями."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="17350-103">Многоуровневое приложение .NET, использующее очереди служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="17350-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="17350-104">Введение</span><span class="sxs-lookup"><span data-stu-id="17350-104">Introduction</span></span>
<span data-ttu-id="17350-105">Разработка для Microsoft Azure — это простой, с помощью Visual Studio и hello бесплатные Azure SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="17350-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="17350-106">Этот учебник поможет выполнить шаги toocreate hello приложения, использующего несколько ресурсов Azure, работающих в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="17350-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="17350-107">Вы узнаете следующее hello.</span><span class="sxs-lookup"><span data-stu-id="17350-107">You will learn hello following:</span></span>

* <span data-ttu-id="17350-108">Как tooenable компьютера для разработки Azure с одним загрузить и установить.</span><span class="sxs-lookup"><span data-stu-id="17350-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="17350-109">Как toouse toodevelop Visual Studio для Azure.</span><span class="sxs-lookup"><span data-stu-id="17350-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="17350-110">Как toocreate многоуровневого приложения в Azure с помощью веб- и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="17350-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="17350-111">Как toocommunicate между уровнями с использованием очередей Service Bus.</span><span class="sxs-lookup"><span data-stu-id="17350-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="17350-112">В этом учебнике предстоит Постройте и запустите многоуровневого приложения hello в облачной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="17350-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="17350-113">Hello внешнего интерфейса веб-роль ASP.NET MVC. она hello серверной части рабочих роль, которая использует очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="17350-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="17350-114">Можно создать hello того же многоуровневые приложения с внешнего интерфейса hello как веб-проекта, развернутого tooan вместо облачной службы веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="17350-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="17350-115">Также можно попробовать hello [на локальная/облачная гибридного приложения .NET](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="17350-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="17350-116">Hello следующем снимке экрана показано приложение hello завершена.</span><span class="sxs-lookup"><span data-stu-id="17350-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="17350-117">Обзор сценария: обмен данными между ролями</span><span class="sxs-lookup"><span data-stu-id="17350-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="17350-118">toosubmit заказ для обработки переднего плана пользовательского интерфейса компонента hello, работающих в веб-роли hello, должны взаимодействовать с логикой hello среднего уровня, работающих в hello рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="17350-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="17350-119">В этом примере для hello взаимодействия между уровнями hello сообщений Service Bus.</span><span class="sxs-lookup"><span data-stu-id="17350-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="17350-120">С помощью Service Bus обмен сообщениями между средней уровни hello web и разделяет эти два компонента.</span><span class="sxs-lookup"><span data-stu-id="17350-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="17350-121">В отличие от hello toodirect обмена сообщениями (то есть, TCP или HTTP), веб-уровень не напрямую; подключиться toohello среднего уровня Вместо этого он отправляет рабочих единиц, как сообщения, в Service Bus, который надежно сохраняет их, пока не будет готов tooconsume hello среднего уровня и обрабатывать их.</span><span class="sxs-lookup"><span data-stu-id="17350-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="17350-122">Шина обслуживания предоставляет два сообщениями через посредника toosupport сущностей: очереди и разделы.</span><span class="sxs-lookup"><span data-stu-id="17350-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="17350-123">С очередями каждое сообщение отправлено toohello очереди используется один получатель.</span><span class="sxs-lookup"><span data-stu-id="17350-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="17350-124">Разделы поддерживать шаблон публикации или подписки hello, в котором каждое опубликованное сообщение становится доступной tooa подписки, зарегистрированной разделе hello.</span><span class="sxs-lookup"><span data-stu-id="17350-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="17350-125">Для каждой подписки ведется собственная логическая очередь сообщений.</span><span class="sxs-lookup"><span data-stu-id="17350-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="17350-126">Подписки также могут быть настроены правила фильтрации, которые ограничивают набор hello сообщений передан toothose очереди подписки hello, соответствующих фильтру hello.</span><span class="sxs-lookup"><span data-stu-id="17350-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="17350-127">Hello следующий пример использует очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="17350-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="17350-128">По сравнению с прямым обменом сообщениями этот механизм взаимодействия имеет ряд преимуществ.</span><span class="sxs-lookup"><span data-stu-id="17350-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="17350-129">**Временное разделение.**</span><span class="sxs-lookup"><span data-stu-id="17350-129">**Temporal decoupling.**</span></span> <span data-ttu-id="17350-130">С hello шаблоном асинхронного обмена сообщениями, производители и потребители не должны быть в Интернете в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="17350-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="17350-131">Service Bus надежно хранит сообщения, пока сторона потребителя hello не будет готова к приему.</span><span class="sxs-lookup"><span data-stu-id="17350-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="17350-132">Это позволяет hello компоненты hello распределенного приложения toobe отключен, либо добровольно, например, для обслуживания или из-за сбоя компонента tooa без ущерба для системы в целом.</span><span class="sxs-lookup"><span data-stu-id="17350-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="17350-133">Кроме того использование приложения hello безопасности может потребоваться toocome сети только в определенное время дня hello.</span><span class="sxs-lookup"><span data-stu-id="17350-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="17350-134">**Выравнивание нагрузки.**</span><span class="sxs-lookup"><span data-stu-id="17350-134">**Load leveling.**</span></span> <span data-ttu-id="17350-135">Во многих приложениях системная нагрузка изменяется во времени, во время обработки hello время, необходимое для каждой единицы работы, как правило, постоянно.</span><span class="sxs-lookup"><span data-stu-id="17350-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="17350-136">Посредничество отправителями и получателями сообщений с очередью означает, что этот hello использует только toobe потребностей приложения (hello рабочих процессов) подготовить tooaccommodate среднюю нагрузку вместо пиковой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="17350-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="17350-137">Глубина Hello hello очереди будет расти или уменьшаться как hello входящая нагрузка меняется.</span><span class="sxs-lookup"><span data-stu-id="17350-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="17350-138">Это напрямую экономит деньги с точки зрения hello объема нагрузки приложения hello необходимые tooservice инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="17350-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="17350-139">**Балансировка нагрузки.**</span><span class="sxs-lookup"><span data-stu-id="17350-139">**Load balancing.**</span></span> <span data-ttu-id="17350-140">По мере увеличения нагрузки больше рабочих процессов могут добавляться tooread из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="17350-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="17350-141">Каждое сообщение обрабатывается только один hello рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="17350-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="17350-142">Кроме того этот запросу распределения нагрузки с учетом позволяет оптимального использования hello рабочих машин даже в случае различаются машины работника с точки зрения вычислительной мощности, как они будут опрашивать сообщения на максимальной скорости.</span><span class="sxs-lookup"><span data-stu-id="17350-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="17350-143">Данный шаблон часто называется hello *конкурентной* шаблон.</span><span class="sxs-lookup"><span data-stu-id="17350-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="17350-144">Hello в следующих разделах рассматриваются hello код, который реализует этой архитектуре.</span><span class="sxs-lookup"><span data-stu-id="17350-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="17350-145">Настройка среды разработки hello</span><span class="sxs-lookup"><span data-stu-id="17350-145">Set up hello development environment</span></span>
<span data-ttu-id="17350-146">Прежде чем начать, разработке приложений Azure, средства hello и настройка среды разработки.</span><span class="sxs-lookup"><span data-stu-id="17350-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="17350-147">Установить hello Azure SDK для .NET из пакета SDK для hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="17350-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="17350-148">В hello **.NET** столбец, выберите версию hello [Visual Studio](http://www.visualstudio.com) вы используете.</span><span class="sxs-lookup"><span data-stu-id="17350-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="17350-149">Hello шаги в данном руководстве используйте Visual Studio 2015, но они также работают с Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="17350-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="17350-150">При запросе toorun или сохранить hello установщика нажмите **запуска**.</span><span class="sxs-lookup"><span data-stu-id="17350-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="17350-151">В hello **Web Platform Installer**, нажмите кнопку **установить** и продолжите установку hello.</span><span class="sxs-lookup"><span data-stu-id="17350-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="17350-152">После завершения установки hello, будет иметь все необходимые toostart приложение hello toodevelop.</span><span class="sxs-lookup"><span data-stu-id="17350-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="17350-153">Hello SDK содержит средства, позволяющие легко разрабатывать приложения Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17350-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="17350-154">Создание пространства имен</span><span class="sxs-lookup"><span data-stu-id="17350-154">Create a namespace</span></span>
<span data-ttu-id="17350-155">Hello следующим шагом является toocreate пространства имен службы и получить ключ подписи общего доступа (SAS).</span><span class="sxs-lookup"><span data-stu-id="17350-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="17350-156">Пространство имен определяет границы каждого приложения, предоставляемого через служебную шину.</span><span class="sxs-lookup"><span data-stu-id="17350-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="17350-157">Ключ SAS создается системой hello при создании пространства имен.</span><span class="sxs-lookup"><span data-stu-id="17350-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="17350-158">Hello сочетание пространства имен и ключ SAS предоставляет учетные данные hello для приложения tooan access tooauthenticate Service Bus.</span><span class="sxs-lookup"><span data-stu-id="17350-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="17350-159">Создание веб-роли</span><span class="sxs-lookup"><span data-stu-id="17350-159">Create a web role</span></span>
<span data-ttu-id="17350-160">В этом разделе сборки hello интерфейсной части приложения.</span><span class="sxs-lookup"><span data-stu-id="17350-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="17350-161">Сначала необходимо создать страницы приветствия, приложение отображает.</span><span class="sxs-lookup"><span data-stu-id="17350-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="17350-162">После этого добавьте код, который отправляет очередь Service Bus tooa элементов и отображает сведения о состоянии очереди hello.</span><span class="sxs-lookup"><span data-stu-id="17350-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="17350-163">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="17350-163">Create hello project</span></span>
1. <span data-ttu-id="17350-164">С правами доступа администратора, запустите Visual Studio: щелкните правой кнопкой мыши hello **Visual Studio** значок программы, а затем нажмите кнопку **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="17350-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="17350-165">Эмулятор вычислений Azure Hello, описанных далее в этой статье, требует запуска Visual Studio с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="17350-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="17350-166">В Visual Studio в hello **файл** меню, нажмите кнопку **New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="17350-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="17350-167">В разделе **Установленные шаблоны** области **Visual C#** щелкните **Облако**, а затем — **Облачная служба Azure**.</span><span class="sxs-lookup"><span data-stu-id="17350-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="17350-168">Имя проекта hello **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="17350-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="17350-169">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17350-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="17350-170">В списке ролей **.NET Framework 4.5** дважды щелкните **Веб-роль ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="17350-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="17350-171">Наведите указатель мыши на **WebRole1** под **решение облачной службы Azure**, щелкните значок карандаша hello и переименования hello веб-роли слишком**FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="17350-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="17350-172">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17350-172">Then click **OK**.</span></span> <span data-ttu-id="17350-173">(Обратите внимание на написание слова «Frontend» со строчной буквой «e» — не «FrontEnd».)</span><span class="sxs-lookup"><span data-stu-id="17350-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="17350-174">Из hello **новый проект ASP.NET** диалогового окна hello **выберите шаблон** выберите **MVC**.</span><span class="sxs-lookup"><span data-stu-id="17350-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="17350-175">По-прежнему в hello **новый проект ASP.NET** диалогового окна выберите hello **изменить аутентификацию** кнопки.</span><span class="sxs-lookup"><span data-stu-id="17350-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="17350-176">В hello **изменить аутентификацию** диалоговое окно, нажмите кнопку **без проверки подлинности**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17350-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="17350-177">В этом учебнике выполняется развертывание приложения, для которого не требуется имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="17350-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="17350-178">Вернитесь в hello **новый проект ASP.NET** диалоговое окно, нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="17350-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="17350-179">В **обозревателе решений**, в hello **FrontendWebRole** щелкните правой кнопкой мыши проект **ссылки**, нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="17350-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="17350-180">Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="17350-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="17350-181">Выберите hello **WindowsAzure.ServiceBus** пакет, нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="17350-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="17350-182">Обратите внимание, что hello необходимые теперь существуют ссылки на сборки клиента и были добавлены некоторые новые файлы кода.</span><span class="sxs-lookup"><span data-stu-id="17350-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="17350-183">В **обозревателе решений** щелкните правой кнопкой мыши **Модели**, а затем выберите **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="17350-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="17350-184">В hello **имя** hello введите имя **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="17350-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="17350-185">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="17350-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="17350-186">Написание кода hello для веб-роли</span><span class="sxs-lookup"><span data-stu-id="17350-186">Write hello code for your web role</span></span>
<span data-ttu-id="17350-187">В этом разделе создается hello различным страницам, отображаемых в приложении.</span><span class="sxs-lookup"><span data-stu-id="17350-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="17350-188">Замените существующее определение пространства имен в файле OnlineOrder.cs hello в Visual Studio, hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="17350-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="17350-189">В **обозревателе решений** дважды щелкните **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="17350-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="17350-190">Добавьте следующее hello **с помощью** инструкции вверху hello hello файл hello tooinclude пространства имен для модели, который вы только что создали, а также Service Bus.</span><span class="sxs-lookup"><span data-stu-id="17350-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="17350-191">Также в файл HomeController.cs hello в Visual Studio, замените существующее определение пространства имен после кода hello.</span><span class="sxs-lookup"><span data-stu-id="17350-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="17350-192">Этот код содержит методы для обработки hello отправки элементов очереди toohello.</span><span class="sxs-lookup"><span data-stu-id="17350-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="17350-193">Из hello **построения** меню, нажмите кнопку **построить решение** tootest hello правильность выполненной работы к текущему моменту.</span><span class="sxs-lookup"><span data-stu-id="17350-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="17350-194">Теперь создайте представление hello для hello `Submit()` метода, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="17350-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="17350-195">Щелкните правой кнопкой мыши в пределах hello `Submit()` метод (hello перегрузку `Submit()` , не принимает параметров) и выберите **добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="17350-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="17350-196">Диалоговое окно для создания представления hello.</span><span class="sxs-lookup"><span data-stu-id="17350-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="17350-197">В hello **шаблона** выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="17350-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="17350-198">В hello **класс модели** выберите hello **OnlineOrder** класса.</span><span class="sxs-lookup"><span data-stu-id="17350-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="17350-199">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="17350-199">Click **Add**.</span></span>
8. <span data-ttu-id="17350-200">Теперь изменим hello отображается имя приложения.</span><span class="sxs-lookup"><span data-stu-id="17350-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="17350-201">В **обозревателе решений**, дважды щелкните **представления\общие\\_Layout.cshtml** файл tooopen его в редакторе Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="17350-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="17350-202">Замените все вхождения элемента **Мое приложение ASP.NET** текстом **Продукты LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="17350-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="17350-203">Удалите hello **Главная**, **о**, и **контакт** ссылки.</span><span class="sxs-lookup"><span data-stu-id="17350-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="17350-204">Удаление выделенной hello кода:</span><span class="sxs-lookup"><span data-stu-id="17350-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="17350-205">Наконец измените hello отправки страницы tooinclude некоторые сведения об очереди hello.</span><span class="sxs-lookup"><span data-stu-id="17350-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="17350-206">В **обозревателе решений**, дважды щелкните **Views\Home\Submit.cshtml** файл tooopen его в редакторе Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="17350-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="17350-207">Добавьте следующие строки после hello `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="17350-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="17350-208">Теперь, hello `ViewBag.MessageCount` пуст.</span><span class="sxs-lookup"><span data-stu-id="17350-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="17350-209">Вы заполните его позже.</span><span class="sxs-lookup"><span data-stu-id="17350-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="17350-210">Пользовательский интерфейс реализован.</span><span class="sxs-lookup"><span data-stu-id="17350-210">You now have implemented your UI.</span></span> <span data-ttu-id="17350-211">Можно нажать клавишу **F5** toorun приложения и убедитесь, что он выглядит так, как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="17350-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="17350-212">Написание кода hello для отправки в очередь Service Bus tooa элементов</span><span class="sxs-lookup"><span data-stu-id="17350-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="17350-213">Теперь добавьте код для отправки в очередь tooa элементов.</span><span class="sxs-lookup"><span data-stu-id="17350-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="17350-214">Сначала вам нужно создать класс, содержащий информацию о подключении к очереди служебной шины,</span><span class="sxs-lookup"><span data-stu-id="17350-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="17350-215">а затем — инициализировать подключение из Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="17350-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="17350-216">И, наконец обновите код отправки hello, созданный ранее в tooa HomeController.cs tooactually отправки элементов очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="17350-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="17350-217">В **обозревателе решений**, щелкните правой кнопкой мыши **FrontendWebRole** (щелкните правой кнопкой мыши проект hello, не hello роли).</span><span class="sxs-lookup"><span data-stu-id="17350-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="17350-218">Щелкните **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="17350-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="17350-219">Имя класса hello **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="17350-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="17350-220">Нажмите кнопку **добавить** toocreate hello класса.</span><span class="sxs-lookup"><span data-stu-id="17350-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="17350-221">Теперь добавьте код, который инкапсулирует сведения о соединении hello и инициализирует очереди Service Bus tooa hello.</span><span class="sxs-lookup"><span data-stu-id="17350-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="17350-222">Замените все содержимое hello QueueConnector.cs после кода hello и введите значения для `your Service Bus namespace` (ваше пространство имен) и `yourKey`, который является hello **первичного ключа** ранее получены из hello Azure портал.</span><span class="sxs-lookup"><span data-stu-id="17350-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="17350-223">Теперь нужно обеспечить вызов метода **Initialize**.</span><span class="sxs-lookup"><span data-stu-id="17350-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="17350-224">В **обозревателе решений** дважды щелкните **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="17350-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="17350-225">Добавьте следующие строки кода в конце hello hello hello **Application_Start** метод.</span><span class="sxs-lookup"><span data-stu-id="17350-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="17350-226">Наконец обновите hello веб-кода, созданного ранее, для отправки в очередь toohello элементов.</span><span class="sxs-lookup"><span data-stu-id="17350-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="17350-227">В **обозревателе решений** дважды щелкните **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="17350-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="17350-228">Обновление hello `Submit()` метод (hello перегрузку, которая не принимает параметров) следующим tooget приветственное сообщение для расчета hello очереди.</span><span class="sxs-lookup"><span data-stu-id="17350-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="17350-229">Обновление hello `Submit(OnlineOrder order)` метод (hello перегрузку, которая принимает один параметр) следующим toosubmit порядок сведения toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="17350-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="17350-230">Теперь можно запустить приложение hello еще раз.</span><span class="sxs-lookup"><span data-stu-id="17350-230">You can now run hello application again.</span></span> <span data-ttu-id="17350-231">Каждый раз при отправке заказа, увеличивает число сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="17350-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="17350-232">Создание рабочей роли hello</span><span class="sxs-lookup"><span data-stu-id="17350-232">Create hello worker role</span></span>
<span data-ttu-id="17350-233">Теперь вы создадите hello рабочая роль, обрабатывающая hello отправки заказа.</span><span class="sxs-lookup"><span data-stu-id="17350-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="17350-234">В этом примере используется hello **рабочая роль с очередью Service Bus** шаблон проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17350-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="17350-235">Hello необходимые учетные данные уже получен из портала hello.</span><span class="sxs-lookup"><span data-stu-id="17350-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="17350-236">Убедитесь, что вы подключились Visual Studio tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="17350-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="17350-237">В Visual Studio в **обозревателе решений** щелкните правой кнопкой мыши **ролей** папку hello **MultiTierApp** проекта.</span><span class="sxs-lookup"><span data-stu-id="17350-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="17350-238">Щелкните **Добавить** и выберите **Создать проект рабочей роли**.</span><span class="sxs-lookup"><span data-stu-id="17350-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="17350-239">Hello **добавить новый проект роли** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="17350-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="17350-240">В hello **добавить новый проект роли** диалоговое окно, нажмите кнопку **рабочая роль с очередью Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="17350-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="17350-241">В hello **имя** поле, имя проекта hello **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="17350-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="17350-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="17350-242">Then click **Add**.</span></span>
6. <span data-ttu-id="17350-243">Скопируйте строку подключения hello, полученный на шаге 9 буфера toohello раздел «Создать пространство имен служебной шины» hello.</span><span class="sxs-lookup"><span data-stu-id="17350-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="17350-244">В **обозревателе решений**, щелкните правой кнопкой мыши hello **OrderProcessingRole** созданный на шаге 5 (Убедитесь, что вы щелкните правой кнопкой мыши **OrderProcessingRole** под **Роли**, а не hello класса).</span><span class="sxs-lookup"><span data-stu-id="17350-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="17350-245">Выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="17350-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="17350-246">На hello **параметры** вкладка hello **свойства** диалоговое окно, щелкните внутри hello **значение** поле для **Microsoft.ServiceBus.ConnectionString**, а затем вставьте значение конечной точки hello, скопированным на шаге 6.</span><span class="sxs-lookup"><span data-stu-id="17350-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="17350-247">Создание **OnlineOrder** класса toorepresent hello заказов, как обработать их из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="17350-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="17350-248">При необходимости используйте ранее созданный класс.</span><span class="sxs-lookup"><span data-stu-id="17350-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="17350-249">В **обозревателе решений**, щелкните правой кнопкой мыши hello **OrderProcessingRole** класса (щелкните правой кнопкой мыши значок класса hello, не hello роли).</span><span class="sxs-lookup"><span data-stu-id="17350-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="17350-250">Щелкните **Добавить**, а затем — **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="17350-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="17350-251">Найдите вложенную папку toohello для **FrontendWebRole\Models**, а затем дважды щелкните **OnlineOrder.cs** tooadd его toothis проекта.</span><span class="sxs-lookup"><span data-stu-id="17350-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="17350-252">В **WorkerRole.cs**, измените значение hello hello **QueueName** переменную `"ProcessingQueue"` слишком`"OrdersQueue"` как показано в следующим hello.</span><span class="sxs-lookup"><span data-stu-id="17350-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="17350-253">Добавьте следующее hello using с hello начало файла WorkerRole.cs hello.</span><span class="sxs-lookup"><span data-stu-id="17350-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="17350-254">В hello `Run()` функция внутри hello `OnMessage()` call, замените содержимое hello hello `try` предложение with hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="17350-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="17350-255">Вы завершили приложения hello.</span><span class="sxs-lookup"><span data-stu-id="17350-255">You have completed hello application.</span></span> <span data-ttu-id="17350-256">Полный приложения hello можно проверить, щелкнув правой кнопкой мыши проект MultiTierApp hello в обозревателе решений при выборе **Назначить запускаемым проектом**, а затем нажать клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="17350-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="17350-257">Обратите внимание, что количество сообщений не увеличивается, так как hello рабочая роль обрабатывает элементы из очереди hello и помечает их как выполненные.</span><span class="sxs-lookup"><span data-stu-id="17350-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="17350-258">Выходные данные трассировки hello рабочей роли можно увидеть, просмотрев hello пользовательский Интерфейс эмулятора вычислений Azure.</span><span class="sxs-lookup"><span data-stu-id="17350-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="17350-259">Это можно сделать, щелкнув правой кнопкой мыши значок эмулятора hello в hello области уведомлений панели задач и выбрав **Показать пользовательский Интерфейс эмулятора вычислений**.</span><span class="sxs-lookup"><span data-stu-id="17350-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="17350-260">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17350-260">Next steps</span></span>
<span data-ttu-id="17350-261">toolearn Дополнительные сведения о Service Bus см. следующие ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="17350-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="17350-262">[Документация по служебной шине Azure][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="17350-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="17350-263">[Страница службы служебной шины][sbacom]</span><span class="sxs-lookup"><span data-stu-id="17350-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="17350-264">[Как tooUse очереди шины обслуживания][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="17350-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="17350-265">toolearn Дополнительные сведения о многоуровневые сценарии, см.:</span><span class="sxs-lookup"><span data-stu-id="17350-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="17350-266">[Многоуровневое приложение .NET, использующее таблицы, очереди и большие двоичные объекты хранилища][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="17350-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
