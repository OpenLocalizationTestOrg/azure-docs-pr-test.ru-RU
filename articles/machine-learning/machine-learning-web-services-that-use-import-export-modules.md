---
title: "aaaUsing импорта и экспорта данных в веб-службы машинного обучения Azure | Документы Microsoft"
description: "Узнайте, как toouse hello toosend модули данных импорта и экспорта данных и получать данные из веб-службы."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="b47e5-103">Развертывание веб-служб машинного обучения Azure, использующих модули импорта и экспорта данных</span><span class="sxs-lookup"><span data-stu-id="b47e5-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="b47e5-104">При создании прогнозного эксперимента обычно добавляются вход и выход веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b47e5-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="b47e5-105">При развертывании hello эксперимент, потребители могут отправки и получения данных из веб-службу hello hello входы и выходы.</span><span class="sxs-lookup"><span data-stu-id="b47e5-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="b47e5-106">В некоторых приложениях данные пользователя могут быть доступны через веб-канал данных или уже находиться во внешнем источнике данных, таком как хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="b47e5-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="b47e5-107">В этих случаях для чтения и записи данных им не требуются входы и выходы веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b47e5-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="b47e5-108">Они могут, вместо этого использовать hello пакетного выполнения службы (BES) tooread данные из источника данных hello модуль импорта данных с помощью и записи hello оценки результатов tooa расположения различных данных, с помощью модуль экспорта данных.</span><span class="sxs-lookup"><span data-stu-id="b47e5-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="b47e5-109">Hello данных импорта и экспорта данных модулей, можно считывающие и записывающие toovarious данные, которые предоставляют местоположения, такие как URL-адрес через HTTP, запрос Hive, база данных Azure SQL, хранилище таблиц Azure, хранилище больших двоичных объектов Azure, веб-канала данных или из локальной базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b47e5-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="b47e5-110">Hello в этом разделе используется «пример 5: обучение теста оценки для двоичной классификации: для взрослых набора данных» образец и предполагает hello набора данных в таблице Azure SQL с именем censusdata уже загружен.</span><span class="sxs-lookup"><span data-stu-id="b47e5-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="b47e5-111">Создание эксперимента обучения hello</span><span class="sxs-lookup"><span data-stu-id="b47e5-111">Create hello training experiment</span></span>
<span data-ttu-id="b47e5-112">При открытии hello «пример 5: обучение теста оценки для двоичной классификации: для взрослых набора данных» образец он использует образец hello двоичной классификации для взрослых переписи доход, набора данных.</span><span class="sxs-lookup"><span data-stu-id="b47e5-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="b47e5-113">И эксперимента hello hello визуальный элемент будет выглядеть аналогично toohello после изображения.</span><span class="sxs-lookup"><span data-stu-id="b47e5-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![Первоначальная настройка hello эксперимента.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="b47e5-115">tooread hello данные из таблицы hello Azure SQL:</span><span class="sxs-lookup"><span data-stu-id="b47e5-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="b47e5-116">Удалите модуль hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="b47e5-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="b47e5-117">В поле поиска hello компонентов введите импорта.</span><span class="sxs-lookup"><span data-stu-id="b47e5-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="b47e5-118">Из списка результатов hello, добавьте *импорта данных* toohello модуль поэкспериментировать холста.</span><span class="sxs-lookup"><span data-stu-id="b47e5-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="b47e5-119">Подсоедините выход hello *импорта данных* входные данные модуля hello объекта hello *Очистка недостающих данных* модуля.</span><span class="sxs-lookup"><span data-stu-id="b47e5-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="b47e5-120">В панели «Свойства» выберите **базы данных SQL Azure** в hello **источника данных** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="b47e5-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="b47e5-121">В hello **имя сервера базы данных**, **имя базы данных**, **имя пользователя**, и **пароль** введите соответствующую информацию hello для базы данных.</span><span class="sxs-lookup"><span data-stu-id="b47e5-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="b47e5-122">В поле запроса hello базы данных введите приветствия при следующем запросе.</span><span class="sxs-lookup"><span data-stu-id="b47e5-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="b47e5-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="b47e5-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="b47e5-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="b47e5-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="b47e5-125">Внизу hello холст эксперимента hello, нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="b47e5-126">Создание прогнозирующего эксперимента hello</span><span class="sxs-lookup"><span data-stu-id="b47e5-126">Create hello predictive experiment</span></span>
<span data-ttu-id="b47e5-127">Далее настройте hello прогнозной эксперимент, из которого развернуть веб-службу.</span><span class="sxs-lookup"><span data-stu-id="b47e5-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="b47e5-128">Внизу hello холст эксперимента hello, нажмите кнопку **настройки веб-службы** и выберите **прогнозной веб-службы (рекомендуется)**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="b47e5-129">Удалите hello *входных данных для службы Web* и *Вывод службы веб-модули* из эксперимента прогнозной hello.</span><span class="sxs-lookup"><span data-stu-id="b47e5-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="b47e5-130">В поле поиска hello компонентов введите экспорта.</span><span class="sxs-lookup"><span data-stu-id="b47e5-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="b47e5-131">Из списка результатов hello, добавьте *Экспорт данных* toohello модуль поэкспериментировать холста.</span><span class="sxs-lookup"><span data-stu-id="b47e5-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="b47e5-132">Подсоедините выход hello *модель оценки* входные данные модуля hello объекта hello *Экспорт данных* модуля.</span><span class="sxs-lookup"><span data-stu-id="b47e5-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="b47e5-133">В панели «Свойства» выберите **базы данных SQL Azure** в раскрывающемся списке целевой данных hello.</span><span class="sxs-lookup"><span data-stu-id="b47e5-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="b47e5-134">В hello **имя сервера базы данных**, **имя базы данных**, **имя учетной записи пользователя сервера**, и **пароль учетной записи пользователя сервера** введите Hello соответствующие сведения для базы данных.</span><span class="sxs-lookup"><span data-stu-id="b47e5-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="b47e5-135">В hello **разделенный запятыми список столбцов toobe Сохранить** введите меток оцененных значений.</span><span class="sxs-lookup"><span data-stu-id="b47e5-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="b47e5-136">В hello **поле имя таблицы данных**, введите dbo. ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="b47e5-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="b47e5-137">Если таблица hello не существует, оно создается при запуске эксперимента hello или hello веб-служба вызывается.</span><span class="sxs-lookup"><span data-stu-id="b47e5-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="b47e5-138">В hello **разделенный запятыми список столбцов таблицы данных** введите ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="b47e5-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="b47e5-139">При написании приложения, что вызовы hello окончательного веб-службы, вы можете toospecify другой входной запрос или целевой таблице во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="b47e5-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="b47e5-140">tooconfigure эти входы и выходы, использовать hello параметры веб-службы компонент tooset hello *импорта данных* модуль *источника данных* свойство и hello *Экспорт данных* режим свойство данных назначения.</span><span class="sxs-lookup"><span data-stu-id="b47e5-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="b47e5-141">Дополнительные сведения о параметры веб-службы см. в разделе hello [входа параметры веб-службы AzureML](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) по hello Cortana аналитики и обучения машины.</span><span class="sxs-lookup"><span data-stu-id="b47e5-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="b47e5-142">hello tooconfigure параметры веб-службы для запроса импорта hello и hello целевую таблицу:</span><span class="sxs-lookup"><span data-stu-id="b47e5-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="b47e5-143">На панели свойств hello для hello *импорта данных* модуля, нажмите значок hello в hello верхнему правому углу hello **запроса базы данных** и выберите **задать в качестве параметра веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="b47e5-144">На панели свойств hello для hello *Экспорт данных* модуля, нажмите значок hello в hello верхнему правому углу hello **имя таблицы данных** и выберите **задать в качестве параметра веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="b47e5-145">Внизу hello hello *Экспорт данных* модуль «свойства» в hello **параметры веб-службы** щелкните запрос базы данных и переименуйте его в запросе.</span><span class="sxs-lookup"><span data-stu-id="b47e5-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="b47e5-146">Щелкните **Имя таблицы данных** и измените его имя на **Таблица**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="b47e5-147">Когда вы закончите, эксперимента должен выглядеть примерно toohello после изображения:</span><span class="sxs-lookup"><span data-stu-id="b47e5-147">When you are done, your experiment should look similar toohello following image:</span></span>

![Окончательный вид эксперимента.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="b47e5-149">Теперь можно развернуть hello эксперимент как веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b47e5-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="b47e5-150">Развернуть веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="b47e5-150">Deploy hello web service</span></span>
<span data-ttu-id="b47e5-151">Вы можете развернуть tooeither классический или создать веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b47e5-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="b47e5-152">Развертывание классической веб-службы</span><span class="sxs-lookup"><span data-stu-id="b47e5-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="b47e5-153">toodeploy классического веб-службы и создать приложение tooconsume его:</span><span class="sxs-lookup"><span data-stu-id="b47e5-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="b47e5-154">Внизу hello холст эксперимента hello нажмите кнопку "Выполнить".</span><span class="sxs-lookup"><span data-stu-id="b47e5-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="b47e5-155">После завершения выполнения hello щелкните **развертывание веб-службы** и выберите **развертывание веб-службы [классический]**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="b47e5-156">Найдите свой ключ API на hello мониторинга веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b47e5-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="b47e5-157">Скопируйте и сохраните его toouse позже.</span><span class="sxs-lookup"><span data-stu-id="b47e5-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="b47e5-158">В hello **конечной точки по умолчанию** щелкните hello **Пакетное выполнение** hello tooopen ссылку API справочную страницу.</span><span class="sxs-lookup"><span data-stu-id="b47e5-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="b47e5-159">В Visual Studio создайте консольное приложение C# в Visual Studio (**Создать** > **Проект** > **Visual C#** > **Классический рабочий стол Windows** > **Консольное приложение (.NET Framework**).</span><span class="sxs-lookup"><span data-stu-id="b47e5-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="b47e5-160">Найдите на hello API справочная страница hello **образец кода** раздел hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="b47e5-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="b47e5-161">Скопируйте и вставьте hello образца кода на C# в файле Program.cs удаление хранилища больших двоичных объектов toohello все ссылки.</span><span class="sxs-lookup"><span data-stu-id="b47e5-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="b47e5-162">Обновите значение hello hello *apiKey* переменных с ключом hello API, сохраненный ранее.</span><span class="sxs-lookup"><span data-stu-id="b47e5-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="b47e5-163">Найдите hello запроса объявления и обновление hello значения параметры веб-службы, переданные toohello *импорта данных* и *Экспорт данных* модулей.</span><span class="sxs-lookup"><span data-stu-id="b47e5-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="b47e5-164">В этом случае используйте hello исходный запрос, но определить новое имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="b47e5-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="b47e5-165">Запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b47e5-165">Run hello application.</span></span> 

<span data-ttu-id="b47e5-166">По завершении выполнения hello новая таблица добавляется toohello базы данных, содержащей hello оценки результатов.</span><span class="sxs-lookup"><span data-stu-id="b47e5-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="b47e5-167">Развертывание новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="b47e5-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="b47e5-168">toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки вы развертывание hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b47e5-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="b47e5-169">Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="b47e5-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="b47e5-170">toodeploy как веб-службу и создания приложения tooconsume его:</span><span class="sxs-lookup"><span data-stu-id="b47e5-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="b47e5-171">Внизу hello холст эксперимента hello, нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="b47e5-172">После завершения выполнения hello щелкните **развертывание веб-службы** и выберите **развертывания [новое] веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="b47e5-173">На странице развертывание эксперимента hello, введите имя веб-службы и выбрать ценовой план, а затем нажмите кнопку **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="b47e5-174">На hello **краткое руководство** щелкните **использование**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="b47e5-175">В hello **образец кода** щелкните **пакета**.</span><span class="sxs-lookup"><span data-stu-id="b47e5-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="b47e5-176">В Visual Studio создайте консольное приложение C# в Visual Studio (**Создать** > **Проект** > **Visual C#** > **Классический рабочий стол Windows** > **Консольное приложение (.NET Framework**).</span><span class="sxs-lookup"><span data-stu-id="b47e5-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="b47e5-177">Скопируйте и вставьте образец кода C# hello в файле Program.cs.</span><span class="sxs-lookup"><span data-stu-id="b47e5-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="b47e5-178">Обновите значение hello hello *apiKey* переменных с hello **первичного ключа** в hello **потребления основные сведения о** раздела.</span><span class="sxs-lookup"><span data-stu-id="b47e5-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="b47e5-179">Найдите hello *scoreRequest* объявления и обновления значения hello параметры веб-службы, переданные toohello *импорта данных* и *Экспорт данных* модулей.</span><span class="sxs-lookup"><span data-stu-id="b47e5-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="b47e5-180">В этом случае используйте hello исходный запрос, но определить новое имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="b47e5-180">In this case, you use hello original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="b47e5-181">Запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b47e5-181">Run hello application.</span></span> 

