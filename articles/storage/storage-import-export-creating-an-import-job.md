---
title: "aaaCreate задание импорта для импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как toocreate импортировать hello службы импорта и экспорта Microsoft Azure."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Создание задания импорта для hello службы импорта и экспорта Azure

Создание задания импорта службы импорта и экспорта Microsoft Azure hello, с использованием hello REST API включает hello следующие шаги.

-   Подготовка дисков с hello средство импорта и экспорта Azure.

-   Получение hello расположение toowhich tooship hello диска.

-   Создание задания импорта hello.

-   Доставка hello дисков tooMicrosoft через перевозчика.

-   Обновление задания импорта hello с hello доставки сведений.

 В разделе [tooBlob hello импорта и экспорта Microsoft Azure службы tooTransfer данные хранилища с помощью](storage-import-export-service.md) Обзор службы импорта и экспорта hello и учебник, в котором показано, как toouse hello [портал Azure](https://portal.azure.com/) toocreate и управления импортом и экспортом заданий.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Подготовка дисков с hello средство импорта и экспорта Azure

Hello действия tooprepare дисков для задания импорта hello же того, необходимо создать портал hello jobvia hello или через hello REST API.

Ниже вкратце описана процедура подготовки диска. См. toohello [Справочник ExportTool импорта Azure](storage-import-export-tool-how-to-v1.md) Полные инструкции по установке. Вы можете загрузить средство импорта и экспорта Azure hello [здесь](http://go.microsoft.com/fwlink/?LinkID=301900).

Подготовка дисков включает следующие действия:

-   Идентификационные данные toobe hello импортированы.

-   Определение hello целевых больших двоичных объектов в хранилище Windows Azure.

-   С помощью средства импорта и экспорта Azure toocopy hello вашей tooone данных или несколько жестких дисков.

 Hello средство импорта и экспорта Azure также создаст файл манифеста для каждого из устройств hello при его подготовке. Этот файл манифеста содержит:

-   Перечисление всех hello файлы, предназначенные для отправки и сопоставления hello tooblobs эти файлы.

-   Контрольные суммы сегментов каждого файла hello.

-   Сведения о hello метаданных и свойств tooassociate каждого большого двоичного объекта.

-   Список tootake действие hello если большой двоичный объект, передаваемая имеет hello одинаковые имена, как существующий большой двоичный объект в контейнере hello. Возможные параметры: a) перезапись большого двоичного объекта hello с файлом hello, б) сохранение hello существующий большой двоичный объект и пропустить при передаче файла hello, c), добавьте имя toohello суффикса не конфликтует с другими файлами.

## <a name="obtaining-your-shipping-location"></a>Получение расположения для отправки

Перед созданием задания импорта, необходимо tooobtain название организации и адрес, вызывающий hello [перечисление расположений](/rest/api/storageimportexport/listlocations) операции. Операция `List Locations` вернет список расположений и почтовых адресов. Можно выбрать расположение из hello вернул список и отправить свой адрес toothat жестких дисков. Можно также использовать hello `Get Location` адрес в определенное место доставки непосредственно hello tooobtain операции.

 Выполните действия hello ниже расположение доставки tooobtain hello.

-   Определите имя hello hello расположение учетной записи хранилища. Это значение можно найти в разделе hello **расположение** на учетную запись хранения hello **мониторинга** в hello портал Azure или запросить с помощью hello службы управления API-операции [получения хранилища Свойства учетной записи](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Получить расположение hello, доступных tooprocess этой учетной записи хранения, вызывающему Привет `Get Location` операции.

-   Если hello `AlternateLocations` свойство расположения hello содержит зоной hello, то это хорошо toouse это расположение. В противном случае вызов hello `Get Location` операцию, указав одно из альтернативных расположений hello. исходное расположение Hello временно закрыт для обслуживания.

## <a name="creating-hello-import-job"></a>Создание задания импорта hello
Задание импорта hello toocreate, вызов hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операции. Вам потребуется hello tooprovide следующую информацию:

-   Имя задания hello.

-   Имя учетной записи хранения Hello.

-   Здравствуйте, название организации, полученное из предыдущего шага hello доставки.

-   тип задания (импорт);

-   Hello обратный адрес, где hello диски будут отправлены после завершения задания импорта hello.

-   Список дисков в задании hello Hello. Для каждого диска необходимо включить следующую информацию, что был получен во время подготовки диска hello hello:

    -   Идентификатор диска Hello

    -   ключ BitLocker Hello

    -   относительный путь файла манифеста Hello на жестком диске hello

    -   Хэш MD5 файла манифеста в кодировке Base16 Hello

## <a name="shipping-your-drives"></a>Отправка дисков
Необходимо отправить свой адрес toohello дисков, полученное из предыдущего шага hello, и вы должны предоставить hello службы импорта и экспорта с hello отслеживания номер пакета hello.

> [!NOTE]
>  Диски необходимо отправить через поддерживаемого перевозчика, который предоставит номер для отслеживания посылки.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>Обновление задания импорта hello с данных о доставке
После того как вы номер для отслеживания, вызовите hello [обновления свойств задания](/api/storageimportexport/jobs#Jobs_Update) имя оператора, hello идентификационный номер задания hello и hello номер счета перевозчика для возврата доставки доставки hello tooupdate операции. Кроме того, можно дополнительно указать номер hello дисков, а также дата отгрузки hello.

## <a name="next-steps"></a>Дальнейшие действия

* [С помощью REST API службы импорта и экспорта hello](storage-import-export-using-the-rest-api.md)
