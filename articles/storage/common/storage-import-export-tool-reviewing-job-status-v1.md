---
title: "состояние задания импорта и экспорта Azure - v1 aaaReviewing | Документы Microsoft"
description: "Узнайте, как файлы журналов hello toouse, созданные при hello импорта или экспорта задания был запущен toosee hello состояние задания импорта и экспорта hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>Просмотр состояния задания импорта и экспорта Azure с помощью файлов журнала копирования
Когда hello службы импорта и экспорта Microsoft Azure обрабатывает диски, связанные с заданием импорта или экспорта, она записывает учетной записи копии журнала файлов toohello хранения tooor откуда Импорт или экспорт больших двоичных объектов. Hello файл журнала содержит подробное состояние каждого файла, который был импортирован или экспортирован. файл журнала копирования tooeach URL-адрес Hello возвращается при запросе hello состояние завершенного задания; в разделе [получения задания](/rest/api/storageservices/Get-Job3) для получения дополнительной информации.  

## <a name="example-urls"></a>Примеры URL-адресов

Hello ниже приведены примеры URL-адресов для копирования файлов журнала для задания импорта с двумя дисками.  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 В разделе [службы импорта и экспорта формат файла журнала](../storage-import-export-file-format-log.md) hello формата журналов копирования и полный список кодов состояния hello.  
  
## <a name="next-steps"></a>Дальнейшие действия
 
 * [Установка hello средство импорта и экспорта Azure](storage-import-export-tool-setup-v1.md)   
 * [Подготовка жестких дисков для задания импорта](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [Подготовка задания импорта](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [Подготовка задания экспорта](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [Устранение неполадок средства импорта и экспорта Azure hello](storage-import-export-tool-troubleshooting-v1.md)
