---
title: "сценарии aaaDevelop U-SQL с помощью средств Озера данных для Visual Studio | Документы Microsoft"
description: "Узнайте, как Озера данных tooinstall Tools для Visual Studio и как toodevelop и тестирования сценарии U-SQL."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>Разработка скриптов U-SQL с помощью средств Data Lake для Visual Studio
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


Узнайте, как учетные записи аналитики Озера данных Azure toocreate Visual Studio toouse, определить заданий в [U-SQL](data-lake-analytics-u-sql-get-started.md)и служба аналитики Озера данных toohello задания отправки. Дополнительные сведения о Data Lake Analytics см. в [обзоре Azure Data Lake Analytics](data-lake-analytics-overview.md).


## <a name="prerequisites"></a>Предварительные требования

* **Visual Studio**: поддерживаются все выпуски, кроме Express.
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **Microsoft Azure SDK для .NET** (версии 2.7.1 или выше).  Установите его с помощью hello [установщика веб-платформы](http://www.microsoft.com/web/downloads/platform.aspx).
* Учетная запись **Data Lake Analytics**. в разделе toocreate учетную запись, [Приступая к работе с аналитики Озера данных Azure, с помощью портала Azure](data-lake-analytics-get-started-portal.md).

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>Установка средств Azure Data Lake для Visual Studio 

Загрузите и установите средства Озера данных Azure для Visual Studio [из центра загрузки Майкрософт hello](http://aka.ms/adltoolsvs). После установки обратите внимание на следующее:
* Hello **обозревателя серверов** > **Azure** узел содержит **аналитики Озера данных** узла. 
* Hello **средства** меню содержит **Озера данных** элемента.

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Учетная запись аналитики Озера данных Azure tooan подключения

1. Откройте Visual Studio.
2. Откройте обозреватель сервера, последовательно выбрав пункты **Представление** > **Обозреватель сервера**.
3. Щелкните правой кнопкой мыши **Azure**. Выберите **подключения tooMicrosoft подписки Azure** и следуйте инструкциям, hello.
4. В обозревателе сервера последовательно выберите пункты **Azure** > **Data Lake Analytics**. Отобразится список учетных записей Data Lake Analytics.


## <a name="write-your-first-u-sql-script"></a>Создание первого скрипта U-SQL

После текста Hello является простой скрипт U-SQL. Он определяет небольшой набор данных и записи, которые вызваны хранилища Озера данных по умолчанию toohello набора данных в формате `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a>Отправка задания аналитики озера данных

1. Выберите **Файл** > **Создать** > **Проект**.

2. Выберите hello **проекта U-SQL** введите и нажмите кнопку **ОК**. Visual Studio создаст решение с помощью файла **Script.usql**.

3. Вставьте предыдущий сценарий hello в hello **Script.usql** окна.

4. В левом верхнем углу hello hello **Script.usql** окна, укажите учетную запись аналитики Озера данных hello.

    ![Отправка проекта U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. В левом верхнем углу hello hello **Script.usql** выберите **отправить**.
6. Проверьте hello **учетной записи аналитики**и выберите **отправить**. Результаты отправки доступны в hello средств Озера данных для Visual Studio результаты после завершения отправки hello.

    ![Отправка проекта U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello последние задания состояния и обновить hello экрана, нажмите кнопку **обновление**. При успешном завершении задания hello, он показывает hello **схемы заданий**, **операций с метаданными**, **журнал состояний**, и **диагностики**:

    ![График выполнения задания аналитики озера данных U-SQL в Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **Сводка заданий** показано hello Сводка hello задания.   
   * **Сведения о задании** показывает более конкретные сведения о задании hello, включая сценарий hello, ресурсы и вершин.
   * **График задания** визуализирует hello ход выполнения задания hello.
   * **Операций с метаданными** показывает все hello действия, которые были выполнены на каталог hello U-SQL.
   * **Данные** показывает все hello входов и выходов.
   * В окне **Диагностика** представлены данные расширенного анализа для выполнения задания и оптимизации производительности.

### <a name="toocheck-job-state"></a>состояние задания toocheck

1. В обозревателе сервера последовательно выберите пункты **Azure** > **Data Lake Analytics**. 
2. Разверните имя учетной записи аналитики Озера данных hello.
3. Дважды щелкните **Задания**.
4. Выберите ранее отправленного задания hello.

### <a name="toosee-hello-output-of-a-job"></a>toosee hello выходных данных задания

1. В обозревателе серверов Обзор toohello задание, которое вы отправили.
2. Нажмите кнопку hello **данные** вкладки.
3. В hello **выходных данных задания** вкладке, выберите hello `"/data.csv"` файла.

## <a name="next-steps"></a>Дальнейшие действия

* [Тестирование и отладка заданий U-SQL с помощью локального выполнения и пакета SDK U-SQL для Azure Data Lake](data-lake-analytics-data-lake-tools-local-run.md)
* [Отладка заданий U-SQL](data-lake-analytics-debug-u-sql-jobs.md)
* [Используйте средства Озера данных Azure hello для кода Visual Studio](data-lake-analytics-data-lake-tools-for-vscode.md)
