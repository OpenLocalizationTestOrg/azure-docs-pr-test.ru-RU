---
title: "hello aaaTroubleshooting средство импорта и экспорта Azure | Документы Microsoft"
description: "Дополнительные сведения о некоторых распространенных проблем hello видели, когда с помощью средства импорта и экспорта Azure hello и как toohandle их."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Устранение неполадок средства импорта и экспорта Azure hello
Средство импорта и экспорта Microsoft Azure Hello возвращает сообщения об ошибках, если возникли проблемы. В этом разделе приведены некоторые распространенные проблемы, с которыми могут столкнуться пользователи.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>Сеанс копирования завершается ошибкой, что мне делать?  
 Если сеанс копирования завершается ошибкой, существует два варианта.  
  
 Если ошибка hello повторить, например, если общий сетевой ресурс hello находился в автономном режиме для короткий период и теперь является вернется в оперативный режим, можно возобновить сеанс копирования hello. Если ошибка hello не повторить, например, если указано hello неверный исходный файл каталог в параметрах командной строки hello, требуется сеанс копирования tooabort hello. В разделе [Подготовка жестких дисков для задания импорта](../storage-import-export-tool-preparing-hard-drives-import-v1.md) приведены дополнительные сведения о возобновлении и прерывании сеансов копирования.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>Не удается возобновить или прервать сеанс копирования.  
 Если сеанс копирования hello hello первого сеанса копирования для диска, то сообщение об ошибке hello должна выглядеть следующим образом: «hello первого сеанса копирования, нельзя возобновлять или прервана.» В этом случае можно удалить старый файл журнала hello и повторно выполните команду hello.  
  
 Если сеанс копирования является hello не первый для диске, его можно всегда возобновлять или прервана.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>Я потерял hello файла журнала, можно ли создать задание hello?  
 файл журнала Hello для диска содержит hello полную информацию о копировании toothis диска с данными, и он tooadd необходимые дополнительные файлы toohello диска и будет использоваться toocreate задания импорта. В случае утери hello файла журнала будет иметь tooredo всех сеансов копирования hello hello диска.  
  
## <a name="next-steps"></a>Дальнейшие действия
 
* [Настройка средства импорта и экспорта azure hello](../storage-import-export-tool-setup-v1.md)   
* [Подготовка жестких дисков для задания импорта](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Просмотр состояния задания с помощью файлов журнала копирования](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [Подготовка задания импорта](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Подготовка задания экспорта](../storage-import-export-tool-repairing-an-export-job-v1.md)
