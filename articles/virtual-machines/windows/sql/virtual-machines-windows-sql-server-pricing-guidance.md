---
title: "затраты на aaaManage эффективно для SQL Server на виртуальных машинах Azure | Документы Microsoft"
description: "Предоставляет рекомендации по выбору hello правой виртуальной машины SQL Server модель ценообразования."
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>Руководство по выбору ценовой категории для виртуальных машин SQL Server в Azure

В этом разделе приводятся рекомендации по выбору ценовой категории для виртуальных машин SQL Server в Azure. Существует несколько вариантов, которые влияют на стоимость и является правом изображении hello важные toopick, которая распределяет затраты с бизнес-требованиями.

## <a name="free-licensed-sql-server-editions"></a>Выпуски SQL Server с бесплатными лицензиями

Toodevelop следует проверить, или пробная версия сборки, а затем использовать hello освободить лицензию **SQL Server Developer edition**. Этот выпуск содержит все данные в SQL Server Enterprise edition, поэтому его можно использовать toobuild любое приложение, требуется. Он просто не допускается toorun в рабочей среде. Виртуальную Машину SQL Server Developer только взимает плату за hello стоимость hello виртуальной Машины, не для лицензирования SQL Server.

Если требуется toorun упрощенных рабочей нагрузки в рабочей среде (< 4 ядра, < 1 ГБ памяти, < 10 ГБ/базы данных), затем использовать hello освободить лицензию **выпуска SQL Server Express**. Виртуальной Машине SQL Express будут только плату за hello стоимость hello виртуальной Машины, не Лицензирование SQL.

Кроме того, вы можете сэкономить средства на этих рабочих нагрузках разработки и тестирования или упрощенных рабочих нагрузках, выбрав меньший размер виртуальной машины, который для них подходит. Hello DS1v2 может быть хорошим выбором для этих рабочих нагрузок.

toocreate SQL Server 2016 Azure виртуальной Машины с одного из этих образов см. следующие ссылки hello:

- [Виртуальная машина SQL Server 2016 Developer в Azure](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [Виртуальная машина SQL Server 2016 Express в Azure](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>Платные выпуски SQL Server

При наличии не облегченного рабочей нагрузке, используйте один из следующих выпусков SQL Server hello:

| Выпуск SQL Server | Рабочая нагрузка |
|-----|-----|
| Web | Небольшие веб-сайты |
| Standard | Небольшие toomedium рабочих нагрузок |
| Enterprise | Большие и критически важные рабочие нагрузки|

У вас есть два toopay варианты лицензирования SQL Server для следующих выпусков: *плата за использование* или *использовать собственную лицензию*.

### <a name="pay-per-usage"></a>Оплата за использование

**Плательщики лицензия SQL Server hello за использование** означает, что hello / мин стоимость выполнения hello виртуальной Машины Azure включает стоимость лицензии SQL Server hello hello. Вы увидите hello цены для hello различных выпусках SQL Server (Web, Standard, Enterprise) на hello [виртуальной Машины Azure на странице цен](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Hello затрат hello одинаково для всех версий SQL Server (2008 R2 too2016). Как с SQL Server в общем случае лицензирования hello стоимость лицензирования в минуту зависит hello число ядер виртуальной Машины.

Оплата hello SQL Server лицензии на использование рекомендуется для:

- Временные или периодические рабочие нагрузки. Например, приложение, которое требуется toosupport события для нескольких месяцев каждый год или бизнес-аналитике по понедельникам.
- Рабочие нагрузки с неизвестным временем существования или масштабом. Например, это может быть приложение, не востребованное в течение нескольких месяцев, или приложение, которое может требовать больше или меньше вычислительной мощности в зависимости от потребностей.

toocreate SQL Server 2016 Azure виртуальной Машины с одного из этих образов оплаты в зависимости от использования см. следующие ссылки hello:

- [Виртуальная машина SQL Server 2016 Web в Azure](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [Виртуальная машина SQL Server 2016 Standard в Azure](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [Виртуальная машина SQL Server 2016 Enterprise в Azure](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> При создании виртуальной машины с SQL Server в Azure portal hello hello предполагаемое месячные затраты на hello **выберите размер** колонки не включает стоимость лицензирования SQL Server. Это стоимость hello hello виртуальной Машины отдельно.
>
> ![Колонка выбора размера виртуальной машины](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Hello освободить лицензию Express Edition и Developer Edition сервера SQL Server это итоговая оценочная стоимость hello. Однако для Web, Standard и Enterprise, найти hello дополнительных расходов на лицензирование SQL на hello [страница цен в виртуальных машинах](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). На странице цен hello выберите целевой выпуска SQL Server.

### <a name="bring-your-own-license-byol"></a>Использование собственных лицензий (BYOL)

**Перевод собственную лицензию SQL Server через License Mobility**, также называется tooas **BYOL**, означает использование существующего тома лицензия SQL Server на виртуальной Машине Azure в программе Software Assurance. ВМ SQL Server с помощью BYOL только взимает плату за hello стоимость выполнения hello виртуальной Машины, не для лицензирования SQL Server, учитывая, что вы уже приобрели лицензии и Software Assurance по программе корпоративного лицензирования.

Использование собственных лицензий SQL посредством License Mobility рекомендуется для следующих ситуаций.

- Непрерывные рабочие нагрузки. Например, приложение, которое требуется toosupport бизнес-операции 24 x 7.
- Рабочие нагрузки с известным временем существования и масштабом. Например, приложение, которое требуется для всего года hello и какие запросу был прогнозируемое.

toouse BYOL виртуальная машина SQL Server, необходимо иметь лицензию для SQL Server Standard или Enterprise и [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), который — это обязательный параметр выполнения некоторых [корпоративного лицензирования](https://www.microsoft.com/en-us/download/details.aspx?id=10585) программ и необязательный приобрести с другими разделами.  Hello ценам, предоставляемые в рамках программ корпоративного лицензирования зависит от типа hello соглашения и hello или обязательств, и количество tooSQL сервера. Но, как правило, переводя собственную лицензию для непрерывного рабочих нагрузок имеет следующие преимущества hello:

| Преимущество BYOL | Описание |
|-----|-----|
| **Уменьшение затрат** | Использовать собственную лицензию SQL Server выгоднее, чем платить за ее использование, если рабочая нагрузка на SQL Server Standard или SQL Server Enterprise будет выполняться непрерывно *более 10 месяцев*. |
| **Долгосрочная экономия** | В среднем это *30% дешевле в год* toobuy или продлить лицензию SQL Server для hello первый 3 года. Кроме того после 3 года, не требуется toorenew hello лицензии, просто оплаты по программе Software Assurance. Это *удешевляет использование на 200 %*. |
| **Бесплатная пассивная вторичная реплика** | Еще одним преимуществом приведению собственную лицензию — hello [освободить лицензирования для пассивных одной из вторичных реплик](https://azure.microsoft.com/pricing/licensing-faq/) на SQL Server для обеспечения высокого уровня доступности. Это снижает в половину hello лицензирования стоимость высокодоступное развертывание SQL Server (например, при использовании групп доступности AlwaysOn). Hello права toorun hello пассивный получатель обеспечивается hello преимущество переключения серверов Software Assurance. |

toocreate SQL Server 2016 Azure виртуальной Машины с одного из этих образов перевести--владельцем лицензии см. виртуальные машины hello префикс «{BYOL}».

- [Виртуальная машина SQL Server 2016 Enterprise в Azure](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [Виртуальная машина SQL Server 2016 Standard в Azure](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Сообщите нам в течение 10 дней количество лицензий на SQL Server, которые вы будете использовать в Azure. Hello ссылки toohello предыдущие образы имеют инструкции о том, как toodo это.

## <a name="avoid-unecessary-costs"></a>Устранение лишних затрат

При использовании любой рабочей нагрузки, которые не выполняются непрерывно, рассмотрите возможность завершение работы виртуальной машины hello неактивные периоды hello. Вы платите только за то, что используете.

Например если вы пытаетесь просто ожидания SQL Server на Виртуальной машине Azure, нет смысла tooincur расходов можно случайно оставить для недели. Одним из решений является toouse hello [возможность автоматического завершения работы](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Автоматическое завершение работы виртуальной машины SQL](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

Автоматическое завершение работы — лишь одна функция из большого набора аналогичных функциональных возможностей, предоставляемых [DevTest Azure Labs](https://azure.microsoft.com/services/devtest-lab).

Для других рабочих процессов рассмотрите возможность автоматического завершения работы и перезапуска виртуальных машин Azure с помощью решения на основе сценариев, например [службы автоматизации Azure](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> Выключение и освобождение ВМ — hello единственным способом tooavoid расходов. Просто остановка или с помощью tooshut параметры питания вниз hello виртуальной Машины по-прежнему может привести к дополнительным расходам.

## <a name="next-steps"></a>Дальнейшие действия

Общие рекомендации по ценам Azure приведены в статье [Предотвращение непредвиденных расходов с помощью функции выставления счетов и управления затратами в Azure](../../../billing/billing-getting-started.md).

Hello последнюю виртуальных машин цен, включая SQL Server, см. hello [виртуальной Машины Azure на странице цен](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Просмотрите другие разделы, посвященные виртуальным машинам SQL Server, в статье [Приступая к работе с SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).
