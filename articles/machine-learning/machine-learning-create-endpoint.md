---
title: "Создание конечных точек веб-службы в машинном обучении | Документация Майкрософт"
description: "Создание конечных точек веб-службы в машинном обучении Azure"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 9f83ffc9cf7dbe37c1ce9980fd7f5b9133fe78f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="e4339-103">Создание конечных точек</span><span class="sxs-lookup"><span data-stu-id="e4339-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="e4339-104">В этой статье описаны методы, применимые для **классической** веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="e4339-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="e4339-105">При создании веб-служб для продажи заказчикам необходимо предоставить каждому заказчику обученные модели, привязанные к эксперименту, на основе которого была создана веб-служба.</span><span class="sxs-lookup"><span data-stu-id="e4339-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="e4339-106">Кроме того, все обновления эксперимента следует выборочно применять к конечной точке без перезаписи настроек.</span><span class="sxs-lookup"><span data-stu-id="e4339-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="e4339-107">С этой целью машинное обучение Azure позволяет создать несколько конечных точек для развернутой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e4339-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="e4339-108">Каждая конечная точка в веб-службе адресуется, регулируется и управляется независимо.</span><span class="sxs-lookup"><span data-stu-id="e4339-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="e4339-109">Каждая конечная точка представляет собой уникальный URL-адрес и ключ авторизации, который можно передавать заказчикам.</span><span class="sxs-lookup"><span data-stu-id="e4339-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="e4339-110">Добавление конечных точек в веб-службу</span><span class="sxs-lookup"><span data-stu-id="e4339-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="e4339-111">Существует три способа добавления конечной точки в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="e4339-111">There are three ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="e4339-112">Программным образом</span><span class="sxs-lookup"><span data-stu-id="e4339-112">Programmatically</span></span>
* <span data-ttu-id="e4339-113">С помощью портала веб-служб машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="e4339-113">Through the Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="e4339-114">С помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="e4339-114">Though the Azure classic portal</span></span>

<span data-ttu-id="e4339-115">После создания конечную точку можно использовать в синхронных API, API пакетов и на листах Excel.</span><span class="sxs-lookup"><span data-stu-id="e4339-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="e4339-116">Кроме добавления конечных точек посредством этого пользовательского интерфейса можно также использовать интерфейсы API управления конечными точками, чтобы добавлять конечные точки программно.</span><span class="sxs-lookup"><span data-stu-id="e4339-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="e4339-117">Если в веб-службу добавлены дополнительные конечные точки, установленную по умолчанию конечную точку удалить нельзя.</span><span class="sxs-lookup"><span data-stu-id="e4339-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="e4339-118">Добавление конечной точки программным путем</span><span class="sxs-lookup"><span data-stu-id="e4339-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="e4339-119">Конечную точку можно добавить в веб-службу программным путем, используя образец кода [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="e4339-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="e4339-120">Добавление конечной точки с помощью портала веб-служб машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="e4339-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="e4339-121">В Студии машинного обучения в левой области навигации щелкните "Web Services" (Веб-службы).</span><span class="sxs-lookup"><span data-stu-id="e4339-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="e4339-122">В нижней части панели мониторинга веб-служб щелкните **Manage endpoints** (Управление конечными точками).</span><span class="sxs-lookup"><span data-stu-id="e4339-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="e4339-123">Портал веб-служб машинного обучения Azure откроется на странице конечных точек для веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e4339-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="e4339-124">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e4339-124">Click **New**.</span></span>
4. <span data-ttu-id="e4339-125">Введите имя и описание новой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="e4339-125">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="e4339-126">Имена конечных точек должны и состоять из строчных букв или цифр и не могут содержать более 24 символов.</span><span class="sxs-lookup"><span data-stu-id="e4339-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="e4339-127">Выберите уровень ведения журнала и укажите, включать ли образцы данных.</span><span class="sxs-lookup"><span data-stu-id="e4339-127">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="e4339-128">Дополнительные сведения о ведении журнала см. в статье [Включение функции ведения журналов для веб-служб машинного обучения](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="e4339-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a><span data-ttu-id="e4339-129">Добавление конечной точки с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="e4339-129">Adding an endpoint using the Azure classic portal</span></span>
1. <span data-ttu-id="e4339-130">Войдите на [классический портал Azure](http://manage.windowsazure.com), выберите элемент **Машинное обучение** в левом столбце.</span><span class="sxs-lookup"><span data-stu-id="e4339-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span></span> <span data-ttu-id="e4339-131">Щелкните рабочую область, которая содержит требуемую веб-службу.</span><span class="sxs-lookup"><span data-stu-id="e4339-131">Click the workspace which contains the Web service in which you are interested.</span></span>
   
    ![Перейти к рабочей области](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="e4339-133">Щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="e4339-133">Click **Web Services**.</span></span>
   
    ![Перейти к веб-службам](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="e4339-135">Щелкните веб-службу, которая вас интересует, чтобы увидеть список доступных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="e4339-135">Click the Web service you're interested in to see the list of available endpoints.</span></span>
   
    ![Перейти к конечной точке](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="e4339-137">В нижней части страницы щелкните **Добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="e4339-137">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="e4339-138">Введите имя и описание, а также убедитесь, что в этой веб-службе нет других конечных точек с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="e4339-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span></span> <span data-ttu-id="e4339-139">Оставьте значение по умолчанию для уровня регулирования, если у вас нет конкретных требований.</span><span class="sxs-lookup"><span data-stu-id="e4339-139">Leave the throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="e4339-140">Дополнительную информацию о регулировании см. в статье [Масштабирование веб-службы](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e4339-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Создать конечную точку](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="e4339-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4339-142">Next Steps</span></span>
<span data-ttu-id="e4339-143">[Как использовать веб-службу машинного обучения Azure](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="e4339-143">[How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

