---
title: "Переобучение модели машинного обучения | Документация Майкрософт"
description: "Узнайте, как переобучить модель и обновить веб-службу так, чтобы она использовала заново обученную модель в службе машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: f86c2bc41dd7ff0bc31454a56b84d136dc7d026c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="9f4ec-103">Переобучение модели машинного обучения</span><span class="sxs-lookup"><span data-stu-id="9f4ec-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="9f4ec-104">В рамках процесса операционализации моделей машинного обучения в Машинном обучении Azure модель обучается и сохраняется.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="9f4ec-105">После этого она используется для создания прогнозной веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-105">You then use it to create a predicative Web service.</span></span> <span data-ttu-id="9f4ec-106">Созданная веб-служба может впоследствии использоваться на веб-сайтах, панелях мониторинга и в мобильных приложениях.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="9f4ec-107">Модели, создаваемые с помощью машинного обучения, обычно не статические.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="9f4ec-108">Если появляются новые данные или у пользователя API есть свои данные, модель нужно переобучить.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> 

<span data-ttu-id="9f4ec-109">Переобучение может требоваться достаточно часто.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-109">Retraining may occur frequently.</span></span> <span data-ttu-id="9f4ec-110">Интерфейс API программного переобучения позволяет программным путем переобучить модель с помощью API переобучения и обновить веб-службу, чтобы она использовала эту модель.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span></span> 

<span data-ttu-id="9f4ec-111">В этом документе описана процедура переобучения и показано, как использовать интерфейсы API переобучения.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span></span>

## <a name="why-retrain-defining-the-problem"></a><span data-ttu-id="9f4ec-112">Зачем нужно повторное обучение: определение проблемы</span><span class="sxs-lookup"><span data-stu-id="9f4ec-112">Why retrain: defining the problem</span></span>
<span data-ttu-id="9f4ec-113">В рамках процесса машинного обучения модель обучается с использованием определенного набора данных.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-113">As part of the machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="9f4ec-114">Модели, создаваемые с помощью машинного обучения, обычно не статические.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="9f4ec-115">Если появляются новые данные или у пользователя API есть свои данные, модель нужно переобучить.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span>

<span data-ttu-id="9f4ec-116">В этих сценариях программный API обеспечивает для вас или потребителя API удобный способ создания клиента, который может единовременно или регулярно переобучать модель при помощи собственных данных.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span></span> <span data-ttu-id="9f4ec-117">После этого можно оценить результаты переобучения и обновить API веб-службы, чтобы использовать его с недавно обученной моделью.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="9f4ec-118">Если у вас есть обучающий эксперимент и новая веб-служба, возможно, вас заинтересует раздел, посвященный переобучению существующей прогнозной веб-службы, а не пошаговое руководство, упомянутое в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="9f4ec-119">Комплексный рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="9f4ec-119">End-to-end workflow</span></span>
<span data-ttu-id="9f4ec-120">В процессе задействованы следующие компоненты: обучающий эксперимент и прогнозный эксперимент, опубликованный в виде веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="9f4ec-121">Чтобы включить переобучение обученной модели, обучающий эксперимент необходимо опубликовать в виде веб-службы, выходные данные которой будут представлять собой обученную модель.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span></span> <span data-ttu-id="9f4ec-122">Это позволит использовать API-доступ для переобучения модели.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-122">This enables API access to the model for retraining.</span></span> 

<span data-ttu-id="9f4ec-123">Следующие шаги применяются как к новым, так и к классическим веб-службам.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-123">The following steps apply to both New and Classic Web services:</span></span>

<span data-ttu-id="9f4ec-124">Создание начальной прогнозной веб-службы:</span><span class="sxs-lookup"><span data-stu-id="9f4ec-124">Create the initial Predictive Web service:</span></span>

* <span data-ttu-id="9f4ec-125">Создание обучающего эксперимента</span><span class="sxs-lookup"><span data-stu-id="9f4ec-125">Create a training experiment</span></span>
* <span data-ttu-id="9f4ec-126">Создайте прогнозный веб-эксперимент.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="9f4ec-127">Разверните прогнозную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-127">Deploy a predictive web service</span></span>

<span data-ttu-id="9f4ec-128">Переобучение веб-службы:</span><span class="sxs-lookup"><span data-stu-id="9f4ec-128">Retrain the Web service:</span></span>

* <span data-ttu-id="9f4ec-129">Обновите обучающий эксперимент, чтобы предусмотреть переобучение.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-129">Update training experiment to allow for retraining</span></span>
* <span data-ttu-id="9f4ec-130">Разверните переобучающую веб-службу.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-130">Deploy the retraining web service</span></span>
* <span data-ttu-id="9f4ec-131">Используйте код службы пакетного выполнения, чтобы переобучить модель.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-131">Use the Batch Execution Service code to retrain the model</span></span>

<span data-ttu-id="9f4ec-132">Пошаговое руководство на основе указанных выше шагов см. в разделе [Программное переобучение моделей машинного обучения](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="9f4ec-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="9f4ec-133">Для развертывания новой веб-службы у вас должен быть достаточный уровень разрешений в подписке, в которую выполняется развертывание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="9f4ec-134">Дополнительные сведения см. в статье [Управление веб-службой с помощью портала веб-служб машинного обучения Azure](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="9f4ec-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="9f4ec-135">Если развернута классическая веб-служба, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="9f4ec-136">Создайте новую конечную точку в прогнозной веб-службе.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-136">Create a new Endpoint on the Predictive Web service</span></span>
* <span data-ttu-id="9f4ec-137">Получите URL-адрес и код исправления.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-137">Get the PATCH URL and code</span></span>
* <span data-ttu-id="9f4ec-138">Используйте URL-адрес исправления, чтобы указать новую конечную точку на переобученной модели.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-138">Use the PATCH URL to point the new Endpoint at the retrained model</span></span> 

<span data-ttu-id="9f4ec-139">Пошаговое руководство на основе указанных выше шагов см. в разделе о [переобучении классической веб-службы](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9f4ec-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="9f4ec-140">В случае возникновения трудностей при переобучении классической веб-службы см. раздел [Устранение неполадок при повторном обучении классической веб-службы машинного обучения Azure](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="9f4ec-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="9f4ec-141">Если развернута новая веб-служба, необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9f4ec-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="9f4ec-142">Вход в учетную запись Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9f4ec-142">Sign in to your Azure Resource Manager account</span></span>
* <span data-ttu-id="9f4ec-143">Получить определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-143">Get the Web service definition</span></span>
* <span data-ttu-id="9f4ec-144">Экспортировать определение веб-службы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-144">Export the Web Service Definition as JSON</span></span>
* <span data-ttu-id="9f4ec-145">Обновить ссылку на большой двоичный объект `ilearner` в JSON.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-145">Update the reference to the `ilearner` blob in the JSON</span></span>
* <span data-ttu-id="9f4ec-146">Импортировать JSON в определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-146">Import the JSON into a Web Service Definition</span></span>
* <span data-ttu-id="9f4ec-147">Обновить веб-службу с помощью нового определения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-147">Update the Web service with new Web Service Definition</span></span>

<span data-ttu-id="9f4ec-148">Пошаговое руководство на основе указанных выше шагов см. в статье [Переобучение новой веб-службы с помощью командлетов управления PowerShell Машинного обучения](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9f4ec-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="9f4ec-149">Процесс настройки переобучения для классической веб-службы включает в себя следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9f4ec-149">The process for setting up retraining for a Classic Web service involves the following steps:</span></span>

![Обзор процесса переобучения][1]

<span data-ttu-id="9f4ec-151">Процесс настройки переобучения для новой веб-службы включает в себя следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9f4ec-151">The process for setting up retraining for a New Web service involves the following steps:</span></span>

![Обзор процесса переобучения][7]

## <a name="other-resources"></a><span data-ttu-id="9f4ec-153">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="9f4ec-153">Other Resources</span></span>
* <span data-ttu-id="9f4ec-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/) (Переобучение и обновление моделей машинного обучения Azure с фабрикой данных Azure).</span><span class="sxs-lookup"><span data-stu-id="9f4ec-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)</span></span>
* <span data-ttu-id="9f4ec-155">[Создание множества моделей машинного обучения и конечных точек веб-службы из одного эксперимента с помощью PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9f4ec-155">[Create many Machine Learning models and web service endpoints from one experiment using PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md)</span></span>
* <span data-ttu-id="9f4ec-156">В видео [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) (Переобучение моделей AML с помощью API-интерфейсов) показано, как переобучать модели машинного обучения, созданные в службе машинного обучения Azure, с использованием API-интерфейсов переобучения и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f4ec-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

