---
title: "aaaMoving большие объемы данных из облачного хранилища в Azure | Документы Microsoft"
description: "Обзор hello различные методы для перемещения tooand данных из хранилища Azure."
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 7c8ec9d99cbd48042b8146130c8827f9f25c024d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a>Перенос данных tooand из хранилища Azure
Следует ли toomove локальных данных tooAzure хранения (или наоборот), существует множество способов toodo это. Hello подход, который лучше всего работает для вас будет зависеть от вашего сценария. В этой статье приводится краткий обзор разных сценариев и подходящих способов для каждого из них.

## <a name="building-applications"></a>Создание приложений
При создании приложения в разработке hello API-интерфейса REST или один из наших многочисленные клиентские библиотеки является tooand данных хорошим способом toomove из хранилища Azure.

Служба хранилища Azure предоставляет функциональные клиентские библиотеки для .NET, iOS, Java, Android, универсальной платформы Windows (UWP), Xamarin, C++, Node.JS, PHP, Ruby и Python. Hello клиентские библиотеки предоставляют дополнительные возможности, такие как логику повторных попыток, ведение журнала и параллельные загрузки. Предусмотрена также возможность разрабатывать непосредственно для hello API REST, который может быть вызван для любого языка, который отправляет запросы HTTP/HTTPS.

В разделе [начало работы с хранилищем больших двоичных объектов Azure](../blobs/storage-dotnet-how-to-use-blobs.md) toolearn дополнительные.

Кроме того, мы также предлагаем hello [библиотека перемещения данных для хранилища Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) — библиотеку, предназначенный для высокопроизводительных копирование tooand данных из Azure. Можно найти tooour библиотеки перемещения данных [документации](https://github.com/Azure/azure-storage-net-data-movement) toolearn дополнительные. 

## <a name="quickly-viewinginteracting-with-your-data"></a>Быстрый просмотр данных и взаимодействие с ними
Если нужно легко tooview данные хранилища Azure Имея возможность tooupload hello и загрузки данных, рассмотрите возможность использования обозревателя хранилищ Azure.

См. наш список [обозреватели хранилища Azure](../storage-explorers.md) toolearn дополнительные.

## <a name="system-administration"></a>Системное администрирование
Если требуются или удобнее работать с помощью программы командной строки (например, системных администраторов), Вот несколько параметров для вас tooconsider.

### <a name="azcopy"></a>AzCopy
AzCopy — это программа командной строки Windows, предназначенный для высокопроизводительных копирование tooand данных из хранилища Azure. Также можно копировать данные внутри учетной записи хранения или между разными учетными записями хранения.

В разделе [перенесите данные с помощью служебной программы командной строки AzCopy hello](storage-use-azcopy.md) toolearn дополнительные.

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell — это модуль, предоставляющий командлеты для управления службами Azure. Это оболочка командной строки для выполнения задач и язык сценариев, разработанный специально для администрирования системы.

В разделе [с помощью Azure PowerShell с хранилищем Azure](storage-powershell-guide-full.md) toolearn дополнительные.

### <a name="azure-cli"></a>Инфраструктура CLI Azure
Инфраструктура CLI Azure предоставляет набор межплатформенных команд с открытым кодом для работы со службами Azure. Инфраструктура CLI Azure доступна в Windows, OSX и Linux.

В разделе [использование hello Azure CLI со службой хранилища Azure](../storage-azure-cli.md) toolearn дополнительные.

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>Перемещение больших объемов данных в медленной сети
Одним из крупнейших проблем hello, связанную с передачей больших объемов данных является hello время передачи. Если вы хотите tooget данные из хранилища Azure не беспокоясь о стоимости сети и написание кода, импорта и экспорта Azure является подходящим.

В разделе [импорта и экспорта Azure](../storage-import-export-service.md) toolearn дополнительные.

## <a name="backing-up-your-data"></a>Резервное копирование данных
Если необходимо просто toobackup вашей tooAzure данные хранилища, резервное копирование Azure — toogo способом hello. Это мощное решение для резервного копирования локальных данных и виртуальных машин Azure.

В разделе [резервного копирования Azure](../../backup/backup-introduction-to-azure-backup.md) toolearn дополнительные.

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a>Доступ к данным в локальной и из облака hello
Если требуется решение, для доступа к данным в локальной и из облака hello, затем можно использовать Azure гибридное решение облачного хранилища, StorSimple. Это решение включает физическое устройство StorSimple, которое обеспечивает интеллектуальное хранение часто используемых данных на SSD-дисках, периодически используемых данных — на жестких дисках и неактивных, резервных, архивных данных — в службе хранилища Azure.

В разделе [StorSimple](../../storsimple/storsimple-overview.md) toolearn дополнительные.

## <a name="recovering-your-data"></a>Восстановление данных
При наличии локальных рабочих нагрузок и приложений, необходимо решение, которое позволяет toocontinue вашего бизнеса, под управлением hello для события сбоя. Azure Site Recovery обеспечивает репликацию, отработку отказа и восстановление виртуальных машин и физических серверов. Реплицированные данные хранятся в хранилище Azure, позволяя tooeliminate hello потребность в дополнительном ЦОД на месте.

В разделе [Azure Site Recovery](../../site-recovery/site-recovery-overview.md) toolearn дополнительные.
### <a name="moving-data-faq"></a>Часто задаваемые вопросы о перемещении данных
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a>Можно ли перенести виртуальные жесткие диски из одного региона tooanother без копирования?
Hello только способом toocopy виртуальных жестких дисков между область — это toocopy hello данные между учетными записями хранения в каждом регионе. Для этого можно использовать AZCopy. Передача данных с помощью служебной программы командной строки AzCopy toolearn hello дополнительные в разделе. Для очень больших объемов данных можно использовать службу импорта и экспорта Azure. В разделе [импорта и экспорта Azure](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn дополнительные.
