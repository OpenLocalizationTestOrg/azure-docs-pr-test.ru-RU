---
title: "aaaManage политик резервного копирования StorSimple | Документы Microsoft"
description: "Объясняется, как можно использовать toocreate службы диспетчера StorSimple hello и управлять вручную резервных копий, расписания резервного копирования и хранения резервных копий."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a>Использование политик резервного копирования toomanage службы диспетчера StorSimple hello
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Обзор
В этом учебнике описано, как toouse hello в службе StorSimple Manager **политики резервного копирования** toocontrol процессы резервного копирования и хранения резервных копий для тома StorSimple страницы. В нем также рассматриваются как toocomplete резервной копии вручную.

Hello **политики резервного копирования** страница позволяет toomanage политики резервного копирования и расписание локальных и облачных моментальных снимков. (Политики резервного копирования не используется tooconfigure расписания резервного копирования и хранения резервной копии для набора томов). Политики резервного копирования, обеспечивают tootake моментальный снимок нескольких томах одновременно. Это означает, что hello резервных копий, созданных политику резервного копирования копии на момент аварийного завершения. Эта страница содержит hello политики резервного копирования, их типы, hello связанные тома, количество сохраняемых резервных копий hello и hello параметр tooenable эти политики.

Hello **политики резервного копирования** также можно toofilter hello существующие политики резервного копирования по одному или нескольким hello следующие поля:

* **Имя политики** — hello имя, связанное с политикой hello. Hello различные типы политик:
  
  * Запланированные политики, которые явно создаются пользователем hello.
  * Автоматические политики, которые создаются при включении hello резервное копирование по умолчанию для этого параметра том на время создания тома hello. Эти политики именуются как VolumeName_Default, где имя тома относится имя toohello hello тома StorSimple, настроенного пользователем hello в hello классический портал Azure. Hello автоматические политики выполняют ежедневные облачные моментальные снимки, начиная с временем устройства 22:30.
  * Импорт политики, которые были созданы в hello диспетчера моментальных снимков StorSimple. Они имеют метки, описывающие узел диспетчера моментальных снимков StorSimple hello, hello политики были импортированы.
* **Тома** — hello тома, связанные с политикой hello. Все тома hello, связанные с политикой резервного копирования, группируются вместе при создании резервных копий.
* **Последней успешной архивации** — hello даты и времени hello последней успешной резервной копии, сделанной с этой политикой.
* **Следующая резервная копия** — hello Дата и время hello следующего запланированного резервного копирования, будет инициировано этой политикой.
* **Расписания** — число расписаний, связанных с политикой резервного копирования hello hello.

Hello часто используемых операций, которые можно выполнять на этой странице перечислены.

* Добавление политики архивации 
* Добавление или изменение расписания 
* Удаление политики архивации 
* Создание резервной копии вручную 
* Создание пользовательской политики архивации с несколькими томами и расписаниями 

## <a name="add-a-backup-policy"></a>Добавление политики архивации
Добавьте расписание tooautomatically политику резервного копирования резервных копий. Выполните следующие шаги в hello Azure классического портала tooadd политику резервного копирования для устройства StorSimple hello. После добавления hello политики, можно задать расписание (см. [добавить или изменить расписание](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

![Доступно видео](./media/storsimple-manage-backup-policies/Video_icon.png) **Доступно видео**

Нажмите кнопку toowatch видео, в котором показано, как политика, архивации toocreate локальной или облачной [здесь](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).

## <a name="add-or-modify-a-schedule"></a>Добавление или изменение расписания
Можно добавить или изменить расписание, существует политика резервного копирования вложенного tooan на устройстве StorSimple. Выполните следующие шаги в hello Azure классического портала tooadd hello или изменение расписания.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a>Удаление политики архивации
Выполните следующие действия, описанные в hello Azure классического портала toodelete политику резервного копирования на устройстве StorSimple hello.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Создание резервной копии вручную
Выполните следующие шаги в hello Azure классического портала toocreate по требованию (вручную) резервного копирования для одного тома hello.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Создание пользовательской политики архивации с несколькими томами и расписаниями
Выполните следующие шаги в hello Azure классического портала toocreate настраиваемую политику резервного копирования с несколькими томами и расписаниями hello.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).

