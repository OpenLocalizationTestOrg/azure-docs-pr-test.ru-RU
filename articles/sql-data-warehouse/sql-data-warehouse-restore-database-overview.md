---
title: "хранилище данных Azure — локальные и географически избыточная aaaRestore | Документы Microsoft"
description: "Общие сведения о параметрах восстановления hello базы данных для восстановления базы данных в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>Восстановление хранилища данных SQL
> [!div class="op_single_selector"]
> * [Обзор][Overview]
> * [Портал][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

Хранилище данных SQL предоставляет функции локального восстановления и геовосстановления, входящие в набор средств аварийного восстановления. С помощью данных хранилища резервных копий toorestore tooa восстановления хранилища данных в основном регионе hello, точек или использовать геоизбыточных архивов toorestore tooa другом географическом регионе. В этой статье описываются особенности hello операция восстановления хранилища данных.

## <a name="what-is-a-data-warehouse-restore"></a>Что такое восстановление хранилища данных?
Восстановление хранилища данных означает создание нового хранилища данных из резервной копии существующего или удаленного хранилища данных. Hello восстановленные данные хранилища повторно создает hello хранилища резервных копий данных на определенный момент. Так как хранилище данных SQL является распределенной системой, то восстановленное хранилище данных состоит из множества файлов резервных копий, которые хранятся в больших двоичных объектах Azure. 

Восстановление базы данных является важной частью любой стратегии непрерывности бизнес-процессов и аварийного восстановления, так как позволяет воссоздать данные после случайного повреждения или удаления.

Дополнительные сведения можно найти в разделе 

* [Архивация хранилища данных SQL](sql-data-warehouse-backups.md)
* [Общие сведения о непрерывности бизнес-процессов](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Точки восстановления хранилища данных SQL
Преимущество использования хранилища Azure Premium хранилище данных SQL использует больших двоичных объектов Azure для хранения моментальных снимков toobackup hello первичных данных хранилища. Каждый моментальный снимок содержит точку восстановления, которая представляет время hello hello моментальных снимков к работе. toorestore хранилища данных, следует выбрать точку восстановления и выполните команду restore.  

Хранилище данных SQL всегда восстанавливает hello резервного копирования tooa новое хранилище данных. Можно сохранить hello восстановленных данных хранилища и hello текущего или удалите один из них. Если требуется tooreplace hello текущего хранилища данных с помощью hello восстановления хранилища данных, можно переименовать.

Если вам требуется toorestore хранилища данных, удаленных или приостановлена, вы можете [создать обращение в службу поддержки](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>Геоизбыточное восстановление
Вы можете восстановить поддержки хранилища данных SQL Azure уровня производительности выбранных область tooany хранилища данных. Обратите внимание на то, что 9000 и 18000 DWU не поддерживаются во всех регионах во время предварительного просмотра hello.

> [!NOTE]
> географически избыточное tooperform восстановления, вы не должны отказались от этой функции.
> 
> 

## <a name="restore-timeline"></a>Временная шкала восстановления
Можно восстановить базу данных tooany доступной точки восстановления в пределах hello последних семи дней. Моментальные снимки запуск каждые четыре часа tooeight и доступны в течение семи дней. Если моментальный снимок старше семи дней, то срок его действия истекает и его точка восстановления перестает быть доступной.

## <a name="restore-costs"></a>Затраты на восстановление
Hello хранилища плата за хранилище восстановленных данных hello оплачивается по тарифу хранилища Azure Premium hello. 

Если навести на складе восстановленных данных взимается плата для хранилища по тарифу хранилища Azure Premium hello. Приостановка Hello преимущество — не взиматься плата за вычислительные ресурсы DWU hello.

Ознакомиться с ценами на хранилище данных SQL можно [здесь](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Применение восстановления
Hello главным образом используется для восстановления хранилища данных — toorecover данные после случайную потерю данных или повреждения.

Tooretain восстановления хранилища данных резервной копии также можно использовать для более семи дней. После восстановления резервной копии hello имеется hello хранилище данных через Интернет и его выполнение можно приостановить бесконечно toosave вычислительных затрат. База данных приостановлена Hello расходы на хранение скоростью hello хранилища Azure Premium. 

## <a name="related-topics"></a>Связанные разделы
### <a name="scenarios"></a>Сценарии
* Сведения об обеспечении непрерывности бизнес-процессов см. в [этом обзоре](../sql-database/sql-database-business-continuity.md).

<!-- ### Tasks -->

tooperform хранилища данных восстановления, восстановление с помощью:

* Azure портала, см. в разделе [восстановления хранилища данных, с помощью портала Azure hello](sql-data-warehouse-restore-database-portal.md)
* командлеты PowerShell (ознакомьтесь с разделом [Восстановление хранилища данных SQL Azure (PowerShell)](sql-data-warehouse-restore-database-powershell.md));
* REST API см. в разделе [восстановления хранилища данных, с помощью API-интерфейсов REST hello](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
