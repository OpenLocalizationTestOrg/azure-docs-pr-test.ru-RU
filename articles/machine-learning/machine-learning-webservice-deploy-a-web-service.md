---
title: "aaaDeploying веб-службу в машинном обучении Azure | Документы Microsoft"
description: "рабочий процесс Hello ARM развертывания на основе веб-службы"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="87e53-103">Развертывание новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="87e53-103">Deploy a new web service</span></span>
<span data-ttu-id="87e53-104">Машины Microsoft Azure теперь предоставляет веб-служб, основанных на [диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md) поддержка новые параметры плана выставления счетов и развертывание вашей web service toomultiple областей.</span><span class="sxs-lookup"><span data-stu-id="87e53-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="87e53-105">— общий рабочий процесс Hello toodeploy веб-службы с помощью веб-службы Microsoft Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="87e53-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="87e53-106">создание прогнозного эксперимента;</span><span class="sxs-lookup"><span data-stu-id="87e53-106">Create a predictive experiment</span></span>
* <span data-ttu-id="87e53-107">его развертывание;</span><span class="sxs-lookup"><span data-stu-id="87e53-107">deploy it</span></span>
* <span data-ttu-id="87e53-108">настройка имени этого эксперимента;</span><span class="sxs-lookup"><span data-stu-id="87e53-108">configure its name</span></span>
* <span data-ttu-id="87e53-109">Тарифный план</span><span class="sxs-lookup"><span data-stu-id="87e53-109">billing plan</span></span>
* <span data-ttu-id="87e53-110">его тестирование;</span><span class="sxs-lookup"><span data-stu-id="87e53-110">test it</span></span>
* <span data-ttu-id="87e53-111">и использование.</span><span class="sxs-lookup"><span data-stu-id="87e53-111">consume it.</span></span>

<span data-ttu-id="87e53-112">Следующий график Hello показан рабочий процесс hello.</span><span class="sxs-lookup"><span data-stu-id="87e53-112">hello following graphic illustrates hello workflow.</span></span>

![Рабочий процесс развертывания веб-службы][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="87e53-114">Развертывание веб-службы из Студии</span><span class="sxs-lookup"><span data-stu-id="87e53-114">Deploy web service from Studio</span></span>
<span data-ttu-id="87e53-115">toodeploy эксперимент как веб-службу.</span><span class="sxs-lookup"><span data-stu-id="87e53-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="87e53-116">Вход в студии машинного обучения hello и создайте новый прогнозирующей веб-службы.</span><span class="sxs-lookup"><span data-stu-id="87e53-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="87e53-117">**Примечание**. Если вы уже развернули эксперимент как классическую веб-службу, вы не сможете развернуть его как новую веб-службу.</span><span class="sxs-lookup"><span data-stu-id="87e53-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="87e53-118">Нажмите кнопку **запуска** внизу hello hello поэкспериментировать холст, а затем нажмите кнопку **развертывание веб-службы** и **развертывания [новое] веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="87e53-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="87e53-119">Откроется страница Hello развертывания диспетчера hello машины обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="87e53-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="87e53-120">Страница развертывания эксперимента в диспетчере веб-службы машинного обучения</span><span class="sxs-lookup"><span data-stu-id="87e53-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="87e53-121">На странице развертывание эксперимента hello введите имя для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="87e53-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="87e53-122">Выберите ценовой план.</span><span class="sxs-lookup"><span data-stu-id="87e53-122">Select a pricing plan.</span></span> <span data-ttu-id="87e53-123">При наличии существующего ценовой план, можно выбрать его, в противном случае необходимо создать новый план цены для службы hello.</span><span class="sxs-lookup"><span data-stu-id="87e53-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="87e53-124">В hello **плана цены** раскрывающийся список, выберите существующий план или hello **выберите новый план** параметр.</span><span class="sxs-lookup"><span data-stu-id="87e53-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="87e53-125">В **имя плана**, введите имя, которое будет идентифицировать hello плана на вашем счете.</span><span class="sxs-lookup"><span data-stu-id="87e53-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="87e53-126">Выберите один из hello **ежемесячные уровней плана**.</span><span class="sxs-lookup"><span data-stu-id="87e53-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="87e53-127">Обратите внимание, что hello плана уровней по умолчанию toohello планы для своего региона по умолчанию веб-службы — развернутой toothat область.</span><span class="sxs-lookup"><span data-stu-id="87e53-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="87e53-128">Нажмите кнопку **развернуть** и открывает страницу приветствия быстрого запуска веб-службы.</span><span class="sxs-lookup"><span data-stu-id="87e53-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="87e53-129">Страница "Quickstart" (Быстрый запуск)</span><span class="sxs-lookup"><span data-stu-id="87e53-129">Quickstart page</span></span>
<span data-ttu-id="87e53-130">Краткое руководство страницу приветствия веб-службы позволяет руководство и доступа на hello наиболее распространенных задач, которые необходимо выполнить после создания нового веб-службы.</span><span class="sxs-lookup"><span data-stu-id="87e53-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="87e53-131">Здесь можно легко получить оба hello **тест** страницы и **использование** страницы.</span><span class="sxs-lookup"><span data-stu-id="87e53-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="87e53-132">Тестирование веб-службы</span><span class="sxs-lookup"><span data-stu-id="87e53-132">Testing your web service</span></span>
<span data-ttu-id="87e53-133">В списке общих задач hello страницу быстрого запуска, щелкните тест веб-службы.</span><span class="sxs-lookup"><span data-stu-id="87e53-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="87e53-134">веб-служба hello tootest как запрос-ответ службы (RR):</span><span class="sxs-lookup"><span data-stu-id="87e53-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="87e53-135">Нажмите кнопку **теста** меню hello.</span><span class="sxs-lookup"><span data-stu-id="87e53-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="87e53-136">Щелкните **Request-Response**(Запрос-ответ).</span><span class="sxs-lookup"><span data-stu-id="87e53-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="87e53-137">Введите соответствующие значения для входных столбцов hello эксперимента.</span><span class="sxs-lookup"><span data-stu-id="87e53-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="87e53-138">Щелкните **Test Request-Response**(Тестировать "запрос-ответ").</span><span class="sxs-lookup"><span data-stu-id="87e53-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="87e53-139">Результаты будут отображаться hello правой стороны страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="87e53-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="87e53-140">tootest веб-службы пакетного выполнения службы (BES) используется в CSV-файл:</span><span class="sxs-lookup"><span data-stu-id="87e53-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="87e53-141">Нажмите кнопку **теста** меню hello.</span><span class="sxs-lookup"><span data-stu-id="87e53-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="87e53-142">Щелкните **Batch**(Пакет).</span><span class="sxs-lookup"><span data-stu-id="87e53-142">Click **Batch**.</span></span>
* <span data-ttu-id="87e53-143">В разделе входные данные нажмите кнопку обзора и перейдите tooyour образец файла данных.</span><span class="sxs-lookup"><span data-stu-id="87e53-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="87e53-144">Нажмите **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="87e53-144">Click **Test**.</span></span>

<span data-ttu-id="87e53-145">Hello состояние теста отображается в списке **тестирования пакетных заданий**.</span><span class="sxs-lookup"><span data-stu-id="87e53-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="87e53-146">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="87e53-146">Consuming your Web Service</span></span>
<span data-ttu-id="87e53-147">При публикации в качестве веб-службы эксперименты машинного обучения Azure предоставляют REST API, который может использоваться самыми различными устройствами и платформами.</span><span class="sxs-lookup"><span data-stu-id="87e53-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="87e53-148">Это так, как сообщения в формате hello простой API-Интерфейс REST принимает и отправляет в ответ JSON.</span><span class="sxs-lookup"><span data-stu-id="87e53-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="87e53-149">Hello портала машинного обучения Azure предоставляет код, который может использоваться toocall hello веб-службы в R, C# и Python.</span><span class="sxs-lookup"><span data-stu-id="87e53-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="87e53-150">На странице приветствия Consuming можно найти:</span><span class="sxs-lookup"><span data-stu-id="87e53-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="87e53-151">ключ Hello API и URI для использования веб-службы в приложениях.</span><span class="sxs-lookup"><span data-stu-id="87e53-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="87e53-152">Excel и веб-tookick шаблоны приложений запускайте процесс потребления.</span><span class="sxs-lookup"><span data-stu-id="87e53-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="87e53-153">Пример кода на C#, python и R tooget был запущен.</span><span class="sxs-lookup"><span data-stu-id="87e53-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="87e53-154">Дополнительные сведения об использовании веб-служб см. в разделе [как tooconsume в Azure Machine обучения, веб-службу](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="87e53-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87e53-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87e53-155">Next Steps</span></span>
<span data-ttu-id="87e53-156">Дополнительные сведения об использовании веб-служб см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="87e53-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="87e53-157">Как tooconsume Azure машины обучения, веб-службы</span><span class="sxs-lookup"><span data-stu-id="87e53-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="87e53-158">Развертывание и использование веб-служб Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="87e53-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
