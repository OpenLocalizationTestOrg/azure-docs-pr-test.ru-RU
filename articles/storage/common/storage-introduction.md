---
title: "aaaIntroduction tooAzure хранилища | Документы Microsoft"
description: "Введение tooAzure хранилища, хранилища данных корпорации Майкрософт в облаке hello."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Введение tooMicrosoft хранилища Azure

Служба хранилища Microsoft Azure является облачной службой под управлением корпорации Майкрософт, которая предоставляет хранилище с высоким уровнем доступности, безопасности, надежности, масштабируемости и избыточности. Корпорация Майкрософт отвечает за обслуживание и решает критические проблемы, не требуя вашего участия. 

Служба хранилища Azure состоит из трех служб данных: хранилища BLOB-объектов, хранилища файлов и хранилища очередей. Хранилище больших двоичных объектов поддерживает хранение standard и premium, с хранилищем premium с помощью только SSD для наивысшей производительности hello. Другой возможностью является ожиданием хранилище, позволяя toostorage больших объемов редко используемых данных для более низкой цене.

В этой статье рассматриваются следующие вопросы hello следующее:
* службы хранилища Azure Hello
* типы учетных записей хранения Hello
* доступ к BLOB-объектам, очередям и файлам;
* шифрование;
* репликация; 
* передача данных в хранилище или из него;
* Здравствуйте множество клиентских библиотек хранилища доступен. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Введение в службы хранилища Azure hello

toouse любых служб hello указано службой хранилища Azure — хранилище больших двоичных объектов, хранения файлов и хранилища очередей--сначала создать учетную запись хранилища, и затем можно перенести данные из службы в этой учетной записи хранения. 

## <a name="blob-storage"></a>Хранилище BLOB-объектов

BLOB-объекты по сути являются файлами — такими же, как и те, что хранятся на вашем компьютере (планшете, мобильном устройстве и т. д.). Это могут быть изображения, файлы Microsoft Excel, HTML-файлы, виртуальные жесткие диски (VHD), большие данные, например журналы, резервные копии баз данных, то есть практически любые файлы. Большие двоичные объекты хранятся в контейнеры, которые являются аналогичные toofolders. 

После сохранения файлов в хранилище больших двоичных объектов, они будут доступны в любом месте в Здравствуй, мир! с помощью URL-адреса, hello интерфейс REST или один из клиентских библиотек хранилища Azure SDK hello. Клиентские библиотеки хранилища доступны для нескольких языков, включая Node.js, Java, PHP, Python, Ruby и .NET. 

Есть три типа больших двоичных объектов: блочные, добавочные и страничные (используемые для VHD-файлов).

* Блочные большие двоичные объекты являются обычных файлов используется toohold копирование tooabout 4,7 ТБ. 
* Страничные большие двоичные объекты — это файлы произвольного доступа используется toohold копирование too8 ТБ. Эти значения используются для hello VHD-файлы, которые поддерживают виртуальные машины.
* Добавление большие двоичные объекты состоят из блоков, таких как hello блочных больших двоичных объектов, но оптимизированы для операций добавления. Эти значения используются для таких вещей, как ведение журнала сведения toohello же больших двоичных объектов из нескольких виртуальных машин.

Для очень больших наборов данных, где ограничения сети выбрать передачей или загрузкой tooBlob хранения данных по сети hello разнообразны можно отправить набор tooimport tooMicrosoft жестких дисков или экспортировать данные непосредственно из центра обработки данных hello. В разделе [использовать hello службы импорта и экспорта Microsoft Azure tooTransfer данных tooBlob хранения](../storage-import-export-service.md).

## <a name="file-storage"></a>Хранилище файлов

Hello службы файлов Azure позволяет tooset копирование высокой доступности сетевых общих папок, к которым можно обращаться с помощью стандартного протокола Server Message Block (SMB) hello. Что означает, что можно совместно использовать несколько виртуальных машин hello же файлы с чтение и запись. Также может считывать файлы hello, с помощью интерфейса REST hello и клиентских библиотек хранилища hello. 

Единственное, что отличает хранилища Azure File из файлов в общей папке корпоративной файл является доступен hello файлы из любого места в hello world, используя URL-адрес, который указывает файл toohello и содержит маркер подписи общего доступа. Может создавать маркеры SAS; они позволяют закрытый активов tooa специальный доступ на определенное время. 

Общие папки можно использовать для множества распространенных сценариев. 

* Многие локальные приложения используют общие папки. Эта функция упрощает проще toomigrate этих приложений, которые совместно используют tooAzure данных. Если подключить hello же буква hello toohello общий ресурс файла локальным приложением, hello часть вашего приложения, который обращается к общей папке hello должны работать с минимальной при его наличии, изменения.

* В общей папке могут храниться файлы конфигурации. К ним можно получить доступ из нескольких виртуальных машин. Здравствуйте, средства и служебные программы, используемые несколькими разработчиками в группе могут храниться на файловом ресурсе, гарантируя, что все мог найти их, и что они используют одинаковые версии.

* Журналы диагностики, метрики и аварийные дампы являются только три примера данных, которые могут быть записаны tooa общей папки и обработки или позже проанализировать.

В это время, проверка подлинности на основе Active Directory и доступа не поддерживаются списки управления (доступом ACL), но они будут в некоторый момент в будущем hello. учетные данные учетной записи хранилища Hello, используемых tooprovide проверки подлинности для доступа к toohello общей папки. Это значит, любой пользователь с общей папкой hello подключен будут общего ресурса toohello доступа чтения и записи.

## <a name="queue-storage"></a>Хранилище очередей

Hello службы очередей Azure — используется toostore и получения сообщения. Очередь может содержать миллионы сообщений очереди сообщений может быть вверх too64 КБ Очереди являются списки часто используемые toostore toobe сообщения обрабатываются асинхронно. 

Например предположим, требуется изображений может tooupload toobe клиентов, и вы хотите toocreate эскизов для каждого изображения. Можно было бы ожидать эскизы hello toocreate при загрузке изображений hello клиента. Альтернативным вариантом могут быть toouse очереди. По завершении его передачи клиента hello записи toohello очереди сообщений. Затем имеют функцию Azure получать приветственное сообщение из очереди hello и создавать эскизы hello. Всех компонентов hello эта обработка может масштабироваться отдельно, расширяя возможности управления его настройки для использования.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>Хранилище таблиц
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
Хранилище таблиц Azure класса "Стандартный" теперь входит в состав Cosmos DB. Кроме того, для хранилища таблиц Azure доступна версия "Премиум", которая предоставляет оптимизированные для пропускной способности таблицы, глобальное распределение и автоматическое дополнительное индексирование. Дополнительные toolearn и испытать новые возможности "премиум" hello, ознакомьтесь с [Azure Cosmos DB: таблица API](https://aka.ms/premiumtables).

## <a name="disk-storage"></a>Дисковый накопитель

Группа разработчиков хранилища Azure Hello также является владельцем дисков, которого включает все управляемые hello и возможности неуправляемые диска, используемым виртуальными машинами. Дополнительные сведения об этих функциях см. в разделе hello [документации по службе вычислений](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).

## <a name="types-of-storage-accounts"></a>Типы учетных записей хранения 

Эта таблица содержит hello различных типов объектов, которые можно использовать с каждым и учетных записей хранилища.

|**Тип учетной записи хранения**|**Общего назначения, класс "Стандартный"**|**Общего назначения, класс "Премиум"**|**Хранилище BLOB-объектов, "горячий" и "холодный" уровни доступа**|
|-----|-----|-----|-----|
|**Поддерживаемые службы**| Службы BLOB-объектов, файлов, очередей | Служба BLOB-объектов | Служба BLOB-объектов|
|**Типы поддерживаемых BLOB-объектов**|Блочные, страничные и добавочные BLOB-объекты | Blob-страницы | Блочные и добавочные BLOB-объекты|

### <a name="general-purpose-storage-accounts"></a>Учетные записи хранения общего назначения

Есть два типа учетных записей хранения общего назначения. 

#### <a name="standard-storage"></a>Хранилище уровня "Стандартный" 

Чаще всего используются Hello учетных записей хранилища, учетных записей стандартного хранилища, которые могут быть использованы для всех типов данных. Данные toostore магнитных носителей использовать учетных записей стандартного хранилища.

#### <a name="premium-storage"></a>Хранилище уровня "Премиум"

Хранилище класса "Премиум" обеспечивает высокопроизводительное хранение страничных BLOB-объектов, которые в основном используются для VHD-файлов. Данные toostore SSD использовать учетные записи хранения Premium. Корпорация Майкрософт рекомендует использовать для всех виртуальных машин хранилище класса "Премиум".

### <a name="blob-storage-accounts"></a>Учетные записи хранилища BLOB-объектов

Учетная запись хранилища больших двоичных объектов Hello — учетная запись хранения специализированные используется toostore блочных больших двоичных объектов и добавления больших двоичных объектов. Страничные BLOB-объекты нельзя хранить в этих учетных записях, поэтому в них нельзя хранить и файлы VHD. Эти учетные записи позволяют tooset tooHot уровня доступа или стильной; Hello уровня могут измениться в любое время. 

Hello уровня горячей доступа используется для файлов, которые часто запрашиваются--вы платите более высокая стоимость для хранения, но hello доступ к большим двоичным объектам hello обходится намного ниже. Для больших двоичных объектов, хранящихся в hello ожиданием доступ уровня вы платите более высокая стоимость для доступа к большим двоичным объектам hello, но hello хранилища обходится намного ниже.

## <a name="accessing-your-blobs-files-and-queues"></a>Доступ к BLOB-объектам, файлам и очередям

В каждой учетной записи хранения предусмотрено два ключа проверки подлинности, которые можно использовать для любой операции. Существует два ключа для сведения по hello иногда ключи безопасности tooenhance. Очень важно, что эти ключи требуется обеспечить безопасность, так как владению вместе с именем учетной записи hello, разрешает неограниченный доступ tooall данных в учетной записи хранения hello. 

В этом разделе рассматриваются два способа toosecure hello учетной записи хранилища и его данные. Подробные сведения об обеспечении безопасности вашей учетной записи хранилища и данных в разделе hello [руководство по безопасности хранилища Azure](storage-security-guide.md).

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Защита доступа toostorage учетные записи, с помощью Azure AD

Tooyour хранения toosecure одним из способов доступа к данным — управление ключи учетной записи хранения toohello доступа. С помощью диспетчера ресурсов управления доступом на основе ролей (RBAC) можно назначить роли toousers, групп или приложений. Эти роли связаны tooa определенный набор действий, которые разрешены или запрещены. С помощью RBAC учетной записи хранилища toogrant доступа tooa обрабатывает только hello операции управления для этой учетной записи хранения, таких как изменение уровня доступа hello. Нельзя использовать RBAC toogrant доступа toodata таких объектов, как конкретного контейнера или в общей папке. Тем не менее, можно использовать RBAC toogrant доступа toohello ключи учетной записи хранения, которые затем могут быть объектами данных используется tooread hello. 

### <a name="securing-access-using-shared-access-signatures"></a>Защита доступа при помощи подписанных URL-адресов 

Можно использовать подписей общего доступа и хранимые объекты анализа toosecure политики доступа. Подписанный URL-адрес (SAS) — строка, содержащая маркер безопасности, который может быть присоединен toohello URI для ресурса, который позволяет toospecific хранения toodelegate обращаться к объектам, а также toospecify ограничения, такие как разрешения и hello диапазон даты и времени доступа. Эта функция имеет расширенные возможности. Подробные сведения см. в разделе слишком[с помощью общего доступа подписи (SAS)](storage-dotnet-shared-access-signature-part-1.md).

### <a name="public-access-tooblobs"></a>Tooblobs общего доступа

Hello службы BLOB-объектов можно tooprovide общего доступа tooa контейнера и его BLOB-объектов или определенным BLOB-объектом. Если вы указываете, что контейнер или BLOB-объект является общедоступным, любой пользователь может читать его анонимно, и проверка подлинности при этом не требуется. Примером будет при необходимости toodo, это когда у вас есть веб-сайт с помощью изображений, видео или документы из хранилища больших двоичных объектов. Дополнительные сведения см. в разделе [управления toocontainers анонимный доступ для чтения и больших двоичных объектов](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>Шифрование

Существует несколько основных типа шифрования для служб хранилища hello. 

### <a name="encryption-at-rest"></a>Шифрование при хранении 

Можно включить шифрование службы хранилища (SSE) для любой службы файлов hello (Предварительная версия) или hello BLOB-объектов учетной записи хранилища Azure. Если параметр включен, все данные, записанные определенной службы toohello шифруется перед записью. При чтении данных hello он расшифровывается до возвращения. 

### <a name="client-side-encryption"></a>шифрования на стороне клиента

Hello клиентских библиотек хранилища имеют методы, можно вызвать tooprogrammatically шифрования данных перед их отправкой по линии hello из клиента tooAzure hello. Они хранятся в зашифрованном виде. Это означает, что в неактивном состоянии они также зашифрованы. При чтении данных hello назад, то расшифровать hello сведения после их получения. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>Шифрование при обмене данными с файловыми ресурсами Azure

Дополнительные сведения см. в статье об [использовании подписанных URL-адресов (SAS)](../storage-dotnet-shared-access-signature-part-1.md). В разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](../blobs/storage-manage-access-to-resources.md) и [проверки подлинности для служб хранилища Azure hello](https://msdn.microsoft.com/library/azure/dd179428.aspx) Дополнительные сведения об учетной записи хранилища tooyour безопасного доступа.

Дополнительные сведения об обеспечении безопасности вашей учетной записи хранилища и шифрования см. в разделе hello [руководство по безопасности хранилища Azure](storage-security-guide.md).

## <a name="replication"></a>Репликация

В tooensure порядке, что данные будут сохранены хранилище Azure есть возможность tookeep hello (и управлять) несколько копий данных. Этот процесс называется репликацией (иногда избыточностью). При настройке учетной записи хранения вы выбираете тип репликации. В большинстве случаев этот параметр можно изменить после настройки учетной записи хранилища hello. 

Для всех учетных записей хранения используется **локально избыточное хранилище (LRS)**. Это означает, что три копии данных управляются с помощью хранилища Azure в центре обработки данных hello указано, когда учетная запись хранения hello был настроен. Если изменения будут зафиксированы tooone копировать, hello другие две копии будут обновлены до возвращения успех. Это означает, что три реплики hello всегда находятся в синхронизированном состоянии. Кроме того hello три копии находятся в отдельных доменах сбоя и доменах обновления, что означает, что данные будут доступны даже в случае сбоя узла хранилища, удержание данных или обновляется сделанной toobe вне сети. 

**Локально избыточное хранилище (LRS)**

Как было описано выше, благодаря LRS в одном центре обработки данных поддерживается три копии данных. Обрабатывает проблему hello данных становится недоступной, узел хранилища или переводится в автономный toobe обновлены, но не hello регистр весь центр обработки данных становится недоступной.

**Хранилище, избыточное в пределах зоны (ZRS)**

Хранилище, избыточное в пределах зоны (ZRS) поддерживает три hello локальные копии данных, а также другой набор три копии данных. Hello второй набор три копии реплицируются асинхронно в центрах обработки данных в пределах одного или двух областей. Обратите внимание, что хранилище ZRS доступно только для блочных BLOB-объектов в учетных записях хранения общего назначения. Кроме того, после создания учетной записи хранилища и выбран ZRS, его нельзя преобразовать toouse tooany других типа репликации, или наоборот.

Учетные записи ZRS обеспечивают большую надежность, чем LRS, но не предоставляют такие возможности, как метрики или ведение журналов. 

**Геоизбыточное хранилище (GRS)**

Географически избыточное хранилище (GRS) поддерживает три hello локальные копии данных в основном регионе, а также другой набор три копии данных в дополнительном регионе сотни километров от основного региона hello. В случае сбоя в основном регионе hello hello хранилища Azure будут действовать при сбое toohello дополнительный регион. 

**Геоизбыточное хранилище с доступом для чтения (RA-GRS)** 

Географически избыточное хранилище с доступом на чтение — так же, как GRS, за исключением того, что позволяет получить доступ на чтение данных toohello в дополнительное расположение hello. Если временно hello основного центра обработки данных становится недоступным, можно продолжить tooread hello данные из дополнительного расположения hello. Это может быть очень полезно. Например имеется веб-приложения, изменения в режиме только для чтения и указывает toohello дополнительная копия, позволяя доступ, даже если обновления недоступны. 

> [!IMPORTANT]
> Можно изменить, как данные реплицируются после создания учетной записи хранилища, если не указано ZRS при создании учетной записи hello. Тем не менее Обратите внимание, что вы можете понести стоимость при переключении из LRS tooGRS или RA-GRS передачи дополнительных данных одноразовый.
>

Дополнительные сведения о репликации см. в статье [Репликация службы хранилища Azure](storage-redundancy.md).

Для аварийного восстановления сведения см. в разделе [какие toodo в случае сбоя хранилища Azure](storage-disaster-recovery-guidance.md).

Пример того, как tooleverage RA-GRS хранения tooensure высокого уровня доступности и в разделе [проектирование высокой доступных приложений с помощью RA-GRS](storage-designing-ha-apps-with-ragrs.md).

## <a name="transferring-data-tooand-from-azure-storage"></a>Передача данных tooand из хранилища Azure

Можно использовать данные файлов и больших двоичных объектов программа AzCopy toocopy hello в вашей учетной записи хранилища или нескольких учетных записей хранения. Узнать, одно из следующих hello статьи для получения справки:

* [Transfer data with the AzCopy on Windows](storage-use-azcopy.md) (Перенос данных с использованием AzCopy для Windows).
* [Перенос данных с помощью AzCopy для Linux](storage-use-azcopy-linux.md).

AzCopy является надстройкой hello [библиотеки перемещения данных Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), которая в настоящее время доступна в предварительной версии.

Hello службы импорта и экспорта Azure можно использовать tooimport или экспорт больших объемов tooor данных больших двоичных объектов из вашей учетной записи хранилища. Подготовка и почты несколько жестких дисков tooan центр обработки данных Azure, где они будут перенесены данные hello из жестких дисков hello и отправки tooyou обратно hello жестких дисков. Дополнительные сведения о hello службы импорта и экспорта см. в разделе [использовать hello службы импорта и экспорта Microsoft Azure tooTransfer данных tooBlob хранения](../storage-import-export-service.md).

## <a name="pricing"></a>Цены

Подробные сведения о ценах на хранилище Azure см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/storage/blobs/).

## <a name="storage-apis-libraries-and-tools"></a>API-интерфейсы, библиотеки и средства хранилища
Для доступа к ресурсам хранилища Azure можно воспользоваться любым языком, позволяющим отправлять запросы HTTP или HTTPS. Кроме того, хранилище Azure предлагает библиотеки программирования для нескольких распространенных языков. Эти библиотеки упрощают многие аспекты работы со службой хранилища Azure, охватывая такие процессы, как синхронный и асинхронный вызов, пакетная обработка операций, управление исключениями, автоматические повторы, рабочее поведение и т. д. Библиотеки в настоящее время доступны для следующих языков hello и платформ с другими пользователями в hello конвейера:

### <a name="azure-storage-data-services"></a>Службы данных хранилища Azure
* [API-интерфейс REST служб хранилища](/rest/api/storageservices/)
* [Клиентская библиотека хранилища для .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Клиентская библиотека хранилища для C++](https://github.com/Azure/azure-storage-cpp)
* [Клиентская библиотека хранилища для Java/Android](https://azure.microsoft.com/develop/java/)
* [Клиентская библиотека хранилища для Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Клиентская библиотека хранилища для PHP](https://azure.microsoft.com/develop/php/)
* [Клиентская библиотека хранилища для Python](https://azure.microsoft.com/develop/python/)
* [Клиентская библиотека хранилища для Ruby](https://azure.microsoft.com/develop/ruby/)
* [Командлеты хранилища для PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [Команды хранилища для CLI 2.0](/cli/azure/storage)

## <a name="next-steps"></a>Дальнейшие действия

* [Introduction to Blob storage](../blobs/storage-blobs-introduction.md) (Общие сведения о хранилище BLOB-объектов)
* [Introduction to Azure File storage](../storage-files-introduction.md) (Общие сведения о хранилище файлов)
* [Introduction to Queues](../queues/storage-queues-introduction.md) (Общие сведения о хранилище очередей)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Для администраторов
* [Использование Azure PowerShell со службой хранилища Azure](storage-powershell-guide-full.md)
* [Использование интерфейса командной строки (CLI) Azure со службой хранилища Azure](../storage-azure-cli.md)

### <a name="for-net-developers"></a>Для разработчиков .NET
* [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Приступая к работе с хранилищем очередей Azure с помощью .NET](../storage-dotnet-how-to-use-queues.md)
* [Приступая к работе с хранилищем файлов Azure в Windows](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Для разработчиков Java и Android
* [Как toouse хранилища BLOB-объектов из Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Как toouse хранилище таблиц из Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [Как toouse хранилища очередей из Java](../storage-java-how-to-use-queue-storage.md)
* [Как toouse хранения файлов из Java](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Для разработчиков Node.js
* [Как toouse хранилища BLOB-объектов из Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Как toouse хранилище таблиц из Node.js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Как toouse хранилища очередей из Node.js](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Для разработчиков PHP
* [Как toouse хранилища BLOB-объектов из PHP](../blobs/storage-php-how-to-use-blobs.md)
* [Как toouse хранилище таблиц из PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [Как toouse хранилища очередей из PHP](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Для разработчиков Ruby
* [Как toouse хранилища BLOB-объектов из Ruby](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [Как toouse хранилище таблиц из Ruby](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [Как toouse хранилища очередей из Ruby](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Для разработчиков Python
* [Как toouse хранилища BLOB-объектов из Python](../blobs/storage-python-how-to-use-blob-storage.md)
* [Как toouse хранилище таблиц из Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [Как toouse хранилища очередей из Python](../storage-python-how-to-use-queue-storage.md)   
* [Как toouse хранения файлов из Python](../storage-python-how-to-use-file-storage.md) 
-->