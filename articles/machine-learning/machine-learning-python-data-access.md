---
title: "Доступ к наборам данных с помощью клиентской библиотеки Python для машинного обучения | Документация Майкрософт"
description: "Установка и использование клиентской библиотеки Python для безопасного доступа к данным Машинного обучения Azure и управления ими из локальной среды Python."
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
ms.openlocfilehash: e3ae712e0f8d386f637520fbbff4b348bc86f32d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="access-datasets-with-python-using-the-azure-machine-learning-python-client-library"></a><span data-ttu-id="f7f12-103">Доступ к наборам данных через Python с помощью клиентской библиотеки Python для машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="f7f12-103">Access datasets with Python using the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="f7f12-104">Предварительная версия клиентской библиотеки Python для машинного обучения Microsoft Azure может обеспечить безопасный доступ к наборам данных машинного обучения Azure из локальной среды Python. Она также позволяет создавать наборы данных и управлять ими в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f7f12-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="f7f12-105">В этой статье описано, как:</span><span class="sxs-lookup"><span data-stu-id="f7f12-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="f7f12-106">установить клиентскую библиотеку Python для машинного обучения;</span><span class="sxs-lookup"><span data-stu-id="f7f12-106">install the Machine Learning Python client library</span></span> 
* <span data-ttu-id="f7f12-107">обращаться к наборам данных и передавать их, включая указания по получению авторизации для доступа к наборам данных машинного обучения Azure из локальной среды Python;</span><span class="sxs-lookup"><span data-stu-id="f7f12-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="f7f12-108">получать доступ к промежуточным наборам данных из экспериментов;</span><span class="sxs-lookup"><span data-stu-id="f7f12-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="f7f12-109">использовать клиентскую библиотеку Python для перечисления наборов данных, получать доступ к метаданным, читать содержимое набора данных, создавать новые наборы данных и обновлять существующие наборы данных.</span><span class="sxs-lookup"><span data-stu-id="f7f12-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="f7f12-110"><a name="prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f7f12-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="f7f12-111">Клиентская библиотека Python была протестирована в следующих средах:</span><span class="sxs-lookup"><span data-stu-id="f7f12-111">The Python client library has been tested under the following environments:</span></span>

* <span data-ttu-id="f7f12-112">Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="f7f12-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="f7f12-113">Python 2.7, 3.3 и 3.4</span><span class="sxs-lookup"><span data-stu-id="f7f12-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="f7f12-114">Зависит от следующих пакетов:</span><span class="sxs-lookup"><span data-stu-id="f7f12-114">It has a dependency on the following packages:</span></span>

* <span data-ttu-id="f7f12-115">requests</span><span class="sxs-lookup"><span data-stu-id="f7f12-115">requests</span></span>
* <span data-ttu-id="f7f12-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="f7f12-116">python-dateutil</span></span>
* <span data-ttu-id="f7f12-117">pandas</span><span class="sxs-lookup"><span data-stu-id="f7f12-117">pandas</span></span>

<span data-ttu-id="f7f12-118">Мы рекомендуем использовать дистрибутив Python, например [Anaconda](http://continuum.io/downloads#all) или [Canopy](https://store.enthought.com/downloads/), который поставляется с Python, IPython и тремя устанавливаемыми пакетами, перечисленными выше.</span><span class="sxs-lookup"><span data-stu-id="f7f12-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span></span> <span data-ttu-id="f7f12-119">Хотя использование IPython не является обязательным, это отличная среда для интерактивного управления данными и их визуализации.</span><span class="sxs-lookup"><span data-stu-id="f7f12-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="f7f12-120"><a name="installation"></a>Как установить клиентскую библиотеку Python для Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="f7f12-120"><a name="installation"></a>How to install the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="f7f12-121">Клиентскую библиотеку Python для Машинного обучения Azure также необходимо установить для выполнения задач, описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f7f12-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span></span> <span data-ttu-id="f7f12-122">Она доступна в [каталоге пакетов Python](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="f7f12-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="f7f12-123">Чтобы установить ее в своей среде Python, выполните следующую команду в локальной среде Python:</span><span class="sxs-lookup"><span data-stu-id="f7f12-123">To install it in your Python environment, run the following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="f7f12-124">Кроме того, можно скачать и установить ее из источников на портале [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="f7f12-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="f7f12-125">Если на компьютере установлено приложение git, вы можете использовать команду pip для установки непосредственно из репозитория git:</span><span class="sxs-lookup"><span data-stu-id="f7f12-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="f7f12-126"><a name="datasetAccess"></a>Использование фрагментов кода Студии для доступа к наборам данных</span><span class="sxs-lookup"><span data-stu-id="f7f12-126"><a name="datasetAccess"></a>Use Studio Code snippets to access datasets</span></span>
<span data-ttu-id="f7f12-127">Клиентская библиотека Python обеспечивает программный доступ к существующим наборам данных от экспериментов, которые были выполнены.</span><span class="sxs-lookup"><span data-stu-id="f7f12-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="f7f12-128">С помощью веб-интерфейса Студии можно создавать фрагменты кода, содержащие все необходимые данные для скачивания и десериализации наборов данных в качестве объектов Pandas DataFrame в папку на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f7f12-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="f7f12-129"><a name="security"></a>Безопасность доступа к данным</span><span class="sxs-lookup"><span data-stu-id="f7f12-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="f7f12-130">Фрагменты кода, предоставляемые Студией для использования с клиентской библиотекой Python, включают в себя идентификатор рабочей области и маркер авторизации.</span><span class="sxs-lookup"><span data-stu-id="f7f12-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="f7f12-131">Они предоставляют полный доступ к рабочей области, и их необходимо защитить, например, паролем.</span><span class="sxs-lookup"><span data-stu-id="f7f12-131">These provide full access to your workspace and must be protected, like a password.</span></span>

<span data-ttu-id="f7f12-132">По соображениям безопасности функциональность фрагмента кода доступна только пользователям с ролью **Владелец** для рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f7f12-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span></span> <span data-ttu-id="f7f12-133">Роль пользователя отображается в Студии машинного обучения Azure на странице **Пользователи** в разделе **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="f7f12-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span></span>

![Безопасность][security]

<span data-ttu-id="f7f12-135">Если ваша роль не **Владелец**, то вы можете запросить приглашение в качестве владельца или обратиться к владельцу рабочей области за предоставлением фрагмента кода.</span><span class="sxs-lookup"><span data-stu-id="f7f12-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span></span>

<span data-ttu-id="f7f12-136">Чтобы получить маркер авторизации, выполните одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="f7f12-136">To obtain the authorization token, you can do one of the following:</span></span>

* <span data-ttu-id="f7f12-137">Запросите маркер у владельца.</span><span class="sxs-lookup"><span data-stu-id="f7f12-137">Ask for a token from an owner.</span></span> <span data-ttu-id="f7f12-138">Владельцы могут получить доступ к маркерам авторизации на странице «Параметры» своего рабочего пространства в Студии.</span><span class="sxs-lookup"><span data-stu-id="f7f12-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span></span> <span data-ttu-id="f7f12-139">Выберите **Параметры** в левой области и щелкните **Authorization tokens** (Маркеры авторизации), чтобы просмотреть основной и дополнительный маркеры.</span><span class="sxs-lookup"><span data-stu-id="f7f12-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span></span>  <span data-ttu-id="f7f12-140">Хотя в фрагменте кода могут использоваться как основные, так и дополнительные маркеры авторизации, владельцам рекомендуется предоставлять только дополнительные маркеры авторизации.</span><span class="sxs-lookup"><span data-stu-id="f7f12-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span></span>

![Маркеры авторизации](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="f7f12-142">Обратитесь за повышением уровня до роли владельца.</span><span class="sxs-lookup"><span data-stu-id="f7f12-142">Ask to be promoted to role of owner.</span></span>  <span data-ttu-id="f7f12-143">Для этого текущему владельцу рабочей области сначала необходимо удалить вас из рабочей области, а затем повторно пригласить в качестве владельца.</span><span class="sxs-lookup"><span data-stu-id="f7f12-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span></span>

<span data-ttu-id="f7f12-144">Получив идентификатор рабочей области и маркер авторизации, разработчики могут получить доступ к рабочей области с помощью фрагмента кода вне зависимости от своей роли.</span><span class="sxs-lookup"><span data-stu-id="f7f12-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span></span>

<span data-ttu-id="f7f12-145">Для управления маркерами авторизации используется раздел **Параметры** страницы **Authorization tokens** (Маркеры авторизации).</span><span class="sxs-lookup"><span data-stu-id="f7f12-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="f7f12-146">Их можно создать повторно, но эта процедура отменяет доступ для предыдущего маркера.</span><span class="sxs-lookup"><span data-stu-id="f7f12-146">You can regenerate them, but this procedure revokes access to the previous token.</span></span>

### <span data-ttu-id="f7f12-147"><a name="accessingDatasets"></a>Доступ к наборам данных из локального приложения Python</span><span class="sxs-lookup"><span data-stu-id="f7f12-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="f7f12-148">В Студии машинного обучения на панели навигации слева щелкните **НАБОРЫ ДАННЫХ** .</span><span class="sxs-lookup"><span data-stu-id="f7f12-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span></span>
2. <span data-ttu-id="f7f12-149">Выберите набор данных, к которому хотите получить доступ.</span><span class="sxs-lookup"><span data-stu-id="f7f12-149">Select the dataset you would like to access.</span></span> <span data-ttu-id="f7f12-150">Вы можете выбрать любой из наборов данных в списке **My datasets** (Мои наборы данных) или **Примеры**.</span><span class="sxs-lookup"><span data-stu-id="f7f12-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span></span>
3. <span data-ttu-id="f7f12-151">На нижней панели инструментов щелкните **Generate Data Access Code**(Создать код доступа к данным).</span><span class="sxs-lookup"><span data-stu-id="f7f12-151">From the bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="f7f12-152">Эта кнопка отключена, если данные хранятся в формате, несовместимом с клиентской библиотекой Python.</span><span class="sxs-lookup"><span data-stu-id="f7f12-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span></span>
   
    ![НАБОРЫ ДАННЫХ][datasets]
4. <span data-ttu-id="f7f12-154">Выберите фрагмент кода в появившемся окне и скопируйте его в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="f7f12-154">Select the code snippet from the window that appears and copy it to your clipboard.</span></span>
   
    ![Код доступа][dataset-access-code]
5. <span data-ttu-id="f7f12-156">Вставьте код в заметки своего локального приложения Python.</span><span class="sxs-lookup"><span data-stu-id="f7f12-156">Paste the code into the notebook of your local Python application.</span></span>
   
    ![Заметки][ipython-dataset]

## <span data-ttu-id="f7f12-158"><a name="accessingIntermediateDatasets"></a>Доступ к промежуточным наборам данных из экспериментов машинного обучения</span><span class="sxs-lookup"><span data-stu-id="f7f12-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="f7f12-159">После выполнения эксперимента в Студии машинного обучения можно получить доступ к промежуточным наборам данных из выходных узлов модулей.</span><span class="sxs-lookup"><span data-stu-id="f7f12-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span></span> <span data-ttu-id="f7f12-160">Промежуточные наборы данных — это данные, создаваемые и используемые на промежуточных шагах после запуска инструмента моделирования.</span><span class="sxs-lookup"><span data-stu-id="f7f12-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="f7f12-161">Доступ к промежуточным наборам данных можно получить при условии, что формат данных совместим с клиентской библиотекой Python.</span><span class="sxs-lookup"><span data-stu-id="f7f12-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span></span>

<span data-ttu-id="f7f12-162">Поддерживаются следующие форматы (константы для них находятся в классе `azureml.DataTypeIds` ):</span><span class="sxs-lookup"><span data-stu-id="f7f12-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="f7f12-163">PlainText</span><span class="sxs-lookup"><span data-stu-id="f7f12-163">PlainText</span></span>
* <span data-ttu-id="f7f12-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="f7f12-164">GenericCSV</span></span>
* <span data-ttu-id="f7f12-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="f7f12-165">GenericTSV</span></span>
* <span data-ttu-id="f7f12-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="f7f12-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="f7f12-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="f7f12-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="f7f12-168">Определить формат можно, наведя указатель мыши на выходной узел модуля.</span><span class="sxs-lookup"><span data-stu-id="f7f12-168">You can determine the format by hovering over a module output node.</span></span> <span data-ttu-id="f7f12-169">Он отображается во всплывающей подсказке вместе с именем узла.</span><span class="sxs-lookup"><span data-stu-id="f7f12-169">It is displayed along with the node name, in a tooltip.</span></span>

<span data-ttu-id="f7f12-170">Некоторые модули, например модуль [Разделение][split], выводят данные в формат `Dataset`, который не поддерживается клиентской библиотекой Python.</span><span class="sxs-lookup"><span data-stu-id="f7f12-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span></span>

![Формат набора данных][dataset-format]

<span data-ttu-id="f7f12-172">В этом случае требуется модуль преобразования, например [Преобразовать в CSV][convert-to-csv], чтобы получить выходные данные в поддерживаемом формате.</span><span class="sxs-lookup"><span data-stu-id="f7f12-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span></span>

![Формат GenericCSV][csv-format]

<span data-ttu-id="f7f12-174">Далее показан пример, который создает эксперимент, выполняет его и обращается к промежуточному набору данных.</span><span class="sxs-lookup"><span data-stu-id="f7f12-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span></span>

1. <span data-ttu-id="f7f12-175">Создайте новый эксперимент.</span><span class="sxs-lookup"><span data-stu-id="f7f12-175">Create a new experiment.</span></span>
2. <span data-ttu-id="f7f12-176">Вставьте модуль набора данных **Adult Census Income Binary Classification** .</span><span class="sxs-lookup"><span data-stu-id="f7f12-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="f7f12-177">Вставьте модуль [Разделение][split] и подключите к его вводу выходные данные модуля набора данных.</span><span class="sxs-lookup"><span data-stu-id="f7f12-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span></span>
4. <span data-ttu-id="f7f12-178">Вставьте модуль [Преобразовать в CSV][convert-to-csv] и подключите к его вводу выходные данные модуля набора данных [Разделение][split].</span><span class="sxs-lookup"><span data-stu-id="f7f12-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span></span>
5. <span data-ttu-id="f7f12-179">Сохраните эксперимент, выполните его и дождитесь завершения выполнения.</span><span class="sxs-lookup"><span data-stu-id="f7f12-179">Save the experiment, run it, and wait for it to finish running.</span></span>
6. <span data-ttu-id="f7f12-180">Щелкните выходной узел в модуле [Преобразовать в CSV][convert-to-csv].</span><span class="sxs-lookup"><span data-stu-id="f7f12-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="f7f12-181">В появившемся контекстном меню щелкните пункт **Generate Data Access Code** (Создать код доступа к данным).</span><span class="sxs-lookup"><span data-stu-id="f7f12-181">When the context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Контекстное меню][experiment]
8. <span data-ttu-id="f7f12-183">Выберите фрагмент кода в появившемся окне и скопируйте его в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="f7f12-183">Select the code snippet and copy it to your clipboard from the window that appears.</span></span>
   
    ![Код доступа][intermediate-dataset-access-code]
9. <span data-ttu-id="f7f12-185">Вставьте код в заметки.</span><span class="sxs-lookup"><span data-stu-id="f7f12-185">Paste the code in your notebook.</span></span>
   
    ![Заметки][ipython-intermediate-dataset]
10. <span data-ttu-id="f7f12-187">Вы можете визуализировать данные с помощью matplotlib.</span><span class="sxs-lookup"><span data-stu-id="f7f12-187">You can visualize the data using matplotlib.</span></span> <span data-ttu-id="f7f12-188">Вот как выглядит гистограмма для столбца возраста:</span><span class="sxs-lookup"><span data-stu-id="f7f12-188">This displays in a histogram for the age column:</span></span>
    
    ![Гистограмма][ipython-histogram]

## <span data-ttu-id="f7f12-190"><a name="clientApis"></a>Использование клиентской библиотеки Python для машинного обучения для осуществления доступа, чтения, создания и управления наборами данных</span><span class="sxs-lookup"><span data-stu-id="f7f12-190"><a name="clientApis"></a>Use the Machine Learning Python client library to access, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="f7f12-191">Рабочая область</span><span class="sxs-lookup"><span data-stu-id="f7f12-191">Workspace</span></span>
<span data-ttu-id="f7f12-192">Рабочая область — это точка входа для клиентской библиотеки Python.</span><span class="sxs-lookup"><span data-stu-id="f7f12-192">The workspace is the entry point for the Python client library.</span></span> <span data-ttu-id="f7f12-193">Предоставьте класс `Workspace` с идентификатором рабочей области и маркером авторизации для создания экземпляра:</span><span class="sxs-lookup"><span data-stu-id="f7f12-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="f7f12-194">Перечисление наборов данных</span><span class="sxs-lookup"><span data-stu-id="f7f12-194">Enumerate datasets</span></span>
<span data-ttu-id="f7f12-195">Для перечисления всех наборов данных в заданной рабочей области:</span><span class="sxs-lookup"><span data-stu-id="f7f12-195">To enumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="f7f12-196">Для перечисления только созданных пользователями наборов данных:</span><span class="sxs-lookup"><span data-stu-id="f7f12-196">To enumerate just the user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="f7f12-197">Для перечисления только примеров наборов данных:</span><span class="sxs-lookup"><span data-stu-id="f7f12-197">To enumerate just the example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="f7f12-198">Можно обратиться к набору данных по имени (с учетом регистра):</span><span class="sxs-lookup"><span data-stu-id="f7f12-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="f7f12-199">Или по индексу:</span><span class="sxs-lookup"><span data-stu-id="f7f12-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="f7f12-200">Метаданные</span><span class="sxs-lookup"><span data-stu-id="f7f12-200">Metadata</span></span>
<span data-ttu-id="f7f12-201">Кроме содержимого в наборах данных имеются метаданные.</span><span class="sxs-lookup"><span data-stu-id="f7f12-201">Datasets have metadata, in addition to content.</span></span> <span data-ttu-id="f7f12-202">(Промежуточные наборы данных являются исключением из этого правила и не имеют метаданных.)</span><span class="sxs-lookup"><span data-stu-id="f7f12-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span></span>

<span data-ttu-id="f7f12-203">Некоторые значения метаданных назначаются пользователем во время создания:</span><span class="sxs-lookup"><span data-stu-id="f7f12-203">Some metadata values are assigned by the user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="f7f12-204">Другие значения назначаются Машинным обучением Azure:</span><span class="sxs-lookup"><span data-stu-id="f7f12-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="f7f12-205">Дополнительную информацию о доступных метаданных см. в описании класса `SourceDataset`.</span><span class="sxs-lookup"><span data-stu-id="f7f12-205">See the `SourceDataset` class for more on the available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="f7f12-206">Чтение содержимого</span><span class="sxs-lookup"><span data-stu-id="f7f12-206">Read contents</span></span>
<span data-ttu-id="f7f12-207">Фрагменты кода, предоставляемые Студией машинного обучения, автоматически скачивают набор данных и выполняют его десериализацию в объект Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="f7f12-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span></span> <span data-ttu-id="f7f12-208">Это выполняется методом `to_dataframe` :</span><span class="sxs-lookup"><span data-stu-id="f7f12-208">This is done with the `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="f7f12-209">Если вы предпочитаете скачать необработанные данные и выполнить десериализацию вручную, это возможно.</span><span class="sxs-lookup"><span data-stu-id="f7f12-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span></span> <span data-ttu-id="f7f12-210">На данный момент это единственная возможность для таких форматов, как «ARFF», которые клиентская библиотека Python не может десериализовать.</span><span class="sxs-lookup"><span data-stu-id="f7f12-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span></span>

<span data-ttu-id="f7f12-211">Для считывания содержимого в виде текста:</span><span class="sxs-lookup"><span data-stu-id="f7f12-211">To read the contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="f7f12-212">Для считывания содержимого в виде двоичного файла:</span><span class="sxs-lookup"><span data-stu-id="f7f12-212">To read the contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="f7f12-213">Можно также просто открыть поток содержимого:</span><span class="sxs-lookup"><span data-stu-id="f7f12-213">You can also just open a stream to the contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="f7f12-214">Создание нового набора данных</span><span class="sxs-lookup"><span data-stu-id="f7f12-214">Create a new dataset</span></span>
<span data-ttu-id="f7f12-215">Клиентская библиотека Python позволяет передавать наборы данных из программы Python.</span><span class="sxs-lookup"><span data-stu-id="f7f12-215">The Python client library allows you to upload datasets from your Python program.</span></span> <span data-ttu-id="f7f12-216">Эти наборы данных затем станут доступными для использования в вашей рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f7f12-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="f7f12-217">Если данные в формате Pandas DataFrame, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="f7f12-217">If you have your data in a Pandas DataFrame, use the following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="f7f12-218">Если данные уже сериализованы, можно использовать:</span><span class="sxs-lookup"><span data-stu-id="f7f12-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="f7f12-219">Клиентская библиотека Python может сериализовать объекты Pandas DataFrame в следующие форматы (константы для них находятся в классе `azureml.DataTypeIds` ):</span><span class="sxs-lookup"><span data-stu-id="f7f12-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="f7f12-220">PlainText</span><span class="sxs-lookup"><span data-stu-id="f7f12-220">PlainText</span></span>
* <span data-ttu-id="f7f12-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="f7f12-221">GenericCSV</span></span>
* <span data-ttu-id="f7f12-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="f7f12-222">GenericTSV</span></span>
* <span data-ttu-id="f7f12-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="f7f12-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="f7f12-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="f7f12-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="f7f12-225">Обновление существующего набора данных</span><span class="sxs-lookup"><span data-stu-id="f7f12-225">Update an existing dataset</span></span>
<span data-ttu-id="f7f12-226">Если вы попытаетесь передать новый набор данных с именем, которое совпадает с именем существующего набора данных, то произойдет ошибка конфликта.</span><span class="sxs-lookup"><span data-stu-id="f7f12-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="f7f12-227">Чтобы обновить существующий набор данных, сначала необходимо получить ссылку на существующий набор данных:</span><span class="sxs-lookup"><span data-stu-id="f7f12-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="f7f12-228">Затем используйте `update_from_dataframe` для сериализации и замены содержимого набора данных в Azure:</span><span class="sxs-lookup"><span data-stu-id="f7f12-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="f7f12-229">Если вы хотите сериализовать данные в другой формат, укажите значение необязательного параметра `data_type_id` .</span><span class="sxs-lookup"><span data-stu-id="f7f12-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="f7f12-230">При необходимости можно задать новое описание, указав значение для параметра `description` .</span><span class="sxs-lookup"><span data-stu-id="f7f12-230">You can optionally set a new description by specifying a value for the `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up to feb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to feb 2015'

<span data-ttu-id="f7f12-231">Кроме того, при необходимости можно задать новое имя, указав значение для параметра `name` .</span><span class="sxs-lookup"><span data-stu-id="f7f12-231">You can optionally set a new name by specifying a value for the `name` parameter.</span></span> <span data-ttu-id="f7f12-232">Теперь вы сможете извлекать набор данных только с помощью нового имени.</span><span class="sxs-lookup"><span data-stu-id="f7f12-232">From now on, you'll retrieve the dataset using the new name only.</span></span> <span data-ttu-id="f7f12-233">Следующий код обновляет данные, имя и описание.</span><span class="sxs-lookup"><span data-stu-id="f7f12-233">The following code updates the data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up to feb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up to feb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="f7f12-234">Параметры `data_type_id`, `name` и `description` являются необязательными, и по умолчанию используются их предыдущие значения.</span><span class="sxs-lookup"><span data-stu-id="f7f12-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span></span> <span data-ttu-id="f7f12-235">Параметр `dataframe` всегда является обязательным.</span><span class="sxs-lookup"><span data-stu-id="f7f12-235">The `dataframe` parameter is always required.</span></span>

<span data-ttu-id="f7f12-236">Если данные уже сериализованы, вместо `update_from_dataframe` используйте `update_from_raw_data`:</span><span class="sxs-lookup"><span data-stu-id="f7f12-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="f7f12-237">Он работает точно так же, просто вместо `raw_data` передается `dataframe`.</span><span class="sxs-lookup"><span data-stu-id="f7f12-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

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

