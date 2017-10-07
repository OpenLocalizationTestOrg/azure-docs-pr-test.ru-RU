---
title: "Вычислений aaaAzure - диагностического расширения для Linux | Документы Microsoft"
description: "Как tooconfigure hello toocollect метрики диагностики расширение Azure Linux (LAD) и вести журнал из виртуальных машин Linux, работающих в Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Использовать журналы и показатели toomonitor диагностического расширения для Linux

В этом документе описывается версии 3.0 и более поздних из hello диагностического расширения для Linux.

> [!IMPORTANT]
> Сведения о версии 2.3 и более ранних см. в [этом документе](./classic/diagnostic-extension-v2.md).

## <a name="introduction"></a>Введение

Hello диагностического расширения для Linux помогает пользователю монитор hello работоспособности виртуальной машины Linux в Microsoft Azure. Он имеет hello следующие возможности:

* Сбор метрик производительности системы hello виртуальной Машины и сохраняет их в конкретную таблицу в учетной записи указанного хранилища.
* Получает журнал событий из системного журнала и сохраняет их в конкретную таблицу в hello, назначенные учетной записи хранилища.
* Позволяет пользователям toocustomize hello данных метрик, которые собраны и отправлены.
* Позволяет средств syslog hello toocustomize пользователей и степени серьезности событий, которые собраны и отправлены.
* Позволяет пользователям tooupload указанного журнала файлов tooa указанного хранилища таблицы.
* Поддержка отправки метрики журнала событий tooarbitrary EventHub конечных точек и и большие двоичные объекты в формате JSON в hello назначить учетной записи хранилища.

Это расширение работает с обеими моделями развертывания Azure.

## <a name="installing-hello-extension-in-your-vm"></a>Установка расширения hello в виртуальной Машине

Это расширение можно включить с помощью командлетов Azure PowerShell hello, скрипты Azure CLI или шаблоны развертывания Azure. Дополнительные сведения см. в статье [Обзор расширений](./extensions-features.md).

Hello портал Azure нельзя использовать tooenable или настроить LAD 3.0. С его помощью устанавливается и настраивается версия 2.3. Оповещения Azure портала диаграмм и работать с данными из обеих версий расширения hello.

С помощью этих инструкций по установке и [доступного для скачивания образца конфигурации](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) можно настроить LAD 3.0 для выполнения следующих задач:

* Создайте и сохраните hello одинаковых метрик как предоставил LAD 2.3;
* записи полезных метрик системы файл, новый tooLAD 3.0;
* записать включаемые LAD 2.3; сбора syslog по умолчанию hello
* Включите hello взаимодействие с портала Azure для построения графиков и оповещениями на метрики виртуальной Машины.

Конфигурация, загружаемая Hello всего лишь пример; изменить его toosuit потребностями.

### <a name="prerequisites"></a>Предварительные требования

* **Агент Linux для Azure 2.2.0 или более поздней версии**. Большинство образов в коллекции виртуальных машин Azure на базе Linux включает версию 2.2.7 или более позднюю. Запустите `/usr/sbin/waagent -version` tooconfirm hello версию, установленную на hello виртуальной Машины. Если hello виртуальная машина работает под управлением более старой версии hello гостевого агента, выполните [эти инструкции](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate его.
* **Azure CLI**. [Настройка hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) среды на компьютере.
* Здравствуйте wget команду, если вы его еще нет: запустите `sudo apt-get install wget`.
* Существующая подписка Azure и существующее хранилище учетной записи в него данных toostore hello.

### <a name="sample-installation"></a>Пример установки

Заполните hello правильные параметры на hello первые три строки, а затем выполнить этот скрипт как корневой элемент:

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

URL-адрес Hello hello пример конфигурации и его содержимое, toochange субъекта. Загрузите копию параметров портала hello JSON-файл и настроить его для потребностей. Все создаваемые вами шаблоны или средства автоматизации должны использовать вашу собственную копию, а не скачивать каждый раз файл по этому URL-адресу.

### <a name="updating-hello-extension-settings"></a>Обновление параметров расширения hello

После изменения Protected или открытых параметров, разверните их toohello виртуальной Машины, выполнив hello в одной команде. Если что-либо изменен в параметрах hello, hello обновлены параметры отправляются toohello расширения. LAD перезагружает конфигурации hello и перезапускает сам.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Миграция с предыдущих версий расширения hello

Последняя версия расширения hello Hello — **3.0**. **Все предыдущие версии (2.x) не рекомендуются к использованию, и их публикация может быть отменена 31 июля 2018 г. или позднее**.

> [!IMPORTANT]
> Этот модуль предоставляет критические изменения toohello конфигурации расширения hello. Один такой изменения безопасности hello tooimprove hello расширения; в результате обратной совместимости с 2.x может не поддерживаться. Кроме того hello издателя расширения для этого расширения отличается от издателя hello для версий 2.x hello.
>
> toomigrate из новой версии 2.x toothis hello расширения необходимо удалить старым расширением hello (под hello старое имя издателя), а затем установить версию 3 hello расширения.

Рекомендации

* Установите расширение hello включено обновление автоматического дополнительный номер версии.
  * В классической модели развертывания виртуальных машин укажите «3.*» hello версии при установке расширения hello с помощью Azure XPLAT-CLI или Powershell.
  * На развертывания диспетчера ресурсов Azure модель виртуальных машин, включают "«autoUpgradeMinorVersion»: true" в шаблон развертывания виртуальной Машины hello.
* Используйте новую или другую учетную запись хранения для LAD 3.0. Между LAD 2.3 и LAD 3.0 есть несколько небольших несовместимостей, которые затрудняют использование одной и той же учетной записи.
  * LAD 3.0 сохраняет события системного журнала в таблице с другим именем.
  * Hello counterSpecifier строки для `builtin` метрики различаются LAD 3.0.

## <a name="protected-settings"></a>Защищенные параметры

Этот набор данных конфигурации включает в себя конфиденциальные сведения, которые не должны быть общедоступными, например учетные данные для доступа к хранилищу. Эти параметры используются передаваемых tooand хранятся по расширению hello в зашифрованном виде.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

Имя | Значение
---- | -----
storageAccountName | Имя учетной записи хранения hello, в котором данные записываются с помощью расширения hello Hello.
storageAccountEndPoint | Идентификация hello облака, в которой hello учетная запись хранения существует конечная точка hello (необязательно). Если этот параметр отсутствует, LAD по умолчанию toohello общедоступное облако Azure, `https://core.windows.net`. toouse учетной записи хранения в Германии Azure, Azure для государственных или Azure China это значение соответствующим образом.
storageAccountSasToken | [Маркер SAS для учетной записи](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) для службы BLOB-объектов и таблиц (`ss='bt'`), соответствующий toocontainers и объекты (`srt='co'`), добавить какие-либо права, создать, список, обновления и разрешения на запись (`sp='acluw'`). Сделать *не* включают hello первый вопросительный знак (?).
mdsdHttpProxy | (необязательно) Прокси-сервер HTTP сведения, необходимые hello tooenable расширения toohello tooconnect указан учетной записи хранилища и конечной точки.
sinksConfig | (необязательно) Сведения об альтернативных назначения toowhich метрики и события может быть доставлено. Hello подробные сведения для каждого поддерживаемого расширением hello приемник данных описаны в последующих разделах hello.

Легко можно создать токен SAS hello необходимые через портал Azure hello.

1. Выберите toowhich учетной записи хранилища общего назначения hello, требуется расширение toowrite hello
1. Выберите «Подписанном URL-адресе» из части левого меню hello параметры hello
1. Сделать hello соответствующих разделов в соответствии с указаниями
1. Нажмите кнопку «Создать SAS» hello.

![изображение](./media/diagnostic-extension/make_sas.png)

Hello копирования созданы SAS в поле storageAccountSasToken hello; Удалите hello начальные вопросительным знаком (»?»).

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

Этот дополнительный раздел определяет дополнительные назначения, отправляемую расширения hello toowhich hello сведения, полученные. Массив «приемник» Hello содержит объект для каждого приемника дополнительные данные. Здравствуйте, определяет атрибут «type» hello других атрибутов в hello объекта.

Элемент | Значение
------- | -----
name | Строка, используемое приемник toothis toorefer в другом месте в конфигурации расширения hello.
type | тип приемника определяемой Hello. Определяет hello другие значения (если таковые имеются) в экземплярах этого типа.

Версии 3.0 hello диагностического расширения для Linux поддерживает два типа приемника: EventHub и JsonBlob.

#### <a name="hello-eventhub-sink"></a>приемник EventHub Hello

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

запись «sasURL» Hello содержит полный URL-адрес, включая маркер SAS, для hello toowhich данных концентратора событий должны публиковаться приветствия. LAD требует именования политики, которая включает утверждение отправки hello SAS. Пример:

* Создание пространства имен концентраторов событий с именем `contosohub`
* Создать концентратор событий в hello пространство имен`syslogmsgs`
* Создать политику общего доступа для концентратора событий с именем hello `writer` hello, позволяет отправлять утверждения

Если вы создали подписанный URL-адрес хорошо до полуночи 1 января 2018, UTC hello sasURL значение может быть:

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Дополнительные сведения о создании токенов SAS для концентраторов событий см. на [этой веб-странице](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).

#### <a name="hello-jsonblob-sink"></a>приемник JsonBlob Hello

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

Данные направлены приемник JsonBlob tooa хранится в BLOB-объектов в хранилище Azure. Каждый экземпляр LAD каждый час создает BLOB-объект для каждого имени приемника. Каждый BLOB-объект всегда содержит синтаксически правильный массив JSON объекта. Массив toohello атомарным образом добавляются новые записи. Большие двоичные объекты хранятся в контейнере с точно такое же имя в качестве приемника hello hello. Здравствуйте правила хранилища Azure имена контейнеров больших двоичных объектов относиться имена toohello JsonBlob приемников: от 3 до 63 строчные буквенно-цифровые символы ASCII или дефисы.

## <a name="public-settings"></a>Общедоступные параметры

Эта структура содержит различные блоки параметры, определяющие hello сведения, собранные с помощью расширения hello. Все параметры являются необязательными. При указании `ladCfg` также необходимо указать `StorageAccount`.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

Элемент | Значение
------- | -----
StorageAccount | Имя учетной записи хранения hello, в котором данные записываются с помощью расширения hello Hello. Должны быть одинаковые имена, как указано в hello hello [защищенные параметры](#protected-settings).
mdsdHttpProxy | (необязательно) Отличается от используемого hello [защищенные параметры](#protected-settings). значение открытого Hello переопределяется значение частного hello, если задать. Поместите параметры прокси-сервера, которые содержат секрета, например пароль в hello [защищенные параметры](#protected-settings).

остальные элементы Hello подробно описываются в следующих разделах hello.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

Приемники метрик и журналов для доставки toohello службы и tooother данные метрик Azure сборе данных hello необязательно структуры элементов управления. Необходимо указать `performanceCounters`, `syslogEvents` или и то, и другое. Необходимо указать hello `metrics` структуры.

Элемент | Значение
------- | -----
eventVolume | (необязательно) Элементы управления hello число секций, создаваемых в таблицу хранилища hello. Должно иметь значение `"Large"`, `"Medium"` или `"Small"`. Если не указан, значение по умолчанию hello — `"Medium"`.
sampleRateInSeconds | Интервал по умолчанию (необязательно) hello между сбор метрик raw (необъединенных). частота выборки наименьшее Hello поддерживается составляет 15 секунд. Если не указан, значение по умолчанию hello — `15`.

#### <a name="metrics"></a>Метрики

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

Элемент | Значение
------- | -----
resourceId | Идентификатор ресурса диспетчера ресурсов Azure Hello hello виртуальной Машины или масштабирования виртуальных машин hello задать toowhich hello, к которому относится виртуальная машина. Этот параметр должен быть также указан, если любой приемник JsonBlob используется в конфигурации hello.
scheduledTransferPeriod | Hello частоту, с которой статистические показатели, toobe вычисляемые столбцы и передаются tooAzure метрик, выраженное как 8601 — интервал времени. Наименьший период передачи Hello составляет 60 секунд, то есть PT1M. Необходимо указать по крайней мере одно значение scheduledTransferPeriod.

Образцы приветствия показатели, указанные в разделе performanceCounters hello собираются каждые 15 секунд или скоростью образец hello, явно определенные для счетчика "hello". Если несколько частот scheduledTransferPeriod отображается (как в примере hello), каждое статистическое выражение вычисляется независимо друг от друга.

#### <a name="performancecounters"></a>performanceCounters

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

Этот дополнительный раздел управляет hello сбор метрик. Образцы необработанные вычисляются для каждого [scheduledTransferPeriod](#metrics) tooproduce следующих значений:

* mean
* minimum
* maximum
* последнее собранное значение;
* Количество необработанных выборок используется статистическая функция toocompute hello

Элемент | Значение
------- | -----
sinks | (необязательно) Список разделенных запятыми имен приемников toowhich LAD отправляет агрегированных результатов метрики. Все статистические показатели являются приемник опубликованных tooeach в списке. См. [sinksConfig](#sinksconfig). Пример: `"EHsink1, myjsonsink"`.
type | Определяет поставщика фактическое hello hello метрики.
class | Вместе с «счетчик» определяет конкретную метрику hello в пространство имен поставщика hello.
Счетчик | Вместе с «класс» определяет конкретную метрику hello в пространство имен поставщика hello.
counterSpecifier | Определяет конкретную метрику hello в пределах пространства имен метрики Azure hello.
condition | (необязательно) Выбирает экземпляр hello объекта toowhich hello метрики применяет или выбирает hello статистической обработки для всех экземпляров этого объекта. Дополнительные сведения см. в разделе hello [ `builtin` определения показателей](#metrics-supported-by-builtin).
sampleRate | — 8601 интервала, который задает скорость hello собранные необработанные образцов для этой метрики. Если не задан, интервал сбора hello задается значение hello [sampleRateInSeconds](#ladcfg). Hello кратчайший поддерживаемых дискретизации составляет 15 секунд (PT15S).
unit | Значением должна быть одна из следующих строк: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond". Определяет единицу hello hello метрики. Потребители данных, собранных hello ожидается, что hello собранные данные значения toomatch это устройство. LAD игнорирует это поле.
displayName | toobe метки (в hello язык, заданный параметром hello параметр соответствующий языковой стандарт) Hello присоединенного toothis данных в Azure метрики. LAD игнорирует это поле.

Hello counterSpecifier представляет произвольный идентификатор. Потребители показателей, как hello Azure портала построения графиков и компонента, предупреждения об изменении counterSpecifier служит hello «ключ», который определяет метрики или экземпляра метрики. Для метрик `builtin` рекомендуется использовать значения counterSpecifier, начинающиеся с `/builtin/`. При сборе экземпляр метрики, рекомендуется присоединить идентификатор hello значения counterSpecifier toohello экземпляра hello. Некоторые примеры

* `/builtin/Processor/PercentIdleTime` — среднее время простоя всех ядер;
* `/builtin/Disk/FreeSpace(/mnt)`-Свободного пространства для файловой системы/mnt hello
* `/builtin/Disk/FreeSpace` — средний объем свободного пространства для всех подключенных файловых систем.

LAD ни hello портал Azure предполагает, что значение toomatch hello counterSpecifier любой шаблон. При формировании значений counterSpecifier соблюдайте единообразие.

При указании `performanceCounters`, LAD всегда записывает tooa таблицы данных в хранилище Azure. Вы может иметь hello же данные, записанные tooJSON больших двоичных объектов и/или концентраторов событий, но не удается отключить таблицу tooa хранение данных. Все экземпляры toouse диагностического расширения, настроенного hello hello учетную запись хранения имени и конечной точки добавьте свои журналы и показатели toohello одной таблицы. Если записи слишком много виртуальных машин toohello, которые могут привести к перегрузке секции таблицы, Azure записывает toothat секции. параметр toobe записи причины eventVolume Hello распределены 1 (маленький), 10 (средний) или 100 (крупный) различных секций. Как правило, «Средний» достаточно tooensure трафик не регулируется. компонент Azure метрики Hello hello портал Azure использует hello данные в этой таблице tooproduce диаграмм или tootrigger предупреждения. Имя таблицы Hello-hello объединение этих строк:

* `WADMetrics`
* Hello «scheduledTransferPeriod» для hello статистическая обработка значений, хранящихся в таблице hello
* `P10DV2S`
* Даты в форме hello «ГГГГММДД», изменяется в течение 10 дней

Примеры: `WADMetricsPT1HP10DV2S20170410` и `WADMetricsPT1MP10DV2S20170609`.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

Этот дополнительный раздел управляет hello коллекции журналов событий из системного журнала. Если раздел hello опущен, события syslog вообще не сохраняются.

Коллекция syslogEventConfiguration Hello содержит одну запись для каждого средства syslog, представляющие интерес. Если minSeverity является «Нет» для определенной территории или этого средства не отображаются в элементе hello, события из этого устройства не регистрируются.

Элемент | Значение
------- | -----
sinks | Список разделенных запятыми имен приемников toowhich отдельный журнал событий публикуются. Всех журналов событий, соответствующих ограничений hello в syslogEventConfiguration являются приемник опубликованных tooeach в списке. Пример: "EHforsyslog"
facilityName | Имя субъекта системного журнала (например, "LOG\_USER" или "LOG\_LOCAL0"). Обратитесь к разделу «средства» hello hello [syslog справочную страницу](http://man7.org/linux/man-pages/man3/syslog.3.html) для полного списка hello.
minSeverity | Уровень серьезности системного журнала (например, "LOG\_ERR" или "LOG\_INFO"). Обратитесь к разделу «уровень» hello hello [syslog справочную страницу](http://man7.org/linux/man-pages/man3/syslog.3.html) для полного списка hello. расширение Hello захватывает toohello события, отправляемые на первом или выше hello указанный уровень.

При указании `syslogEvents`, LAD всегда записывает tooa таблицы данных в хранилище Azure. Вы может иметь hello же данные, записанные tooJSON больших двоичных объектов и/или концентраторов событий, но не удается отключить таблицу tooa хранение данных. Здравствуйте Hello секционирование поведение для этой таблицы, так же, как описано для `performanceCounters`. Имя таблицы Hello-hello объединение этих строк:

* `LinuxSyslog`
* Даты в форме hello «ГГГГММДД», изменяется в течение 10 дней

Примеры: `LinuxSyslog20170410` и `LinuxSyslog20170609`.

### <a name="perfcfg"></a>perfCfg

Этот необязательный раздел управляет выполнением произвольных запросов [OMI](https://github.com/Microsoft/omi).

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

Элемент | Значение
------- | -----
пространство_имен | (необязательно) hello OMI пространство имен, в какие hello должен выполняться запрос. Если не указан, значение по умолчанию hello — «корневой/scx», реализуемый hello [поставщики кросс платформенных System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).
query | выполнен запрос toobe OMI Hello.
таблица | (необязательно) hello хранилища Azure таблицы в hello, назначенные учетной записи хранения (в разделе [защищенные параметры](#protected-settings)).
frequency | количество секунд между выполнением запроса hello hello (необязательно). Значение по умолчанию — 300 (5 минут); минимальное значение — 15 секунд.
sinks | (необязательно) Список разделенных запятыми имен результатов метрики необработанные образец toowhich дополнительных приемники необходимо опубликовать. Ни один агрегат в этих примерах необработанные вычисляемым модулем hello Azure метрик.

Необходимо указать либо table, либо sinks, либо оба эти элемента.

### <a name="filelogs"></a>fileLogs

Элементы управления hello записи файлов журнала. LAD захватывает новые строки текста, как они записываются в файл toohello и записывает их tootable строк и/или любой указанной приемники (JsonBlob или EventHub).

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

Элемент | Значение
------- | -----
file | Hello полным путем к toobe файла журнала hello наблюдали и записи. Hello путь должен указывать имя одного файла, он не имя каталога или содержать подстановочные знаки.
таблица | (необязательно) hello хранилища Azure таблицы в назначенный hello хранилища учетной записи (как указано в конфигурации hello защищенный), в какие новые строки hello «с префиксом tail «hello файла записи.
sinks | (необязательно) Список разделенных запятыми имен строк журнала toowhich дополнительных приемники отправлено.

Необходимо указать либо table, либо sinks, либо оба эти элемента.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Метрики, поддерживаемых поставщиком builtin hello

Hello builtin метрики поставщик является источником метрики наиболее интересные tooa широкого набора пользователей. Эти метрики делятся на пять основных классов:

* Процессор
* Память
* Сеть
* Файловая система
* Диск

### <a name="builtin-metrics-for-hello-processor-class"></a>показатели Builtin hello класса процессора

Hello класса процессора метрик сведения о загрузке процессора в hello виртуальной Машины. При статистической обработке проценты, hello результат — hello среднее для всех процессоров. В двух основных виртуальных Машин Если одно ядро был занят 100%, а hello других — 100% простоя, hello сообщила, что PercentIdleTime будет равно 50. Если каждое ядро был занят для 50% hello же период, hello сообщил, что результат также будет равно 50. В четырех основных компонентов виртуальной Машины, занят одно ядро 100% и hello простоя, другие hello сообщила, что PercentIdleTime бы 75.

Счетчик | Значение
------- | -------
PercentIdleTime | Процент времени, во время периода hello статистической обработки, что процессоров выполнялись hello ядра пустых циклов
PercentProcessorTime | Процент времени, который был затрачен на выполнение всех потоков, кроме бездействующего.
PercentIOWaitTime | Процент времени ожидания toocomplete операций ввода-ВЫВОДА
PercentInterruptTime | Процент времени, затраченный на выполнение аппаратных и программных прерываний и отложенных вызовов процедур.
PercentUserTime | Простаивающего время окно агрегата hello hello процент времени, затраченный на пользователя более с обычным приоритетом
PercentNiceTime | Времени hello процент затраченного снижения приоритетом (хорошо)
PercentPrivilegedTime | Времени hello процент затраченного в привилегированном режиме

Hello первые четыре счетчики сумма должна составлять too100%. Hello последние три счетчики также сумма too100%; они разделить сумму hello PercentProcessorTime, PercentIOWaitTime и PercentInterruptTime.

задать один показатель статистически обрабатываются для всех процессоров tooobtain `"condition": "IsAggregate=TRUE"`. tooobtain метрики для конкретного процессора, так как второй логический процессор hello из четырех основных виртуальных Машин, установите `"condition": "Name=\\"1\\""`. Номера логических процессоров находятся в диапазоне hello `[0..n-1]`.

### <a name="builtin-metrics-for-hello-memory-class"></a>показатели Builtin hello класс памяти

Hello класса памяти метрик предоставляет сведения об использовании памяти, разбиение по страницам и замены.

Счетчик | Значение
------- | -------
AvailableMemory | Доступный объем физической памяти в МиБ.
PercentAvailableMemory | Доступный объем физической памяти в процентах от общего объема памяти.
UsedMemory | Используемый объем физической памяти (МиБ).
PercentUsedMemory | Используемый объем физической памяти в процентах от общего объема памяти.
PagesPerSec | Общее количество операций подкачки (чтения и записи).
PagesReadPerSec | Число страниц, считанных из резервного хранилища (файла подкачки, файла программы, сопоставленного файла и т. д.).
PagesWrittenPerSec | Страниц, записанных toobacking хранения (файл подкачки, сопоставленный файл, и т. д.)
AvailableSwap | Размер неиспользуемой области подкачки (МиБ).
PercentAvailableSwap | Размер неиспользуемой области подкачки в процентах от общего размера области подкачки.
UsedSwap | Размер используемой области подкачки (МиБ).
PercentUsedSwap | Размер используемой области подкачки в процентах от общего размера области подкачки.

Этот класс метрик имеет только один экземпляр. атрибут «условие» Hello не имеет полезных параметров и должен быть опущен.

### <a name="builtin-metrics-for-hello-network-class"></a>встроенные метрики для класса сети hello

Hello класса сети метрик сведения о сетевой активности для отдельных сетевых интерфейсов с момента загрузки. LAD не предоставляет метрики пропускной способности, которые можно получить из метрик узла.

Счетчик | Значение
------- | -------
BytesTransmitted | Общее количество байт, отправленное с момента загрузки.
Получено байт | Общее количество байт, полученное с момента загрузки.
BytesTotal | Общее количество байт, отправленное или полученное с момента загрузки.
PacketsTransmitted | Общее количество пакетов, отправленных с момента загрузки.
PacketsReceived | Общее количество пакетов, полученных с момента загрузки.
TotalRxErrors | Количество ошибок приема с момента загрузки.
TotalTxErrors | Количество ошибок передачи с момента загрузки.
TotalCollisions | Число конфликтов, о которых сообщили hello сетевые порты с момента загрузки

 Хотя экземпляры этого класса создаются, LAD не поддерживает сбор совокупных метрик сети по всем сетевым устройствам. задать tooobtain hello метрики для определенного интерфейса, такие как eth0, `"condition": "InstanceID=\\"eth0\\""`.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>показатели Builtin hello класса файловой системы

Класс файловой системы показателей Hello содержит сведения об использовании файловой системы. Абсолютное и процентное значения выводятся как отображаемых tooan обычного пользователя (не root).

Счетчик | Значение
------- | -------
FreeSpace | Доступное дисковое пространство в байтах.
UsedSpace | Используемое дисковое пространство в байтах.
PercentFreeSpace | Процент свободного пространства.
PercentUsedSpace | Процент используемого пространства.
PercentFreeInodes | Процент неиспользуемых inode.
PercentUsedInodes | Процент выделенных (используемых) inode по всем файловым системам.
BytesReadPerSecond | Число прочитанных байт за секунду.
BytesWrittenPerSecond | Число записанных байт за секунду.
Байт/с | Число прочитанных или записанных байт за секунду.
ReadsPerSecond | Число операций чтения за секунду.
WritesPerSecond | Число операций записи за секунду.
TransfersPerSecond | Число операций чтения или записи за секунду.

Совокупные значения по всем файловым системам можно получить, задав `"condition": "IsAggregate=True"`. Значения для определенной подключенной файловой системы, например "/mnt", можно получить, задав `"condition": 'Name="/mnt"'`.

### <a name="builtin-metrics-for-hello-disk-class"></a>показатели Builtin hello класса диск

Hello класса диск метрик предоставляет сведения об использовании диска устройства. Эти статистические данные применяются ко всему диску toohello. В случае нескольких файловых систем на устройстве, hello счетчики для этого устройства являются, по сути, статистически обрабатываются по всем из них.

Счетчик | Значение
------- | -------
ReadsPerSecond | Число операций чтения за секунду.
WritesPerSecond | Число операций записи за секунду.
TransfersPerSecond | Общее число операций за секунду.
AverageReadTime | Среднее число секунд на операцию чтения.
AverageWriteTime | Среднее число секунд на операцию записи.
AverageTransferTime | Среднее число секунд на операцию.
AverageDiskQueueLength | Среднее число операций с диском, помещенных в очередь.
ReadBytesPerSecond | Количество прочитанных байт за секунду.
WriteBytesPerSecond | Количество записанных байт за секунду.
Байт/с | Количество прочитанных или записанных байт за секунду.

Совокупные значения по всем дискам можно получить, задав `"condition": "IsAggregate=True"`. задать сведения о tooget для конкретного устройства (например, / dev/sdf1), `"condition": "Name=\\"/dev/sdf1\\""`.

## <a name="installing-and-configuring-lad-30-via-cli"></a>Установка и настройка LAD 3.0 с помощью интерфейса командной строки

При условии, что защищенный параметры находятся в файле hello PrivateConfig.json открытой конфигурации данные имеют PublicConfig.json, выполните следующую команду:

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

Hello предполагается, что вы используете режим управления ресурсами Azure hello (arm) hello Azure CLI. tooconfigure LAD для классического развертывания модель виртуальных машин (ASM), слишком переключения режима «asm» (`azure config mode asm`) и не указывайте имя группы ресурсов hello в команде hello. Дополнительные сведения см. в разделе hello [документации CLI кросс платформенных](https://docs.microsoft.com/azure/xplat-cli-connect).

## <a name="an-example-lad-30-configuration"></a>Пример конфигурации LAD 3.0

На основании предшествующий определений, здесь в образце конфигурации расширения LAD 3.0 с некоторыми пояснениями hello. tooapply tooyour этот образец варианта, следует использовать имя учетной записи хранилища, учесть маркер SAS и маркеры EventHubs SAS.

### <a name="privateconfigjson"></a>PrivateConfig.json

Эти закрытые параметры настраивают:

* учетную запись хранения;
* соответствующий токен SAS учетной записи;
* несколько приемников (JsonBlob или EventHubs с токенами SAS).

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

Эти общедоступные параметры обеспечивают выполнение расширением LAD следующих действий:

* Отправка toohello метрик процент загруженности процессора и использовать дискового пространства `WADMetrics*` таблицы
* Отправка сообщения системного журнала toohello средство «user» и серьезности «info» `LinuxSyslog*` таблицы
* Передать необработанные OMI запроса результаты (PercentProcessorTime и PercentIdleTime) toohello с именем `LinuxCPU` таблицы
* Отправка строк, добавленных в файле `/var/log/myladtestlog` toohello `MyLadTestLog` таблицы

В каждом случае данные также передаются в следующие места:

* Хранилище больших двоичных объектов Azure (имя контейнера — как определено в приемник hello JsonBlob)
* Конечная точка EventHubs (как указано в приемник hello EventHubs)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

Hello `resourceId` в hello конфигурации должны совпадать, масштабирования виртуальных машин виртуальной Машины или hello hello набора.

* Метрики платформы Azure построения графиков и предупреждений об изменении знает resourceId hello объекта hello виртуальной Машины, над которыми вы работаете. Ожидается, что toofind hello данных для виртуальной Машины с помощью hello resourceId hello Уточняющий запрос ключа.
* При использовании автомасштабирования Azure resourceId hello в настройки автомасштабирования hello должно соответствовать используемой LAD resourceId hello.
* Hello resourceId встроено в написанном LAD JsonBlobs имена hello.

## <a name="view-your-data"></a>Просмотр данных

Используйте данные о производительности Azure портала tooview hello или настроить оповещения:

![изображение](./media/diagnostic-extension/graph_metrics.png)

Hello `performanceCounters` данные всегда хранятся в таблице хранилища Azure. Интерфейсы API службы хранилища Azure доступны для множества языков и платформ.

Данные, отправляемые приемники tooJsonBlob хранится в BLOB-объектов в hello учетной записи хранилища с именем в hello [защищенные параметры](#protected-settings). Вы можете использовать hello данных blob при помощи любого API хранилища больших двоичных объектов Azure.

Кроме того можно использовать эти данные hello tooaccess средства пользовательского интерфейса в службе хранилища Azure:

* Обозреватель сервера Visual Studio.
* [Обозреватель хранилищ Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Обозреватель хранилищ Azure").

Этот моментальный снимок сеанса Microsoft Azure Storage Explorer показывает hello созданные таблицы хранилища Azure и контейнеры из правильно настроенной расширения LAD 3.0 на тестовой виртуальной Машине. Hello изображения не соответствует точно hello [LAD 3.0 пример конфигурации](#an-example-lad-30-configuration).

![изображение](./media/diagnostic-extension/stg_explorer.png)

См. соответствующие hello [EventHubs документации](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn как tooconsume сообщений опубликованные конечной точки EventHubs tooan.

## <a name="next-steps"></a>Дальнейшие действия

* Создание метрики оповещений в [монитора Azure](../../monitoring-and-diagnostics/insights-alerts-portal.md) для сбора метрик hello.
* Создайте [диаграммы мониторинга](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) для метрик.
* Узнайте, каким образом слишком[создания набора масштабирования виртуальных машин](/azure/virtual-machines/linux/tutorial-create-vmss) автомасштабирования о toocontrol метрики.
