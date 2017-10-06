---
title: "aaaUsing подписи коллективного доступа (SAS) в хранилище Azure | Документы Microsoft"
description: "Узнайте, toouse общего доступа подписи (SAS) toodelegate доступа tooAzure хранения ресурсов, включая больших двоичных объектов, очередей, таблиц и файлов."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 53e06c78fbfdaa5fd209add719995ef2a6bc8f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>Использование подписанных URL-адресов (SAS)

Подписанный URL-адрес (SAS) предоставляет способ toogrant ограниченный доступ tooobjects в вашей учетной записи хранилища клиенты tooother без предоставления ключа учетной записи. В этой статье мы укажите общие сведения о модели SAS hello, просмотрите рекомендации SAS и рассмотрим несколько примеров.

Дополнительные примеры кода с помощью SAS, помимо тех, представленные здесь, в разделе [Приступая к работе с хранилищем больших двоичных объектов Azure в .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) и в других образцах, доступных в hello [образцы кода Azure](https://azure.microsoft.com/documentation/samples/?service=storage) библиотеки. Можно загрузить пример приложения hello и запускать их или просмотр кода hello в GitHub.

## <a name="what-is-a-shared-access-signature"></a>Что такое подписанный URL-адрес?
Подписанный URL-адрес предоставляет tooresources делегированный доступ в вашей учетной записи хранилища. SAS вы можете предоставить клиентам получать доступ к tooresources вашей учетной записи хранилища без совместного использования ключи учетной записи. Это основная задача hello использования подписанных URL-адресов в приложениях--подписанный URL-адрес является tooshare безопасным способом ресурсов без ущерба для ключи учетной записи хранения.

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

SAS обеспечивает точный контроль над hello тип доступа, который вы предоставляете tooclients, имеющего hello SAS, включая:

* Интервал приветствия, через который hello SAS допустимыми, включая hello времени начала и окончания срока действия hello.
* Hello разрешения, предоставляемые hello SAS. Например SAS для большого двоичного объекта может предоставить чтения и записи большого двоичного объекта toothat разрешения но не удалить разрешения.
* Здравствуйте SAS, дополнительный IP-адрес или диапазон IP-адресов, из которых будет принимать хранилища Azure. Например можно указать диапазон IP-адресов, принадлежащих организации tooyour.
* протокол Hello, через который хранилища Azure будет принимать hello SAS. Можно использовать этот доступ tooclients toorestrict необязательный параметр, с помощью протокола HTTPS.

## <a name="when-should-you-use-a-shared-access-signature"></a>Когда следует использовать подписанный URL-адрес?
При необходимости tooresources tooprovide доступ в ваш клиент tooany учетной записи хранилища, не имеет клавиши доступа учетной записи хранилища можно использовать подписанный URL-адрес. Ваша учетная запись хранения относится и ключ первичного и вторичного доступа, которые предоставьте учетной записи tooyour административный доступ и все ресурсы в ней. Предоставление доступа к любой из этих ключей открывает вероятность вредоносной или намеренное использование вашей учетной записи toohello. Подписи коллективного доступа предоставляют безопасной альтернативой, которая позволяет клиентам tooread, запись и удаление данных в вашей учетной записи хранилища, toohello разрешения, которые явно предоставлены в соответствии с и без необходимости ключ учетной записи.

Общие сценарии, когда полезно SAS — это служба, где пользователи чтение и запись учетной записи хранилища tooyour свои собственные данные. В сценарии, где в учетной записи хранения хранятся пользовательские данные, существует два направления разработки:

1. Клиенты отправляют и скачивают данные с помощью службы интерфейсного прокси-сервера, выполняющей аутентификацию. Этой службы интерфейса прокси-сервера имеет преимущество hello, позволяя проверки бизнес-правил, но для больших объемов данных или большого объема транзакций, создание службы, которую можно масштабировать запросу toomatch может быть дорогостоящей или сложной задачей.

  ![Схема сценария. Служба интерфейсного прокси-сервера][sas-storage-fe-proxy-service]

1. Упрощенная служба проверяет подлинность клиента hello, при необходимости, а затем создает подписанный URL-адрес. После hello клиент получает hello SAS, они становятся доступными ресурсами учетных записей хранилища непосредственно с hello разрешения, определенные hello SAS и интервал приветствия, допускаемые hello SAS. Hello SAS устраняет необходимость hello для маршрутизации всех данных с помощью hello переднего плана прокси-службы.

  ![Схема сценария. Служба поставщика SAS][sas-storage-provider-service]

Многие реальные службы могут использовать сочетание этих двух подходов. Например некоторые данные могут обрабатываются и проверить через hello прокси-сервер переднего плана, а другие данные сохранены или напрямую с помощью SAS.

Кроме того вам потребуется toouse объект источника tooauthenticate hello SAS в ходе операции копирования в определенных сценариях:

* При копировании большого двоичного объекта tooanother большой двоичный объект, находящийся в другую учетную запись хранения, необходимо использовать SAS tooauthenticate hello исходного большого двоичного объекта. При необходимости можно использовать SAS tooauthenticate hello BLOB-объект назначения также.
* При копировании файла tooanother файла, находящегося в другую учетную запись хранения, необходимо использовать SAS tooauthenticate hello исходного файла. SAS tooauthenticate hello целевого файла также можно использовать при необходимости.
* При копировании файла tooa большого двоичного объекта или большого двоичного объекта файла tooa, даже если hello источника и назначения находятся объекты hello же необходимо использовать объект источника hello SAS tooauthenticate учетной записи хранилища.

## <a name="types-of-shared-access-signatures"></a>Типы подписанных URL-адресов
Теперь вы можете создавать подписанные URL-адреса двух типов:

* **SAS службы.** делегаты SAS Hello службы доступа к ресурсу tooa в одном из службы хранилища hello: hello службы больших двоичных объектов, очередей, таблицы или файла. . В разделе [создав SAS службы](https://msdn.microsoft.com/library/dn140255.aspx) и [примеры служб SAS](https://msdn.microsoft.com/library/dn140256.aspx) подробные сведения о построении маркер SAS hello службы.
* **SAS учетной записи.** делегаты SAS Hello учетной записи доступа к tooresources в одной или нескольких служб хранилища hello. Все операции hello, доступные через службу SAS также доступны через учетную запись SAS. Кроме того, с учетной записью hello SAS, вы можете делегировать доступ toooperations, применить tooa конкретной службе, такие как **Get и Set свойства службы** и **Получение статистики службы**. Вы также можете делегировать доступ tooread, запись и операции удаления контейнеров больших двоичных объектов, таблиц, очередей и общие файловые ресурсы, не допускается в отношении службы SAS. В разделе [создав SAS для учетной записи](https://msdn.microsoft.com/library/mt584140.aspx) подробные сведения о построении токен SAS hello учетной записи.

## <a name="how-a-shared-access-signature-works"></a>Принцип работы подписанного URL-адреса
Подписанный URL-адрес является знаком URI, который указывает tooone или больше ресурсов хранилища и включает маркер, содержащий специальный набор параметров запроса. токен Hello указывает способ доступа к ресурсам hello может клиентом hello. Один из параметров запроса hello, hello подписи, создается на основе параметров SAS hello и подписана ключом учетной записи hello. Эта подпись используется хранилище Azure tooauthenticate hello SAS.

Ниже приведен пример SAS URI, отображающий hello ресурса (URI) и маркер SAS hello:

![Компоненты URI SAS][sas-storage-uri]

Hello маркера SAS является строка, созданных на hello *клиента* стороны (hello в разделе [примеры SAS](#sas-examples) разделе примеры кода). Маркер SAS, созданные с помощью клиентской библиотеки хранилища hello, например, не отслеживается службой хранилища Azure каким-либо образом. Можно создать неограниченное число токенов SAS на стороне клиента hello.

Если клиент предоставляет tooAzure универсальный код Ресурса SAS хранилища как часть запроса, hello служба проверяет, параметров SAS hello и их правильность для проверки подлинности запроса hello tooverify подписи. Если служба hello проверяет допустимость подписи hello, затем hello запрос проходит проверку подлинности. В противном случае — запрос hello отклонено с кодом ошибки 403 (запрещено).

## <a name="shared-access-signature-parameters"></a>Параметры подписанного URL-адреса
Учетная запись Hello SAS токенов SAS службы включают самые распространенные параметры и принять несколько параметров, которые отличаются.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>Параметры общих tooaccount SAS и службы токенов SAS
* **Версия API** необязательный параметр, который указывает hello хранилища версии toouse tooexecute hello запрос на обслуживание.
* **Версия службы** обязательный параметр, который указывает hello хранилища версии toouse tooauthenticate hello запрос на обслуживание.
* **Время начала.** Это время hello, какие hello SAS становится недопустимым. время начала Hello подписанный URL-адрес является необязательным. Если указано время начала, hello SAS вступает в силу немедленно. Hello время начала должны задаваться в формате UTC (UTC), с обозначением специальные UTC («Z»), например `1994-11-05T13:15:30Z`.
* **Время окончания срока действия.** Это время hello, после чего hello SAS больше недействительна. Рекомендуется указать время окончания срока действия для подписи общего доступа или связать ее с хранимой политикой доступа. Hello время истечения срока действия должны быть выражены в формате UTC (UTC), с обозначением специальные UTC («Z»), например `1994-11-05T13:15:30Z` (см. Подробности ниже).
* **Разрешения.** Hello разрешения, заданные на hello SAS указывать какие операции hello клиент может выполнить для ресурса хранилища hello, с помощью hello SAS. Разрешения, доступные для SAS учетной записи и SAS службы, различаются.
* **IP-адрес.** Необязательный параметр, который указывает IP-адрес или диапазон IP-адресов за пределами Azure (см. раздел hello [маршрутизации состояние конфигурации сеанса](../expressroute/expressroute-workflows.md#routing-session-configuration-state) для Express Route) из какие tooaccept запросы.
* **Протокол.** Необязательный параметр, указывающий протокол hello разрешена для запроса. Возможными значениями являются HTTPS и HTTP (`https,http`), который является значением по умолчанию hello или HTTPS только (`https`). Обратите внимание, что использовать только протокол HTTP нельзя.
* **Подпись.** Hello подпись составляется из hello других параметров указано как часть маркера, а затем. Он использовал tooauthenticate hello SAS.

### <a name="parameters-for-a-service-sas-token"></a>Параметры маркера SAS службы
* **Ресурс хранилища.** SAS службы позволяет делегировать доступ к следующим ресурсам хранилища:
  * контейнеры и большие двоичные объекты;
  * Общие папки и файлы
  * Очереди
  * Таблицы и диапазоны сущностей таблицы

### <a name="parameters-for-an-account-sas-token"></a>Параметры маркера SAS учетной записи
* **Служба или службы.** SAS учетную запись можно делегировать доступ tooone или несколько служб хранилища hello. Например можно создать учетную запись SAS, делегатов, доступ к службе BLOB-объектов и файла toohello. Или можно создать SAS, делегатов, доступ к tooall четыре службы (больших двоичных объектов, очередей, таблицы и файла).
* **Типы ресурсов хранилища.** Счет SAS применяется tooone или несколько классов ресурсов хранения, а не конкретный ресурс. Можно создать SAS toodelegate учетной записи доступа к:
  * Уровень обслуживания API вызове для hello ресурс учетной записи хранения. Вот некоторые примеры: **Get/Set Service Properties**, **Get Service Stats** и **List Containers/Queues/Tables/Shares**.
  * API уровня контейнера, которые вызываются от объектов-контейнеров hello для каждой службы: BLOB-объектов контейнеров, очередей, таблиц и общих файловых ресурсов. Вот некоторые примеры: **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share** и **List Blobs/Files and Directories**.
  * API-интерфейсы уровня объектов, которые вызываются для больших двоичных объектов, сообщений в очереди, сущностей таблицы и отдельных файлов. Например: **Put Blob**, **Query Entity**, **Get Messages** и **Create File**.

## <a name="examples-of-sas-uris"></a>Примеры универсального кода ресурса (URI) подписанного URL-адреса

### <a name="service-sas-uri-example"></a>Пример службы URI SAS

Ниже приведен пример службы SAS URI, который предоставляет чтение и запись большого двоичного объекта tooa разрешения. Таблица Hello разбивает каждую часть hello URI toounderstand как его влияют toohello SAS:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Имя | Сегмент SAS | Описание |
| --- | --- | --- |
| URI BLOB-объекта |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |адрес Hello hello большого двоичного объекта. Обратите внимание, что настоятельно рекомендуется использовать HTTPS. |
| Версия служб хранилища |`sv=2015-04-05` |Для служб хранилища версии 2012-02-12 и более поздних версиях этот параметр указывает toouse версии hello. |
| Время начала |`st=2015-04-29T22%3A18%3A26Z` |Указывается в формате UTC. Hello SAS toobe допустимым немедленно, Опускайте hello времени начала. |
| Время окончания срока действия |`se=2015-04-30T02%3A23%3A26Z` |Указывается в формате UTC. |
| Ресурс |`sr=b` |Hello ресурсом является большой двоичный объект. |
| Разрешения |`sp=rw` |Hello разрешения, предоставляемые hello SAS включают Read (r) и записи (w). |
| Диапазон IP-адресов |`sip=168.1.5.60-168.1.5.70` |Hello диапазон IP-адресов, из которых будут приниматься запрос. |
| Протокол |`spr=https` |Разрешены запросы только по протоколу HTTPS. |
| Подпись |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Использовать большой двоичный объект toohello tooauthenticate доступа. Hello подпись представляет собой код HMAC, вычисленная строку для подписания и ключ с помощью алгоритма SHA256 hello и затем кодируются с использованием кодировки Base64. |

### <a name="account-sas-uri-example"></a>Пример URI SAS учетной записи

Ниже приведен пример учетной записи, SAS, использует hello же общие параметры маркера hello. Описание этих параметров приведено выше. Только hello параметры, которые определенные tooaccount SAS описаны в следующей таблице hello.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Имя | Сегмент SAS | Описание |
| --- | --- | --- |
| Универсальный код ресурса (URI) |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Здравствуйте, конечная точка службы BLOB-объекта с параметрами, для получения свойств службы (при вызове GET) или задания свойств службы (при вызове с НАБОРОМ). |
| Службы |`ss=bf` |применяет Hello SAS toohello больших двоичных объектов и файловых служб |
| Типы ресурсов |`srt=s` |Hello SAS применяется tooservice уровне операции. |
| Разрешения |`sp=rw` |разрешения Hello предоставления доступа tooread и операций записи. |

Учитывая, что разрешения ограничены уровня обслуживания toohello, операций доступ этот SAS, **получение свойств службы BLOB-объектов** (чтение) и **Set Blob Service Properties** (запись). Тем не менее, с другой URI ресурса, hello тот же токен SAS может стать слишком используется доступа toodelegate**Получение статистики службы больших двоичных объектов** (чтения).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Использование хранимой политики доступа для управления SAS
Подпись общего доступа может принимать одну из двух форм:

* **Ad hoc SAS:** при создании нерегламентированного SAS, hello время начала, время окончания срока действия и разрешения для hello SAS указаны в hello универсальный код Ресурса SAS (или подразумеваемых, в случае hello, где отсутствует время начала). Этот тип можно использовать для SAS учетной записи и SAS службы.
* **SAS с хранимой политикой доступа:** хранимая политика доступа определен в контейнере ресурса — контейнер больших двоичных объектов, таблицы, очереди, или общая папка--и может быть используется toomanage ограничений для одного или нескольких подписей общего доступа. При связывании подписанный URL-адрес с хранимой политикой доступа hello SAS наследует ограничения hello--hello время начала, время окончания и разрешения--, определенные для hello хранимые политики доступа.

> [!NOTE]
> На данный момент SAS учетной записи может быть только нерегламентированным. Хранимые политики доступа для SAS учетной записи пока не поддерживаются.

Hello различия между hello двух форм являются важными для одного ключевого сценария: отзыва. Так как SAS URI URL-адрес, любой пользователь, который получает hello SAS можно использовать, независимо от того, кто первоначально создал. Если открыто опубликована SAS, он может использоваться кем Здравствуй, мир!. SAS предоставляет доступ tooresources tooanyone исходя из он пока не произойдет одно из четырех возможных действий:

1. Hello окончания времени, указанного на hello достижения SAS.
2. время окончания срока действия Hello указан в политике доступа хранятся hello ссылается hello достижения SAS (если ссылаться хранимая политика доступа, и если он задает время истечения срока действия). Это может произойти, так как истекло hello, или был изменен политики доступа hello хранятся с временем окончания срока действия в hello последние, что является одним из способов toorevoke hello SAS.
3. Hello хранимой политики доступа, ссылается hello удаляется SAS, который является другим способом toorevoke hello SAS. Обратите внимание, что при повторном создании hello хранимые политики доступа с точно таким же именем, все существующие сопоставления безопасности Здравствуйте, маркеры будет снова быть допустимым соответствующим toohello разрешения, связанные с этой хранимой политики доступа (при условии, что это время окончания срока действия hello на hello SAS не прошел). Если планируется toorevoke hello SAS будет убедиться, что toouse другое имя при повторном создании hello политики доступа в будущем hello срока истечения срока действия.
4. ключ учетной записи Hello, используемые toocreate hello SAS повторно. Повторное создание ключа учетной записи приведет все компоненты приложения, с помощью этого ключа toofail tooauthenticate пока они обновлены toouse либо hello других действительной учетной записи или ключа hello вновь сформированный учетной записи.

> [!IMPORTANT]
> URI подписи коллективного доступа связан с сигнатурой hello toocreate ключа используется учетная запись hello и hello связанных хранимой политики доступа (если таковые имеются). Если хранимая политика доступа не указан, hello только способом toorevoke подписанный URL-адрес является ключ учетной записи toochange hello.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Аутентификация в клиентском приложении с SAS
Клиент, владеющий SAS можно использовать tooauthenticate SAS hello запроса к учетной записи хранилища, для которой они не имеют hello ключи учетной записи. SAS могут быть включены в строку подключения и использования непосредственно из hello соответствующего конструктора или метода.

### <a name="using-a-sas-in-a-connection-string"></a>Использование SAS в строке подключения
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>Использование SAS в конструкторе или методе
Несколько конструкторов библиотека клиента хранилища Azure и перегрузок методов предлагают параметром SAS для проверки подлинности службы toohello запрос с SAS.

Например SAS URI это используется toocreate ссылки tooa большого двоичного объекта. Hello SAS предоставляет hello только учетные данные, необходимые для запроса hello. ссылка большого двоичного объекта блока Hello затем используется для операции записи:

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>Рекомендации по использованию SAS
При использовании подписанных URL-адресов в приложениях, необходимые toobe учитывать две возможные риски.

* В случае утечки подписи ей сможет пользоваться любой человек, что потенциально может нарушить безопасность вашей учетной записи хранения.
* Если SAS tooa клиентское приложение завершается, и приложение hello — не удается tooretrieve новый SAS из службы, может ухудшить функциональность приложения hello.

Hello следующие рекомендации по использованию подписи коллективного доступа может помочь избежать этих рисков:

1. **Всегда использовать протокол HTTPS** toocreate и не распространяйте SAS. Передается по протоколу HTTP и перехват SAS, злоумышленник, выполнение атаки в середине — может tooread hello SAS и воспользуйтесь так же, как hello нужной пользователя может быть конфиденциальная конфиденциальные данные или позволить повреждения данных, hello пользователь-злоумышленник.
2. **Ссылайтесь на хранимые политики доступа, где это возможно.** Хранимые hello параметр toorevoke разрешения без необходимости ключи учетной записи хранения hello tooregenerate обеспечивает политики доступа. Срок действия hello набора на очень большом в hello будущих (или бесконечной) и убедитесь, что он регулярно обновил toomove его дальше в будущем hello.
3. **Используйте небольшой срок для нерегламентированной SAS.** Таким образом, даже если SAS скомпрометирован, он будет действителен только в течение короткого времени. Это особенно важно в случаях, когда нельзя ссылаться на хранимую политику доступа. Оперативные сроков также ограничить hello объем данных, которые могут быть записаны, ограничивая hello время доступных tooupload tooit tooa больших двоичных объектов.
4. **У клиентов автоматического возобновления hello SAS, при необходимости.** Клиенты должны обновлять hello SAS задолго до истечения срока действия hello, в порядке времени tooallow для повторных попыток в случае недоступности hello службой, предоставляющей hello SAS. Если ваш SAS предназначена toobe, используемый для небольшого числа немедленно, кратковременных операции, которые требуется toobe завершены в течение срока действия hello, то это может быть ненужные ожидаемым hello SAS не обновлен toobe. Тем не менее если у вас есть клиент, который регулярно выполняет запросы через SAS, hello возможность истечения срока действия вступает в действие. Hello ключа нюанс заключается в необходимости hello toobalance для hello SAS toobe кратковременных (как было указано) с tooensure необходимость hello, hello клиент запрашивает обновление раньше достаточно (tooavoid перебоев в работе из-за обновления истекающим сроком действия предыдущего toosuccessful toohello SAS).
5. **Будьте осторожны со временем начала действия SAS.** Следует установить время начала hello для SAS слишком**теперь**, а затем наклон tooclock (различия в текущее время, в соответствии с toodifferent машины), из-за сбоев может появляться периодически hello первые несколько минут. Как правило задайте toobe время начала hello по крайней мере 15 минут в последние hello. Или не задавайте вообще. Так SAS будет немедленно становиться действительным во всех случаях. таким же, как правило, применим tooexpiry времени также--Hello помните, можно заметить вверх too15 минут от часов наклона в любом направлении любого запроса. Для клиентов, использующих REST версии предыдущих too2012-02-12 hello максимальную продолжительность SAS, который не ссылается на хранимую политику доступа — 1 час и все политики, указание термин больше времени, чем, завершится ошибкой.
6. **Быть точным с toobe ресурсов hello доступ.** Рекомендации по безопасности — tooprovide пользователя с hello минимальные необходимые права. Если пользователю требуется только доступ для чтения tooa одной сущности, предоставьте им доступ на чтение toothat одной сущности и сущности tooall доступ не чтения, записи или удаления. Это также помогает уменьшить ущерб hello компрометация SAS причине hello SAS меньше возможностей в руках hello злоумышленника.
7. **Учитывайте, что ваша учетная запись тарифицируется за любое использование, включая то, что осуществляется посредством SAS.** Если предоставить доступ на запись tooa больших двоичных объектов, пользователь может выбрать tooupload большого двоичного объекта в 200 ГБ. Если вы предоставили их также доступ для чтения, они могут выбрать toodownload 10 раз несения 2 ТБ в исходящих издержки для вас. Опять же, предоставляют ограниченные разрешения toohelp снизить hello возможные действия злоумышленников. Используйте эту угрозу кратковременных tooreduce SAS (но следует учитывать расфазировки синхронизирующих импульсов по времени окончания hello).
8. **Проверьте данные, записанные с помощью SAS.** Когда клиентское приложение записывает данные учетной записи хранилища tooyour, имейте в виду, что могут возникнуть проблемы с этими данными. Если приложения необходимо, чтобы проверить или права, прежде чем он будет готов toouse данные, необходимо выполнять проверки после записи данных hello и до его использования в приложении. Такой подход также обеспечивает защиту от поврежденных или вредоносных данных, записываемых tooyour учетной записи, либо пользователем, который правильно получена hello SAS, либо пользователь применяет потерянных SAS.
9. **Не следует всегда использовать SAS.** Иногда hello риски, связанные с конкретной операции в вашей учетной записи хранилища hello перевешивает преимущества, получаемые SAS. Для таких операций создания службы среднего уровня, которая записывает учетной записи хранилища tooyour после выполнения бизнес правила проверки, проверку подлинности и аудита. Кроме того иногда бывает более простой доступ toomanage другими способами. Например, если вы хотите toomake все большие двоичные объекты в контейнере для чтения, можно сделать hello контейнера Public, вместо tooevery клиента SAS для доступа.
10. **Используйте приложение toomonitor аналитики хранилища.** Можно использовать ведение журнала и метрик tooobserve любой скачки сбоев проверки подлинности из-за сбоя tooan вашей SAS поставщика службы или toohello непреднамеренному удалению хранимой политики доступа. В разделе hello [блог группы разработчиков хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) для получения дополнительных сведений.

## <a name="sas-examples"></a>Примеры SAS
Ниже приведены примеры подписанных URL-адресов обоих типов: SAS учетной записи и SAS службы.

toorun примеров C# необходимо hello tooreference следующие пакеты NuGet в проекте:

* [Библиотека клиента хранилища Azure для .NET](http://www.nuget.org/packages/WindowsAzure.Storage), версии 6.x или более поздней версии (toouse учетной записи сопоставления безопасности).
* [Диспетчер конфигураций Azure](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Дополнительные примеры, показывающие, как toocreate и тестирования SAS, в разделе [образцы кода Azure для хранения](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Пример. Создание и использование учетной записи SAS
Hello следующий пример кода создает учетную запись SAS, который является допустимым для hello больших двоичных объектов и файловых служб и дает hello клиентские разрешения чтения, записи и разрешения списка tooaccess обновления API-интерфейсы. Учетная запись Hello SAS ограничивает tooHTTPS протокола hello, поэтому запрос hello следует выполнять с помощью протокола HTTPS.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

Учетная запись SAS toouse hello tooaccess уровня обслуживания API-интерфейсы для службы BLOB-объектов hello, создания клиентского объекта BLOB-объекта с помощью hello SAS и hello конечная точка хранилища больших двоичных объектов для вашей учетной записи.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Пример. Создание хранимой политики доступа
Hello следующий код создает хранимую политику доступа на контейнер. Ограничения toospecify политики доступа hello можно использовать для службы SAS для контейнера hello или его больших двоичных объектов.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Пример. Создание SAS службы для контейнера
Привет, следующий код создает SAS в контейнере. Если предоставляется hello имя существующей политики доступа, что политика связана с hello SAS. Если хранимая политика доступа, кода hello создает ad-hoc SAS для контейнера hello.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Пример. Создание SAS службы для BLOB-объекта
Привет, следующий код создает SAS для большого двоичного объекта. Если предоставляется hello имя существующей политики доступа, что политика связана с hello SAS. Если хранимая политика доступа, кода hello создает ad-hoc SAS для большого двоичного объекта hello.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Заключение
Подписи общего доступа являются полезным для предоставления ограниченных разрешений tooclients tooyour хранилища учетной записи, которой не нужен ключ учетной записи hello. Таким образом они являются жизненно важной частью hello модель безопасности для всех приложений, использующих хранилище Azure. Если выполнены рекомендации hello перечисленные здесь, можно использовать SAS tooprovide большую гибкость tooresources доступа к вашей учетной записи хранилища без ущерба для безопасности приложения hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Управление toocontainers анонимный доступ для чтения и больших двоичных объектов](storage-manage-access-to-resources.md)
* [Делегирование доступа с помощью подписанного URL-адреса](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Введение в использование SAS таблиц и очередей](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)

[sas-storage-fe-proxy-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png
[sas-storage-provider-service]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png
[sas-storage-uri]: ./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png
