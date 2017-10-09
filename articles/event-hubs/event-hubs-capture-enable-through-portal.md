---
title: "Включение захвата концентраторов событий aaaAzure через портал | Документы Microsoft"
description: "Включите функцию захвата концентраторов событий hello, с помощью портала Azure hello."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>Разрешить отслеживание концентраторов событий с помощью портала Azure hello

Можно настроить записи время hello события концентратора создания с помощью hello [портал Azure](https://portal.azure.com). Вы можете либо tooan данных отслеживания hello Azure [хранилище больших двоичных объектов](https://azure.microsoft.com/services/storage/blobs/) контейнера или tooan [хранилища Озера данных Azure](https://azure.microsoft.com/services/data-lake-store/) учетной записи.

## <a name="capture-data-tooan-azure-storage-account"></a>Учетная запись для записи данных tooan хранилища Azure  

При создании концентратора событий можно включить сбор, щелкнув hello **на** кнопку в hello **создать концентратор событий** портала колонку. Затем укажите учетную запись хранилища и контейнера, нажав кнопку **хранилища Azure** в hello **записи поставщика** поле. Поскольку записи концентраторов событий использует проверку подлинности для службы с хранилищем, toospecify строки подключения хранилища не обязательно. Средство выбора ресурсов Hello автоматически выбирает hello ресурса (URI) для вашей учетной записи. При использовании Azure Resource Manager этот универсальный код ресурса необходимо явным образом указать как строку.

временное окно Hello по умолчанию равно 5 минутам. Hello минимальное значение равно 1, максимальное 15 hello. Hello **размер** окно имеет диапазон от 10 – 500 МБ.

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>Учетная запись для записи данных tooan хранилища Озера данных Azure

tooAzure данных toocapture хранилища Озера данных, создать учетную запись хранилища Озера данных и концентратор событий:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Создание учетной записи и папок Azure Data Lake Store

1. Создать учетную запись хранилища Озера данных, следуя инструкциям hello [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Создать папку в этой учетной записи, следуйте инструкциям hello в hello [создавать папки в учетной записи хранилища Озера данных Azure](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) раздела.
3. В колонке учетной записи хранилища Озера данных hello щелкните **обозреватель данных**.
4. Щелкните **Доступ**.
5. Щелкните **Добавить**.
6. В hello **поиска по имени или по электронной почте** введите **Microsoft.EventHubs** и выберите этот параметр. 
7. Hello **разрешений** появляется вкладка. Задайте разрешения hello, как показано в следующий рисунок hello:

    ![][6]

8. Нажмите кнопку **ОК**.
9. Теперь создайте папку в корневой папке hello путем просмотра toohello целевую папку и щелкните имя папки hello.
10. Щелкните **Доступ**.
11. Щелкните **Добавить**.
12. В hello **поиска по имени или по электронной почте** введите **Microsoft.EventHubs** и выберите этот параметр.
13. Hello **разрешений** появляется вкладка. Задайте разрешения hello, как показано в следующий рисунок hello:

    ![][5]

### <a name="create-an-event-hub"></a>Создание концентратора событий

1. Обратите внимание должен быть этот концентратор событий hello в hello ту же подписку Azure hello хранилища Озера данных Azure, вы только что создали. Концентратор событий hello создать, щелкнув hello **на** под заголовком **захвата** в hello **создать концентратор событий** портала колонку. 
2. В hello **создать концентратор событий** портала колонки, **хранилища Озера данных Azure** из hello **записи поставщика** поле.
3. В **Выбор хранилища Озера данных**, укажите hello учетной записи хранилища Озера данных, созданную ранее, а hello **пути Озера данных** введите данные hello путь toohello папку, созданную.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Добавление или настройка функции записи для существующего концентратора событий

Функцию записи можно настроить в существующих концентраторах событий, расположенных в соответствующих пространствах имен. tooenable записи на существующий концентратор событий, или toochange параметры отслеживания, щелкните приветствия имен tooload hello **Essentials** колонке нажмите кнопку hello концентратора событий, для которого вы хотите tooenable или изменить приветствия системы отслеживания. Наконец, нажмите кнопку hello **свойства** раздел Привет открыть колонку и затем измените параметры захвата hello, как показано на следующих иллюстрациях hello:

### <a name="azure-blob-storage"></a>Хранилище больших двоичных объектов Azure

![][2]

### <a name="azure-data-lake-store"></a>Хранилище озера данных Azure

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>Дальнейшие действия

Запись концентраторов событий можно также настроить с помощью шаблонов Azure Resource Manager. См. дополнительные сведения [о включении записи с помощью шаблона Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).
