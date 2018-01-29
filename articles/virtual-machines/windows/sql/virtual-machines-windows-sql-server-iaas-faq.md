---
title: "Часто задаваемые вопросы об SQL Server на виртуальных машинах Azure (Windows) | Документация Майкрософт"
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
ms.topic: troubleshooting
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 12/14/2017
ms.author: v-shysun
ms.openlocfilehash: 141dd1fe9e727f430b7c45dbb798f5471167c355
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-windows-azure-virtual-machines"></a>Часто задаваемые вопросы по SQL Server на виртуальных машинах Azure (Windows)

> [!div class="op_single_selector"]
> * [Windows](virtual-machines-windows-sql-server-iaas-faq.md)
> * [Linux](../../linux/sql/sql-server-linux-faq.md)

В этой статье содержатся ответы на некоторые распространенные вопросы о запуске [SQL Server на виртуальных машинах Windows Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

> [!NOTE]
> Это статье рассматриваются проблемы, относящиеся к SQL Server на виртуальных машинах Windows. Если вы используете SQL Server на виртуальных машинах Linux, см. [вопросы и ответы о виртуальных машинах Linux](../../linux/sql/sql-server-linux-faq.md).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a id="images"></a>Изображения

1. **Какие образах коллекции виртуальных машин SQL Server доступны?**

   Azure использует образы виртуальных машин для всех поддерживаемых основные выпуски SQL Server во всех выпусках Windows и Linux. Дополнительные сведения см. Полный список [образов виртуальных Машин Windows](virtual-machines-windows-sql-server-iaas-overview.md#payasyougo) и [образов виртуальных Машин Linux](../../linux/sql/sql-server-linux-virtual-machines-overview.md#create).

1. **Обновляются существующие образах коллекции виртуальных машин SQL Server**

   Каждые два месяца обновления образов SQL Server в коллекции виртуальных машин с последней Windows и Linux обновления. Для образов Windows Сюда входят все обновления, помеченные как важные обновления Windows, включая важные обновления для системы безопасности SQL Server и пакетов обновления. Для образов Linux Сюда входят последние обновления системы. Накопительные пакеты обновления SQL Server, обрабатываются по-разному для Linux и Windows. Для Linux накопительные пакеты обновления SQL Server также включается в обновление. Однако в данный момент виртуальные машины Windows не обновляются с накопительными пакетами обновления для SQL Server или Windows Server.

1. **Образы виртуальных машин SQL Server можно получить удален из каталога?**

   Да. Azure поддерживает только одно изображение в основной номер версии и выпуска. Например при выпуске нового пакета обновления SQL Server, Azure добавляет новый образ в коллекцию для этого пакета обновления. Образ SQL Server для предыдущего пакета обновления немедленно удаляется из портала Azure. Тем не менее он доступен для подготовки из PowerShell для следующих трех месяцев. После трех месяцев на предыдущем рисунке пакет службы больше не доступны. Эта политика удаления также можно применить в случае версии SQL Server не поддерживается при достижении конца своего жизненного цикла.

1. **Можно ли настраивать конфигурации, которых нет в коллекции виртуальных машин (например Windows 2008 R2 + SQL Server 2012)?**

   Нет. Вы можете выбрать только один из представленных в коллекции образов виртуальных машин с SQL Server.

## <a name="creation"></a>Создание

1. **Как создать виртуальную машину Azure с SQL Server?**

   Самый простой способ — создать виртуальную машину с SQL Server. Руководство по регистрации в Azure и создание виртуальной Машины SQL на портале см. в разделе [подготовки виртуальной машины SQL Server на портале Azure](virtual-machines-windows-portal-sql-server-provision.md). Можно выбрать образ виртуальной машины, использующей лицензирование SQL Server с поминутной оплатой, или можно использовать образ, который позволяет использовать собственную лицензию SQL Server. Кроме того, вы можете вручную установить SQL Server на виртуальной машине, используя выпуск с бесплатной лицензией (Developer или Express) или предоставив существующую локальную лицензию. При использовании собственной лицензии у вас должно быть преимущество [Перемещение лицензий в рамках программы Software Assurance в Azure](https://azure.microsoft.com/pricing/license-mobility/). Дополнительные сведения см. в [руководстве по выбору ценовой категории для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Как перенести локальную базу данных SQL Server в облако?**

   Сначала создайте виртуальную машину Azure с экземпляром SQL Server. Затем перенесите локальные базы данных в этот экземпляр. Стратегии переноса данных см. в статье [Миграция базы данных SQL Server в экземпляр SQL Server на виртуальной машине Azure](virtual-machines-windows-migrate-sql.md).

## <a name="licensing"></a>Лицензирование

1. **Как установить лицензированную копию SQL Server в виртуальной машине Azure?**

   Это можно сделать двумя способами. Можно подготовить один из [образов виртуальных машин, которые поддерживают лицензии](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Кроме того, можно скопировать установочный носитель SQL Server на виртуальную машину Windows Server, а затем установить SQL Server на виртуальную машину. В соответствии с требованиями лицензирования у вас должно быть преимущество [Перемещение лицензий в рамках программы Software Assurance в Azure](https://azure.microsoft.com/pricing/license-mobility/). Дополнительные сведения см. в [руководстве по выбору ценовой категории для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Можно ли настроить виртуальную машину для использования собственной лицензии SQL Server, если она была создана из одного из образов коллекции с оплатой по мере использования?**

   Нет. Возможность перейти с лицензирования с поминутной оплатой на свою собственную лицензию не предусмотрена. Создайте виртуальную машину Azure, используя один из [образов BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), а затем перенесите базы данных на новый сервер с помощью стандартных [методов переноса данных](virtual-machines-windows-migrate-sql.md).

1. **Нужно ли платить за лицензирование SQL Server на виртуальной машине Azure, если она используется только для резервирования или отработки отказа?**

   Вам не нужно платить за лицензию на один сервер SQL Server, участвующий в качестве пассивной вторичной реплики в развертывании с высоким уровнем доступности, если у вас есть Software Assurance и вы используете перемещение лицензий, как описано в разделе [Виртуальные машины — вопросы и ответы по лицензированию](http://azure.microsoft.com/pricing/licensing-faq/). В противном случае вам нужно приобрести лицензию.


## <a name="administration"></a>Администрирование

1. **Можно ли установить второй экземпляр SQL Server в той же виртуальной машине? Можно изменить установленные компоненты экземпляра по умолчанию?**

   Да. Установочный носитель SQL Server находится в папке на диске **C** . Запустите файл **Setup.exe** из этого расположения, чтобы добавить новые экземпляры SQL Server или изменить другие компоненты SQL Server, установленные на виртуальной машине. Обратите внимание, что некоторые функции, такие как автоматическая архивация, автоматическое исправление и интеграция с Azure Key Vault, работают только с экземпляром по умолчанию.

1. **Можно ли удалить экземпляр по умолчанию SQL Server?**

   Да. Однако существуют определенные особенности. Как уже говорилось в предыдущем ответе, функции, которые используют [расширение агента IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md), работают только с экземпляром по умолчанию. Если вы удалите экземпляр по умолчанию, расширение будет непрерывно искать его и даже порождать ошибки, регистрируемые в журнале. У этих ошибок два источника: **служба управления учетными данными Microsoft SQL Server** и **агент IaaS Microsoft SQL Server**. Пример одной из ошибок показан ниже.

      При подключении к SQL Server произошла ошибка, связанная с сетью или с определенным экземпляром. Сервер не найден или недоступен.

   Если вы решите удалить экземпляр по умолчанию, удалите и [расширение агента IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).
   
   >[!NOTE]
   >Плата за использование виртуальной машины Azure SQL Server начисляется, как описано в статье [Руководство по выбору ценовой категории для виртуальных машин SQL Server в Azure](virtual-machines-windows-sql-server-pricing-guidance.md). Если удалить SQL Server, плата за использование продолжит взиматься. Если вам больше не нужен SQL Server, можно развернуть новую виртуальную машину и перенести туда данные и приложения. Затем виртуальную машину SQL Server можно удалить.

## <a name="updating-and-patching"></a>Обновления и исправления

1. **Как выполнить обновление до новой версии или выпуска SQL Server в виртуальной машине Azure?**

   В настоящее время выполнить обновление на месте для SQL Server в виртуальной машине Azure невозможно. Создайте виртуальную машину Azure с нужной версией или выпуском SQL Server, а затем перенесите базы данных на новый сервер с помощью стандартных [методов переноса данных](virtual-machines-windows-migrate-sql.md).

1. **Как обновления и пакеты обновления применяются к виртуальной машине SQL Server?**

   Виртуальные машины позволяют контролировать сервер, в том числе время и способ применения обновлений. Что касается операционной системы, вы можете вручную применять обновления для Windows или включить службу расписаний под названием [Автоматическое исправление](virtual-machines-windows-sql-automated-patching.md). Эта служба устанавливает все обновления, помеченные как важные, включая обновления SQL Server из этой категории. Другие необязательные обновления для SQL Server необходимо устанавливать вручную.

## <a name="general"></a>Общие сведения

1. **Поддерживаются ли экземпляры отказоустойчивого кластера SQL Server на виртуальных машинах Azure?**

   Да. Вы можете [создать отказоустойчивый кластер Windows на платформе Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) и использовать локальные дисковые пространства (S2D) для хранилища кластера. Кроме того, можно использовать сторонние решения кластеризации или хранения, как описано в статье [Высокий уровень доступности и аварийное восстановление для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **В чем разница между виртуальными машинами SQL и службой "База данных SQL"?**

   По существу выполнение SQL Server в виртуальной машине Azure не отличается от выполнения SQL Server в удаленном центре данных. В свою очередь, служба [База данных SQL](../../../sql-database/sql-database-technical-overview.md) предлагается на основе модели "база данных как услуга". При использовании Базы данных SQL у вас нет доступа к компьютерам, на которых размещаются ваши базы данных. Полное сравнение доступно в статье [Вы можете выбрать компонент SQL Server в облаке: база данных SQL Azure (PaaS) или SQL Server на виртуальных машинах Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Как установить SQL Server Data Tools в виртуальной машине Azure?**

    Скачайте инструменты SQL Server Data Tools со страницы [Microsoft SQL Server Data Tools ― Business Intelligence для Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313) и установите их.

## <a name="resources"></a>Ресурсы

**Для виртуальных машин Windows**:

* [Приступая к работе с SQL Server на виртуальных машинах Azure (Windows)](virtual-machines-windows-sql-server-iaas-overview.md)
* [Подготовка виртуальной машины SQL Server на базе Windows](virtual-machines-windows-portal-sql-server-provision.md).
* [Миграция базы данных в SQL Server на виртуальной машине Azure](virtual-machines-windows-migrate-sql.md)
* [Высокий уровень доступности и аварийное восстановление для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-high-availability-dr.md)
* [Рекомендации по оптимизации производительности SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-performance.md)
* [Шаблоны приложений и стратегии разработки для SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md)

**Для виртуальных машин Linux**:

* [Обзор SQL Server на виртуальных машинах Linux](../../linux/sql/sql-server-linux-virtual-machines-overview.md).
* [Подготовка виртуальной машины SQL Server на базе Linux на портале Azure](../../linux/sql/provision-sql-server-linux-virtual-machine.md)
* [Frequently asked questions for SQL Server on Linux Azure Virtual Machines](../../linux/sql/sql-server-linux-faq.md) (Часто задаваемые вопросы об SQL Server на виртуальных машинах Azure (Linux))
* [Документация по SQL Server в Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-overview)
