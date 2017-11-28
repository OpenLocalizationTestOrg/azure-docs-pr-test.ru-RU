---
title: "Использование параметров веб-службы машинного обучения Azure | Документация Майкрософт"
description: "Как использовать параметры веб-службы машинного обучения Azure для изменения поведения модели при доступе к веб-службе."
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
ms.openlocfilehash: 482726c1dae5385964e08b720e529817d5907537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="d1663-103">Параметры веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="d1663-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="d1663-104">Веб-служба машинного обучения Azure создается при публикации эксперимента, содержащего модули с настраиваемыми параметрами.</span><span class="sxs-lookup"><span data-stu-id="d1663-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="d1663-105">В некоторых случаях может потребоваться изменение поведения модуля, пока веб-служба выполняется.</span><span class="sxs-lookup"><span data-stu-id="d1663-105">In some cases, you may want to change the module behavior while the web service is running.</span></span> <span data-ttu-id="d1663-106">*Параметры веб-службы* позволяют это сделать.</span><span class="sxs-lookup"><span data-stu-id="d1663-106">*Web Service Parameters* allow you to do this task.</span></span> 

<span data-ttu-id="d1663-107">Типичный пример — настройка модуля [Импорт данных][reader], благодаря которому пользователь опубликованной веб-службы может указать другой источник данных при обращении к веб-службе.</span><span class="sxs-lookup"><span data-stu-id="d1663-107">A common example is setting up the [Import Data][reader] module so that the user of the published web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="d1663-108">Или настройка модуля [Export Data][writer] (Экспорт данных), позволяющего указать другое назначение.</span><span class="sxs-lookup"><span data-stu-id="d1663-108">Or configuring the [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="d1663-109">Некоторые другие примеры включают изменение количества битов модуля [Feature Hashing][feature-hashing] (Хэширование функций) или количества желаемых функций для модуля [Filter-Based Feature Selection][filter-based-feature-selection] (Выбор компонентов на основе фильтра).</span><span class="sxs-lookup"><span data-stu-id="d1663-109">Some other examples include changing the number of bits for the [Feature Hashing][feature-hashing] module or the number of desired features for the [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="d1663-110">Можно определить параметры веб-службы и связать их с одним или несколькими параметрами модуля в эксперименте. Вы также можете указать, являются они обязательными или нет.</span><span class="sxs-lookup"><span data-stu-id="d1663-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="d1663-111">Пользователь веб-службы затем может предоставить значения этих параметров при вызове веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d1663-111">The user of the web service can then provide values for these parameters when they call the web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-to-set-and-use-web-service-parameters"></a><span data-ttu-id="d1663-112">Как установить и использовать параметры веб-службы</span><span class="sxs-lookup"><span data-stu-id="d1663-112">How to set and use Web Service Parameters</span></span>
<span data-ttu-id="d1663-113">Параметр веб-службы задается путем щелчка по значку рядом с параметром конкретного модуля и выбора команды "Установить в качестве параметра веб-службы".</span><span class="sxs-lookup"><span data-stu-id="d1663-113">You define a Web Service Parameter by clicking the icon next to the parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="d1663-114">При этом создается новый параметр веб-службы, который связывается с параметром модуля.</span><span class="sxs-lookup"><span data-stu-id="d1663-114">This creates a new Web Service Parameter and connects it to that module parameter.</span></span> <span data-ttu-id="d1663-115">Затем при доступе к веб-службе пользователь может указать значение параметра веб-службы, который будет применен к параметру модуля.</span><span class="sxs-lookup"><span data-stu-id="d1663-115">Then, when the web service is accessed, the user can specify a value for the Web Service Parameter and it is applied to the module parameter.</span></span>

<span data-ttu-id="d1663-116">После определения параметр веб-службы будет доступен для любого другого параметра модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="d1663-116">Once you define a Web Service Parameter, it's available to any other module parameter in the experiment.</span></span> <span data-ttu-id="d1663-117">Если вы определите параметр веб-службы, связанный с параметром для одного модуля, можно использовать этот же параметр веб-службы для любого другого модуля в тех случаях, когда параметр использует значения одного типа.</span><span class="sxs-lookup"><span data-stu-id="d1663-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as the parameter expects the same type of value.</span></span> <span data-ttu-id="d1663-118">Например, если параметр веб-службы имеет числовое значение, это означает, что его можно использовать только для параметров модуля, которые принимают числовые значения.</span><span class="sxs-lookup"><span data-stu-id="d1663-118">For example, if the Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="d1663-119">Когда пользователь устанавливает значение для параметра веб-службы, оно будет применено ко всем связанным параметрам модуля.</span><span class="sxs-lookup"><span data-stu-id="d1663-119">When the user sets a value for the Web Service Parameter, it will be applied to all associated module parameters.</span></span>

<span data-ttu-id="d1663-120">Вы можете принять решение о том, следует ли предоставлять значение по умолчанию для параметра веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d1663-120">You can decide whether to provide a default value for the Web Service Parameter.</span></span> <span data-ttu-id="d1663-121">Если принимается решение предоставлять это значение, то параметр становится необязательным для пользователя веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d1663-121">If you do, then the parameter is optional for the user of the web service.</span></span> <span data-ttu-id="d1663-122">Если вы не предоставите значение по умолчанию, то от пользователя потребуется ввести значение при доступе к веб-службе.</span><span class="sxs-lookup"><span data-stu-id="d1663-122">If you don't provide a default value, then the user is required to enter a value when the web service is accessed.</span></span>

<span data-ttu-id="d1663-123">Документация по API для веб-службы содержит сведения для пользователя веб-службы о том, как программно указать параметр веб-службы при доступе к ней.</span><span class="sxs-lookup"><span data-stu-id="d1663-123">The API documentation for the web service includes information for the web service user on how to specify the Web Service Parameter programmatically when accessing the web service.</span></span>

> [!NOTE]
> <span data-ttu-id="d1663-124">Документация по API для классической веб-службы предоставляется по ссылке на **страницу справки API**, доступной на **панели мониторинга** этой веб-службы в Студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d1663-124">The API documentation for a classic web service is provided through the **API help page** link in the web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="d1663-125">Документация по API для новой веб-службы предоставляется на портале [веб-служб Машинного обучения Azure](https://services.azureml.net/Quickstart) на страницах **Consume** (Использование) и **Swagger API** этой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d1663-125">The API documentation for a new web service is provided through the [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on the **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="d1663-126">Пример</span><span class="sxs-lookup"><span data-stu-id="d1663-126">Example</span></span>
<span data-ttu-id="d1663-127">В качестве примера предположим, что у нас имеется эксперимент с модулем [Export Data][writer] (Экспорт данных), который отправляет сведения в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="d1663-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information to Azure blob storage.</span></span> <span data-ttu-id="d1663-128">Мы определим параметр веб-службы с именем "Путь к BLOB-объекту", который позволяет пользователю веб-службы изменять путь к хранилищу BLOB-объектов при доступе к этой службе.</span><span class="sxs-lookup"><span data-stu-id="d1663-128">We'll define a Web Service Parameter named "Blob path" that allows the web service user to change the path to the blob storage when the service is accessed.</span></span>

1. <span data-ttu-id="d1663-129">В Студии машинного обучения щелкните модуль [Export Data][writer] (Экспорт данных), чтобы выбрать его.</span><span class="sxs-lookup"><span data-stu-id="d1663-129">In Machine Learning Studio, click the [Export Data][writer] module to select it.</span></span> <span data-ttu-id="d1663-130">Его свойства отображаются на панели "Свойства" справа от холста эксперимента.</span><span class="sxs-lookup"><span data-stu-id="d1663-130">Its properties are shown in the Properties pane to the right of the experiment canvas.</span></span>
2. <span data-ttu-id="d1663-131">Укажите тип хранилища.</span><span class="sxs-lookup"><span data-stu-id="d1663-131">Specify the storage type:</span></span>
   
   * <span data-ttu-id="d1663-132">В разделе **Укажите целевое местоположение данных**выберите "Хранилище BLOB-объектов Azure".</span><span class="sxs-lookup"><span data-stu-id="d1663-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="d1663-133">В разделе **Укажите тип проверки подлинности**выберите "Учетная запись".</span><span class="sxs-lookup"><span data-stu-id="d1663-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="d1663-134">Введите данные учетной записи для хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="d1663-134">Enter the account information for the Azure blob storage.</span></span> 
     <p /><span data-ttu-id="d1663-135">
3. Щелкните значок справа от элемента **Path to blob beginning with container parameter** (Путь к большому двоичному объекту, начиная с параметра контейнера).</span><span class="sxs-lookup"><span data-stu-id="d1663-135">
3. Click the icon to the right of the **Path to blob beginning with container parameter**.</span></span> <span data-ttu-id="d1663-136">Это выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d1663-136">It looks like this:</span></span>
   
   ![Значок параметра веб-службы][icon]
   
   <span data-ttu-id="d1663-138">Выберите "Установить как параметр веб-службы".</span><span class="sxs-lookup"><span data-stu-id="d1663-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="d1663-139">В раздел **Параметры веб-службы** внизу на странице "Свойства" добавляется запись с именем "Путь к BLOB-объекту, начиная с контейнера".</span><span class="sxs-lookup"><span data-stu-id="d1663-139">An entry is added under **Web Service Parameters** at the bottom of the Properties pane with the name "Path to blob beginning with container".</span></span> <span data-ttu-id="d1663-140">Этот параметр веб-службы теперь связан с параметром модуля [Export Data][writer] (Экспорт данных).</span><span class="sxs-lookup"><span data-stu-id="d1663-140">This is the Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="d1663-141">Чтобы переименовать параметр веб-службы, щелкните имя, введите "Путь к BLOB-объекту", после чего нажмите клавишу **ВВОД** .</span><span class="sxs-lookup"><span data-stu-id="d1663-141">To rename the Web Service Parameter, click the name, enter "Blob path", and press the **Enter** key.</span></span> 
5. <span data-ttu-id="d1663-142">Чтобы предоставить значение по умолчанию для параметра веб-службы, щелкните значок справа от имени, выберите "Предоставить значение по умолчанию", введите значение (например, "контейнер1/выход1.csv"), после чего нажмите клавишу **ВВОД** .</span><span class="sxs-lookup"><span data-stu-id="d1663-142">To provide a default value for the Web Service Parameter, click the icon to the right of the name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press the **Enter** key.</span></span>
   
   ![Параметр веб-службы][parameter]
6. <span data-ttu-id="d1663-144">Щелкните **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="d1663-144">Click **Run**.</span></span> 
7. <span data-ttu-id="d1663-145">Щелкните **Deploy Web Service** (Развернуть веб-службу) и выберите **Deploy Web Service [Classic]** (Развернуть веб-службу [классическую]) или **Deploy Web Service [New]** (Развернуть веб-службу [новую]), чтобы развернуть ее.</span><span class="sxs-lookup"><span data-stu-id="d1663-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** to deploy the web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="d1663-146">Для развертывания новой веб-службы у вас должен быть достаточный уровень разрешений в подписке, в которую выполняется развертывание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d1663-146">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="d1663-147">Дополнительные сведения см. в статье [Управление веб-службой с помощью портала веб-служб машинного обучения Azure](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d1663-147">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="d1663-148">Теперь пользователь веб-службы может указать новое расположение для модуля [Export Data][writer] (Экспорт данных) при доступе к веб-службе.</span><span class="sxs-lookup"><span data-stu-id="d1663-148">The user of the web service can now specify a new destination for the [Export Data][writer] module when accessing the web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="d1663-149">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="d1663-149">More information</span></span>
<span data-ttu-id="d1663-150">Более подробный пример см. в публикации [AzureML Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) (Параметры веб-службы AzureML) [блога, посвященного машинному обучению](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1663-150">For a more detailed example, see the [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in the [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="d1663-151">Дополнительные сведения о доступе к веб-службе машинного обучения см. в статье [Как использовать веб-службу машинного обучения Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="d1663-151">For more information on accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

