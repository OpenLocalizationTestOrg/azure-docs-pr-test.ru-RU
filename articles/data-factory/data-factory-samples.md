---
title: "aaaAzure фабрика данных — примеры"
description: "Сведения об образцах, которые поставляются вместе с hello служба фабрики данных Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Фабрика данных Azure — примеры
## <a name="samples-on-github"></a>Примеры на GitHub
Hello [репозитория GitHub Azure-DataFactory](https://github.com/azure/azure-datafactory) содержит несколько примеров, которые помогут быстро ramp up, со службой фабрики данных Azure (или) измените hello скрипты и использовать его в собственные приложения. Папка Samples\JSON Hello содержит фрагменты JSON для распространенных сценариев.

| Образец | Описание |
|:--- |:--- |
| [Пошаговое руководство по ADF](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |Этот образец предоставляет начала до конца пошагового руководства для обработки файлов журнала с помощью фабрики данных Azure tooturn данных из файлов журналов в tooinsights. <br/><br/>В этом пошаговом руководстве hello конвейера фабрики данных собирает журналы образца, процессы и обогащает hello данных из журналов с помощью эталонных данных и преобразует hello данных tooevaluate hello эффективности маркетинговой кампании, недавно было запущено. |
| [Примеры JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |В этой выборке представлены примеры кода JSON для распространенных сценариев. |
| [Пример загрузчика данных HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |Этот образец демонстрирует загрузку данных из tooAzure конечной точки HTTP хранилища больших двоичных объектов с помощью настраиваемых действий .NET. |
| [Пример действия перекрестного домена приложения .NET](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Этот образец позволяет tooauthor пользовательское действие .NET, который не ограничен tooassembly версии, используемые hello ADF запуска (например, WindowsAzure.Storage версии 4.3.0, Newtonsoft.Json v6.0.x, и т. д.). |
| [Запуск сценария R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |Этот пример включает пользовательское действие фабрики данных hello, которое можно использовать tooinvoke RScript.exe. Этот пример работает только с вашим собственным кластером HDInsight (не по требованию), в которое уже установлен R. |
| [Вызов заданий Spark в кластере HDInsight Hadoop](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |В этом примере показано, как tooinvoke действие MapReduce toouse программы Spark. Программа Hello spark просто копирует данные из одного tooanother контейнер больших двоичных объектов Azure. |
| [Анализ Twitter с использованием действия пакетной оценки показателей машинного обучения Azure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |В этом примере показано, как модель tooinvoke AzureMLBatchScoringActivity toouse машинного обучения Microsoft Azure, выполняет анализ мнений twitter, оценки, прогноз и т. д. |
| [Анализ Twitter с использованием настраиваемого действия](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |В этом примере показано, как пользовательские действия tooinvoke .NET модель машинного обучения Azure, которая выполняет toouse twitter анализ мнений, оценки, прогноз и т. д. |
| [Параметризованные конвейеры для машинного обучения Azure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |Образец Hello предоставляет конца в конец C# кода toodeploy N конвейеры для оценки и переподготовки, каждый из которых параметр другой регион, где hello список регионов поступает из файла parameters.txt, который входит в состав этого образца. |
| [Обновление эталонных данных для заданий в службе Azure Stream Analytics](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |В этом примере показано, как обновление toouse фабрики данных Azure и Azure Stream Analytics вместе toorun hello запросы с hello данных и установки ссылку для ссылочных данных по расписанию. |
| [Гибридный конвейер с локальным кластером Hadoop Hortonworks](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |Образец Hello использует локального кластера Hadoop в качестве целевой вычислений для выполнения заданий в фабрике данных так же, как другие целевые объекты вычислений необходимо добавить как HDInsight на основе кластеров Hadoop в облаке. |
| [Средство преобразования JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |Это средство позволяет tooconvert JSONs из предыдущих too2015-07-01-preview toolatest версии или 2015-07-01-preview (по умолчанию). |
| [Пример входного файла U-SQL](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |Это пример файла, который используется действием U-SQL. |
| [Удаление файла большого двоичного объекта](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | Этот пример демонстрирует файл C#, который может использоваться как часть ADF пользовательские .net действия toodelete файлы из источника hello расположение BLOB-объектов Azure, после копирования файлов hello.|

## <a name="azure-resource-manager-templates"></a>Шаблоны диспетчера ресурсов Azure
Можно найти следующие шаблоны диспетчера ресурсов Azure для фабрики данных на сайте GitHub hello.

| Шаблон | Описание |
| --- | --- |
| [Скопируйте из tooAzure хранилища больших двоичных объектов базы данных SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |При развертывании этого шаблона создается фабрикой данных Azure с конвейером, что копирует данные из hello указано базы данных Azure SQL toohello хранилища BLOB-объектов Azure |
| [Скопируйте из Salesforce tooAzure хранилища больших двоичных объектов](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |При развертывании этого шаблона создается фабрикой данных Azure с конвейером, что копирует данные из hello указано хранилище больших двоичных объектов toohello учетной записи Salesforce. |
| [Преобразование данных путем запуска сценария Hive в кластере Azure HDInsight](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |При развертывании этого шаблона создается фабрикой данных Azure с конвейером преобразования данных, запустив скрипт Hive образец hello на кластере Azure HDInsight Hadoop. |

## <a name="samples-in-azure-portal"></a>Примеры на портале Azure
Можно использовать hello **образец конвейеры** плитки на домашней странице hello конвейеры образец toodeploy фабрики данных и их связанные сущности (наборы данных и связанных служб) в фабрике данных tooyour.

1. Создайте или откройте существующую фабрику данных. В разделе [копирования данных из хранилища больших двоичных объектов tooSQL базы данных с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для действия toocreate фабрики данных.
2. В hello **ФАБРИКИ данных** колонке hello фабрики данных, нажмите кнопку hello **образец конвейеры** плитки.

    ![Плитка "Примеры конвейеров"](./media/data-factory-samples/SamplePipelinesTile.png)
3. В hello **образец конвейеры** колонка, щелкните hello **образец** нужных toodeploy.

    ![Колонка "Примеры конвейеров"](./media/data-factory-samples/SampleTile.png)
4. Укажите параметры конфигурации для образца hello. Например, вы можете указать имя и ключ вашей учетной записи хранения Azure, имя сервера SQL Azure, базу данных, идентификатор пользователя, пароль и т. д.

    ![Колонка примера](./media/data-factory-samples/SampleBlade.png)
5. После завершения задание параметров конфигурации hello, нажмите кнопку **создать** toocreate и развертывания hello образец конвейеров и связанных служб и таблицы, используемые конвейеры hello.
6. Вы видите hello состояние развертывания на плитке образец hello вы перешли ранее hello **образец конвейеры** колонку.

    ![Состояния развертывания](./media/data-factory-samples/DeploymentStatus.png)
7. При появлении hello **успешно развернуто** сообщение hello плитки для образца hello, закрыть hello **образец конвейеры** колонку.  
8. На **ФАБРИКИ данных** колонке вы видите, что связанные службы, наборов данных и конвейеры добавляются tooyour фабрики данных.  

    ![Колонка "Фабрика данных"](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Примеры в Visual Studio
### <a name="prerequisites"></a>Предварительные требования
Необходимо иметь следующие hello, установленной на компьютере.

* Visual Studio 2013 или Visual Studio 2015.
* Загрузите пакет SDK Azure для Visual Studio 2013 или Visual Studio 2015. Перейдите в слишком[странице загрузки Azure](https://azure.microsoft.com/downloads/) и нажмите кнопку **VS 2013** или **VS 2015** в hello **.NET** раздела.
* Загрузите hello последнюю фабрики данных Azure, подключаемый модуль для Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) или [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Если вы используете Visual Studio 2013, можно также обновить hello подключаемого модуля, выполнив следующие шаги hello: hello меню **средства** -> **расширения и обновления**  ->  **Online** -> **коллекции Visual Studio** -> **средства фабрики данных Microsoft Azure для Visual Studio**  ->  **Обновление**.

### <a name="use-data-factory-templates"></a>Использование шаблонов фабрики данных
1. Нажмите кнопку **файл** hello меню выберите слишком**New**и нажмите кнопку **проекта**.
2. В hello **новый проект** диалогового окна поле, hello следующие действия:

   1. Выберите **Фабрика данных** в разделе **Шаблоны**.
   2. Выберите **шаблоны фабрики данных** hello правой панели.
   3. Введите **имя** для проекта hello.
   4. Выберите **расположение** для проекта hello.
   5. Нажмите кнопку **ОК**.

      ![Диалоговое окно "Новый проект"](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. В hello **шаблоны фабрики данных** диалоговое окно, выберите hello образец шаблона из hello **вариант использования шаблонов** и нажмите кнопку **Далее**. Hello следующее пошаговыми руководствами с помощью hello **профилирование клиента** шаблона. Шаги похожи для hello других примеров.

    ![Диалоговое окно "Шаблоны фабрики данных"](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. В hello **конфигурации фабрики данных** диалоговое окно, нажмите кнопку **Далее** на hello **основы фабрики данных** страницы.
5. На hello **фабрики данных Настройка** страницы, hello следующие действия:
   1. Выберите элемент **Create New Data Factory** (Создать фабрику данных). Можно также выбрать **Использовать существующую фабрику данных**.
   2. Введите **имя** для фабрики данных hello.
   3. Выберите hello **подписки Azure** , необходимо hello данных фабрики toobe создан.
   4. Выберите hello **группы ресурсов** для фабрики данных hello.
   5. Выберите hello **Запад США**, **Восток США**, или **Северной Европе** для hello **области**.
   6. Щелкните **Далее**.
6. В hello **Настройка хранилищ данных** укажите существующий **базы данных Azure SQL** и **учетной записи хранилища Azure** (или) Создание базы данных и хранилища и нажмите кнопку Далее.
7. В hello **Настройка вычислений** выберите значения по умолчанию и нажмите кнопку **Далее**.
8. В hello **Сводка** , просмотрите все параметры и нажмите кнопку **Далее**.
9. В hello **состояние развертывания** страницы, дождитесь завершения развертывания hello и нажмите кнопку **Готово**.
10. Щелкните правой кнопкой мыши проект в обозревателе решений hello и нажмите кнопку **публикации**.
11. Если вы видите **входа в учетную запись Майкрософт tooyour** диалоговое окно, введите свои учетные данные для hello учетной записи, имеющей подписку Azure и нажмите кнопку **входа**.
12. Вы должны увидеть следующие диалоговое окно приветствия.

    ![Диалоговое окно "Опубликовать"](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. В hello **фабрики данных Настройка** страницы, hello следующие действия:

    1. Убедитесь, что выбран параметр **Use existing data factory** (Использовать существующую фабрику данных).
    2. Выберите hello **фабрики данных** бы select при использовании шаблона hello.
    3. Нажмите кнопку **Далее** tooswitch toohello **публиковать элементы** страницы. (Нажмите клавишу **ВКЛАДКЕ** toomove из hello имя поля tooif hello **Далее** кнопка отключена.)
14. В hello **публиковать элементы** убедитесь, что все hello фабрик данных сущностей установлены и нажмите кнопку **Далее** tooswitch toohello **Сводка** страницы.     
15. Просмотрите hello сводки и нажмите кнопку **Далее** toostart hello развертывания процесса и представление hello **состояние развертывания**.
16. В hello **состояние развертывания** страницы, вы увидите hello состояние процесса развертывания hello. После завершения развертывания hello, нажмите кнопку "Готово".

В разделе [построение первой фабрики данных (Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md) подробные сведения об использовании Visual Studio tooauthor фабрики данных сущностей и их публикации tooAzure.          
