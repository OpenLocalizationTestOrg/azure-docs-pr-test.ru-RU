---
title: "aaaCreate приложения .NET Service Fabric в Azure | Документы Microsoft"
description: "Создание приложения .NET для Azure с помощью быстрого запуска образца hello Service Fabric."
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
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a><span data-ttu-id="e39c1-103">Создание приложения .NET Service Fabric в Azure</span><span class="sxs-lookup"><span data-stu-id="e39c1-103">Create a .NET Service Fabric application in Azure</span></span>
<span data-ttu-id="e39c1-104">Azure Service Fabric — это платформа распределенных систем для развертывания масштабируемых надежных микрослужб и контейнеров и управления ими.</span><span class="sxs-lookup"><span data-stu-id="e39c1-104">Azure Service Fabric is a distributed systems platform for deploying and managing scalable and reliable microservices and containers.</span></span> 

<span data-ttu-id="e39c1-105">Краткого руководства показано, как toodeploy вашего первого tooService приложения .NET структуры.</span><span class="sxs-lookup"><span data-stu-id="e39c1-105">This quickstart shows how toodeploy your first .NET application tooService Fabric.</span></span> <span data-ttu-id="e39c1-106">После завершения имеется голосования приложение с ASP.NET Core веб-интерфейса, который сохраняет результаты голосования в с отслеживанием состояния внутренней службы в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span>

![Снимок экрана приложения](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

<span data-ttu-id="e39c1-108">С помощью этого приложения вы узнаете, как выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e39c1-108">Using this application you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e39c1-109">Создание приложения с использованием .NET и Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e39c1-109">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="e39c1-110">Использование ASP.NET Core в качестве клиентского веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39c1-110">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="e39c1-111">Хранение данных приложения в службе с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="e39c1-111">Store application data in a stateful service</span></span>
> * <span data-ttu-id="e39c1-112">Локальная отладка приложения</span><span class="sxs-lookup"><span data-stu-id="e39c1-112">Debug your application locally</span></span>
> * <span data-ttu-id="e39c1-113">Развертывание кластера tooa приложения hello в Azure</span><span class="sxs-lookup"><span data-stu-id="e39c1-113">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="e39c1-114">Hello масштабирования приложения на нескольких узлах</span><span class="sxs-lookup"><span data-stu-id="e39c1-114">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="e39c1-115">Последовательное обновление приложения</span><span class="sxs-lookup"><span data-stu-id="e39c1-115">Perform a rolling application upgrade</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e39c1-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e39c1-116">Prerequisites</span></span>
<span data-ttu-id="e39c1-117">toocomplete краткого руководства:</span><span class="sxs-lookup"><span data-stu-id="e39c1-117">toocomplete this quickstart:</span></span>
1. <span data-ttu-id="e39c1-118">[Установка Visual Studio 2017 г](https://www.visualstudio.com/) с hello **разработки Azure** и **ASP.NET и веб-разработки** рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="e39c1-118">[Install Visual Studio 2017](https://www.visualstudio.com/) with hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
2. <span data-ttu-id="e39c1-119">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="e39c1-119">[Install Git](https://git-scm.com/)</span></span>
3. [<span data-ttu-id="e39c1-120">Установить пакет Microsoft Azure Service Fabric SDK hello</span><span class="sxs-lookup"><span data-stu-id="e39c1-120">Install hello Microsoft Azure Service Fabric SDK</span></span>](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. <span data-ttu-id="e39c1-121">Выполните следующие команды tooenable Visual Studio toodeploy toohello локального кластера Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-121">Run hello following command tooenable Visual Studio toodeploy toohello local Service Fabric cluster:</span></span>
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a><span data-ttu-id="e39c1-122">Загрузить образец hello</span><span class="sxs-lookup"><span data-stu-id="e39c1-122">Download hello sample</span></span>
<span data-ttu-id="e39c1-123">В окне командной строки запустите hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="e39c1-123">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="e39c1-124">Запустите приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="e39c1-124">Run hello application locally</span></span>
<span data-ttu-id="e39c1-125">Щелкните правой кнопкой мыши значок hello Visual Studio в меню "Пуск" hello и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-125">Right-click hello Visual Studio icon in hello Start Menu and choose **Run as administrator**.</span></span> <span data-ttu-id="e39c1-126">В порядке tooattach hello отладчик tooyour служб необходимо toorun Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="e39c1-126">In order tooattach hello debugger tooyour services, you need toorun Visual Studio as administrator.</span></span>

<span data-ttu-id="e39c1-127">Откройте hello **Voting.sln** решения Visual Studio из репозитория hello, можно клонировать.</span><span class="sxs-lookup"><span data-stu-id="e39c1-127">Open hello **Voting.sln** Visual Studio solution from hello repository you cloned.</span></span>

<span data-ttu-id="e39c1-128">приложение hello toodeploy, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-128">toodeploy hello application, press **F5**.</span></span>

> [!NOTE]
> <span data-ttu-id="e39c1-129">Hello в первый раз, запуска и развертывания приложения hello, Visual Studio создает локального кластера для отладки.</span><span class="sxs-lookup"><span data-stu-id="e39c1-129">hello first time you run and deploy hello application, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="e39c1-130">Эта операция может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="e39c1-130">This operation may take some time.</span></span> <span data-ttu-id="e39c1-131">Состояние создания кластера Hello отображается в окне вывода Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-131">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="e39c1-132">После завершения развертывания hello запускает браузер и открыть эту страницу: `http://localhost:8080` -hello клиентского веб-интерфейса приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-132">When hello deployment is complete, launch a browser and open this page: `http://localhost:8080` - hello web front-end of hello application.</span></span>

![Клиентская часть приложения](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

<span data-ttu-id="e39c1-134">Теперь можно добавить варианты для выбора в голосовании и начать прием голосов.</span><span class="sxs-lookup"><span data-stu-id="e39c1-134">You can now add a set of voting options, and start taking votes.</span></span> <span data-ttu-id="e39c1-135">Здравствуйте, приложение будет работать и сохраняет все данные кластера Service Fabric, без необходимости hello отдельную базу данных.</span><span class="sxs-lookup"><span data-stu-id="e39c1-135">hello application runs and stores all data in your Service Fabric cluster, without hello need for a separate database.</span></span>

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="e39c1-136">Перемещайтесь голосования пример приложения hello</span><span class="sxs-lookup"><span data-stu-id="e39c1-136">Walk through hello voting sample application</span></span>
<span data-ttu-id="e39c1-137">Hello голосования приложения состоит из двух служб.</span><span class="sxs-lookup"><span data-stu-id="e39c1-137">hello voting application consists of two services:</span></span>
- <span data-ttu-id="e39c1-138">Веб-интерфейса службы (VotingWeb) — ASP.NET Core веб-интерфейса службы, который будет служить hello веб-страницы и предоставляет доступ к веб-API-интерфейсы toocommunicate с серверной службы hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-138">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="e39c1-139">Внутренняя служба (VotingData)-ASP.NET Core веб-служба предоставляет один голос hello toostore API приводит к надежным словарь сохраняются на диске.</span><span class="sxs-lookup"><span data-stu-id="e39c1-139">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Диаграмма приложения](./media/service-fabric-quickstart-dotnet/application-diagram.png)

<span data-ttu-id="e39c1-141">Когда голосовать в следующие hello приложения hello происходят события.</span><span class="sxs-lookup"><span data-stu-id="e39c1-141">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="e39c1-142">JavaScript отправляет toohello веб-запроса API hello голос hello веб-интерфейса службы как запрос HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="e39c1-142">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="e39c1-143">Hello клиентского веб-интерфейса службы использует toolocate прокси-сервера и пересылать запрос HTTP PUT toohello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="e39c1-143">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="e39c1-144">Hello внутренняя служба принимает входящий запрос hello и хранилищ hello обновил результат в надежные словаря, который получает реплицированные toomultiple узлами в кластере hello и сохраняются на диске.</span><span class="sxs-lookup"><span data-stu-id="e39c1-144">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="e39c1-145">Все приложения hello данные хранятся в кластере hello, поэтому не требуется ни одной базы данных.</span><span class="sxs-lookup"><span data-stu-id="e39c1-145">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="e39c1-146">Отладка в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e39c1-146">Debug in Visual Studio</span></span>
<span data-ttu-id="e39c1-147">При отладке приложения в Visual Studio вы используете локальный кластер разработки Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e39c1-147">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="e39c1-148">У вас есть параметр tooadjust hello отладки сценария tooyour качества.</span><span class="sxs-lookup"><span data-stu-id="e39c1-148">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="e39c1-149">В этом приложении мы храним данные во внутренней службе с помощью надежного словаря.</span><span class="sxs-lookup"><span data-stu-id="e39c1-149">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="e39c1-150">Visual Studio удаляет приложение hello по умолчанию, при остановке отладчика hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-150">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="e39c1-151">Удаление приложения hello вызывает hello данных в серверной части hello tooalso службы удаляется.</span><span class="sxs-lookup"><span data-stu-id="e39c1-151">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="e39c1-152">toopersist hello данных между сеансами отладки, можно изменить hello **режим отладки приложения** как свойство hello **Голосование** проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e39c1-152">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="e39c1-153">toolook, что происходит в коде hello завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="e39c1-153">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="e39c1-154">Откройте hello **VotesController.cs** файла и задать точку останова в hello веб-API **поместить** метод (строка 47 -), можно выполнить поиск файла hello в hello обозревателя решений в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e39c1-154">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="e39c1-155">Откройте hello **VoteDataController.cs** файл и установите точку останова в этом веб-API **поместить** метод (строка 50).</span><span class="sxs-lookup"><span data-stu-id="e39c1-155">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="e39c1-156">Вернитесь к предыдущему окну toohello браузера и нажмите кнопку голосования параметр или добавить новую голосования.</span><span class="sxs-lookup"><span data-stu-id="e39c1-156">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="e39c1-157">Попадании hello первой точки останова в hello веб-интерфейса контроллер api.</span><span class="sxs-lookup"><span data-stu-id="e39c1-157">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    - <span data-ttu-id="e39c1-158">Это где hello JavaScript в браузере hello отправляет контроллер запроса toohello web API в клиентской службы hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-158">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Добавление интерфейсной службы Vote](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - <span data-ttu-id="e39c1-160">Сначала мы создаем URL-адрес hello toohello ReverseProxy для наших служб **(1)**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-160">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    - <span data-ttu-id="e39c1-161">Затем мы отправляем hello запроса HTTP PUT toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-161">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    - <span data-ttu-id="e39c1-162">Наконец hello мы возвращаем hello ответа от клиента toohello внутренней службе hello **(3)**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-162">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="e39c1-163">Нажмите клавишу **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="e39c1-163">Press **F5** toocontinue</span></span>
    - <span data-ttu-id="e39c1-164">Теперь вы находитесь в точке останова hello в hello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="e39c1-164">You are now at hello break point in hello back-end service.</span></span>
    
    ![Добавление внутренней службы Vote](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - <span data-ttu-id="e39c1-166">В первую строку hello в методе hello **(1)** мы используем hello `StateManager` tooget или добавление надежного словаря, который называется `counts`.</span><span class="sxs-lookup"><span data-stu-id="e39c1-166">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    - <span data-ttu-id="e39c1-167">Все взаимодействие с надежным словарем осуществляется с помощью транзакций. Для создания транзакции используется инструкция using **(2)**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-167">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    - <span data-ttu-id="e39c1-168">В транзакции hello, мы затем измените значение hello hello соответствующего ключа для голосования параметр hello и фиксации hello операции **(3)**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-168">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="e39c1-169">После фиксации hello методом hello данных обновляется в словаре hello и реплицируются tooother узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-169">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="e39c1-170">Hello данные теперь безопасно хранятся в кластере hello и hello внутренней службы при сбое tooother узлов, по-прежнему возникают hello данные недоступны.</span><span class="sxs-lookup"><span data-stu-id="e39c1-170">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="e39c1-171">Нажмите клавишу **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="e39c1-171">Press **F5** toocontinue</span></span>

<span data-ttu-id="e39c1-172">hello toostop сеанса, нажмите клавишу отладки **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-172">toostop hello debugging session, press **Shift+F5**.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="e39c1-173">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="e39c1-173">Deploy hello application tooAzure</span></span>
<span data-ttu-id="e39c1-174">toodeploy hello кластера tooa приложения в Azure, можно выбрать toocreate собственные кластера или использования кластера стороной.</span><span class="sxs-lookup"><span data-stu-id="e39c1-174">toodeploy hello application tooa cluster in Azure, you can either choose toocreate your own cluster, or use a Party Cluster.</span></span>

<span data-ttu-id="e39c1-175">Кластеры, стороннего производителя, бесплатные, ограничено по времени кластеров Service Fabric размещаются в Azure и выполняются командой Service Fabric hello, где любой пользователь может развертывать приложения и Дополнительные сведения о платформе hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-175">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="e39c1-176">tooa доступа tooget кластера стороны [следуйте инструкциям hello](http://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="e39c1-176">tooget access tooa Party Cluster, [follow hello instructions](http://aka.ms/tryservicefabric).</span></span> 

<span data-ttu-id="e39c1-177">Сведения о создании собственного кластера см. в разделе [Создание первого кластера Service Fabric в Azure](service-fabric-get-started-azure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e39c1-177">For information about creating your own cluster, see [Create your first Service Fabric cluster on Azure](service-fabric-get-started-azure-cluster.md).</span></span>

> [!Note]
> <span data-ttu-id="e39c1-178">Hello веб-интерфейса службы является настроенным toolisten через порт 8080 для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="e39c1-178">hello web front-end service is configured toolisten on port 8080 for incoming traffic.</span></span> <span data-ttu-id="e39c1-179">Убедитесь, что порт открыт в кластере.</span><span class="sxs-lookup"><span data-stu-id="e39c1-179">Make sure that port is open in your cluster.</span></span> <span data-ttu-id="e39c1-180">При использовании кластера стороны hello этот порт открыт.</span><span class="sxs-lookup"><span data-stu-id="e39c1-180">If you are using hello Party Cluster, this port is open.</span></span>
>

### <a name="deploy-hello-application-using-visual-studio"></a><span data-ttu-id="e39c1-181">Развертывание приложения hello, с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e39c1-181">Deploy hello application using Visual Studio</span></span>
<span data-ttu-id="e39c1-182">Теперь, когда приложение hello готов, его можно развернуть кластер tooa непосредственно из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e39c1-182">Now that hello application is ready, you can deploy it tooa cluster directly from Visual Studio.</span></span>

1. <span data-ttu-id="e39c1-183">Щелкните правой кнопкой мыши **Голосование** в hello в обозревателе решений и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-183">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="e39c1-184">Откроется диалоговое окно публикации Hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-184">hello Publish dialog appears.</span></span>

    ![Диалоговое окно "Опубликовать"](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. <span data-ttu-id="e39c1-186">Тип в hello конечной точки подключения кластера hello в hello **конечной точки подключения** поле и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-186">Type in hello Connection Endpoint of hello cluster in hello **Connection Endpoint** field and click **Publish**.</span></span> <span data-ttu-id="e39c1-187">При регистрации для hello стороны кластера, в браузере hello предоставляется hello конечной точки подключения.</span><span class="sxs-lookup"><span data-stu-id="e39c1-187">When signing up for hello Party Cluster, hello Connection Endpoint is provided in hello browser.</span></span> <span data-ttu-id="e39c1-188">Например, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span><span class="sxs-lookup"><span data-stu-id="e39c1-188">- for example, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span></span>

3. <span data-ttu-id="e39c1-189">Например, откройте браузер и введите в адрес кластера hello - `http://winh1x87d1d.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="e39c1-189">Open a browser and type in hello cluster address - for example, `http://winh1x87d1d.westus.cloudapp.azure.com`.</span></span> <span data-ttu-id="e39c1-190">Теперь вы увидите приложения hello, запущенного в кластере hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="e39c1-190">You should now see hello application running in hello cluster in Azure.</span></span>

![Клиентская часть приложения](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a><span data-ttu-id="e39c1-192">Масштабирование приложений и служб в кластере</span><span class="sxs-lookup"><span data-stu-id="e39c1-192">Scale applications and services in a cluster</span></span>
<span data-ttu-id="e39c1-193">Служб Service Fabric, можно легко масштабировать на tooaccommodate кластера при изменении нагрузки hello в службах hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-193">Service Fabric services can easily be scaled across a cluster tooaccommodate for a change in hello load on hello services.</span></span> <span data-ttu-id="e39c1-194">Масштабирование службы, изменив hello количество экземпляров, работающих в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-194">You scale a service by changing hello number of instances running in hello cluster.</span></span> <span data-ttu-id="e39c1-195">Существует несколько способов масштабирования служб — вы можете использовать сценарии PowerShell или команды интерфейса командной строки Service Fabric (sfctl).</span><span class="sxs-lookup"><span data-stu-id="e39c1-195">You have multiple ways of scaling your services, you can use scripts or commands from PowerShell or Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="e39c1-196">В этом примере мы используем Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="e39c1-196">In this example, we are using Service Fabric Explorer.</span></span>

<span data-ttu-id="e39c1-197">Обозреватель Service Fabric выполняется во всех кластерах службы структуры и может осуществляться из браузера, просматривая порт управления кластерами HTTP toohello (19080), например, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="e39c1-197">Service Fabric Explorer runs in all Service Fabric clusters and can be accessed from a browser, by browsing toohello clusters HTTP management port (19080), for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>

<span data-ttu-id="e39c1-198">tooscale hello веб-службы интерфейса, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e39c1-198">tooscale hello web front-end service, do hello following steps:</span></span>

1. <span data-ttu-id="e39c1-199">Откройте Service Fabric Explorer в своем кластере (например, по ссылке `http://winh1x87d1d.westus.cloudapp.azure.com:19080`).</span><span class="sxs-lookup"><span data-stu-id="e39c1-199">Open Service Fabric Explorer in your cluster - for example,`http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
2. <span data-ttu-id="e39c1-200">Щелкните Далее toohello hello многоточие (три точки) **fabric: / голосование/VotingWeb** узел в hello treeview и выберите **служба масштабирования**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-200">Click on hello ellipsis (three dots) next toohello **fabric:/Voting/VotingWeb** node in hello treeview and choose **Scale Service**.</span></span>

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    <span data-ttu-id="e39c1-202">Теперь можно выбрать tooscale hello число экземпляров hello веб-интерфейса службы.</span><span class="sxs-lookup"><span data-stu-id="e39c1-202">You can now choose tooscale hello number of instances of hello web front-end service.</span></span>

3. <span data-ttu-id="e39c1-203">Изменить номер hello слишком**2** и нажмите кнопку **служба масштабирования**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-203">Change hello number too**2** and click **Scale Service**.</span></span>
4. <span data-ttu-id="e39c1-204">Щелкните hello **fabric: / голосование/VotingWeb** узла в дерево hello и разверните узел раздела hello (представленные кодами GUID).</span><span class="sxs-lookup"><span data-stu-id="e39c1-204">Click on hello **fabric:/Voting/VotingWeb** node in hello tree-view and expand hello partition node (represented by a GUID).</span></span>

    ![Масштабирование службы в Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    <span data-ttu-id="e39c1-206">Теперь вы увидите hello служба имеет два экземпляра, что в представлении дерева hello можно узнать, какие узлы, проведение hello экземпляров.</span><span class="sxs-lookup"><span data-stu-id="e39c1-206">You can now see that hello service has two instances, and in hello tree view you see which nodes hello instances run on.</span></span>

<span data-ttu-id="e39c1-207">Эта задача простое управление мы вдвое hello ресурсы, доступные для нашей службы интерфейса tooprocess пользовательской нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e39c1-207">By this simple management task, we doubled hello resources available for our front-end service tooprocess user load.</span></span> <span data-ttu-id="e39c1-208">Это важные toounderstand, не требуется несколько экземпляров службы toohave, он работает надежно.</span><span class="sxs-lookup"><span data-stu-id="e39c1-208">It's important toounderstand that you do not need multiple instances of a service toohave it run reliably.</span></span> <span data-ttu-id="e39c1-209">При сбое в работе службы Service Fabric гарантирует, что новый экземпляр службы работает в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-209">If a service fails, Service Fabric makes sure a new service instance runs in hello cluster.</span></span>

## <a name="perform-a-rolling-application-upgrade"></a><span data-ttu-id="e39c1-210">Последовательное обновление приложения</span><span class="sxs-lookup"><span data-stu-id="e39c1-210">Perform a rolling application upgrade</span></span>
<span data-ttu-id="e39c1-211">При развертывании новых обновлений tooyour приложения Service Fabric развертывает обновления hello безопасным способом.</span><span class="sxs-lookup"><span data-stu-id="e39c1-211">When deploying new updates tooyour application, Service Fabric rolls out hello update in a safe way.</span></span> <span data-ttu-id="e39c1-212">Последовательные обновления позволяют избежать простоя, а также автоматического отката в случае возникновения ошибок.</span><span class="sxs-lookup"><span data-stu-id="e39c1-212">Rolling upgrades gives you no downtime while upgrading as well as automated rollback should errors occur.</span></span>

<span data-ttu-id="e39c1-213">tooupgrade Здравствуйте, приложения, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e39c1-213">tooupgrade hello application, do hello following:</span></span>

1. <span data-ttu-id="e39c1-214">Откройте hello **Index.cshtml** файл в Visual Studio — можно выполнить поиск файла hello в hello обозревателя решений в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e39c1-214">Open hello **Index.cshtml** file in Visual Studio - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="e39c1-215">Изменить заголовок hello на странице приветствия, добавив текст - пример.</span><span class="sxs-lookup"><span data-stu-id="e39c1-215">Change hello heading on hello page by adding some text - for example.</span></span>
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. <span data-ttu-id="e39c1-216">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-216">Save hello file.</span></span>
4. <span data-ttu-id="e39c1-217">Щелкните правой кнопкой мыши **Голосование** в hello в обозревателе решений и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-217">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="e39c1-218">Откроется диалоговое окно публикации Hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-218">hello Publish dialog appears.</span></span>
5. <span data-ttu-id="e39c1-219">Нажмите кнопку hello **версии манифеста** кнопку версии hello toochange hello службы и приложения.</span><span class="sxs-lookup"><span data-stu-id="e39c1-219">Click hello **Manifest Version** button toochange hello version of hello service and application.</span></span>
6. <span data-ttu-id="e39c1-220">Изменение версии hello hello **кода** элемента под **VotingWebPkg** слишком «2.0.0», например, и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-220">Change hello version of hello **Code** element under **VotingWebPkg** too"2.0.0", for example, and click **Save**.</span></span>

    ![Диалоговое окно изменения версии](./media/service-fabric-quickstart-dotnet/change-version.png)
7. <span data-ttu-id="e39c1-222">В hello **опубликовать приложение Service Fabric** окна, проверка hello обновления hello приложения флажок и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="e39c1-222">In hello **Publish Service Fabric Application** dialog, check hello Upgrade hello Application checkbox, and click **Publish**.</span></span>

    ![Параметр "Обновить приложение" в диалоговом окне публикации](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. <span data-ttu-id="e39c1-224">Откройте браузер и перейдите toohello адрес кластера для порта 19080 - например, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="e39c1-224">Open your browser and browse toohello cluster address on port 19080 - for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
9. <span data-ttu-id="e39c1-225">Щелкните hello **приложений** узел в дереве hello, а затем **обновления выполняется** hello правой панели.</span><span class="sxs-lookup"><span data-stu-id="e39c1-225">Click on hello **Applications** node in hello tree view, and then **Upgrades in Progress** in hello right-hand pane.</span></span> <span data-ttu-id="e39c1-226">Вы увидите сводный hello обновления через hello доменов обновления в кластере, убедившись, что каждый домен находится в работоспособном состоянии перед продолжением toohello Далее.</span><span class="sxs-lookup"><span data-stu-id="e39c1-226">You see how hello upgrade rolls through hello upgrade domains in your cluster, making sure each domain is healthy before proceeding toohello next.</span></span>
    <span data-ttu-id="e39c1-227">![Представление обновления в Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span><span class="sxs-lookup"><span data-stu-id="e39c1-227">![Upgrade View in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span></span>

    <span data-ttu-id="e39c1-228">Service Fabric делает безопасном обновлений, ожидающих двух минут после обновления службы hello на каждом узле в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-228">Service Fabric makes upgrades safe by waiting two minutes after upgrading hello service on each node in hello cluster.</span></span> <span data-ttu-id="e39c1-229">Ожидается, что tootake всего обновления hello около 8 минут.</span><span class="sxs-lookup"><span data-stu-id="e39c1-229">Expect hello entire update tootake approximately eight minutes.</span></span>

10. <span data-ttu-id="e39c1-230">Пока выполняется обновление hello, по-прежнему можно использовать приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e39c1-230">While hello upgrade is running, you can still use hello application.</span></span> <span data-ttu-id="e39c1-231">Из-за наличия двух экземпляров службы hello, работающих в кластере hello некоторые из ваших запросов может возникнуть обновленной версии приложения hello пока другим пользователям все равно может получить hello старую версию.</span><span class="sxs-lookup"><span data-stu-id="e39c1-231">Because you have two instances of hello service running in hello cluster, some of your requests may get an upgraded version of hello application, while others may still get hello old version.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e39c1-232">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e39c1-232">Next steps</span></span>
<span data-ttu-id="e39c1-233">Из этого руководства вы узнали, как выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e39c1-233">In this quickstart, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e39c1-234">Создание приложения с использованием .NET и Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e39c1-234">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="e39c1-235">Использование ASP.NET Core в качестве клиентского веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39c1-235">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="e39c1-236">Хранение данных приложения в службе с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="e39c1-236">Store application data in a stateful service</span></span>
> * <span data-ttu-id="e39c1-237">Локальная отладка приложения</span><span class="sxs-lookup"><span data-stu-id="e39c1-237">Debug your application locally</span></span>
> * <span data-ttu-id="e39c1-238">Развертывание кластера tooa приложения hello в Azure</span><span class="sxs-lookup"><span data-stu-id="e39c1-238">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="e39c1-239">Hello масштабирования приложения на нескольких узлах</span><span class="sxs-lookup"><span data-stu-id="e39c1-239">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="e39c1-240">Последовательное обновление приложения</span><span class="sxs-lookup"><span data-stu-id="e39c1-240">Perform a rolling application upgrade</span></span>

<span data-ttu-id="e39c1-241">toolearn Дополнительные сведения о Service Fabric и .NET, ознакомьтесь с учебником:</span><span class="sxs-lookup"><span data-stu-id="e39c1-241">toolearn more about Service Fabric and .NET, take a look at this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e39c1-242">Приложение .NET в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e39c1-242">.NET application on Service Fabric</span></span>](service-fabric-tutorial-create-dotnet-app.md)