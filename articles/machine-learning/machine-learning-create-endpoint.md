---
title: "конечные точки службы Web aaaCreating в машинном обучении | Документы Microsoft"
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
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="e975e-103">Создание конечных точек</span><span class="sxs-lookup"><span data-stu-id="e975e-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="e975e-104">В этом разделе описывается tooa применимые методы **классический** веб-машины обучения службы.</span><span class="sxs-lookup"><span data-stu-id="e975e-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="e975e-105">При создании веб-служб, торгующих прямой tooyour клиентов необходимо tooprovide обученных моделей tooeach клиента, которые по-прежнему связанные toohello эксперимент, из которого hello Web служба была создана.</span><span class="sxs-lookup"><span data-stu-id="e975e-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="e975e-106">Кроме того все обновления, должно быть toohello эксперимента применяемой выборочно tooan конечной точки без перезаписи hello настроек.</span><span class="sxs-lookup"><span data-stu-id="e975e-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="e975e-107">tooaccomplish, машинного обучения Azure позволяет toocreate несколько конечных точек для развернутого веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e975e-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="e975e-108">Каждая конечная точка веб-службы hello независимо обращаться, регулирование и управляемых.</span><span class="sxs-lookup"><span data-stu-id="e975e-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="e975e-109">Каждая конечная точка является уникальным ключом URL-адрес и авторизации, можно распространять tooyour клиентов.</span><span class="sxs-lookup"><span data-stu-id="e975e-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="e975e-110">Добавление конечных точек tooa веб-служб</span><span class="sxs-lookup"><span data-stu-id="e975e-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="e975e-111">Существует три способа tooadd tooa конечной точки веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e975e-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="e975e-112">Программным образом</span><span class="sxs-lookup"><span data-stu-id="e975e-112">Programmatically</span></span>
* <span data-ttu-id="e975e-113">Через портал веб-службы Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="e975e-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="e975e-114">Хотя hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="e975e-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="e975e-115">После создания конечной точки hello, можно использовать его через синхронного API, пакетных API и листы excel.</span><span class="sxs-lookup"><span data-stu-id="e975e-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="e975e-116">В дополнение к этому tooadding конечные точки через этот пользовательский Интерфейс, можно также использовать API-интерфейсы управления конечной точки tooprogrammatically hello добавить конечные точки.</span><span class="sxs-lookup"><span data-stu-id="e975e-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="e975e-117">Если вы добавили toohello дополнительные конечные точки веб-службы, нельзя удалить конечную точку по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="e975e-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="e975e-118">Добавление конечной точки программным путем</span><span class="sxs-lookup"><span data-stu-id="e975e-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="e975e-119">Можно добавить веб-служба конечной точки tooyour программно с помощью hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) пример кода.</span><span class="sxs-lookup"><span data-stu-id="e975e-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="e975e-120">Добавление конечной точки с помощью портала веб-службы Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="e975e-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="e975e-121">В студии машинного обучения на столбце hello навигации слева, нажмите кнопку веб-служб.</span><span class="sxs-lookup"><span data-stu-id="e975e-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="e975e-122">Внизу hello hello мониторинга веб-службы, нажмите кнопку **Управление конечными точками**.</span><span class="sxs-lookup"><span data-stu-id="e975e-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="e975e-123">портал веб-службы Azure Machine Learning Hello, откроется страница toohello конечных точек для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e975e-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="e975e-124">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e975e-124">Click **New**.</span></span>
4. <span data-ttu-id="e975e-125">Введите имя и описание для новой конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="e975e-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="e975e-126">Имена конечных точек должны и состоять из строчных букв или цифр и не могут содержать более 24 символов.</span><span class="sxs-lookup"><span data-stu-id="e975e-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="e975e-127">Выберите уровень ведения журнала hello и включена ли образец данных.</span><span class="sxs-lookup"><span data-stu-id="e975e-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="e975e-128">Дополнительные сведения о ведении журнала см. в статье [Включение функции ведения журналов для веб-служб машинного обучения](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="e975e-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="e975e-129">Добавление конечной точки с помощью hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="e975e-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="e975e-130">Войдите в toohello [классический портал Azure](http://manage.windowsazure.com), нажмите кнопку **машинного обучения** в левом столбце hello.</span><span class="sxs-lookup"><span data-stu-id="e975e-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="e975e-131">Щелкните рабочую область hello, который содержит hello веб-службы, в котором вы заинтересованы.</span><span class="sxs-lookup"><span data-stu-id="e975e-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Перейдите tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="e975e-133">Щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="e975e-133">Click **Web Services**.</span></span>
   
    ![Переход службы tooWeb](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="e975e-135">Выберите веб-служба hello, вас интересует toosee hello список доступных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="e975e-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Перейдите tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="e975e-137">Внизу hello страницы приветствия щелкните **добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="e975e-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="e975e-138">Введите имя и описание, убедитесь, что нет других конечных точек с hello точно такое же имя в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="e975e-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="e975e-139">Оставьте уровень регулировки hello со значением по умолчанию, если у вас нет особых требований.</span><span class="sxs-lookup"><span data-stu-id="e975e-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="e975e-140">toolearn Дополнительные сведения о регулирования количества запросов, в разделе [масштабирование конечные точки API](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e975e-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Создать конечную точку](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="e975e-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e975e-142">Next Steps</span></span>
<span data-ttu-id="e975e-143">[Как tooconsume в Azure Machine обучения, веб-службу](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e975e-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

