---
title: "Шифрование на стороне aaaClient с Python хранилища Microsoft Azure | Документы Microsoft"
description: "Hello клиентская библиотека хранилища Azure для Python поддерживает шифрование на стороне клиента для обеспечения максимальной безопасности для приложений хранилища Azure."
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 3a52b64f93daf85a55308f8a4bee9c98b2315d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Шифрование на стороне клиента с помощью Python для службы хранилища Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Обзор
Hello [клиентская библиотека хранилища Azure для Python](https://pypi.python.org/pypi/azure-storage) поддерживает шифрование данных в клиентские приложения перед загрузкой tooAzure хранилища и расшифровки данных при загрузке toohello клиента.

> [!NOTE]
> Библиотека Python хранилища Azure Hello находится в предварительной версии.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Шифрование и расшифровка через метод конверт hello
процессы Hello шифрования и расшифровки выполните метод конверт hello.

### <a name="encryption-via-hello-envelope-technique"></a>Шифрование через метод конверт hello
Шифрование через метод конверт hello работает в hello следующими способами:

1. Клиентская библиотека хранилища Azure Hello создает ключ шифрования содержимого (CEK), который является симметричным ключом, используйте один раз.
2. Данные пользователя шифруются с помощью этого ключа CEK.
3. Hello CEK заключается в оболочку (зашифрованный) с помощью ключа hello ключа шифрования (ключ обмена Ключами). Hello KEK идентифицируется идентификатора ключа и может быть пары асимметричных ключей или симметричным ключом, который управляется локально.
   Клиентская библиотека хранилища Hello сам никогда не имеет доступа tooKEK. Библиотека Hello вызывает ключ hello упаковки алгоритма, предоставляемые hello ключа обмена Ключами. Пользователи могут выбирать toouse настраиваемых поставщиков для ключа упаковки и развертывания классом при необходимости.
4. Hello зашифрованные данные будет отправлен службе toohello хранилища Azure. Hello упакованного ключа и некоторые метаданные дополнительное шифрование хранятся как метаданные (blob) либо интерполируются с hello зашифрованные данные (очереди сообщений и сущностей таблиц).

### <a name="decryption-via-hello-envelope-technique"></a>Расшифровка через метод конверт hello
Расшифровка через метод конверт hello работает в hello следующими способами:

1. Hello клиентская библиотека предполагает, что этот пользователь hello управляет ключ hello ключа шифрования (ключ обмена Ключами) локально. Hello пользователя не требуется определенного ключа hello tooknow, который использовался для шифрования. Вместо этого ключа Сопоставитель, который разрешает tookeys разные идентификаторы ключей, можно настроить и использовать.
2. Клиентская библиотека Hello загружает hello зашифрованные данные вместе с материалами шифрования, хранящиеся в службе hello.
3. ключ шифрования перенесенного содержимого Hello (CEK) — затем распаковать (расшифрованные) с помощью ключа шифрования ключа (ключ обмена Ключами) "hello". Здесь снова, hello клиентская библиотека не имеет доступа tooKEK. Он просто вызывает распаковки алгоритм hello пользовательского поставщика.
4. Hello содержимого ключа шифрования (CEK) будет использовать toodecrypt hello шифрования пользовательских данных.

## <a name="encryption-mechanism"></a>Механизм шифрования
Клиентская библиотека хранилища Hello использует [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) в порядке tooencrypt пользовательских данных. Говоря более конкретно, это режим [цепочки цифровых блоков или CBC](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) вместе с AES. Каждая служба работает по-разному, поэтому каждая служба рассматривается отдельно.

### <a name="blobs"></a>BLOB-объекты
Клиентская библиотека Hello в настоящее время поддерживает шифрование всего больших двоичных объектов только. В частности, шифрование поддерживается, если пользователи используют hello **создания*** методы. Поддерживаются полное скачивание и скачивание диапазона, кроме того, доступно распараллеливание передачи и скачивания.

Во время шифрования hello клиентская библиотека создаст случайных вектор инициализации (IV) из 16 байтов, вместе с ключом шифрования произвольного содержимого (CEK) 32 байта и выполнять шифрование конвертов hello данных большого двоичного объекта с помощью этих сведений. Hello изолировано CEK и некоторые метаданные дополнительное шифрование затем сохраняются как метаданные вместе с hello зашифрованный BLOB-объект в службе hello больших двоичных объектов.

> [!WARNING]
> Если вы изменяете или отправке метаданные для большого двоичного объекта hello, требуется tooensure, что эти метаданные сохраняются. При передаче новые метаданные без эти метаданные, CEK упакованное Здравствуйте, вектор Инициализации и другие метаданные будут утеряны и содержимое большого двоичного объекта hello никогда не будет извлекаемые еще раз.
> 
> 

Загрузка BLOB-объект зашифрованного подразумевает получение содержимого hello hello весь большой двоичный объект с помощью hello **получить*** удобных методов. Hello упакованного CEK без оболочки и использовать в сочетании с hello вектор Инициализации (хранятся в виде метаданных большого двоичного объекта в этом случае) tooreturn hello расшифровать данные toohello пользователи.

Загрузка произвольный диапазон (**получить*** переданный методов с параметрами диапазона) в hello зашифрованный BLOB-объект состоит в настройке hello диапазон, если пользователям в порядке tooget небольшой объем дополнительных данных, которые можно использовать hello расшифровки toosuccessfully запрошенный диапазон.

Только блочные и страничные BLOB-объекты могут быть зашифрованы и расшифрованы с помощью этой схемы. В настоящее время не поддерживается шифрование добавочных BLOB-объектов.

### <a name="queues"></a>Очереди
Так как очередь сообщений может иметь любой формат, hello клиентская библиотека определяет пользовательский формат, который включает в текст сообщения hello hello вектор инициализации (IV) и ключа шифрования зашифрованного содержимого hello (CEK).

Во время шифрования hello клиентская библиотека создает случайные IV 16 байтов вместе с случайных CEK 32 байта и выполняет шифрование конвертов для текста сообщения hello очереди, используя эту информацию. Hello изолировано CEK и некоторые метаданные дополнительное шифрование затем добавляются toohello зашифрованные очереди сообщений. Это измененное сообщение (см. ниже) хранится на службу hello.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

Во время расшифровки упакованный ключ hello извлечено из очереди сообщения hello и без оболочки. Hello IV также извлекаются из очереди сообщения hello и используются вместе с данные hello без оболочки ключа toodecrypt hello очереди сообщений. Обратите внимание, что метаданные шифрования hello мал (под 500 байт), пока учитываются hello ограничение 64 КБ для очереди сообщений, hello влияние должно быть управляемым.

### <a name="tables"></a>Таблицы
Здравствуйте клиента библиотека поддерживает шифрование свойств сущности, для вставки операций и замены.

> [!NOTE]
> Слияние в настоящее время не поддерживается. Так как подмножество свойств может зашифрованные ранее с помощью другой ключ, просто слияние новых свойств hello и обновление метаданных hello приведет к потере данных. Слияние либо требует внесения дополнительных службы вызывает tooread hello существующих сущностей из службы hello, либо с помощью нового ключа каждого свойства, которые не подходят для повышения производительности.
> 
> 

Шифрование табличных данных выполняется следующим образом.

1. Пользователи указывают toobe свойства hello зашифрованы.
2. Клиентская библиотека Hello приводит к возникновению случайных вектор инициализации (IV) 16 байтов вместе с случайных ключ шифрования содержимого (CEK) 32 байта для каждой сущности и выполняет шифрование конвертов toobe отдельные свойства hello зашифрованные путем наследования новый вектор Инициализации, на свойство. Свойство Hello шифрования, хранимые как двоичные данные.
3. Hello изолировано CEK и некоторые метаданные дополнительное шифрование затем сохраняются как два дополнительных свойства зарезервированным. Hello сначала зарезервированного свойства (\_ClientEncryptionMetadata1) — это свойство строки, которая содержит hello информацию о IV, версию и упакованный ключ. Здравствуйте, во-вторых зарезервированного свойства (\_ClientEncryptionMetadata2) имеет двоичное свойство, которое содержит hello сведения о свойствах hello, которые зашифрованы. Здравствуйте, сведения в этом свойстве, второй (\_ClientEncryptionMetadata2) сам по себе зашифрован.
4. Из-за toothese дополнительные зарезервированные свойства, необходимые для шифрования пользователи теперь могут иметь только 250 пользовательские свойства вместо 252. общий размер Hello hello объекта должен быть меньше 1 МБ.
   
   Обратите внимание, что зашифрованы могут быть только строковые свойства. Если других типов свойств toobe зашифрованы, они должны быть преобразованный toostrings. Hello зашифрованные строки хранятся в службе hello как двоичные свойства и их преобразование задней toostrings (необработанных строк, не EntityProperties с типом EdmType.STRING) после расшифровки.
   
   Для таблиц Кроме toohello политики шифрования, пользователи должны указать toobe свойства hello зашифрованы. Это можно сделать, либо хранения этих свойств в объектах TableEntity с tooEdmType.STRING набор типа hello и шифрование набор tootrue или параметр encryption_resolver_function hello объекта tableservice hello. Сопоставитель шифрования — это функция, которая получает ключ секции, ключ строки и имя свойства, а затем возвращает логическое значение, которое указывает, следует ли это свойство шифровать. Во время шифрования hello клиентской библиотеки будет использовать этот toodecide сведения ли свойства должны быть зашифрованы при записи toohello сети. Делегат Hello также предоставляет возможность hello логики вокруг как свойства шифруются. (Например, если значение равно X, то шифровать свойство А; в противном случае шифровать свойства А и В.) Обратите внимание, что он является не обязательным tooprovide эти сведения при чтении или выполнения запросов к сущностям.

### <a name="batch-operations"></a>Пакетные операции
Одна политика шифрования применяется tooall строк в пакете hello. Клиентская библиотека Hello внутренне создаст нового случайного вектора Инициализации и случайных CEK каждой строки в пакете hello. Пользователи также могут выбирать tooencrypt различные свойства для каждой операции в пакете hello, определив это поведение в сопоставителе шифрования hello.
Если пакет создается диспетчер контекста с помощью метода batch() tableservice hello, политика шифрования hello tableservice автоматически будет применен toohello пакета. Если пакет был явно создан путем вызова конструктора hello, политика шифрования hello должны передаваться как параметр и без изменений для hello время существования пакета hello влево.
Обратите внимание, шифрование сущностей их вставки в пакет hello, с помощью политики шифрования пакета hello (сущности не шифруются во время фиксации hello пакета с помощью политики шифрования hello tableservice hello).

### <a name="queries"></a>Запросы
tooperform операций запроса, необходимо указать Сопоставитель ключа, может tooresolve все hello ключей в результирующем наборе hello. Если сущность, содержащиеся в результатах запроса hello не удается разрешить tooa поставщика, клиентская библиотека hello вызовет ошибку. Для любого запроса, который выполняет проекций на стороне сервера, клиентская библиотека hello добавить свойства метаданных hello специальные шифрования (\_ClientEncryptionMetadata1 и \_ClientEncryptionMetadata2) по умолчанию toohello выбранные столбцы .

> [!IMPORTANT]
> Учтите следующие важные моменты при использовании шифрования на стороне клиента.
> 
> * Если чтение из или написанием tooan зашифрован blob, передачи всего большого двоичного объекта с помощью команд и команды загрузки диапазона или целые больших двоичных объектов. Избежать написания tooan зашифрованный BLOB-объект с помощью протокола операции, такие как поместить блок, поместить список блокировок, записи страниц или очистить страниц. в противном случае может привести к повреждению hello зашифрованный BLOB-объект и не мог прочитать.
> * Для таблиц существуют аналогичные ограничения. Быть тщательно toonot зашифрованные свойства без обновления метаданных шифрования hello.
> * Если задать метаданные для зашифрованных hello большого двоичного объекта, могут быть перезаписаны hello связанные с шифрованием метаданных, необходимых для расшифровки, так как не аддитивны помещение метаданных. Это также касается моментальных снимков. Не указывайте метаданные во время создания моментального снимка зашифрованного большого двоичного объекта. Если должны быть заданы метаданные, будет убедиться, что hello toocall **get_blob_metadata** tooget первый метод hello текущих метаданных шифрования и избежать параллельных операций записи, во время метаданных.
> * Включить hello **require_encryption** флаг для hello объекта службы для пользователей, которые должны работать только с зашифрованными данными. См. дополнительные сведения ниже.
> 
> 

Клиентская библиотека хранилища Hello ожидает hello условии, что ключ обмена Ключами и ключей арбитр hello tooimplement следующий интерфейс. [хранилище ключей Azure](https://azure.microsoft.com/services/key-vault/) ожидается и будет интегрирована в эту библиотеку, когда будет готова.

## <a name="client-api--interface"></a>API-интерфейс клиента / интерфейс
После создания объекта службы хранилища (т. е. blockblobservice) hello пользователь может назначать значения toohello поля, которые составляют политику шифрования: key_encryption_key key_resolver_function и require_encryption. Пользователи могут предоставлять только ключ шифрования ключей, только сопоставитель или и то, и другое. key_encryption_key — hello базовый тип ключа, определяется с помощью идентификатора ключа и предоставляющий hello логику для упаковки и развертывания. key_resolver_function — используется tooresolve ключ во время расшифровки hello. При этом возвращается допустимый KEK по заданному идентификатору ключа. Это обеспечивает toochoose возможность hello пользователей между несколько ключей, управление которыми осуществляется в нескольких местах.

Hello KEK необходимо реализовать следующие hello toosuccessfully методы шифрования данных:

* wrap_key(CEK): hello формирует оболочку для указанного CEK (в байтах), с помощью алгоритма hello по выбору пользователя. Возвращает hello упакованного ключа.
* get_key_wrap_algorithm(): возвращает hello алгоритмом, используемым toowrap ключей.
* get_kid(): возвращает hello строка идентификатора ключа для этого ключа обмена Ключами.
  Hello ключа обмена Ключами, должны реализовывать следующие методы toosuccessfully расшифровки данных hello:
* unwrap_key (cek, алгоритм): форма hello без оболочки возвращает hello указан CEK с помощью алгоритма указана строка hello.
* get_kid(): возвращает идентификатор ключа строки для данного KEK.

Сопоставитель ключа Hello по крайней мере необходимо реализовать метод, указанный идентификатор ключа, возвращающий hello соответствующий ключ обмена Ключами реализации hello интерфейс выше. Только этот метод является toobe, назначенный свойству key_resolver_function toohello hello объекта службы.

* Для шифрования всегда используется ключ hello и hello отсутствия ключа приведет к ошибке.
* Для расшифровки:
  
  * Сопоставитель ключа Hello вызывается в том случае, если указан ключ tooget hello. Если указан Сопоставитель hello, но нет сопоставления для идентификатора ключа hello, возникает ошибка.
  * Если Сопоставитель не указан, но указанный ключ, ключ hello используется в том случае, если ее идентификатор совпадает с идентификатором ключа требуется hello. Если идентификатор hello не совпадают, возникает ошибка.
    
    Примеры шифрования в azure.storage.samples Hello <fix URL>демонстрируют более подробные сценарии конца в конец BLOB-объектов, очередей и таблиц.
      Образец реализации hello ключа обмена Ключами и ключей арбитр указаны в файлах образца hello KeyWrapper и KeyResolver соответственно.

### <a name="requireencryption-mode"></a>Режим RequireEncryption
При необходимости можно включить режим работы, где все передачи и загрузки должны быть зашифрованы. В этом режиме не удастся попыток tooupload данные без шифрования политики или загрузки данных, не шифруются на службу hello на приветствия клиента. Hello **require_encryption** флаг такое поведение службы hello объекта-элементы управления.

### <a name="blob-service-encryption"></a>Шифрование службы BLOB-объектов
Значение поля политики шифрования hello объекта blockblobservice hello. Все остальные будут обрабатываться клиентской библиотекой hello внутренним образом.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>Шифрование службы очередей
Значение поля политики шифрования hello объекта queueservice hello. Все остальные будут обрабатываться клиентской библиотекой hello внутренним образом.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>Шифрование службы таблиц
В дополнение к этому toocreating политику шифрования и задание его параметров запроса, необходимо указать **encryption_resolver_function** на hello **tableservice**, или набор hello зашифровать атрибут на Hello EntityProperty.

### <a name="using-hello-resolver"></a>С помощью сопоставителя hello

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>Использование атрибутов
Как упоминалось выше, свойства могут быть помечены для шифрования, сохраняя его в объект EntityProperty и установка hello шифрование поля.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>Шифрование и производительность
Обратите внимание, что шифрование результатов анализа данных хранилища отрицательно влияет на производительность. Здравствуйте, содержимое, ключ и вектор Инициализации должен быть создан, должен быть зашифрован само содержимое hello и дополнительные метаданные должны быть в формате и отправки. Эти затраты будут зависеть от hello Кол-во время шифрования данных. Мы рекомендуем клиентам всегда тестировать свои приложения для повышения производительности во время разработки.

## <a name="next-steps"></a>Дальнейшие действия
* Загрузите hello [клиентская библиотека хранилища Azure для Java PyPi пакета](https://pypi.python.org/pypi/azure-storage)
* Загрузите hello [клиентская библиотека хранилища Azure для Python исходного кода из GitHub](https://github.com/Azure/azure-storage-python)
