---
title: "aaaOptimizing Azure кода в Visual Studio | Документы Microsoft"
description: "Узнайте, каким образом средства оптимизации кода Azure в Visual Studio помогут сделать код более надежным и производительным."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="78ee7-103">Оптимизация кода Azure</span><span class="sxs-lookup"><span data-stu-id="78ee7-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="78ee7-104">При программировании приложений, использующих Microsoft Azure, существуют некоторые методики написания кода, необходимо следовать toohelp избежать проблем с масштабированием, поведения и производительности в облачной среде.</span><span class="sxs-lookup"><span data-stu-id="78ee7-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="78ee7-105">Майкрософт предлагает инструмент анализа кода Azure, который распознает и идентифицирует часто встречающиеся проблемы, а также помогает их решить.</span><span class="sxs-lookup"><span data-stu-id="78ee7-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="78ee7-106">Вы можете загрузить средство hello в Visual Studio через NuGet.</span><span class="sxs-lookup"><span data-stu-id="78ee7-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="78ee7-107">Правила анализа кода Azure</span><span class="sxs-lookup"><span data-stu-id="78ee7-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="78ee7-108">Средство анализа кода Azure Hello использует hello правилам tooautomatically пометок кода Azure при обнаружении известных проблем, влияющих на производительность.</span><span class="sxs-lookup"><span data-stu-id="78ee7-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="78ee7-109">Обнаруженные проблемы отображаются в виде предупреждений или ошибок компилятора.</span><span class="sxs-lookup"><span data-stu-id="78ee7-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="78ee7-110">Через значок лампочки часто предоставляются код исправления или подсказки tooresolve hello предупреждения или ошибки.</span><span class="sxs-lookup"><span data-stu-id="78ee7-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="78ee7-111">Старайтесь не использовать режим состояния сеанса по умолчанию (внутрипроцессорный)</span><span class="sxs-lookup"><span data-stu-id="78ee7-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-112">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-112">ID</span></span>
<span data-ttu-id="78ee7-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="78ee7-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-114">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-114">Description</span></span>
<span data-ttu-id="78ee7-115">Если вы используете режим состояния сеанса (в процессе) по умолчанию hello для облачных приложений, вы можете потерять состояние сеанса.</span><span class="sxs-lookup"><span data-stu-id="78ee7-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="78ee7-116">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-117">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-117">Reason</span></span>
<span data-ttu-id="78ee7-118">По умолчанию режим состояния сеанса hello, указанных в файле web.config hello в процессе.</span><span class="sxs-lookup"><span data-stu-id="78ee7-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="78ee7-119">Кроме того Если нет записи, указанную в файле конфигурации hello, hello режим состояния сеанса по умолчанию tooin процесса.</span><span class="sxs-lookup"><span data-stu-id="78ee7-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="78ee7-120">Hello внутрипроцессный режим хранит состояние сеанса в памяти на веб-сервере hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="78ee7-121">При перезапуске экземпляра или экземпляра используется для балансировки нагрузки и отработки отказа, не сохраняется состояние сеанса hello, хранятся в памяти на веб-сервере hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="78ee7-122">Такая ситуация не позволяет hello приложению быть масштабируемым в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="78ee7-123">Состояние сеанса ASP.NET поддерживает несколько различных параметров хранения данных о состоянии сеанса: InProc, StateServer, SQLServer, Custom и Off.</span><span class="sxs-lookup"><span data-stu-id="78ee7-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="78ee7-124">Рекомендуется использовать пользовательский режим toohost данных на внешнем хранилище состояния сеанса, таких как [поставщик состояния сеанса Azure для Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="78ee7-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-125">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-125">Solution</span></span>
<span data-ttu-id="78ee7-126">Одно из рекомендуемых решений — toostore состояние сеанса на управляемой службы кэша.</span><span class="sxs-lookup"><span data-stu-id="78ee7-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="78ee7-127">Узнайте, как toouse [поставщик состояния сеанса Azure для Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore состояния сеанса.</span><span class="sxs-lookup"><span data-stu-id="78ee7-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="78ee7-128">Можно также сеанс магазина указать его в других местах tooensure что масштабируемые приложения в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="78ee7-129">Дополнительные сведения об альтернативных решений прочитайте toolearn [режимы состояния сеанса](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="78ee7-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="78ee7-130">Метод Run не должен быть асинхронным</span><span class="sxs-lookup"><span data-stu-id="78ee7-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-131">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-131">ID</span></span>
<span data-ttu-id="78ee7-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="78ee7-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-133">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-133">Description</span></span>
<span data-ttu-id="78ee7-134">Создайте асинхронные методы (такие как [await](https://msdn.microsoft.com/library/hh156528.aspx)) за пределами hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метода, а затем вызов hello асинхронные методы из [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="78ee7-135">Объявления hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод асинхронным приводит hello рабочей роли tooenter цикл перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="78ee7-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="78ee7-136">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-137">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-137">Reason</span></span>
<span data-ttu-id="78ee7-138">Вызов асинхронных методов в hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод вызывает hello облачной службы среды выполнения toorecycle hello рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="78ee7-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="78ee7-139">При запуске рабочей роли все выполнение программы происходит внутри hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="78ee7-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="78ee7-140">Для существующих hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод вызывает рабочий hello toorestart роли.</span><span class="sxs-lookup"><span data-stu-id="78ee7-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="78ee7-141">Среда выполнения hello рабочей роли, достигнув hello асинхронного метода, он производит диспетчеризацию всех операций после асинхронного метода hello и возвращается.</span><span class="sxs-lookup"><span data-stu-id="78ee7-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="78ee7-142">В результате hello рабочей роли tooexit из hello [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод и перезапуска.</span><span class="sxs-lookup"><span data-stu-id="78ee7-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="78ee7-143">В следующей итерации hello выполнения hello рабочей роли попаданий hello попытку асинхронного метода и вызывает hello рабочей роли toorecycle еще раз, а также перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="78ee7-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-144">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-144">Solution</span></span>
<span data-ttu-id="78ee7-145">Разместите все асинхронные операции вне hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="78ee7-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="78ee7-146">Затем вызовите асинхронный метод hello рефакторинг из внутри hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) метода, например .wait RunAsync ().</span><span class="sxs-lookup"><span data-stu-id="78ee7-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="78ee7-147">Средство анализа кода Azure Hello может помочь решить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="78ee7-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="78ee7-148">Привет, следующий фрагмент кода демонстрирует hello исправление кода для устранения этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="78ee7-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="78ee7-149">Использование проверки подлинности подписанного URL-адреса с помощью служебной шины</span><span class="sxs-lookup"><span data-stu-id="78ee7-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-150">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-150">ID</span></span>
<span data-ttu-id="78ee7-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="78ee7-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-152">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="78ee7-152">Description</span></span>
<span data-ttu-id="78ee7-153">Используйте для проверки подлинности подписанный URL-адрес (SAS).</span><span class="sxs-lookup"><span data-stu-id="78ee7-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="78ee7-154">Служба управления доступом (ACS) больше не используется для проверки подлинности служебной шины.</span><span class="sxs-lookup"><span data-stu-id="78ee7-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="78ee7-155">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-156">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-156">Reason</span></span>
<span data-ttu-id="78ee7-157">Для повышения уровня безопасности Azure Active Directory заменяет проверку подлинности с помощью ACS на проверку подлинности с использованием SAS.</span><span class="sxs-lookup"><span data-stu-id="78ee7-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="78ee7-158">В разделе [Azure Active Directory является hello будущих служб ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) сведения о плане перехода hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-159">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-159">Solution</span></span>
<span data-ttu-id="78ee7-160">В приложениях используйте проверку подлинности SAS.</span><span class="sxs-lookup"><span data-stu-id="78ee7-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="78ee7-161">Hello в следующем примере показано, как toouse существующие SAS маркера tooaccess службы шины пространства имен или сущности.</span><span class="sxs-lookup"><span data-stu-id="78ee7-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="78ee7-162">В разделе hello в следующих разделах приводятся дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="78ee7-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="78ee7-163">Общие сведения см. в статье [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx) (Аутентификация на основе подписанного URL-адреса с помощью служебной шины).</span><span class="sxs-lookup"><span data-stu-id="78ee7-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="78ee7-164">Как toouse проверки подлинности подписи общий доступ со служебной шиной</span><span class="sxs-lookup"><span data-stu-id="78ee7-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="78ee7-165">Пример проекта см. на странице [Примеры кода Azure](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c).</span><span class="sxs-lookup"><span data-stu-id="78ee7-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="78ee7-166">Рассмотрите возможность использования OnMessage метод tooavoid «цикла получения»</span><span class="sxs-lookup"><span data-stu-id="78ee7-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-167">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-167">ID</span></span>
<span data-ttu-id="78ee7-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="78ee7-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-169">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-169">Description</span></span>
<span data-ttu-id="78ee7-170">tooavoid, поступающих в «цикл получения», вызывающему Привет **OnMessage** метод является лучшим решением для получения сообщений, чем вызывающему Привет **Receive** метод.</span><span class="sxs-lookup"><span data-stu-id="78ee7-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="78ee7-171">Тем не менее если необходимо использовать hello **Receive** метод и укажите значение времени ожидания сервера не по умолчанию, убедитесь, что время ожидания сервера hello более одной минуты.</span><span class="sxs-lookup"><span data-stu-id="78ee7-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="78ee7-172">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-173">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-173">Reason</span></span>
<span data-ttu-id="78ee7-174">При вызове **OnMessage**, hello клиент начинает процесс обработки внутренних сообщений, который постоянно опрашивает hello очереди или подписки.</span><span class="sxs-lookup"><span data-stu-id="78ee7-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="78ee7-175">Этот процесс обработки сообщений содержит бесконечный цикл, который отправляет вызов tooreceive сообщений.</span><span class="sxs-lookup"><span data-stu-id="78ee7-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="78ee7-176">Если время ожидания вызова hello, он выдает новый вызов.</span><span class="sxs-lookup"><span data-stu-id="78ee7-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="78ee7-177">интервал времени ожидания Hello определяется по значению hello hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) свойство hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx), который используется.</span><span class="sxs-lookup"><span data-stu-id="78ee7-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="78ee7-178">Здравствуйте, преимущество использования **OnMessage** по сравнению слишком**Receive** является то, что пользователи не toomanually опрос на наличие сообщений, обработки исключений, обработки нескольких сообщений в параллельном режиме и завершить hello сообщения.</span><span class="sxs-lookup"><span data-stu-id="78ee7-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="78ee7-179">При вызове метода **Receive** без использования значения по умолчанию, было бы убедиться, что hello *ServerWaitTime* значение — более одной минуты.</span><span class="sxs-lookup"><span data-stu-id="78ee7-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="78ee7-180">Установка *ServerWaitTime* toomore, чем на одну минуту предотвратит превышение времени ожидания до полного получения сообщения hello hello сервера.</span><span class="sxs-lookup"><span data-stu-id="78ee7-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-181">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-181">Solution</span></span>
<span data-ttu-id="78ee7-182">См. следующие примеры рекомендованного использования кода hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="78ee7-183">Дополнительные сведения см. в статьях [Метод QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) и [Метод QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="78ee7-184">производительность hello tooimprove hello инфраструктуры обмена сообщениями Azure, см. шаблон проектирования hello [начало асинхронного обмена сообщениями](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="78ee7-185">Hello ниже приведен пример использования **OnMessage** tooreceive сообщений.</span><span class="sxs-lookup"><span data-stu-id="78ee7-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="78ee7-186">Hello ниже приведен пример использования **Receive** время ожидания сервера по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="78ee7-187">Hello ниже приведен пример использования **Receive** с сервера не по умолчанию время ожидания.</span><span class="sxs-lookup"><span data-stu-id="78ee7-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="78ee7-188">Рассмотрите возможность использования асинхронных методов служебной шины</span><span class="sxs-lookup"><span data-stu-id="78ee7-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-189">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-189">ID</span></span>
<span data-ttu-id="78ee7-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="78ee7-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-191">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-191">Description</span></span>
<span data-ttu-id="78ee7-192">Используйте асинхронную Service Bus методы tooimprove производительности обмена сообщениями через посредника.</span><span class="sxs-lookup"><span data-stu-id="78ee7-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="78ee7-193">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-194">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-194">Reason</span></span>
<span data-ttu-id="78ee7-195">Использование асинхронных методов обеспечивает программный параллелизм приложений, так как выполнение каждого вызова не блокирует основной поток hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="78ee7-196">При использовании методов обмена сообщениями служебной шины требуется время на выполнение операции (отправки, получения, удаления и т. д.).</span><span class="sxs-lookup"><span data-stu-id="78ee7-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="78ee7-197">Это время включает в себя hello обработку hello операции по hello службы Service Bus задержки toohello сложения hello запроса и ответа hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="78ee7-198">tooincrease число hello операций в единицу времени, необходимо выполнять их параллельно.</span><span class="sxs-lookup"><span data-stu-id="78ee7-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="78ee7-199">Дополнительные сведения см. слишком[советы и рекомендации по производительности улучшения с помощью Service Bus обмен сообщениями](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-200">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-200">Solution</span></span>
<span data-ttu-id="78ee7-201">В разделе [класс QueueClient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) сведения о как toouse hello рекомендуется асинхронного метода.</span><span class="sxs-lookup"><span data-stu-id="78ee7-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="78ee7-202">производительность hello tooimprove hello инфраструктуры обмена сообщениями Azure, см. шаблон проектирования hello [начало асинхронного обмена сообщениями](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="78ee7-203">Попробуйте секционировать очереди и разделы служебной шины</span><span class="sxs-lookup"><span data-stu-id="78ee7-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-204">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-204">ID</span></span>
<span data-ttu-id="78ee7-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="78ee7-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-206">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="78ee7-206">Description</span></span>
<span data-ttu-id="78ee7-207">Секционирование очередей и разделов служебной шины для повышения производительности обмена сообщениями служебной шины.</span><span class="sxs-lookup"><span data-stu-id="78ee7-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="78ee7-208">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-209">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-209">Reason</span></span>
<span data-ttu-id="78ee7-210">Секционирование очередей и разделов Service Bus повышает производительность пропускную способность и доступность службы, так как hello общая пропускная способность секционированной очереди или раздела больше не ограничивается hello производительностью одного брокера сообщений или хранилища обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="78ee7-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="78ee7-211">Кроме того, из-за временного сбоя хранилища сообщений секционированная очередь или раздел не становятся недоступными.</span><span class="sxs-lookup"><span data-stu-id="78ee7-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="78ee7-212">Дополнительную информацию см. в разделе [Разделение сущностей обмена сообщениями](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-213">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-213">Solution</span></span>
<span data-ttu-id="78ee7-214">Здравствуйте, в следующем фрагменте кода показан код как toopartition сущностей обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="78ee7-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="78ee7-215">Дополнительные сведения см. в разделе [секционированные очереди Service Bus и разделы | Блог Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) и извлечь hello [Microsoft Azure Service Bus секционированной очереди](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) образца.</span><span class="sxs-lookup"><span data-stu-id="78ee7-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="78ee7-216">Не задавайте значение SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="78ee7-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-217">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-217">ID</span></span>
<span data-ttu-id="78ee7-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="78ee7-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-219">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-219">Description</span></span>
<span data-ttu-id="78ee7-220">Следует избегать использования SharedAccessStartTimeset toohello текущей загрузке tooimmediately hello политики общего доступа.</span><span class="sxs-lookup"><span data-stu-id="78ee7-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="78ee7-221">Требуется только tooset это свойство Если политики общего доступа toostart hello позже.</span><span class="sxs-lookup"><span data-stu-id="78ee7-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="78ee7-222">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-223">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-223">Reason</span></span>
<span data-ttu-id="78ee7-224">Синхронизация часов вызывает небольшую разницу во времени между центрами обработки данных.</span><span class="sxs-lookup"><span data-stu-id="78ee7-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="78ee7-225">Например можно логически подразумевается параметр hello время запуска политики SAS хранилища hello текущее время с помощью DateTime.Now или аналогичного метода может привести к тому hello SAS политики tootake силу немедленно.</span><span class="sxs-lookup"><span data-stu-id="78ee7-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="78ee7-226">Однако hello небольшая разница во времени между центрами обработки данных может вызвать проблемы с данным, так как иногда центра обработки данных может быть немного позже, чем время начала hello, а другие — опережать.</span><span class="sxs-lookup"><span data-stu-id="78ee7-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="78ee7-227">В результате hello политики SAS может истечь, быстро (или даже немедленно) Если слишком короткое время жизни политики hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="78ee7-228">Дополнительные рекомендации по использованию подписи общего доступа в службе хранилища Azure см. в разделе [Знакомство с SAS таблицы (подпись общего доступа) SAS очереди сайта и обновление tooBlob SAS - блоге разработчиков хранилища Microsoft Azure — Главная — блоги MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-229">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-229">Solution</span></span>
<span data-ttu-id="78ee7-230">Удалите оператор hello, которое задает время начала hello hello общей политики доступа.</span><span class="sxs-lookup"><span data-stu-id="78ee7-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="78ee7-231">Средство анализа кода Azure Hello предоставляется исправление, устраняющее эту проблему.</span><span class="sxs-lookup"><span data-stu-id="78ee7-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="78ee7-232">Дополнительные сведения об управлении безопасностью см. в разделе шаблон разработки hello [шаблон ключа Valet](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="78ee7-233">Привет, следующий фрагмент кода демонстрирует hello исправление кода для устранения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="78ee7-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="78ee7-234">Время окончания срока действия общей политики доступа должно быть больше пяти минут</span><span class="sxs-lookup"><span data-stu-id="78ee7-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-235">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-235">ID</span></span>
<span data-ttu-id="78ee7-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="78ee7-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-237">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-237">Description</span></span>
<span data-ttu-id="78ee7-238">Может быть как разница пять минут в часы между центрами обработки данных в другое расположение, из-за tooa, называемое «расфазировки синхронизирующих импульсов.»</span><span class="sxs-lookup"><span data-stu-id="78ee7-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="78ee7-239">tooprevent hello SAS маркера политики раньше, чем запланировано, задать toobe время истечения срока действия hello более пяти минут.</span><span class="sxs-lookup"><span data-stu-id="78ee7-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="78ee7-240">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-241">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-241">Reason</span></span>
<span data-ttu-id="78ee7-242">Центры обработки данных в разных местах по всему Здравствуй, мир! синхронизировать по сигналу часов.</span><span class="sxs-lookup"><span data-stu-id="78ee7-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="78ee7-243">Поскольку требуется времени для расположений toodifferent tootravel сигнал часов, хотя теоретически все синхронизировано может быть разница во времени между центрами обработки данных в разных географических местоположениях.</span><span class="sxs-lookup"><span data-stu-id="78ee7-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="78ee7-244">Разница во времени может повлиять на hello общего доступа начала времени и истечения срока действия интервала политики.</span><span class="sxs-lookup"><span data-stu-id="78ee7-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="78ee7-245">Таким образом tooensure политику общего доступа вступает в силу немедленно, не указывается время начала hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="78ee7-246">Кроме того убедитесь, что срок действия hello больше, чем 5 минут, раннее tooprevent истечение времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="78ee7-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="78ee7-247">Дополнительные сведения об использовании подписи общего доступа в службе хранилища Azure см. в разделе [Знакомство с SAS таблицы (подпись общего доступа) SAS очереди сайта и обновление tooBlob SAS - блоге разработчиков хранилища Microsoft Azure — Главная — блоги MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-248">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-248">Solution</span></span>
<span data-ttu-id="78ee7-249">Дополнительные сведения об управлении безопасностью см. шаблон проектирования hello [шаблон ключа Valet](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="78ee7-250">Hello ниже приведен пример не указано время запуска политики общего доступа.</span><span class="sxs-lookup"><span data-stu-id="78ee7-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="78ee7-251">Hello ниже приведен пример указано время запуска политики общего доступа с длительностью политики более пять минут.</span><span class="sxs-lookup"><span data-stu-id="78ee7-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="78ee7-252">Дополнительную информацию см. в статье [Создание и использование подписанного URL-адреса](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="78ee7-253">Используйте CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="78ee7-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-254">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-254">ID</span></span>
<span data-ttu-id="78ee7-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="78ee7-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-256">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-256">Description</span></span>
<span data-ttu-id="78ee7-257">С помощью hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) класса для проектов, таких как веб-сайт Azure и мобильных служб Azure, не вызовет проблемы среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="78ee7-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="78ee7-258">Рекомендуется, однако это рекомендуется toouse облака[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) как единый способ управления конфигурациями всех приложений облака Azure.</span><span class="sxs-lookup"><span data-stu-id="78ee7-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="78ee7-259">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-260">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-260">Reason</span></span>
<span data-ttu-id="78ee7-261">CloudConfigurationManager считывает среду приложения toohello соответствующий файл конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="78ee7-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="78ee7-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="78ee7-263">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-263">Solution</span></span>
<span data-ttu-id="78ee7-264">Рефакторинг toouse вашего кода hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="78ee7-265">Средство анализа кода Azure hello предоставляются исправления кода для этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="78ee7-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="78ee7-266">Привет, следующий фрагмент кода демонстрирует hello исправление кода для устранения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="78ee7-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="78ee7-267">Замените</span><span class="sxs-lookup"><span data-stu-id="78ee7-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="78ee7-268">на</span><span class="sxs-lookup"><span data-stu-id="78ee7-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="78ee7-269">Ниже приведен пример как toostore hello параметр конфигурации в файле App.config или Web.config.</span><span class="sxs-lookup"><span data-stu-id="78ee7-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="78ee7-270">Добавьте параметры hello toohello раздел appSettings файла конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="78ee7-271">Hello Приведем hello файл Web.config для предыдущего примера кода hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="78ee7-272">Избегайте использования жестко запрограммированных строк подключения</span><span class="sxs-lookup"><span data-stu-id="78ee7-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-273">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-273">ID</span></span>
<span data-ttu-id="78ee7-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="78ee7-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-275">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-275">Description</span></span>
<span data-ttu-id="78ee7-276">Если использовать жестко запрограммированные строки подключения и необходимые tooupdate их позже будет toomake изменения tooyour исходный код и перекомпилировать приложение hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="78ee7-277">Тем не менее если хранить строки подключения в файле конфигурации, можно изменить их позже, просто обновив файл конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="78ee7-278">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-279">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-279">Reason</span></span>
<span data-ttu-id="78ee7-280">Жестко запрограммированные строки подключения является нежелательным, поскольку возникают проблемы при toobe быстро изменить необходимые строки подключения.</span><span class="sxs-lookup"><span data-stu-id="78ee7-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="78ee7-281">Кроме того Если hello проекту требуется возврат управления toosource toobe, жестко запрограммированные строки подключения привести уязвимости системы безопасности, поскольку hello строки можно увидеть в исходном коде hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-282">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-282">Solution</span></span>
<span data-ttu-id="78ee7-283">Хранение строк соединения в файлах конфигурации hello или средах Azure.</span><span class="sxs-lookup"><span data-stu-id="78ee7-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="78ee7-284">Для автономных приложений используйте параметры строки подключения toostore app.config.</span><span class="sxs-lookup"><span data-stu-id="78ee7-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="78ee7-285">Для размещенных в IIS веб-приложений используйте строки подключения toostore web.config.</span><span class="sxs-lookup"><span data-stu-id="78ee7-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="78ee7-286">Для приложений ASP.NET vNext используйте configuration.json toostore соединения строки.</span><span class="sxs-lookup"><span data-stu-id="78ee7-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="78ee7-287">Сведения об использовании файлов конфигурации, таких как web.config или app.config, см. в разделе [Правила веб-конфигурации ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="78ee7-288">Сведения о принципах работы переменных среды Azure см. в записи блога [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) (Веб-сайты Microsoft Azure: как работают строки приложения и строки подключения).</span><span class="sxs-lookup"><span data-stu-id="78ee7-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="78ee7-289">Чтобы узнать о хранении строки подключения в системе управления версиями см. в разделе [Source Control (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control) (Система управления версиями (создание реальных облачных приложений в Azure)).</span><span class="sxs-lookup"><span data-stu-id="78ee7-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="78ee7-290">Использование файла конфигурации диагностики</span><span class="sxs-lookup"><span data-stu-id="78ee7-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-291">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-291">ID</span></span>
<span data-ttu-id="78ee7-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="78ee7-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-293">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-293">Description</span></span>
<span data-ttu-id="78ee7-294">Вместо настройки параметров диагностики в коде, например, с помощью Здравствуйте Microsoft.WindowsAzure.Diagnostics программным интерфейсом API, следует настроить параметры диагностики в файле diagnostics.wadcfg hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="78ee7-295">(или в файле diagnostics.wadcfgx, если используется пакет Azure SDK 2.5).</span><span class="sxs-lookup"><span data-stu-id="78ee7-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="78ee7-296">Таким образом, можно изменить параметры диагностики без необходимости toorecompile кода.</span><span class="sxs-lookup"><span data-stu-id="78ee7-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="78ee7-297">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-298">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-298">Reason</span></span>
<span data-ttu-id="78ee7-299">Прежде чем Azure SDK 2.5 (с использованием диагностики Azure 1.3), Azure Diagnostics (WAD) можно было настраивать с использованием нескольких методов: добавление его toohello конфигурации BLOB-объектов в хранилище, с помощью императивного кода, декларативной конфигурации или по умолчанию hello Конфигурация.</span><span class="sxs-lookup"><span data-stu-id="78ee7-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="78ee7-300">Тем не менее hello предпочтительный способ tooconfigure диагностики — toouse файла конфигурации XML (diagnostics.wadcfg или diagnositcs.wadcfgx для пакета SDK 2.5 и более поздние версии) в проект приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="78ee7-301">При таком подходе файл diagnostics.wadcfg hello полностью определяет конфигурацию hello и может обновляться и повторно развертываться по желанию.</span><span class="sxs-lookup"><span data-stu-id="78ee7-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="78ee7-302">Смешивание hello использование файла конфигурации diagnostics.wadcfg hello с hello программными методами настройки конфигураций при применении hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)или [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) классы можно привести tooconfusion.</span><span class="sxs-lookup"><span data-stu-id="78ee7-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="78ee7-303">Дополнительную информацию см. в статье [Инициализация или изменение конфигурации службы диагностики Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ee7-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="78ee7-304">Начиная с версии 1.3 службы WAD (входит в состав пакета Azure SDK 2.5), он больше не tooconfigure диагностики возможных toouse кода.</span><span class="sxs-lookup"><span data-stu-id="78ee7-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="78ee7-305">В результате можно предоставить только hello конфигурации при применении или обновлении расширения диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-306">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-306">Solution</span></span>
<span data-ttu-id="78ee7-307">Использование hello конфигурации конструктора toomove параметров диагностики toohello диагностики файла конфигурации диагностики (diagnositcs.wadcfg или diagnositcs.wadcfgx для пакета SDK 2.5 и более поздние версии).</span><span class="sxs-lookup"><span data-stu-id="78ee7-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="78ee7-308">Кроме того, рекомендуется установить [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) и использовать последние функции диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="78ee7-309">Hello контекстного меню для роли hello, которое следует tooconfigure выберите свойства и выберите вкладки "Конфигурация" hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="78ee7-310">В hello **диагностики** статьи, убедитесь, что hello **включить диагностику** установлен флажок.</span><span class="sxs-lookup"><span data-stu-id="78ee7-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="78ee7-311">Выберите hello **Настройка** кнопки.</span><span class="sxs-lookup"><span data-stu-id="78ee7-311">Choose hello **Configure** button.</span></span>

   ![Доступ к параметр Включить диагностику hello](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="78ee7-313">Дополнительную информацию см. в статье [Настройка системы диагностики для облачных служб и виртуальных машин Azure](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="78ee7-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="78ee7-314">Не объявляйте объекты DbContext статическими</span><span class="sxs-lookup"><span data-stu-id="78ee7-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="78ee7-315">ИД</span><span class="sxs-lookup"><span data-stu-id="78ee7-315">ID</span></span>
<span data-ttu-id="78ee7-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="78ee7-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="78ee7-317">Описание</span><span class="sxs-lookup"><span data-stu-id="78ee7-317">Description</span></span>
<span data-ttu-id="78ee7-318">toosave памяти, не объявляйте объекты DBContext как статические.</span><span class="sxs-lookup"><span data-stu-id="78ee7-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="78ee7-319">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="78ee7-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="78ee7-320">Причина</span><span class="sxs-lookup"><span data-stu-id="78ee7-320">Reason</span></span>
<span data-ttu-id="78ee7-321">Объекты DBContext содержат hello результаты запроса из каждого вызова.</span><span class="sxs-lookup"><span data-stu-id="78ee7-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="78ee7-322">Статические объекты DBContext не удаляются, пока не будет выгружен домен приложения hello.</span><span class="sxs-lookup"><span data-stu-id="78ee7-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="78ee7-323">В связи с этим статический объект DBContext может использовать большой объем памяти.</span><span class="sxs-lookup"><span data-stu-id="78ee7-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="78ee7-324">Решение</span><span class="sxs-lookup"><span data-stu-id="78ee7-324">Solution</span></span>
<span data-ttu-id="78ee7-325">Объявите DBContext как локальную переменную или поле нестатического экземпляра, используйте его для задачи, а после использования он будет удален.</span><span class="sxs-lookup"><span data-stu-id="78ee7-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="78ee7-326">Следующий пример класса контроллера MVC Hello показано, как toouse hello объекта DBContext.</span><span class="sxs-lookup"><span data-stu-id="78ee7-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="78ee7-327">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78ee7-327">Next steps</span></span>
<span data-ttu-id="78ee7-328">toolearn Дополнительные сведения о оптимизация и устранение неполадок приложения Azure в разделе [Устранение неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="78ee7-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
