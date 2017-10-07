---
title: "aaaOverview сервера SQL Server на виртуальных машинах Azure | Документы Microsoft"
description: "Узнайте, как toorun полный выпусков SQL Server на виртуальных машинах Azure. Получение прямых ссылок tooall виртуальной Машине SQL Server изображения и связанное содержимое."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Приступая к работе с SQL Server в виртуальных машинах Azure
В этом разделе описываются параметры, позволяющие под управлением SQL Server на виртуальных машинах (ВМ) Azure вместе с [ссылки изображения tooportal](#option-1-create-a-sql-vm-with-per-minute-licensing) и Обзор [общих задач](#manage-your-sql-vm).

> [!NOTE]
> Если вы уже знакомы с SQL Server и просто toosee toodeploy ВМ SQL Server. в статье [подготовки виртуальной машины SQL Server в Azure portal hello](virtual-machines-windows-portal-sql-server-provision.md).
> 
> 

## <a name="overview"></a>Обзор
Если вы являетесь администратором базы данных или разработчик, виртуальные машины Azure предоставляют toomove способом вашего локального SQL Server рабочих нагрузок и приложений toohello облака. Hello следующие видеоматериалы содержат Технический обзор виртуальных машин Azure в SQL Server.

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

Hello видео рассматриваются hello в следующих областях:

| Время | Область |
| --- | --- |
| 00:21 |Что такое виртуальные машины Azure? |
| 01:45 |Безопасность |
| 02:50 |Соединение |
| 03:30 |Надежность и быстродействие хранилища |
| 05:20 |Размеры виртуальной машины |
| 05:54 |Высокая доступность и соглашение об уровне обслуживания |
| 07:30 |Поддержка конфигурации |
| 08:00 |Мониторинг |
| 08:32 |Демонстрация: создание виртуальной машины SQL Server 2016 |

> [!NOTE]
> Hello видео нацелен на SQL Server 2016, однако Azure предоставляет образов виртуальных Машин для многих версий SQL Server, включая 2012, 2014 и 2016. 
> 
> 

## <a name="scenarios"></a>Сценарии
Существует множество причин, которые можно выбрать toohost данные в Azure. Если приложение является перемещение tooAzure, это повышает производительность tooalso перемещения hello данных. Но это еще не все преимущества. Автоматически получает доступ toomultiple центрах обработки данных для глобального присутствия и аварийного восстановления. Hello данных также высокой безопасных и надежных.

Выполнение SQL Server на виртуальной машине Azure — один из вариантов хранения реляционных данных в Azure. Это хороший выбор для нескольких сценариев. Например может потребоваться tooconfigure hello ВМ Azure как аналогично возможных tooan на локальном компьютере, на SQL Server. Можно toorun дополнительные приложения и службы на hello или же сервер базы данных. Используя ресурсы, приведенные ниже, вы можете продумать в деталях еще больше сценариев и факторов.

* [SQL Server на виртуальных машинах Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/) Общие сведения о сценариях наиболее hello для использования SQL Server на виртуальных машинах Azure. 
* [Вы можете выбрать компонент SQL Server в облаке: база данных SQL Azure (PaaS) или SQL Server на виртуальных машинах Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md) — детальное сравнение базы данных SQL и SQL Server на виртуальной машине.

## <a name="create-a-new-sql-vm"></a>Создание виртуальной машины SQL
Hello следующих разделах toohello прямые ссылки портала Azure для образов коллекции виртуальных машин SQL Server hello. В зависимости от выбранного изображения hello вы можете либо оплаты по стоимости лицензирования SQL Server на основе минуту или можно использовать собственную лицензию (BYOL).

Ознакомьтесь с пошаговым руководством для создания новой виртуальной Машины SQL в учебнике hello [подготовки виртуальной машины SQL Server в Azure portal hello](virtual-machines-windows-portal-sql-server-provision.md). Кроме того, просмотрите hello [рекомендации по производительности для виртуальных машин SQL Server](virtual-machines-windows-sql-performance.md), объясняется, как tooselect hello соответствующий компьютер размер и другие функции, доступные во время инициализации.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>Вариант 1. Создание виртуальной машины SQL с лицензированием по поминутному тарифу
Hello ниже таблица содержит hello последнюю образов SQL Server в коллекции виртуальных машин hello. Щелкните любой toobegin ссылку, создание новой виртуальной Машины SQL с указанной версией, выпуска и операционной системы. 

> [!TIP]
> hello toounderstand виртуальной Машины и SQL, цены на эти образы в разделе [цены рекомендации для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

| Version (версия) | Операционная система | Выпуск |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

Кроме списка toothis другие сочетания операционных систем и версий SQL Server доступны. Найти другие изображения путем поиска marketplace в hello портал Azure. 

## <a id="BYOL"></a>Вариант 2. Создание виртуальной машины SQL с имеющейся лицензией
Вы также можете использовать собственную лицензию (BYOL). В этом сценарии вы платите только за hello виртуальной Машины без стоимость лицензирования SQL Server. toouse собственную лицензию матрицы hello использования версий SQL Server, выпуски и ниже операционных систем. На портале hello эти изображения префикса **{BYOL}**.

> [!TIP]
> Использование технологии BYOL со временем позволяет снизить расходы на использование непрерывных производственных рабочих нагрузок. Дополнительные сведения см. в [руководстве по выбору ценовой категории для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

| Version (версия) | операционная система | Выпуск |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

Кроме списка toothis другие сочетания операционных систем и версий SQL Server доступны. Найти другие изображения путем поиска marketplace в hello портал Azure (выполните поиск «SQL Server {BYOL}»).

> [!IMPORTANT]
> образы виртуальных Машин BYOL toouse, необходимо иметь соглашение Enterprise с [License Mobility по программе Software Assurance в Azure](https://azure.microsoft.com/pricing/license-mobility/). Требуется действующая лицензия для hello версия или выпуск SQL Server требуется toouse. Вы должны [предоставляют hello необходимые BYOL сведения tooMicrosoft](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) в **10** дней подготовки виртуальной Машины. 

> [!NOTE]
> Это не hello возможных toochange лицензирования модели toouse виртуальной Машине SQL Server-минуту собственную лицензию. В этом случае необходимо создать новую виртуальную Машину BYOL и перенести toohello вашей базы данных новой виртуальной Машины. 

## <a name="manage-your-sql-vm"></a>Управление виртуальной машиной SQL
После подготовки виртуальной машины SQL Server вы можете выполнить несколько дополнительных задач по управлению. Во многих аспектах настройка и управление SQL Server ничем не отличаются от аналогичных процедур в локальном экземпляре SQL Server. Тем не менее некоторые задачи являются конкретного tooAzure. Hello следующих разделах описываются некоторые из этих областей сведениями toomore ссылки.

### <a name="connect-toohello-vm"></a>Подключение toohello виртуальной Машины
Одно из основных действий управления hello — tooyour tooconnect виртуальной Машине SQL Server через средства, такие как SQL Server Management Studio (SSMS). Инструкции по tooconnect tooyour нового SQL Server виртуальной Машины, в статье [подключения виртуальной машины SQL Server в Azure tooa](virtual-machines-windows-sql-connect.md).

### <a name="migrate-your-data"></a>Перенос данных
Если у вас есть существующая база данных, будет необходимо toomove, toohello обслуживаемого SQL виртуальной Машины. Список вариантов миграции и рекомендации см. в разделе [миграция tooSQL базы данных сервера на Виртуальной машине Azure](virtual-machines-windows-migrate-sql.md).

### <a name="configure-high-availability"></a>Настройка высокой доступности
Если требуется высокий уровень доступности, вам помогут группы доступности SQL Server. Это подразумевает использование нескольких виртуальных машин Azure в виртуальной сети. Hello портал Azure содержит шаблон, который задает настройки для вас. Дополнительные сведения см. в статье [Автоматическая настройка группы доступности AlwaysOn на виртуальной машине Azure в модели Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Toomanually настроить группу доступности и ассоциированного прослушивателя в разделе [Настройка группы доступности AlwaysOn в виртуальной Машине Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Дополнительные рекомендации по обеспечению высокого уровня доступности см. в статье [Высокий уровень доступности и аварийное восстановление для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-high-availability-dr.md).

### <a name="back-up-your-data"></a>Резервное копирование данных
Виртуальные машины Azure могут воспользоваться преимуществами [автоматического резервного копирования](virtual-machines-windows-sql-automated-backup.md), который регулярно создает резервные копии tooblob хранилища базы данных. Это также можно выполнять вручную. Дополнительные сведения см. в статье [Использование службы хранилища Azure для архивации и восстановления SQL Server](virtual-machines-windows-use-storage-sql-server-backup-restore.md). Обзор параметров резервного копирования и восстановления см. в статье [Резервное копирование и восстановление SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-backup-recovery.md).

### <a name="automate-updates"></a>Автоматизация обновлений
Можно использовать виртуальные машины Azure [автоматического исправления](virtual-machines-windows-sql-automated-patching.md) tooschedule периода обслуживания для установки важных windows и SQL Server обновляется автоматически.

### <a name="customer-experience-improvement-program-ceip"></a>Программа улучшения качества программного обеспечения (CEIP)
Hello программы улучшения качества (CEIP) включен по умолчанию. Периодически отправляет отчеты tooMicrosoft toohelp улучшить SQL Server. Нет ни одна задача управления требуется с помощью программы улучшения качества по, если вы хотите toodisable его после инициализации. Можно настроить или отключить hello программы улучшения качества по, соединение toohello виртуальной Машины с помощью удаленного рабочего стола. Затем запустите hello **использование отчетов об ошибках SQL Server и** программы. Выполните hello инструкции toodisable отчетов. 

Дополнительные сведения см. в разделе hello CEIP раздел hello [принять условия лицензии](https://msdn.microsoft.com/library/ms143343.aspx) раздела. 

## <a name="next-steps"></a>Дальнейшие действия

Ответы на вопросы о ценах см [цены рекомендации для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md) и hello [Azure странице цен](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Выберите целевой выпуска SQL Server в hello **операционной системы или программного обеспечения** списка. Просмотрите hello цены по-разному размера виртуальных машин.

У вас остались вопросы? Во-первых, в разделе hello [SQL Server на виртуальных машинах Azure часто задаваемые вопросы о](virtual-machines-windows-sql-server-iaas-faq.md). Но также добавить к вопросам и с комментариями toohello внизу toointeract разделы любой виртуальной Машине SQL сообщество Майкрософт и hello.
