---
title: "aaaManage контейнерами томов StorSimple на устройства серии StorSimple 8000 hello | Документы Microsoft"
description: "Объясняется, как можно использовать диспетчер устройств StorSimple контейнеры томов службы страницы tooadd, изменить или удалить контейнер томов hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Используйте контейнеры томов StorSimple toomanage службы hello диспетчер устройств StorSimple

## <a name="overview"></a>Обзор
Этот учебник объясняется, как toouse hello toocreate службы диспетчера StorSimple устройств и Управление контейнерами томов StorSimple.

Контейнер томов в устройстве Microsoft Azure StorSimple содержит один или несколько томов, которые совместно используют учетную запись хранения, функцию шифрования и параметры потребления полосы пропускания. В устройстве может быть несколько контейнеров томов для всех его томов. 

Контейнер томов обладает hello следующие атрибуты:

* **Тома** — hello многоуровневого или локально закрепленного тома StorSimple, содержащиеся в контейнере томов hello. 
* **Шифрование** — ключ шифрования, который можно задать для каждого контейнера томов. Этот ключ используется для шифрования данных hello, который отправляется в облаке toohello устройства StorSimple. Ключ оборонному стандарту AES-256 бит используется с вводимым пользователем ключом hello. toosecure данных, рекомендуется всегда применять шифрование в облаке.
* **Учетная запись хранения** — hello учетной записи хранилища Azure, — это данные, используемые toostore hello. Все тома hello, находящихся в контейнере томов совместно использовать эту учетную запись хранения. Можно выбрать учетную запись из существующего списка или создайте новую учетную запись, при создании контейнера томов hello и затем укажите учетные данные для hello доступа для этой учетной записи.
* **Пропускная способность облака** — hello пропускной способностью, используемой hello устройства при отправке облака toohello hello данные с устройства hello. При создании контейнера можно ограничить пропускную способность, указав значение от 1 до 1000 Мбит/с. Hello устройства tooconsume всю доступную пропускную способность, установите это поле слишком**неограниченное количество**. Можно также создать и применить пропускной способности tooallocate шаблона пропускной способности на основе расписания.

Hello следующих процедурах объясняется, как toouse hello StorSimple **контейнеры томов** hello toocomplete колонке следующие общие операции:

* Добавить контейнер томов
* Изменение контейнера томов
* Удаление контейнера томов

## <a name="add-a-volume-container"></a>Добавить контейнер томов
Выполните следующие шаги tooadd контейнер томов hello.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>Изменение контейнера томов
Выполните следующие шаги toomodify контейнер томов hello.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Удаление контейнера томов
Контейнер томов содержит тома. Его можно удалить только в том случае, если сначала удаляются все содержащиеся в нем тома hello. Выполните следующие шаги toodelete контейнер томов hello.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше об [управлении томами StorSimple](storsimple-8000-manage-volumes-u2.md). 
* Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

