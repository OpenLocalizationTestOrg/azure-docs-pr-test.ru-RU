---
title: "toodo aaaWhat hello для события сбоя хранилища Azure | Документы Microsoft"
description: "Какие toodo hello для события сбоя хранилища Azure"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: ee7eb71311c6e453dc078ec3566267ee0c2f444a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>Какие toodo в случае сбоя хранилища Azure
В корпорации Майкрософт мы работать жестких toomake в том, что наши службы всегда доступны. Иногда по независящим от нас обстоятельствам происходят незапланированные простои служб в одном или нескольких регионах. toohelp обработки таких редких случаев, мы предоставляем hello следующие общие рекомендации для служб хранилища Azure.

## <a name="how-tooprepare"></a>Как tooprepare
Очень важно для каждого клиента tooprepare собственные плана аварийного восстановления. toorecover усилий Hello из доступа к хранилищу обычно включает в себя сотрудников отдела эксплуатации и автоматизированные процедуры в порядке tooreactivate вашего приложения в состоянии работает. См. документации по Azure ниже toobuild toohello собственного плана аварийного восстановления:

* [Аварийное восстановление и высокий уровень доступности для приложений Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Техническое руководство по обеспечению устойчивости в Azure](../resiliency/resiliency-technical-guidance.md)
* [Служба Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)
* [Репликация службы хранилища Azure](storage-redundancy.md)
* [Служба архивации Azure](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>Как toodetect
Hello рекомендованные способом toodetermine hello Azure состояние toosubscribe toohello [панель мониторинга работоспособности службы Azure](https://azure.microsoft.com/status/).

## <a name="what-toodo-if-a-storage-outage-occurs"></a>Какие toodo в случае сбоя хранилища
Если один или несколько служб хранилища временно недоступны в одну или несколько областей, существует два варианта для вас tooconsider. Если нужен непосредственный доступ к данным tooyour рассмотрите вариант 2.

### <a name="option-1-wait-for-recovery"></a>Вариант 1. ожидание восстановления
В этом случае вам не нужно предпринимать какие-либо действия. Мы работаем тщательно доступности службы Azure toorestore hello. Можно отслеживать состояние службы hello на hello [панель мониторинга работоспособности службы Azure](https://azure.microsoft.com/status/).

### <a name="option-2-copy-data-from-secondary"></a>Вариант 2. Копирование данных из дополнительного региона
Если вы выбрали [геоизбыточное хранилище доступ для чтения (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (рекомендуется) для учетных записей хранилища, будет иметь доступ на чтение данных tooyour из вторичного региона hello. Можно использовать средства, такие как [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md)и hello [перемещение данных Azure библиотеки](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) toocopy данные из вторичного региона hello в другую учетную запись в unimpacted регион, а затем учетной записи хранилища toothat приложения для чтения и записи, доступности.

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>Какие tooexpect в случае отработки отказа хранилища
Если вы выбрали [Геоизбыточное хранилище](storage-redundancy.md#geo-redundant-storage) или [Доступ к геоизбыточному хранилищу для чтения](storage-redundancy.md#read-access-geo-redundant-storage) (рекомендуется), служба хранилища Azure будет хранить данные устойчиво в двух регионах (основном и дополнительном). В обоих регионах служба хранилища Azure постоянно поддерживает несколько реплик ваших данных.

Когда региональной аварии влияет на ваш основной регион, мы сначала будет предпринята попытка service toorestore hello в этом регионе. Зависит от природы hello аварийного hello и его влияние, в некоторых редких случаях мы может быть основной регион может toorestore hello. В этом случае мы выполняем географическую отработку отказа. Репликация данных в различных регионах Hello является асинхронного процесса, что может включать задержки, поэтому возможно, что изменения, которые еще не были реплицированы дополнительный регион toohello могут быть потеряны. Вы можете запрашивать hello [«Время последней синхронизации» вашей учетной записи хранилища](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) tooget сведения о состоянии репликации hello.

Существует ряд аспектов возможности географическая отработка отказа hello хранилища:

* Географическая хранилища отработка отказа будет запускаться только hello группой хранилища Azure — нет действий клиента не требуется.
* Существующие службы хранения конечных точек для больших двоичных объектов, таблиц, очередей и файлы останутся hello же после отработки отказа hello; Hello запись DNS потребуется обновить toobe tooswitch из вторичного региона hello основной регион toohello.
* До и во время географическая hello отработка отказа вы не будете иметь доступ на запись tooyour учетной записи хранилища из-за влияния toohello аварийного hello, но можно по-прежнему считывать из вторичного hello Если вашей учетной записи хранилища была настроена в качестве RA-GRS.
* Если hello распространяют изменения DNS географическая hello отработка отказа завершена, будет продолжена учетной записи хранилища tooyour чтение и запись; Этот атрибут указывает toobe toowhat используется вашей дополнительной конечной точки. 
* Обратите внимание, если у вас есть GRS или RA-GRS настроен для учетной записи хранилища hello разрешен доступ для записи. 
* Вы можете запрашивать [«Geo перехода на другой ресурс время последнего» вашей учетной записи хранилища](https://msdn.microsoft.com/library/azure/ee460802.aspx) tooget более подробные сведения.
* После отработки отказа hello вашей учетной записи хранения будут задействованы, но в состоянии «Деградация», как он фактически размещается в область автономного с нет возможности географической репликации. toomitigate этого риска, мы восстановит hello исходной основной регион, а затем выполните восстановление размещения географически toorestore hello исходное состояние. Если исходный основной регион hello является неисправимой, мы приведет к выделению другого дополнительный регион.
  Дополнительные сведения о hello инфраструктуры георепликацию хранилища Azure см. статьи toohello блоге группы хранилища hello о [параметры избыточности и RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

## <a name="best-practices-for-protecting-your-data"></a>Советы и рекомендации по защите данных
Существуют некоторые рекомендуемые подходы tooback копии хранилища данных на регулярной основе.

* Диски ВМ — использование hello [службы архивации Azure](https://azure.microsoft.com/services/backup/) tooback hello диски виртуальных Машин, используемых виртуальных машин Azure.
* Блочных BLOB-объектов — создать [моментального снимка](https://msdn.microsoft.com/library/azure/hh488361.aspx) каждого блока больших двоичных объектов или скопировать в другой области с помощью учетной записи хранилища tooanother большие двоичные объекты hello [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), или hello [ Библиотека Azure перемещения данных](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/).
* Использование таблиц — [AzCopy](storage-use-azcopy.md) tooexport hello таблицы данных в другой учетной записи хранилища в другом регионе.
* Использовать файлы — [AzCopy](storage-use-azcopy.md) или [Azure PowerShell](storage-powershell-guide-full.md) toocopy учетной записи хранилища tooanother файлы в другую область.

Сведения о создании приложений, которые полностью используют функции hello RA-GRS, можно найти [проектирование высокой доступных приложений с помощью RA-GRS хранилища](storage-designing-ha-apps-with-ragrs.md)

