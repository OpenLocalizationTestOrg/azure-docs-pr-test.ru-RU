---
title: "aaaAccess наборов данных с клиентской библиотеки Python обучения машины | Документы Microsoft"
description: "Установить и использовать hello tooaccess библиотека клиентов Python и безопасно управлять данными машинного обучения Azure из локальной среды Python."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="3676d-103">Наборы данных Access в Python с помощью клиентской библиотеки hello Azure Machine Learning Python</span><span class="sxs-lookup"><span data-stu-id="3676d-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="3676d-104">Предварительный просмотр Hello клиентской библиотеки Microsoft Azure Machine Learning Python можно включить безопасный доступ tooyour машинного обучения Azure наборы данных из локальной среды Python и обеспечивает создание hello и управления наборов данных в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3676d-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="3676d-105">В этой статье описано, как:</span><span class="sxs-lookup"><span data-stu-id="3676d-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="3676d-106">установить клиентскую библиотеку hello машины обучения Python</span><span class="sxs-lookup"><span data-stu-id="3676d-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="3676d-107">доступ и загрузить наборы данных, включая инструкции по авторизации tooget tooaccess машинного обучения Azure наборы данных из локальной среды Python</span><span class="sxs-lookup"><span data-stu-id="3676d-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="3676d-108">получать доступ к промежуточным наборам данных из экспериментов;</span><span class="sxs-lookup"><span data-stu-id="3676d-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="3676d-109">использовать наборы данных tooenumerate библиотека клиентов Python hello, доступ к метаданным, читать содержимое hello объекта dataset, создать новые наборы данных и обновлять существующие наборы данных</span><span class="sxs-lookup"><span data-stu-id="3676d-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="3676d-110"><a name="prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3676d-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="3676d-111">Библиотека клиентов Python Hello был протестирован в следующих средах hello:</span><span class="sxs-lookup"><span data-stu-id="3676d-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="3676d-112">Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="3676d-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="3676d-113">Python 2.7, 3.3 и 3.4</span><span class="sxs-lookup"><span data-stu-id="3676d-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="3676d-114">Он имеет зависимость от hello следующие пакеты:</span><span class="sxs-lookup"><span data-stu-id="3676d-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="3676d-115">requests</span><span class="sxs-lookup"><span data-stu-id="3676d-115">requests</span></span>
* <span data-ttu-id="3676d-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="3676d-116">python-dateutil</span></span>
* <span data-ttu-id="3676d-117">pandas</span><span class="sxs-lookup"><span data-stu-id="3676d-117">pandas</span></span>

<span data-ttu-id="3676d-118">Рекомендуется с помощью распространения Python, например [Anaconda](http://continuum.io/downloads#all) или [Canopy](https://store.enthought.com/downloads/), который поставляются с Python, IPython и установить пакеты hello трех перечисленных выше.</span><span class="sxs-lookup"><span data-stu-id="3676d-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="3676d-119">Хотя использование IPython не является обязательным, это отличная среда для интерактивного управления данными и их визуализации.</span><span class="sxs-lookup"><span data-stu-id="3676d-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="3676d-120"><a name="installation"></a>Как tooinstall hello Azure Machine Learning Python клиентской библиотеки</span><span class="sxs-lookup"><span data-stu-id="3676d-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="3676d-121">Клиентская библиотека Hello Azure Machine Learning Python также должен быть установленных toocomplete hello задачи, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="3676d-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="3676d-122">Он доступен из hello [индекс пакета Python](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="3676d-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="3676d-123">tooinstall его в вашей среде Python, запустите следующую команду из локальной среды Python hello:</span><span class="sxs-lookup"><span data-stu-id="3676d-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="3676d-124">Кроме того, можно загрузить и установить из источников hello на [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="3676d-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="3676d-125">При наличии git, которые установлены на компьютере, можно использовать напрямую из репозитория git hello tooinstall PIP-адрес:</span><span class="sxs-lookup"><span data-stu-id="3676d-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="3676d-126"><a name="datasetAccess"></a>Использовать наборы данных tooaccess фрагменты кода Studio</span><span class="sxs-lookup"><span data-stu-id="3676d-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="3676d-127">Библиотека клиентов Python Hello дает существующие наборы данных tooyour программный доступ из экспериментов, которые были запущены.</span><span class="sxs-lookup"><span data-stu-id="3676d-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="3676d-128">На основе hello Studio веб-интерфейса можно создавать фрагменты кода, включающие все toodownload hello необходимые сведения и выполнить десериализацию наборы данных как объекты Pandas кадр данных на компьютере расположение.</span><span class="sxs-lookup"><span data-stu-id="3676d-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="3676d-129"><a name="security"></a>Безопасность доступа к данным</span><span class="sxs-lookup"><span data-stu-id="3676d-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="3676d-130">Здравствуйте, фрагменты кода, предоставляемые Studio для использования с hello Python клиентская библиотека включает идентификатор рабочей области и авторизации маркера.</span><span class="sxs-lookup"><span data-stu-id="3676d-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="3676d-131">Они предоставляют полный доступ tooyour рабочей и должны быть защищены, подобно паролю.</span><span class="sxs-lookup"><span data-stu-id="3676d-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="3676d-132">По соображениям безопасности функциональность фрагмент кода hello является только доступные toousers, имеющий их роли, задать в качестве **владельца** для hello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3676d-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="3676d-133">Роль пользователя отображается в студии машинного обучения Azure в hello **пользователей** в разделе **параметры**.</span><span class="sxs-lookup"><span data-stu-id="3676d-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![Безопасность][security]

<span data-ttu-id="3676d-135">Если ваша роль не задан в качестве **владельца**, можно запросить toobe повторное приглашение является владельцем, или попросите владельца hello tooprovide hello рабочей области с фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="3676d-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="3676d-136">Маркер авторизации tooobtain hello, необходимо выполнить одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="3676d-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="3676d-137">Запросите маркер у владельца.</span><span class="sxs-lookup"><span data-stu-id="3676d-137">Ask for a token from an owner.</span></span> <span data-ttu-id="3676d-138">Владельцы доступны токены авторизации hello параметры диалогового окна их рабочей области в Studio.</span><span class="sxs-lookup"><span data-stu-id="3676d-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="3676d-139">Выберите **параметры** из hello слева и щелкните **МАРКЕРАХ АВТОРИЗАЦИИ** toosee hello токены первичный и вторичный.</span><span class="sxs-lookup"><span data-stu-id="3676d-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="3676d-140">Несмотря на то, что hello первичного или вторичного авторизации маркеры hello может использоваться фрагмент кода hello, рекомендуется владельцев обмениваться только маркеры получателей авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="3676d-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![Маркеры авторизации](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="3676d-142">Попросите toorole toobe повышается владельца.</span><span class="sxs-lookup"><span data-stu-id="3676d-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="3676d-143">toodo это, текущий владелец toofirst потребностей hello рабочей области можно удалить из рабочей области hello. После этого повторно отправить приглашение tooit в качестве владельца.</span><span class="sxs-lookup"><span data-stu-id="3676d-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="3676d-144">Когда разработчики получили hello идентификатор рабочей области и авторизации токена, они являются рабочей области может tooaccess hello, используя фрагмент кода hello независимо от их роли.</span><span class="sxs-lookup"><span data-stu-id="3676d-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="3676d-145">Токены Авторизация осуществляется на hello **МАРКЕРАХ АВТОРИЗАЦИИ** в разделе **параметры**.</span><span class="sxs-lookup"><span data-stu-id="3676d-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="3676d-146">Можно создать их повторно, но эта процедура отменяет доступ toohello предыдущий маркер.</span><span class="sxs-lookup"><span data-stu-id="3676d-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="3676d-147"><a name="accessingDatasets"></a>Доступ к наборам данных из локального приложения Python</span><span class="sxs-lookup"><span data-stu-id="3676d-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="3676d-148">В студии машинного обучения, нажмите кнопку **наборы данных** hello панели навигации слева hello.</span><span class="sxs-lookup"><span data-stu-id="3676d-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="3676d-149">Выберите набор данных hello хотелось бы tooaccess.</span><span class="sxs-lookup"><span data-stu-id="3676d-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="3676d-150">Можно выбрать любой из наборов данных hello из hello **Мои наборы данных** списка или из hello **ОБРАЗЦЫ** списка.</span><span class="sxs-lookup"><span data-stu-id="3676d-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="3676d-151">На нижней панели инструментов hello нажмите **сформировать код для доступа к данным**.</span><span class="sxs-lookup"><span data-stu-id="3676d-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="3676d-152">Если данные hello в формате, несовместимые с клиентской библиотеки Python hello, данная кнопка отключена.</span><span class="sxs-lookup"><span data-stu-id="3676d-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![НАБОРЫ ДАННЫХ][datasets]
4. <span data-ttu-id="3676d-154">Выберите фрагмент кода hello в появившемся окне hello и скопируйте его в буфер обмена tooyour.</span><span class="sxs-lookup"><span data-stu-id="3676d-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![Код доступа][dataset-access-code]
5. <span data-ttu-id="3676d-156">Вставьте код hello в записной книжке hello локального приложения Python.</span><span class="sxs-lookup"><span data-stu-id="3676d-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![Заметки][ipython-dataset]

## <span data-ttu-id="3676d-158"><a name="accessingIntermediateDatasets"></a>Доступ к промежуточным наборам данных из экспериментов машинного обучения</span><span class="sxs-lookup"><span data-stu-id="3676d-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="3676d-159">После выполнения эксперимента в студии машинного обучения hello это возможных tooaccess hello промежуточных наборов данных из выходных узлов hello модулей.</span><span class="sxs-lookup"><span data-stu-id="3676d-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="3676d-160">Промежуточные наборы данных — это данные, создаваемые и используемые на промежуточных шагах после запуска инструмента моделирования.</span><span class="sxs-lookup"><span data-stu-id="3676d-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="3676d-161">Промежуточные наборов данных может осуществляться при условии, что формат данных hello совместим с клиентской библиотеки Python hello.</span><span class="sxs-lookup"><span data-stu-id="3676d-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="3676d-162">Hello поддерживаются следующие форматы (константы для них находятся в hello `azureml.DataTypeIds` класс):</span><span class="sxs-lookup"><span data-stu-id="3676d-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="3676d-163">PlainText</span><span class="sxs-lookup"><span data-stu-id="3676d-163">PlainText</span></span>
* <span data-ttu-id="3676d-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="3676d-164">GenericCSV</span></span>
* <span data-ttu-id="3676d-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="3676d-165">GenericTSV</span></span>
* <span data-ttu-id="3676d-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="3676d-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="3676d-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="3676d-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="3676d-168">Можно определить формат hello навести указатель мыши на узел модуля выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3676d-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="3676d-169">Оно отображается вместе с именем узла hello, во всплывающей подсказке.</span><span class="sxs-lookup"><span data-stu-id="3676d-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="3676d-170">Некоторые модули hello, например hello [разбиение] [ split] модуля, формат вывода tooa с именем `Dataset`, который не поддерживается клиентской библиотекой hello Python.</span><span class="sxs-lookup"><span data-stu-id="3676d-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![Формат набора данных][dataset-format]

<span data-ttu-id="3676d-172">Требуется toouse модуля преобразования [преобразовать tooCSV][convert-to-csv], tooget выходные данные в поддерживаемый формат.</span><span class="sxs-lookup"><span data-stu-id="3676d-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![Формат GenericCSV][csv-format]

<span data-ttu-id="3676d-174">Hello следующие шаги показывают пример, который создает эксперимента, он обращается к hello промежуточного набора данных.</span><span class="sxs-lookup"><span data-stu-id="3676d-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="3676d-175">Создайте новый эксперимент.</span><span class="sxs-lookup"><span data-stu-id="3676d-175">Create a new experiment.</span></span>
2. <span data-ttu-id="3676d-176">Вставьте модуль набора данных **Adult Census Income Binary Classification** .</span><span class="sxs-lookup"><span data-stu-id="3676d-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="3676d-177">Вставить [разбиение] [ split] модуля и подключите его выходные данные модуля toohello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="3676d-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="3676d-178">Вставить [преобразовать tooCSV] [ convert-to-csv] модуля и подключите его ввода tooone hello [разбиение] [ split] выводит модуля.</span><span class="sxs-lookup"><span data-stu-id="3676d-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="3676d-179">Сохраните hello эксперимент, запустите его и дождитесь ее toofinish под управлением.</span><span class="sxs-lookup"><span data-stu-id="3676d-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="3676d-180">Щелкните узел hello выходные данные на hello [преобразовать tooCSV] [ convert-to-csv] модуля.</span><span class="sxs-lookup"><span data-stu-id="3676d-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="3676d-181">В появившемся контекстном меню hello выберите **сформировать код для доступа к данным**.</span><span class="sxs-lookup"><span data-stu-id="3676d-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Контекстное меню][experiment]
8. <span data-ttu-id="3676d-183">Выберите фрагмент кода hello и скопируйте его в буфер обмена tooyour в появившемся окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="3676d-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![Код доступа][intermediate-dataset-access-code]
9. <span data-ttu-id="3676d-185">Вставьте код hello в блокноте.</span><span class="sxs-lookup"><span data-stu-id="3676d-185">Paste hello code in your notebook.</span></span>
   
    ![Заметки][ipython-intermediate-dataset]
10. <span data-ttu-id="3676d-187">Вы можете визуализировать данные hello, с помощью matplotlib.</span><span class="sxs-lookup"><span data-stu-id="3676d-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="3676d-188">Будут отображены в гистограмме для hello столбец «Возраст»:</span><span class="sxs-lookup"><span data-stu-id="3676d-188">This displays in a histogram for hello age column:</span></span>
    
    ![Гистограмма][ipython-histogram]

## <span data-ttu-id="3676d-190"><a name="clientApis"></a>Используйте hello tooaccess библиотеки Python обучения машины клиента, чтение, создание и Управление наборами данных</span><span class="sxs-lookup"><span data-stu-id="3676d-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="3676d-191">Рабочая область</span><span class="sxs-lookup"><span data-stu-id="3676d-191">Workspace</span></span>
<span data-ttu-id="3676d-192">Рабочая область Hello — hello точку входа для клиентской библиотеки Python hello.</span><span class="sxs-lookup"><span data-stu-id="3676d-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="3676d-193">Укажите hello `Workspace` экземпляра класса с вашей рабочей области идентификатора и авторизации маркера toocreate:</span><span class="sxs-lookup"><span data-stu-id="3676d-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="3676d-194">Перечисление наборов данных</span><span class="sxs-lookup"><span data-stu-id="3676d-194">Enumerate datasets</span></span>
<span data-ttu-id="3676d-195">tooenumerate всех наборов данных в данной рабочей области:</span><span class="sxs-lookup"><span data-stu-id="3676d-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="3676d-196">наборы данных tooenumerate просто hello созданные пользователем:</span><span class="sxs-lookup"><span data-stu-id="3676d-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="3676d-197">tooenumerate просто hello пример наборов данных:</span><span class="sxs-lookup"><span data-stu-id="3676d-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="3676d-198">Можно обратиться к набору данных по имени (с учетом регистра):</span><span class="sxs-lookup"><span data-stu-id="3676d-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="3676d-199">Или по индексу:</span><span class="sxs-lookup"><span data-stu-id="3676d-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="3676d-200">Метаданные</span><span class="sxs-lookup"><span data-stu-id="3676d-200">Metadata</span></span>
<span data-ttu-id="3676d-201">Наборы данных имеют метаданных, в toocontent сложения.</span><span class="sxs-lookup"><span data-stu-id="3676d-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="3676d-202">(Промежуточные наборы данных являются правило toothis исключений и не иметь все метаданные).</span><span class="sxs-lookup"><span data-stu-id="3676d-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="3676d-203">Некоторые значения метаданных назначаются пользователем hello во время создания:</span><span class="sxs-lookup"><span data-stu-id="3676d-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="3676d-204">Другие значения назначаются Машинным обучением Azure:</span><span class="sxs-lookup"><span data-stu-id="3676d-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="3676d-205">В разделе hello `SourceDataset` класс для дополнительные on hello имеющихся метаданных.</span><span class="sxs-lookup"><span data-stu-id="3676d-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="3676d-206">Чтение содержимого</span><span class="sxs-lookup"><span data-stu-id="3676d-206">Read contents</span></span>
<span data-ttu-id="3676d-207">фрагменты кода Hello, автоматически предоставляемые студии машинного обучения загрузить и выполнить десериализацию объекта кадр данных Pandas tooa dataset hello.</span><span class="sxs-lookup"><span data-stu-id="3676d-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="3676d-208">Это делается с hello `to_dataframe` метод:</span><span class="sxs-lookup"><span data-stu-id="3676d-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="3676d-209">Если предпочтение toodownload hello необработанных данных и самостоятельно выполнять десериализации hello, который является параметром.</span><span class="sxs-lookup"><span data-stu-id="3676d-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="3676d-210">В момент hello это единственная возможность hello форматы, такие как «ARFF», не удается выполнить десериализацию какие hello Python клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="3676d-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="3676d-211">содержимое hello tooread как текст:</span><span class="sxs-lookup"><span data-stu-id="3676d-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="3676d-212">содержимое tooread hello в двоичном виде:</span><span class="sxs-lookup"><span data-stu-id="3676d-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="3676d-213">Можно также просто открыть toohello содержимое потока:</span><span class="sxs-lookup"><span data-stu-id="3676d-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="3676d-214">Создание нового набора данных</span><span class="sxs-lookup"><span data-stu-id="3676d-214">Create a new dataset</span></span>
<span data-ttu-id="3676d-215">Библиотека клиентов Python Hello позволяет tooupload наборы данных из программы Python.</span><span class="sxs-lookup"><span data-stu-id="3676d-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="3676d-216">Эти наборы данных затем станут доступными для использования в вашей рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3676d-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="3676d-217">При наличии данных в кадр данных под Pandas используйте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="3676d-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="3676d-218">Если данные уже сериализованы, можно использовать:</span><span class="sxs-lookup"><span data-stu-id="3676d-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="3676d-219">Hello библиотека клиентов Python — может tooserialize toohello Pandas кадр данных следующие форматы (константы для них находятся в hello `azureml.DataTypeIds` класс):</span><span class="sxs-lookup"><span data-stu-id="3676d-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="3676d-220">PlainText</span><span class="sxs-lookup"><span data-stu-id="3676d-220">PlainText</span></span>
* <span data-ttu-id="3676d-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="3676d-221">GenericCSV</span></span>
* <span data-ttu-id="3676d-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="3676d-222">GenericTSV</span></span>
* <span data-ttu-id="3676d-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="3676d-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="3676d-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="3676d-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="3676d-225">Обновление существующего набора данных</span><span class="sxs-lookup"><span data-stu-id="3676d-225">Update an existing dataset</span></span>
<span data-ttu-id="3676d-226">При попытке tooupload новый набор данных с именем, соответствующим существующий набор данных, следует получать ошибку конфликта.</span><span class="sxs-lookup"><span data-stu-id="3676d-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="3676d-227">tooupdate существующий набор данных, необходимо сначала tooget эталонный набор данных существующего toohello:</span><span class="sxs-lookup"><span data-stu-id="3676d-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="3676d-228">Затем с помощью `update_from_dataframe` tooserialize и заменить содержимое hello hello набора данных в Azure:</span><span class="sxs-lookup"><span data-stu-id="3676d-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="3676d-229">Если требуется другой формат данных hello tooa tooserialize, укажите значение для hello необязательно `data_type_id` параметра.</span><span class="sxs-lookup"><span data-stu-id="3676d-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="3676d-230">При необходимости можно задать новое описание, указав значение для hello `description` параметра.</span><span class="sxs-lookup"><span data-stu-id="3676d-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="3676d-231">При необходимости можно задать новое имя, указав значение для hello `name` параметра.</span><span class="sxs-lookup"><span data-stu-id="3676d-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="3676d-232">Теперь вы получите hello набора данных с помощью hello только новое имя.</span><span class="sxs-lookup"><span data-stu-id="3676d-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="3676d-233">После кода Hello обновляет данные hello, имя и описание.</span><span class="sxs-lookup"><span data-stu-id="3676d-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="3676d-234">Hello `data_type_id`, `name` и `description` параметры являются необязательными и tootheir предыдущее значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3676d-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="3676d-235">Hello `dataframe` всегда является обязательным.</span><span class="sxs-lookup"><span data-stu-id="3676d-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="3676d-236">Если данные уже сериализованы, вместо `update_from_dataframe` используйте `update_from_raw_data`:</span><span class="sxs-lookup"><span data-stu-id="3676d-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="3676d-237">Он работает точно так же, просто вместо `raw_data` передается `dataframe`.</span><span class="sxs-lookup"><span data-stu-id="3676d-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

