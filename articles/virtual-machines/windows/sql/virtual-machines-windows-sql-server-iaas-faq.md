---
title: "Часто задаваемые вопросы об SQL Server на виртуальных машинах Azure | Документация Майкрософт"
description: "В этой статье содержатся ответы на часто задаваемые вопросы о запуске SQL Server в виртуальных машинах Azure."
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
ms.openlocfilehash: 447ece9653a4cf69153f9c85e222e3ea4e8bae16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Часто задаваемые вопросы по SQL Server на виртуальных машинах Azure
В этой статье содержатся ответы на некоторые наиболее распространенные вопросы о запуске [SQL Server в виртуальных машинах Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

1. **Как создать виртуальную машину Azure с SQL Server?**

    Самый простой способ — создать виртуальную машину с SQL Server. Учебник по регистрации в Azure и созданию виртуальной машины SQL на портале см. в статье [Подготовка виртуальной машины SQL Server на портале Azure](virtual-machines-windows-portal-sql-server-provision.md). Можно выбрать образ виртуальной машины, использующей лицензирование SQL Server с поминутной оплатой, или можно использовать образ, который позволяет использовать собственную лицензию SQL Server. Вы можете также вручную установить SQL Server на виртуальной машине и повторно использовать локальную лицензию. При использовании собственной лицензии у вас должно быть преимущество [Перемещение лицензий в рамках программы Software Assurance в Azure](https://azure.microsoft.com/pricing/license-mobility/). Дополнительные сведения см. в [руководстве по выбору ценовой категории для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **В чем разница между виртуальными машинами SQL и службой "База данных SQL"?**

    По существу выполнение SQL Server в виртуальной машине Azure не отличается от выполнения SQL Server в удаленном центре данных. В свою очередь, служба [База данных SQL](../../../sql-database/sql-database-technical-overview.md) предлагается на основе модели "база данных как услуга". При использовании Базы данных SQL у вас нет доступа к компьютерам, на которых размещаются ваши базы данных. Полное сравнение доступно в статье [Вы можете выбрать компонент SQL Server в облаке: база данных SQL Azure (PaaS) или SQL Server на виртуальных машинах Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Как перенести локальную базу данных SQL Server в облако?**

    Сначала создайте виртуальную машину Azure с экземпляром SQL Server. Затем перенесите локальные базы данных в этот экземпляр. Стратегии переноса данных см. в статье [Миграция базы данных SQL Server в экземпляр SQL Server на виртуальной машине Azure](virtual-machines-windows-migrate-sql.md).

1. **Можно ли установить второй экземпляр SQL Server в той же виртуальной машине? Можно изменить установленные компоненты экземпляра по умолчанию?**

    Да. Установочный носитель SQL Server находится в папке на диске **C** . Запустите файл **Setup.exe** из этого расположения, чтобы добавить новые экземпляры SQL Server или изменить другие компоненты SQL Server, установленные на виртуальной машине. Обратите внимание, что некоторые функции, такие как автоматическая архивация, автоматическое исправление и интеграция с Azure Key Vault, работают только с экземпляром по умолчанию.

1. **Можно ли удалить экземпляр по умолчанию SQL Server?**

    Да. Однако существуют определенные особенности. Как уже говорилось в предыдущем ответе, функции, которые используют [расширение агента IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md), работают только с экземпляром по умолчанию. Если вы удалите экземпляр по умолчанию, расширение будет непрерывно искать его и даже порождать ошибки, регистрируемые в журнале. У этих ошибок два источника: **служба управления учетными данными Microsoft SQL Server** и **агент IaaS Microsoft SQL Server**. Пример одной из ошибок показан ниже.
    
        A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. 
        
    Если вы решите удалить экземпляр по умолчанию, удалите и [расширение агента IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

1. **Как выполнить обновление до новой версии или выпуска SQL Server в виртуальной машине Azure?**

    В настоящее время выполнить обновление на месте для SQL Server в виртуальной машине Azure невозможно. Создайте виртуальную машину Azure с нужной версией или выпуском SQL Server, а затем перенесите базы данных на новый сервер с помощью стандартных [методов переноса данных](virtual-machines-windows-migrate-sql.md).

1. **Как установить лицензированную копию SQL Server в виртуальной машине Azure?**

    Это можно сделать двумя способами. Можно подготовить один из [образов виртуальных машин, которые поддерживают лицензии](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Кроме того, можно скопировать установочный носитель SQL Server на виртуальную машину Windows Server, а затем установить SQL Server на виртуальную машину. В соответствии с требованиями лицензирования у вас должно быть преимущество [Перемещение лицензий в рамках программы Software Assurance в Azure](https://azure.microsoft.com/pricing/license-mobility/). Дополнительные сведения см. в [руководстве по выбору ценовой категории для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Можно ли настроить виртуальную машину для использования собственной лицензии SQL Server, если она была создана из одного из образов коллекции с оплатой по мере использования?**

    Нет. Невозможно перейти с лицензирования с поминутной оплатой на свою собственную лицензию. Создайте виртуальную машину Azure, используя один из [образов BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), а затем перенесите базы данных на новый сервер с помощью стандартных [методов переноса данных](virtual-machines-windows-migrate-sql.md).

1. **Поддерживаются ли экземпляры отказоустойчивого кластера SQL Server на виртуальных машинах Azure?**

   Да. Вы можете [создать отказоустойчивый кластер Windows на платформе Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) и использовать локальные дисковые пространства (S2D) для хранилища кластера. Кроме того, можно использовать сторонние решения кластеризации или хранения, как описано в статье [Высокий уровень доступности и аварийное восстановление для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **Нужно ли платить за лицензирование SQL Server на виртуальной машине Azure, если она используется только для резервирования или отработки отказа?**

    Вам не нужно платить за лицензию на один сервер SQL Server, участвующий в качестве пассивной вторичной реплики в развертывании с высоким уровнем доступности, если у вас имеется Software Assurance и вы используете перемещение лицензий, как описано в разделе [Виртуальные машины — вопросы и ответы по лицензированию](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Как обновления и пакеты обновления применяются к виртуальной машине SQL Server?**

    Виртуальные машины позволяют контролировать сервер, в том числе время и способ применения обновлений. Что касается операционной системы, вы можете вручную применять обновления для Windows или включить службу расписаний под названием [Автоматическое исправление](virtual-machines-windows-sql-automated-patching.md). Эта служба устанавливает все обновления, помеченные как важные, включая обновления SQL Server из этой категории. Другие необязательные обновления для SQL Server необходимо устанавливать вручную.

1. **Можно ли настраивать конфигурации, которых нет в коллекции виртуальных машин (например Windows 2008 R2 + SQL Server 2012)?**

    Нет. Вы можете выбрать только один из представленных в коллекции образов виртуальных машин с SQL Server.

1. **Как установить SQL Server Data Tools в виртуальной машине Azure?**

     Скачайте инструменты SQL Server Data Tools со страницы [Microsoft SQL Server Data Tools ― Business Intelligence для Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313) и установите их.

## <a name="resources"></a>Ресурсы

Чтобы получить общие сведения об SQL Server на виртуальных машинах Azure, просмотрите видео [Azure VM is the best platform for SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)(Виртуальные машины Azure — лучшая платформа для SQL Server 2016). Полезные общие сведения по этой теме также можно найти в статье [Приступая к работе с SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).

Другие ресурсы:

* [Подготовка виртуальной машины SQL Server на портале Azure](virtual-machines-windows-portal-sql-server-provision.md)
* [Миграция базы данных в SQL Server на виртуальной машине Azure](virtual-machines-windows-migrate-sql.md)
* [Высокий уровень доступности и аварийное восстановление для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-high-availability-dr.md)
* [Рекомендации по оптимизации производительности SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-performance.md)
* [Шаблоны приложений и стратегии разработки для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 