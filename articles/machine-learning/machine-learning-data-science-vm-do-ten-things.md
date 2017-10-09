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
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>Десять фактов, которые можно выполнять на обработки и анализа данных hello виртуальной машины
Hello виртуальной машины обработки и анализа данных Microsoft (DSVM) — это среда разработки обработки и анализа данных, позволяющий вы tooperform различные задачи и моделирование данных. Hello среда поставляется уже встроенного и распространение популярных данными средства аналитики, которые позволяют легко tooget быстро начать работу с анализа для локальной, облака и гибридной развертываний. Hello DSVM работает в тесном сотрудничестве с множество служб Azure и могут tooread и обработки данных, который уже хранится в Azure, в хранилище данных SQL Azure, Озера данных Azure, хранилище Azure или в базе данных Azure Cosmos. Она также может использовать другие инструменты аналитики, такие как машинное обучение Azure и фабрика данных Azure.

В этой статье мы рассмотрим как toouse вашей tooperform DSVM задачи обработки и анализа различных данных, а также взаимодействовать с другими службами Azure. Ниже приведены некоторые hello вещей, которые можно выполнять на hello DSVM.

1. Просмотр данных и разработки моделей локально на hello DSVM, с помощью Microsoft R Server Python
2. Использовать tooexperiment записной книжки Jupyter с данными в браузере, с помощью Python 2, Python 3 Microsoft R готовы версия enterprise R обеспечивает масштабируемость и производительность
3. Ввод моделей, построенных с помощью R и Python, в эксплуатацию в службе машинного обучения Azure, чтобы клиентские приложения могли обращаться к ним с использованием простого интерфейса веб-служб
4. Администрирование ресурсов Azure с помощью портала Azure или PowerShell.
5. Увеличение объема хранилища и предоставление всем членам команды общего доступа к большим наборам данных и коду за счет создания файлового хранилища Azure в виде подключаемого диска в DSVM.
6. Совместное использование кода с коллегами с помощью GitHub и доступа в репозиторий, пользуясь hello предварительно установленные клиенты Git - Git Bash Git графического интерфейса пользователя.
7. Доступ к различным службам данных и службам аналитики Azure, таким как хранилище BLOB-объектов, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, хранилище данных SQL Azure и базы данных Azure.
8. Создавать отчеты и панели мониторинга с помощью Power BI Desktop, предустановленные на hello DSVM hello и развертывать их в облаке hello
9. Динамически масштабировать ваш toomeet DSVM, необходимые для проекта
10. Установка дополнительных инструментов на виртуальной машине   

> [!NOTE]
> Взимается плата за использование дополнительных для многих hello дополнительные данные хранилища и аналитика служб, перечисленных в этой статье. См. toohello [цены Azure](https://azure.microsoft.com/pricing/) для получения подробной информации.
> 
> 

**Предварительные требования**

* Вам понадобится подписка Azure. Вы можете зарегистрироваться [здесь](https://azure.microsoft.com/free/), чтобы получить бесплатную пробную версию.
* Инструкции по подготовке виртуальная машина анализа данных на hello портал Azure можно найти по адресу [создания виртуальной машины](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1. Просмотр данных и разработка моделей с помощью Microsoft R Server или Python
Аналитики данных языками, такими как toodo R и Python можно использовать на hello DSVM вправо.

Для R можно использовать Интегрированную называется «Revolution R Enterprise 8.0», можно найти в меню "Пуск" hello "или" hello рабочего стола. Корпорация Майкрософт предоставляет дополнительные библиотеки hello откройте источник/CRAN-R tooenable масштабируемой аналитики и hello возможность tooanalyze данных больше, чем размер памяти hello, выполнив параллельной фрагментированный анализа. Вы можете установить любую другую интегрированную среду разработки R, например [RStudio](https://www.rstudio.com/products/rstudio-desktop/).

Для Python можно использовать интегрированную среду разработки, как Visual Studio Community Edition, имеющая hello средства Python для предварительно установленной расширения Visual Studio (PTVS). По умолчанию в PTVS настроена только базовая версия Python 2.7 (без аналитических библиотек, таких как SciKit, Pandas). В порядке tooenable Anaconda Python 2.7 и 3.5 необходимо toodo hello следующее:

* Создание пользовательских средах для каждой версии, перейдя по слишком**средства** -> **средства Python** -> **среды Python** и выбрав команду " **+ Настраиваемый**«в Visual Studio 2015 Community Edition hello
* Укажите описание и префикс пути, как задавать hello среды *c:\anaconda* Anaconda Python 2.7 или *c:\anaconda\envs\py35* Anaconda Python 3.5
* Нажмите кнопку **автоопределение** и затем **применить** toosave hello среды.

Вот какие настройки нестандартной среды hello, выглядит как в Visual Studio.

![Установка PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

В разделе hello [PTVS документации](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) Дополнительные сведения о том, как toocreate среды Python.

Теперь вы настраиваются toocreate новый проект Python. Перейдите в слишком**файл** -> **New** -> **проекта** -> **Python** и выберите тип hello Приложения Python, в которой выполняется сборка. Можно установить среду Python hello hello текущего проекта toohello нужную версию (Anaconda 2.7 или 3.5): щелкните правой кнопкой мыши hello **среды Python**выберите **Установка и удаление среды Python**, и затем выберите hello требуемого tooassociate среды с проектом hello. Дополнительные сведения о работе с PTVS на hello продукта можно найти [документации](https://github.com/Microsoft/PTVS/wiki) страницы.

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2. С помощью tooexplore книжке Jupyter и модели данных с помощью Python или R
Hello книжке Jupyter — мощная среда, которая предоставляет браузера «интегрированной среды разработки» для моделирования и просмотра данных. Python 2, Python 3 или R (открытым исходным кодом и hello Microsoft R Server) можно использовать в записной книжке Jupyter.

hello toolaunch книжке Jupyter щелкните значок меню Пуск hello / значка на рабочем столе под названием **книжке Jupyter**. На hello DSVM можно также просмотреть слишком "https://localhost:9999 /» tooaccess hello Юпитер ноутбука. Если предлагается ввести пароль, используйте инструкции, приведенные в hello ***как toocreate надежный пароль на сервере записной книжки Jupyter hello*** раздел hello [подготовки hello виртуальная машина Microsoft данных анализа](machine-learning-data-science-provision-vm.md)toocreate разделе записной книжке Jupyter hello tooaccess надежный пароль. 

После открытия записной книжки hello, вы увидите, что каталог, содержащий несколько записных книжек пример, предварительно упакованные в hello DSVM. Теперь вы можете:

* Щелкните кода hello toosee записной книжки hello.
* выполнить каждую ячейку нажатием сочетания клавиш **SHIFT + ВВОД**;
* Запустите всей записной книжки hello, щелкнув **ячейки** -> **запуска**
* создать новую, щелкнув значок Jupyter (левый верхний угол) hello и выбрав **New** кнопки hello справа и выбрав язык hello записной книжки (также известный как ядер).   

> [!NOTE]
> В настоящее время мы поддерживаем Python 2.7, Python 3.5 и R. ядра hello R поддерживает программирование в R с открытым кодом как, так и hello enterprise масштабируемой Microsoft R Server.   
> 
> 

После входа в записной книжке hello можно исследовать данные, построена модель hello, проверка hello модели на любом из библиотек.

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3. Создание моделей с помощью R или Python и их ввод в эксплуатацию с помощью машинного обучения Azure
После создания и проверки модели hello следующим шагом обычно является toodeploy его в рабочей среде. Это позволяет клиентских приложений tooinvoke hello модели прогнозов в реальном времени или на основе пакетного режима. Машинное обучение Azure предоставляет toooperationalize механизм модель, встроенных в R или Python.

После ввода в эксплуатацию модели в машинном обучении Azure предоставляется веб-службы, позволяющую клиентам toomake вызовы REST, которые передачи входных параметров и получения прогнозов из модели hello как выходные данные.   

> [!NOTE]
> Если вы еще не еще зарегистрировались для машинного обучения Azure, можно получить бесплатную рабочую область или стандартной рабочей области, перейдя по адресу hello [студии машинного обучения Azure](https://studio.azureml.net/) домашнюю страницу и щелкните на «Приступая к работе».   
> 
> 

### <a name="build-and-operationalize-python-models"></a>Создание и ввод в эксплуатацию моделей Python
Ниже приведен фрагмент кода, разработанного в записной книжке Jupyter Python, создающий простой модели с помощью библиотеки узнать SciKit hello.

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

метод Hello используется toodeploy вашей tooAzure моделей python прогноза hello качестве оболочки для машинного обучения модели hello в функцию и оформляет его с атрибутами, предоставляемые библиотекой hello предустановленных машинного обучения Azure python, указывающих на машине Azure Идентификатор рабочей области обучения, ключ API и hello входные и выходные параметры.  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

Клиенту теперь можно выполнять вызовы toohello веб-службы. Существуют удобства оболочек, создания запросов REST API hello. Ниже приведен пример кода tooconsume hello веб-службы.

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> Библиотека машинного обучения Azure Hello поддерживается только на Python 2.7 в настоящее время.   
> 
> 

### <a name="build-and-operationalize-r-models"></a>Создание и ввод в эксплуатацию моделей R
Вы можете развернуть R моделях, основанных на hello виртуальная машина анализа данных, или в другом месте на машинного обучения Azure в режиме, аналогичные toohow, который выполняется для Python. Ее hello шагов:

* Создайте tooprovide файл settings.json, идентификатор рабочей области и проверки подлинности маркера, как показано в следующий образец кода hello.
* записать оболочку для функции прогнозирования hello модели.
* Вызовите ```publishWebService``` в hello toopass библиотеки машинного обучения Azure в оболочку функции hello.  

Вот hello процедуры и фрагменты кода, может быть используется tooset вверх, построения, публиковать и использовать модель веб-службы в машинном обучении Azure.

#### <a name="setup"></a>Настройка
1. Установить пакет R обучения машины hello, введя ```install.packages("AzureML")``` в Revolution R Enterprise 8.0 IDE или R интерфейс IDE.
2. Загрузите RTools [отсюда](https://cran.r-project.org/bin/windows/Rtools/). Требуется программа hello пути (и именованные zip.exe) toooperationalize hello zip R-пакет в машинного обучения.
3. Создайте файл settings.json каталог с именем ```.azureml``` в домашнем каталоге и введите параметры hello в рабочей области машинного обучения Azure:

структура файла Settings.json:

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>Создание модели на языке R и ее публикация в службе машинного обучения Azure
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

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>Работать с моделью hello, развернутых в машинном обучении Azure
tooconsume hello модели из клиентских приложений, мы используем toolook библиотеки машинного обучения Azure hello копирование hello опубликованных веб-службы по имени, используя hello `services` конечной hello toodetermine вызовов API. Затем нужно просто вызвать hello `consume` функции, а затем передать hello данных кадра toobe прогноз.
После кода Hello — модель используется tooconsume hello, опубликованы как веб-службы машинного обучения Azure.

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

Дополнительные сведения о библиотеке hello Azure Machine Learning R можно найти [здесь](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4. Администрирование ресурсов Azure с помощью портала Azure или PowerShell.
Hello DSVM позволяет не только вы toobuild решении analytics локально на hello виртуальной машины, но и обеспечивает службы tooaccess в облаке Azure корпорации Майкрософт. Azure предоставляет несколько вычислительных служб, служб хранения данных и служб аналитики данных, а также ряд других служб, которые можно администрировать и к которым можно обращаться с DSVM.

tooadminister подписку и облачную ресурсами Azure можно использовать обозреватель и точки toothe [портал Azure](https://portal.azure.com). Также можно использовать Azure Powershell tooadminister подписка Azure и ресурсов через сценарий.
Можно запустить Azure Powershell с помощью ярлыка на рабочем столе hello или из hello меню «Пуск» под названием «Microsoft Azure Powershell». Дополнительные сведения об администрировании подписки и ресурсов Azure с помощью сценариев Windows PowerShell см. в [документации по Microsoft Azure PowerShell](../powershell-azure-resource-manager.md).

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5. Увеличение объема хранилища за счет общей файловой системы
Специалисты по анализу данных могут совместно использовать большие наборы данных, кода или других ресурсов в команде hello. Hello DSVM сам имеет примерно 70 ГБ доступного пространства. tooextend хранилища, можно использовать hello службы файлов Azure и подключить его на hello DSVM или получить к нему доступ через REST API.   

> [!NOTE]
> Hello максимальное hello службы файлов Azure папки размером 5 ТБ и места максимальный размер отдельного файла составляет 1 ТБ.   
> 
> 

Можно использовать Azure Powershell toocreate ресурс службы файлов Azure. Вот hello toorun сценарий в Azure PowerShell toocreate Azure файловый ресурс службы.

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


Созданную общую папку Azure можно подключить к любой виртуальной машине в Azure. Настоятельно рекомендуется этого hello виртуальной Машины — в одном центре обработки данных Azure как задержка tooavoid учетной записи хранилища hello и данные передачи расходов. Ниже приведены hello команды toomount hello диска на hello DSVM, который можно запустить в Azure Powershell.

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


Теперь можно использовать этот диск, как и любой обычный диск на hello виртуальной Машины.

## <a name="6-share-code-with-your-team-using-github"></a>6. Совместное использование кода командой с помощью GitHub
GitHub — это хранилище кода, где можно найти много примеров кода и источники для различных средств, с использованием различных технологий, совместно с сообществом разработчиков hello. Она использует Git, как hello технологию tootrack и хранилище версий файлов кода hello. GitHub также является платформой которого можно создать собственный репозиторий toostore общего кода и документации, команды реализовать систему управления версиями, а также элемент управления, обладающих доступом tooview и добавлять код. Перейдите на страницу приветствия [страниц справки GitHub](https://help.github.com/) Дополнительные сведения об использовании Git. Можно использовать GitHub как один из способов toocollaborate hello с другими участниками команды, используйте код, разработанный сообществом hello и участие сообщества задней toohello кода.

Hello DSVM уже загружена клиентских средств на обоих командной строки как хорошо tooaccess графического интерфейса пользователя репозитории GitHub. Hello toowork средство командной строки с Git и GitHub называется Git Bash. Visual Studio, установленной на hello DSVM имеет расширения hello Git. Можно найти при запуске значки для этих средств hello меню "Пуск" и рабочего стола hello.

toodownload кода из репозитория GitHub использовать hello ```git clone``` команды. Например репозитории обработки и анализа данных toodownload, опубликованные корпорацией Майкрософт в текущем каталоге hello можно запустить следующую команду, после входа в hello ```git-bash```.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

В Visual Studio можно выполнить hello же операции клонирования. Следующий снимок экрана приветствия показано, как tooaccess Git и GitHub средства в Visual Studio.

![Git в Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

Можно найти дополнительные сведения об использовании своего репозитория GitHub из нескольких ресурсов, доступных в github.com Git toowork. Hello [памятку](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) является полезным ссылкой.

## <a name="7-access-various-azure-data-and-analytics-services"></a>7. Доступ к различным службам данных и службам аналитики Azure
### <a name="azure-blob"></a>Большой двоичный объект Azure
Большой двоичный объект Azure является надежным и экономичным облачным хранилищем для больших и малых объемов данных. Рассмотрим перенос tooAzure данных больших двоичных объектов и доступа к данным, хранящимся в BLOB-объект Azure.

**Предварительные требования**

* **Создайте учетную запись хранения BLOB-объектов Azure на [портале Azure](https://portal.azure.com).**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Убедитесь, что hello средство AzCopy предустановленных командной строки найдено в ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```. Можно добавить hello каталога содержащий hello azcopy.exe tooyour путь среды переменной tooavoid ввода hello полностью команда путь при запуске этого средства. Дополнительные сведения о средство AzCopy см слишком[AzCopy документации](../storage/common/storage-use-azcopy.md)
* Запустите средство hello обозреватель хранилища Azure. Его можно скачать с сайта [Microsoft Azure Storage Explorer](http://storageexplorer.com/). 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**Перемещение данных из виртуальной Машины tooAzure больших двоичных объектов: AzCopy**

toomove данных между локальным файлам и хранилище больших двоичных объектов, можно использовать AzCopy в командной строки или PowerShell:

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

Замените **C:\myfolder** toohello путь, где хранится файл, **mystorageaccount** имя учетной записи хранилища больших двоичных объектов tooyour **mycontainer** toohello имя контейнера, **ключ учетной записи хранения** ключ доступа к хранилищу больших двоичных объектов tooyour. Данные вашей учетной записи хранения находятся на [портале Azure](https://portal.azure.com).

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

Выполните команду AzCopy в PowerShell или из командной строки. Далее приведен пример использования команды AzCopy.

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



После выполнения вашей tooan toocopy команды AzCopy BLOB-объектов Azure указан файл отображается в обозреватель хранилищ Azure скоро.

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**Перемещение данных из виртуальной Машины tooAzure больших двоичных объектов: Обозреватель хранилищ Azure**

Также можно передать данные из локального файла hello в ВМ с помощью обозревателя хранилищ Azure:

* контейнер tooa tooupload данных, выберите hello целевой контейнер и нажмите кнопку hello **отправить** кнопки.![ Отправка в обозревателе хранилищ](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* Щелкните hello **...**  toohello справа от приветствия **файлы** , выберите один или несколько файлов tooupload hello файловой системе и нажмите кнопку **отправить** toobegin, передача файлов hello.![ Отправка файлов tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**Чтение данных из большого двоичного объекта Azure: модуль "Читатель" машинного обучения**

В студии машинного обучения Azure можно использовать **модуль импорта данных** tooread данные из большого двоичного объекта.

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**Чтение данных из BLOB-объекта Azure: Python ODBC**

Можно использовать **BlobService** библиотеки tooread данных непосредственно из большого двоичного объекта в программе книжке Jupyter или Python.

Сначала импортируйте необходимые пакеты.

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

Затем подключите учетные данные BLOB-объекта Azure и считайте данные из BLOB-объекта.

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

Hello данные считываются в виде блока данных:

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Озеро данных Azure
Хранилище Azure Data Lake является гипермасштабируемым репозиторием для рабочих нагрузок аналитической обработки больших данных, совместимым с распределенной файловой системой Hadoop (HDFS). Она работает с экосистемой Hadoop hello и hello аналитики Озера данных Azure. Мы покажем, как можно переместить данные в хранилище Озера данных Azure hello и выполнить анализ с помощью аналитики Озера данных Azure.

**Предварительные требования**

* Создайте экземпляр Azure Data Lake Analytics на [портале Azure](https://portal.azure.com).

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* Hello **средства Озера данных Azure** в **Visual Studio** находится в следующей [ссылку](https://www.microsoft.com/download/details.aspx?id=49504) уже установлены на hello Visual Studio Community Edition, который находится на виртуальной машине hello. После запуска Visual Studio и ведения журнала в вашей подписке Azure, вы должны увидеть вашей учетной записи Azure анализа данных и хранения hello левой панели Visual Studio.

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**Перемещение данных из виртуальной Машины tooData Озера: проводник Озера данных Azure**

Можно использовать **обозреватель Озера данных Azure** tooupload данные из локальных файлов hello в хранилище Озера tooData виртуальной машины.

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

Можно также создать конвейер данных tooproductionize вашей tooor перемещения данных из Озера данных Azure с помощью hello [Factory(ADF) данных Azure](https://azure.microsoft.com/services/data-factory/). Мы называем toothis [статьи](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide можно выполнить с помощью данных hello toobuild действия hello конвейеров.

**Чтение данных из Озера tooData больших двоичных объектов Azure: U-SQL**

Если данные хранятся в хранилище BLOB-объектов Azure, их можно считывать непосредственно из BLOB-объекта хранилища Azure в запросе U-SQL. Прежде чем составление U-SQL-запрос, убедитесь, что учетной записи хранилища BLOB-объектов — связанные tooyour Озера данных Azure. Go слишком**портал Azure**найти информационную панель аналитики Озера данных Azure, нажмите кнопку **добавить источник данных**, выберите тип хранения слишком**хранилища Azure** и подключите хранилище Azure Имя учетной записи и ключа. Затем предпринимается может tooreference hello данные, хранящиеся в учетной записи хранилища hello.

![Ввод имени учетной записи хранения и ключа](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

В Visual Studio можно считывать данные из хранилища больших двоичных объектов, сделать некоторые операции с данными, конструируются и вывод hello результирующие данные tooeither Озера данных Azure или хранилища больших двоичных объектов. При создании ссылок данных hello в хранилище больших двоичных объектов, используйте **wasb: / /**; при ссылке на hello данных Озера данных Azure, используйте **swbhdfs: / /**

![Кадр данных](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

Можно использовать следующие запросы U-SQL в Visual Studio hello:

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



После запроса является отправленной toohello сервером, отображается диаграмма, показывающая hello состояние задания.

![Схема состояния задания](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**Запрос данных в озере данных: U-SQL**

После набора данных hello полученный в Озера данных Azure, вы можете использовать [U-SQL языка](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery и изучать данные hello. U-SQL языка аналогичные tooT-SQL, но объединяет некоторые функции C# таким образом, чтобы пользователи могут записывать пользовательские модули, определяемых пользователем функций и и т. д. Можно использовать скрипты hello в предыдущем шаге hello.

После запроса hello отправленной tooserver, tripdata_summary. CSV можно найти в скором времени **обозреватель Озера данных Azure**, может просмотреть данные hello, щелкните правой кнопкой мыши файл hello.

![Файл в Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

сведения о файле hello toosee:

![Сведения о файле](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>Кластеры HDInsight Hadoop
Azure HDInsight является управляемой службой Apache Hadoop, Spark, HBase и Storm в облаке hello. Легко можно работать с кластерами Azure HDInsight из виртуальная машина анализа данных hello.

**Предварительные требования**

* Создайте учетную запись хранения BLOB-объектов Azure на [портале Azure](https://portal.azure.com). Эта учетная запись хранения — используется toostore данные для кластеров HDInsight.

![Создание учетной записи хранения больших двоичных объектов Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Настройте кластеры HDInsight Hadoop в Azure на [портале Azure](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * Необходимо связать учетную запись хранения hello, создан с кластером HDInsight, при его создании. Эта учетная запись используется для доступа к данным, которое может быть обработано в кластере hello.

![Связать учетную запись toostorage создан с кластером HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* Необходимо включить **удаленного доступа** toohello головного узла кластера hello после его создания. Запоминать учетные данные удаленного доступа hello, указанные здесь (отличающиеся от параметров, указанных для hello кластера при его создании): при необходимости в последующих процедурах hello.

![Включение удаленного доступа](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* Создайте рабочую область машинного обучения Azure. В ней будут храниться эксперименты машинного обучения. Выберите параметры hello выделяются на портале, как показано на следующий снимок экрана приветствия:

![Создание рабочей области машинного обучения Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* Затем введите параметры hello для рабочей области

![Ввод параметров рабочей области машинного обучения](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* Загрузите данные с помощью IPython Notebook. Сначала импортируйте необходимые пакеты, подключите в учетных данных, создание базы данных в вашей учетной записи хранилища, а затем загрузить кластеры tooHDI данных.

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


* Кроме того, можно использовать эту [Пошаговое руководство](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC такси данных tooHDI кластера. Ниже перечислены основные действия.
  
  * AzCopy: загрузите ZIP-CSV большой двоичный объект открытого tooyour локальной папке
  * AzCopy: Отправка распакованную CSV из локальной папки tooHDI кластера
  * Войдите в hello головного узла кластера Hadoop и подготовка для исследовательского анализа

После загрузки tooHDI кластера hello данных можно проверить данные в обозреватель хранилища Azure. Кроме того, в кластере HDI находится созданная база данных nyctaxidb.

**Просмотр данных: запросы Hive в Python**

Поскольку данные hello в кластере Hadoop, можно использовать hello pyodbc пакета tooconnect tooHadoop кластеров и с помощью просмотра toodo Hive и конструируются запрос к базе данных. Вы можете просмотреть hello существующие таблицы, созданной на шаге готовности hello.

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Просмотр имеющихся таблиц](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

Давайте рассмотрим hello количество записей в каждый месяц и hello частоты скошенные или отсутствует в таблице trip hello:

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

Мы также вычислять hello расстояние между раскладки и расположение dropoff и сравнения его toohello быть расстояние.

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

Подготовим сокращенный набор данных (1 %) для моделирования. Эти данные можно использовать в модуле "Читатель" машинного обучения.

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

Через некоторое время можно увидеть, что данные hello были загружены в кластеры Hadoop:

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Таблицы данных](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**Чтение данных из HDI с помощью машинного обучения: модуль "Читатель"**

Можно также использовать hello **чтения** модуля в студии машинного обучения tooaccess hello и базы данных в кластере Hadoop. Подключите hello учетные данные HDI кластеров и tooenable учетной записи хранилища Azure построения операция с использованием машинного обучения моделей с помощью базы данных в кластерах HDI.

![Свойства модуля "Читатель"](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

Hello Оцененный набор данных можно будет просмотреть:

![Просмотр оцененного набора данных](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>Хранилище данных SQL Azure и базы данных
Хранилище данных SQL Azure — это хранилище эластичных данных "как услуга" с возможностями SQL Server корпоративного класса.

Можно подготовить хранилище данных SQL Azure, следуя инструкциям hello в этом [статьи](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md). После подготовки хранилища данных SQL Azure можно использовать это [Пошаговое руководство](machine-learning-data-science-process-sqldw-walkthrough.md) отправить toodo данных и моделирование с использованием данных в хранилище данных SQL hello.

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
Azure Cosmos DB база данных NoSQL в облаке hello. Он позволяет toowork с документами, таких как JSON и позволяет toostore и запрос документов hello.

Необходимо после tooaccess действия-реквизиты Azure Cosmos DB от hello DSVM hello toodo.

1. Установите пакет SDK Python для DocumentDB (выполните команду ```pip install pydocumentdb``` из командной строки).
2. Создайте учетную запись и базу данных Azure Cosmos DB на [портале Azure](https://portal.azure.com).
3. Загрузить «Средство миграции базы данных Azure Cosmos» с [здесь](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) и извлеките tooa каталог
4. Импорт данных JSON (вулканов данных), хранящиеся на [большой двоичный объект открытого](https://cahandson.blob.core.windows.net/samples/volcano.json) в DB Cosmos инструментом следующие команды Параметры toohello миграции (dtui.exe из hello каталог, где установлены средства миграции DB Cosmos hello). Введите расположение исходной и целевой hello со следующими параметрами:
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1

После импорта данных hello, возможность перехода tooJupyter и откройте hello переносные под названием *DocumentDBSample* , содержащее python code tooaccess DocumentDB и выполните основные запросов. Дополнительные сведения о Cosmos DB, перейдя по адресу hello службы [страницы документации](https://docs.microsoft.com/azure/cosmos-db/).

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8. Создание отчетов и панель мониторинга с помощью hello Power BI Desktop
Сообщите нам визуализируйте hello вулканов JSON-файла, мы видели в предшествующих примере Cosmos DB в Power BI toogain visual анализировать данные hello hello. Подробные инструкции доступны в hello [Power BI статьи](../cosmos-db/powerbi-visualize.md). Ниже приведены общие действия hello.

1. Откройте Power BI Desktop и щелкните "Получение данных". Укажите URL-адрес hello как: https://cahandson.blob.core.windows.net/samples/volcano.json
2. Вы увидите записи JSON hello, импортированные как список
3. Преобразовать в таблицу tooa hello, чтобы Power BI можно работать с hello же
4. Разверните hello столбцы, щелкнув hello разверните значок (hello один со значком «стрелка влево и Стрелка вправо» hello на hello справа от столбца hello)
5. Обратите внимание, что расположение является полем "Запись". Разверните запись hello и выберите только координаты hello. Координаты указаны в столбце списка.
6. Добавление нового столбца tooconvert hello список координат столбца в виде запятой отдельного LatLong столбца объединения hello двух элементов в поле списка координат hello, с помощью формулы hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.
7. Наконец преобразовать hello ```Elevation``` tooDecimal столбца и выберите hello **закрыть** и **применить**.

Вместо предыдущих шагах, вы можете вставить hello, следующий код, скрипты hello шаги, используемые в hello расширенного редактора в Power BI, позволяющий преобразования данных hello toowrite на языке запросов.

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



Теперь у вас есть hello данных в модели данных Power BI. Рабочий стол Power BI Desktop должен выглядеть так:

![Power BI Desktop;](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

Можно приступать к созданию отчетов и визуализаций с помощью модели данных hello. Выполните действия hello в этом [Power BI статьи](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild отчета. Hello конечным результатом является отчет, который выглядит как hello ниже.

![Представление отчета в Power BI Desktop — соединитель Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9. Динамически масштабировать ваш toomeet DSVM, необходимые для проекта
Можно масштабировать вверх и вниз toomeet DSVM hello, необходимые для проекта. Если не требуется toouse hello виртуальной Машины в вечернюю hello или выходные, можно просто завершить работу hello виртуальной Машины из hello [портал Azure](https://portal.azure.com).

> [!NOTE]
> При использовании только hello кнопку завершения работы операционной системы на hello виртуальной Машины с вас взимается плата за вычислительные операции.  
> 
> 

Если нужно toohandle крупномасштабных анализ и потребности в дополнительной емкости ЦП и памяти или диска можно найти большой разные размеры виртуальной Машины с точки зрения ядер ЦП, объем памяти и типов дисков (включая твердотельные накопители), удовлетворяющих ваших потребностей бюджета и вычислений. Hello полный список виртуальных машин вместе с их почасовых вычислений ценовую доступен на hello [цены на виртуальных машинах Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) страницы.

Аналогичным образом Если уменьшает необходимость обработки емкость виртуальной Машины (например: переместить основные рабочей нагрузки tooa Hadoop или кластер Spark), можно масштабировать кластер hello из hello [портал Azure](https://portal.azure.com) , поэтому параметры toohello вашей виртуальной машины экземпляр. Ниже приведен снимок экрана.

![Параметры экземпляра виртуальной машины](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10. Установка дополнительных инструментов на виртуальной машине
Упакованные несколько средств, которые мы считаем, что может tooaddress многие hello analytics потребности в общих данных, который следует сэкономить время, чтобы избежать необходимости tooinstall и настройка сред один за другим и сэкономить деньги, оплата только ресурсы, которые являются используете.

Можно использовать другие данных Azure и службы аналитики профилирование в этой статье tooenhance анализируемые. Мы понимаем, что в определенных случаях могут потребоваться дополнительные средства, включая некоторые инструменты сторонних производителей. У вас есть полный административный доступ hello виртуальной машины tooinstall новые средства, необходимые. Вы также можете установить дополнительные пакеты на Python и R, которые не предустановлены. Для Python можно использовать ```conda``` или ```pip```. R можно использовать hello ```install.packages()``` в hello R консоли или использовать hello интегрированной среды разработки и выберите «**пакетов** -> **пакетов установки...** ".

## <a name="summary"></a>Сводка
Это лишь часть hello вещей, которые можно выполнять на hello виртуальная машина анализа данных Microsoft. Существует много больше вещей, которые можно сделать toomake его действующие analytics среды.

