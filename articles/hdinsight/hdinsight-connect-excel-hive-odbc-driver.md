---
title: "aaaConnect tooHadoop Excel с hello Hive драйвер ODBC - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как tooset копирование и использование hello драйвер Microsoft Hive ODBC для tooquery данные Excel в кластерах HDInsight из Microsoft Excel."
keywords: hadoop excel, hive excel, hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>Подключение Excel tooHadoop в Azure HDInsight с драйвером Microsoft Hive ODBC hello

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

В решении для больших данных Майкрософт компоненты Microsoft Business Intelligence (BI) интегрируется с Apache Hadoop кластеры, которые были развернуты hello Azure HDInsight. Примером такой интеграции — hello возможность tooconnect Excel toohello Hive хранилище данных кластера Hadoop в HDInsight с помощью hello драйвера Microsoft Hive Open Database Connectivity (ODBC).

Также возможно tooconnect hello данные, связанные с кластера HDInsight и другим источникам данных, включая других (отличных от HDInsight) Hadoop, кластеров из Excel с помощью hello надстройки Microsoft Power Query для Excel. Сведения об установке и использовании Power Query см. в разделе [tooHDInsight Excel подключиться с помощью Power Query][hdinsight-power-query].

> [!NOTE]
> Хотя hello шаги в этой статье может использоваться с любой ОС Linux или кластера HDInsight под управлением Windows, Windows необходима для hello клиентской рабочей станции.
> 
> 

**Предварительные требования**:

Прежде чем приступать к этой статье, необходимо иметь hello следующих элементов:

* **Кластер HDInsight**. разделе toocreate, [Приступая к работе с Azure HDInsight][hdinsight-get-started].
* **Рабочая станция** с Office 2013 профессиональный плюс, Office 365 профессиональный плюс, Excel 2013 автономный или Office 2010 профессиональный плюс.

## <a name="install-microsoft-hive-odbc-driver"></a>Установка драйвера Microsoft Hive ODBC
Загрузите и установите драйвер Microsoft ODBC Hive hello [центра загрузки Майкрософт][hive-odbc-driver-download].

Этот драйвер можно установить на 32-разрядной или 64-разрядной версии Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 и Windows Server 2012. драйвер Hello допускает подключения tooAzure HDInsight (версия 1.6 и более поздние версии) и эмулятор Azure HDInsight (v.1.0.0.0 и более поздние версии). Должны установить hello версию, соответствующую версии hello приложения hello, где использовать драйвер ODBC hello. В этом учебнике hello драйвер используется в Office Excel.

## <a name="create-hive-odbc-data-source"></a>Создание источника данных Hive ODBC
Hello следующие шаги показывают, как toocreate Hive источника данных ODBC.

1. Windows 8 или Windows 10, нажмите начальный экран приветствия Windows ключа tooopen hello, а затем введите **источники данных**.
2. Нажмите кнопку **Настройка источников данных ODBC (32-разр.)** или **Настройка источников данных ODBC (64-разр.)** в зависимости от версии Office. Если вы используете Windows 7, выберите **Источники данных ODBC (32-разр.)** или **Источники данных ODBC (64-разр.)** в разделе **Администрирование**. Вы увидите hello **администратор источников данных ODBC** диалогового окна.
   
    ![Администратор источников данных ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Настройка DSN с помощью администратора источников данных ODBC")

3. От пользователя DNS, нажмите кнопку **добавить** tooopen hello **Создание нового источника данных** мастера.
4. Выберите **Драйвер Microsoft Hive ODBC** и щелкните **Готово**. Вы увидите hello **Microsoft Hive ODBC DNS установки драйвера** диалогового окна.
5. Введите или выберите hello следующие значения:
   
   | Свойство | Description (Описание) |
   | --- | --- |
   |  Имя источника данных |Предоставьте имя источника данных tooyour |
   |  Узел |Введите &lt;имя_кластера_HDInsight>.azurehdinsight.net. Например, myHDICluster.azurehdinsight.net |
   |  Порт |Используйте <strong>443</strong>. (Этот порт был изменен из 563 too443.) |
   |  База данных |Используйте <strong>значение по умолчанию</strong>. |
   |  Механизм |Выберите <strong>Служба Azure HDInsight</strong>. |
   |  Имя пользователя |Введите имя пользователя HTTP кластера HDInsight. имя пользователя по умолчанию Hello <strong>администратора</strong>. |
   |  Пароль |Введите пароль пользователя кластера HDInsight. |
   
    </table>
   
    Существуют некоторые важные параметры toobe, учитывать при нажатии кнопки **Дополнительно**:
   
   | Параметр | Description (Описание) |
   | --- | --- |
   |  Использовать исходный запрос |При этом, драйвер ODBC hello не предпринимает tooconvert TSQL в HiveQL. Следует использовать только при 100% уверенности в отправке действительных инструкций HiveQL. При подключении tooSQL сервера или базы данных SQL Azure, следует оставить этот флажок снят. |
   |  Строки, загружаемые для каждого блока |При получении большого количества записей, настройки этого параметра может быть обязательным tooensure оптимальную производительность. |
   |  Длина столбца строки по умолчанию, длина столбца двоичного кода, масштаб столбца десятичных значений |Тип данных Hello длины и точности могут повлиять на способ возвращаются данные. Они могут вызывать toobe неверные сведения, возвращаемые из-за tooloss точности и/или усечения. |

    ![Дополнительные параметры](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Дополнительные параметры конфигурации DSN")

1. Нажмите кнопку **тест** источника данных tootest hello. При правильной настройке источника данных hello показывает *тесты успешно ЗАВЕРШЕНА!*.
2. Нажмите кнопку **ОК** tooclose hello проверить диалоговое окно. Hello нового источника данных должны отображаться на hello **администратор источников данных ODBC**.
3. Нажмите кнопку **ОК** tooexit приветствия мастера.

## <a name="import-data-into-excel-from-hdinsight"></a>Импорт данных в Excel из службы HDInsight
Hello следующие шаги описывают hello как tooimport данные из таблицы Hive в книгу Excel с использованием источника данных ODBC hello, созданную в предыдущем разделе hello.

1. Откройте новую или существующую рабочую книгу в Excel.
2. Из hello **данные** щелкните **получить данные**, нажмите кнопку **из других источников**и нажмите кнопку **из ODBC** toolaunch hello  **Мастер подключения данных**.
   
    ![Открытие мастера подключения к данным](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Открытие мастера подключения к данным")
4. Имя, созданный в последнем разделе hello источника данных выберите hello и нажмите кнопку **ОК**.
5. Введите имя пользователя Hadoop (имя по умолчанию hello-admin) и hello пароль и нажмите кнопку **Connect**.
6. В навигаторе разверните узлы **HIVE**, **по умолчанию**, выберите **hivesampletable**, а затем нажмите кнопку **Загрузить**. Он занимает несколько секунд перед импортированных tooExcel получает данные.

    ![Навигатор ODBC Hive в HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Открытие мастера подключения данных")


## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, как toouse hello данные tooretrieve драйвера Microsoft Hive ODBC из hello службы HDInsight в Excel. Аналогичным образом могут получать данные из службы HDInsight hello в базу данных SQL. Это также возможно tooupload данных в службу HDInsight. toolearn более, см.:

* [Анализ данных о задержке рейсов с помощью Hive в HDInsight][hdinsight-analyze-flight-data]
* [Отправка данных tooHDInsight][hdinsight-upload-data]
* [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


