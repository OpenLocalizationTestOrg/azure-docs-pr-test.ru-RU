---
title: "aaaAzure импорта и экспорта метаданных и свойств формат файла | Документы Microsoft"
description: "Узнайте, как toospecify метаданных и свойств для одного или нескольких больших двоичных объектов, являются частью Импорт или экспорт заданий."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a>Формат файла свойств и файла метаданных службы импорта и экспорта Azure
В рамках задания импорта или экспорта можно указать метаданные и свойства для одного или нескольких больших двоичных объектов. tooset метаданных или свойств для больших двоичных объектов, которые создаются в рамках задания импорта, можно указать файл метаданных или свойств на hello жесткий диск, содержащий toobe данных hello импортированы. Для задания экспорта метаданные и свойства записываются tooa файл метаданных или свойств, который включается на жестком диске hello возвращается tooyou.  
  
## <a name="metadata-file-format"></a>Формат файла метаданных  
Hello файла метаданных имеет следующий формат:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|XML-элемент|Тип|Описание|  
|-----------------|----------|-----------------|  
|`Metadata`|Корневой элемент|корневой элемент файла метаданных hello Hello.|  
|`metadata-name`|Строка|необязательный параметр. Hello-XML-элемент указывает имя hello hello метаданных для большого двоичного объекта hello и его значение указывает значение параметра метаданных hello hello.|  
  
## <a name="properties-file-format"></a>Формат файла свойств  
Hello файл свойств имеет следующий формат:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|XML-элемент|Тип|Описание|  
|-----------------|----------|-----------------|  
|`Properties`|Корневой элемент|корневой элемент файла свойств hello Hello.|  
|`Last-Modified`|Строка|необязательный параметр. Hello время последнего изменения для hello большого двоичного объекта. Только для заданий экспорта.|  
|`Etag`|Строка|необязательный параметр. Здравствуйте, значение ETag большого двоичного объекта. Только для заданий экспорта.|  
|`Content-Length`|Строка|необязательный параметр. размер Hello hello большого двоичного объекта в байтах. Только для заданий экспорта.|  
|`Content-Type`|Строка|необязательный параметр. Тип содержимого Hello hello большого двоичного объекта.|  
|`Content-MD5`|Строка|необязательный параметр. Здравствуйте хэш MD5 большого двоичного объекта.|  
|`Content-Encoding`|Строка|необязательный параметр. Здравствуйте, содержимое большого двоичного объекта кодирования.|  
|`Content-Language`|Строка|необязательный параметр. Здравствуйте, язык содержимого большого двоичного объекта.|  
|`Cache-Control`|Строка|необязательный параметр. Hello строку управления кэшем для большого двоичного объекта hello.|  

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные правила настройки свойств и метаданных больших двоичных объектов см. в статьях [Set Blob Properties](/rest/api/storageservices/set-blob-properties) (Задание свойств большого двоичного объекта), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) (Задание метаданных большого двоичного объекта) и [Setting and Retrieving Properties and Metadata for Blob Resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Задание и получение свойств и метаданных для ресурсов больших двоичных объектов).
