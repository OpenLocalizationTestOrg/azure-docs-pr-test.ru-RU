---
title: "tooBizTalk решений EDI BizTalk Server aaaMigrating техническое руководство по службами | Документы Microsoft"
description: "Перенос EDI tooMABS; Службы BizTalk Microsoft Azure"
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>Перенос решений EDI BizTalk Server tooBizTalk служб: техническое руководство

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Авторы: Тим Виман (Tim Wieman) и Нитин Мехротра (Nitin Mehrotra)

Рецензенты: Катрик Брахти (Karthik Bharthy)

Написано с использованием служб BizTalk Microsoft Azure, выпуск от февраля 2014 г.

## <a name="introduction"></a>Введение
Электронный обмен данными (EDI) является одним из наиболее распространенных средств hello, по которому предприятий обмена данными в электронном виде, также называют бизнес- или B2B-транзакции. BizTalk Server имела поддерживает EDI более десятилетия, со hello первоначального выпуска BizTalk Server. С помощью служб BizTalk Корпорация Майкрософт продолжает поддерживать решения EDI hello на платформе Microsoft Azure hello. B2B-транзакции являются главным образом внешних tooan организации и таким образом, является tooimplement проще, если она была реализована на облачной платформе. Microsoft Azure предоставляет такую возможность посредством служб BizTalk.

Хотя некоторые клиенты смотрят на службы BizTalk как «Гринфилд» платформу для новых решений EDI, многие клиенты располагают решениями EDI в BizTalk Server им хотелось toomigrate tooAzure. Поскольку EDI служб BizTalk — архитектурой на основе hello ключ сущности как архитектура EDI в BizTalk Server (Торговые партнеры, сущности, соглашения), это tooBizTalk артефактов EDI в BizTalk Server возможных toomigrate служб.

В этом документе рассматриваются некоторые отличия hello, связанные с перенос tooBizTalk артефактов EDI в BizTalk Server служб. Этот документ предполагает наличие у читателя практического опыта обработки EDI для BizTalk Server и соглашений между торговыми партнерами. Дополнительные сведения о EDI для BizTalk Server см. в статье [Управление торговыми партнерами с помощью BizTalk Server](https://msdn.microsoft.com/library/bb259970.aspx).

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>Какая версия артефактов EDI в BizTalk Server можно перенести tooBizTalk служб?
модуль BizTalk Server EDI Hello был значительно усовершенствован для BizTalk Server 2010, когда он был переработанное tooinclude партнеры, профили и соглашения. Использует службы BizTalk hello же hello tooorganize модели, торговых партнеров и hello бизнес-подразделений торговых партнеров. В результате миграции EDI служб артефакты из BizTalk Server 2010 и более поздних версиях tooBizTalk, является намного более простым процессом. toomigrate артефакты EDI, связанные с tooBizTalk предыдущие версии Server 2010, необходимо сначала обновить tooBizTalk Server 2010 и затем перенести артефакты EDI tooBizTalk служб.

## <a name="scenariosmessage-flow"></a>Сценарии и поток сообщений
Как и в BizTalk Server, обработка EDI в службах BizTalk построена вокруг решения управления торговыми партнерами (TPM). Hello TPM-решение имеет следующие основные компоненты hello.

* Торговые партнеры, которые представляют организацию в B2B-транзакции.
* Профили, которые представляют подразделения торгового партнера.
* Торговых партнеров соглашений (или соглашения), которые представляют Привет бизнес-соглашения между двумя партнерами или профилями.

Hello следующие иллюстрации показаны сходства hello, а также различия между решением BizTalk Server EDI и решения EDI служб BizTalk:

![][EDImessageflow]

Здравствуйте, основные различия и сходства между работой решения EDI в BizTalk Server и службы BizTalk:

* Так же, как BizTalk Server использует конвейер EDIReceive tooreceive сообщений EDI и toosend конвейер EDISend сообщение EDI, службы BizTalk использует tooreceive моста получения EDI и отправки EDI bridge toosend сообщений EDI. В BizTalk Server конвейеры hello связаны с соглашением с помощью отправки или получения порты. В службах BizTalk само соглашение hello обозначает отправки hello или моста получения.
* В BizTalk Server после процессы конвейер EDIReceive hello hello сообщение EDI, сообщение hello является которого был создан дамп tooa базы данных SQL Server. Hello конвейер EdiSend затем извлекает сообщение hello из базы данных SQL Server hello, обрабатывает его и отправляет его toohello торгового партнера.
  
    В службах BizTalk после hello EDI сообщение моста процессы hello EDI, он направляет сообщение hello: tooan внешний процесс. Hello внешний процесс может быть запущен Microsoft Azure или локально. Hello внешний процесс должен отправить toohello сообщение hello отправки EDI bridge; мост отправки Hello по своей природе не запрашивает приветственное сообщение. После обработки сообщения hello hello мост отправки EDI направляет сообщение hello: toohello торгового партнера.

Службы BizTalk предоставляет tooquickly конфигурации для использования возможности создания и развертывания B2B-соглашений между торговыми партнерами без настройки все вычисления Microsoft Azure экземпляров (рабочих и веб-роли), все базы данных SQL Microsoft Azure или любые Учетные записи хранения Microsoft Azure. Более сложные сценарии требуют привязок в рабочих процессах или другой службы вне пределов «вокруг hello грани» соглашения между торговыми партнерами, т. е., до или после обработки мостами EDI соглашений служб торговых партнеров. В сведениях о, hello следующие последовательности событий возникают во время обработки в службах BizTalk сообщений EDI.

1. Сообщение EDI получено от торгового партнера Fabrikam.  Для получения сообщений EDI от торговых партнеров службы BizTalk поддерживают такие транспортные протоколы, как FTP, SFTP, AS2 и HTTP/S.
2. Hello торговых партнеров соглашение на стороне приема обработки дизассемблирует сообщение EDI hello в формате tooXML.  Можно направить hello дизассемблируется сообщения (в формате XML) EDI tooService конечные точки шины как конечную точку ретрансляции шины обслуживания, шины обслуживания, очередь шины обслуживания или мостов служб BizTalk.
3. Hello дизассемблированные XML-сообщения затем могут быть получены из hello конечной точки для дальнейшей пользовательской обработки.  Эти конечные точки могут обрабатываться компонент локальной или вычисления Microsoft Azure экземпляр toofurther процесса сообщение hello в службе Windows Workflow (WF) или службы Windows Communication Foundation (WCF), например.
4. Hello «обработка стороне отправителя» соглашения между торговыми партнерами hello затем компонует hello XML-сообщения в формате EDI и отправляет его tootrading партнеру Contoso.  Для отправки сообщений EDI tootrading партнеров, BizTalk Services поддерживает hello же протоколы, которые используются для получения сообщений EDI.

Далее в этом документе содержатся подробные указания по переносу некоторых hello различных EDI в BizTalk Server артефакты tooBizTalk служб.

## <a name="sendreceive-ports-tootrading-partners"></a>Порты отправки и получения tooTrading партнеров
В BizTalk Server можно настроить расположения получения и порты получения сообщений EDI/XML tooreceive от торговых партнеров и настроить порты отправки toosend EDI/XML сообщения tootrading партнера. Затем нужно связать эти порты tooa, соглашение торговых партнеров с помощью консоли администрирования BizTalk Server hello. В службах BizTalk hello расположения, где происходит получение сообщений от торговых партнеров и где отправкой сообщений tootrading партнеры настраиваются как часть hello соглашение торговых партнеров себя (как часть параметров транспорта) в hello портале служб BizTalk .  Поэтому у вас действительно hello концепция «портов отправки» и «расположений получения», сам по себе, в службах BizTalk. Дополнительные сведения см. в статье [Создание соглашений](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx).

## <a name="pipelines-bridges"></a>Конвейеры (мосты)
В BizTalk Server EDI конвейеры являются сущности для обработки сообщений, которые могут также включать настраиваемую логику для особые вычислительные возможности, как того требует приложение hello. Для служб BizTalk hello эквивалентные будет мост EDI. Однако в службах BizTalk, пока мосты EDI hello «закрыто».  То есть невозможно добавить мост EDI tooan собственные пользовательские действия. Любая Настраиваемая обработка должна выполняться за пределами мост EDI hello в вашем приложении до или после поступления сообщения hello hello мост, настроенный как часть hello соглашения между торговыми партнерами. Мосты EAI имеют hello параметр toodo пользовательской обработки. При необходимости настраиваемой обработки можно использовать мосты EAI до или после обработки сообщения hello мостом EDI hello. Дополнительные сведения см. в разделе [как tooInclude пользовательского кода в мостах](https://msdn.microsoft.com/library/azure/dn232389.aspx).

Можно вставить поток публикаций или подписок с пользовательским кодом или с помощью обмена сообщениями очереди и разделы перед hello соглашение торговых партнеров получает сообщение hello или после hello соглашение обрабатывает сообщение hello и направляет его в конечную точку Service Bus tooa Service Bus.

В разделе **сценарии и поток сообщений** в этом разделе приводятся шаблон потока сообщений hello.

## <a name="agreements"></a>Соглашения
Если вы знакомы с соглашениями между торговыми партнерами BizTalk Server 2010, используются для обработки EDI hello, затем служб BizTalk соглашения между торговыми партнерами очень знакомыми. Большинство параметров являются hello же соглашение hello и используйте hello же терминологию. В некоторых случаях параметры соглашения Здравствуйте, являются гораздо проще по сравнению toohello же параметрами в BizTalk Server. Службы BizTalk Microsoft Azure поддерживают транспортные протоколы X12, EDIFACT и AS2.

Службы BizTalk Microsoft Azure также предоставляют **переноса данных TPM** инструментов toomigrate торговых партнеров и соглашений из модуля торговых партнеров BizTalk Server tooBizTalk портала служб. Средство переноса данных TPM Hello доступно как часть пакета средств, который можно загрузить из hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057). пакет Hello также включает файл readme, описано, как средство hello средство toouse hello и основные сведения об устранении неполадок.

## <a name="schemas"></a>Схемы
Службы BizTalk предоставляют схемы EDI, которые можно использовать в решениях служб BizTalk.  Кроме того схемы BizTalk Server EDI также используется со службами BizTalk, так как корневой узел схемы EDI hello hello же через BizTalk Server, а также службы BizTalk. Таким образом можно будет toodirectly может взять схем EDI в BizTalk Server и использовать их в решениях EDI hello, разрабатываемых с помощью служб BizTalk. Можно также загрузить hello схемы hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057).

## <a name="maps-transforms"></a>Сопоставления (преобразования)
Сопоставления в BizTalk Server называются преобразованиями в службах BizTalk. Миграция сопоставлений из BizTalk Server tooBizTalk службы может быть одним из hello более сложные задачи tooachieve (в зависимости от сложности сопоставления). средство сопоставления Hello, используемое для служб BizTalk отличается от модуля сопоставления BizTalk hello. Несмотря на то, что сопоставления hello выглядит практически Здравствуйте таким же, базовый формат сопоставления hello отличается. Здравствуйте, функтоиды (называется **операции сопоставления** в службах BizTalk) toohello доступны пользователям, также будут отличаться.  По сути, напрямую сопоставление BizTalk в службах BizTalk использовать нельзя. Кроме того не все функтоиды hello, доступные в BizTalk Server доступны как операции сопоставления в службах BizTalk.

### <a name="new-transform-operations"></a>Новые операции преобразования
Хотя hello список доступных операций сопоставления преобразований может показаться значительно отличается от hello сопоставления BizTalk Server, BizTalk Services преобразуют имеют новые способы выполнения одной задачи hello. Например, в преобразованиях служб BizTalk доступен **Список операций**. Этого не было в модуле сопоставления BizTalk hello.  Hello **список операций** позволяют toocreate и работают с «Список», где список представляет собой набор элементов (также называется «строки») и, где каждый элемент может иметь несколько членов (также называется «столбцы»).  Можно сортировать список hello, выберите элементов на основании условий и т. д.

Другой пример новой функциональности в BizTalk Services преобразуют являются hello **операции цикла**.  Бывает сложно toocreate вложенных циклов в hello сопоставления BizTalk Server.  Таким образом операции сопоставления цикла hello добавляются для BizTalk Services преобразуют hello.

Еще один пример — hello **If-Then-Else** операция сопоставления.  If-then-else операции было возможно в модуле сопоставления BizTalk hello, но ему требуется несколько функтоидов tooaccomplish внешне простой задачи.

### <a name="migrating-biztalk-server-maps"></a>Миграция сопоставлений BizTalk Server
Службы BizTalk Microsoft Azure предоставляет средство toomigrate BizTalk Server сопоставляет tooBizTalk службы преобразования. Hello **BTMMigrationTool** доступен как часть hello **средства** пакет, в состав hello [загрузки пакета SDK служб BizTalk](http://go.microsoft.com/fwlink/p/?LinkId=235057). Дополнительные сведения об инструменте hello см. в разделе [преобразовать tooa карты BizTalk, преобразование служб BizTalk](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx).

Вы также можете изучить пример Сандро перейра, BizTalk MVP, на слишком как[перенести преобразований служб tooBizTalk карты BizTalk Server](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx).

## <a name="orchestrations"></a>Взаимодействия
При необходимости toomigrate tooMicrosoft обработки orchestration BizTalk Server Azure hello взаимодействий, должны toobe переписать так, как Microsoft Azure не поддерживает выполнение взаимодействий BizTalk Server.  Можно переписать функциональность взаимодействия hello в службе Windows Workflow Foundation 4.0 (WF4).  Поскольку существует в настоящее время не переноса из tooWF4 взаимодействий BizTalk Server, будет полностью переписан. Ниже приведены некоторые ресурсы для Windows Workflow.

* [*Как toointegrate WCF службы Workflow Service с очереди Service Bus и разделами* ](https://msdn.microsoft.com/library/azure/hh709041.aspx) Паоло сальватори. 
* [*Построение приложений с помощью Windows Workflow Foundation и Azure* сеанса](http://go.microsoft.com/fwlink/p/?LinkId=237314) с конференции Build 2011 hello.
* [*Центр разработчиков Windows Workflow Foundation*](http://go.microsoft.com/fwlink/p/?LinkId=237315) в MSDN.
* [*Документация по Windows Workflow Foundation 4 (WF4)*](https://msdn.microsoft.com/library/dd489441.aspx) в MSDN.

## <a name="other-considerations"></a>Дополнительные рекомендации
Ниже приведены некоторые рекомендации, которые необходимо учитывать при использовании служб BizTalk.

### <a name="fallback-agreements"></a>Резервные соглашения
Обработка BizTalk Server EDI использует концепцию «Резервных соглашений» hello.  В службах BizTalk понятия резервных соглашений пока **нет**.  В следующих разделах документации BizTalk [hello роль соглашений в обработке EDI](http://go.microsoft.com/fwlink/p/?LinkId=237317) и [Настройка глобальных или Fallback свойства соглашения о](https://msdn.microsoft.com/library/bb245981.aspx) сведения о том, как стандартные соглашения используются в BizTalk Сервер.

### <a name="routing-toomultiple-destinations"></a>Направления маршрутизации toomultiple
Мостов службы BizTalk в ее текущем состоянии не поддерживает toomultiple направления маршрутизации сообщений, с помощью публикации-подписки модели. Вместо этого вы можете направлять сообщения от службы BizTalk bridge tooa раздела Service Bus, который может иметь несколько подписок tooreceive приветственное сообщение более одной конечной точке.

## <a name="conclusion"></a>Заключение
Microsoft Azure BizTalk Services обновляется в tooadd регулярного вехи функциями и возможностями. С каждым обновлением мы рассчитываем toofacilitate функциональные возможности увеличить toosupporting решений начала до конца, с использованием служб BizTalk и другие технологии Azure.

## <a name="see-also"></a>См. также
[Разработка корпоративных приложений с Azure](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
