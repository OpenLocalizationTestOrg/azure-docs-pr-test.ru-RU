---
title: "aaaDiagnostics и восстановление после ошибок для заданий импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как ведение подробного журнала tooenable для импорта и экспорта Microsoft Azure службы заданий."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a>Диагностика и восстановление после ошибок для заданий импорта и экспорта Azure
Для каждого обрабатываемого диска hello службы импорта и экспорта Azure создает журнал ошибок в учетной записи хранения связанных hello. Можно также включить ведение подробного журнала, задание hello `LogLevel` свойство слишком`Verbose` при вызове hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) или [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) операций.

 По умолчанию журналы записываются tooa контейнер с именем `waimportexport`. Можно указать другое имя, установка hello `DiagnosticsPath` свойства при вызове hello `Put Job` или `Update Job Properties` операций. Hello журналы хранятся в виде блочных больших двоичных объектов с hello следующее соглашение об именовании: `waies/jobname_driveid_timestamp_logtype.xml`.

 Вы можете получить hello URI журналов заданий hello, вызывающему Привет [получения задания](/rest/api/storageimportexport/jobs#Jobs_Get) операции. Hello URI для hello подробного журнала возвращается в hello `VerboseLogUri` свойство для каждого диска, а hello URI для журнала ошибок hello возвращается в hello `ErrorLogUri` свойство.

Можно использовать hello, ведение журнала данных tooidentify hello следующих ситуаций.

## <a name="drive-errors"></a>Ошибки диска

Hello следующих элементов относятся ошибки диска:

-   Ошибки доступа или чтении hello файла манифеста

-   Неправильные ключи BitLocker.

-   Ошибки операций чтения или записи с диском.

## <a name="blob-errors"></a>Ошибки больших двоичных объектов

Hello следующих элементов относятся ошибки больших двоичных объектов:

-   Неправильные либо конфликтующие большие двоичные объекты или их имена.

-   Отсутствуют файлы.

-   Не удалось найти большой двоичный объект.

-   Усеченные файлы (файлы hello на диске hello меньше, чем указано в манифесте hello)

-   Повреждено содержимое файла (для заданий импорта, выявляется по несовпадению контрольной суммы MD5).

-   Повреждены файлы метаданных и свойств большого двоичного объекта (обнаружено несовпадение контрольной суммы MD5).

-   Неверная схема для свойства большого двоичного объекта hello или файлов метаданных

Возможны ситуации, где некоторые части задания импорта или экспорта не завершаются успешно, хотя hello в целом по-прежнему завершения задания. В этом случае можно передать или загрузить hello отсутствует части hello данных по сети, или можно создать новые данные hello tootransfer задания. В разделе hello [Справочник средство импорта и экспорта Azure](storage-import-export-tool-how-to-v1.md) toolearn как toorepair hello данных по сети.

## <a name="next-steps"></a>Дальнейшие действия

* [С помощью REST API службы импорта и экспорта hello](storage-import-export-using-the-rest-api.md)
