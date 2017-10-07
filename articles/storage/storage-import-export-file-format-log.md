---
title: "формат файла журнала импорта и экспорта aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о формате hello hello файлов журналов, созданные при выполнении шагов для задания службы импорта и экспорта."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Формат файла журнала службы импорта и экспорта Azure
Когда hello службы импорта и экспорта Microsoft Azure выполняет действия на диске в рамках задания импорта или экспорта, журналы записываются tooblock большие двоичные объекты в учетной записи хранения hello, связанной с этим заданием.  
  
Существует два журнала, которые могут записывать hello службы импорта и экспорта.  
  
-   Hello журнал ошибок всегда создается в hello события ошибки.  
  
-   Hello подробного журнала не включено по умолчанию, но может быть включена путем установки hello `EnableVerboseLog` свойство [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) или [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) операции.  
  
## <a name="log-file-location"></a>Расположение файла журнала  
Hello журналы записываются tooblock большие двоичные объекты в контейнере hello или виртуальный каталог, заданный параметром hello `ImportExportStatesPath` параметр, который можно установить на `Put Job` операции. Hello расположение toowhich hello журналы записываются зависит от того, каким образом задана проверка подлинности для задания hello и hello значение, указанное для `ImportExportStatesPath`. Проверка подлинности для задания hello может быть указан с помощью ключа учетной записи хранения или SAS (подписанного URL-адреса) контейнера.  
  
Имя Hello hello контейнер или виртуальный каталог может быть именем по умолчанию hello `waimportexport`, или другой контейнер или имя виртуального каталога.  
  
в следующей таблице Hello показаны hello возможные параметры:  
  
|Метод проверки подлинности|Значение параметра `ImportExportStatesPath`Element|Расположение больших двоичных объектов журналов|  
|---------------------------|----------------------------------------------|---------------------------|  
|Ключ учетной записи хранения|Значение по умолчанию|Контейнер с именем `waimportexport`, который является контейнером по умолчанию hello. Например:<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|Ключ учетной записи хранения|Значение, заданное пользователем|Контейнер с именем hello пользователь. Например:<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|SAS контейнера|Значение по умолчанию|Виртуальный каталог с именем `waimportexport`, которое является именем по умолчанию hello, контейнере hello, указанном в hello SAS.<br /><br /> Например, если hello SAS для задания hello является `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, то будет расположение журнала hello`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|SAS контейнера|Значение, заданное пользователем|Виртуальный каталог с именем пользователем hello контейнере hello, указанном в hello SAS.<br /><br /> Например, если hello SAS для hello задания является `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, с указанием hello виртуальный каталог называется `mylogblobs`, то расположением журнала hello будет `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.|  
  
Вы можете получить hello URL-адрес ошибки hello и подробных журналов, вызывающему Привет [получения задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операции. Hello журналы доступны после завершения обработки диска hello.  
  
## <a name="log-file-format"></a>Формат файла журнала  
Hello формат у обоих журналов hello же: большой двоичный объект, содержащий XML-описания событий hello, возникших при копировании больших двоичных объектов между hello жестких дисков и счет клиента hello.  
  
Hello подробный журнал содержит полные сведения о состоянии hello hello операции копирования для каждого большого двоичного объекта (для задания импорта) или файла (для задания экспорта), а hello журнал ошибок содержит только hello сведения о больших двоичных объектов или файлов, в которых обнаружены ошибки во время hello Импорт или экспорт заданий.  
  
Далее приведен формат подробного журнала Hello. журнал ошибок Hello имеет hello же структуру, но отфильтрованы успешные операции.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

Hello следующей таблице описываются элементы hello hello файла журнала.  
  
|XML-элемент|Тип|Описание|  
|-----------------|----------|-----------------|  
|`DriveLog`|XML-элемент|Представляет журнал диска.|  
|`Version`|Атрибут, строка|версия формата журнала hello Hello.|  
|`DriveId`|Строка|Здравствуйте, серийный номер диска.|  
|`Status`|Строка|Состояние обработки диска hello. В разделе hello `Drive Status Codes` таблицу ниже для получения дополнительной информации.|  
|`Blob`|Вложенный XML-элемент|Представляет большой двоичный объект.|  
|`Blob/BlobPath`|Строка|Здравствуйте, URI большого двоичного объекта hello.|  
|`Blob/FilePath`|Строка|файл toohello Hello относительный путь на диске hello.|  
|`Blob/Snapshot`|DateTime|версия моментального снимка большого двоичного объекта hello, для задания экспорта только Hello.|  
|`Blob/Length`|Целое число |Общая длина Hello hello большого двоичного объекта в байтах.|  
|`Blob/LastModified`|DateTime|Hello даты и времени последнего изменения большого двоичного объекта hello только задания экспорта.|  
|`Blob/ImportDisposition`|Строка|стратегией большого двоичного объекта hello, импорт только для задания импорта Hello.|  
|`Blob/ImportDisposition/@Status`|Атрибут, строка|состояние Hello hello стратегией импорта.|  
|`PageRangeList`|Вложенный XML-элемент|Представляет список диапазонов страниц для страничного BLOB-объекта.|  
|`PageRange`|XML-элемент|Представляет диапазон страниц.|  
|`PageRange/@Offset`|Атрибут, целое число|Начальное смещение диапазона страниц hello в большом двоичном объекте hello.|  
|`PageRange/@Length`|Атрибут, целое число|Длина в байтах hello диапазона страниц.|  
|`PageRange/@Hash`|Атрибут, строка|Кодировке base16 MD5-хэш диапазона страниц hello.|  
|`PageRange/@Status`|Атрибут, строка|Состояние обработки диапазона страниц hello.|  
|`BlockList`|Вложенный XML-элемент|Представляет список блоков блочного BLOB-объекта.|  
|`Block`|XML-элемент|Представляет блок.|  
|`Block/@Offset`|Атрибут, целое число|Начальное смещение блока hello в большом двоичном объекте hello.|  
|`Block/@Length`|Атрибут, целое число|Длина в байтах блока hello.|  
|`Block/@Id`|Атрибут, строка|Идентификатор блока Hello.|  
|`Block/@Hash`|Атрибут, строка|Кодировке base16 MD5-хэш блока hello.|  
|`Block/@Status`|Атрибут, строка|Состояние обработки блока hello.|  
|`Metadata`|Вложенный XML-элемент|Представляет метаданные hello большого двоичного объекта.|  
|`Metadata/@Status`|Атрибут, строка|Состояние обработки метаданных большого двоичного объекта hello.|  
|`Metadata/GlobalPath`|Строка|Относительный путь toohello глобального файла метаданных.|  
|`Metadata/GlobalPath/@Hash`|Атрибут, строка|Кодировке base16 MD5-хэш hello глобального файла метаданных.|  
|`Metadata/Path`|Строка|Относительный путь к файлу метаданных toohello.|  
|`Metadata/Path/@Hash`|Атрибут, строка|Кодировке base16 MD5-хэш файла метаданных hello.|  
|`Properties`|Вложенный XML-элемент|Представляет свойства большого двоичного объекта hello.|  
|`Properties/@Status`|Атрибут, строка|Состояние обработки свойств большого двоичного объекта hello, например файл не найден, завершена.|  
|`Properties/GlobalPath`|Строка|Относительный путь toohello глобального файла свойств.|  
|`Properties/GlobalPath/@Hash`|Атрибут, строка|Кодировке base16 MD5-хэш файла hello глобальные свойства.|  
|`Properties/Path`|Строка|Файл свойств toohello относительный путь.|  
|`Properties/Path/@Hash`|Атрибут, строка|Кодировке base16 MD5-хэш файла свойств hello.|  
|`Blob/Status`|Строка|Состояние обработки hello большого двоичного объекта.|  
  
# <a name="drive-status-codes"></a>Коды состояний диска  
Hello следующей таблице перечислены коды состояния hello для обработки диска.  
  
|Код состояния|Описание|  
|-----------------|-----------------|  
|`Completed`|диск Hello завершил обработку без ошибок.|  
|`CompletedWithWarnings`|Обработка с предупреждениями в один или несколько больших двоичных объектах в hello стратегией импорта, заданной для больших двоичных объектов hello завершилась Hello диска.|  
|`CompletedWithErrors`|Hello диска завершена с ошибками в одной или нескольких больших двоичных объектов или блоков.|  
|`DiskNotFound`|Диск не найден на диске hello.|  
|`VolumeNotNtfs`|Hello первый том данных на диске hello не в формате NTFS.|  
|`DiskOperationFailed`|Неизвестный сбой при выполнении операций на диске hello.|  
|`BitLockerVolumeNotFound`|Не найден том, зашифрованный с помощью BitLocker.|  
|`BitLockerNotActivated`|BitLocker не включена на томе hello.|  
|`BitLockerProtectorNotFound`|на томе hello Hello числовой предохранитель ключа пароля не существует.|  
|`BitLockerKeyInvalid`|Hello числовому паролю не удается разблокировать том hello.|  
|`BitLockerUnlockVolumeFailed`|Произошла неизвестная ошибка произошла при попытке toounlock hello тома.|  
|`BitLockerFailed`|Произошла неизвестная ошибка при выполнении операций с BitLocker.|  
|`ManifestNameInvalid`|Недопустимое имя файла манифеста Hello.|  
|`ManifestNameTooLong`|указано слишком длинное имя файла манифеста Hello.|  
|`ManifestNotFound`|не найден файл манифеста Hello.|  
|`ManifestAccessDenied`|Файл манифеста toohello доступ запрещен.|  
|`ManifestCorrupted`|Hello поврежден файл манифеста (hello содержимое не совпадает с хэшем).|  
|`ManifestFormatInvalid`|содержимое манифеста Hello не соответствует требуемому формату toohello.|  
|`ManifestDriveIdMismatch`|Здравствуйте, код в файле манифеста hello не соответствует hello одно чтение с диска hello диска.|  
|`ReadManifestFailed`|При чтении из файла манифеста hello произошла ошибка ввода-вывода диска.|  
|`BlobListFormatInvalid`|Hello экспорта списка больших двоичных объектов не соответствует требуемому формату toohello.|  
|`BlobRequestForbidden`|Запрещен доступ toohello BLOB-объектов в учетной записи хранения hello. Это может произойти из-за tooinvalid ключ учетной записи хранилища или SAS контейнера.|  
|`InternalError`|И произошла внутренняя ошибка при обработке диска hello.|  
  
## <a name="blob-status-codes"></a>Коды состояний большого двоичного объекта  
Hello следующей таблице перечислены коды состояния hello для обработки большого двоичного объекта.  
  
|Код состояния|Описание|  
|-----------------|-----------------|  
|`Completed`|большой двоичный объект Hello обработка завершилась без ошибок.|  
|`CompletedWithErrors`|большой двоичный объект Hello завершения обработки ошибок в один или несколько диапазонов страниц или блоков, метаданных или свойств.|  
|`FileNameInvalid`|Недопустимое имя файла Hello.|  
|`FileNameTooLong`|указано слишком длинное имя файла Hello.|  
|`FileNotFound`|Hello файл не найден.|  
|`FileAccessDenied`|Файл toohello доступ запрещен.|  
|`BlobRequestFailed`|Сбой запроса службы BLOB-объектов Hello что tooaccess hello большого двоичного объекта.|  
|`BlobRequestForbidden`|Hello большого двоичного объекта запроса службы tooaccess hello больших двоичных объектов запрещено. Это может произойти из-за tooinvalid ключ учетной записи хранилища или SAS контейнера.|  
|`RenameFailed`|Не удалось toorename hello blob (для задания импорта) или файл hello (для задания экспорта).|  
|`BlobUnexpectedChange`|Непредвиденное изменение произошла с hello больших двоичных объектов (для задания экспорта).|  
|`LeasePresent`|Нет Аренда на большой двоичный объект hello.|  
|`IOFailed`|Диск или сетевой ошибки ввода-вывода произошла при обработке больших двоичных объектов hello.|  
|`Failed`|Неизвестная ошибка при обработке больших двоичных объектов hello.|  
  
## <a name="import-disposition-status-codes"></a>Коды состояний метода обработки импорта  
Hello следующей таблице перечислены коды состояния hello для устранения ошибок стратегии импорта.  
  
|Код состояния|Описание|  
|-----------------|-----------------|  
|`Created`|Hello BLOB-объект был создан.|  
|`Renamed`|Hello большой двоичный объект переименован на переименование стратегии импорта. Hello `Blob/BlobPath` элемент содержит hello URI для hello переименован большого двоичного объекта.|  
|`Skipped`|Hello большой двоичный объект был пропущен в `no-overwrite` стратегией импорта.|  
|`Overwritten`|Hello большой двоичный объект перезаписал существующий большой двоичный объект в `overwrite` стратегией импорта.|  
|`Cancelled`|Предыдущий сбой позволил продолжить обработку стратегии импорта hello.|  
  
## <a name="page-rangeblock-status-codes"></a>Коды состояний диапазона страниц или блока  
Hello следующей таблице перечислены коды состояния hello для обработки диапазона страниц или блока.  
  
|Код состояния|Описание|  
|-----------------|-----------------|  
|`Completed`|Hello диапазон или блок страниц завершил обработку без ошибок.|  
|`Committed`|Hello блок был зафиксирован, но не в hello полного списка блокировок из-за других блоков возникли ошибки или поместить полного списка блокировок не удалась.|  
|`Uncommitted`|Hello блок загружен, но не были зафиксированы.|  
|`Corrupted`|Hello диапазон или блок страниц поврежден (содержимое hello не совпадает с хэшем).|  
|`FileUnexpectedEnd`|Обнаружен непредвиденный конец файла.|  
|`BlobUnexpectedEnd`|Обнаружен непредвиденный конец большого двоичного объекта.|  
|`BlobRequestFailed`|Здравствуйте запроса службы BLOB-объектов tooaccess hello диапазона страниц или блок не удалось.|  
|`IOFailed`|Диск или сетевой ошибки ввода-вывода произошла при обработке hello диапазона или блока страниц.|  
|`Failed`|Неизвестная ошибка при обработке hello диапазона или блока страниц.|  
|`Cancelled`|Предыдущий сбой позволил продолжить обработку hello диапазона или блока страниц.|  
  
## <a name="metadata-status-codes"></a>Коды состояний метаданных  
Hello следующей таблице перечислены коды состояния hello для обработки метаданных большого двоичного объекта.  
  
|Код состояния|Описание|  
|-----------------|-----------------|  
|`Completed`|метаданные Hello обработка завершилась без ошибок.|  
|`FileNameInvalid`|Недопустимое имя файла метаданных Hello.|  
|`FileNameTooLong`|указано слишком длинное имя файла метаданных Hello.|  
|`FileNotFound`|файл метаданных Hello не найден.|  
|`FileAccessDenied`|Файл метаданных toohello доступ запрещен.|  
|`Corrupted`|поврежден файл метаданных Hello (hello содержимое не совпадает с хэшем).|  
|`XmlReadFailed`|содержимое метаданных Hello не соответствует требуемому формату toohello.|  
|`XmlWriteFailed`|Запись метаданных hello ошибка XML.|  
|`BlobRequestFailed`|Сбой запроса службы BLOB-объектов Hello что tooaccess hello метаданных.|  
|`IOFailed`|Произошла ошибка ввода-вывода диска или сети при обработке метаданных hello.|  
|`Failed`|Неизвестная ошибка при обработке метаданных hello.|  
|`Cancelled`|Предыдущий сбой позволил продолжить обработку метаданных hello.|  
  
## <a name="properties-status-codes"></a>Коды состояний свойств  
Hello следующей таблице перечислены коды состояния hello для обработки свойств большого двоичного объекта.  
  
|Код состояния|Описание|  
|-----------------|-----------------|  
|`Completed`|свойства Hello закончена обработка без ошибок.|  
|`FileNameInvalid`|Недопустимое имя файла свойств Hello.|  
|`FileNameTooLong`|указано слишком длинное имя файла свойств Hello.|  
|`FileNotFound`|файл свойств Hello не найден.|  
|`FileAccessDenied`|Файл свойств toohello доступ запрещен.|  
|`Corrupted`|поврежден файл свойств Hello (hello содержимое не совпадает с хэшем).|  
|`XmlReadFailed`|содержимое свойства Hello не соответствует требуемому формату toohello.|  
|`XmlWriteFailed`|Запись свойства hello, ошибка XML.|  
|`BlobRequestFailed`|Сбой запроса службы BLOB-объектов Hello что tooaccess hello свойства.|  
|`IOFailed`|Произошла ошибка ввода-вывода диска или сети при обработке свойств hello.|  
|`Failed`|Неизвестная ошибка при обработке свойств hello.|  
|`Cancelled`|Предыдущий сбой позволил продолжить обработку свойств hello.|  
  
## <a name="sample-logs"></a>Примеры журналов  
Hello ниже приведен пример подробного журнала.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
Ниже приведен соответствующий журнал ошибок Hello.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 Hello журнал ошибок для задания импорта содержит ошибку о ненайденном файле на диске импорта hello. Обратите внимание, что состояние последующих компонентов hello `Cancelled`.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

Hello следующий журнал ошибок задания экспорта указывает, что содержимое большого двоичного объекта hello был успешно записан toohello диска, но что произошла ошибка при экспорте свойства hello большого двоичного объекта.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>Дальнейшие действия
 
* [Справочник по REST API импорта и экспорта службы хранилища](/rest/api/storageimportexport/)
