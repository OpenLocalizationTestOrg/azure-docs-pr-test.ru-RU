---
title: "Параметры веб-службы Azure Machine Learning aaaUse | Документы Microsoft"
description: "Как параметры веб-службы Azure Machine Learning toomodify toouse hello поведение модели при обращении к веб-службе hello."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="585ea-103">Параметры веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="585ea-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="585ea-104">Веб-служба машинного обучения Azure создается при публикации эксперимента, содержащего модули с настраиваемыми параметрами.</span><span class="sxs-lookup"><span data-stu-id="585ea-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="585ea-105">В некоторых случаях может требоваться toochange hello модуля поведение во время выполнения hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="585ea-105">In some cases, you may want toochange hello module behavior while hello web service is running.</span></span> <span data-ttu-id="585ea-106">*Параметры веб-службы* позволяют toodo этой задачи.</span><span class="sxs-lookup"><span data-stu-id="585ea-106">*Web Service Parameters* allow you toodo this task.</span></span> 

<span data-ttu-id="585ea-107">Распространенным примером Настройка hello [импорта данных] [ reader] модуля, в него hello hello опубликованных веб-службы можно указать другой источник данных, при обращении к веб-службе hello.</span><span class="sxs-lookup"><span data-stu-id="585ea-107">A common example is setting up hello [Import Data][reader] module so that hello user of hello published web service can specify a different data source when hello web service is accessed.</span></span> <span data-ttu-id="585ea-108">Или настройка hello [Экспорт данных] [ writer] модуль, можно задать другой целевой.</span><span class="sxs-lookup"><span data-stu-id="585ea-108">Or configuring hello [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="585ea-109">Другие примеры включают изменение hello число битов для hello [хэширование признаков] [ feature-hashing] модуля или hello число необходимых компонентов для hello [Выбор компонентов на основе фильтра] [ filter-based-feature-selection] модуля.</span><span class="sxs-lookup"><span data-stu-id="585ea-109">Some other examples include changing hello number of bits for hello [Feature Hashing][feature-hashing] module or hello number of desired features for hello [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="585ea-110">Можно определить параметры веб-службы и связать их с одним или несколькими параметрами модуля в эксперименте. Вы также можете указать, являются они обязательными или нет.</span><span class="sxs-lookup"><span data-stu-id="585ea-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="585ea-111">во время звонка hello веб-службы пользователя Hello hello веб-службы может предоставить значения для этих параметров.</span><span class="sxs-lookup"><span data-stu-id="585ea-111">hello user of hello web service can then provide values for these parameters when they call hello web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a><span data-ttu-id="585ea-112">Как tooset и используйте параметры веб-службы</span><span class="sxs-lookup"><span data-stu-id="585ea-112">How tooset and use Web Service Parameters</span></span>
<span data-ttu-id="585ea-113">Определение параметра веб-службы, щелкнув hello значок следующего toohello параметра для модуля «Набор как параметр веб-службы».</span><span class="sxs-lookup"><span data-stu-id="585ea-113">You define a Web Service Parameter by clicking hello icon next toohello parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="585ea-114">Это создает новый параметр веб-службы и подключает его toothat параметра модуля.</span><span class="sxs-lookup"><span data-stu-id="585ea-114">This creates a new Web Service Parameter and connects it toothat module parameter.</span></span> <span data-ttu-id="585ea-115">Затем при обращении к веб-службе hello hello пользователь может указать значение для параметра веб-службы hello и примененные toohello параметр модуля.</span><span class="sxs-lookup"><span data-stu-id="585ea-115">Then, when hello web service is accessed, hello user can specify a value for hello Web Service Parameter and it is applied toohello module parameter.</span></span>

<span data-ttu-id="585ea-116">После определения параметра веб-службы является доступной tooany других параметров модуля в эксперименте hello.</span><span class="sxs-lookup"><span data-stu-id="585ea-116">Once you define a Web Service Parameter, it's available tooany other module parameter in hello experiment.</span></span> <span data-ttu-id="585ea-117">При определении параметра веб-службы, связанные с параметром для одного модуля, можно использовать этот же параметр веб-службы для любой другой модуль, до тех пор, пока параметр hello ожидает hello того же типа значения.</span><span class="sxs-lookup"><span data-stu-id="585ea-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as hello parameter expects hello same type of value.</span></span> <span data-ttu-id="585ea-118">Например если hello параметра веб-службы — это числовое значение, затем он может использоваться только для параметры модуля, которые ожидают числовое значение.</span><span class="sxs-lookup"><span data-stu-id="585ea-118">For example, if hello Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="585ea-119">Hello пользователь устанавливает значение для hello параметра веб-службы, он будет применен tooall связанные параметры модуля.</span><span class="sxs-lookup"><span data-stu-id="585ea-119">When hello user sets a value for hello Web Service Parameter, it will be applied tooall associated module parameters.</span></span>

<span data-ttu-id="585ea-120">Можно ли tooprovide значение по умолчанию значение для hello параметра веб-службы.</span><span class="sxs-lookup"><span data-stu-id="585ea-120">You can decide whether tooprovide a default value for hello Web Service Parameter.</span></span> <span data-ttu-id="585ea-121">Если затем hello параметр является необязательным для пользователя hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="585ea-121">If you do, then hello parameter is optional for hello user of hello web service.</span></span> <span data-ttu-id="585ea-122">Если не предоставить значение по умолчанию, hello пользователя является обязательным tooenter значение при обращении к веб-службе hello.</span><span class="sxs-lookup"><span data-stu-id="585ea-122">If you don't provide a default value, then hello user is required tooenter a value when hello web service is accessed.</span></span>

<span data-ttu-id="585ea-123">Hello документации по API для hello веб-службы включает сведения для hello пользователь веб-службы на том, как toospecify hello параметра веб-службы программным способом при доступе к веб-службе hello.</span><span class="sxs-lookup"><span data-stu-id="585ea-123">hello API documentation for hello web service includes information for hello web service user on how toospecify hello Web Service Parameter programmatically when accessing hello web service.</span></span>

> [!NOTE]
> <span data-ttu-id="585ea-124">Здравствуйте документации по API для классических веб-службы предоставляется через hello **страница справки по API** ссылку в веб-службу hello **МОНИТОРИНГА** в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="585ea-124">hello API documentation for a classic web service is provided through hello **API help page** link in hello web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="585ea-125">Здравствуйте, документация по API для нового веб-службы предоставляется через hello [веб-службы Azure Machine Learning](https://services.azureml.net/Quickstart) портала на hello **использование** и **Swagger API** страницы для вашей веб-служба.</span><span class="sxs-lookup"><span data-stu-id="585ea-125">hello API documentation for a new web service is provided through hello [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on hello **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="585ea-126">Пример</span><span class="sxs-lookup"><span data-stu-id="585ea-126">Example</span></span>
<span data-ttu-id="585ea-127">Например, предположим, что у нас есть эксперимент с [Экспорт данных] [ writer] модуль, который отправляет сведения о хранилище больших двоичных объектов tooAzure.</span><span class="sxs-lookup"><span data-stu-id="585ea-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information tooAzure blob storage.</span></span> <span data-ttu-id="585ea-128">Мы определим параметра веб-службы с именем «Путь к BLOB-объектов», позволяющий hello веб-службы пользователя toochange hello путь toohello BLOB-объекта хранилища, при обращении к службе hello.</span><span class="sxs-lookup"><span data-stu-id="585ea-128">We'll define a Web Service Parameter named "Blob path" that allows hello web service user toochange hello path toohello blob storage when hello service is accessed.</span></span>

1. <span data-ttu-id="585ea-129">В студии машинного обучения, щелкните hello [Экспорт данных] [ writer] tooselect модуля его.</span><span class="sxs-lookup"><span data-stu-id="585ea-129">In Machine Learning Studio, click hello [Export Data][writer] module tooselect it.</span></span> <span data-ttu-id="585ea-130">Его свойства отображаются в hello toohello панели свойств справа от холст эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="585ea-130">Its properties are shown in hello Properties pane toohello right of hello experiment canvas.</span></span>
2. <span data-ttu-id="585ea-131">Указание типа hello хранилища:</span><span class="sxs-lookup"><span data-stu-id="585ea-131">Specify hello storage type:</span></span>
   
   * <span data-ttu-id="585ea-132">В разделе **Укажите целевое местоположение данных**выберите "Хранилище BLOB-объектов Azure".</span><span class="sxs-lookup"><span data-stu-id="585ea-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="585ea-133">В разделе **Укажите тип проверки подлинности**выберите "Учетная запись".</span><span class="sxs-lookup"><span data-stu-id="585ea-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="585ea-134">Введите данные учетной записи hello для hello хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="585ea-134">Enter hello account information for hello Azure blob storage.</span></span> 
     <p /><span data-ttu-id="585ea-135">
3.Щелкните toohello hello значок справа от приветствия **tooblob путь, начиная с параметра container**.</span><span class="sxs-lookup"><span data-stu-id="585ea-135">
3. Click hello icon toohello right of hello **Path tooblob beginning with container parameter**.</span></span> <span data-ttu-id="585ea-136">Это выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="585ea-136">It looks like this:</span></span>
   
   ![Значок параметра веб-службы][icon]
   
   <span data-ttu-id="585ea-138">Выберите "Установить как параметр веб-службы".</span><span class="sxs-lookup"><span data-stu-id="585ea-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="585ea-139">Запись добавляется в **параметры веб-службы** hello нижней области свойства hello hello имя «путь tooblob, начинающимся с контейнера».</span><span class="sxs-lookup"><span data-stu-id="585ea-139">An entry is added under **Web Service Parameters** at hello bottom of hello Properties pane with hello name "Path tooblob beginning with container".</span></span> <span data-ttu-id="585ea-140">Это параметр веб-службы, которая теперь находится hello связанный с этим [Экспорт данных] [ writer] параметра модуля.</span><span class="sxs-lookup"><span data-stu-id="585ea-140">This is hello Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="585ea-141">toorename hello параметра веб-службы, щелкните имя hello, введите «Путь к BLOB-объектов» и нажмите hello **ввод** ключа.</span><span class="sxs-lookup"><span data-stu-id="585ea-141">toorename hello Web Service Parameter, click hello name, enter "Blob path", and press hello **Enter** key.</span></span> 
5. <span data-ttu-id="585ea-142">tooprovide значение по умолчанию для hello параметра веб-службы щелкните hello toohello значок справа от имени hello выберите «Предоставлять значение по умолчанию», введите значение (например, «container1/output1.csv») и нажмите клавишу hello **ввод** ключа.</span><span class="sxs-lookup"><span data-stu-id="585ea-142">tooprovide a default value for hello Web Service Parameter, click hello icon toohello right of hello name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press hello **Enter** key.</span></span>
   
   ![Параметр веб-службы][parameter]
6. <span data-ttu-id="585ea-144">Щелкните **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="585ea-144">Click **Run**.</span></span> 
7. <span data-ttu-id="585ea-145">Нажмите кнопку **развертывание веб-службы** и выберите **развертывание веб-службы [классический]** или **развертывания [новое] веб-службы** toodeploy hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="585ea-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** toodeploy hello web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="585ea-146">toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки вы развертывание hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="585ea-146">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="585ea-147">Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="585ea-147">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="585ea-148">пользователь Hello hello веб-службы теперь можно указать новое место назначения для hello [Экспорт данных] [ writer] модуля при доступе к веб-службе hello.</span><span class="sxs-lookup"><span data-stu-id="585ea-148">hello user of hello web service can now specify a new destination for hello [Export Data][writer] module when accessing hello web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="585ea-149">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="585ea-149">More information</span></span>
<span data-ttu-id="585ea-150">Более подробный пример см. в разделе hello [параметры веб-службы](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) запись в hello [машины обучения блог](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span><span class="sxs-lookup"><span data-stu-id="585ea-150">For a more detailed example, see hello [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in hello [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="585ea-151">Дополнительные сведения о доступе к веб-службы машинного обучения см. в разделе [как tooconsume в Azure Machine обучения, веб-службу](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="585ea-151">For more information on accessing a Machine Learning web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

