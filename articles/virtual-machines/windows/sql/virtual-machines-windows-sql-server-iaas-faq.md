---
title: "aaaSQL Server на виртуальных машинах Azure часто задаваемые вопросы о | Документы Microsoft"
description: "В этой статье содержатся ответы toofrequently вопросы и ответы о запуске SQL Server на виртуальных машинах Azure."
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Часто задаваемые вопросы по SQL Server на виртуальных машинах Azure
Этот раздел содержит ответы toosome из hello самые распространенные вопросы о запуске [SQL Server на виртуальных машинах Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

1. **Как создать виртуальную машину Azure с SQL Server?**

    Hello простым решением является toocreate виртуальной машины, которая включает SQL Server. Руководство по регистрации в Azure и создание виртуальной Машины SQL из портала hello см. в разделе [подготовки виртуальной машины SQL Server в портале Azure hello](virtual-machines-windows-portal-sql-server-provision.md). Можно выбрать образ виртуальной машины, который использует SQL Server минуту лицензирования, или можно использовать изображение, которое позволяет вам toobring собственную лицензию SQL Server. Также имеется возможность hello вручную установки SQL Server на виртуальной Машине и повторное использование лицензии на локальный. При использовании собственной лицензии у вас должно быть преимущество [Перемещение лицензий в рамках программы Software Assurance в Azure](https://azure.microsoft.com/pricing/license-mobility/). Дополнительные сведения см. в [руководстве по выбору ценовой категории для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Что такое hello разницу между виртуальных машин SQL и hello служба базы данных SQL**

    По существу выполнение SQL Server в виртуальной машине Azure не отличается от выполнения SQL Server в удаленном центре данных. В свою очередь, служба [База данных SQL](../../../sql-database/sql-database-technical-overview.md) предлагается на основе модели "база данных как услуга". С базой данных SQL у вас доступ toohello компьютерах размещения баз данных. Полное сравнение доступно в статье [Вы можете выбрать компонент SQL Server в облаке: база данных SQL Azure (PaaS) или SQL Server на виртуальных машинах Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Как перенести Мои toohello базы данных SQL Server в локальной среде облака**

    Сначала создайте виртуальную машину Azure с экземпляром SQL Server. Затем перенести toothat экземпляр локальной базы данных. Стратегии миграции данных, в разделе [перенести tooSQL базы данных сервера SQL Server на виртуальной Машине Azure](virtual-machines-windows-migrate-sql.md).

1. **Можно ли установить второй экземпляр SQL Server на hello одной виртуальной Машины? Можно изменить установленные компоненты экземпляра по умолчанию hello**

    Да. Hello установочного носителя SQL Server находится в папке на hello **C** диска. Запустите **Setup.exe** из этого расположения tooadd новые экземпляры SQL Server или toochange других установлены компоненты SQL Server на компьютере hello. Обратите внимание, что некоторые функции, такие как автоматическое резервное копирование, автоматического исправления и интеграция хранилища ключей Azure, работают только с экземпляром по умолчанию hello.

1. **Можно удалить экземпляр SQL Server по умолчанию hello**

    Да. Однако существуют определенные особенности. Как указано в предыдущий ответ hello, функции, которые зависят от hello [расширения агента SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md) работать только на экземпляре по умолчанию hello. При удалении экземпляра по умолчанию hello расширение hello продолжается toolook и могут возникать ошибки в журнале событий. Эти ошибки представляют собой из следующих двух источников hello: **управления учетных данных Microsoft SQL Server** и **агента IaaS Microsoft SQL Server**. Одной из ошибок hello может быть примерно toohello следующее:
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    Если экземпляр по умолчанию hello toouninstall, удалите hello [расширения агента SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md) также.

1. **Как обновить tooa новой версии и выпуска hello SQL Server на виртуальной Машине Azure?**

    В настоящее время выполнить обновление на месте для SQL Server в виртуальной машине Azure невозможно. Создайте новую виртуальную машину Azure с hello требуемого версия или выпуск SQL Server и затем перенести базы данных toohello нового сервера с использованием стандарта [методов переноса данных](virtual-machines-windows-migrate-sql.md).

1. **Как установить лицензированную копию SQL Server в виртуальной машине Azure?**

    Существует два способа toodo это. Можно подготовить один hello [образы виртуальных машин, которые поддерживает лицензий](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Другой вариант — носителя установки tooa виртуальной Машины Windows Server toocopy hello SQL Server и установите SQL Server на hello виртуальной Машины. В соответствии с требованиями лицензирования у вас должно быть преимущество [Перемещение лицензий в рамках программы Software Assurance в Azure](https://azure.microsoft.com/pricing/license-mobility/). Дополнительные сведения см. в [руководстве по выбору ценовой категории для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Можно ли изменить toouse ВМ собственную лицензию SQL Server, если он был создан из одного из образов по мере использования коллекции hello?**

    Нет. Нельзя перейти из лицензирования toousing минуту собственную лицензию. Создание новой виртуальной машины Azure с помощью одного из hello [изображения BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), и затем перенести базы данных toohello нового сервера с использованием стандарта [методов переноса данных](virtual-machines-windows-migrate-sql.md).

1. **Поддерживаются ли экземпляры отказоустойчивого кластера SQL Server на виртуальных машинах Azure?**

   Да. Вы можете [создать отказоустойчивый кластер Windows в Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) и использования дисковых пространств (S2D) для хранения данных кластера hello. Кроме того, можно использовать сторонние решения кластеризации или хранения, как описано в статье [Высокий уровень доступности и аварийное восстановление для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **Нужно ли toopay toolicense SQL Server на Виртуальной машине Azure, если он используется только для режима ожидания или отработку отказа?**

    У вас toopay toolicense один SQL Server участвующие в качестве пассивного вторичной реплики в развертывании высокого уровня ДОСТУПНОСТИ, если вы используете Software Assurance и используйте License Mobility, как описано в [виртуальной машины вопросы и ответы](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Как обновления и пакеты обновления применяются к виртуальной машине SQL Server?**

    Виртуальные машины позволяют управлять хост-компьютера hello, включая время и способ установки обновлений. Для hello операционной системы, можно вручную применить обновления windows или включить планирования службу под названием [автоматического исправления](virtual-machines-windows-sql-automated-patching.md). Эта служба устанавливает все обновления, помеченные как важные, включая обновления SQL Server из этой категории. TooSQL другие необязательные обновления, сервер должен быть установлен вручную.

1. **Это возможно tooset конфигурации, не отображаются в коллекции виртуальных машин hello (для, например Windows 2008 R2 + SQL Server 2012)?**

    Нет. Для образов коллекции виртуальных машин, включающие SQL Server необходимо выбрать один из образов hello.

1. **Как установить SQL Server Data Tools в виртуальной машине Azure?**

     Загрузите и установите средства hello данных SQL из [Microsoft SQL Server Data Tools - Business Intelligence для Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Ресурсы

Общие сведения о SQL Server на виртуальных машинах Azure видео hello [виртуальная машина Azure — hello лучшей платформы для SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). Можно также получить хорошее представление в разделе hello [SQL Server на виртуальных машинах Azure Обзор](virtual-machines-windows-sql-server-iaas-overview.md).

Другие ресурсы:

* [Подготовьте виртуальную машину SQL Server в hello портала Azure](virtual-machines-windows-portal-sql-server-provision.md)
* [Миграция базы данных tooSQL Server на Виртуальной машине Azure](virtual-machines-windows-migrate-sql.md)
* [Высокий уровень доступности и аварийное восстановление для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-high-availability-dr.md)
* [Рекомендации по оптимизации производительности SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-performance.md)
* [Шаблоны приложений и стратегии разработки для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 