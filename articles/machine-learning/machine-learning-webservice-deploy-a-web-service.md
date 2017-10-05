---
title: "Развертывание новой веб-службы в Машинном обучении Azure | Документация Майкрософт"
description: "Рабочий процесс развертывания веб-службы на основе ARM"
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
redirect_document_id: TRUE
ms.openlocfilehash: 1415709f9da2bb2cce859af9feb0ec15c1fa5801
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="6d2a2-103">Развертывание новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="6d2a2-103">Deploy a new web service</span></span>
<span data-ttu-id="6d2a2-104">Теперь служба машинного обучения Microsoft Azure предоставляет веб-службы на основе [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Это позволяет предложить новые варианты планов выставления счетов и возможности развертывания веб-службы в нескольких регионах.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service to multiple regions.</span></span>

<span data-ttu-id="6d2a2-105">Ниже приведен общий рабочий процесс развертывания веб-службы с помощью веб-служб Машинного обучения Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="6d2a2-105">The general workflow to deploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="6d2a2-106">создание прогнозного эксперимента;</span><span class="sxs-lookup"><span data-stu-id="6d2a2-106">Create a predictive experiment</span></span>
* <span data-ttu-id="6d2a2-107">его развертывание;</span><span class="sxs-lookup"><span data-stu-id="6d2a2-107">deploy it</span></span>
* <span data-ttu-id="6d2a2-108">настройка имени этого эксперимента;</span><span class="sxs-lookup"><span data-stu-id="6d2a2-108">configure its name</span></span>
* <span data-ttu-id="6d2a2-109">Тарифный план</span><span class="sxs-lookup"><span data-stu-id="6d2a2-109">billing plan</span></span>
* <span data-ttu-id="6d2a2-110">его тестирование;</span><span class="sxs-lookup"><span data-stu-id="6d2a2-110">test it</span></span>
* <span data-ttu-id="6d2a2-111">и использование.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-111">consume it.</span></span>

<span data-ttu-id="6d2a2-112">Этот рабочий процесс иллюстрируется на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-112">The following graphic illustrates the workflow.</span></span>

![Рабочий процесс развертывания веб-службы][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="6d2a2-114">Развертывание веб-службы из Студии</span><span class="sxs-lookup"><span data-stu-id="6d2a2-114">Deploy web service from Studio</span></span>
<span data-ttu-id="6d2a2-115">Чтобы развернуть эксперимент в качестве новой веб-службы, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-115">To deploy an experiment as a new web service.</span></span> <span data-ttu-id="6d2a2-116">Войдите в Студию машинного обучения и создайте новую прогнозную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-116">Sign into the Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="6d2a2-117">**Примечание**. Если вы уже развернули эксперимент как классическую веб-службу, вы не сможете развернуть его как новую веб-службу.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="6d2a2-118">Щелкните **Run** (Выполнить) в нижней части холста эксперимента, затем щелкните **Deploy Web Service** (Развернуть веб-службу) и **Deploy Web Service [New]** (Развернуть веб-службу [новую]).</span><span class="sxs-lookup"><span data-stu-id="6d2a2-118">Click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="6d2a2-119">Откроется страница развертывания диспетчера веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-119">The deployment page of the Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="6d2a2-120">Страница развертывания эксперимента в диспетчере веб-службы машинного обучения</span><span class="sxs-lookup"><span data-stu-id="6d2a2-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="6d2a2-121">На странице "Deploy Experiment" (Развертывание эксперимента) введите имя веб-службы.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-121">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="6d2a2-122">Выберите ценовой план.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-122">Select a pricing plan.</span></span> <span data-ttu-id="6d2a2-123">Если у вас уже имеется ценовой план, то можно выбрать его. В противном случае необходимо создать ценовой план для службы.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span> 

1. <span data-ttu-id="6d2a2-124">В раскрывающемся списке **Price Plan** (Ценовой план) выберите существующий план или щелкните **Select new plan** (Выбрать новый план).</span><span class="sxs-lookup"><span data-stu-id="6d2a2-124">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="6d2a2-125">В поле **Имя плана**введите имя для идентификации плана в счете.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-125">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="6d2a2-126">Выберите один из вариантов **Monthly Plan Tier**(Уровень ежемесячного плана).</span><span class="sxs-lookup"><span data-stu-id="6d2a2-126">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="6d2a2-127">Обратите внимание, что по умолчанию указаны уровни плана для вашего региона по умолчанию, и веб-служба развертывается в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-127">Note that the plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="6d2a2-128">Щелкните **Deploy** (Развернуть). Откроется страница быстрого запуска веб-службы.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-128">Click **Deploy** and the Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="6d2a2-129">Страница "Quickstart" (Быстрый запуск)</span><span class="sxs-lookup"><span data-stu-id="6d2a2-129">Quickstart page</span></span>
<span data-ttu-id="6d2a2-130">Страница быстрого запуска веб-службы предоставляет доступ и рекомендации к наиболее распространенным задачам, выполняемым после создания новой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-130">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="6d2a2-131">С нее легко перейти на страницу **Test** (Тестирование) и **Consume** (Использование).</span><span class="sxs-lookup"><span data-stu-id="6d2a2-131">From here you can easily access both the **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="6d2a2-132">Тестирование веб-службы</span><span class="sxs-lookup"><span data-stu-id="6d2a2-132">Testing your web service</span></span>
<span data-ttu-id="6d2a2-133">На странице "Quickstart" (Быстрый запуск) щелкните "Test web service" (Тестировать веб-службу) в разделе общих задач.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-133">From the Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="6d2a2-134">Чтобы протестировать веб-службу как службу RRS (запрос-ответ), выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-134">To test the web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="6d2a2-135">Щелкните **Test** (Тестировать) в строке меню.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-135">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="6d2a2-136">Щелкните **Request-Response**(Запрос-ответ).</span><span class="sxs-lookup"><span data-stu-id="6d2a2-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="6d2a2-137">Введите соответствующие значения для входных столбцов эксперимента.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-137">Enter appropriate values for the input columns of your experiment.</span></span>
* <span data-ttu-id="6d2a2-138">Щелкните **Test Request-Response**(Тестировать "запрос-ответ").</span><span class="sxs-lookup"><span data-stu-id="6d2a2-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="6d2a2-139">Результаты будут показаны в правой части страницы.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-139">You results will display on the right hand side of the page.</span></span>

<span data-ttu-id="6d2a2-140">Чтобы протестировать веб-службу как службу пакетного выполнения (BES), мы используем CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-140">To test a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="6d2a2-141">Щелкните **Test** (Тестировать) в строке меню.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-141">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="6d2a2-142">Щелкните **Batch**(Пакет).</span><span class="sxs-lookup"><span data-stu-id="6d2a2-142">Click **Batch**.</span></span>
* <span data-ttu-id="6d2a2-143">В разделе входных данных нажмите кнопку "Browse" (Обзор) и перейдите к примеру файла данных.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-143">Under your input, click Browse and navigate to your sample data file.</span></span>
* <span data-ttu-id="6d2a2-144">Нажмите **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-144">Click **Test**.</span></span>

<span data-ttu-id="6d2a2-145">Состояние теста отображается в разделе **Test Batch Jobs**(Тестирование пакетных заданий).</span><span class="sxs-lookup"><span data-stu-id="6d2a2-145">The status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="6d2a2-146">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="6d2a2-146">Consuming your Web Service</span></span>
<span data-ttu-id="6d2a2-147">При публикации в качестве веб-службы эксперименты машинного обучения Azure предоставляют REST API, который может использоваться самыми различными устройствами и платформами.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="6d2a2-148">Это происходит благодаря тому, что простой REST API принимает сообщения в формате JSON и отвечает на них в таком же формате.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-148">This is because the simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="6d2a2-149">Портал машинного обучения Azure предоставляет код, который может использоваться для вызова веб-службы на языках R, C# и Python.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-149">The Azure Machine Learning portal provides code that can be used to call the web service in R, C#, and Python.</span></span>

<span data-ttu-id="6d2a2-150">На странице "Consuming" (Использование) можно найти:</span><span class="sxs-lookup"><span data-stu-id="6d2a2-150">On the Consuming page you can find:</span></span>

* <span data-ttu-id="6d2a2-151">ключ API и универсальные коды ресурса (URI) для использования веб-службы в приложениях;</span><span class="sxs-lookup"><span data-stu-id="6d2a2-151">The API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="6d2a2-152">шаблоны Excel и шаблоны веб-приложений, позволяющие быстро начать процесс использования;</span><span class="sxs-lookup"><span data-stu-id="6d2a2-152">Excel and web app templates to kick start your consumption process.</span></span>
* <span data-ttu-id="6d2a2-153">пример кода на C#, Python и R, с помощью которого можно приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="6d2a2-153">Sample code in C#, python, and R to get you started.</span></span>

<span data-ttu-id="6d2a2-154">Дополнительные сведения об использовании веб-служб см. в статье [Как использовать веб-службу машинного обучения Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="6d2a2-154">For more information on consuming web services, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d2a2-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d2a2-155">Next Steps</span></span>
<span data-ttu-id="6d2a2-156">Дополнительные сведения об использовании веб-служб см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="6d2a2-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="6d2a2-157">Как использовать веб-службу машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="6d2a2-157">How to consume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="6d2a2-158">Развертывание и использование веб-служб Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="6d2a2-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
