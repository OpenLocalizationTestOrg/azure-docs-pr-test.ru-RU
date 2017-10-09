---
title: "aaaMigrate tooSQL базы данных сервера SQL Server на виртуальной Машине | Документы Microsoft"
description: "Узнайте, как toomigrate пользователя локальной базы данных tooSQL Server в виртуальной машине Azure."
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>Перенос tooSQL базы данных сервера SQL Server на виртуальной Машине Azure

Существует ряд методов toomigrate пользователя базы данных локального SQL Server tooSQL Server на виртуальной Машине Azure. В этой статье будет кратко рассматриваются различные методы и рекомендуем hello наилучший способ для различных сценариев.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>Что такое первичный методов hello
доступны следующие методы Hello основной миграции:

* Выполните резервное копирование локально с помощью сжатия и вручную копирование hello резервного копирования файла в hello виртуальной машины Azure
* TooURL резервного копирования и восстановления в виртуальной машине Azure с URL-адреса hello hello
* Отсоединение, затем скопируйте hello данных и журнала файлов tooAzure хранилища больших двоичных объектов и затем присоединить tooSQL Server на виртуальной Машине Azure с URL-адреса
* Преобразование локального физического компьютера tooHyper-V VHD отправьте tooAzure хранилища больших двоичных объектов, а затем развернуть новую виртуальную Машину с помощью отправки виртуального жесткого диска
* Доставка жесткого диска в службу импорта и экспорта Windows.
* Если у вас есть AlwaysOn локального развертывания, используйте hello [мастер добавления реплики Azure](../classic/sql-onprem-availability.md) toocreate реплики в Azure, а затем перехода на другой ресурс, указывающий экземпляр базы данных SQL Azure toohello пользователей
* Используйте SQL Server [репликации транзакций](https://msdn.microsoft.com/library/ms151176.aspx) tooconfigure hello Azure SQL Server в качестве подписчика, а затем отключить репликации, указывающий экземпляр базы данных SQL Azure toohello пользователей

> [!TIP]
> Также можно использовать эти же методы между VM SQL Server в Azure toomove базы данных. Например имеется не поддерживает выполнение tooupgrade коллекции образов виртуальной Машины SQL Server из одного tooanother версия или выпуск. В этом случае следует создать новую виртуальную Машину SQL Server с hello выпуска новой версии или и использовать один из методов переноса hello в этой статье toomove баз данных. 

## <a name="choosing-your-migration-method"></a>Выбор метода миграции
Для повышения производительности передачи данных оптимальный перенести файлы базы данных hello в hello виртуальной Машины Azure с использованием сжатого файла резервной копии.

toominimize время простоя во время процесса миграции hello базы данных, используйте параметр AlwaysOn hello или репликации транзакций параметр hello.

Если это не hello возможных toouse выше методов, вручную перенести базу данных. При использовании этого метода будет обычно начинают с резервной копии базы данных следуют копию hello резервной копии базы данных в Azure и затем выполните восстановление базы данных. Можно также скопировать hello сами файлы базы данных в Azure, а затем подключите их. Существует несколько методов, с помощью которых можно выполнить ручной перенос базы данных на виртуальную машину Azure.

> [!NOTE]
> При обновлении с предыдущих версий SQL Server tooSQL Server 2014 или SQL Server 2016 необходимо учитывать, нужны ли изменения. Рекомендуется учесть все зависимости функций, не поддерживается hello новой версией SQL Server в рамках проекта миграции. Дополнительные сведения о поддерживаемых hello выпусках и сценариях см. в разделе [обновление tooSQL сервера](https://msdn.microsoft.com/library/bb677622.aspx).

Hello в следующей таблице отображается список всех методов основной hello и обсуждается, когда лучше всего подходит hello использования каждого метода.

| Метод | Версия исходной базы данных | Версия базы данных назначения | Ограничение на размер файла резервной копии исходной базы данных | Примечания |
| --- | --- | --- | --- | --- |
| [Выполните резервное копирование локально с помощью сжатия и вручную копирование hello резервного копирования файла в hello виртуальной машины Azure](#backup-and-restore) |SQL Server 2005 или более поздней версии |SQL Server 2005 или более поздней версии |[Ограничение на размер хранилища виртуальной машины Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Это очень простая и проверенная методика перемещения баз данных между компьютерами. |
| [TooURL резервного копирования и восстановления в виртуальной машине Azure с URL-адреса hello hello](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 или более поздней версии |SQL Server 2012 SP1 CU2 или более поздней версии |Менее 12,8 ТБ для SQL Server 2016, в противном случае менее 1 ТБ | Этот метод является hello toomove еще одно способом – toohello файл резервной копии виртуальной Машины с помощью хранилища Azure. |
| [Отсоединение, затем скопируйте hello данных и журнала файлов tooAzure хранилища больших двоичных объектов и затем присоединить tooSQL Server на виртуальной машине Azure с URL-адреса](#detach-and-attach-from-url) |SQL Server 2005 или более поздней версии |SQL Server 2014 или более поздней версии |[Ограничение на размер хранилища виртуальной машины Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Используйте этот метод при планировании слишком[хранить эти файлы с помощью службы хранилища больших двоичных объектов Azure hello](https://msdn.microsoft.com/library/dn385720.aspx) и присоединить их tooSQL сервер запущен на виртуальной Машине Azure, особенно в очень больших баз данных |
| [Преобразование локального компьютера tooHyper-V VHD отправьте tooAzure хранилища больших двоичных объектов, а затем развернуть новую виртуальную машину с помощью загруженного VHD-файла](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 или более поздней версии |SQL Server 2005 или более поздней версии |[Ограничение на размер хранилища виртуальной машины Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Используется, когда [перевод собственную лицензию SQL Server](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), при переносе базы данных, которая будет выполняться на более старой версии SQL Server или перенос системных и пользовательских баз данных вместе как часть hello миграции базы данных, зависят от друга пользовательских баз данных и/или системных баз данных. |
| [Доставка жестких дисков в службу импорта и экспорта Windows.](#ship-hard-drive) |SQL Server 2005 или более поздней версии |SQL Server 2005 или более поздней версии |[Ограничение на размер хранилища виртуальной машины Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Используйте hello [службы импорта и экспорта Windows](../../../storage/common/storage-import-export-service.md) при метод ручного копирования становится слишком низкой, такие как с очень больших баз данных |
| [Здравствуйте, используйте мастер добавления реплики Azure](../classic/sql-onprem-availability.md) |SQL Server 2012 или более поздней версии |SQL Server 2012 или более поздней версии |[Ограничение на размер хранилища виртуальной машины Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Сокращает время простоя, используется при наличии локального развертывания AlwaysOn. |
| [Использование репликации транзакций SQL Server](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 или более поздней версии |SQL Server 2005 или более поздней версии |[Ограничение на размер хранилища виртуальной машины Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Следует использовать, когда требуется время простоя toominimize и не имеют AlwaysOn локального развертывания |

## <a name="backup-and-restore"></a>Архивация и восстановление
Резервное копирование базы данных с использованием сжатия скопируйте hello резервного копирования toohello виртуальной Машины, а затем восстановите hello базы данных. Если файл резервной копии превышает 1 ТБ, необходимо чередовать его так, как максимальный размер диска ВМ hello составляет 1 ТБ. Используйте следующие общие шаги toomigrate пользовательской базы данных с помощью этого метода вручную hello.

1. Выполните расположение локальной tooan резервной копии всей базы данных.
2. Создание и передать виртуальную машину с SQL Server требуемой версии hello.
3. Настройте подключения в соответствии со своими требованиями. В разделе [подключения виртуальной машины SQL Server в Azure (диспетчера ресурсов) tooa](virtual-machines-windows-sql-connect.md).
4. Скопируйте вашей tooyour резервного копирования файлов виртуальных Машин с помощью удаленного рабочего стола, проводника Windows или hello команды копирования из командной строки.

## <a name="backup-toourl-and-restore"></a>TooURL резервного копирования и восстановления
Вместо создания резервной копии tooa локальный файл, можно использовать hello [резервного копирования tooURL](https://msdn.microsoft.com/library/dn435916.aspx) и восстанавливать toohello URL-адрес виртуальной Машины. С SQL Server 2016 чередующиеся резервные наборы данных, поддерживаются, рекомендуется для повышения производительности и необходимые tooexceed hello ограничения на размер каждого большого двоичного объекта. Для очень больших баз данных hello использование hello [службы импорта и экспорта Windows](../../../storage/common/storage-import-export-service.md) рекомендуется.

## <a name="detach-and-attach-from-url"></a>Отключение и подключение с использованием URL-адреса
Отсоединение базы данных и журнала файлов и передает их слишком[хранилища больших двоичных объектов Azure](https://msdn.microsoft.com/library/dn385720.aspx). Затем присоедините базу данных hello из hello URL-адрес своей ВМ Azure. Применяется, если вы хотите tooreside файлы hello физической базы данных в хранилище больших двоичных объектов. Это может быть удобно для очень больших баз данных. Используйте следующие общие шаги toomigrate пользовательской базы данных с помощью этого метода вручную hello.

1. Отключите файлы базы данных hello от hello в локальный экземпляр базы данных.
2. Скопируйте файлы базы данных hello отсоединена в хранилище больших двоичных объектов с помощью hello [командной строки программу AZCopy](../../../storage/common/storage-use-azcopy.md).
3. Присоединение файлов базы данных hello из экземпляра SQL Server toohello hello URL-адрес Azure в виртуальной Машине Azure hello.

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>Преобразовать tooVM и отправка tooURL и развернуть в качестве новой виртуальной Машины
Используйте этот метод toomigrate все системные и пользовательские базы данных на виртуальной машине tooAzure экземпляра локального SQL Server. Используйте следующие общие шаги toomigrate всего экземпляра SQL Server с помощью этого метода вручную hello.

1. Преобразование физических или виртуальных машин tooHyper-V VHD с помощью [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).
2. Отправить файлы виртуального жесткого диска tooAzure хранилища с помощью hello [командлета Add-AzureVHD](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3. Развертывание новой виртуальной машины с помощью hello отправки виртуального жесткого диска.

> [!NOTE]
> toomigrate всего приложения, рассмотрите возможность использования [Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Отправка жестких дисков
Используйте hello [метода службы импорта и экспорта Windows](../../../storage/common/storage-import-export-service.md) tootransfer больших объемов данных файла tooAzure хранилища больших двоичных объектов в ситуациях, когда передача по сети hello дорого стоит или не представляется возможной. С этой службой отправлять одну или несколько жестких дисков, содержащий этот данных tooan центр обработки данных Azure, где данные будут отправлены tooyour учетной записи хранилища.

## <a name="next-steps"></a>Дальнейшие действия
Подробные сведения о работе SQL Server на виртуальных машинах Azure см. в разделе [Общие сведения об SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).

Инструкции по созданию образ виртуальной машины Azure SQL Server см. в разделе [советы и рекомендации для клонирования виртуальных машин Azure SQL из записанных образов](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) на hello блог инженеров CSS SQL Server.

