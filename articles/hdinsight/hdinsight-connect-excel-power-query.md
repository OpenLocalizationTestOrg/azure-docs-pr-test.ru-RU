---
title: "aaaConnect tooHadoop Excel с помощью Power Query - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как сохранить преимущества tootake компонентов бизнес-аналитики и используйте Power Query для Excel tooaccess данных в Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>Подключение Excel tooHadoop с помощью Power Query
Одна важная особенность решения для больших данных Майкрософт hello — hello интеграции компонентов бизнес-аналитики (BI) Майкрософт с кластерами Hadoop в Azure HDInsight. Основной пример — hello возможность tooconnect Excel toohello учетной записи хранилища Azure, которая содержит hello данных, связанной с кластером Hadoop с помощью надстройки Excel для hello Microsoft Power Query. В этой статье описывается управление tooset копирование и использование Power Query tooquery данные, связанные с кластеру с HDInsight.

### <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь hello следующих элементов:

* **Кластер HDInsight**. разделе tooconfigure, [Приступая к работе с Azure HDInsight][hdinsight-get-started].
* **Рабочая станция** под управлением Windows 7, Windows Server 2008 R2 или последующих версий операционной системы.
* **Office 2016, Office 2013 профессиональный плюс, Office 365 профессиональный плюс, Excel 2013 автономный или Office профессиональный плюс 2010**.

## <a name="install-power-query"></a>Установка Power Query
Power Query может импортировать данные, которые были выведены или созданы заданием Hadoop, выполняющимся в кластере HDInsight.

В Excel 2016 Power Query встроено в ленте данных hello в разделе hello Get и преобразование раздела. Для более старых версиях Excel, загрузите Microsoft Power Query для Excel с hello [центра загрузки Майкрософт] [ powerquery-download] и установить его.

## <a name="import-hdinsight-data-into-excel"></a>Импорт данных HDInsight в Excel
Hello надстройка Power Query для Excel позволяет легко tooimport данные из кластера HDInsight в Excel, где средств бизнес-Аналитики, такие как PowerPivot и Power карты могут быть используется tooinspect, анализа и представления данных hello.

**tooimport данные из кластера HDInsight**

1. Откройте Excel.
2. Создайте новую пустую книгу.
3. Выполните следующие действия в зависимости от версии Excel hello hello.

    - Excel 2016

        - Нажмите кнопку hello **данные** меню, нажмите кнопку **получить данные** из hello **получения и преобразования данных** ленты, нажмите кнопку **из Azure**и нажмите кнопку  **Из Azure HDInsight(HDFS)**.

        ![HDI.PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013 или 2010

        - Щелкните hello **Power Query** меню, нажмите кнопку **из Azure**, а затем нажмите кнопку **из Microsoft Azure HDInsight**.
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Примечание:** Если вы не видите hello **Power Query** меню перейдите слишком**файл** > **параметры** > **Add-Ins**и выберите **надстройки COM** из раскрывающегося списка hello **управление** в нижней части вкладки hello страницы приветствия. Выберите hello **перейдите...**  кнопку и убедитесь в этом окне приветствия, для проверки hello Power Query для надстройки Excel.
       
        **Примечание:** Power Query также позволяет tooimport данных из HDFS, щелкнув **из других источников**.
4. Для **имя учетной записи**, введите имя учетной записи хранилища больших двоичных объектов Azure hello связанной с кластером hello и нажмите кнопку **ОК**. Эта учетная запись может быть hello [учетная запись хранения по умолчанию](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) или связанной учетной записи хранения.  Формат Hello *https://&lt;StorageAccountName >.blob.core.windows.net/*.
5. Для **ключ учетной записи**, введите ключ hello для hello учетной записи хранилища больших двоичных объектов и нажмите кнопку **Сохранить**. (Требуется только hello сведения учетной записи tooenter hello первого просмотра этого хранилища.)
6. В hello **Навигатор** панели hello левой части редактора запросов hello, дважды щелкните имя контейнера хранилища больших двоичных объектов hello. По умолчанию имя контейнера hello hello таким же именем, как имя кластера hello.
7. Найдите **HiveSampleData.txt** в hello **имя** столбца (путь к папке hello **... hive, хранилища и hivesampletable/**), а затем нажмите кнопку **двоичных** hello левой стороны HiveSampleData.txt. HiveSampleData.txt поставляется с всех кластеров hello. При необходимости можно использовать собственный файл.
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. Если требуется, можно переименовать hello имена столбцов. Когда будете готовы, щелкните **Закрыть и загрузить**.  Hello данных был загружен tooyour книги.
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, как toouse tooretrieve данные Power Query из HDInsight в Excel. Аналогичным образом можно извлекать данные из HDInsight в SQL Azure. Это также возможно tooupload данных в HDInsight. toolearn более, см. следующие статьи hello.

* [Связь с hello Hive драйвер ODBC для Microsoft Excel tooHDInsight][hdinsight-ODBC]
* [Отправка данных tooHDInsight][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
