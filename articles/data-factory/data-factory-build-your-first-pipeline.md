---
title: "Руководство по фабрике данных: первый конвейер данных | Документация Майкрософт"
description: "Этот учебник фабрики данных Azure показано, как toocreate и расписания обработки данных с помощью Hive в фабрике данных сценария в кластере Hadoop."
services: data-factory
keywords: "руководство по фабрике данных Azure, кластер hadoop, hadoop hive"
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>Учебник: Построение первые данные конвейера tootransform использование кластера Hadoop
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-build-your-first-pipeline.md)
> * [Портал Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Шаблон Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

Из этого учебника вы узнаете, как создать свою первую фабрику данных Azure, используя конвейер данных. Hello конвейера преобразует входные данные, выполнив скрипт Hive в выходных данных tooproduce кластера Azure HDInsight (Hadoop).  

Эта статья содержит обзор и необходимые компоненты для учебника hello. После завершения hello предварительные требования, можно сделать учебника hello, с помощью одного из hello следующие средства и пакеты SDK: портал Azure, Visual Studio, PowerShell, REST API диспетчера ресурсов шаблона. Выберите один из вариантов hello в раскрывающемся списке hello hello начале (или) ссылки в конце hello этого учебника hello toodo статьи с помощью одного из этих параметров.    

## <a name="tutorial-overview"></a>Обзор учебника
В этом учебнике выполните следующие шаги hello.

1. Создание **фабрики данных**. Фабрика данных может содержать один или несколько конвейеров данных для перемещения и преобразования данных. 

    В этом учебнике создается один конвейер в фабрике данных hello. 
2. Создание **конвейера**. Конвейер может включать одно или несколько действий (например, действие копирования, действие Hive HDInsight). Этот пример использует hello действие Hive в HDInsight, которое запускает сценарий Hive в кластере HDInsight Hadoop. Hello сценария сначала создается таблица, ссылки hello необработанные веб-данных журнала, хранящихся в хранилище больших двоичных объектов и затем секций hello необработанные данные за год и месяц.

    В этом учебнике конвейера hello использует данные tootransform hello действие Hive, выполнив запрос Hive в кластере Azure HDInsight Hadoop. 
3. Создание **связанных служб**. Для создания toolink связанной службы хранилища данных или фабрику вычислений toohello службы данных. Хранилище данных, таких как хранилище Azure содержит данные ввода вывода действий в конвейере hello. Служба вычислений, такая как кластер HDInsight Hadoop, обрабатывает и преобразует данные.

    В этом учебнике рассказывается о том, как создать две связанные службы: **службу хранилища Azure** и **Azure HDInsight**. Hello хранилища Azure связанные ссылки на службы, содержащий фабрики данных toohello hello ввода вывода данных учетной записи хранилища Azure. Azure HDInsight связанные ссылки службы кластера Azure HDInsight, фабрики данных toohello tootransform используемых данных. 
3. Создание входных и выходных **наборов данных**. Входной набор данных представляет hello входных данных для действия в конвейере hello и выходной набор данных представляет hello выходные данные для действия "hello".

    В данном учебнике, hello входных и выходных данных наборы данных укажите расположение входных данных и вывода данных в hello хранилища больших двоичных объектов. Hello связанной службой хранилища Azure указывает, что учетной записи хранилища Azure используется. Входной набор данных указывает, где расположены входные файлы hello и выходной набор данных указывает расположение выходных файлов hello. 


В разделе [tooAzure введение фабрики данных](data-factory-introduction.md) статье подробный обзор фабрики данных Azure.
  
Вот hello **представление диаграммы** сборки в этом учебнике фабрики данных образец hello. У **MyFirstPipeline** есть одно действие типа Hive, которое использует набор данных **AzureBlobInput** в качестве входных данных и выдает набор данных **AzureBlobOutput** в качестве выходных данных. 

![Схема в руководстве по фабрике данных](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


В этом учебнике **inputdata** папки hello **adfgetstarted** контейнера больших двоичных объектов содержит один файл с именем input.log. Этот файл журнала содержит записи за три месяца: январь, февраль и март 2016 г. Вот hello образцов строк для каждого месяца во входном файле hello. 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

При обработке файла hello hello конвейер с действиями Hive в HDInsight, действие hello запускает сценарий Hive в кластере HDInsight hello, секции входные данные за год и месяц. Hello сценарий создает три выходных данных папок, содержащих файл с записями из каждого месяца.  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

Из строк образец hello, показанном выше, hello сначала полноразмерных (2016-01-01) записывается файл 000000_0 toohello hello месяц = 1 папке. Аналогичным образом hello второй записывается файл toohello hello месяц = 2 папки и hello третий файл toohello оно записано в месяце hello = 3 папки.  

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь hello следующие предварительные требования:

1. **Подписка Azure**. Если ее нет, можно за пару минут создать бесплатную пробную учетную запись. В разделе hello [бесплатная пробная версия](https://azure.microsoft.com/pricing/free-trial/) статьи на как можно получить бесплатную пробную учетную запись.
2. **Хранилище Azure** — использовать учетную запись общего назначения стандартное хранилище Azure для хранения данных hello в этом учебнике. Если нет учетной записи общего назначения стандартное хранилище Azure, см. раздел hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи. После создания учетной записи хранилища hello запишите hello **имя учетной записи** и **ключ доступа**. См. разделы о [просмотре, копировании и повторном создании ключей доступа к хранилищу](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).
3. Загрузить и просмотреть файл запрос Hive hello (**HQL**), расположенный: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql). Этот запрос преобразует входные данные tooproduce выходных данных. 
4. Загрузите и прочтите hello пример входного файла (**input.log**), расположенный: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. Создайте контейнер больших двоичных объектов с именем **adfgetstarted** в хранилище BLOB-объектов Azure. 
6. Отправка **partitionweblogs.hql** файл toohello **сценарий** папки в hello **adfgetstarted** контейнера. Воспользуйтесь таким средством, как [Обозреватель службы хранилища Microsoft Azure](http://storageexplorer.com/). 
7. Отправка **input.log** файл toohello **inputdata** папки в hello **adfgetstarted** контейнера. 

После завершения hello необходимые компоненты, выберите один из hello следующие средства и пакеты SDK toodo hello учебника. 

- [Портал Azure](data-factory-build-your-first-pipeline-using-editor.md)
- [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [Шаблон Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
- [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

Портал Azure и Visual Studio позволяют создавать фабрики данных с помощью графического пользовательского интерфейса. PowerShell, шаблон Resource Manager и интерфейс REST API, в свою очередь, дают возможность сделать это с помощью средств создания сценариев и программирования.

> [!NOTE]
> конвейер данных Hello в этом учебнике преобразует входные данные tooproduce выходных данных. Копирует данные из источника данных хранилища tooa целевое хранилище данных. Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Вы можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Подробные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md). 





  
