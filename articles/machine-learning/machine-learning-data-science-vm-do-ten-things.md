---
title: "Виртуальная машина анализа данных hello aaaTen вы можете делать на | Документы Microsoft"
description: "Выполните различные задачи моделирования и просмотра данных для обработки и анализа данных hello виртуальной машины."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a><span data-ttu-id="292c5-103">Десять фактов, которые можно выполнять на обработки и анализа данных hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="292c5-103">Ten things you can do on hello Data science Virtual Machine</span></span>
<span data-ttu-id="292c5-104">Hello виртуальной машины обработки и анализа данных Microsoft (DSVM) — это среда разработки обработки и анализа данных, позволяющий вы tooperform различные задачи и моделирование данных.</span><span class="sxs-lookup"><span data-stu-id="292c5-104">hello Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you tooperform various data exploration and modeling tasks.</span></span> <span data-ttu-id="292c5-105">Hello среда поставляется уже встроенного и распространение популярных данными средства аналитики, которые позволяют легко tooget быстро начать работу с анализа для локальной, облака и гибридной развертываний.</span><span class="sxs-lookup"><span data-stu-id="292c5-105">hello environment comes already built and bundled with several popular data analytics tools that make it easy tooget started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="292c5-106">Hello DSVM работает в тесном сотрудничестве с множество служб Azure и могут tooread и обработки данных, который уже хранится в Azure, в хранилище данных SQL Azure, Озера данных Azure, хранилище Azure или в базе данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="292c5-106">hello DSVM works closely with many Azure services and is able tooread and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="292c5-107">Она также может использовать другие инструменты аналитики, такие как машинное обучение Azure и фабрика данных Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="292c5-108">В этой статье мы рассмотрим как toouse вашей tooperform DSVM задачи обработки и анализа различных данных, а также взаимодействовать с другими службами Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-108">In this article we walk you through how toouse your DSVM tooperform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="292c5-109">Ниже приведены некоторые hello вещей, которые можно выполнять на hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="292c5-109">Here are some of hello things you can do on hello DSVM:</span></span>

1. <span data-ttu-id="292c5-110">Просмотр данных и разработки моделей локально на hello DSVM, с помощью Microsoft R Server Python</span><span class="sxs-lookup"><span data-stu-id="292c5-110">Explore data and develop models locally on hello DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="292c5-111">Использовать tooexperiment записной книжки Jupyter с данными в браузере, с помощью Python 2, Python 3 Microsoft R готовы версия enterprise R обеспечивает масштабируемость и производительность</span><span class="sxs-lookup"><span data-stu-id="292c5-111">Use a Jupyter notebook tooexperiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="292c5-112">Ввод моделей, построенных с помощью R и Python, в эксплуатацию в службе машинного обучения Azure, чтобы клиентские приложения могли обращаться к ним с использованием простого интерфейса веб-служб</span><span class="sxs-lookup"><span data-stu-id="292c5-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="292c5-113">Администрирование ресурсов Azure с помощью портала Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="292c5-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="292c5-114">Увеличение объема хранилища и предоставление всем членам команды общего доступа к большим наборам данных и коду за счет создания файлового хранилища Azure в виде подключаемого диска в DSVM.</span><span class="sxs-lookup"><span data-stu-id="292c5-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="292c5-115">Совместное использование кода с коллегами с помощью GitHub и доступа в репозиторий, пользуясь hello предварительно установленные клиенты Git - Git Bash Git графического интерфейса пользователя.</span><span class="sxs-lookup"><span data-stu-id="292c5-115">Share code with your team using GitHub and access your repository using hello pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="292c5-116">Доступ к различным службам данных и службам аналитики Azure, таким как хранилище BLOB-объектов, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, хранилище данных SQL Azure и базы данных Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="292c5-117">Создавать отчеты и панели мониторинга с помощью Power BI Desktop, предустановленные на hello DSVM hello и развертывать их в облаке hello</span><span class="sxs-lookup"><span data-stu-id="292c5-117">Build reports and dashboard using hello Power BI Desktop pre-installed on hello DSVM and deploy them on hello cloud</span></span>
9. <span data-ttu-id="292c5-118">Динамически масштабировать ваш toomeet DSVM, необходимые для проекта</span><span class="sxs-lookup"><span data-stu-id="292c5-118">Dynamically scale your DSVM toomeet your project needs</span></span>
10. <span data-ttu-id="292c5-119">Установка дополнительных инструментов на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="292c5-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="292c5-120">Взимается плата за использование дополнительных для многих hello дополнительные данные хранилища и аналитика служб, перечисленных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="292c5-120">Additional usage charges apply for many of hello additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="292c5-121">См. toohello [цены Azure](https://azure.microsoft.com/pricing/) для получения подробной информации.</span><span class="sxs-lookup"><span data-stu-id="292c5-121">Please refer toohello [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="292c5-122">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="292c5-122">**Prerequisites**</span></span>

* <span data-ttu-id="292c5-123">Вам понадобится подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-123">You need an Azure subscription.</span></span> <span data-ttu-id="292c5-124">Вы можете зарегистрироваться [здесь](https://azure.microsoft.com/free/), чтобы получить бесплатную пробную версию.</span><span class="sxs-lookup"><span data-stu-id="292c5-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="292c5-125">Инструкции по подготовке виртуальная машина анализа данных на hello портал Azure можно найти по адресу [создания виртуальной машины](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="292c5-125">Instructions for provisioning a Data Science Virtual Machine on hello Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="292c5-126">1. Просмотр данных и разработка моделей с помощью Microsoft R Server или Python</span><span class="sxs-lookup"><span data-stu-id="292c5-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="292c5-127">Аналитики данных языками, такими как toodo R и Python можно использовать на hello DSVM вправо.</span><span class="sxs-lookup"><span data-stu-id="292c5-127">You can use languages like R and Python toodo your data analytics right on hello DSVM.</span></span>

<span data-ttu-id="292c5-128">Для R можно использовать Интегрированную называется «Revolution R Enterprise 8.0», можно найти в меню "Пуск" hello "или" hello рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="292c5-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on hello start menu or hello desktop.</span></span> <span data-ttu-id="292c5-129">Корпорация Майкрософт предоставляет дополнительные библиотеки hello откройте источник/CRAN-R tooenable масштабируемой аналитики и hello возможность tooanalyze данных больше, чем размер памяти hello, выполнив параллельной фрагментированный анализа.</span><span class="sxs-lookup"><span data-stu-id="292c5-129">Microsoft has provided additional libraries on top of hello Open source/CRAN-R tooenable scalable analytics and hello ability tooanalyze data larger than hello memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="292c5-130">Вы можете установить любую другую интегрированную среду разработки R, например [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="292c5-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="292c5-131">Для Python можно использовать интегрированную среду разработки, как Visual Studio Community Edition, имеющая hello средства Python для предварительно установленной расширения Visual Studio (PTVS).</span><span class="sxs-lookup"><span data-stu-id="292c5-131">For Python, you can use an IDE like Visual Studio Community Edition which has hello Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="292c5-132">По умолчанию в PTVS настроена только базовая версия Python 2.7 (без аналитических библиотек, таких как SciKit, Pandas).</span><span class="sxs-lookup"><span data-stu-id="292c5-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="292c5-133">В порядке tooenable Anaconda Python 2.7 и 3.5 необходимо toodo hello следующее:</span><span class="sxs-lookup"><span data-stu-id="292c5-133">In order tooenable Anaconda Python 2.7 and 3.5, you need toodo hello following:</span></span>

* <span data-ttu-id="292c5-134">Создание пользовательских средах для каждой версии, перейдя по слишком**средства** -> **средства Python** -> **среды Python** и выбрав команду " **+ Настраиваемый**«в Visual Studio 2015 Community Edition hello</span><span class="sxs-lookup"><span data-stu-id="292c5-134">Create custom environments for each version by navigating too**Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in hello Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="292c5-135">Укажите описание и префикс пути, как задавать hello среды *c:\anaconda* Anaconda Python 2.7 или *c:\anaconda\envs\py35* Anaconda Python 3.5</span><span class="sxs-lookup"><span data-stu-id="292c5-135">Give a description and set hello environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="292c5-136">Нажмите кнопку **автоопределение** и затем **применить** toosave hello среды.</span><span class="sxs-lookup"><span data-stu-id="292c5-136">Click **Auto Detect** and then **Apply** toosave hello environment.</span></span>

<span data-ttu-id="292c5-137">Вот какие настройки нестандартной среды hello, выглядит как в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="292c5-137">Here is what hello custom environment setup looks like in Visual Studio.</span></span>

![Установка PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="292c5-139">В разделе hello [PTVS документации](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) Дополнительные сведения о том, как toocreate среды Python.</span><span class="sxs-lookup"><span data-stu-id="292c5-139">See hello [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how toocreate Python Environments.</span></span>

<span data-ttu-id="292c5-140">Теперь вы настраиваются toocreate новый проект Python.</span><span class="sxs-lookup"><span data-stu-id="292c5-140">Now you are set up toocreate a new Python project.</span></span> <span data-ttu-id="292c5-141">Перейдите в слишком**файл** -> **New** -> **проекта** -> **Python** и выберите тип hello Приложения Python, в которой выполняется сборка.</span><span class="sxs-lookup"><span data-stu-id="292c5-141">Navigate too**File** -> **New** -> **Project** -> **Python** and select hello type of Python application you are building.</span></span> <span data-ttu-id="292c5-142">Можно установить среду Python hello hello текущего проекта toohello нужную версию (Anaconda 2.7 или 3.5): щелкните правой кнопкой мыши hello **среды Python**выберите **Установка и удаление среды Python**, и затем выберите hello требуемого tooassociate среды с проектом hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-142">You can set hello Python environment for hello current project toohello desired version (Anaconda 2.7 or 3.5): right-click hello **Python environment**, select **Add/Remove Python Environments**, and then select hello desired environment tooassociate with hello project.</span></span> <span data-ttu-id="292c5-143">Дополнительные сведения о работе с PTVS на hello продукта можно найти [документации](https://github.com/Microsoft/PTVS/wiki) страницы.</span><span class="sxs-lookup"><span data-stu-id="292c5-143">You can find more information about working with PTVS on hello product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="292c5-144">2. С помощью tooexplore книжке Jupyter и модели данных с помощью Python или R</span><span class="sxs-lookup"><span data-stu-id="292c5-144">2. Using a Jupyter Notebook tooexplore and model your data with Python or R</span></span>
<span data-ttu-id="292c5-145">Hello книжке Jupyter — мощная среда, которая предоставляет браузера «интегрированной среды разработки» для моделирования и просмотра данных.</span><span class="sxs-lookup"><span data-stu-id="292c5-145">hello Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="292c5-146">Python 2, Python 3 или R (открытым исходным кодом и hello Microsoft R Server) можно использовать в записной книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="292c5-146">You can use Python 2, Python 3 or R (both Open Source and hello Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="292c5-147">hello toolaunch книжке Jupyter щелкните значок меню Пуск hello / значка на рабочем столе под названием **книжке Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="292c5-147">toolaunch hello Jupyter Notebook click on hello start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="292c5-148">На hello DSVM можно также просмотреть слишком "https://localhost:9999 /» tooaccess hello Юпитер ноутбука.</span><span class="sxs-lookup"><span data-stu-id="292c5-148">On hello DSVM you can also browse too"https://localhost:9999/" tooaccess hello Jupiter Notebook.</span></span> <span data-ttu-id="292c5-149">Если предлагается ввести пароль, используйте инструкции, приведенные в hello ***как toocreate надежный пароль на сервере записной книжки Jupyter hello*** раздел hello [подготовки hello виртуальная машина Microsoft данных анализа](machine-learning-data-science-provision-vm.md)toocreate разделе записной книжке Jupyter hello tooaccess надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="292c5-149">If it prompts you for a password, use instructions provided in hello ***How toocreate a strong password on hello Jupyter notebook server*** section of hello [Provision hello Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic toocreate a strong password tooaccess hello Jupyter notebook.</span></span> 

<span data-ttu-id="292c5-150">После открытия записной книжки hello, вы увидите, что каталог, содержащий несколько записных книжек пример, предварительно упакованные в hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="292c5-150">Once you have opened hello notebook, you should see a directory that contains a few example notebooks that are pre-packaged into hello DSVM.</span></span> <span data-ttu-id="292c5-151">Теперь вы можете:</span><span class="sxs-lookup"><span data-stu-id="292c5-151">Now you can:</span></span>

* <span data-ttu-id="292c5-152">Щелкните кода hello toosee записной книжки hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-152">click on hello notebook toosee hello code.</span></span>
* <span data-ttu-id="292c5-153">выполнить каждую ячейку нажатием сочетания клавиш **SHIFT + ВВОД**;</span><span class="sxs-lookup"><span data-stu-id="292c5-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="292c5-154">Запустите всей записной книжки hello, щелкнув **ячейки** -> **запуска**</span><span class="sxs-lookup"><span data-stu-id="292c5-154">run hello entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="292c5-155">создать новую, щелкнув значок Jupyter (левый верхний угол) hello и выбрав **New** кнопки hello справа и выбрав язык hello записной книжки (также известный как ядер).</span><span class="sxs-lookup"><span data-stu-id="292c5-155">create a new notebook by clicking on hello Jupyter Icon (left top corner) and then clicking **New** button on hello right and then choosing hello notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="292c5-156">В настоящее время мы поддерживаем Python 2.7, Python 3.5 и R. ядра hello R поддерживает программирование в R с открытым кодом как, так и hello enterprise масштабируемой Microsoft R Server.</span><span class="sxs-lookup"><span data-stu-id="292c5-156">Currently we support Python 2.7, Python 3.5 and R. hello R kernel supports programming in both Open source R as well as hello enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="292c5-157">После входа в записной книжке hello можно исследовать данные, построена модель hello, проверка hello модели на любом из библиотек.</span><span class="sxs-lookup"><span data-stu-id="292c5-157">Once you are in hello notebook you can explore your data, build hello model, test hello model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="292c5-158">3. Создание моделей с помощью R или Python и их ввод в эксплуатацию с помощью машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="292c5-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="292c5-159">После создания и проверки модели hello следующим шагом обычно является toodeploy его в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="292c5-159">Once you have built and validated your model hello next step is usually toodeploy it into production.</span></span> <span data-ttu-id="292c5-160">Это позволяет клиентских приложений tooinvoke hello модели прогнозов в реальном времени или на основе пакетного режима.</span><span class="sxs-lookup"><span data-stu-id="292c5-160">This allows your client applications tooinvoke hello model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="292c5-161">Машинное обучение Azure предоставляет toooperationalize механизм модель, встроенных в R или Python.</span><span class="sxs-lookup"><span data-stu-id="292c5-161">Azure Machine Learning provides a mechanism toooperationalize a model built in either R or Python.</span></span>

<span data-ttu-id="292c5-162">После ввода в эксплуатацию модели в машинном обучении Azure предоставляется веб-службы, позволяющую клиентам toomake вызовы REST, которые передачи входных параметров и получения прогнозов из модели hello как выходные данные.</span><span class="sxs-lookup"><span data-stu-id="292c5-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients toomake REST calls that pass in input parameters and receive predictions from hello model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="292c5-163">Если вы еще не еще зарегистрировались для машинного обучения Azure, можно получить бесплатную рабочую область или стандартной рабочей области, перейдя по адресу hello [студии машинного обучения Azure](https://studio.azureml.net/) домашнюю страницу и щелкните на «Приступая к работе».</span><span class="sxs-lookup"><span data-stu-id="292c5-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="292c5-164">Создание и ввод в эксплуатацию моделей Python</span><span class="sxs-lookup"><span data-stu-id="292c5-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="292c5-165">Ниже приведен фрагмент кода, разработанного в записной книжке Jupyter Python, создающий простой модели с помощью библиотеки узнать SciKit hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using hello SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="292c5-166">метод Hello используется toodeploy вашей tooAzure моделей python прогноза hello качестве оболочки для машинного обучения модели hello в функцию и оформляет его с атрибутами, предоставляемые библиотекой hello предустановленных машинного обучения Azure python, указывающих на машине Azure Идентификатор рабочей области обучения, ключ API и hello входные и выходные параметры.</span><span class="sxs-lookup"><span data-stu-id="292c5-166">hello method used toodeploy your python models tooAzure Machine Learning wraps hello prediction of hello model into a function and decorates it with attributes provided by hello pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and hello input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="292c5-167">Клиенту теперь можно выполнять вызовы toohello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="292c5-167">A client can now make calls toohello web service.</span></span> <span data-ttu-id="292c5-168">Существуют удобства оболочек, создания запросов REST API hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-168">There are convenience wrappers that construct hello REST API requests.</span></span> <span data-ttu-id="292c5-169">Ниже приведен пример кода tooconsume hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="292c5-169">Here is a sample code tooconsume hello web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="292c5-170">Библиотека машинного обучения Azure Hello поддерживается только на Python 2.7 в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="292c5-170">hello Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="292c5-171">Создание и ввод в эксплуатацию моделей R</span><span class="sxs-lookup"><span data-stu-id="292c5-171">Build and Operationalize R models</span></span>
<span data-ttu-id="292c5-172">Вы можете развернуть R моделях, основанных на hello виртуальная машина анализа данных, или в другом месте на машинного обучения Azure в режиме, аналогичные toohow, который выполняется для Python.</span><span class="sxs-lookup"><span data-stu-id="292c5-172">You can deploy R models built on hello Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar toohow it is done for Python.</span></span> <span data-ttu-id="292c5-173">Ее hello шагов:</span><span class="sxs-lookup"><span data-stu-id="292c5-173">Her are hello steps:</span></span>

* <span data-ttu-id="292c5-174">Создайте tooprovide файл settings.json, идентификатор рабочей области и проверки подлинности маркера, как показано в следующий образец кода hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-174">create a settings.json file tooprovide your workspace ID and auth token as shown in hello following code sample.</span></span>
* <span data-ttu-id="292c5-175">записать оболочку для функции прогнозирования hello модели.</span><span class="sxs-lookup"><span data-stu-id="292c5-175">write a wrapper for hello model's predict function.</span></span>
* <span data-ttu-id="292c5-176">Вызовите ```publishWebService``` в hello toopass библиотеки машинного обучения Azure в оболочку функции hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-176">call ```publishWebService``` in hello Azure Machine Learning library toopass in hello function wrapper.</span></span>  

<span data-ttu-id="292c5-177">Вот hello процедуры и фрагменты кода, может быть используется tooset вверх, построения, публиковать и использовать модель веб-службы в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-177">Here is hello procedure and code snippets that can be used tooset up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="292c5-178">Настройка</span><span class="sxs-lookup"><span data-stu-id="292c5-178">Setup</span></span>
1. <span data-ttu-id="292c5-179">Установить пакет R обучения машины hello, введя ```install.packages("AzureML")``` в Revolution R Enterprise 8.0 IDE или R интерфейс IDE.</span><span class="sxs-lookup"><span data-stu-id="292c5-179">Install hello Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="292c5-180">Загрузите RTools [отсюда](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="292c5-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="292c5-181">Требуется программа hello пути (и именованные zip.exe) toooperationalize hello zip R-пакет в машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="292c5-181">You need hello zip utility in hello path (and named zip.exe) toooperationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="292c5-182">Создайте файл settings.json каталог с именем ```.azureml``` в домашнем каталоге и введите параметры hello в рабочей области машинного обучения Azure:</span><span class="sxs-lookup"><span data-stu-id="292c5-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter hello parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="292c5-183">структура файла Settings.json:</span><span class="sxs-lookup"><span data-stu-id="292c5-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="292c5-184">Создание модели на языке R и ее публикация в службе машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="292c5-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="292c5-185">Работать с моделью hello, развернутых в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="292c5-185">Consume hello model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="292c5-186">tooconsume hello модели из клиентских приложений, мы используем toolook библиотеки машинного обучения Azure hello копирование hello опубликованных веб-службы по имени, используя hello `services` конечной hello toodetermine вызовов API.</span><span class="sxs-lookup"><span data-stu-id="292c5-186">tooconsume hello model from a client application, we use hello Azure Machine Learning library toolook up hello published web service by name using hello `services` API call toodetermine hello endpoint.</span></span> <span data-ttu-id="292c5-187">Затем нужно просто вызвать hello `consume` функции, а затем передать hello данных кадра toobe прогноз.</span><span class="sxs-lookup"><span data-stu-id="292c5-187">Then you just call hello `consume` function and pass in hello data frame toobe predicted.</span></span>
<span data-ttu-id="292c5-188">После кода Hello — модель используется tooconsume hello, опубликованы как веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-188">hello following code is used tooconsume hello model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="292c5-189">Дополнительные сведения о библиотеке hello Azure Machine Learning R можно найти [здесь](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="292c5-189">More information about hello Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="292c5-190">4. Администрирование ресурсов Azure с помощью портала Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="292c5-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="292c5-191">Hello DSVM позволяет не только вы toobuild решении analytics локально на hello виртуальной машины, но и обеспечивает службы tooaccess в облаке Azure корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="292c5-191">hello DSVM not only allows you toobuild your analytics solution locally on hello virtual machine, but also allows you tooaccess services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="292c5-192">Azure предоставляет несколько вычислительных служб, служб хранения данных и служб аналитики данных, а также ряд других служб, которые можно администрировать и к которым можно обращаться с DSVM.</span><span class="sxs-lookup"><span data-stu-id="292c5-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="292c5-193">tooadminister подписку и облачную ресурсами Azure можно использовать обозреватель и точки toothe [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="292c5-193">tooadminister your Azure subscription and cloud resources you can use your browser and point toothe [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="292c5-194">Также можно использовать Azure Powershell tooadminister подписка Azure и ресурсов через сценарий.</span><span class="sxs-lookup"><span data-stu-id="292c5-194">You can also use Azure Powershell tooadminister your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="292c5-195">Можно запустить Azure Powershell с помощью ярлыка на рабочем столе hello или из hello меню «Пуск» под названием «Microsoft Azure Powershell».</span><span class="sxs-lookup"><span data-stu-id="292c5-195">You can run Azure Powershell from a shortcut on hello desktop or from hello start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="292c5-196">Дополнительные сведения об администрировании подписки и ресурсов Azure с помощью сценариев Windows PowerShell см. в [документации по Microsoft Azure PowerShell](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="292c5-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="292c5-197">5. Увеличение объема хранилища за счет общей файловой системы</span><span class="sxs-lookup"><span data-stu-id="292c5-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="292c5-198">Специалисты по анализу данных могут совместно использовать большие наборы данных, кода или других ресурсов в команде hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-198">Data scientists can share large datasets, code or other resources within hello team.</span></span> <span data-ttu-id="292c5-199">Hello DSVM сам имеет примерно 70 ГБ доступного пространства.</span><span class="sxs-lookup"><span data-stu-id="292c5-199">hello DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="292c5-200">tooextend хранилища, можно использовать hello службы файлов Azure и подключить его на hello DSVM или получить к нему доступ через REST API.</span><span class="sxs-lookup"><span data-stu-id="292c5-200">tooextend your storage, you can use hello Azure File Service and either mount it on hello DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="292c5-201">Hello максимальное hello службы файлов Azure папки размером 5 ТБ и места максимальный размер отдельного файла составляет 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="292c5-201">hello maximum space of hello Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="292c5-202">Можно использовать Azure Powershell toocreate ресурс службы файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-202">You can use Azure Powershell toocreate an Azure File Service share.</span></span> <span data-ttu-id="292c5-203">Вот hello toorun сценарий в Azure PowerShell toocreate Azure файловый ресурс службы.</span><span class="sxs-lookup"><span data-stu-id="292c5-203">Here is hello script toorun under Azure PowerShell toocreate an Azure File service share.</span></span>

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="292c5-204">Созданную общую папку Azure можно подключить к любой виртуальной машине в Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="292c5-205">Настоятельно рекомендуется этого hello виртуальной Машины — в одном центре обработки данных Azure как задержка tooavoid учетной записи хранилища hello и данные передачи расходов.</span><span class="sxs-lookup"><span data-stu-id="292c5-205">It is highly recommended that hello VM is in same Azure data center as hello storage account tooavoid latency and data transfer charges.</span></span> <span data-ttu-id="292c5-206">Ниже приведены hello команды toomount hello диска на hello DSVM, который можно запустить в Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="292c5-206">Here are hello commands toomount hello drive on hello DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="292c5-207">Теперь можно использовать этот диск, как и любой обычный диск на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="292c5-207">Now you can access this drive as you would any normal drive on hello VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="292c5-208">6. Совместное использование кода командой с помощью GitHub</span><span class="sxs-lookup"><span data-stu-id="292c5-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="292c5-209">GitHub — это хранилище кода, где можно найти много примеров кода и источники для различных средств, с использованием различных технологий, совместно с сообществом разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by hello developer community.</span></span> <span data-ttu-id="292c5-210">Она использует Git, как hello технологию tootrack и хранилище версий файлов кода hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-210">It uses Git as hello technology tootrack and store versions of hello code files.</span></span> <span data-ttu-id="292c5-211">GitHub также является платформой которого можно создать собственный репозиторий toostore общего кода и документации, команды реализовать систему управления версиями, а также элемент управления, обладающих доступом tooview и добавлять код.</span><span class="sxs-lookup"><span data-stu-id="292c5-211">GitHub is also a platform where you can create your own repository toostore your team's shared code and documentation, implement version control and also control who have access tooview and contribute code.</span></span> <span data-ttu-id="292c5-212">Перейдите на страницу приветствия [страниц справки GitHub](https://help.github.com/) Дополнительные сведения об использовании Git.</span><span class="sxs-lookup"><span data-stu-id="292c5-212">Please visit hello [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="292c5-213">Можно использовать GitHub как один из способов toocollaborate hello с другими участниками команды, используйте код, разработанный сообществом hello и участие сообщества задней toohello кода.</span><span class="sxs-lookup"><span data-stu-id="292c5-213">You can use GitHub as one of hello ways toocollaborate with your team, use code developed by hello community and contribute code back toohello community.</span></span>

<span data-ttu-id="292c5-214">Hello DSVM уже загружена клиентских средств на обоих командной строки как хорошо tooaccess графического интерфейса пользователя репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="292c5-214">hello DSVM already comes loaded with client tools on both command-line as well GUI tooaccess GitHub repository.</span></span> <span data-ttu-id="292c5-215">Hello toowork средство командной строки с Git и GitHub называется Git Bash.</span><span class="sxs-lookup"><span data-stu-id="292c5-215">hello command-line tool toowork with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="292c5-216">Visual Studio, установленной на hello DSVM имеет расширения hello Git.</span><span class="sxs-lookup"><span data-stu-id="292c5-216">Visual Studio installed on hello DSVM has hello Git extensions.</span></span> <span data-ttu-id="292c5-217">Можно найти при запуске значки для этих средств hello меню "Пуск" и рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-217">You can find start-up icons for these tools on hello start menu and hello desktop.</span></span>

<span data-ttu-id="292c5-218">toodownload кода из репозитория GitHub использовать hello ```git clone``` команды.</span><span class="sxs-lookup"><span data-stu-id="292c5-218">toodownload code from a GitHub repository you use hello ```git clone``` command.</span></span> <span data-ttu-id="292c5-219">Например репозитории обработки и анализа данных toodownload, опубликованные корпорацией Майкрософт в текущем каталоге hello можно запустить следующую команду, после входа в hello ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="292c5-219">For example toodownload data science repository published by Microsoft into hello current directory you can run hello following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="292c5-220">В Visual Studio можно выполнить hello же операции клонирования.</span><span class="sxs-lookup"><span data-stu-id="292c5-220">In Visual Studio, you can do hello same clone operation.</span></span> <span data-ttu-id="292c5-221">Следующий снимок экрана приветствия показано, как tooaccess Git и GitHub средства в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="292c5-221">hello  following screen-shot shows how tooaccess Git and GitHub tools in Visual Studio.</span></span>

![Git в Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="292c5-223">Можно найти дополнительные сведения об использовании своего репозитория GitHub из нескольких ресурсов, доступных в github.com Git toowork. Hello [памятку](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) является полезным ссылкой.</span><span class="sxs-lookup"><span data-stu-id="292c5-223">You can find more information on using Git toowork with your GitHub repository from several resources available on github.com. hello [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="292c5-224">7. Доступ к различным службам данных и службам аналитики Azure</span><span class="sxs-lookup"><span data-stu-id="292c5-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="292c5-225">Большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="292c5-225">Azure Blob</span></span>
<span data-ttu-id="292c5-226">Большой двоичный объект Azure является надежным и экономичным облачным хранилищем для больших и малых объемов данных.</span><span class="sxs-lookup"><span data-stu-id="292c5-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="292c5-227">Рассмотрим перенос tooAzure данных больших двоичных объектов и доступа к данным, хранящимся в BLOB-объект Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-227">Let us look at how you can move data tooAzure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="292c5-228">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="292c5-228">**Prerequisite**</span></span>

* <span data-ttu-id="292c5-229">**Создайте учетную запись хранения BLOB-объектов Azure на [портале Azure](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="292c5-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="292c5-231">Убедитесь, что hello средство AzCopy предустановленных командной строки найдено в ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="292c5-231">Confirm that hello pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="292c5-232">Можно добавить hello каталога содержащий hello azcopy.exe tooyour путь среды переменной tooavoid ввода hello полностью команда путь при запуске этого средства.</span><span class="sxs-lookup"><span data-stu-id="292c5-232">You can add hello directory containing hello azcopy.exe tooyour PATH environment variable tooavoid typing hello full command path when running this tool.</span></span> <span data-ttu-id="292c5-233">Дополнительные сведения о средство AzCopy см слишком[AzCopy документации](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="292c5-233">For more info on AzCopy tool please refer too[AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="292c5-234">Запустите средство hello обозреватель хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-234">Start hello Azure Storage Explorer tool.</span></span> <span data-ttu-id="292c5-235">Его можно скачать с сайта [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="292c5-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="292c5-237">**Перемещение данных из виртуальной Машины tooAzure больших двоичных объектов: AzCopy**</span><span class="sxs-lookup"><span data-stu-id="292c5-237">**Move data from VM tooAzure Blob: AzCopy**</span></span>

<span data-ttu-id="292c5-238">toomove данных между локальным файлам и хранилище больших двоичных объектов, можно использовать AzCopy в командной строки или PowerShell:</span><span class="sxs-lookup"><span data-stu-id="292c5-238">toomove data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="292c5-239">Замените **C:\myfolder** toohello путь, где хранится файл, **mystorageaccount** имя учетной записи хранилища больших двоичных объектов tooyour **mycontainer** toohello имя контейнера, **ключ учетной записи хранения** ключ доступа к хранилищу больших двоичных объектов tooyour.</span><span class="sxs-lookup"><span data-stu-id="292c5-239">Replace **C:\myfolder** toohello path where your file is stored, **mystorageaccount** tooyour blob storage account name, **mycontainer** toohello container name, **storage account key** tooyour blob storage access key.</span></span> <span data-ttu-id="292c5-240">Данные вашей учетной записи хранения находятся на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="292c5-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="292c5-242">Выполните команду AzCopy в PowerShell или из командной строки.</span><span class="sxs-lookup"><span data-stu-id="292c5-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="292c5-243">Далее приведен пример использования команды AzCopy.</span><span class="sxs-lookup"><span data-stu-id="292c5-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="292c5-244">После выполнения вашей tooan toocopy команды AzCopy BLOB-объектов Azure указан файл отображается в обозреватель хранилищ Azure скоро.</span><span class="sxs-lookup"><span data-stu-id="292c5-244">Once you run your AzCopy command toocopy tooan Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="292c5-246">**Перемещение данных из виртуальной Машины tooAzure больших двоичных объектов: Обозреватель хранилищ Azure**</span><span class="sxs-lookup"><span data-stu-id="292c5-246">**Move data from VM tooAzure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="292c5-247">Также можно передать данные из локального файла hello в ВМ с помощью обозревателя хранилищ Azure:</span><span class="sxs-lookup"><span data-stu-id="292c5-247">You can also upload data from hello local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="292c5-248">контейнер tooa tooupload данных, выберите hello целевой контейнер и нажмите кнопку hello **отправить** кнопки.![ Отправка в обозревателе хранилищ](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="292c5-248">tooupload data tooa container, select hello target container and click hello **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="292c5-249">Щелкните hello **...**  toohello справа от приветствия **файлы** , выберите один или несколько файлов tooupload hello файловой системе и нажмите кнопку **отправить** toobegin, передача файлов hello.![ Отправка файлов tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="292c5-249">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="292c5-250">**Чтение данных из большого двоичного объекта Azure: модуль "Читатель" машинного обучения**</span><span class="sxs-lookup"><span data-stu-id="292c5-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="292c5-251">В студии машинного обучения Azure можно использовать **модуль импорта данных** tooread данные из большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="292c5-251">In Azure Machine Learning Studio you can use an **Import Data module** tooread data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="292c5-253">**Чтение данных из BLOB-объекта Azure: Python ODBC**</span><span class="sxs-lookup"><span data-stu-id="292c5-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="292c5-254">Можно использовать **BlobService** библиотеки tooread данных непосредственно из большого двоичного объекта в программе книжке Jupyter или Python.</span><span class="sxs-lookup"><span data-stu-id="292c5-254">You can use **BlobService** library tooread data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="292c5-255">Сначала импортируйте необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="292c5-255">First, import required packages:</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

<span data-ttu-id="292c5-256">Затем подключите учетные данные BLOB-объекта Azure и считайте данные из BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="292c5-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="292c5-257">Hello данные считываются в виде блока данных:</span><span class="sxs-lookup"><span data-stu-id="292c5-257">hello data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="292c5-259">Озеро данных Azure</span><span class="sxs-lookup"><span data-stu-id="292c5-259">Azure Data Lake</span></span>
<span data-ttu-id="292c5-260">Хранилище Azure Data Lake является гипермасштабируемым репозиторием для рабочих нагрузок аналитической обработки больших данных, совместимым с распределенной файловой системой Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="292c5-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="292c5-261">Она работает с экосистемой Hadoop hello и hello аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-261">It works with both hello Hadoop ecosystem and hello Azure Data Lake Analytics.</span></span> <span data-ttu-id="292c5-262">Мы покажем, как можно переместить данные в хранилище Озера данных Azure hello и выполнить анализ с помощью аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-262">We show how you can move data into hello Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="292c5-263">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="292c5-263">**Prerequisite**</span></span>

* <span data-ttu-id="292c5-264">Создайте экземпляр Azure Data Lake Analytics на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="292c5-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="292c5-266">Hello **средства Озера данных Azure** в **Visual Studio** находится в следующей [ссылку](https://www.microsoft.com/download/details.aspx?id=49504) уже установлены на hello Visual Studio Community Edition, который находится на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-266">hello  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on hello Visual Studio Community Edition which is on hello virtual machine.</span></span> <span data-ttu-id="292c5-267">После запуска Visual Studio и ведения журнала в вашей подписке Azure, вы должны увидеть вашей учетной записи Azure анализа данных и хранения hello левой панели Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="292c5-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in hello left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="292c5-269">**Перемещение данных из виртуальной Машины tooData Озера: проводник Озера данных Azure**</span><span class="sxs-lookup"><span data-stu-id="292c5-269">**Move data from VM tooData Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="292c5-270">Можно использовать **обозреватель Озера данных Azure** tooupload данные из локальных файлов hello в хранилище Озера tooData виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="292c5-270">You can use **Azure Data Lake Explorer** tooupload data from hello local files in your Virtual Machine tooData Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="292c5-272">Можно также создать конвейер данных tooproductionize вашей tooor перемещения данных из Озера данных Azure с помощью hello [Factory(ADF) данных Azure](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="292c5-272">You can also build a data pipeline tooproductionize your data movement tooor from Azure Data Lake using hello [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="292c5-273">Мы называем toothis [статьи](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide можно выполнить с помощью данных hello toobuild действия hello конвейеров.</span><span class="sxs-lookup"><span data-stu-id="292c5-273">We refer you toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide you through hello steps toobuild hello data pipelines.</span></span>

<span data-ttu-id="292c5-274">**Чтение данных из Озера tooData больших двоичных объектов Azure: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="292c5-274">**Read data from Azure Blob tooData Lake: U-SQL**</span></span>

<span data-ttu-id="292c5-275">Если данные хранятся в хранилище BLOB-объектов Azure, их можно считывать непосредственно из BLOB-объекта хранилища Azure в запросе U-SQL.</span><span class="sxs-lookup"><span data-stu-id="292c5-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="292c5-276">Прежде чем составление U-SQL-запрос, убедитесь, что учетной записи хранилища BLOB-объектов — связанные tooyour Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-276">Before composing your U-SQL query, make sure your blob storage account is linked tooyour Azure Data Lake.</span></span> <span data-ttu-id="292c5-277">Go слишком**портал Azure**найти информационную панель аналитики Озера данных Azure, нажмите кнопку **добавить источник данных**, выберите тип хранения слишком**хранилища Azure** и подключите хранилище Azure Имя учетной записи и ключа.</span><span class="sxs-lookup"><span data-stu-id="292c5-277">Go too**Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type too**Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="292c5-278">Затем предпринимается может tooreference hello данные, хранящиеся в учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-278">Then you are able tooreference hello data stored in hello storage account.</span></span>

![Ввод имени учетной записи хранения и ключа](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="292c5-280">В Visual Studio можно считывать данные из хранилища больших двоичных объектов, сделать некоторые операции с данными, конструируются и вывод hello результирующие данные tooeither Озера данных Azure или хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="292c5-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output hello resulting data tooeither Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="292c5-281">При создании ссылок данных hello в хранилище больших двоичных объектов, используйте **wasb: / /**; при ссылке на hello данных Озера данных Azure, используйте **swbhdfs: / /**</span><span class="sxs-lookup"><span data-stu-id="292c5-281">When you reference hello data in blob storage, use **wasb://**; when you reference hello data in Azure Data Lake, use **swbhdfs://**</span></span>

![Кадр данных](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="292c5-283">Можно использовать следующие запросы U-SQL в Visual Studio hello:</span><span class="sxs-lookup"><span data-stu-id="292c5-283">You may use hello following U-SQL queries in Visual Studio:</span></span>

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="292c5-284">После запроса является отправленной toohello сервером, отображается диаграмма, показывающая hello состояние задания.</span><span class="sxs-lookup"><span data-stu-id="292c5-284">After your query is submitted toohello server, a diagram showing hello status of your job is displayed.</span></span>

![Схема состояния задания](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="292c5-286">**Запрос данных в озере данных: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="292c5-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="292c5-287">После набора данных hello полученный в Озера данных Azure, вы можете использовать [U-SQL языка](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery и изучать данные hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-287">After hello dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery and explore hello data.</span></span> <span data-ttu-id="292c5-288">U-SQL языка аналогичные tooT-SQL, но объединяет некоторые функции C# таким образом, чтобы пользователи могут записывать пользовательские модули, определяемых пользователем функций и и т. д. Можно использовать скрипты hello в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-288">U-SQL language is similar tooT-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use hello scripts in hello previous step.</span></span>

<span data-ttu-id="292c5-289">После запроса hello отправленной tooserver, tripdata_summary. CSV можно найти в скором времени **обозреватель Озера данных Azure**, может просмотреть данные hello, щелкните правой кнопкой мыши файл hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-289">After hello query is submitted tooserver, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview hello data by right-click hello file.</span></span>

![Файл в Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="292c5-291">сведения о файле hello toosee:</span><span class="sxs-lookup"><span data-stu-id="292c5-291">toosee hello file information:</span></span>

![Сведения о файле](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="292c5-293">Кластеры HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="292c5-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="292c5-294">Azure HDInsight является управляемой службой Apache Hadoop, Spark, HBase и Storm в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on hello cloud.</span></span> <span data-ttu-id="292c5-295">Легко можно работать с кластерами Azure HDInsight из виртуальная машина анализа данных hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-295">You can work easily with Azure HDInsight clusters from hello data science virtual machine.</span></span>

<span data-ttu-id="292c5-296">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="292c5-296">**Prerequisite**</span></span>

* <span data-ttu-id="292c5-297">Создайте учетную запись хранения BLOB-объектов Azure на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="292c5-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="292c5-298">Эта учетная запись хранения — используется toostore данные для кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="292c5-298">This storage account is used toostore data for HDInsight clusters.</span></span>

![Создание учетной записи хранения больших двоичных объектов Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="292c5-300">Настройте кластеры HDInsight Hadoop в Azure на [портале Azure](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="292c5-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="292c5-301">Необходимо связать учетную запись хранения hello, создан с кластером HDInsight, при его создании.</span><span class="sxs-lookup"><span data-stu-id="292c5-301">You must link hello storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="292c5-302">Эта учетная запись используется для доступа к данным, которое может быть обработано в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-302">This storage account is used for accessing data that can be processed within hello cluster.</span></span>

![Связать учетную запись toostorage создан с кластером HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="292c5-304">Необходимо включить **удаленного доступа** toohello головного узла кластера hello после его создания.</span><span class="sxs-lookup"><span data-stu-id="292c5-304">You must enable **Remote Access** toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="292c5-305">Запоминать учетные данные удаленного доступа hello, указанные здесь (отличающиеся от параметров, указанных для hello кластера при его создании): при необходимости в последующих процедурах hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-305">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them in hello subsequent procedure.</span></span>

![Включение удаленного доступа](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="292c5-307">Создайте рабочую область машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="292c5-308">В ней будут храниться эксперименты машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="292c5-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="292c5-309">Выберите параметры hello выделяются на портале, как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="292c5-309">Select hello highlighted options in Portal as shown in hello following screenshot:</span></span>

![Создание рабочей области машинного обучения Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="292c5-311">Затем введите параметры hello для рабочей области</span><span class="sxs-lookup"><span data-stu-id="292c5-311">Then enter hello parameters for your workspace</span></span>

![Ввод параметров рабочей области машинного обучения](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="292c5-313">Загрузите данные с помощью IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="292c5-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="292c5-314">Сначала импортируйте необходимые пакеты, подключите в учетных данных, создание базы данных в вашей учетной записи хранилища, а затем загрузить кластеры tooHDI данных.</span><span class="sxs-lookup"><span data-stu-id="292c5-314">First import required packages, plug in credentials, create a db in your storage account, then load data tooHDI clusters.</span></span>

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="292c5-315">Кроме того, можно использовать эту [Пошаговое руководство](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC такси данных tooHDI кластера.</span><span class="sxs-lookup"><span data-stu-id="292c5-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC Taxi data tooHDI cluster.</span></span> <span data-ttu-id="292c5-316">Ниже перечислены основные действия.</span><span class="sxs-lookup"><span data-stu-id="292c5-316">Major steps include:</span></span>
  
  * <span data-ttu-id="292c5-317">AzCopy: загрузите ZIP-CSV большой двоичный объект открытого tooyour локальной папке</span><span class="sxs-lookup"><span data-stu-id="292c5-317">AzCopy: download zipped CSV's from public blob tooyour local folder</span></span>
  * <span data-ttu-id="292c5-318">AzCopy: Отправка распакованную CSV из локальной папки tooHDI кластера</span><span class="sxs-lookup"><span data-stu-id="292c5-318">AzCopy: upload unzipped CSV's from local folder tooHDI cluster</span></span>
  * <span data-ttu-id="292c5-319">Войдите в hello головного узла кластера Hadoop и подготовка для исследовательского анализа</span><span class="sxs-lookup"><span data-stu-id="292c5-319">Log into hello head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="292c5-320">После загрузки tooHDI кластера hello данных можно проверить данные в обозреватель хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="292c5-320">After hello data is loaded tooHDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="292c5-321">Кроме того, в кластере HDI находится созданная база данных nyctaxidb.</span><span class="sxs-lookup"><span data-stu-id="292c5-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="292c5-322">**Просмотр данных: запросы Hive в Python**</span><span class="sxs-lookup"><span data-stu-id="292c5-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="292c5-323">Поскольку данные hello в кластере Hadoop, можно использовать hello pyodbc пакета tooconnect tooHadoop кластеров и с помощью просмотра toodo Hive и конструируются запрос к базе данных.</span><span class="sxs-lookup"><span data-stu-id="292c5-323">Since hello data is in Hadoop cluster, you can use hello pyodbc package tooconnect tooHadoop Clusters and query database using Hive toodo exploration and feature engineering.</span></span> <span data-ttu-id="292c5-324">Вы можете просмотреть hello существующие таблицы, созданной на шаге готовности hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-324">You can view hello existing tables we created in hello prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Просмотр имеющихся таблиц](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="292c5-326">Давайте рассмотрим hello количество записей в каждый месяц и hello частоты скошенные или отсутствует в таблице trip hello:</span><span class="sxs-lookup"><span data-stu-id="292c5-326">Let's look at hello number of records in each month and hello frequencies of tipped or not in hello trip table:</span></span>

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Диаграмма количества записей за каждый месяц](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Диаграмма частотности чаевых](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

<span data-ttu-id="292c5-329">Мы также вычислять hello расстояние между раскладки и расположение dropoff и сравнения его toohello быть расстояние.</span><span class="sxs-lookup"><span data-stu-id="292c5-329">We can also compute hello distance between pickup location and dropoff location and then compare it toohello trip distance.</span></span>

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Таблица данных о посадке и высадке](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Расстояние раскладки/dropoff tootrip расстояние рисунка](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="292c5-332">Подготовим сокращенный набор данных (1 %) для моделирования.</span><span class="sxs-lookup"><span data-stu-id="292c5-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="292c5-333">Эти данные можно использовать в модуле "Читатель" машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="292c5-333">We can use this data in Machine Learning reader module.</span></span>

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

<span data-ttu-id="292c5-334">Через некоторое время можно увидеть, что данные hello были загружены в кластеры Hadoop:</span><span class="sxs-lookup"><span data-stu-id="292c5-334">After a while, you can see hello data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Таблицы данных](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="292c5-336">**Чтение данных из HDI с помощью машинного обучения: модуль "Читатель"**</span><span class="sxs-lookup"><span data-stu-id="292c5-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="292c5-337">Можно также использовать hello **чтения** модуля в студии машинного обучения tooaccess hello и базы данных в кластере Hadoop.</span><span class="sxs-lookup"><span data-stu-id="292c5-337">You may also use hello **reader** module in Machine Learning Studio tooaccess hello database in Hadoop cluster.</span></span> <span data-ttu-id="292c5-338">Подключите hello учетные данные HDI кластеров и tooenable учетной записи хранилища Azure построения операция с использованием машинного обучения моделей с помощью базы данных в кластерах HDI.</span><span class="sxs-lookup"><span data-stu-id="292c5-338">Plug in hello credentials of your HDI clusters and Azure Storage Account tooenable build ing machine learning models using database in HDI clusters.</span></span>

![Свойства модуля "Читатель"](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="292c5-340">Hello Оцененный набор данных можно будет просмотреть:</span><span class="sxs-lookup"><span data-stu-id="292c5-340">hello scored dataset can then be viewed:</span></span>

![Просмотр оцененного набора данных](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="292c5-342">Хранилище данных SQL Azure и базы данных</span><span class="sxs-lookup"><span data-stu-id="292c5-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="292c5-343">Хранилище данных SQL Azure — это хранилище эластичных данных "как услуга" с возможностями SQL Server корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="292c5-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="292c5-344">Можно подготовить хранилище данных SQL Azure, следуя инструкциям hello в этом [статьи](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="292c5-344">You can provision your Azure SQL Data Warehouse by following hello instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="292c5-345">После подготовки хранилища данных SQL Azure можно использовать это [Пошаговое руководство](machine-learning-data-science-process-sqldw-walkthrough.md) отправить toodo данных и моделирование с использованием данных в хранилище данных SQL hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) toodo data upload, exploration and modeling using data within hello SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="292c5-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="292c5-346">Azure Cosmos DB</span></span>
<span data-ttu-id="292c5-347">Azure Cosmos DB база данных NoSQL в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-347">Azure Cosmos DB is a NoSQL database in hello cloud.</span></span> <span data-ttu-id="292c5-348">Он позволяет toowork с документами, таких как JSON и позволяет toostore и запрос документов hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-348">It allows you toowork with documents like JSON and allows you toostore and query hello documents.</span></span>

<span data-ttu-id="292c5-349">Необходимо после tooaccess действия-реквизиты Azure Cosmos DB от hello DSVM hello toodo.</span><span class="sxs-lookup"><span data-stu-id="292c5-349">You need toodo hello following per-requisites steps tooaccess Azure Cosmos DB from hello DSVM.</span></span>

1. <span data-ttu-id="292c5-350">Установите пакет SDK Python для DocumentDB (выполните команду ```pip install pydocumentdb``` из командной строки).</span><span class="sxs-lookup"><span data-stu-id="292c5-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="292c5-351">Создайте учетную запись и базу данных Azure Cosmos DB на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="292c5-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="292c5-352">Загрузить «Средство миграции базы данных Azure Cosmos» с [здесь](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) и извлеките tooa каталог</span><span class="sxs-lookup"><span data-stu-id="292c5-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract tooa directory of your choice</span></span>
4. <span data-ttu-id="292c5-353">Импорт данных JSON (вулканов данных), хранящиеся на [большой двоичный объект открытого](https://cahandson.blob.core.windows.net/samples/volcano.json) в DB Cosmos инструментом следующие команды Параметры toohello миграции (dtui.exe из hello каталог, где установлены средства миграции DB Cosmos hello).</span><span class="sxs-lookup"><span data-stu-id="292c5-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters toohello migration tool (dtui.exe from hello directory where you installed hello Cosmos DB Migration Tool).</span></span> <span data-ttu-id="292c5-354">Введите расположение исходной и целевой hello со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="292c5-354">Enter hello source and target location with these parameters:</span></span>
   
    <span data-ttu-id="292c5-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="292c5-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="292c5-356">После импорта данных hello, возможность перехода tooJupyter и откройте hello переносные под названием *DocumentDBSample* , содержащее python code tooaccess DocumentDB и выполните основные запросов.</span><span class="sxs-lookup"><span data-stu-id="292c5-356">Once you import hello data, you can go tooJupyter and open hello notebook titled *DocumentDBSample* which contains python code tooaccess DocumentDB and do some basic querying.</span></span> <span data-ttu-id="292c5-357">Дополнительные сведения о Cosmos DB, перейдя по адресу hello службы [страницы документации](https://docs.microsoft.com/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="292c5-357">You can learn more about Cosmos DB by visiting hello service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a><span data-ttu-id="292c5-358">8. Создание отчетов и панель мониторинга с помощью hello Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="292c5-358">8. Build reports and dashboard using hello Power BI Desktop</span></span>
<span data-ttu-id="292c5-359">Сообщите нам визуализируйте hello вулканов JSON-файла, мы видели в предшествующих примере Cosmos DB в Power BI toogain visual анализировать данные hello hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-359">Let us visualize hello Volcano JSON file that we saw in hello preceding Cosmos DB example in Power BI toogain visual insights into hello data.</span></span> <span data-ttu-id="292c5-360">Подробные инструкции доступны в hello [Power BI статьи](../cosmos-db/powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="292c5-360">Detailed steps are available in hello [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="292c5-361">Ниже приведены общие действия hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-361">Here are hello high-level steps:</span></span>

1. <span data-ttu-id="292c5-362">Откройте Power BI Desktop и щелкните "Получение данных".</span><span class="sxs-lookup"><span data-stu-id="292c5-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="292c5-363">Укажите URL-адрес hello как: https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="292c5-363">Specify hello URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="292c5-364">Вы увидите записи JSON hello, импортированные как список</span><span class="sxs-lookup"><span data-stu-id="292c5-364">You should see hello JSON records imported as a list</span></span>
3. <span data-ttu-id="292c5-365">Преобразовать в таблицу tooa hello, чтобы Power BI можно работать с hello же</span><span class="sxs-lookup"><span data-stu-id="292c5-365">Convert hello list tooa table so Power BI can work with hello same</span></span>
4. <span data-ttu-id="292c5-366">Разверните hello столбцы, щелкнув hello разверните значок (hello один со значком «стрелка влево и Стрелка вправо» hello на hello справа от столбца hello)</span><span class="sxs-lookup"><span data-stu-id="292c5-366">Expand hello columns by clicking on hello expand icon (hello one with hello "left arrow and a right arrow" icon on hello right of hello column)</span></span>
5. <span data-ttu-id="292c5-367">Обратите внимание, что расположение является полем "Запись".</span><span class="sxs-lookup"><span data-stu-id="292c5-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="292c5-368">Разверните запись hello и выберите только координаты hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-368">Expand hello record and select only hello coordinates.</span></span> <span data-ttu-id="292c5-369">Координаты указаны в столбце списка.</span><span class="sxs-lookup"><span data-stu-id="292c5-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="292c5-370">Добавление нового столбца tooconvert hello список координат столбца в виде запятой отдельного LatLong столбца объединения hello двух элементов в поле списка координат hello, с помощью формулы hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="292c5-370">Add a new column tooconvert hello list coordinate column into a comma separate LatLong column concatenating hello two elements in hello coordinate list field using hello formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="292c5-371">Наконец преобразовать hello ```Elevation``` tooDecimal столбца и выберите hello **закрыть** и **применить**.</span><span class="sxs-lookup"><span data-stu-id="292c5-371">Finally convert hello ```Elevation``` column tooDecimal and select hello **Close** and **Apply**.</span></span>

<span data-ttu-id="292c5-372">Вместо предыдущих шагах, вы можете вставить hello, следующий код, скрипты hello шаги, используемые в hello расширенного редактора в Power BI, позволяющий преобразования данных hello toowrite на языке запросов.</span><span class="sxs-lookup"><span data-stu-id="292c5-372">Instead of preceding steps, you can paste hello following code that scripts out hello steps used in hello Advanced Editor in Power BI that allows you toowrite hello data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="292c5-373">Теперь у вас есть hello данных в модели данных Power BI.</span><span class="sxs-lookup"><span data-stu-id="292c5-373">You now have hello data in your Power BI data model.</span></span> <span data-ttu-id="292c5-374">Рабочий стол Power BI Desktop должен выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="292c5-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI Desktop;](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="292c5-376">Можно приступать к созданию отчетов и визуализаций с помощью модели данных hello.</span><span class="sxs-lookup"><span data-stu-id="292c5-376">You can start building reports and visualizations using hello data model.</span></span> <span data-ttu-id="292c5-377">Выполните действия hello в этом [Power BI статьи](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild отчета.</span><span class="sxs-lookup"><span data-stu-id="292c5-377">You can follow hello steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild a report.</span></span> <span data-ttu-id="292c5-378">Hello конечным результатом является отчет, который выглядит как hello ниже.</span><span class="sxs-lookup"><span data-stu-id="292c5-378">hello end result is a report that looks like hello following.</span></span>

![Представление отчета в Power BI Desktop — соединитель Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a><span data-ttu-id="292c5-380">9. Динамически масштабировать ваш toomeet DSVM, необходимые для проекта</span><span class="sxs-lookup"><span data-stu-id="292c5-380">9. Dynamically scale your DSVM toomeet your project needs</span></span>
<span data-ttu-id="292c5-381">Можно масштабировать вверх и вниз toomeet DSVM hello, необходимые для проекта.</span><span class="sxs-lookup"><span data-stu-id="292c5-381">You can scale up and down hello DSVM toomeet your project needs.</span></span> <span data-ttu-id="292c5-382">Если не требуется toouse hello виртуальной Машины в вечернюю hello или выходные, можно просто завершить работу hello виртуальной Машины из hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="292c5-382">If you don't need toouse hello VM in hello evening or weekends, you can just shut down hello VM from hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="292c5-383">При использовании только hello кнопку завершения работы операционной системы на hello виртуальной Машины с вас взимается плата за вычислительные операции.</span><span class="sxs-lookup"><span data-stu-id="292c5-383">You incur compute charges if you use just hello Operating system shutdown button on hello VM.</span></span>  
> 
> 

<span data-ttu-id="292c5-384">Если нужно toohandle крупномасштабных анализ и потребности в дополнительной емкости ЦП и памяти или диска можно найти большой разные размеры виртуальной Машины с точки зрения ядер ЦП, объем памяти и типов дисков (включая твердотельные накопители), удовлетворяющих ваших потребностей бюджета и вычислений.</span><span class="sxs-lookup"><span data-stu-id="292c5-384">If you need toohandle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="292c5-385">Hello полный список виртуальных машин вместе с их почасовых вычислений ценовую доступен на hello [цены на виртуальных машинах Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) страницы.</span><span class="sxs-lookup"><span data-stu-id="292c5-385">hello full list of VMs along with their hourly compute pricing is available on hello [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="292c5-386">Аналогичным образом Если уменьшает необходимость обработки емкость виртуальной Машины (например: переместить основные рабочей нагрузки tooa Hadoop или кластер Spark), можно масштабировать кластер hello из hello [портал Azure](https://portal.azure.com) , поэтому параметры toohello вашей виртуальной машины экземпляр.</span><span class="sxs-lookup"><span data-stu-id="292c5-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload tooa Hadoop or a Spark cluster), you can scale down hello cluster from hello [Azure portal](https://portal.azure.com) and going toohello settings of your VM instance.</span></span> <span data-ttu-id="292c5-387">Ниже приведен снимок экрана.</span><span class="sxs-lookup"><span data-stu-id="292c5-387">Here is a screenshot.</span></span>

![Параметры экземпляра виртуальной машины](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="292c5-389">10. Установка дополнительных инструментов на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="292c5-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="292c5-390">Упакованные несколько средств, которые мы считаем, что может tooaddress многие hello analytics потребности в общих данных, который следует сэкономить время, чтобы избежать необходимости tooinstall и настройка сред один за другим и сэкономить деньги, оплата только ресурсы, которые являются используете.</span><span class="sxs-lookup"><span data-stu-id="292c5-390">We have packaged several tools that we believe are able tooaddress many of hello common data analytics needs and that should save you time by avoiding having tooinstall and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="292c5-391">Можно использовать другие данных Azure и службы аналитики профилирование в этой статье tooenhance анализируемые.</span><span class="sxs-lookup"><span data-stu-id="292c5-391">You can leverage other Azure data and analytics services profiled in this article tooenhance your analytics environment.</span></span> <span data-ttu-id="292c5-392">Мы понимаем, что в определенных случаях могут потребоваться дополнительные средства, включая некоторые инструменты сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="292c5-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="292c5-393">У вас есть полный административный доступ hello виртуальной машины tooinstall новые средства, необходимые.</span><span class="sxs-lookup"><span data-stu-id="292c5-393">You have full administrative access on hello virtual machine tooinstall new tools you need.</span></span> <span data-ttu-id="292c5-394">Вы также можете установить дополнительные пакеты на Python и R, которые не предустановлены.</span><span class="sxs-lookup"><span data-stu-id="292c5-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="292c5-395">Для Python можно использовать ```conda``` или ```pip```.</span><span class="sxs-lookup"><span data-stu-id="292c5-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="292c5-396">R можно использовать hello ```install.packages()``` в hello R консоли или использовать hello интегрированной среды разработки и выберите «**пакетов** -> **пакетов установки...** ".</span><span class="sxs-lookup"><span data-stu-id="292c5-396">For R you can use hello ```install.packages()``` in hello R console or use hello IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="292c5-397">Сводка</span><span class="sxs-lookup"><span data-stu-id="292c5-397">Summary</span></span>
<span data-ttu-id="292c5-398">Это лишь часть hello вещей, которые можно выполнять на hello виртуальная машина анализа данных Microsoft.</span><span class="sxs-lookup"><span data-stu-id="292c5-398">These are just some of hello things you can do on hello Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="292c5-399">Существует много больше вещей, которые можно сделать toomake его действующие analytics среды.</span><span class="sxs-lookup"><span data-stu-id="292c5-399">There are many more things you can do toomake it an effective analytics environment.</span></span>

