---
title: "вопросы и ответы для хранилища Озера данных Azure aaaFrequently | Документы Microsoft"
description: "Руководство по устранению неполадок или снижению рисков их возникновения с помощью Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Часто задаваемые вопросы об Azure Data Lake Store
В этой статье вы узнаете о связанных tooAzure часто задаваемые вопросы о хранилище Озера данных.

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>Как дополнительно защитить данные от случайного удаления и общерегиональных аварий
Hello данных в вашей учетной записи хранилища Озера данных Azure является устойчивым tootransient сбои оборудования в области с помощью автоматизированных реплик. Это обеспечивает отказоустойчивость и высокий уровень доступности, собрания hello об уровне ОБСЛУЖИВАНИЯ хранилища Озера данных Azure. Здесь приводится ряд советов по как toofurther защитить данные от сбоев редких всей области или случайного удаления.

### <a name="disaster-recovery-guidance"></a>Руководство по аварийному восстановлению
Очень важно для каждого клиента tooprepare собственные плана аварийного восстановления. См. документации по Azure ниже toobuild toohello плана аварийного восстановления. Ниже приведены некоторые ресурсы, которые помогу составить план аварийного восстановления.

* [Аварийное восстановление и высокий уровень доступности для приложений Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Техническое руководство по обеспечению устойчивости в Azure](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>Рекомендации
Рекомендуется скопировать на критически важных данных tooanother хранилища Озера данных в другую область с потребностями toohello частоты выравниваются плана аварийного восстановления. Существует множество методов toocopy данных, в том числе [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) или [фабрики данных Azure](../data-factory/data-factory-azure-datalake-connector.md). Фабрика данных Azure — это полезная служба для создания и развертывания конвейеров перемещения данных на регулярной основе.

В случае сбоя региональные данные в регионе hello, куда скопирован hello данных затем доступны. Вы можете отслеживать hello [панель мониторинга работоспособности службы Azure](https://azure.microsoft.com/status/) toodetermine hello состояния службы Azure по всему миру hello.

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>Руководство по восстановлению данных после повреждения или случайного удаления
Хотя за счет автоматических реплик Azure Data Lake Store и обеспечивает устойчивость данных, они по-прежнему не защищены от повреждения или случайного удаления в приложении (а также разработчиками или пользователями).

#### <a name="best-practices"></a>Рекомендации
tooprevent случайного удаления, рекомендуется сначала установить политики hello правильные права доступа для учетной записи хранилища Озера данных.  Это включает в себя сопоставление [блокировки ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md) toolock работу важных ресурсов, а также применять контроль доступа на уровне учетной записи и файл с помощью доступных hello [функции безопасности хранилища Озера данных](data-lake-store-security-overview.md). Кроме того, мы советуем регулярно создавать копии важных данных в других учетных записях Data Lake Store, папках и подписках Azure с помощью [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) или [фабрики данных Azure](../data-factory/data-factory-azure-datalake-connector.md).  Это может быть используется toorecover из данных повреждение или удаление инцидента. Фабрика данных Azure — это полезная служба для создания и развертывания конвейеров перемещения данных на регулярной основе.

Можно также включить организаций [ведения журнала диагностики](data-lake-store-diagnostic-logs.md) для их хранилища Озера данных Azure учетной записи toocollect журналы аудита доступа к данным, которая предоставляет информацию о кто может удалили или обновили файл.

## <a name="next-steps"></a>Дальнейшие действия
* [Начало работы с Azure Data Lake Store с помощью портала Azure](data-lake-store-get-started-portal.md)
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)

