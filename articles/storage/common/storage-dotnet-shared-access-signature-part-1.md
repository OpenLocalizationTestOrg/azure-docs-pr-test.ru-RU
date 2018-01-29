---
title: "Использование подписанных URL-адресов (SAS) в службе хранилища Azure | Документация Майкрософт"
description: "Сведения о делегировании доступа к ресурсам службы хранилища Azure, включая большие двоичные объекты, очереди, таблицы и файлы, с помощью подписанного URL-адреса (SAS)."
services: storage
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: tamram
ms.openlocfilehash: 32e92e6ffc376d27297810596691f0371770e86d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="using-shared-access-signatures-sas"></a>Использование подписанных URL-адресов (SAS)

Подписанный URL-адрес (SAS) позволяет вам предоставлять другим клиентам ограниченный доступ к объектам в вашей учетной записи хранения без предоставления ключа вашей учетной записи. В этой статье содержится обзор модели SAS, рекомендации по использованию SAS, а также рассмотрены некоторые примеры.

Дополнительные примеры кода, использующего SAS, кроме представленных здесь, см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure в .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/). Другие примеры см. в библиотеке [Примеры кода Azure](https://azure.microsoft.com/documentation/samples/?service=storage). Вы можете скачать примеры приложений и запустить их или просмотреть код на GitHub.

## <a name="what-is-a-shared-access-signature"></a>Что такое подписанный URL-адрес?
Подпись общего доступа обеспечивает делегированный доступ к ресурсам в вашей учетной записи хранения. С помощью SAS можно предоставить клиентам доступ к ресурсам в учетной записи хранения, не предоставляя общий доступ к ключам учетной записи. Это ключевой момент использования подписанного URL-адреса в приложениях — SAS представляет собой безопасный способ предоставления общего доступа к ресурсам хранилища без ущерба для ключей учетной записи.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

SAS обеспечивает детализированный контроль над типом доступа, предоставляемого клиентам, имеющим SAS, включая:

* Период действия SAS, включая время начала и окончания срока действия.
* Разрешения, предоставляемые с помощью SAS. Например, SAS для большого двоичного объекта может предоставить разрешения на чтение и запись для него, но не разрешение на удаление.
* Дополнительный IP-адрес или диапазон IP-адресов, по которым служба хранилища Azure будет принимать SAS. Например, можно указать диапазон IP-адресов, принадлежащих организации.
* Протокол, по которому служба хранилища Azure будет принимать SAS. С помощью этого необязательного параметра можно ограничить доступ к клиентам, использующим протокол HTTPS.

## <a name="when-should-you-use-a-shared-access-signature"></a>Когда следует использовать подписанный URL-адрес?
SAS можно использовать, когда доступ к ресурсам в вашей учетной записи хранения требуется предоставить клиенту, который не имеет ключей доступа к вашей учетной записи. Ваша учетная запись хранения включает в себя как первичный, так и вторичный ключ, и оба эти ключа предоставляют административный доступ к вашей учетной записи и всем ее ресурсам. Предоставление любого из этих ключей делает учетную запись уязвимой для вредоносного или небрежного использования. Подписанные URL-адреса обеспечивают безопасную альтернативу, позволяющую клиентам считывать, записывать и удалять данные в вашей учетной записи хранения в соответствии с явно выданными вами разрешениями и без потребности в ключе учетной записи.

Распространенным сценарием использования подписей общего доступа является служба, где пользователи считывают и записывают собственные данные в вашей учетной записи хранения. В сценарии, где в учетной записи хранения хранятся пользовательские данные, существует два направления разработки:

1. Клиенты отправляют и скачивают данные с помощью службы интерфейсного прокси-сервера, выполняющей аутентификацию. Эта служба интерфейсного прокси-сервера позволяет проверять бизнес-правила, однако для больших объемов данных или крупных транзакций создание службы, поддерживающей масштабирование в соответствии с потребностями, может оказаться дорогостоящей или сложной задачей.

  ![Схема сценария. Служба интерфейсного прокси-сервера](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png)   

1. Облегченная служба аутентифицирует клиент по мере необходимости, а затем создает SAS. Клиент, получив эту подпись общего доступа, может осуществлять прямой доступ к ресурсам учетной записи хранения с разрешениями, определенными в подписи, и в течение разрешенного подписью периода времени. Подпись общего доступа уменьшает потребность в маршрутизации всех данных через службу интерфейсного прокси-сервера.

  ![Схема сценария. Служба поставщика SAS](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png)   

Многие реальные службы могут использовать сочетание этих двух подходов. Например, некоторые данные обрабатываются и проверяются через интерфейсный прокси-сервер, а другие данные сохраняются и (или) считываются непосредственно с помощью SAS.

Кроме того, SAS потребуется использовать для проверки подлинности исходного объекта в операции копирования при определенных сценариях:

* При копировании большого двоичного объекта в другой большой двоичный объект, который относится к другой учетной записи, необходимо использовать SAS для проверки подлинности исходного большого двоичного объекта. Вы можете по желанию использовать SAS также для аутентификации конечного большого двоичного объекта.
* При копировании файла в другой файл, который относится к другой учетной записи, необходимо использовать SAS для проверки подлинности исходного файла. Вы можете по желанию использовать SAS также для аутентификации конечного файла.
* При копировании большого двоичного объекта в файл или файла в большой двоичный объект, необходимо использовать SAS для проверки подлинности исходного объекта, даже если исходный и конечный объекты относятся к одной и той же учетной записи хранения.

## <a name="types-of-shared-access-signatures"></a>Типы подписанных URL-адресов
Теперь вы можете создавать подписанные URL-адреса двух типов:

* **SAS службы.** SAS службы делегирует доступ к ресурсу только в одной из служб хранения: службе BLOB-объектов, очередей, таблиц или файлов. Подробные сведения о создании маркеров SAS службы см. в статьях [Создание SAS службы](https://msdn.microsoft.com/library/dn140255.aspx) и [Примеры SAS службы](https://msdn.microsoft.com/library/dn140256.aspx).
* **SAS учетной записи.** SAS учетной записи делегирует доступ к ресурсам в одной или нескольких службах хранилища. SAS учетной записи предоставляет доступ ко всем операциям, которые доступны через SAS службы. Кроме того, SAS учетной записи позволяет делегировать доступ к операциям, относящимся к конкретной службе, таким как **получение и установка свойств службы** или **получение статистики службы**. Вы также можете делегировать доступ к операциям чтения, записи и удаления в контейнерах больших двоичных объектов, таблицах, очередях и общих папках, которые запрещены в SAS службы. Подробные сведения о создании маркера SAS учетной записи см. в статье [Создание подписанного URL-адреса уровня учетной записи](https://msdn.microsoft.com/library/mt584140.aspx).

## <a name="how-a-shared-access-signature-works"></a>Принцип работы подписанного URL-адреса
Подписанный URL-адрес — это подписанный URI, который указывает на один или несколько ресурсов хранилища и содержит маркер с особым набором параметров запроса. Маркер определяет способы доступа к ресурсам, предоставляемые клиенту. Один из параметров запроса (подпись) состоит из параметров SAS и подписывается с помощью ключа учетной записи. Эта подпись используется хранилищем Azure для проверки подлинности подписи общего доступа.

Ниже представлен пример URI SAS, показывающий URI ресурса и маркер SAS:

![Компоненты URI SAS](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png)   

Маркер SAS — это строка, созданная на стороне [клиента](#sas-examples) (примеры кода см. в разделе *Примеры SAS* ниже). Например, служба хранилища Azure не отслеживает маркер SAS, созданный клиентской библиотекой хранилища. На стороне клиента можно создать неограниченное число маркеров SAS.

Если клиент предоставляет URI SAS в службу хранилища Azure как часть запроса, то служба проверяет параметры и подпись SAS, чтобы убедиться, что он является допустимым для аутентификации запроса. Если в ходе проверки подпись оказывается допустимой, запрос проходит аутентификацию. В противном случае запрос отклоняется и происходит ошибка с кодом 403 (запрещено).

## <a name="shared-access-signature-parameters"></a>Параметры подписанного URL-адреса
Некоторые параметры маркеров SAS учетной записи и SAS службы совпадают, но есть и параметры, которые различаются.

### <a name="parameters-common-to-account-sas-and-service-sas-tokens"></a>Параметры, общие для маркеров SAS учетной записи и SAS службы
* **Версия API.** Необязательный параметр, который указывает версию службы хранилища для выполнения запроса.
* **Версия службы.** Обязательный параметр, который указывает версию службы хранилища для аутентификации запроса.
* **Время начала.** Это время, когда подпись общего доступа становится действительной. Оно необязательно для подписанного URL-адреса. Если время начала не указано, SAS вступает в силу немедленно. Время начала должно быть выражено в формате UTC с соответствующим указателем ("Z"), например `1994-11-05T13:15:30Z`.
* **Время окончания срока действия.** Это время, после которого подпись общего доступа перестает быть действительной. Рекомендуется указать время окончания срока действия для подписи общего доступа или связать ее с хранимой политикой доступа. Время окончания срока действия должно быть выражено в формате UTC с соответствующим указателем ("Z"), например `1994-11-05T13:15:30Z` (дополнительные сведения см. ниже).
* **Разрешения.** Разрешения, заданные для подписи общего доступа, указывают операции, которые клиент может выполнять для ресурсов хранилища с помощью этой подписи общего доступа. Разрешения, доступные для SAS учетной записи и SAS службы, различаются.
* **IP-адрес.** Необязательный параметр, который указывает IP-адрес или диапазон IP-адресов за пределами Azure (см. раздел [Состояние конфигурации сеанса маршрутизации](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) для ExpressRoute), с которых следует принимать запросы.
* **Протокол.** Необязательный параметр, который задает допустимый протокол для запроса. Параметр может иметь значение `https,http` (принимаются протоколы HTTPS и HTTP, это значение используется по умолчанию) или `https` (только протокол HTTPS). Обратите внимание, что использовать только протокол HTTP нельзя.
* **Подпись.** Подпись составляется из других параметров, указанных в маркере, а затем шифруется. Она используется для проверки подлинности SAS.

### <a name="parameters-for-a-service-sas-token"></a>Параметры маркера SAS службы
* **Ресурс хранилища.** SAS службы позволяет делегировать доступ к следующим ресурсам хранилища:
  * контейнеры и большие двоичные объекты;
  * Общие папки и файлы
  * Очереди
  * Таблицы и диапазоны сущностей таблицы

### <a name="parameters-for-an-account-sas-token"></a>Параметры маркера SAS учетной записи
* **Служба или службы.** SAS учетной записи может делегировать доступ к одной или нескольким службам хранилища. Например, вы можете создать подписанный URL-адрес учетной записи, делегирующий доступ к службе BLOB-объектов или службе файлов. Также вы можете создать подписанный URL-адрес, делегирующий доступ ко всем четырем службам (BLOB-объектов, очередей, таблиц и файлов).
* **Типы ресурсов хранилища.** SAS учетной записи применяется к одному или нескольким классам ресурсов хранилища, а не к конкретному ресурсу. С помощью SAS учетной записи можно делегировать доступ к следующим типам ресурсов:
  * API-интерфейсы уровня службы, которые вызываются для ресурсов учетной записи хранения. Вот некоторые примеры: **Get/Set Service Properties**, **Get Service Stats** и **List Containers/Queues/Tables/Shares**.
  * API-интерфейсы уровня контейнеров, которые вызываются для объектов-контейнеров каждой службы: BLOB-контейнеров, очередей, таблиц и общих папок. Вот некоторые примеры: **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share** и **List Blobs/Files and Directories**.
  * API-интерфейсы уровня объектов, которые вызываются для больших двоичных объектов, сообщений в очереди, сущностей таблицы и отдельных файлов. Например: **Put Blob**, **Query Entity**, **Get Messages** и **Create File**.

## <a name="examples-of-sas-uris"></a>Примеры универсального кода ресурса (URI) подписанного URL-адреса

### <a name="service-sas-uri-example"></a>Пример службы URI SAS

В примере ниже универсальный код ресурса (URI) подписанного URL-адреса службы предоставляет разрешения на чтение и запись для BLOB-объекта. В таблице описана каждая из частей URI, чтобы можно было понять ее роль в работе подписи общего доступа:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Имя | Сегмент SAS | Описание |
| --- | --- | --- |
| URI BLOB-объекта |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |Адрес BLOB-объекта. Обратите внимание, что настоятельно рекомендуется использовать HTTPS. |
| Версия служб хранилища |`sv=2015-04-05` |Для служб хранилища версии 2012-02-12 и более поздней этот параметр указывает используемую версию. |
| Время начала |`st=2015-04-29T22%3A18%3A26Z` |Указывается в формате UTC. Чтобы подпись общего доступа вступала в силу сразу же, не указывайте время начала действия. |
| Время окончания срока действия |`se=2015-04-30T02%3A23%3A26Z` |Указывается в формате UTC. |
| Ресурс |`sr=b` |Ресурс является BLOB-объектом. |
| Разрешения |`sp=rw` |Разрешения, предоставляемые подписью общего доступа, включают в себя чтение (r) и запись (w). |
| Диапазон IP-адресов |`sip=168.1.5.60-168.1.5.70` |Диапазон IP-адресов, с которых будут приниматься запросы. |
| Протокол |`spr=https` |Разрешены запросы только по протоколу HTTPS. |
| Подпись |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Используется для проверки подлинности доступа к BLOB-объекту. Подпись представляет собой код HMAC, рассчитанный по алгоритму SHA256 с использованием ключа и преобразования строки в символы. Полученное значение преобразуется в кодировку Base64. |

### <a name="account-sas-uri-example"></a>Пример URI SAS учетной записи

В этом примере представлен SAS учетной записи c теми же общими параметрами маркера. Описание этих параметров приведено выше. В следующей таблице указаны только те параметры, которые относятся к SAS учетной записи.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Имя | Сегмент SAS | Описание |
| --- | --- | --- |
| Универсальный код ресурса (URI) |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Конечная точка службы BLOB-объектов с параметрами для получения свойств службы (для запроса GET) или задания свойств службы (для запроса SET). |
| Службы |`ss=bf` |SAS применяется к службам больших двоичных объектов и службам файлов. |
| Типы ресурсов |`srt=s` |SAS применяется к операциям на уровне службы. |
| Разрешения |`sp=rw` |Разрешения предоставляют доступ к операциям чтения и записи. |

Так как разрешения ограничены уровнем служб, этот SAS позволяет выполнять такие операции: **Get Blob Service Properties** (чтение) и **Set Blob Service Properties** (запись). Этот же токен SAS с другим универсальным кодом ресурса (URI) ресурса будет предоставлять доступ к операции **Получение статистики службы BLOB-объектов** (чтение).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Использование хранимой политики доступа для управления SAS
Подпись общего доступа может принимать одну из двух форм:

* **Нерегламентированный SAS.** При создании нерегламентированного SAS время начала, время окончания срока действия и разрешения для SAS указываются в URI SAS (или подразумеваются в случае, когда опускается время начала). Этот тип можно использовать для SAS учетной записи и SAS службы.
* **SAS с хранимой политикой доступа.** Хранимая политика доступа определяется в контейнере ресурсов (контейнере больших двоичных объектов, таблице, очереди или общей папке) и может использоваться для управления ограничениями одного или нескольких подписанных URL-адресов. При сопоставлении подписанного URL-адреса с хранимой политикой доступа этот адрес наследует ограничения (время начала, время окончания и разрешения), определенные для данной хранимой политики доступа.

> [!NOTE]
> На данный момент SAS учетной записи может быть только нерегламентированным. Хранимые политики доступа для SAS учетной записи пока не поддерживаются.

Различие между этими двумя формами важно для одного ключевого сценария — отзыва. Так как URI SAS представляет собой URL-адрес, любой пользователь, который получает SAS, может его использовать независимо от того, кто его первоначально создал. Размещенный в свободном доступе подписанный URL-адрес сможет использовать любой человек. SAS предоставляет доступ к ресурсам любому пользователю, который им обладает, пока не произойдет одно из четырех возможных событий:

1. Наступает время истечения срока действия, указанное для данной подписи общего доступа.
2. Наступает время истечения срока действия, указанное в хранимой политике доступа, на которую ссылается подпись общего доступа (если имеется ссылка на хранимую политику доступа, в которой задано время окончания срока действия). Это может произойти либо из-за истечения заданного времени, либо из-за изменения хранимой политики доступа с переносом времени окончания срока действия в прошлое, что является одним из способов отозвать подписанный URL-адрес.
3. Удаляется хранимая политика доступа, на которую ссылается подпись, что является другим способом отозвать подпись общего доступа. Заметьте, что при повторном создании хранимой политики доступа с таким же именем все существующие маркеры подписи общего доступа снова станут действительными в соответствии с разрешениями, связанными с этой хранимой политикой доступа (предполагается, что время окончания срока действия для подписи общего доступа еще не истекло). Если планируется отозвать подпись общего доступа, следует использовать другое имя при повторном создании политики доступа, у которой время окончания срока действия относится к будущему.
4. Повторно создается ключ учетной записи, который был использован для создания подписи общего доступа. Повторное создание ключа учетной записи приведет к тому, что все компоненты приложения, которые используют этот ключ, будут неспособны пройти аутентификацию до тех пор, пока они не будут обновлены, чтобы использовать другой действительный или вновь созданный ключ учетной записи.

> [!IMPORTANT]
> URI подписанного URL-адреса связан с ключом учетной записи, который использовался для создания подписи и соответствующей хранимой политики доступа (при наличии таковой). Если хранимая политика доступа не указана, то единственный способ отменить подписанный URL-адрес — изменить ключ учетной записи.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Аутентификация в клиентском приложении с SAS
Клиент, владеющий SAS, может использовать его для аутентификации запроса к учетной записи хранения, для которой у него нет ключей учетной записи. SAS можно добавить в строку подключения и непосредственно использовать в соответствующем конструкторе или методе.

### <a name="using-a-sas-in-a-connection-string"></a>Использование SAS в строке подключения
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>Использование SAS в конструкторе или методе
Несколько конструкторов и перегрузок методов из клиентской библиотеки службы хранилища Azure предлагают параметр SAS, чтобы можно было аутентифицировать запрос к службе с использованием SAS.

Например, здесь URI SAS позволяет создать ссылку на большой двоичный объект. SAS предоставляет только учетные данные, необходимые для запроса. Затем ссылка на блочный BLOB-объект используется для операции записи:

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with the specified name to the container.
// If the blob does not exist, it will be created. If it does exist, it will be overwritten.
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
При использовании подписей общего доступа в приложениях необходимо иметь в виду две потенциальные проблемы:

* В случае утечки подписи ей сможет пользоваться любой человек, что потенциально может нарушить безопасность вашей учетной записи хранения.
* Если срок действия подписи, предоставленной клиентскому приложению, истекает и приложение не может получить новую подпись из вашей службы, это может нарушить работу приложения.

Следующие рекомендации по использованию подписанных URL-адресов помогут нейтрализовать эти риски:

1. **Всегда используйте HTTPS** для создания подписанного URL-адреса или его распространения. Если SAS передается по протоколу HTTP и перехватывается, посредством атак "злоумышленник в середине" злоумышленник сможет считать SAS и затем использовать его вместо предполагаемого пользователя, что может привести к раскрытию конфиденциальных данных или к повреждению данных злоумышленником.
2. **Ссылайтесь на хранимые политики доступа, где это возможно.** Хранимые политики доступа дают возможность отозвать разрешения без повторного создания ключей учетной записи хранения. Задайте для них очень большой (или бесконечный) срок действия и убедитесь, что он регулярно переносится на будущее время.
3. **Используйте небольшой срок для нерегламентированной SAS.** Таким образом, даже если SAS скомпрометирован, он будет действителен только в течение короткого времени. Это особенно важно в случаях, когда нельзя ссылаться на хранимую политику доступа. Небольшой срок также позволяет ограничить объем данных, который может быть записан в большой двоичный объект, путем ограничения времени на отправку этих данных.
4. **Запрограммируйте автоматическое обновление подписи клиентами при необходимости.** Клиенты должны обновлять SAS задолго до окончания его срока действия, чтобы оставить время для повторных попыток в случае недоступности службы, предоставляющей SAS. Если SAS будет использоваться для небольшого числа кратковременных операций, которые должны быть завершены в течение заданного периода действия, такая мера может оказаться лишней, так как обновление SAS не предусматривается. Однако если имеется клиент, регулярно выполняющий запросы через подпись, то возможность истечения срока действия следует принять во внимание. Рекомендуется сбалансировать требование к кратковременности использования подписи (как указано ранее) с требованием того, чтобы клиент запрашивал обновление достаточно рано во избежание проблем, связанных с истечением срока действия SAS до завершения обновления.
5. **Будьте осторожны со временем начала действия SAS.** Если задать для времени начала действия SAS значение **now**, то из-за разницы во времени (разницы в текущем времени на разных компьютерах) могут наблюдаться периодические сбои в течение первых нескольких минут. В общем, устанавливайте время начала действия на 15 минут или более в прошлом времени. Или не задавайте вообще. Так SAS будет немедленно становиться действительным во всех случаях. То же касается и времени истечения срока действия. Помните, что для каждого запроса может наблюдаться рассинхронизация по времени до 15 минут в любом направлении. Для клиентов, использующих версию REST, предшествующую версии 2012-02-12, максимальный срок действия SAS, который не ссылается на хранимую политику, составляет 1 час, а все политики, где указано большее время, вызовут сбой.
6. **Четко указывайте ресурс, к которому осуществляется доступ.** Из соображений безопасности рекомендуется предоставить пользователю минимально необходимый набор прав. Если пользователю требуется только доступ для чтения к отдельной сущности, предоставьте доступ на чтение к этой сущности, а не доступ на чтение, запись и удаление для всех сущностей. Это также позволяет уменьшить ущерб, если SAS скомпрометирован, так как такой SAS предоставляет меньше возможностей злоумышленнику.
7. **Учитывайте, что ваша учетная запись тарифицируется за любое использование, включая то, что осуществляется посредством SAS.** Если вы предоставляете доступ на запись к BLOB-объекту, пользователь может отправить BLOB-объект размером 200 ГБ. Если вы также предоставляете доступ на чтение, пользователь может скачать его 10 раз, в результате чего вам потребуется оплачивать исходящий трафик объемом 2 ТБ. Опять же, ограниченные разрешения помогают сузить спектр возможностей злоумышленников. Используйте краткосрочные подписи, чтобы снизить угрозу (но помните о влиянии рассинхронизации часов на время окончания действия).
8. **Проверьте данные, записанные с помощью SAS.** Когда клиентское приложение записывает данные в вашу учетную запись хранения, помните, что эти данные могут стать источником проблем. Если приложение требует проверять достоверность или подлинность данных перед их использованием, такую проверку следует выполнять после записи данных и перед их использованием в приложении. Такой подход также обеспечивает защиту от поврежденных или вредоносных данных, записываемых в вашу учетную запись как пользователем, который получил подпись правомерно, так и пользователем, использующим подпись после ее утечки.
9. **Не следует всегда использовать SAS.** Иногда риски для вашей учетной записи хранения, связанные с конкретной операцией, перевешивают преимущества подписи общего доступа. Для таких операций создавайте службу среднего уровня, которая записывает данные в вашу учетную запись хранения после выполнения проверки, проверки подлинности и аудита на основании бизнес-правил. Кроме того, иногда проще организовать управление доступом другим образом. Например, если вы хотите сделать все BLOB-объекты в контейнере общедоступными для чтения, можно сделать этот контейнер открытым, не предоставляя всем клиентам подпись общего доступа.
10. **Используйте аналитику хранилища для мониторинга приложения.** Вы можете использовать ведение журнала и метрики, чтобы определять всплески сбоев проверки подлинности, вызванных сбоем в службе поставщика подписей общего доступа или непреднамеренным удалением хранимой политики доступа. Дополнительные сведения см. в [блоге группы разработчиков хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx).

## <a name="sas-examples"></a>Примеры SAS
Ниже приведены примеры подписанных URL-адресов обоих типов: SAS учетной записи и SAS службы.

Для выполнения этих примеров C# необходимо ссылаться на следующие пакеты NuGet в своем проекте:

* [Клиентская библиотека службы хранилища Azure для .NET](http://www.nuget.org/packages/WindowsAzure.Storage)версии 6.0 или более поздней (для использования учетной записи SAS).
* [Диспетчер конфигураций Azure](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Дополнительные примеры, в которых показано, как создать и проверить SAS, см. в разделе [Примеры кода Azure для хранилища](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Пример. Создание и использование учетной записи SAS
В следующем примере кода показано создание подписанного URL-адреса учетной записи, который действует для службы BLOB-объектов или службы файлов и предоставляет клиенту права на чтение, запись и получение списков через API-интерфейсы уровня службы. В SAS учетной записи указано ограничение на использование протоколов, поэтому запрос должен быть выполнен с помощью протокола HTTPS.

```csharp
static string GetAccountSASToken()
{
    // To create the account SAS, you need to use your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for the account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return the SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

Чтобы использовать SAS учетной записи для доступа к API-интерфейсам уровня службы для службы BLOB-объектов, создайте клиентский BLOB-объект с помощью SAS и конечной точки хранилища BLOB-объектов для вашей учетной записи хранения.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using the SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and the account name to create a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set the service properties for the Blob client created with the SAS.
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

    // The permissions granted by the account SAS also permit you to retrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Пример. Создание хранимой политики доступа
Следующий код создает хранимую политику доступа для контейнера. Политики доступа можно использовать для указания ограничений для SAS службы, накладываемые на контейнер или BLOB-объекты.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // The access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
        // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get the container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Пример. Создание SAS службы для контейнера
Следующий код создает SAS для контейнера. Если указано имя существующей хранимой политики доступа, то эта политика будет связана с SAS. Если хранимая политика доступа не указана, код создает для контейнера временную SAS.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that the SharedAccessBlobPolicy class is used both to define the parameters of an ad-hoc SAS, and
        // to construct a shared access policy that is saved to the container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
            // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate the shared access signature on the container, setting the constraints directly on the signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate the shared access signature on the container. In this case, all of the constraints for the
        // shared access signature are specified on the stored access policy, which is provided by name.
        // It is also possible to specify some constraints on an ad-hoc SAS and others on the stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Пример. Создание SAS службы для BLOB-объекта
Следующий код создает SAS для BLOB-объекта. Если указано имя существующей хранимой политики доступа, то эта политика будет связана с SAS. Если хранимая политика доступа не указана, код создает для BLOB-объекта временную SAS.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference to a blob within the container.
    // Note that the blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that the SharedAccessBlobPolicy class is used both to define the parameters of an ad-hoc SAS, and
        // to construct a shared access policy that is saved to the container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When the start time for the SAS is omitted, the start time is assumed to be the time when the storage service receives the request.
            // Omitting the start time for a SAS that is effective immediately helps to avoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate the shared access signature on the blob, setting the constraints directly on the signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate the shared access signature on the blob. In this case, all of the constraints for the
        // shared access signature are specified on the container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Заключение
Подписи общего доступа удобно применять в целях предоставления ограниченных разрешений для вашей учетной записи хранения тем клиентам, которые нельзя передавать ключ учетной записи. Таким образом, они являются важной частью модели обеспечения безопасности для любого приложения, использующего хранилище Azure. Если следовать указанным здесь рекомендациям, подписи общего доступа позволяют повысить гибкость доступа к ресурсам в вашей учетной записи хранения без ущерба для безопасности приложения.

## <a name="next-steps"></a>Дальнейшие действия
* [Подписанные URL-адреса. Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов](../blobs/storage-dotnet-shared-access-signature-part-2.md)
* [Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам](../blobs/storage-manage-access-to-resources.md)
* [Делегирование доступа с помощью подписанного URL-адреса](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Введение в использование SAS таблиц и очередей](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
