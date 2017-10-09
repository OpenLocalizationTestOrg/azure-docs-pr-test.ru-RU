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
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>Наборы данных Access в Python с помощью клиентской библиотеки hello Azure Machine Learning Python
Предварительный просмотр Hello клиентской библиотеки Microsoft Azure Machine Learning Python можно включить безопасный доступ tooyour машинного обучения Azure наборы данных из локальной среды Python и обеспечивает создание hello и управления наборов данных в рабочей области.

В этой статье описано, как:

* установить клиентскую библиотеку hello машины обучения Python 
* доступ и загрузить наборы данных, включая инструкции по авторизации tooget tooaccess машинного обучения Azure наборы данных из локальной среды Python
* получать доступ к промежуточным наборам данных из экспериментов;
* использовать наборы данных tooenumerate библиотека клиентов Python hello, доступ к метаданным, читать содержимое hello объекта dataset, создать новые наборы данных и обновлять существующие наборы данных

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>Предварительные требования
Библиотека клиентов Python Hello был протестирован в следующих средах hello:

* Windows, Mac и Linux.
* Python 2.7, 3.3 и 3.4

Он имеет зависимость от hello следующие пакеты:

* requests
* python-dateutil
* pandas

Рекомендуется с помощью распространения Python, например [Anaconda](http://continuum.io/downloads#all) или [Canopy](https://store.enthought.com/downloads/), который поставляются с Python, IPython и установить пакеты hello трех перечисленных выше. Хотя использование IPython не является обязательным, это отличная среда для интерактивного управления данными и их визуализации.

### <a name="installation"></a>Как tooinstall hello Azure Machine Learning Python клиентской библиотеки
Клиентская библиотека Hello Azure Machine Learning Python также должен быть установленных toocomplete hello задачи, описанные в этом разделе. Он доступен из hello [индекс пакета Python](https://pypi.python.org/pypi/azureml). tooinstall его в вашей среде Python, запустите следующую команду из локальной среды Python hello:

    pip install azureml

Кроме того, можно загрузить и установить из источников hello на [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).

    python setup.py install

При наличии git, которые установлены на компьютере, можно использовать напрямую из репозитория git hello tooinstall PIP-адрес:

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>Использовать наборы данных tooaccess фрагменты кода Studio
Библиотека клиентов Python Hello дает существующие наборы данных tooyour программный доступ из экспериментов, которые были запущены.

На основе hello Studio веб-интерфейса можно создавать фрагменты кода, включающие все toodownload hello необходимые сведения и выполнить десериализацию наборы данных как объекты Pandas кадр данных на компьютере расположение.

### <a name="security"></a>Безопасность доступа к данным
Здравствуйте, фрагменты кода, предоставляемые Studio для использования с hello Python клиентская библиотека включает идентификатор рабочей области и авторизации маркера. Они предоставляют полный доступ tooyour рабочей и должны быть защищены, подобно паролю.

По соображениям безопасности функциональность фрагмент кода hello является только доступные toousers, имеющий их роли, задать в качестве **владельца** для hello рабочей области. Роль пользователя отображается в студии машинного обучения Azure в hello **пользователей** в разделе **параметры**.

![Безопасность][security]

Если ваша роль не задан в качестве **владельца**, можно запросить toobe повторное приглашение является владельцем, или попросите владельца hello tooprovide hello рабочей области с фрагмент кода hello.

Маркер авторизации tooobtain hello, необходимо выполнить одно из следующих hello:

* Запросите маркер у владельца. Владельцы доступны токены авторизации hello параметры диалогового окна их рабочей области в Studio. Выберите **параметры** из hello слева и щелкните **МАРКЕРАХ АВТОРИЗАЦИИ** toosee hello токены первичный и вторичный.  Несмотря на то, что hello первичного или вторичного авторизации маркеры hello может использоваться фрагмент кода hello, рекомендуется владельцев обмениваться только маркеры получателей авторизации hello.

![Маркеры авторизации](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* Попросите toorole toobe повышается владельца.  toodo это, текущий владелец toofirst потребностей hello рабочей области можно удалить из рабочей области hello. После этого повторно отправить приглашение tooit в качестве владельца.

Когда разработчики получили hello идентификатор рабочей области и авторизации токена, они являются рабочей области может tooaccess hello, используя фрагмент кода hello независимо от их роли.

Токены Авторизация осуществляется на hello **МАРКЕРАХ АВТОРИЗАЦИИ** в разделе **параметры**. Можно создать их повторно, но эта процедура отменяет доступ toohello предыдущий маркер.

### <a name="accessingDatasets"></a>Доступ к наборам данных из локального приложения Python
1. В студии машинного обучения, нажмите кнопку **наборы данных** hello панели навигации слева hello.
2. Выберите набор данных hello хотелось бы tooaccess. Можно выбрать любой из наборов данных hello из hello **Мои наборы данных** списка или из hello **ОБРАЗЦЫ** списка.
3. На нижней панели инструментов hello нажмите **сформировать код для доступа к данным**. Если данные hello в формате, несовместимые с клиентской библиотеки Python hello, данная кнопка отключена.
   
    ![НАБОРЫ ДАННЫХ][datasets]
4. Выберите фрагмент кода hello в появившемся окне hello и скопируйте его в буфер обмена tooyour.
   
    ![Код доступа][dataset-access-code]
5. Вставьте код hello в записной книжке hello локального приложения Python.
   
    ![Заметки][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a>Доступ к промежуточным наборам данных из экспериментов машинного обучения
После выполнения эксперимента в студии машинного обучения hello это возможных tooaccess hello промежуточных наборов данных из выходных узлов hello модулей. Промежуточные наборы данных — это данные, создаваемые и используемые на промежуточных шагах после запуска инструмента моделирования.

Промежуточные наборов данных может осуществляться при условии, что формат данных hello совместим с клиентской библиотеки Python hello.

Hello поддерживаются следующие форматы (константы для них находятся в hello `azureml.DataTypeIds` класс):

* PlainText
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

Можно определить формат hello навести указатель мыши на узел модуля выходных данных. Оно отображается вместе с именем узла hello, во всплывающей подсказке.

Некоторые модули hello, например hello [разбиение] [ split] модуля, формат вывода tooa с именем `Dataset`, который не поддерживается клиентской библиотекой hello Python.

![Формат набора данных][dataset-format]

Требуется toouse модуля преобразования [преобразовать tooCSV][convert-to-csv], tooget выходные данные в поддерживаемый формат.

![Формат GenericCSV][csv-format]

Hello следующие шаги показывают пример, который создает эксперимента, он обращается к hello промежуточного набора данных.

1. Создайте новый эксперимент.
2. Вставьте модуль набора данных **Adult Census Income Binary Classification** .
3. Вставить [разбиение] [ split] модуля и подключите его выходные данные модуля toohello входного набора данных.
4. Вставить [преобразовать tooCSV] [ convert-to-csv] модуля и подключите его ввода tooone hello [разбиение] [ split] выводит модуля.
5. Сохраните hello эксперимент, запустите его и дождитесь ее toofinish под управлением.
6. Щелкните узел hello выходные данные на hello [преобразовать tooCSV] [ convert-to-csv] модуля.
7. В появившемся контекстном меню hello выберите **сформировать код для доступа к данным**.
   
    ![Контекстное меню][experiment]
8. Выберите фрагмент кода hello и скопируйте его в буфер обмена tooyour в появившемся окне приветствия.
   
    ![Код доступа][intermediate-dataset-access-code]
9. Вставьте код hello в блокноте.
   
    ![Заметки][ipython-intermediate-dataset]
10. Вы можете визуализировать данные hello, с помощью matplotlib. Будут отображены в гистограмме для hello столбец «Возраст»:
    
    ![Гистограмма][ipython-histogram]

## <a name="clientApis"></a>Используйте hello tooaccess библиотеки Python обучения машины клиента, чтение, создание и Управление наборами данных
### <a name="workspace"></a>Рабочая область
Рабочая область Hello — hello точку входа для клиентской библиотеки Python hello. Укажите hello `Workspace` экземпляра класса с вашей рабочей области идентификатора и авторизации маркера toocreate:

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>Перечисление наборов данных
tooenumerate всех наборов данных в данной рабочей области:

    for ds in ws.datasets:
        print(ds.name)

наборы данных tooenumerate просто hello созданные пользователем:

    for ds in ws.user_datasets:
        print(ds.name)

tooenumerate просто hello пример наборов данных:

    for ds in ws.example_datasets:
        print(ds.name)

Можно обратиться к набору данных по имени (с учетом регистра):

    ds = ws.datasets['my dataset name']

Или по индексу:

    ds = ws.datasets[0]


### <a name="metadata"></a>Метаданные
Наборы данных имеют метаданных, в toocontent сложения. (Промежуточные наборы данных являются правило toothis исключений и не иметь все метаданные).

Некоторые значения метаданных назначаются пользователем hello во время создания:

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

Другие значения назначаются Машинным обучением Azure:

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

В разделе hello `SourceDataset` класс для дополнительные on hello имеющихся метаданных.

### <a name="read-contents"></a>Чтение содержимого
фрагменты кода Hello, автоматически предоставляемые студии машинного обучения загрузить и выполнить десериализацию объекта кадр данных Pandas tooa dataset hello. Это делается с hello `to_dataframe` метод:

    frame = ds.to_dataframe()

Если предпочтение toodownload hello необработанных данных и самостоятельно выполнять десериализации hello, который является параметром. В момент hello это единственная возможность hello форматы, такие как «ARFF», не удается выполнить десериализацию какие hello Python клиентской библиотеки.

содержимое hello tooread как текст:

    text_data = ds.read_as_text()

содержимое tooread hello в двоичном виде:

    binary_data = ds.read_as_binary()

Можно также просто открыть toohello содержимое потока:

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>Создание нового набора данных
Библиотека клиентов Python Hello позволяет tooupload наборы данных из программы Python. Эти наборы данных затем станут доступными для использования в вашей рабочей области.

При наличии данных в кадр данных под Pandas используйте hello, следующий код:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Если данные уже сериализованы, можно использовать:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Hello библиотека клиентов Python — может tooserialize toohello Pandas кадр данных следующие форматы (константы для них находятся в hello `azureml.DataTypeIds` класс):

* PlainText
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

### <a name="update-an-existing-dataset"></a>Обновление существующего набора данных
При попытке tooupload новый набор данных с именем, соответствующим существующий набор данных, следует получать ошибку конфликта.

tooupdate существующий набор данных, необходимо сначала tooget эталонный набор данных существующего toohello:

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Затем с помощью `update_from_dataframe` tooserialize и заменить содержимое hello hello набора данных в Azure:

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Если требуется другой формат данных hello tooa tooserialize, укажите значение для hello необязательно `data_type_id` параметра.

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

При необходимости можно задать новое описание, указав значение для hello `description` параметра.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

При необходимости можно задать новое имя, указав значение для hello `name` параметра. Теперь вы получите hello набора данных с помощью hello только новое имя. После кода Hello обновляет данные hello, имя и описание.

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

Hello `data_type_id`, `name` и `description` параметры являются необязательными и tootheir предыдущее значение по умолчанию. Hello `dataframe` всегда является обязательным.

Если данные уже сериализованы, вместо `update_from_dataframe` используйте `update_from_raw_data`: Он работает точно так же, просто вместо `raw_data` передается `dataframe`.

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

