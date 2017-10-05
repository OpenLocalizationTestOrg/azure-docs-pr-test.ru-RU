---
title: "Создание приложения .NET Service Fabric в Azure | Документы Майкрософт"
description: "Создание приложения .NET в Azure с помощью примера для Service Fabric."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: d11b9af982112db8ba94b62110c18be843f1abb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a><span data-ttu-id="1036e-103">Создание приложения .NET Service Fabric в Azure</span><span class="sxs-lookup"><span data-stu-id="1036e-103">Create a .NET Service Fabric application in Azure</span></span>
<span data-ttu-id="1036e-104">Azure Service Fabric — это платформа распределенных систем для развертывания масштабируемых надежных микрослужб и контейнеров и управления ими.</span><span class="sxs-lookup"><span data-stu-id="1036e-104">Azure Service Fabric is a distributed systems platform for deploying and managing scalable and reliable microservices and containers.</span></span> 

<span data-ttu-id="1036e-105">В этом руководстве описано, как развернуть свое первое приложение .NET в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1036e-105">This quickstart shows how to deploy your first .NET application to Service Fabric.</span></span> <span data-ttu-id="1036e-106">После завершения этого руководства вы получите приложение для голосования с клиентской частью в виде веб-приложения ASP.NET Core, которое сохраняет результаты голосования во внутренней службе с отслеживанием состояния в кластере.</span><span class="sxs-lookup"><span data-stu-id="1036e-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in the cluster.</span></span>

![Снимок экрана приложения](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

<span data-ttu-id="1036e-108">С помощью этого приложения вы узнаете, как выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1036e-108">Using this application you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1036e-109">Создание приложения с использованием .NET и Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1036e-109">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="1036e-110">Использование ASP.NET Core в качестве клиентского веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="1036e-110">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="1036e-111">Хранение данных приложения в службе с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="1036e-111">Store application data in a stateful service</span></span>
> * <span data-ttu-id="1036e-112">Локальная отладка приложения</span><span class="sxs-lookup"><span data-stu-id="1036e-112">Debug your application locally</span></span>
> * <span data-ttu-id="1036e-113">Развертывание приложения в кластере Azure</span><span class="sxs-lookup"><span data-stu-id="1036e-113">Deploy the application to a cluster in Azure</span></span>
> * <span data-ttu-id="1036e-114">Масштабирование приложения на несколько узлов</span><span class="sxs-lookup"><span data-stu-id="1036e-114">Scale-out the application across multiple nodes</span></span>
> * <span data-ttu-id="1036e-115">Последовательное обновление приложения</span><span class="sxs-lookup"><span data-stu-id="1036e-115">Perform a rolling application upgrade</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1036e-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1036e-116">Prerequisites</span></span>
<span data-ttu-id="1036e-117">Для работы с этим кратким руководством сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1036e-117">To complete this quickstart:</span></span>
1. <span data-ttu-id="1036e-118">[Установите Visual Studio 2017](https://www.visualstudio.com/), а также рабочие нагрузки **разработка Azure** и **ASP.NET и веб-разработка**.</span><span class="sxs-lookup"><span data-stu-id="1036e-118">[Install Visual Studio 2017](https://www.visualstudio.com/) with the **Azure development** and **ASP.NET and web development** workloads.</span></span>
2. <span data-ttu-id="1036e-119">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="1036e-119">[Install Git](https://git-scm.com/)</span></span>
3. [<span data-ttu-id="1036e-120">Установите пакет SDK для Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1036e-120">Install the Microsoft Azure Service Fabric SDK</span></span>](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. <span data-ttu-id="1036e-121">Выполните следующую команду, чтобы разрешить развертывание на локальный кластер Service Fabric в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="1036e-121">Run the following command to enable Visual Studio to deploy to the local Service Fabric cluster:</span></span>
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-the-sample"></a><span data-ttu-id="1036e-122">Скачивание примера приложения</span><span class="sxs-lookup"><span data-stu-id="1036e-122">Download the sample</span></span>
<span data-ttu-id="1036e-123">В окне терминала выполните следующую команду, чтобы клонировать репозиторий с примером приложения на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="1036e-123">In a command window, run the following command to clone the sample app repository to your local machine.</span></span>
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-the-application-locally"></a><span data-ttu-id="1036e-124">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="1036e-124">Run the application locally</span></span>
<span data-ttu-id="1036e-125">Щелкните правой кнопкой мыши значок Visual Studio в меню "Пуск" и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="1036e-125">Right-click the Visual Studio icon in the Start Menu and choose **Run as administrator**.</span></span> <span data-ttu-id="1036e-126">Чтобы подключить отладчик к службам, необходимо запустить Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="1036e-126">In order to attach the debugger to your services, you need to run Visual Studio as administrator.</span></span>

<span data-ttu-id="1036e-127">В клонированном репозитории откройте решение **Voting.sln** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1036e-127">Open the **Voting.sln** Visual Studio solution from the repository you cloned.</span></span>

<span data-ttu-id="1036e-128">Чтобы развернуть приложение, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="1036e-128">To deploy the application, press **F5**.</span></span>

> [!NOTE]
> <span data-ttu-id="1036e-129">Во время первого запуска и развертывания приложения Visual Studio создает локальный кластер для отладки.</span><span class="sxs-lookup"><span data-stu-id="1036e-129">The first time you run and deploy the application, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="1036e-130">Эта операция может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="1036e-130">This operation may take some time.</span></span> <span data-ttu-id="1036e-131">Процесс создания кластера можно наблюдать в окне вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1036e-131">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="1036e-132">После завершения развертывания будет открыто окно браузера со страницей `http://localhost:8080`. Это страница веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1036e-132">When the deployment is complete, launch a browser and open this page: `http://localhost:8080` - the web front-end of the application.</span></span>

![Клиентская часть приложения](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

<span data-ttu-id="1036e-134">Теперь можно добавить варианты для выбора в голосовании и начать прием голосов.</span><span class="sxs-lookup"><span data-stu-id="1036e-134">You can now add a set of voting options, and start taking votes.</span></span> <span data-ttu-id="1036e-135">Приложение запускается и хранит все данные в кластере Service Fabric без необходимости использования отдельной базы данных.</span><span class="sxs-lookup"><span data-stu-id="1036e-135">The application runs and stores all data in your Service Fabric cluster, without the need for a separate database.</span></span>

## <a name="walk-through-the-voting-sample-application"></a><span data-ttu-id="1036e-136">Описание примера приложения для голосования</span><span class="sxs-lookup"><span data-stu-id="1036e-136">Walk through the voting sample application</span></span>
<span data-ttu-id="1036e-137">Приложение для голосования состоит из двух служб:</span><span class="sxs-lookup"><span data-stu-id="1036e-137">The voting application consists of two services:</span></span>
- <span data-ttu-id="1036e-138">Служба веб-интерфейса (VotingWeb) — служба веб-интерфейса ASP.NET Core, которая обслуживает веб-страницу и предоставляет доступ к веб-API для связи с внутренней службой.</span><span class="sxs-lookup"><span data-stu-id="1036e-138">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves the web page and exposes web APIs to communicate with the backend service.</span></span>
- <span data-ttu-id="1036e-139">Внутренняя служба (VotingData) — веб-служба ASP.NET Core, которая предоставляет API для сохранения результатов голосования в надежном словаре на диске.</span><span class="sxs-lookup"><span data-stu-id="1036e-139">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API to store the vote results in a reliable dictionary persisted on disk.</span></span>

![Диаграмма приложения](./media/service-fabric-quickstart-dotnet/application-diagram.png)

<span data-ttu-id="1036e-141">Во время голосования в приложении происходят следующие события:</span><span class="sxs-lookup"><span data-stu-id="1036e-141">When you vote in the application the following events occur:</span></span>
1. <span data-ttu-id="1036e-142">JavaScript отправляет запрос о голосовании веб-API в службе веб-интерфейса в виде запроса HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="1036e-142">A JavaScript sends the vote request to the web API in the web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="1036e-143">Служба веб-интерфейса использует прокси, чтобы обнаружить и перенаправить запрос HTTP PUT внутренней службе.</span><span class="sxs-lookup"><span data-stu-id="1036e-143">The web front-end service uses a proxy to locate and forward an HTTP PUT request to the back-end service.</span></span>

3. <span data-ttu-id="1036e-144">Внутренняя служба принимает входящий запрос и сохраняет обновленный результат в надежном словаре, который реплицируется на несколько узлов в кластере и сохраняется на диске.</span><span class="sxs-lookup"><span data-stu-id="1036e-144">The back-end service takes the incoming request, and stores the updated result in a reliable dictionary, which gets replicated to multiple nodes within the cluster and persisted on disk.</span></span> <span data-ttu-id="1036e-145">Все данные приложения хранятся в кластере, поэтому база данных не требуется.</span><span class="sxs-lookup"><span data-stu-id="1036e-145">All the application's data is stored in the cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="1036e-146">Отладка в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1036e-146">Debug in Visual Studio</span></span>
<span data-ttu-id="1036e-147">При отладке приложения в Visual Studio вы используете локальный кластер разработки Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1036e-147">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="1036e-148">Вы можете настроить отладку для своего сценария.</span><span class="sxs-lookup"><span data-stu-id="1036e-148">You have the option to adjust your debugging experience to your scenario.</span></span> <span data-ttu-id="1036e-149">В этом приложении мы храним данные во внутренней службе с помощью надежного словаря.</span><span class="sxs-lookup"><span data-stu-id="1036e-149">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="1036e-150">По умолчанию при остановке отладчика Visual Studio удаляет приложение.</span><span class="sxs-lookup"><span data-stu-id="1036e-150">Visual Studio removes the application per default when you stop the debugger.</span></span> <span data-ttu-id="1036e-151">При удалении приложения данные во внутренней службе также удаляются.</span><span class="sxs-lookup"><span data-stu-id="1036e-151">Removing the application causes the data in the back-end service to also be removed.</span></span> <span data-ttu-id="1036e-152">Для сохранения данных между сеансами отладки можно изменить свойство **Режим отладки приложения** проекта **Voting** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1036e-152">To persist the data between debugging sessions, you can change the **Application Debug Mode** as a property on the **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="1036e-153">Чтобы посмотреть, как выполняется код, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1036e-153">To look at what happens in the code, complete the following steps:</span></span>
1. <span data-ttu-id="1036e-154">Откройте файл **VotesController.cs** и установите точку останова в методе **Put** веб-API (строка 47). Найти нужный файл можно с помощью поиска в обозревателе решений в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1036e-154">Open the **VotesController.cs** file and set a breakpoint in the web API's **Put** method (line 47) - You can search for the file in the Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="1036e-155">Откройте файл **VoteDataController.cs** и установите точку останова в методе **Put** этого веб-API (строка 50).</span><span class="sxs-lookup"><span data-stu-id="1036e-155">Open the **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="1036e-156">Вернитесь в браузер и выберите один из вариантов голосования или добавьте новый вариант.</span><span class="sxs-lookup"><span data-stu-id="1036e-156">Go back to the browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="1036e-157">Выполнение остановится на первой точке останова в контроллере API клиентского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1036e-157">You hit the first breakpoint in the web front-end's api controller.</span></span>
    - <span data-ttu-id="1036e-158">Здесь код JavaScript в браузере отправляет запрос контроллеру веб-API в службе веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1036e-158">This is where the JavaScript in the browser sends a request to the web API controller in the front-end service.</span></span>
    
    ![Добавление интерфейсной службы Vote](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - <span data-ttu-id="1036e-160">Сначала мы создадим URL-адрес обратного прокси-сервера внутренней службы **(1)**.</span><span class="sxs-lookup"><span data-stu-id="1036e-160">First we construct the URL to the ReverseProxy for our back-end service **(1)**.</span></span>
    - <span data-ttu-id="1036e-161">Затем мы передадим HTTP-запрос PUT к обратному прокси-серверу **(2)**.</span><span class="sxs-lookup"><span data-stu-id="1036e-161">Then we send the HTTP PUT Request to the ReverseProxy **(2)**.</span></span>
    - <span data-ttu-id="1036e-162">Наконец, мы вернем ответ внутренней службой клиенту **(3)**.</span><span class="sxs-lookup"><span data-stu-id="1036e-162">Finally the we return the response from the back-end service to the client **(3)**.</span></span>

4. <span data-ttu-id="1036e-163">Нажмите клавишу **F5**, чтобы продолжить выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="1036e-163">Press **F5** to continue</span></span>
    - <span data-ttu-id="1036e-164">Теперь вы находитесь в точке останова внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="1036e-164">You are now at the break point in the back-end service.</span></span>
    
    ![Добавление внутренней службы Vote](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - <span data-ttu-id="1036e-166">В первой строке метода **(1)** мы используем `StateManager`, чтобы получить или добавить надежный словарь `counts`.</span><span class="sxs-lookup"><span data-stu-id="1036e-166">In the first line in the method **(1)** we are using the `StateManager` to get or add a reliable dictionary called `counts`.</span></span>
    - <span data-ttu-id="1036e-167">Все взаимодействие с надежным словарем осуществляется с помощью транзакций. Для создания транзакции используется инструкция using **(2)**.</span><span class="sxs-lookup"><span data-stu-id="1036e-167">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    - <span data-ttu-id="1036e-168">В транзакции мы обновляем значение соответствующего ключа для варианта голосования и фиксируем операцию **(3)**.</span><span class="sxs-lookup"><span data-stu-id="1036e-168">In the transaction, we then update the value of the relevant key for the voting option and commits the operation **(3)**.</span></span> <span data-ttu-id="1036e-169">После возврата метода фиксации данные в словаре обновляются и реплицируются на другие узлы в кластере.</span><span class="sxs-lookup"><span data-stu-id="1036e-169">Once the commit method returns, the data is updated in the dictionary and replicated to other nodes in the cluster.</span></span> <span data-ttu-id="1036e-170">Теперь данные безопасно хранятся в кластере, и внутренняя служба может выполнять отработку отказа на другие узлы, сохраняя доступ к данным.</span><span class="sxs-lookup"><span data-stu-id="1036e-170">The data is now safely stored in the cluster, and the back-end service can fail over to other nodes, still having the data available.</span></span>
5. <span data-ttu-id="1036e-171">Нажмите клавишу **F5**, чтобы продолжить выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="1036e-171">Press **F5** to continue</span></span>

<span data-ttu-id="1036e-172">Чтобы остановить сеанс отладки, нажмите **SHIFT + F5**.</span><span class="sxs-lookup"><span data-stu-id="1036e-172">To stop the debugging session, press **Shift+F5**.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="1036e-173">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="1036e-173">Deploy the application to Azure</span></span>
<span data-ttu-id="1036e-174">Для развертывания приложения в кластере Azure можно создать собственный кластер или использовать кластер сообщества.</span><span class="sxs-lookup"><span data-stu-id="1036e-174">To deploy the application to a cluster in Azure, you can either choose to create your own cluster, or use a Party Cluster.</span></span>

<span data-ttu-id="1036e-175">Кластеры сообщества — это бесплатные кластеры Service Fabric, которые доступны в течение ограниченного времени. Эти кластеры размещены в Azure и поддерживаются командой Service Fabric. Любой пользователь может развертывать приложения на этих кластерах и знакомиться с платформой.</span><span class="sxs-lookup"><span data-stu-id="1036e-175">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by the Service Fabric team where anyone can deploy applications and learn about the platform.</span></span> <span data-ttu-id="1036e-176">Чтобы получить доступ к кластеру сообщества, следуйте инструкциям в [этом разделе](http://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="1036e-176">To get access to a Party Cluster, [follow the instructions](http://aka.ms/tryservicefabric).</span></span> 

<span data-ttu-id="1036e-177">Сведения о создании собственного кластера см. в разделе [Создание первого кластера Service Fabric в Azure](service-fabric-get-started-azure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1036e-177">For information about creating your own cluster, see [Create your first Service Fabric cluster on Azure](service-fabric-get-started-azure-cluster.md).</span></span>

> [!Note]
> <span data-ttu-id="1036e-178">Служба веб-интерфейса прослушивает порт 8080 для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="1036e-178">The web front-end service is configured to listen on port 8080 for incoming traffic.</span></span> <span data-ttu-id="1036e-179">Убедитесь, что порт открыт в кластере.</span><span class="sxs-lookup"><span data-stu-id="1036e-179">Make sure that port is open in your cluster.</span></span> <span data-ttu-id="1036e-180">При использовании кластера сообщества этот порт открыт.</span><span class="sxs-lookup"><span data-stu-id="1036e-180">If you are using the Party Cluster, this port is open.</span></span>
>

### <a name="deploy-the-application-using-visual-studio"></a><span data-ttu-id="1036e-181">Развертывание приложения с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1036e-181">Deploy the application using Visual Studio</span></span>
<span data-ttu-id="1036e-182">Теперь, когда приложение готово, можно развернуть его в кластер напрямую из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1036e-182">Now that the application is ready, you can deploy it to a cluster directly from Visual Studio.</span></span>

1. <span data-ttu-id="1036e-183">Щелкните правой кнопкой мыши **Voting** в обозревателе решений и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1036e-183">Right-click **Voting** in the Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="1036e-184">Появится диалоговое окно "Опубликовать".</span><span class="sxs-lookup"><span data-stu-id="1036e-184">The Publish dialog appears.</span></span>

    ![Диалоговое окно "Опубликовать"](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. <span data-ttu-id="1036e-186">Укажите конечную точку подключения кластера в поле **Конечная точка подключения** и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1036e-186">Type in the Connection Endpoint of the cluster in the **Connection Endpoint** field and click **Publish**.</span></span> <span data-ttu-id="1036e-187">При регистрации для доступа к кластеру сообщества конечная точка подключения отображается в браузере.</span><span class="sxs-lookup"><span data-stu-id="1036e-187">When signing up for the Party Cluster, the Connection Endpoint is provided in the browser.</span></span> <span data-ttu-id="1036e-188">Например, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span><span class="sxs-lookup"><span data-stu-id="1036e-188">- for example, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span></span>

3. <span data-ttu-id="1036e-189">Откройте браузер и введите в адрес кластера, например `http://winh1x87d1d.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1036e-189">Open a browser and type in the cluster address - for example, `http://winh1x87d1d.westus.cloudapp.azure.com`.</span></span> <span data-ttu-id="1036e-190">Вы увидите приложения, выполняющиеся в кластере Azure.</span><span class="sxs-lookup"><span data-stu-id="1036e-190">You should now see the application running in the cluster in Azure.</span></span>

![Клиентская часть приложения](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a><span data-ttu-id="1036e-192">Масштабирование приложений и служб в кластере</span><span class="sxs-lookup"><span data-stu-id="1036e-192">Scale applications and services in a cluster</span></span>
<span data-ttu-id="1036e-193">Службы Service Fabric могут легко масштабироваться в кластере с учетом изменения нагрузки на службы.</span><span class="sxs-lookup"><span data-stu-id="1036e-193">Service Fabric services can easily be scaled across a cluster to accommodate for a change in the load on the services.</span></span> <span data-ttu-id="1036e-194">Масштабирование службы осуществляется путем изменения числа экземпляров, запущенных в кластере.</span><span class="sxs-lookup"><span data-stu-id="1036e-194">You scale a service by changing the number of instances running in the cluster.</span></span> <span data-ttu-id="1036e-195">Существует несколько способов масштабирования служб — вы можете использовать сценарии PowerShell или команды интерфейса командной строки Service Fabric (sfctl).</span><span class="sxs-lookup"><span data-stu-id="1036e-195">You have multiple ways of scaling your services, you can use scripts or commands from PowerShell or Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="1036e-196">В этом примере мы используем Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="1036e-196">In this example, we are using Service Fabric Explorer.</span></span>

<span data-ttu-id="1036e-197">Service Fabric Explorer выполняется во всех кластерах Service Fabric. Чтобы его открыть, укажите адрес кластера и порт управления кластерами HTTP (19080) в адресной строке, например `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="1036e-197">Service Fabric Explorer runs in all Service Fabric clusters and can be accessed from a browser, by browsing to the clusters HTTP management port (19080), for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>

<span data-ttu-id="1036e-198">Для масштабирования службы веб-интерфейса выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1036e-198">To scale the web front-end service, do the following steps:</span></span>

1. <span data-ttu-id="1036e-199">Откройте Service Fabric Explorer в своем кластере (например, по ссылке `http://winh1x87d1d.westus.cloudapp.azure.com:19080`).</span><span class="sxs-lookup"><span data-stu-id="1036e-199">Open Service Fabric Explorer in your cluster - for example,`http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
2. <span data-ttu-id="1036e-200">Щелкните многоточие рядом с узлом **fabric:/Voting/VotingWeb** в дереве и выберите **Масштабировать службу**.</span><span class="sxs-lookup"><span data-stu-id="1036e-200">Click on the ellipsis (three dots) next to the **fabric:/Voting/VotingWeb** node in the treeview and choose **Scale Service**.</span></span>

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    <span data-ttu-id="1036e-202">Теперь вы можете изменить количество экземпляров службы веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1036e-202">You can now choose to scale the number of instances of the web front-end service.</span></span>

3. <span data-ttu-id="1036e-203">Измените количество на **2** и нажмите кнопку **Масштабировать службу**.</span><span class="sxs-lookup"><span data-stu-id="1036e-203">Change the number to **2** and click **Scale Service**.</span></span>
4. <span data-ttu-id="1036e-204">Щелкните узел **fabric:/Voting/VotingWeb** в дереве и разверните узел раздела (он отображается в виде идентификатора GUID).</span><span class="sxs-lookup"><span data-stu-id="1036e-204">Click on the **fabric:/Voting/VotingWeb** node in the tree-view and expand the partition node (represented by a GUID).</span></span>

    ![Масштабирование службы в Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    <span data-ttu-id="1036e-206">Теперь вы видите, что у службы есть два экземпляра, а с помощью дерева вы можете определить узлы, на которых запущены эти экземпляры.</span><span class="sxs-lookup"><span data-stu-id="1036e-206">You can now see that the service has two instances, and in the tree view you see which nodes the instances run on.</span></span>

<span data-ttu-id="1036e-207">С помощью этой простой задачи управления мы удвоили количество ресурсов для обработки пользовательской нагрузки для службы веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1036e-207">By this simple management task, we doubled the resources available for our front-end service to process user load.</span></span> <span data-ttu-id="1036e-208">Важно понимать, что для надежной работы службы не требуется запускать несколько экземпляров службы.</span><span class="sxs-lookup"><span data-stu-id="1036e-208">It's important to understand that you do not need multiple instances of a service to have it run reliably.</span></span> <span data-ttu-id="1036e-209">При сбое в работе службы Service Fabric запускает новый экземпляр службы в кластере.</span><span class="sxs-lookup"><span data-stu-id="1036e-209">If a service fails, Service Fabric makes sure a new service instance runs in the cluster.</span></span>

## <a name="perform-a-rolling-application-upgrade"></a><span data-ttu-id="1036e-210">Последовательное обновление приложения</span><span class="sxs-lookup"><span data-stu-id="1036e-210">Perform a rolling application upgrade</span></span>
<span data-ttu-id="1036e-211">Service Fabric развертывает обновления для приложения безопасным способом.</span><span class="sxs-lookup"><span data-stu-id="1036e-211">When deploying new updates to your application, Service Fabric rolls out the update in a safe way.</span></span> <span data-ttu-id="1036e-212">Последовательные обновления позволяют избежать простоя, а также автоматического отката в случае возникновения ошибок.</span><span class="sxs-lookup"><span data-stu-id="1036e-212">Rolling upgrades gives you no downtime while upgrading as well as automated rollback should errors occur.</span></span>

<span data-ttu-id="1036e-213">Для обновления приложения выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1036e-213">To upgrade the application, do the following:</span></span>

1. <span data-ttu-id="1036e-214">Откройте файл **Index.cshtml** в Visual Studio. Найти файл можно в обозревателе решений в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1036e-214">Open the **Index.cshtml** file in Visual Studio - You can search for the file in the Solution Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="1036e-215">Измените заголовок страницы, например, добавив какой-нибудь текст.</span><span class="sxs-lookup"><span data-stu-id="1036e-215">Change the heading on the page by adding some text - for example.</span></span>
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. <span data-ttu-id="1036e-216">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="1036e-216">Save the file.</span></span>
4. <span data-ttu-id="1036e-217">Щелкните правой кнопкой мыши **Voting** в обозревателе решений и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1036e-217">Right-click **Voting** in the Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="1036e-218">Появится диалоговое окно "Опубликовать".</span><span class="sxs-lookup"><span data-stu-id="1036e-218">The Publish dialog appears.</span></span>
5. <span data-ttu-id="1036e-219">Нажмите кнопку **Версия манифеста**, чтобы изменить версию службы и приложения.</span><span class="sxs-lookup"><span data-stu-id="1036e-219">Click the **Manifest Version** button to change the version of the service and application.</span></span>
6. <span data-ttu-id="1036e-220">Например, измените версию элемента **Code** в разделе **VotingWebPkg** на "2.0.0" и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1036e-220">Change the version of the **Code** element under **VotingWebPkg** to "2.0.0", for example, and click **Save**.</span></span>

    ![Диалоговое окно изменения версии](./media/service-fabric-quickstart-dotnet/change-version.png)
7. <span data-ttu-id="1036e-222">В диалоговом окне **Публикация приложения Service Fabric** установите флажок "Обновить приложение" и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1036e-222">In the **Publish Service Fabric Application** dialog, check the Upgrade the Application checkbox, and click **Publish**.</span></span>

    ![Параметр "Обновить приложение" в диалоговом окне публикации](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. <span data-ttu-id="1036e-224">Откройте в браузере адрес кластера, добавив порт 19080 — например, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="1036e-224">Open your browser and browse to the cluster address on port 19080 - for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
9. <span data-ttu-id="1036e-225">Щелкните узел **Приложения** в дереве, а затем щелкните **Выполняемые обновления** в области справа.</span><span class="sxs-lookup"><span data-stu-id="1036e-225">Click on the **Applications** node in the tree view, and then **Upgrades in Progress** in the right-hand pane.</span></span> <span data-ttu-id="1036e-226">Вы увидите, как обновление проходит по доменам обновления в кластере, проверяя работоспособность каждого домена перед переходом к следующему.</span><span class="sxs-lookup"><span data-stu-id="1036e-226">You see how the upgrade rolls through the upgrade domains in your cluster, making sure each domain is healthy before proceeding to the next.</span></span>
    <span data-ttu-id="1036e-227">![Представление обновления в Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span><span class="sxs-lookup"><span data-stu-id="1036e-227">![Upgrade View in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span></span>

    <span data-ttu-id="1036e-228">Service Fabric выполняет надежное обновление. Для этого после обновления службы на каждом узле кластера выполняется ожидание в течение двух минут, и затем Service Fabric переходит к следующему узлу кластера.</span><span class="sxs-lookup"><span data-stu-id="1036e-228">Service Fabric makes upgrades safe by waiting two minutes after upgrading the service on each node in the cluster.</span></span> <span data-ttu-id="1036e-229">Все обновление должно занять около 8 минут.</span><span class="sxs-lookup"><span data-stu-id="1036e-229">Expect the entire update to take approximately eight minutes.</span></span>

10. <span data-ttu-id="1036e-230">Во время обновления вы можете использовать приложение.</span><span class="sxs-lookup"><span data-stu-id="1036e-230">While the upgrade is running, you can still use the application.</span></span> <span data-ttu-id="1036e-231">Из-за наличия двух экземпляров службы, запущенных в кластере, некоторые из ваших запросов могут получить обновленную версию приложения, а другие — старую версию.</span><span class="sxs-lookup"><span data-stu-id="1036e-231">Because you have two instances of the service running in the cluster, some of your requests may get an upgraded version of the application, while others may still get the old version.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1036e-232">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1036e-232">Next steps</span></span>
<span data-ttu-id="1036e-233">Из этого руководства вы узнали, как выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1036e-233">In this quickstart, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1036e-234">Создание приложения с использованием .NET и Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1036e-234">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="1036e-235">Использование ASP.NET Core в качестве клиентского веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="1036e-235">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="1036e-236">Хранение данных приложения в службе с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="1036e-236">Store application data in a stateful service</span></span>
> * <span data-ttu-id="1036e-237">Локальная отладка приложения</span><span class="sxs-lookup"><span data-stu-id="1036e-237">Debug your application locally</span></span>
> * <span data-ttu-id="1036e-238">Развертывание приложения в кластере Azure</span><span class="sxs-lookup"><span data-stu-id="1036e-238">Deploy the application to a cluster in Azure</span></span>
> * <span data-ttu-id="1036e-239">Масштабирование приложения на несколько узлов</span><span class="sxs-lookup"><span data-stu-id="1036e-239">Scale-out the application across multiple nodes</span></span>
> * <span data-ttu-id="1036e-240">Последовательное обновление приложения</span><span class="sxs-lookup"><span data-stu-id="1036e-240">Perform a rolling application upgrade</span></span>

<span data-ttu-id="1036e-241">Дополнительные сведения о Service Fabric и .NET см. в следующем руководстве:</span><span class="sxs-lookup"><span data-stu-id="1036e-241">To learn more about Service Fabric and .NET, take a look at this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1036e-242">Приложение .NET в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1036e-242">.NET application on Service Fabric</span></span>](service-fabric-tutorial-create-dotnet-app.md)