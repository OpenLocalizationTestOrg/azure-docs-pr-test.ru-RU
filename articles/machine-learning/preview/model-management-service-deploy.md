---
title: "Развертывание веб-службы управления моделями Машинного обучения Azure | Документация Майкрософт"
description: "В этом документе описываются шаги, связанные с развертыванием модели машинного обучения с использованием службы управления моделями Машинного обучения Azure."
services: machine-learning
author: raymondl
ms.author: raymondl, aashishb
manager: neerajkh
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 01/03/2018
ms.openlocfilehash: 965e33f3c7d050dca8f6c4e92d75cb7c7a8fa60d
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2018
---
# <a name="deploying-a-machine-learning-model-as-a-web-service"></a>Развертывание модели машинного обучения в качестве веб-службы

Служба управления моделями Машинного обучения Azure предоставляет интерфейсы для развертывания моделей в виде контейнерных веб-служб на основе Docker. Вы можете развернуть созданные модели с помощью таких платформ, как Spark, Microsoft Cognitive Toolkit (CNTK), Keras, Tensorflow и Python. 

В этом документе рассматриваются действия по развертыванию модели в виде веб-службы с помощью интерфейса командной строки службы управления моделями Машинного обучения Azure.

## <a name="deploying-web-services"></a>Развертывание веб-служб
С помощью интерфейсов командной строки можно развернуть веб-службы для запуска на локальном компьютере или в кластере.

Мы советуем начинать с локального развертывания. Сначала убедитесь, что модель и код работают, а затем разверните веб-службу в кластер для использования в производственных масштабах. Дополнительные сведения о настройке среды для развертывания кластера см. в статье [Установка службы управления моделями](deployment-setup-configuration.md). 

Ниже приведены действия по развертыванию.
1. Использование сохраненной обученной модели машинного обучения.
2. Создание схемы для входных и выходных данных веб-службы.
3. Создание образа контейнера на основе Docker
4. Создание и развертывание веб-службы

### <a name="1-save-your-model"></a>1. Сохранение модели
Начните с сохраненного файла обученной модели, например mymodel.pkl. Расширение файла зависит от платформы, которая используется для обучения и сохранения модели. 

Например, можно использовать библиотеку Python Pickle, чтобы сохранить обученную модель в файл. Ниже приведен [пример](http://scikit-learn.org/stable/modules/model_persistence.html) использования набора данных Iris:

```python
import pickle
from sklearn import datasets
iris = datasets.load_iris()
X, y = iris.data, iris.target
clf = linear_model.LogisticRegression()
clf.fit(X, y)  
saved_model = pickle.dumps(clf)
```

### <a name="2-create-a-schemajson-file"></a>2. Создание файла schema.json
Этот шаг не является обязательным. 

Создайте схему для автоматической проверки входных и выходных данных веб-службы. Интерфейс командной строки также использует схему для создания документа Swagger для веб-службы.

Чтобы создать схему, импортируйте следующие библиотеки:

```python
from azureml.api.schema.dataTypes import DataTypes
from azureml.api.schema.sampleDefinition import SampleDefinition
from azureml.api.realtime.services import generate_schema
```
Затем определите входные переменные, например кадр данных Spark, кадр данных Pandas или массив NumPy. В следующем примере используется массив NumPy.

```python
inputs = {"input_array": SampleDefinition(DataTypes.NUMPY, yourinputarray)}
generate_schema(run_func=run, inputs=inputs, filepath='service_schema.json')
```
В следующем примере используется кадр данных Spark.

```python
inputs = {"input_df": SampleDefinition(DataTypes.SPARK, yourinputdataframe)}
generate_schema(run_func=run, inputs=inputs, filepath='service_schema.json')
```

В следующем примере используется кадр данных Pandas.

```python
inputs = {"input_df": SampleDefinition(DataTypes.PANDAS, yourinputdataframe)}
generate_schema(run_func=run, inputs=inputs, filepath='service_schema.json')
```

### <a name="3-create-a-scorepy-file"></a>3. Создание файла score.py
Предоставьте файл score.py, который загружает модель и возвращает результаты прогноза с помощью модели.

Файл должен содержать две функции: init и run.

Добавьте следующий код в верхнюю часть файла score.py для включения функции сбора данных, которая позволяет собирать входные данные модели и данные прогнозирования.

```python
from azureml.datacollector import ModelDataCollector
```

Дополнительные сведения о том, как использовать эту функцию, см. в разделе [Сбор данных модели](how-to-use-model-data-collection.md).

#### <a name="init-function"></a>Функция Init
Используйте функцию init для загрузки сохраненной модели.

Пример простой функции init, выполняющей загрузку модели данных.

```python
def init():  
    from sklearn.externals import joblib
    global model, inputs_dc, prediction_dc
    model = joblib.load('model.pkl')

    inputs_dc = ModelDataCollector('model.pkl',identifier="inputs")
    prediction_dc = ModelDataCollector('model.pkl', identifier="prediction")
```

#### <a name="run-function"></a>Функция run
Функция run использует модель и входные данные, чтобы вернуть прогноз.

Пример простой функции run, которая обрабатывает входные данные и возвращает результат прогнозирования:

```python
def run(input_df):
    global clf2, inputs_dc, prediction_dc
    try:
        prediction = model.predict(input_df)
        inputs_dc.collect(input_df)
        prediction_dc.collect(prediction)
        return prediction
    except Exception as e:
        return (str(e))
```

### <a name="4-register-a-model"></a>4. Регистрация модели
Следующая команда используется для регистрации модели, созданной на шаге 1.

```
az ml model register --model [path to model file] --name [model name]
```

### <a name="5-create-manifest"></a>5. Создание манифеста
Следующая команда помогает создать манифест для модели.

```
az ml manifest create --manifest-name [your new manifest name] -f [path to code file] -r [runtime for the image, e.g. spark-py]
```
Вы можете добавить ранее зарегистрированную модель в манифест, используя аргумент `--model-id` или `-i` в команде, показанной выше. С помощью дополнительных аргументов "-i" можно указать несколько моделей.

### <a name="6-create-an-image"></a>6. Создание образа 
Можно создать образ с возможностью предварительного создания манифеста. 

```
az ml image create -n [image name] -manifest-id [the manifest ID]
```

Или же создать манифест и образ одной командой. 

```
az ml image create -n [image name] --model-file [model file or folder path] -f [code file, e.g. the score.py file] -r [the runtime eg.g. spark-py which is the Docker container image base]
```

>[!NOTE]
>Для получения более подробной информации о параметрах команды введите -h в конце команды, например az ml image create -h.


### <a name="7-create-and-deploy-the-web-service"></a>7. Создание и развертывание веб-службы
Разверните службу, используя следующую команду:

```
az ml service create realtime --image-id <image id> -n <service name>
```

>[!NOTE] 
>Вы можете также использовать одну команду для выполнения четырех предыдущих шагов. Используйте -h с командой service create, чтобы получить более подробные сведения.

### <a name="8-test-the-service"></a>8. Тестирование службы
Чтобы получить сведения о том, как вызвать службу, выполните следующую команду:

```
az ml service usage realtime -i <service id>
```

Вызовите службу из командной строки, используя функцию run:

```
az ml service run realtime -i <service id> -d "{\"input_df\": [INPUT DATA]}"
```

В следующем примере вызывается пример веб-службы Iris:

```
az ml service run realtime -i <service id> -d "{\"input_df\": [{\"sepal length\": 3.0, \"sepal width\": 3.6, \"petal width\": 1.3, \"petal length\":0.25}]}"
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы протестировали веб-службу в локальной среде, ее можно развернуть в кластере для крупномасштабного использования. Дополнительные сведения о настройке кластера для развертывания веб-службы см. в статье [Установка службы управления моделями](deployment-setup-configuration.md). 
