---
title: "aaaLogging для веб-службы машинного обучения | Документы Microsoft"
description: "Узнайте, как tooenable ведения журнала для машинного обучения веб-службы. Ведение журнала предоставляет дополнительные сведения, toohelp Устранение hello API-интерфейсы."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="484af-104">Включение функции ведения журналов для веб-служб машинного обучения</span><span class="sxs-lookup"><span data-stu-id="484af-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="484af-105">Этот документ содержит сведения о hello, ведение журнала возможности веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="484af-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="484af-106">Ведение журнала предоставляет дополнительные сведения, помимо номеру ошибки и сообщения, могут помочь устранить вашей toohello вызовы API-интерфейсы машины обучения.</span><span class="sxs-lookup"><span data-stu-id="484af-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="484af-107">Как tooenable ведения журнала для веб-службы</span><span class="sxs-lookup"><span data-stu-id="484af-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="484af-108">Включение ведения журнала hello [веб-службы Azure Machine Learning](https://services.azureml.net) портала.</span><span class="sxs-lookup"><span data-stu-id="484af-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="484af-109">Войдите в портал веб-службы Azure Machine Learning toohello на [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="484af-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="484af-110">Классический веб-службы, можно также получить toohello портала, щелкнув **новый веб-интерфейс служб** на странице веб-службы обучения машины hello в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="484af-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Ссылка New Web Services Experience (Новый интерфейс веб-служб)](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="484af-112">Hello верхнем меню щелкните **веб-службы** для нового веб-службы, или нажмите кнопку **классического веб-служб** для классического веб-службы.</span><span class="sxs-lookup"><span data-stu-id="484af-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Выбор новых или классических веб-служб](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="484af-114">Для нового веб-службы щелкните имя веб-службы hello.</span><span class="sxs-lookup"><span data-stu-id="484af-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="484af-115">Классического веб-службы щелкните имя веб-службы hello, а затем на следующую страницу приветствия щелкните hello соответствующей конечной точке.</span><span class="sxs-lookup"><span data-stu-id="484af-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="484af-116">Hello верхнем меню щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="484af-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="484af-117">Набор hello **включить ведение журнала** параметр слишком*ошибка* (toolog только ошибки) или *все* (для полное протоколирование).</span><span class="sxs-lookup"><span data-stu-id="484af-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![Выбор уровня ведения журнала](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="484af-119">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="484af-119">Click **Save**.</span></span>

7. <span data-ttu-id="484af-120">Классический веб-службы, создайте hello **ml диагностики** контейнера.</span><span class="sxs-lookup"><span data-stu-id="484af-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="484af-121">Все веб-службы журналов хранятся в контейнер больших двоичных объектов с именем **ml диагностики** в учетной записи хранения hello, связанные с hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="484af-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="484af-122">Новый веб-службы этот контейнер создается hello первом обращении к веб-службе hello.</span><span class="sxs-lookup"><span data-stu-id="484af-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="484af-123">Классического веб-службы нужны toocreate hello контейнера, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="484af-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="484af-124">В hello [портал Azure](https://portal.azure.com)перейдите учетной записи хранилища toohello, связанные с hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="484af-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="484af-125">В колонке **Служба BLOB-объектов** щелкните **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="484af-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="484af-126">Если контейнер hello **ml диагностики** не существует, нажмите кнопку **+ контейнер**, добавьте hello контейнера hello имя «ml диагностики» и выберите hello **тип доступа** как «Большой двоичный объект».</span><span class="sxs-lookup"><span data-stu-id="484af-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="484af-127">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="484af-127">Click **OK**.</span></span>

      ![Выбор уровня ведения журнала](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="484af-129">Классический веб-службы hello панель мониторинга Web Services в студии машинного обучения также имеет tooenable коммутатора ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="484af-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="484af-130">Тем не менее поскольку ведение журнала теперь можно управлять через портал hello веб-службы, вам потребуется tooenable входа через портал hello, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="484af-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="484af-131">Если вы уже включили ведение журнала в Studio, в hello службы веб-портал, необходимо отключить ведение журнала и снова включите ее.</span><span class="sxs-lookup"><span data-stu-id="484af-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="484af-132">Включение ведения журнала последствия Hello</span><span class="sxs-lookup"><span data-stu-id="484af-132">hello effects of enabling logging</span></span>
<span data-ttu-id="484af-133">Если включено ведение журнала, диагностики hello и ошибки из hello конечной веб-службы записываются в hello **ml диагностики** контейнер больших двоичных объектов в учетной записи хранилища Azure hello связаны с рабочей областью hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="484af-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="484af-134">Этот контейнер содержит все сведения о hello диагностики для всех конечных точек службы hello web для всех рабочих областей hello, связанные с этой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="484af-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="484af-135">журналы Hello можно просматривать при помощи любого из hello несколько доступных tooexplore средства учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="484af-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="484af-136">Hello простой может быть toonavigate toohello учетной записи хранилища в hello портал Azure, нажмите кнопку **контейнеры**и затем щелкните контейнер hello **ml диагностики**.</span><span class="sxs-lookup"><span data-stu-id="484af-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="484af-137">Ведение журнала подробных сведений о больших двоичных объектах</span><span class="sxs-lookup"><span data-stu-id="484af-137">Log blob detail information</span></span>
<span data-ttu-id="484af-138">Каждый BLOB-объект в контейнере hello содержит hello диагностическую информацию по одному из hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="484af-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="484af-139">Выполнение метода hello выполнения пакетов</span><span class="sxs-lookup"><span data-stu-id="484af-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="484af-140">Выполнение метода hello запрос-ответ</span><span class="sxs-lookup"><span data-stu-id="484af-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="484af-141">Инициализация контейнера "запрос-ответ"</span><span class="sxs-lookup"><span data-stu-id="484af-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="484af-142">Hello имя каждого большого двоичного объекта имеет префикс hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="484af-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="484af-143">Где _тип журнала_ является одним из hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="484af-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="484af-144">или пакетный</span><span class="sxs-lookup"><span data-stu-id="484af-144">batch</span></span>  
* <span data-ttu-id="484af-145">score/requests</span><span class="sxs-lookup"><span data-stu-id="484af-145">score/requests</span></span>  
* <span data-ttu-id="484af-146">score/init</span><span class="sxs-lookup"><span data-stu-id="484af-146">score/init</span></span>  

