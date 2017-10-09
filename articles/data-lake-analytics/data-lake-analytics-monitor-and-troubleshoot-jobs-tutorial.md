---
title: "задания aaaTroubleshoot аналитики Озера данных Azure, с помощью портала Azure | Документы Microsoft"
description: "Узнайте, как toouse hello задания аналитики Озера данных tootroubleshoot портала Azure. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>Устранение неполадок с заданиями аналитики озера данных Azure с помощью портала Azure
Узнайте, как toouse hello задания аналитики Озера данных tootroubleshoot портала Azure.

В этом учебнике будет настроить проблемы отсутствующего файла источника и использовать hello портала Azure tootroubleshoot hello проблему.

## <a name="submit-a-data-lake-analytics-job"></a>Отправка задания аналитики озера данных

Отправьте hello после задания U-SQL:

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
Hello является исходным файлом, определенных в скрипте hello **/Samples/Data/SearchLog.tsv1**, где она должна быть **/Samples/Data/SearchLog.tsv**.


## <a name="troubleshoot-hello-job"></a>Диагностика заданий hello

**toosee все hello заданий**

1. Hello портал Azure, щелкните **Microsoft Azure** в верхнем левом углу hello.
2. Щелкните плитку hello имя вашей учетной записи аналитики Озера данных.  Сводка по заданию Hello отображается на hello **управление заданиями** плитки.

    ![Аналитика озера данных Azure: управление заданиями](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    Задание Hello управления позволяет быстро hello состояние задания. Обратите внимание, что здесь имеется задание, завершившееся сбоем.
3. Нажмите кнопку hello **управление заданиями** плитки toosee hello заданий. задания Hello разделены на **под управлением**, **в очереди**, и **завершено**. Вы увидите сбоя задания в hello **завершено** раздела. Это должен быть первый в списке hello. Если у вас много заданий, можно щелкнуть **фильтра** toohelp вы toolocate заданий.

    ![Аналитика озера данных Azure: фильтрация заданий](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. Щелкните hello невыполненного задания с hello tooopen список hello сведений о задании в Новая колонка:

    ![Аналитика озера данных Azure: невыполненное задание](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    Обратите внимание hello **повторно отправить** кнопки. После устранения проблемы hello, можно повторно отправить задания hello.
5. Щелкните выделенную часть из hello предыдущего экрана tooopen hello сведения об ошибке.  Отобразится примерно следующий текст:

    ![Аналитика озера данных Azure: сведения о невыполненном задании](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    Оно сообщает, что исходная папка hello не найден.
6. Щелкните **Дублировать скрипт**.
7. Обновление hello **FROM** toohello следующие пути:

    /Samples/Data/SearchLog.tsv
8. Щелкните **Отправить задание**.

## <a name="see-also"></a>Дополнительные материалы
* [Обзор аналитики озера данных Azure](data-lake-analytics-overview.md)
* [Начало работы с аналитикой озера данных Azure с помощью Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Начало работы с аналитикой озера данных Azure и U-SQL с помощью Visual Studio](data-lake-analytics-u-sql-get-started.md)
* [Управление аналитикой озера данных Azure с помощью портала Azure](data-lake-analytics-manage-use-portal.md)
