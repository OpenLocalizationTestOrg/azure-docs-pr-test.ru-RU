---
title: "Оптимизация кода Azure в Visual Studio | Документация Майкрософт"
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
ms.openlocfilehash: 8f145502a856798d6e69ac11f324c72fa23f938e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="a8d82-103">Оптимизация кода Azure</span><span class="sxs-lookup"><span data-stu-id="a8d82-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="a8d82-104">Существуют определенные принципы программирования, позволяющие избежать проблем с масштабированием, поведением и производительностью приложений, использующих Microsoft Azure, в облачной среде.</span><span class="sxs-lookup"><span data-stu-id="a8d82-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow to help avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="a8d82-105">Майкрософт предлагает инструмент анализа кода Azure, который распознает и идентифицирует часто встречающиеся проблемы, а также помогает их решить.</span><span class="sxs-lookup"><span data-stu-id="a8d82-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="a8d82-106">Его можно загрузить в Visual Studio на платформе NuGet.</span><span class="sxs-lookup"><span data-stu-id="a8d82-106">You can download the tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="a8d82-107">Правила анализа кода Azure</span><span class="sxs-lookup"><span data-stu-id="a8d82-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="a8d82-108">Выявляя известные проблемы, влияющие на производительность, инструмент анализа кода Azure автоматически помечает соответствующий код Azure в соответствии с описанными ниже правилами.</span><span class="sxs-lookup"><span data-stu-id="a8d82-108">The Azure Code Analysis tool uses the following rules to automatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="a8d82-109">Обнаруженные проблемы отображаются в виде предупреждений или ошибок компилятора.</span><span class="sxs-lookup"><span data-stu-id="a8d82-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="a8d82-110">Для отображения рекомендаций по устранению ошибок и предупреждений используется значок лампочки.</span><span class="sxs-lookup"><span data-stu-id="a8d82-110">Code fixes or suggestions to resolve the warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="a8d82-111">Старайтесь не использовать режим состояния сеанса по умолчанию (внутрипроцессорный)</span><span class="sxs-lookup"><span data-stu-id="a8d82-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-112">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-112">ID</span></span>
<span data-ttu-id="a8d82-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="a8d82-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-114">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8d82-114">Description</span></span>
<span data-ttu-id="a8d82-115">При использовании режима состояния сеанса по умолчанию (внутрипроцессный) для облачных приложений можно потерять состояние сеанса.</span><span class="sxs-lookup"><span data-stu-id="a8d82-115">If you use the default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="a8d82-116">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-117">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-117">Reason</span></span>
<span data-ttu-id="a8d82-118">По умолчанию режимом состояния сеанса, указанным в файле web.config, является внутрипроцессный.</span><span class="sxs-lookup"><span data-stu-id="a8d82-118">By default, the session state mode specified in the web.config file is in-process.</span></span> <span data-ttu-id="a8d82-119">Кроме того, если в файле конфигурации нет соответствующей записи, режимом состояния сеанса по умолчанию становится внутрипроцессный.</span><span class="sxs-lookup"><span data-stu-id="a8d82-119">Also, if no entry specified in the configuration file, the Session State mode defaults to in-process.</span></span> <span data-ttu-id="a8d82-120">Внутрипроцессный режим хранит состояние сеанса в памяти на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="a8d82-120">The in-process mode stores session state in memory on the web server.</span></span> <span data-ttu-id="a8d82-121">При перезапуске экземпляра или при использовании нового экземпляра для балансировки нагрузки и отработки отказа не сохраняется состояние сеанса, хранимое в памяти на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="a8d82-121">When an instance is restarted or a new instance is used for load balancing or failover support, the session state stored in memory on the web server isn’t saved.</span></span> <span data-ttu-id="a8d82-122">Такая ситуация не позволяет приложению быть масштабируемым в облаке.</span><span class="sxs-lookup"><span data-stu-id="a8d82-122">This situation prevents the application from being scalable on the cloud.</span></span>

<span data-ttu-id="a8d82-123">Состояние сеанса ASP.NET поддерживает несколько различных параметров хранения данных о состоянии сеанса: InProc, StateServer, SQLServer, Custom и Off.</span><span class="sxs-lookup"><span data-stu-id="a8d82-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="a8d82-124">Рекомендуется использовать пользовательский режим для размещения данных на внешнем хранилище состояния сеанса, таком как [поставщик состояния сеанса Azure для Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="a8d82-124">It’s recommended that you use Custom mode to host data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-125">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-125">Solution</span></span>
<span data-ttu-id="a8d82-126">Одно из рекомендуемых решений — хранение состояния сеанса в управляемой службе кэша.</span><span class="sxs-lookup"><span data-stu-id="a8d82-126">One recommended solution is to store session state on a managed cache service.</span></span> <span data-ttu-id="a8d82-127">Узнайте, как сохранять состояния сеанса, используя [поставщик состояний сеанса Azure для Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="a8d82-127">Learn how to use [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) to store your session state.</span></span> <span data-ttu-id="a8d82-128">Чтобы обеспечить масштабируемость приложения в облаке, состояния сеансов можно хранить и в других местах.</span><span class="sxs-lookup"><span data-stu-id="a8d82-128">You can also store session state in other places to ensure your application is scalable on the cloud.</span></span> <span data-ttu-id="a8d82-129">Чтобы больше узнать об альтернативных решениях, ознакомьтесь со статьей [Режимы состояний сеанса](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="a8d82-129">To learn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="a8d82-130">Метод Run не должен быть асинхронным</span><span class="sxs-lookup"><span data-stu-id="a8d82-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-131">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-131">ID</span></span>
<span data-ttu-id="a8d82-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="a8d82-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-133">Описание</span><span class="sxs-lookup"><span data-stu-id="a8d82-133">Description</span></span>
<span data-ttu-id="a8d82-134">Создайте асинхронные методы (такие как [await](https://msdn.microsoft.com/library/hh156528.aspx)) вне метода [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx), а затем вызовите эти методы из [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call the async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="a8d82-135">Объявление метода [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) асинхронным приводит к тому, что рабочая роль входит в цикл перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="a8d82-135">Declaring the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes the worker role to enter a restart loop.</span></span>

<span data-ttu-id="a8d82-136">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-137">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-137">Reason</span></span>
<span data-ttu-id="a8d82-138">Вызов асинхронных методов в методе [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) заставляет среду выполнения облачной службы обновить рабочую роль.</span><span class="sxs-lookup"><span data-stu-id="a8d82-138">Calling async methods inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the cloud service runtime to recycle the worker role.</span></span> <span data-ttu-id="a8d82-139">При запуске рабочей роли все выполнение программы происходит в методе [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a8d82-139">When a worker role starts, all program execution takes place inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="a8d82-140">Выход из метода [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) приводит к перезапуску рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="a8d82-140">Exiting the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the worker role to restart.</span></span> <span data-ttu-id="a8d82-141">В случаях, когда среда выполнения рабочей роли сталкивается с асинхронным методом, она производит диспетчеризацию всех операций после асинхронного метода, а затем возвращается.</span><span class="sxs-lookup"><span data-stu-id="a8d82-141">When the worker role runtime hits the async method, it dispatches all operations after the async method and then returns.</span></span> <span data-ttu-id="a8d82-142">Это приводит к тому, что рабочая роль выходит из метода [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) и перезапускается.</span><span class="sxs-lookup"><span data-stu-id="a8d82-142">This causes the worker role to exit from the [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="a8d82-143">В следующей итерации выполнения рабочая роль снова попадает на асинхронный метод и перезапускается, что опять приводит к ее обновлению.</span><span class="sxs-lookup"><span data-stu-id="a8d82-143">In the next iteration of execution, the worker role hits the async method again and restarts, causing the worker role to recycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-144">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-144">Solution</span></span>
<span data-ttu-id="a8d82-145">Разместите все асинхронные операции вне метода [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a8d82-145">Place all async operations outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="a8d82-146">Затем вызовите рефакторизованный асинхронный метод из метода [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) , например RunAsync().wait.</span><span class="sxs-lookup"><span data-stu-id="a8d82-146">Then, call the refactored async method from inside the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="a8d82-147">Инструмент анализа кода Azure может помочь решить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="a8d82-147">The Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="a8d82-148">В следующем фрагменте кода продемонстрировано исправление кода для устранения этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="a8d82-148">The following code snippet demonstrates the code fix for this issue:</span></span>

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

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="a8d82-149">Использование проверки подлинности подписанного URL-адреса с помощью служебной шины</span><span class="sxs-lookup"><span data-stu-id="a8d82-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-150">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-150">ID</span></span>
<span data-ttu-id="a8d82-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="a8d82-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-152">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8d82-152">Description</span></span>
<span data-ttu-id="a8d82-153">Используйте для проверки подлинности подписанный URL-адрес (SAS).</span><span class="sxs-lookup"><span data-stu-id="a8d82-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="a8d82-154">Служба управления доступом (ACS) больше не используется для проверки подлинности служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a8d82-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="a8d82-155">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-156">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-156">Reason</span></span>
<span data-ttu-id="a8d82-157">Для повышения уровня безопасности Azure Active Directory заменяет проверку подлинности с помощью ACS на проверку подлинности с использованием SAS.</span><span class="sxs-lookup"><span data-stu-id="a8d82-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="a8d82-158">Информацию о плане перехода см. в статье [Azure Active Directory is the future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) (Azure Active Directory — будущее для ACS).</span><span class="sxs-lookup"><span data-stu-id="a8d82-158">See [Azure Active Directory is the future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on the transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-159">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-159">Solution</span></span>
<span data-ttu-id="a8d82-160">В приложениях используйте проверку подлинности SAS.</span><span class="sxs-lookup"><span data-stu-id="a8d82-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="a8d82-161">В приведенном ниже примере показано использование существующего токена SAS для доступа к пространству имен или сущности служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a8d82-161">The following example shows how to use an existing SAS token to access a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="a8d82-162">Дополнительные сведения см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="a8d82-162">See the following topics for more information.</span></span>

* <span data-ttu-id="a8d82-163">Общие сведения см. в статье [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx) (Аутентификация на основе подписанного URL-адреса с помощью служебной шины).</span><span class="sxs-lookup"><span data-stu-id="a8d82-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="a8d82-164">Использование проверки подлинности подписанного URL-адреса с помощью служебной шины</span><span class="sxs-lookup"><span data-stu-id="a8d82-164">How to use Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="a8d82-165">Пример проекта см. на странице [Примеры кода Azure](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c).</span><span class="sxs-lookup"><span data-stu-id="a8d82-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-to-avoid-receive-loop"></a><span data-ttu-id="a8d82-166">Рекомендуется использовать метод OnMessage, чтобы избежать "цикла получения"</span><span class="sxs-lookup"><span data-stu-id="a8d82-166">Consider using OnMessage method to avoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-167">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-167">ID</span></span>
<span data-ttu-id="a8d82-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="a8d82-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-169">Описание</span><span class="sxs-lookup"><span data-stu-id="a8d82-169">Description</span></span>
<span data-ttu-id="a8d82-170">Чтобы избежать вхождения в "цикл получения", для получения сообщений лучше использовать вызов метода **OnMessage**, чем вызов метода **Receive**.</span><span class="sxs-lookup"><span data-stu-id="a8d82-170">To avoid going into a "receive loop," calling the **OnMessage** method is a better solution for receiving messages than calling the **Receive** method.</span></span> <span data-ttu-id="a8d82-171">Но если необходимо использовать метод **Receive** и задать время ожидания сервера, отличное от значения по умолчанию, убедитесь, что время ожидания сервера превышает одну минуту.</span><span class="sxs-lookup"><span data-stu-id="a8d82-171">However, if you must use the **Receive** method, and you specify a non-default server wait time, make sure the server wait time is more than one minute.</span></span>

<span data-ttu-id="a8d82-172">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-173">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-173">Reason</span></span>
<span data-ttu-id="a8d82-174">При вызове метода **OnMessage**клиент начинает процесс обработки внутренних сообщений, который постоянно опрашивает очередь или подписку.</span><span class="sxs-lookup"><span data-stu-id="a8d82-174">When calling **OnMessage**, the client starts an internal message pump that constantly polls the queue or subscription.</span></span> <span data-ttu-id="a8d82-175">Этот процесс обработки сообщений содержит бесконечный цикл, который отправляет вызов для получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="a8d82-175">This message pump contains an infinite loop that issues a call to receive messages.</span></span> <span data-ttu-id="a8d82-176">Если время ожидания вызова истекает, выдается новый вызов.</span><span class="sxs-lookup"><span data-stu-id="a8d82-176">If the call times out, it issues a new call.</span></span> <span data-ttu-id="a8d82-177">Интервал времени ожидания определяется по значению свойства [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) используемого [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-177">The timeout interval is determined by the value of the [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of the [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="a8d82-178">Преимущество метода **OnMessage** по сравнению с методом **Receive** заключается в том, что пользователям не требуется вручную извлекать сообщения, обрабатывать исключения, параллельно обрабатывать несколько сообщений и завершать сообщения.</span><span class="sxs-lookup"><span data-stu-id="a8d82-178">The advantage of using **OnMessage** compared to **Receive** is that users don’t have to manually poll for messages, handle exceptions, process multiple messages in parallel, and complete the messages.</span></span>

<span data-ttu-id="a8d82-179">При вызове метода **Receive** без использования значения по умолчанию убедитесь, что значение *ServerWaitTime* превышает одну минуту.</span><span class="sxs-lookup"><span data-stu-id="a8d82-179">If you call **Receive** without using its default value, be sure the *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="a8d82-180">Установка для *ServerWaitTime* значения больше одной минуты позволяет предотвратить истечение времени ожидания сервера до полного получения сообщения.</span><span class="sxs-lookup"><span data-stu-id="a8d82-180">Setting *ServerWaitTime* to more than one minute prevents the server from timing out before the message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-181">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-181">Solution</span></span>
<span data-ttu-id="a8d82-182">См. примеры рекомендованного использования кода ниже.</span><span class="sxs-lookup"><span data-stu-id="a8d82-182">Please see the following code examples for recommended usages.</span></span> <span data-ttu-id="a8d82-183">Дополнительные сведения см. в статьях [Метод QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) и [Метод QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="a8d82-184">Для повышения производительности инфраструктуры обмена сообщениями Azure ознакомьтесь с шаблоном проекта в разделе [Учебник по асинхронному обмену сообщениями](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-184">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="a8d82-185">Ниже приведен пример использования метода **OnMessage** для получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="a8d82-185">The following is an example of using **OnMessage** to receive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if the message-pump should call complete on messages after the callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates the maximum number of concurrent calls to the callback the pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you to get notified of any errors encountered by the message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates the message pump and callback is invoked for each message that is recieved, calling close on the client will stop the pump.
    {
        // Process the message.
    }, options);
    Console.WriteLine("Press any key to exit.");
    Console.ReadKey();
```

<span data-ttu-id="a8d82-186">Ниже приведен пример использования метода **Receive** с временем ожидания сервера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a8d82-186">The following is an example of using **Receive** with the default server wait time.</span></span>

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

<span data-ttu-id="a8d82-187">Ниже приведен пример использования метода **Receive** с временем ожидания сервера не по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a8d82-187">The following is an example of using **Receive** with a non-default server wait time.</span></span>

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
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="a8d82-188">Рассмотрите возможность использования асинхронных методов служебной шины</span><span class="sxs-lookup"><span data-stu-id="a8d82-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-189">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-189">ID</span></span>
<span data-ttu-id="a8d82-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="a8d82-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-191">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8d82-191">Description</span></span>
<span data-ttu-id="a8d82-192">Используйте асинхронные методы служебной шины для повышения производительности обмена сообщениями через посредника.</span><span class="sxs-lookup"><span data-stu-id="a8d82-192">Use asynchronous Service Bus methods to improve performance with brokered messaging.</span></span>

<span data-ttu-id="a8d82-193">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-194">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-194">Reason</span></span>
<span data-ttu-id="a8d82-195">Использование асинхронных методов обеспечивает программный параллелизм приложений, так как выполнение каждого вызова не блокирует основной поток.</span><span class="sxs-lookup"><span data-stu-id="a8d82-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block the main thread.</span></span> <span data-ttu-id="a8d82-196">При использовании методов обмена сообщениями служебной шины требуется время на выполнение операции (отправки, получения, удаления и т. д.).</span><span class="sxs-lookup"><span data-stu-id="a8d82-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="a8d82-197">В это время входит обработка операции службой Service Bus, а также задержка запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="a8d82-197">This time includes the processing of the operation by the Service Bus service in addition to the latency of the request and the reply.</span></span> <span data-ttu-id="a8d82-198">Чтобы увеличить количество операций в единицу времени, необходимо выполнять их параллельно.</span><span class="sxs-lookup"><span data-stu-id="a8d82-198">To increase the number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="a8d82-199">Дополнительные сведения см. в статье [Советы и рекомендации по повышению производительности с помощью обмена сообщениями через посредника служебной шины](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-199">For more information please refer to [Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-200">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-200">Solution</span></span>
<span data-ttu-id="a8d82-201">Сведения о способах использования рекомендованного асинхронного метода см. в статье [Класс QueueClient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how to use the recommended asynchronous method.</span></span>

<span data-ttu-id="a8d82-202">Для повышения производительности инфраструктуры обмена сообщениями Azure ознакомьтесь с шаблоном проекта в разделе [Учебник по асинхронному обмену сообщениями](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-202">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="a8d82-203">Попробуйте секционировать очереди и разделы служебной шины</span><span class="sxs-lookup"><span data-stu-id="a8d82-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-204">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-204">ID</span></span>
<span data-ttu-id="a8d82-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="a8d82-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-206">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8d82-206">Description</span></span>
<span data-ttu-id="a8d82-207">Секционирование очередей и разделов служебной шины для повышения производительности обмена сообщениями служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a8d82-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="a8d82-208">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-209">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-209">Reason</span></span>
<span data-ttu-id="a8d82-210">Секционирование очередей и разделов служебной шины повышает производительность, пропускную способность и доступность службы, поскольку общая пропускная способность секционированной очереди или раздела не ограничивается производительностью одного брокера сообщений или хранилища сообщений.</span><span class="sxs-lookup"><span data-stu-id="a8d82-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because the overall throughput of a partitioned queue or topic is no longer limited by the performance of a single message broker or messaging store.</span></span> <span data-ttu-id="a8d82-211">Кроме того, из-за временного сбоя хранилища сообщений секционированная очередь или раздел не становятся недоступными.</span><span class="sxs-lookup"><span data-stu-id="a8d82-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="a8d82-212">Дополнительную информацию см. в разделе [Разделение сущностей обмена сообщениями](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-213">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-213">Solution</span></span>
<span data-ttu-id="a8d82-214">В следующем фрагменте кода показано, как выполнить секционирование сущностей обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="a8d82-214">The following code snippet shows how to partition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="a8d82-215">Чтобы узнать больше, ознакомьтесь с записью [блога Microsoft Azure, посвященной секционированным очередям и разделам служебной шины](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/), и примером [секционированной очереди служебной шины Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f).</span><span class="sxs-lookup"><span data-stu-id="a8d82-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out the [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="a8d82-216">Не задавайте значение SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="a8d82-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-217">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-217">ID</span></span>
<span data-ttu-id="a8d82-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="a8d82-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-219">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8d82-219">Description</span></span>
<span data-ttu-id="a8d82-220">Не задавайте значение текущего времени для параметра SharedAccessStartTime, чтобы немедленно запустить политику общего доступа.</span><span class="sxs-lookup"><span data-stu-id="a8d82-220">You should avoid using SharedAccessStartTimeset to the current time to immediately start the Shared Access policy.</span></span> <span data-ttu-id="a8d82-221">Это свойство следует задавать только в тех случаях, если политику общего доступа планируется запустить позднее.</span><span class="sxs-lookup"><span data-stu-id="a8d82-221">You only need to set this property if you want to start the Shared Access policy at a later time.</span></span>

<span data-ttu-id="a8d82-222">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-223">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-223">Reason</span></span>
<span data-ttu-id="a8d82-224">Синхронизация часов вызывает небольшую разницу во времени между центрами обработки данных.</span><span class="sxs-lookup"><span data-stu-id="a8d82-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="a8d82-225">Например, может показаться логичным, что если указать время запуска политики SAS хранилища на текущее время с помощью метода DateTime.Now или аналогичного метода, то это вызовет немедленное применение политики SAS.</span><span class="sxs-lookup"><span data-stu-id="a8d82-225">For example, you would logically think setting the start time of a storage SAS policy as the current time by using DateTime.Now or a similar method will cause the SAS policy to take effect immediately.</span></span> <span data-ttu-id="a8d82-226">Однако небольшая разница во времени между центрами обработки данных может вызывать проблемы, так как одни центры обработки данных будут немного отставать от времени запуска, а другие — опережать.</span><span class="sxs-lookup"><span data-stu-id="a8d82-226">However, the slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than the start time, while others ahead of it.</span></span> <span data-ttu-id="a8d82-227">В результате срок действия политики SAS может быстро (или даже немедленно) закончиться, если установлено слишком короткое время жизни политики.</span><span class="sxs-lookup"><span data-stu-id="a8d82-227">As a result, the SAS policy can expire quickly (or even immediately) if the policy lifetime is set too short.</span></span>

<span data-ttu-id="a8d82-228">Дополнительные рекомендации по использованию подписанного URL-адреса в службе хранилища Azure см. в записи блога MSDN [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx) (Знакомство с SAS (подписанный URL-адрес) таблиц, SAS очередей и изменениями SAS больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="a8d82-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-229">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-229">Solution</span></span>
<span data-ttu-id="a8d82-230">Удалите инструкцию, которая задает время запуска политики общего доступа.</span><span class="sxs-lookup"><span data-stu-id="a8d82-230">Remove the statement that sets the start time of the shared access policy.</span></span> <span data-ttu-id="a8d82-231">Средство анализа кода Azure может помочь решить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="a8d82-231">The Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="a8d82-232">Чтобы узнать больше об управлении безопасностью, ознакомьтесь с конструктивным шаблоном [Ключ камердинера](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-232">For more information on security management, please see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="a8d82-233">В следующем фрагменте кода продемонстрировано исправление кода для устранения этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="a8d82-233">The following code snippet demonstrates the code fix for this issue.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="a8d82-234">Время окончания срока действия общей политики доступа должно быть больше пяти минут</span><span class="sxs-lookup"><span data-stu-id="a8d82-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-235">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-235">ID</span></span>
<span data-ttu-id="a8d82-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="a8d82-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-237">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8d82-237">Description</span></span>
<span data-ttu-id="a8d82-238">Разница во времени между центрами обработки данных в разных расположениях может составлять до пяти минут в силу условия, известного как расфазировка синхронизирующих импульсов.</span><span class="sxs-lookup"><span data-stu-id="a8d82-238">There can be as much as a five minute difference in clocks among datacenters at different locations due to a condition known as "clock skew."</span></span> <span data-ttu-id="a8d82-239">Чтобы маркер политики SAS не устарел раньше, чем планировалось, установите срок действия больше пяти минут.</span><span class="sxs-lookup"><span data-stu-id="a8d82-239">To prevent the SAS policy token from expiring earlier than planned, set the expiry time to be more than five minutes.</span></span>

<span data-ttu-id="a8d82-240">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-241">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-241">Reason</span></span>
<span data-ttu-id="a8d82-242">Центры обработки данных в разных местах по всему миру синхронизируются по сигналу часов.</span><span class="sxs-lookup"><span data-stu-id="a8d82-242">Datacenters at different locations around the world synchronize by a clock signal.</span></span> <span data-ttu-id="a8d82-243">Поскольку передача сигнала в разные расположения требует времени, возможна разница во времени между центрами обработки в разных географических местоположениях, хотя теоретически все синхронизировано.</span><span class="sxs-lookup"><span data-stu-id="a8d82-243">Because it takes time for clock signal to travel to different locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="a8d82-244">Разница во времени может повлиять на время запуска и интервал истечения срока действия политики общего доступа.</span><span class="sxs-lookup"><span data-stu-id="a8d82-244">This time difference can affect the Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="a8d82-245">Таким образом, чтобы убедиться, что политика общего доступа вступает в силу немедленно, не указывайте время начала.</span><span class="sxs-lookup"><span data-stu-id="a8d82-245">Therefore, to ensure Shared Access policy takes effect immediately, don’t specify the start time.</span></span> <span data-ttu-id="a8d82-246">Кроме того, убедитесь, что срок действия составляет более 5 минут, чтобы предотвратить раннее истечение времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="a8d82-246">In addition, make sure the expiration time is more than 5 minutes to prevent early timeout.</span></span>

<span data-ttu-id="a8d82-247">Дополнительную информацию по использованию подписанного URL-адреса в службе хранилища Azure см. в записи блога MSDN [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx) (Знакомство с SAS (подписанный URL-адрес) таблиц, SAS очередей и изменениями SAS больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="a8d82-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-248">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-248">Solution</span></span>
<span data-ttu-id="a8d82-249">Чтобы узнать больше об управлении безопасностью, ознакомьтесь с конструктивным шаблоном [Ключ камердинера](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-249">For more information on security management, see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="a8d82-250">Ниже приведен пример, в котором не указано время запуска политики общего доступа.</span><span class="sxs-lookup"><span data-stu-id="a8d82-250">The following is an example of not specifying a Shared Access policy start time.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="a8d82-251">Ниже приведен пример, в котором указано время запуска политики общего доступа со сроком действия больше пяти минут.</span><span class="sxs-lookup"><span data-stu-id="a8d82-251">The following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="a8d82-252">Дополнительную информацию см. в статье [Создание и использование подписанного URL-адреса](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="a8d82-253">Используйте CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="a8d82-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-254">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-254">ID</span></span>
<span data-ttu-id="a8d82-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="a8d82-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-256">Описание</span><span class="sxs-lookup"><span data-stu-id="a8d82-256">Description</span></span>
<span data-ttu-id="a8d82-257">Использование класса [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) для таких проектов, как веб-сайт Azure и мобильные службы Azure, не вызовет проблем времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="a8d82-257">Using the [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="a8d82-258">Рекомендуется использовать Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) как единый способ управления конфигурациями всех облачных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d82-258">As a best practice, however, it's a good idea to use Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="a8d82-259">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-260">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-260">Reason</span></span>
<span data-ttu-id="a8d82-261">CloudConfigurationManager выполняет считывание файла конфигурации, который подходит для среды приложения.</span><span class="sxs-lookup"><span data-stu-id="a8d82-261">CloudConfigurationManager reads the configuration file appropriate to the application environment.</span></span>

[<span data-ttu-id="a8d82-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="a8d82-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="a8d82-263">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-263">Solution</span></span>
<span data-ttu-id="a8d82-264">Переработайте свой код для использования [класса CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-264">Refactor your code to use the [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="a8d82-265">Инструмент анализа кода Azure позволяет исправить код и устранить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="a8d82-265">A code fix for this issue is provided by the Azure Code Analysis tool.</span></span>

<span data-ttu-id="a8d82-266">В следующем фрагменте кода продемонстрировано исправление кода для устранения этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="a8d82-266">The following code snippet demonstrates the code fix for this issue.</span></span> <span data-ttu-id="a8d82-267">Замените</span><span class="sxs-lookup"><span data-stu-id="a8d82-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="a8d82-268">на</span><span class="sxs-lookup"><span data-stu-id="a8d82-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="a8d82-269">Ниже приведен пример того, как сохранить параметры конфигурации в файл App.config или Web.config.</span><span class="sxs-lookup"><span data-stu-id="a8d82-269">Here's an example of how to store the configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="a8d82-270">Добавьте параметры в раздел appSettings файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a8d82-270">Add the settings to the appSettings section of the configuration file.</span></span> <span data-ttu-id="a8d82-271">Ниже приведен файл Web.config для предыдущего примера кода.</span><span class="sxs-lookup"><span data-stu-id="a8d82-271">The following is the Web.config file for the previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="a8d82-272">Избегайте использования жестко запрограммированных строк подключения</span><span class="sxs-lookup"><span data-stu-id="a8d82-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-273">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-273">ID</span></span>
<span data-ttu-id="a8d82-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="a8d82-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-275">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8d82-275">Description</span></span>
<span data-ttu-id="a8d82-276">Если используются жестко запрограммированные строки подключения, которые вам потребуется обновить позднее, необходимо внести изменения в исходный код и перекомпилировать приложение.</span><span class="sxs-lookup"><span data-stu-id="a8d82-276">If you use hard-coded connection strings and you need to update them later, you’ll have to make changes to your source code and recompile the application.</span></span> <span data-ttu-id="a8d82-277">Но если хранить строки подключения в файле конфигурации, вы сможете изменить их позже, просто обновив файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a8d82-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating the configuration file.</span></span>

<span data-ttu-id="a8d82-278">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-279">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-279">Reason</span></span>
<span data-ttu-id="a8d82-280">Не рекомендуется использовать жестко запрограммированные строки подключения, так как из-за этого возникают проблемы при необходимости быстро изменить строки подключения.</span><span class="sxs-lookup"><span data-stu-id="a8d82-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need to be changed quickly.</span></span> <span data-ttu-id="a8d82-281">Кроме того, если проект должен быть помещен в систему управления версиями, жестко запрограммированные строки подключения делают систему безопасности уязвимой, так как строки можно увидеть в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="a8d82-281">In addition, if the project needs to be checked in to source control, hard-coded connection strings introduce security vulnerabilities since the strings can be viewed in the source code.</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-282">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-282">Solution</span></span>
<span data-ttu-id="a8d82-283">Храните строки подключения в файлах конфигурации или в средах Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d82-283">Store connection strings in the configuration files or Azure environments.</span></span>

* <span data-ttu-id="a8d82-284">Для автономных приложений используйте для хранения параметров строки подключения файл app.config.</span><span class="sxs-lookup"><span data-stu-id="a8d82-284">For standalone applications, use app.config to store connection string settings.</span></span>
* <span data-ttu-id="a8d82-285">Для веб-приложений, размещенных в IIS, используйте для хранения параметров строки подключения файл web.config.</span><span class="sxs-lookup"><span data-stu-id="a8d82-285">For IIS-hosted web applications, use web.config to store connection strings.</span></span>
* <span data-ttu-id="a8d82-286">Для приложений ASP.NET vNext используйте для хранения параметров строки подключения файл configuration.json.</span><span class="sxs-lookup"><span data-stu-id="a8d82-286">For ASP.NET vNext applications, use configuration.json to store connection strings.</span></span>

<span data-ttu-id="a8d82-287">Сведения об использовании файлов конфигурации, таких как web.config или app.config, см. в разделе [Правила веб-конфигурации ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="a8d82-288">Сведения о принципах работы переменных среды Azure см. в записи блога [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) (Веб-сайты Microsoft Azure: как работают строки приложения и строки подключения).</span><span class="sxs-lookup"><span data-stu-id="a8d82-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="a8d82-289">Чтобы узнать о хранении строки подключения в системе управления версиями см. в разделе [Source Control (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control) (Система управления версиями (создание реальных облачных приложений в Azure)).</span><span class="sxs-lookup"><span data-stu-id="a8d82-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="a8d82-290">Использование файла конфигурации диагностики</span><span class="sxs-lookup"><span data-stu-id="a8d82-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-291">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-291">ID</span></span>
<span data-ttu-id="a8d82-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="a8d82-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-293">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8d82-293">Description</span></span>
<span data-ttu-id="a8d82-294">Вместо настройки параметров диагностики в коде, например с помощью API программирования Microsoft.WindowsAzure.Diagnostics, следует настроить параметры диагностики в файле diagnostics.wadcfg</span><span class="sxs-lookup"><span data-stu-id="a8d82-294">Instead of configuring diagnostics settings in your code such as by using the Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in the diagnostics.wadcfg file.</span></span> <span data-ttu-id="a8d82-295">(или в файле diagnostics.wadcfgx, если используется пакет Azure SDK 2.5).</span><span class="sxs-lookup"><span data-stu-id="a8d82-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="a8d82-296">Это позволит изменить параметры диагностики без повторной компиляции кода.</span><span class="sxs-lookup"><span data-stu-id="a8d82-296">By doing this, you can change diagnostics settings without having to recompile your code.</span></span>

<span data-ttu-id="a8d82-297">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-298">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-298">Reason</span></span>
<span data-ttu-id="a8d82-299">До появления пакета Azure SDK 2.5 (с использованием диагностики Azure 1.3) диагностику Microsoft Azure (WAD) можно было настраивать с помощью нескольких различных методов: путем ее добавления в BLOB-объект конфигурации в хранилище, с использованием императивного кода, декларативной конфигурации или конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a8d82-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it to the configuration blob in storage, by using imperative code, declarative configuration, or the default configuration.</span></span> <span data-ttu-id="a8d82-300">Однако предпочтительным способом настройки диагностики является использование XML-файла конфигурации (diagnostics.wadcfg или diagnositcs.wadcfgx для пакета SDK 2.5 и более поздних версий) в проекте приложения.</span><span class="sxs-lookup"><span data-stu-id="a8d82-300">However, the preferred way to configure diagnostics is to use an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in the application project.</span></span> <span data-ttu-id="a8d82-301">При таком подходе файл diagnostics.wadcfg полностью определяет конфигурацию, может обновляться и повторно развертываться по желанию.</span><span class="sxs-lookup"><span data-stu-id="a8d82-301">In this approach, the diagnostics.wadcfg file completely defines the configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="a8d82-302">Использование файла конфигурации diagnostics.wadcfg наряду с программными методами настройки конфигураций при применении классов [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx) или [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) может вас запутать.</span><span class="sxs-lookup"><span data-stu-id="a8d82-302">Mixing the use of the diagnostics.wadcfg configuration file with the programmatic methods of setting configurations by using the [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead to confusion.</span></span> <span data-ttu-id="a8d82-303">Дополнительную информацию см. в статье [Инициализация или изменение конфигурации службы диагностики Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8d82-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="a8d82-304">Начиная с версии 1.3 службы WAD (входит в состав пакета SDK для Azure 2.5) нельзя использовать код для настройки диагностики.</span><span class="sxs-lookup"><span data-stu-id="a8d82-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible to use code to configure diagnostics.</span></span> <span data-ttu-id="a8d82-305">В результате вы можете предоставить конфигурацию только при применении или обновлении расширения диагностики.</span><span class="sxs-lookup"><span data-stu-id="a8d82-305">As a result, you can only provide the configuration when applying or updating the diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-306">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-306">Solution</span></span>
<span data-ttu-id="a8d82-307">Используйте конструктор конфигурации диагностики для перемещения диагностических параметров в файл конфигурации диагностики (diagnositcs.wadcfg или diagnositcs.wadcfgx для пакета SDK 2.5 и более поздних версий).</span><span class="sxs-lookup"><span data-stu-id="a8d82-307">Use the diagnostics configuration designer to move diagnostic settings to the diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="a8d82-308">Кроме того, рекомендуется установить пакет [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) и использовать последние функции диагностики.</span><span class="sxs-lookup"><span data-stu-id="a8d82-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use the latest diagnostics feature.</span></span>

1. <span data-ttu-id="a8d82-309">В контекстном меню интересующей вас роли выберите пункт "Свойства", а затем перейдите на вкладку "Конфигурация".</span><span class="sxs-lookup"><span data-stu-id="a8d82-309">On the shortcut menu for the role that you want to configure, choose Properties, and then choose the Configuration tab.</span></span>
2. <span data-ttu-id="a8d82-310">В разделе **Диагностика** установите флажок **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="a8d82-310">In the **Diagnostics** section, make sure that the **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="a8d82-311">Нажмите кнопку **Настроить** .</span><span class="sxs-lookup"><span data-stu-id="a8d82-311">Choose the **Configure** button.</span></span>

   ![Доступ к параметру "Включить диагностику"](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="a8d82-313">Дополнительную информацию см. в статье [Настройка системы диагностики для облачных служб и виртуальных машин Azure](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="a8d82-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="a8d82-314">Не объявляйте объекты DbContext статическими</span><span class="sxs-lookup"><span data-stu-id="a8d82-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="a8d82-315">ИД</span><span class="sxs-lookup"><span data-stu-id="a8d82-315">ID</span></span>
<span data-ttu-id="a8d82-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="a8d82-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="a8d82-317">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a8d82-317">Description</span></span>
<span data-ttu-id="a8d82-318">Для экономии памяти не объявляйте объекты DBContext статическими.</span><span class="sxs-lookup"><span data-stu-id="a8d82-318">To save memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="a8d82-319">Делитесь своими идеями и предложениями на [странице отзывов об анализе кода Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a8d82-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a8d82-320">Причина</span><span class="sxs-lookup"><span data-stu-id="a8d82-320">Reason</span></span>
<span data-ttu-id="a8d82-321">Объекты DBContext содержат результаты запроса из каждого вызова.</span><span class="sxs-lookup"><span data-stu-id="a8d82-321">DBContext objects hold the query results from each call.</span></span> <span data-ttu-id="a8d82-322">Статические объекты DBContext не удаляются, пока не будет выгружен домен приложения.</span><span class="sxs-lookup"><span data-stu-id="a8d82-322">Static DBContext objects are not disposed until the application domain is unloaded.</span></span> <span data-ttu-id="a8d82-323">В связи с этим статический объект DBContext может использовать большой объем памяти.</span><span class="sxs-lookup"><span data-stu-id="a8d82-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="a8d82-324">Решение</span><span class="sxs-lookup"><span data-stu-id="a8d82-324">Solution</span></span>
<span data-ttu-id="a8d82-325">Объявите DBContext как локальную переменную или поле нестатического экземпляра, используйте его для задачи, а после использования он будет удален.</span><span class="sxs-lookup"><span data-stu-id="a8d82-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="a8d82-326">Приведенный пример класса контроллера MVC показывает, как использовать объект DBContext.</span><span class="sxs-lookup"><span data-stu-id="a8d82-326">The following example MVC controller class shows how to use the DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass to DbContext        
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

## <a name="next-steps"></a><span data-ttu-id="a8d82-327">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8d82-327">Next steps</span></span>
<span data-ttu-id="a8d82-328">Дополнительные сведения об оптимизации и устранении неполадок приложений Azure см. в статье [Устранение неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="a8d82-328">To learn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
