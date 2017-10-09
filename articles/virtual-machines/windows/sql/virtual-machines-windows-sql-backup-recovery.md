---
title: "aaaBackup и восстановление для SQL Server | Документы Microsoft"
description: "Содержит сведения об архивации и восстановлении баз данных SQL Server на виртуальных машинах Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Резервное копирование и восстановление SQL Server в виртуальных машинах Azure
## <a name="overview"></a>Обзор
Хранилище Azure поддерживает три копии tooguarantee защита на диске каждой виртуальной Машине Azure от потери или повреждения данных физических данных. Таким образом в отличие от локальной, не требуется tooworry о них. Однако по-прежнему необходимо создать резервную копию вашей tooprotect баз данных SQL Server от ошибок, приложением или пользователем (например, Вставка неверных данных или удаление таблицы) и выполняется доступ toorestore tooa на определенный момент времени.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Для SQL Server на виртуальных машинах Azure можно использовать собственного резервного копирования и восстановления методы, с помощью подключенных дисков для назначения hello hello файлов резервной копии. Однако есть toohello ограничение числа дисков, можно присоединить tooan виртуальной машины Azure, на основании hello [размер виртуальной машины hello](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Имеется также hello издержки управления tooconsider диска.

Начиная с SQL Server 2014, создания резервных копий и восстановление tooMicrosoft хранилища больших двоичных объектов Azure. Дополнительные возможности для этого параметра реализуются также в версии SQL Server 2016. Кроме того, SQL Server 2016 позволяет практически мгновенно создавать резервные копии файлов базы данных, которые находятся в хранилище больших двоичных объектов Microsoft Azure, и быстро их восстанавливать с помощью моментальных снимков Azure. В этой статье содержится обзор этих параметров. Дополнительные сведения см. в статье [Резервное копирование и восстановление SQL Server с помощью службы хранилища BLOB-объектов Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

> [!NOTE]
> Описание параметров hello при резервном копировании очень больших баз данных см. в разделе [несколько терабайт SQL Server базы данных стратегии резервного копирования для виртуальных машин Azure](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx).
> 
> 

в следующих разделах Hello входят сведения о конкретных toohello разные версии SQL Server, поддерживаемая в виртуальной машине Azure.

## <a name="sql-server-virtual-machines"></a>Виртуальные машины SQL Server
Если экземпляр SQL Server работает на виртуальной машине Azure, файлы базы данных уже содержатся на дисках данных в Azure. Эти диски находятся в хранилище BLOB-объектов. Таким образом hello причины архивацию вашей базы данных и hello подходов, которые немного предпринять изменений. Рассмотрим следующие hello. 

* Tooperform защиты tooprovide резервные копии базы данных от сбоев оборудования или носителя больше не нужна, так как Microsoft Azure обеспечивает такую защиту как часть hello службы Microsoft Azure.
* Необходимо по-прежнему tooprovide tooperform базы данных резервных копий защиты от ошибок пользователей или для архивирования, нормативных требований или административных задач.
* Можно сохранить файл резервной копии hello непосредственно в Azure. Дополнительные сведения см. в разделе hello в следующих разделах, которые дают представление о hello разные версии SQL Server.

## <a name="sql-server-2016"></a>SQL Server 2016
Microsoft SQL Server 2016 поддерживает функции [архивации и восстановления с использованием больших двоичных объектов Azure](https://msdn.microsoft.com/library/jj919148.aspx) , реализованные в SQL Server 2014. Однако она также включает следующие усовершенствования hello:

| Усовершенствования 2016 года | Сведения |
| --- | --- |
| **Чередование** |При резервном копировании tooMicrosoft хранилища BLOB-объектов Azure, SQL Server 2016 поддерживает резервное копирование tooenable toomultiple больших двоичных объектов, резервное копирование больших баз данных, копирование максимум tooa 12,8 ТБ. |
| **Резервное копирование моментальных снимков** |С помощью hello моментальные снимки Azure резервное копирование моментальных снимков файлов SQL Server предоставляет практически мгновенного создания резервных копий и быстрое восстановление файлов базы данных, сохраненных с помощью службы хранилища больших двоичных объектов Azure hello. Это дает вам toosimplify политик резервного копирования и восстановления. Функция архивации моментальных снимков файлов поддерживает также восстановление до определенной точки во времени. Дополнительные сведения см. в статье [Резервные копии моментальных снимков файлов для файлов базы данных в Azure](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx). |
| **Планирование управляемого резервного копирования** |SQL Server Managed Backup tooAzure теперь поддерживает пользовательские расписания. Дополнительные сведения см. в разделе [tooMicrosoft SQL Server Managed Backup Azure](https://msdn.microsoft.com/library/dn449496.aspx). |

Учебник hello возможностей SQL Server 2016 при использовании хранилища больших двоичных объектов Azure см. в разделе [учебника: использование службы хранилища больших двоичных объектов Microsoft Azure hello с базами данных SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx).

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 включает следующие усовершенствования hello.

1. **Резервное копирование и восстановление tooAzure**:
   
   * *Резервное копирование SQL Server tooURL* теперь имеет поддержку в среде SQL Server Management Studio. Hello tooback параметр вверх tooAzure теперь доступна при использовании задач резервного копирования или восстановления или мастер планов обслуживания в SQL Server Management Studio. Дополнительные сведения см. в разделе [tooURL резервного копирования SQL Server](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
   * *Управляемое резервное копирование tooAzure* имеет новые функции автоматического управления резервным копированием. Они пригодятся при управлении автоматической архивацией для экземпляров SQL Server 2014, выполняемых на машине Azure. Дополнительные сведения см. в разделе [tooMicrosoft SQL Server Managed Backup Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx).
   * *Автоматическая архивация* предоставляет дополнительные автоматизации позволяют tooautomatically *tooAzure SQL Server Managed Backup* для всех существующих и новых баз данных для виртуальной Машины SQL Server в Azure. Дополнительную информацию см. в статье [Автоматическая архивация SQL Server на виртуальных машинах Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).
   * Обзор всех параметров hello для резервного копирования SQL Server 2014 tooAzure см. в разделе [SQL Server Backup and Restore with Microsoft Azure Blob Storage Service](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
2. **Шифрование**: SQL Server 2014 поддерживает шифрование данных при создании архива. Он поддерживает несколько алгоритмов шифрования и hello использования консорциума osf сертификата или асимметричного ключа. Дополнительные сведения см. в статье [Шифрование резервной копии](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx).

## <a name="sql-server-2012"></a>SQL Server 2012
Подробные сведения об архивации и восстановлении в SQL Server 2012 см. в статье [Резервное копирование и восстановление баз данных SQL Server](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx).

Начиная с SQL Server 2012 с пакетом обновления 1 накопительное обновление 2, можно выполнять архивацию tooand восстановления из службы хранилища больших двоичных объектов hello. Это улучшение можно использовать tooback копии баз данных SQL Server на SQL Server на виртуальной машине Azure или на локальном экземпляре. Дополнительные сведения см. в статье [Резервное копирование и восстановление SQL Server с помощью службы хранилищ больших двоичных объектов Windows Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Перечислены некоторые преимущества использования службы хранилища больших двоичных объектов hello hello hello возможность toobypass hello 16 предельной для подключенных дисков, легкость управления, прямую доступность hello hello файла резервной копии tooanother экземпляр SQL Server, работающий в Azure Виртуальная машина, или на локальном экземпляре для целей миграции или аварийного восстановления. Полный список преимуществ toousing службы хранилища больших двоичных объектов Azure для резервного копирования SQL Server см. в разделе hello *преимущества* статьи [SQL Server Backup and Restore with Azure Blob Storage Service](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Рекомендации и сведения об устранении неполадок см. в статье [Рекомендованные методы резервного копирования и восстановления (служба хранилищ больших двоичных объектов Windows Azure)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx).

## <a name="sql-server-2008"></a>SQL Server 2008
Сведения об архивации и восстановлении в SQL Server 2008 R2 см. в статье [Резервное копирование и восстановление баз данных в SQL Server (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx).

Сведения об архивации и восстановлении в SQL Server 2008 см. в статье [Резервное копирование и восстановление баз данных в SQL Server (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx).

## <a name="next-steps"></a>Дальнейшие действия
При планировании развертывания SQL Server на виртуальной Машине Azure подготовки инструкции можно найти в следующих учебника hello: [подготовки виртуальной машины SQL Server в Azure с помощью диспетчера ресурсов Azure](virtual-machines-windows-portal-sql-server-provision.md).

Несмотря на то что резервного копирования и восстановления можно использовать toomigrate данных, существует потенциально проще tooSQL пути миграции данных сервера на Виртуальной машине Azure. Полное описание вариантов миграции и рекомендации в разделе [миграция tooSQL базы данных сервера на Виртуальной машине Azure](virtual-machines-windows-migrate-sql.md).

Просмотрите и другие [ресурсы по запуску SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).

