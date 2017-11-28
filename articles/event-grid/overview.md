---
title: "Общие сведения о aaaAzure сетки событий"
description: "В статье описываются служба \"Сетка событий Azure\" и ее основные понятия."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="4bd3a-103">Введение tooAzure сетки событий</span><span class="sxs-lookup"><span data-stu-id="4bd3a-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="4bd3a-104">Azure сетки событий позволяет tooeasily создавать приложения с архитектурой, основанной на событиях.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="4bd3a-105">Hello ресурсов Azure, вам потребуется как toosubscribe в и предоставляют hello обработчика событий или события hello toosend конечной точки веб-перехватчика для выбора.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="4bd3a-106">Служба "Сетка событий" обеспечивает встроенную поддержку событий, поступающих из таких служб Azure, как хранилища BLOB-объектов и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="4bd3a-107">Кроме того, служба предоставляет настраиваемую поддержку для приложения и сторонних событий, используя настраиваемые разделы и веб-перехватчики.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="4bd3a-108">Можно использовать фильтры tooroute определенные события toodifferent конечных точек многоадресной рассылки toomultiple конечных точек и убедитесь, что ваш надежно доставляет события.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="4bd3a-109">Служба "Сетка событий" обеспечивает встроенную поддержку для пользовательских и сторонних событий.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="4bd3a-110">Для предварительной версии hello поддерживает сетки событий **westus2** и **westcentralus** расположения.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="4bd3a-111">Будут добавлены другие регионы.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-111">Other regions will be added.</span></span>

<span data-ttu-id="4bd3a-112">В статье представлен обзор службы "Сетка событий Azure".</span><span class="sxs-lookup"><span data-stu-id="4bd3a-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="4bd3a-113">Tooget к работе с сеткой событий см [Создание и маршрута пользовательские события с сеткой событий Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="4bd3a-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Функциональная модель сетки событий](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="4bd3a-115">Сейчас хранилище BLOB-объектов Azure не является общедоступным в качестве издателя.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="4bd3a-116">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="4bd3a-116">Concepts</span></span>

<span data-ttu-id="4bd3a-117">Есть пять основных понятий, с которыми нужно ознакомиться перед началом работы со службой "Сетка событий Azure":</span><span class="sxs-lookup"><span data-stu-id="4bd3a-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="4bd3a-118">**События** — это то, что произошло.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-118">**Events** - What happened.</span></span>
* <span data-ttu-id="4bd3a-119">**Источники событий или издателей** — там, где выполнялась hello событий.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="4bd3a-120">**Разделы** -hello конечной точки, где издателям отправлять события.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="4bd3a-121">**Подписки на события** -hello конечной точки или встроенный механизм tooroute событий, иногда toomultiple обработчиков.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="4bd3a-122">Подписки также используются обработчики toointelligently фильтрация входящих событий.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="4bd3a-123">**Обработчики событий** - hello приложения или службы отклик toohello событий.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="4bd3a-124">Дополнительные сведения об этих понятиях см. в разделе [Concepts in Azure Event Grid](concepts.md) (Основные понятия службы "Сетка событий Azure").</span><span class="sxs-lookup"><span data-stu-id="4bd3a-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="4bd3a-125">Возможности</span><span class="sxs-lookup"><span data-stu-id="4bd3a-125">Capabilities</span></span>

<span data-ttu-id="4bd3a-126">Ниже приведены некоторые ключевые функции hello сетки событий Azure.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="4bd3a-127">**Простота** -точку и нажмите кнопку tooaim события из обработчика событий tooany ресурсов Azure или конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="4bd3a-128">**Расширенная фильтрация** -фильтр на событие типа или событий публикации tooensure путь обработчики событий получают только соответствующие события.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="4bd3a-129">**Развертываемый** -подписаться toohello несколько конечных точек того же события toosend копий hello событие tooas многих местах при необходимости.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="4bd3a-130">**Надежность** -используют 24-часовом повторить с экспоненциально растущим tooensure доставки событий.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="4bd3a-131">**Оплата каждого события** - платить только в течение интервала hello при помощи сетки события.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="4bd3a-132">**Высокая пропускная способность** — в службе "Сетка событий" можно создавать высокие рабочие нагрузки с поддержкой миллионов событий в секунду.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="4bd3a-133">**Встроенные события** — быстрое возобновление работы благодаря встроенным событиям с определяемыми ресурсами.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="4bd3a-134">**Пользовательские события** — используйте маршрутизацию и фильтр службы "Сетка событий", чтобы обеспечить надежную доставку пользовательских событий в приложение.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="4bd3a-135">Встроенная интеграция издателя и обработчика</span><span class="sxs-lookup"><span data-stu-id="4bd3a-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="4bd3a-136">Azure обеспечивает встроенную поддержку событий, а также их издателей и обработчиков с помощью многочисленных служб.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="4bd3a-137">Издатели</span><span class="sxs-lookup"><span data-stu-id="4bd3a-137">Publishers</span></span>

<span data-ttu-id="4bd3a-138">В настоящее время hello следующих служб Azure имеют встроенные издателя поддержку сетки событий:</span><span class="sxs-lookup"><span data-stu-id="4bd3a-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="4bd3a-139">Группы ресурсов (операции управления)</span><span class="sxs-lookup"><span data-stu-id="4bd3a-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="4bd3a-140">Подписки Azure (операции управления)</span><span class="sxs-lookup"><span data-stu-id="4bd3a-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="4bd3a-141">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="4bd3a-141">Event Hubs</span></span>
* <span data-ttu-id="4bd3a-142">Пользовательские разделы</span><span class="sxs-lookup"><span data-stu-id="4bd3a-142">Custom Topics</span></span>

<span data-ttu-id="4bd3a-143">Другие службы Azure будут добавлены в этом году.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="4bd3a-144">Обработчики</span><span class="sxs-lookup"><span data-stu-id="4bd3a-144">Handlers</span></span>

<span data-ttu-id="4bd3a-145">В настоящее время hello следующих служб Azure имеют встроенные обработчик поддержку сетки событий:</span><span class="sxs-lookup"><span data-stu-id="4bd3a-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="4bd3a-146">Функции Azure</span><span class="sxs-lookup"><span data-stu-id="4bd3a-146">Azure Functions</span></span>
* <span data-ttu-id="4bd3a-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4bd3a-147">Logic Apps</span></span>
* <span data-ttu-id="4bd3a-148">Служба автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="4bd3a-148">Azure Automation</span></span>
* <span data-ttu-id="4bd3a-149">Веб-перехватчики</span><span class="sxs-lookup"><span data-stu-id="4bd3a-149">WebHooks</span></span>

<span data-ttu-id="4bd3a-150">Другие службы Azure будут добавлены в этом году.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="4bd3a-151">Что можно сделать с помощью службы "Сетка событий"?</span><span class="sxs-lookup"><span data-stu-id="4bd3a-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="4bd3a-152">Служба "Сетка событий Azure" включает несколько функций, которые значительно расширяют возможности бессерверных операций, автоматизации операций и интеграции.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="4bd3a-153">Архитектура бессерверных приложений</span><span class="sxs-lookup"><span data-stu-id="4bd3a-153">Serverless application architectures</span></span>

![Бессерверное приложение](./media/overview/serverless_web_app.png)

<span data-ttu-id="4bd3a-155">Служба "Сетка событий Azure" связывает источники данных и обработчики событий.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="4bd3a-156">Например используйте триггер tooinstantly сетки событий анализ образов toorun функции без сервера, каждый раз, когда новый фото добавлен tooa контейнер хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="4bd3a-157">Автоматизация операций</span><span class="sxs-lookup"><span data-stu-id="4bd3a-157">Ops Automation</span></span>

![Автоматизация операций](./media/overview/Ops_automation.png)

<span data-ttu-id="4bd3a-159">Сетки событий позволяет toospeed automation и упростить применение политик.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="4bd3a-160">Например, служба "Сетка событий" может уведомлять службу автоматизации Azure о создании виртуальных машин или базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="4bd3a-161">Эти события могут использоваться tooautomatically убедитесь, что установлен конфигураций службы соответствующим, постановки метаданных в операции средства, тег виртуальных машин или файл рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="4bd3a-162">Интеграция приложений</span><span class="sxs-lookup"><span data-stu-id="4bd3a-162">Application integration</span></span>

![Интеграция приложений](./media/overview/app_integration.png)

<span data-ttu-id="4bd3a-164">Служба "Сетка событий Azure" связывает приложения с другими службами.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="4bd3a-165">Например создание toosend пользовательский раздел tooEvent данных событий приложения сетки и воспользоваться преимуществами его надежную доставку, дополнительно маршрутизации и прямая интеграция с Azure.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="4bd3a-166">Кроме того можно использовать сетки событий с данными tooprocess логику приложения в любом месте, без необходимости написания кода.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="4bd3a-167">Чем служба "Сетка событий" отличается от других служб интеграции Azure?</span><span class="sxs-lookup"><span data-stu-id="4bd3a-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="4bd3a-168">Служба "Сетка событий Azure" — это объединяющее решение для обработки событий, обеспечивающее реактивное программирование на основе событий.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="4bd3a-169">Она тесно интегрирована со службами Azure и может интегрироваться со сторонними службами.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="4bd3a-170">сообщение о событии Hello содержит hello сведения, необходимые toochanges tooreact служб и приложений.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="4bd3a-171">Событие сетки не конвейера данных и не доставляет hello фактическому объекту, который был обновлен.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="4bd3a-172">Идеальным вариантом для стандартных корпоративных приложений, которые требуют выполнения транзакций, упорядочивания, поиска повторяющихся сообщений и мгновенного обеспечения согласованности, является служебная шина.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="4bd3a-173">Служба "Сетка событий" предназначена для использования с реактивной моделью, обеспечивая высокую скорость, масштабируемость, экономичность и широкий диапазон применения.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="4bd3a-174">Это хорошо подходит tooserverless архитектура.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="4bd3a-175">Служба "Сетка событий" дополняет другие службы Azure, такие как Logic Apps и концентраторы событий.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="4bd3a-176">Триггеры событий сетки hello toobegin логику приложения его рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="4bd3a-177">Концентраторы событий работает с сетки события, позволяя tooevents tooreact из записи концентраторов событий и конвейеры входящих сообщений и преобразования данных сборки.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="4bd3a-178">Сколько стоит служба "Сетка событий"?</span><span class="sxs-lookup"><span data-stu-id="4bd3a-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="4bd3a-179">Для службы "Сетка событий Azure" применяется модель оплаты за событие, поэтому счет выставляются только за те ресурсы, которые вы используете.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="4bd3a-180">Сетка события обходится $0.60 за миллион операций (0,30 $ во время предварительного просмотра) и hello первые 100 000 операции в месяц бесплатны.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="4bd3a-181">Операциями считаются прием событий, расширенное сопоставление, попытки доставки и вызовы управления.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="4bd3a-182">Дополнительные сведения можно найти на hello [странице цен](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="4bd3a-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bd3a-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4bd3a-183">Next steps</span></span>

* <span data-ttu-id="4bd3a-184">[Создание и подписаться на события toocustom](custom-event-quickstart.md) сразу перейти к делу и начать отправку собственную конечную точку tooany пользовательские события, использование быстрого запуска Azure сетки событий hello.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="4bd3a-185">[С помощью логики приложения, как обработчик события](monitor-virtual-machine-changes-event-grid-logic-app.md) учебник по созданию приложения с помощью tooevents tooreact Logic Apps отправлено сетки событий.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="4bd3a-186">Справочник по REST API службы "Сетка событий Azure"</span><span class="sxs-lookup"><span data-stu-id="4bd3a-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="4bd3a-187">Предоставляет дополнительные технические сведения о hello сетки событий Azure и ссылка для управления подписки на события, маршрутизации и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="4bd3a-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
