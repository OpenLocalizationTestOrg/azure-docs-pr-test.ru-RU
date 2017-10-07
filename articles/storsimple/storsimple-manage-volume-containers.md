---
title: "aaaManage контейнерами томов StorSimple | Документы Microsoft"
description: "Объясняется, как можно использовать hello StorSimple Manager контейнеры томов службы страницы tooadd, изменить или удалить контейнер томов."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a>Используйте контейнеры томов StorSimple toomanage службы hello диспетчера StorSimple
## <a name="overview"></a>Обзор
Этот учебник объясняется, как toouse hello toocreate службы StorSimple Manager и Управление контейнерами томов StorSimple.

Контейнер томов в устройстве Microsoft Azure StorSimple содержит один или несколько томов, которые совместно используют учетную запись хранения, функцию шифрования и параметры потребления полосы пропускания. В устройстве может быть несколько контейнеров томов для всех его томов. 

Контейнер томов обладает hello следующие атрибуты:

* **Тома** — hello многоуровневого или локально закрепленного тома StorSimple, содержащиеся в контейнере томов hello. Контейнер томов может содержать too256 томов StorSimple.
* **Шифрование** — ключ шифрования, который можно задать для каждого контейнера томов. Этот ключ используется для шифрования данных hello, который отправляется в облаке toohello устройства StorSimple. Ключ оборонному стандарту AES-256 бит используется с вводимым пользователем ключом hello. toosecure данных, рекомендуется всегда применять шифрование в облаке.
* **Учетная запись хранения** — hello учетной записи хранилища, связанный tooyour поставщика услуг облачного хранилища. Все тома hello, находящихся в контейнере томов совместно использовать эту учетную запись хранения. Можно выбрать учетную запись из существующего списка или создайте новую учетную запись, при создании контейнера томов hello и затем укажите учетные данные для hello доступа для этой учетной записи.
* **Пропускная способность облака** — hello пропускной способностью, используемой hello устройства при отправке облака toohello hello данные с устройства hello. При настройке контейнера можно ограничить пропускную способность, указав значение от 1 до 1000 Мбит/с. Если вы хотите tooconsume устройства hello всю доступную пропускную способность, задайте tooUnlimited этого поля. Можно также создать и применить пропускной способности tooallocate шаблона пропускной способности на основе расписания.

![Страница контейнеров томов](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

Это следующие процедуры показывают, как toouse hello StorSimple **контейнеры томов** hello toocomplete страницы, следующие общие операции:

* Добавление контейнера томов 
* Изменение контейнера томов 
* Удаление контейнера томов 

## <a name="add-a-volume-container"></a>Добавление контейнера томов
Выполните следующие шаги tooadd контейнер томов hello.

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a>Изменение контейнера томов
Выполните следующие шаги toomodify контейнер томов hello.

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Удаление контейнера томов
Контейнер томов содержит тома. Его можно удалить только в том случае, если сначала удаляются все содержащиеся в нем тома hello. Выполните следующие шаги toodelete контейнер томов hello.

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше об [управлении томами StorSimple](storsimple-manage-volumes.md). 
* Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).

