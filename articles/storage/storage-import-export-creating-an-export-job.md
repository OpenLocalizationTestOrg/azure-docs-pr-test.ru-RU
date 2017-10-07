---
title: "aaaCreate Экспорт заданий импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как toocreate Экспорт задания для hello службы импорта и экспорта Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Создание задания экспорта для hello службы импорта и экспорта Azure
Создание задания экспорта службы импорта и экспорта Microsoft Azure hello, с использованием hello REST API включает hello следующие шаги.

-   При выборе hello tooexport больших двоичных объектов.

-   получение адреса для отправки;

-   Создание задания экспорта hello.

-   Доставка вашей tooMicrosoft пустые диски через перевозчика.

-   Обновление задания экспорта hello с hello данных пакета.

-   Получение hello дисков от Майкрософт.

 В разделе [tooBlob hello импорта и экспорта Windows Azure службы tooTransfer данные хранилища с помощью](storage-import-export-service.md) Обзор службы импорта и экспорта hello и учебник, в котором показано, как toouse hello [портал Azure](https://portal.azure.com/) toocreate и управления импортом и экспортом заданий.

## <a name="selecting-blobs-tooexport"></a>При выборе tooexport больших двоичных объектов
 toocreate задание экспорта, необходимо будет tooprovide список больших двоичных объектов, что нужно tooexport из вашей учетной записи хранилища. Существует несколько способов tooselect toobe экспортировать большие двоичные объекты:

-   Tooselect относительного пути можно использовать один большой двоичный объект и все ее моментальные снимки.

-   Можно использовать один BLOB-объект без его мгновенных снимков tooselect относительного пути.

-   Можно использовать путь относительный больших двоичных объектов и tooselect времени моментальных снимков одного моментального снимка.

-   Все большие двоичные объекты и моментальные снимки можно использовать tooselect префикс BLOB-объекта с префиксом hello.

-   Можно экспортировать все большие двоичные объекты и моментальные снимки в учетной записи хранения hello.

 Дополнительные сведения об указании больших двоичных объектов tooexport, см. в разделе hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операции.

## <a name="obtaining-your-shipping-location"></a>Получение расположения для отправки
Перед созданием задания экспорта, необходимо tooobtain название организации и адрес, вызывающий hello [получить расположение](https://portal.azure.com) или [перечисление расположений](/rest/api/storageimportexport/listlocations) операции. Операция `List Locations` вернет список расположений и почтовых адресов. Можно выбрать расположение из hello вернул список и отправить свой адрес toothat жестких дисков. Можно также использовать hello `Get Location` адрес в определенное место доставки непосредственно hello tooobtain операции.

Выполните действия hello ниже расположение доставки tooobtain hello.

-   Определите имя hello hello расположение учетной записи хранилища. Это значение можно найти в разделе hello **расположение** на учетную запись хранения hello **мониторинга** в классическом hello портала или запросить с помощью hello службы управления API-операции [получить Свойства учетной записи хранения](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Получить расположение hello, которые доступны tooprocess этой учетной записи хранения, вызывающему Привет `Get Location` операции.

-   Если hello `AlternateLocations` свойство расположения hello содержит зоной hello, то это хорошо toouse это расположение. В противном случае вызов hello `Get Location` операцию, указав одно из альтернативных расположений hello. исходное расположение Hello временно закрыт для обслуживания.

## <a name="creating-hello-export-job"></a>Создание задания экспорта hello
 задания экспорта toocreate hello hello вызовов [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операции. Вам потребуется hello tooprovide следующую информацию:

-   Имя задания hello.

-   Имя учетной записи хранения Hello.

-   Здравствуйте, название организации, полученное на предыдущем шаге hello доставки.

-   тип задания (экспорт);

-   Hello обратный адрес, где hello диски будут отправлены после завершения задания экспорта hello.

-   экспортировать список больших двоичных объектов (или префиксов больших двоичных объектов) toobe Hello.

## <a name="shipping-your-drives"></a>Отправка дисков
 Далее используйте hello средство импорта и экспорта Azure toodetermine hello количество дисков требуется toosend, в зависимости от hello больших двоичных объектов, выбранных toobe экспортированы и hello размер диска. В разделе hello [Справочник средство импорта и экспорта Azure](storage-import-export-tool-how-to-v1.md) подробные сведения.

 Пакет hello диски в один пакет и их отправке toohello адресу, полученному hello выше шаг. Обратите внимание, номер пакета для следующего шага hello отслеживания hello.

> [!NOTE]
>  Диски необходимо отправить через поддерживаемого перевозчика, который предоставит номер для отслеживания посылки.

## <a name="updating-hello-export-job-with-your-package-information"></a>Обновление задания экспорта hello с указанием данных пакета
 После того как вы номер для отслеживания, вызовите hello [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) tooupdated hello перевозчика имя операции и номер для hello задания отслеживания. При необходимости можно указать количество дисков, обратный адрес hello и дата отгрузки hello также hello.

## <a name="receiving-hello-package"></a>Получение пакета hello
 После обработки задания экспорта ваши диски будут возвращены tooyou с вашими зашифрованными данными. Можно извлечь ключ BitLocker hello для каждого из устройств hello, вызывающему Привет [получения задания](/rest/api/storageimportexport/jobs#Jobs_Get) операции. Затем можно разблокировать диск hello, с помощью ключа hello. файл манифеста диска Hello на каждом диске содержит hello список файлов на диске hello, а также исходный адрес большого двоичного объекта hello для каждого файла.

## <a name="next-steps"></a>Дальнейшие действия

* [С помощью REST API службы импорта и экспорта hello](storage-import-export-using-the-rest-api.md)
