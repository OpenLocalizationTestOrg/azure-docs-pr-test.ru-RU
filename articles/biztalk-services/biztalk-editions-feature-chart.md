---
title: "aaaLearn о функциях в выпусках служб BizTalk | Документы Microsoft"
description: "Сравнение возможностей hello выпусков служб BizTalk hello: Free, Developer, Basic, Standard и Premium. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>Службы BizTalk: диаграмма выпусков

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Существует несколько выпусков служб BizTalk Azure. Используйте этот toodetermine статьи, какой выпуск соответствует потребностям вашего сценария и бизнес.

## <a name="compare-hello-editions"></a>Сравнение выпусков hello
**Free (предварительный просмотр)**

Позволяет создавать гибридные подключения и управлять ими. Гибридное подключение будет легко tooconnect tooan веб-сайте Azure в локальной системе, как SQL Server.

**Developer**

Включает создание гибридных подключений, обработку сообщений EAI и EDI с помощью простого портала управления для торговых партнеров, поддержку общих схем EDI и обширные возможности обработки EDI через X12 и AS2. Можно создавать общие сценарии EAI подключения службы в облаке hello с любой tooread протоколов HTTP/S, REST, FTP, WCF и SFTP и записывать сообщения.  Используйте подключение локальной tooon бизнес-системами с адаптерами SAP, Oracle eBusiness, база данных Oracle, Siebel и SQL Server готова к использованию. Используйте ориентированную на разработчиков среду с инструментами Visual Studio, упрощающими разработку и развертывание. Ограниченная toodevelopment целей и тестирования только с нет службы соглашения об уровне (SLA).

**базовая;**

Включает большую часть возможностей hello разработчика с ростом в гибридных подключений, мосты EAI, соглашения EDI и пакет адаптера BizTalk подключений. Также обеспечивает высокий уровень доступности и tooscale параметр hello с соглашения уровня службы (SLA).

**Стандартный**

Включает все основные возможности hello с ростом в гибридных подключений, мосты EAI, соглашения EDI и пакет адаптера BizTalk подключений. Также обеспечивает высокий уровень доступности и tooscale параметр hello с соглашения уровня службы (SLA).

**Премиальный**

Включает все стандартные возможности hello с ростом в гибридных подключений, мосты EAI, соглашения EDI и пакет адаптера BizTalk подключений. Также включает архивирования, высокий уровень доступности и tooscale параметр hello с соглашения уровня службы (SLA).

## <a name="editions-chart"></a>Диаграмма выпусков
Hello следующей таблице перечислены различия hello.

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Free (предварительный просмотр)</th>
        <th>Developer</th>
        <th>базовая;</th>
        <th>Стандартная</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>Начальная цена</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Цены — службы BizTalk Azure</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full">Калькулятор цен Azure</a></td>
</tr>
<tr>
<td><strong>Минимальная конфигурация по умолчанию</strong></td>
<td>Один модуль Free</td>
<td>1 Модуль Developer</td>
<td>1 Модуль Basic</td>
<td>1 Модуль Standard</td>
<td>1 Модуль Premium</td>
</tr>
<tr>
<td><strong>Масштабирование</strong></td>
<td>Без масштабирования</td>
<td>Без масштабирования</td>
<td>Да, с шагом в 1 модуль Basic</td>
<td>Да, с шагом в 1 модуль Standard</td>
<td>Да, с шагом в 1 модуль Premium</td>
</tr>
<tr>
<td><strong>Максимально разрешенный масштаб</strong></td>
<td>Без масштабирования</td>
<td>Без масштабирования</td>
<td>Too8 единицы</td>
<td>Too8 единицы</td>
<td>Too8 единицы</td>
</tr>
<tr>
<td><strong>Количество мостов EAI на единицу</strong></td>
<td>Не включено</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
Включает соглашения об управлении торговыми партнерами.</td>
<td>Не включено</td>
<td>Включено. 10 соглашений на единицу.</td>
<td>Включено. 50 соглашений на единицу.</td>
<td>Включено. 250 соглашений на единицу.</td>
<td>Включено. 1000 соглашений на единицу.</td>
</tr>
<tr>
<td><strong>Количество гибридных подключений на единицу</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>Объем передачи данных гибридных подключений (ГБ) на единицу</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>Служба адаптера BizTalk подключения локальной tooon бизнес-системам</strong></td>
<td>Не включено</td>
<td>1 подключение</td>
<td>2 подключений</td>
<td>5 подключений</td>
<td>25 подключений</td>
</tr>
<tr>
<td align="left"><strong>Поддерживаемые протоколы и системы:</strong>
<ul>
<li>HTTP</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>Шина обслуживания (SB)</li>
<li>Большой двоичный объект Azure</li>
<li>Интерфейсы API REST</li>
</ul>
</td>
<td>Не включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
</tr>
<tr>
<td><strong>Высокая доступность</strong>
<br/><br/>
Для соглашения об уровне обслуживания (SLA) см. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">сведения о ценах на службы BizTalk Azure</a>.
</td>
<td>Не включено</td>
<td>Не включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
</tr>
<tr>
<td><strong>Резервное копирование и восстановление</strong></td>
<td>Не включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
</tr>
<tr>
<td><strong>Отслеживание</strong></td>
<td>Не включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
</tr>
<tr>
<td><strong>Архивация</strong><br/><br/>
Включает невозможность отказа на получение (NRR) и возможность загрузки отслеживаемых сообщений.</td>
<td>Не включено</td>
<td>Включено</td>
<td>Не включено</td>
<td>Не включено</td>
<td>Включено</td>
</tr>
<tr>
<td><strong>Использование пользовательского кода</strong></td>
<td>Не включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
</tr>
<tr>
<td><strong>Использование преобразований, в том числе настраиваемых XSLT</strong></td>
<td>Не включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
<td>Включено</td>
</tr>
</table>

> [!NOTE]
> Высокая доступность предполагает наличие нескольких виртуальных машин в одной единице BizTalk для обеспечения устойчивости к сбоям оборудования.
> 
> 

## <a name="faqs"></a>Часто задаваемые вопросы
#### <a name="what-is-a-biztalk-unit"></a>Что такое "единица BizTalk"?
«Единица» — hello атомарном уровне развертывания служб Azure BizTalk. Выпуски поставляются с модулями, которые различаются вычислительной мощностью и объемом памяти. Например, единица в выпуске Basic имеет больше возможностей, чем в Developer, единица в выпуске Standard — больше возможностей, чем в Basic, и т. д. Масштабирование службы BizTalk выполняется относительно единиц.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>Что такое hello разницу между служб BizTalk и виртуальной Машины Azure BizTalk
Службы BizTalk предоставляет true архитектура платформы как услуга (PaaS) для создания решений интеграции в облаке hello. Модель PaaS hello, полностью сосредоточиться на логике приложения hello и оставить все tooMicrosoft управления hello инфраструктуры, включая:

* Нет необходимости toomanage или исправление для виртуальных машин.
* Корпорация Майкрософт обеспечивает доступность.
* Можно контролировать масштаб по требованию, просто запросив более или менее емкости через портал Azure hello.

BizTalk Server на виртуальных машинах Azure предоставляет архитектуру "инфраструктура как услуга" (IaaS). Создание виртуальных машин и настройте их так же, как в локальной среде, сделав его проще toorun существующих приложений в облаке hello без изменения кода. С IaaS по-прежнему отвечает за настройку hello виртуальных машин, управление виртуальными машинами hello (например, установка программного обеспечения и исправлений ОС) и архитектуры приложения hello для обеспечения высокой доступности.

Если вы хотите создавать новые решения интеграции, требующие минимальных издержек на управление инфраструктурой, используйте службы BizTalk. Если вам нужна tooquickly перенести существующие решения BizTalk или поиск по запросу среды toodevelop и тестирования BizTalk Server приложения, используют BizTalk Server на виртуальной машине Azure.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>Что такое hello разницу между службы адаптера BizTalk и гибридные подключения
Hello службы адаптера BizTalk используется службой BizTalk Azure. Hello службы адаптера BizTalk использует hello пакет адаптера BizTalk tooconnect tooan в локальной строке из БИЗНЕС-системе. Гибридное подключение обеспечивает простой и удобный способ tooconnect приложения Azure, так же, как hello веб-приложений в службе приложений Azure и мобильных служб Azure, tooan локальных ресурсов.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>Что означает "Объем передачи данных гибридных подключений (ГБ) на единицу"? Это за минуту, час, день, неделю или месяц? Что происходит при достижении предела hello?
Hello гибридного подключения себестоимость зависит от выпуска служб BizTalk hello. Проще говоря, затраты зависят от объема передаваемых данных. Например, ежедневные затраты на передачу 10 ГБ данных меньше, чем затраты на передачу 100 ГБ ежедневно. Используйте hello [калькулятор цен](https://azure.microsoft.com/pricing/calculator/?scenario=full) для определенных затрат toodetermine службы BizTalk. Как правило ежедневно применяются ограничения hello. Если будет превышено ограничение hello, все избыточные оплачивается hello частотой 1 доллара США за ГБ.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>При создании соглашения в службах BizTalk, почему hello число мосты перейти вверх на два вместо одного?
Каждое соглашение состоит из двух разных мостов: моста стороны отправки и моста стороны приема.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>Что произойдет, помеченным hello предел квоты на количество hello мосты или соглашения?
Вы не удается toodeploy любые новые мосты или создать новые соглашения. toodeploy дополнительные необходимые tooscale toomore единицы службы BizTalk hello или высокого выпуска обновления tooa.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>Как перенести с одного уровня tooanother службы BizTalk?
Hello бесплатный выпуск не может быть уровня tooanother миграции или «масштабируемых» и не удается создать резервную копию и восстановить tooanother уровня. Если требуется другой уровень, создайте новую службу BizTalk с помощью нового уровня hello. Все артефакты, созданные с помощью hello бесплатный выпуск, включая гибридных подключений, toobe необходимость восстановить на hello новую службу BizTalk. 

Для остальных выпусков hello hello архивирования и восстановления использовать для выполнения перехода от одного уровня tooanother вашей артефакты. Например, создать резервную копию вашей артефакты hello стандартном уровне, а затем восстановить их toohello уровня Premium. [Службы BizTalk: Резервное копирование и восстановление](biztalk-backup-restore.md) описаны hello поддерживаемые пути миграции и перечисляет, какие артефакты резервного копирования. Обратите внимание, что для гибридных подключений нельзя создать резервные копии. После резервного копирования и восстановления tooa новый уровень, затем воссоздать hello гибридных подключений.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>Hello службы адаптера BizTalk включается в службе hello? Как получить hello программного обеспечения?
Да, hello службы адаптера BizTalk с hello пакет адаптера BizTalk входят в состав пакета SDK служб BizTalk Azure hello [загрузить](http://www.microsoft.com/download/details.aspx?id=39087).

## <a name="next-steps"></a>Дальнейшие действия
toocreate служб Azure BizTalk в слишком hello Azure перейдите в меню[службы BizTalk: Подготовка с помощью портала Azure "hello"](biztalk-provision-services.md). Создание приложений, перейдите в слишком toostart[служб Azure BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Службы BizTalk: Подготовка с помощью портала Azure hello](biztalk-provision-services.md)<br/>
* [Службы BizTalk. Диаграмма состояния подготовки](biztalk-service-state-chart.md)<br/>
* [Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Backup and restore](biztalk-backup-restore.md)<br/>
* [Службы BizTalk: регулирование](biztalk-throttling-thresholds.md)<br/>
* [Службы BizTalk: имя и ключ издателя](biztalk-issuer-name-issuer-key.md)<br/>
* [Как я запустить с помощью hello пакета SDK служб BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

