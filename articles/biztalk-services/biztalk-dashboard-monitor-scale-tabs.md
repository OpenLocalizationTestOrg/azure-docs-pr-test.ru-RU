---
title: "aaaDashboard монитор, масштабирование, Настройка и гибридные подключения в службах BizTalk | Документы Microsoft"
description: "Дополнительные сведения об элементах управления hello и наблюдения за производительностью hello классического портала вкладок для службы BizTalk: панель мониторинга, монитор, масштабирование, Настройка и гибридных подключений. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Просмотрите hello вкладки панели мониторинга, монитор, масштабирование, Настройка и гибридного подключения

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

После создания службы BizTalk и развертывания приложения, можно изменить некоторые параметры службы BizTalk hello и наблюдения за производительностью приложения hello. 

При открытии hello классический портал Azure, вы автоматически оказываетесь на hello **все ЭЛЕМЕНТЫ** tooview вкладку службы BizTalk, выделите службу BizTalk в hello **все ЭЛЕМЕНТЫ** tab или выберите hello **Службы BIZTALK** ; и затем выберите имя службы BizTalk.

Откроется новое окно с hello следующие вкладки. В данном разделе описываются эти вкладки.

## <a name="quickstart-quickstartquickstart"></a>Быстрый запуск (![Быстрый запуск][Quickstart])
В зависимости от hello выпуск службы BizTalk все параметры в списке не могут быть доступны. 

<table border="1">
    <tr>
        <td><strong>Получить средства hello</strong></td>
        <td>Загрузите hello пакета SDK служб BizTalk tooinstall hello шаблоны проектов Visual Studio на компьютере в локальной среде разработки. Эти шаблоны создают hello <strong>службы BizTalk</strong> (мост) и hello <strong>артефактов службы BizTalk</strong> проектах Visual Studio (преобразования), которые являются tooyour развернутой службы BizTalk.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Как я запустить с помощью hello Azure BizTalk Services SDK </a> и <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">hello Установка пакета SDK служб BizTalk Azure</a> списки hello tooget шагов работы.
        </td>
    </tr>
    <tr>
        <td><strong>Создание партнерских соглашений</strong></td>
        <td>Здравствуйте, открывается портал служб Azure BizTalk, размещенной в Azure, где добавлять партнеров и создавать X12 AS2 и соглашения EDIFACT EDI.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Настройка компонентов для сообщений EDI на портале служб BizTalk</a> списки hello tooget шагов работы.
        </td>
    </tr>

<tr>
        <td><strong>Дополнительные сведения о службах BizTalk</strong></td>
        <td>Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">центр обучения</a> toolearn Дополнительные сведения о службах BizTalk Azure.</td>
</tr>
</table>


На панели задач hello внизу hello вы можете:

<table border="1">

<tr>
<td><strong>Управление</strong> развертыванием приложений</td>
<td>Откроется портал служб Azure BizTalk hello. Конфигурация tooEDI входа hello, включая добавление партнеров и создания X12 AS2, является Hello портале служб BizTalk и соглашения EDIFACT.
<br/><br/>
Это является hello таким же, как <strong>создать партнера соглашения</strong> на hello <strong>быстрый запуск</strong> вкладки.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Настройка компонентов для сообщений EDI на портале служб BizTalk</a> содержатся дополнительные сведения о портале служб BizTalk hello.</td>
</tr>

<tr>
<td><strong>Сведения о соединении</strong> из пространства имен Access Control hello</td>
<td>При выборе сведения о соединении, затем hello пространства имен Access Control, поставщика по умолчанию, и ключ по умолчанию отображаются. Вы можете скопировать эти значения.
<br/><br/>
Можно также открыть hello портал управления доступом. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Создание элемента управления доступом пространство имен</a> предоставляет дополнительные сведения о hello портал управления доступом.</td>
</tr>

<tr>
<td><strong>Синхронизировать ключи</strong> в hello учетной записи хранилища</td>
<td>При создании учетной записи хранения автоматически создаются первичный ключ и вторичный ключ. Эти ключи шифрования управления tooyour доступа к учетной записи хранилища. Службы BizTalk автоматически использует hello первичный ключ. <strong>Синхронизировать ключи</strong> включить tooswitch пользователей между hello первичный ключ и вторичный ключ hello без нарушения hello службы BizTalk.
<br/><br/>
Например вы хотите hello службы BizTalk toouse новый первичный ключ для hello учетной записи хранилища. toodo это:
<br/><br/>
<ol>
<li>Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>. Выберите hello вторичный ключ. При этом служба BizTalk hello запускается с помощью hello вторичный ключ.</li>
<li>В hello классический портал Azure выберите учетную запись хранилища и повторно создать первичный ключ hello. Помните, что служба BizTalk использует hello вторичный ключ.</li>
<li>Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>. Теперь щелкните hello первичный ключ. Это является hello new при повторном создании первичного ключа.</li>
<li>В hello классический портал Azure выберите учетную запись хранилища и повторно создать вторичный ключ hello.</li>
</ol>
<br/>
Этот процесс называется «переключение ключей». Назначение Hello — tooenable tooswitch пользователей между hello первичный ключ и вторичный ключ hello без нарушения hello службы BizTalk.</td>
</tr>

<tr>
<td><strong>Удаление</strong> приложения</td>
<td>При выборе удалить службу BizTalk, а все элементы, которые развернуты tooit удаляются.</td>
</tr>
</table>


## <a name="dashboard"></a>Панель мониторинга
В зависимости от hello выпуск службы BizTalk все параметры в списке не могут быть доступны. 

При выборе имя службы BizTalk, отображается вкладка сводки hello. На панели мониторинга можно выполнять следующие действия.

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>Общие сведения об использовании: Показывает hello количество используемых гибридных подключений
Также отображает hello использование данных в ГБ. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>Диаграмма метрик. Отображается фиксированный список метрик производительности
Эти показатели предоставляют значения в реальном времени работоспособности hello hello службы BizTalk. Вы также можете hello **относительный** или **абсолютный** значения и hello временной диапазон **интервал** hello метрик, отображаемых на диаграмме hello. 

Описание этих метрик производительности, go слишком[доступные метрики](#Metrics) в этом разделе.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>Краткий обзор. Перечисление свойств службы BizTalk
<table border="1">

<tr>
<td><strong>Обновление учетных данных базы данных отслеживания</strong></td>
<td>Здравствуйте, изменения имени пользователя и пароль, используемые toolog в hello базы данных отслеживания.</td>
</tr>
<tr>
<td><strong>Обновление SSL-сертификата</strong></td>
<td>Можно обновить hello службы BizTalk toouse другой сертификат SSL. Самозаверяющий SSL-сертификат автоматически создается при вы <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">создать службу BizTalk hello</a>.</td>
</tr>
<tr>
<td><strong>Скачивание сертификата</strong></td>
<td>Вы можете загрузить hello SSL-сертификаты, используемые на локальный компьютер tooa службы BizTalk.</td>
</tr>
<tr>
<td><strong>Состояние</strong></td>
<td>Отображает текущее состояние hello службы BizTalk. См. раздел <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Службы BizTalk: диаграмма состояния службы</a>. </td>
</tr>
<tr>
<td><strong>URL-адрес службы</strong></td>
<td>Hello URL-адрес службы BizTalk. Это же является hello как hello <strong>URL-адрес домена</strong> вводятся при создании службы BizTalk.</td>
</tr>
<tr>
<td><strong>Общедоступный виртуальный IP-адрес (VIP-адрес)</strong></td>
<td>tooyour IP-адреса, назначенного Hello службы BizTalk. Он используется для всех входных конечных точек и hello исходный адрес для исходящего трафика. Этот IP-адрес принадлежит tooyour службы BizTalk, при условии, что она создана. При удалении службы BizTalk hello hello IP-адрес назначается tooanother службы BizTalk.</td>
</tr>
<tr>
<td><strong>Пространство имен ACS</strong></td>
<td>Выполняет проверку подлинности с hello службы BizTalk.</td>
</tr>
<tr>
<td><strong>Выпуск</strong></td>
<td>Список hello введенный выпуска при создании службы BizTalk hello.</td>
</tr>
<tr>
<td><strong>Расположение</strong></td>
<td>Отображает hello географического региона, в которой размещена ваша служба BizTalk.</td>
</tr>
<tr>
<td><strong>Создано</strong></td>
<td>Hello отображает дату и время hello была создана служба BizTalk.</td>
</tr>
<tr>
<td><strong>База данных отслеживания</strong></td>
<td>Имя базы данных SQL Azure Hello, которое хранит hello отслеживания таблиц, используемых службой BizTalk. 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Требования к Explained</a> предоставляет подробные сведения о hello базы данных отслеживания.</td>
</tr>
<tr>
<td><strong>Хранилище для мониторинга и архивации</strong></td>
<td>Hello имя учетной записи хранилища Azure, сохраняет hello, отслеживающую выходные данные службы BizTalk.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Требования к Explained</a> предоставляет подробные сведения о hello учетной записи хранилища.</td>
</tr>
<tr>
<td><strong>Имя подписки</strong></td>
<td>Список hello подписки, в которой размещена ваша служба BizTalk. Hello подписка регулирует доступ toohello классический портал Azure.</td>
</tr>
<tr>
<td><strong>Идентификатор подписки</strong></td>
<td>Идентификатор подписки создается автоматически во время создания подписки. При использовании интерфейсов API REST, может потребоваться tooenter hello, идентификатор подписки.</td>
</tr>
</table>

[Службы BizTalk: Подготовка классический портал Azure с помощью](http://go.microsoft.com/fwlink/p/?LinkID=302280) списки hello toocreate действия службы BizTalk.

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>Управление, сведения о соединении, синхронизация ключей и удаления на панели задач hello:
<table border="1">

<tr>
<td><strong>Управление</strong> развертыванием приложений</td>
<td>Здравствуйте, открывается портал служб Azure BizTalk. Конфигурация tooEDI входа hello, включая добавление партнеров и создания X12 AS2, является Hello портале служб BizTalk и соглашения EDIFACT.
<br/><br/>
Это является hello таким же, как <strong>создать партнера соглашения</strong> на hello <strong>быстрый запуск</strong> вкладки.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Настройка компонентов для сообщений EDI на портале служб BizTalk</a> содержатся дополнительные сведения о портале служб BizTalk hello.</td>
</tr>
<tr>
<td><strong>Сведения о соединении</strong> из пространства имен Access Control hello</td>
<td>Отображает hello пространства имен Access Control, поставщика по умолчанию и ключ по умолчанию значения; которого могут быть скопированы.
<br/><br/>
Можно также открыть hello портал управления доступом. Этот портал управления доступом является hello такой же, как с помощью параметра Active Directory hello hello левой панели навигации.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Управление Your пространство имен ACS</a> содержатся дополнительные сведения о hello портал управления доступом.</td>
</tr>
<tr>
<td><strong>Синхронизировать ключи</strong> в hello учетной записи хранилища</td>
<td>При создании учетной записи хранения автоматически создаются первичный ключ и вторичный ключ. Эти ключи шифрования управления tooyour доступа к учетной записи хранилища. Службы BizTalk автоматически использует hello первичный ключ. <strong>Синхронизировать ключи</strong> включить tooswitch пользователей между hello первичный ключ и вторичный ключ hello без нарушения hello службы BizTalk.
<br/><br/>
Например вы хотите hello службы BizTalk toouse новый первичный ключ для hello учетной записи хранилища. toodo это:
<br/><br/>
<ol>
<li>Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>. Выберите hello вторичный ключ. При этом служба BizTalk hello запускается с помощью hello вторичный ключ.</li>
<li>В hello классический портал Azure выберите учетную запись хранилища и повторно создать первичный ключ hello. Помните, что служба BizTalk использует hello вторичный ключ.</li>
<li>Выберите службу BizTalk, а затем щелкните <strong>Синхронизировать ключи</strong>. Теперь щелкните hello первичный ключ. Это является hello new при повторном создании первичного ключа.</li>
<li>В hello классический портал Azure выберите учетную запись хранилища и повторно создать вторичный ключ hello.</li>
</ol>
<br/>
Этот процесс называется «переключение ключей». Назначение Hello — tooenable tooswitch пользователей между hello первичный ключ и вторичный ключ hello без нарушения hello службы BizTalk.</td>
</tr>

<tr>
<td><strong>Удаление</strong> приложения</td>
<td>Службы BizTalk и tooit все элементы развертывания, удаляются.</td>
</tr>
</table>


## <a name="monitor"></a>Монитор
Не применяется toohello бесплатный выпуск.

При выборе имя службы BizTalk hello монитор вкладка доступна и отображает hello следующие:

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>График метрики: Hello отображает выбранные метрики производительности
Эти показатели предоставляют значения в реальном времени работоспособности hello hello службы BizTalk. Выбор метрик производительности осуществляется пользователем. Одновременно может отображаться до шести метрик производительности. 

Вы также можете hello **относительный** или **абсолютный** значения и hello временной диапазон **интервал** hello метрик, которые отображаются. 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>метрики tooremove или для отображения на диаграмме hello.
1. Выберите hello **монитор** вкладки.
2. Выберите **добавить метрики** на панели задач hello:  
   ![Выберите «Добавить метрику»][AddMetrics]
3. Проверьте метрики производительности hello требуется toodisplay.
4. Выберите hello флажок tooreturn toohello **монитор** вкладки.
5. Выберите hello круг Далее toohello метрики toodisplay значение этого показателя в hello graph.  
   
    Например, hello **ЦП** серым метрика; его выходные данные не отображаются в hello graph:  
   ![Метрика загрузки ЦП неактивна][GrayedMetric]  
   
    Выберите hello серым hello круг tooenable **ЦП** метрики toodisplay выходные данные в диаграмме hello:  
   ![Метрика загрузки ЦП активна][EnabledMetric]
6. Выберите метрику из диаграммы отображения hello и список hello tooremove **удалить метрику** на панели задач hello. tooadd hello метрики задней toohello выберите **добавить метрики** в панели задач hello, проверьте метрики hello и toohello tooreturn флажком выберите hello **монитор** вкладки. Выберите hello серым метрика hello tooenable круга.

## <a name="Metrics"></a>Доступные метрики
доступны следующие счетчики производительности и показатели Hello.

<table border="1">

<tr>
<td><strong>Задержка кругового пути</strong></td>
<td>Отображает hello среднее время в миллисекундах (мс) tooprocess сообщение от приветственное сообщение hello время получения, пока сообщение hello полностью обрабатывается hello службы BizTalk через все мосты. Учитываются только успешно обработанные сообщения.<br/><br/>
Когда происходят следующие события hello, создается отметку времени.
<ul>
<li>Поступления сообщения hello шлюза</li>
<li>Сообщение является перенаправленное toohello назначения</li>
<li>Получение ответа из места назначения</li>
<li>Отправлено ответов toohello назначения подтверждения шлюза</li>
</ul>
<br/>
Эта Метрика показывает результат hello hello следующие вычисления:
<br/><br/>
[Адрес подтверждение отправлено ответов toohello шлюз] - [поступления сообщения hello шлюза]</td>
</tr>
<tr>
<td><strong>Сбои в источнике</strong></td>
<td>Отображает общее количество сообщений, которые не удалось hello, hello службы BizTalk, когда удаление сообщений из конечных точек источника hello.</td>
</tr>
<tr>
<td><strong>Загрузка ЦП</strong></td>
<td>Список hello среднее время процессора для всех экземпляров ролей.</td>
</tr>
<tr>
<td><strong>Задержка обработки</strong></td>
<td>Отображает среднее время hello в миллисекундах (мс) tooprocess сообщение по hello службы BizTalk через все мосты, за исключением hello времени, затраченное на назначения. Учитываются только успешно обработанные сообщения.<br/><br/>
Если каждый hello следующие события происходят, создается отметку времени:

<ul>
<li>Поступления сообщения hello шлюза</li>
<li>Сообщение является перенаправленное toohello назначения</li>
<li>Получение ответа из места назначения</li>
<li>Отправлено ответов toohello назначения подтверждения шлюза</li>
</ul>
<br/>Эта Метрика показывает результат hello hello следующие вычисления:<br/><br/>
[Адрес подтверждение отправлено ответов toohello шлюз] - [шлюза hello поступления сообщения] - [назначения ответ] + [сообщение является назначение перенаправленное toohello]</td>
</tr>
<tr>
<td><strong>Сбои при обработке</strong></td>
<td>Отображает hello общее количество сообщений, сбой во время обработки, hello службы BizTalk через все мосты hello в течение интервала времени.</td>
</tr>
<tr>
<td><strong>Отправленные сообщения</strong></td>
<td>Отображает hello общее количество сообщений, отправленных hello службы BizTalk через все мосты в течение интервала времени. Эта метрика увеличивается, когда сообщение, отправленное из конвейера достигает hello назначение маршрутизации. Данная метрика не указывает, что сообщение успешно обработано.<br/><br/>
В сценарии "запрос-ответ" метрика hello увеличивается, когда назначение маршрутизации hello отправляет конвейера toohello назад подтверждение поступления.</td>
</tr>
<tr>
<td><strong>Полученные сообщения</strong></td>
<td>Отображает hello общее количество сообщений, полученных hello службы BizTalk через все мосты в течение интервала времени. Эта метрика увеличивается при получении нового сообщения hello конвейера.</td>
</tr>
<tr>
<td><strong>Сообщения в обработке</strong></td>
<td>Отображает hello общее количество сообщений, которые в настоящее время обрабатываемые hello службы BizTalk в течение интервала времени.</td>
</tr>
<tr>
<td><strong>Обработанные сообщения</strong></td>
<td>Отображает hello общее количество сообщений, успешно обрабатываемых hello службы BizTalk через все мосты в течение интервала времени. Эта метрика увеличивается, если сообщение получено конвейера hello и успешно перенаправленное toohello назначения.</td>
</tr>
</table>


## <a name="scale"></a>Масштаб
Во вкладке "масштаб" hello можно добавить или вычесть hello число единиц, используемых службой BizTalk. По умолчанию настроен один модуль. Дополнительные единицы можно добавить tooscale службы BizTalk. При увеличении масштаба hello увеличивая пропускную способность. также увеличивается Hello объем ресурсов, включая развернутых мостов, соглашения, связей бизнес-ОБЪЕКТОВ и вычислительной мощности. Например вы увеличиваете hello шкала от 1 too2 модульные единицы. В этом случае можно развернуть число double hello мосты, double hello соглашений, double hello LOB соединения и двойные hello вычислительной мощности.

Некоторые выпуски BizTalk не поддерживают параметр масштаба. В этом случае разрешен только один модуль. toodetermine количество единиц, можно масштабировать выпуска, см. слишком[службы BizTalk: схема с выпусками](biztalk-editions-feature-chart.md).

Увеличение числа hello единиц может повлиять на цены. При увеличении hello единицы выборе **Сохранить** отображает сообщение, информирующее о том, если это повлияет на выставление счетов. Затем необходимо выбрать toocontinue. При увеличении hello число единиц, изменяет Active tooUpdating hello состояние службы BizTalk. В hello обновление состояния службы BizTalk продолжает toorun.

[Службы BizTalk: диаграмма выпусков](biztalk-editions-feature-chart.md) определяет «единицу измерения».

## <a name="configure"></a>Настройка
Не применяется tooHybrid подключений.

Задает состояние архивации tooNone hello или автоматически. Если значение tooNone, резервные копии не создаются автоматически. Если значение tooAutomatic, настройте расположение резервной копии hello, частота hello hello резервного копирования, и как долго tookeep hello резервного копирования файлов. 

[Службы BizTalk: Резервное копирование и восстановление](biztalk-backup-restore.md) подробно описаны hello. 

## <a name="HybridConnections"></a>Гибридные подключения
Гибридные подключения подключают приложения Azure, такие как веб-приложения и мобильные приложения в службе приложений Azure, tooan локального ресурса, который использует статический TCP-порт, например SQL Server, MySQL, HTTP веб-API и наиболее пользовательских веб-служб. Гибридные подключения осуществляется в службах BizTalk в hello классический портал Azure.

в разделе toocreate гибридных подключений в службе приложений Azure, [доступа к локальным ресурсам с помощью гибридных подключений в службе приложений Azure](../app-service-web/web-sites-hybrid-connection-get-started.md).

toocreate или управлять гибридных подключений в службах BizTalk Azure см. в разделе [гибридные подключения](integration-hybrid-connection-overview.md).

## <a name="next"></a>Далее
Теперь, когда вы знакомы с разных вкладках hello, можно узнать больше о возможностях службы Azure BizTalk hello:

* [Службы BizTalk: регулирование](biztalk-throttling-thresholds.md)  
* [Службы BizTalk: имя и ключ издателя](biztalk-issuer-name-issuer-key.md)  
* [Службы BizTalk: резервное копирование и восстановление](biztalk-backup-restore.md)

## <a name="see-also"></a>См. также
* [Гибридные подключения](integration-hybrid-connection-overview.md)  
* [Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium](biztalk-editions-feature-chart.md)  
* [Создание служб BizTalk с помощью портала Azure](biztalk-provision-services.md)  
* [Службы BizTalk: диаграмма состояния службы BizTalk](biztalk-service-state-chart.md)  
* [Как я запустить с помощью hello пакета SDK служб BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

