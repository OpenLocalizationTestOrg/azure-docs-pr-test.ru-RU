---
title: "записи управления доступом aaaManage в StorSimple | Документы Microsoft"
description: "Описывает принципы управления доступом toouse записей toodetermine (ACR), какие узлы могут подключаться tooa тома на устройстве StorSimple hello."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Использовать записи управления доступом toomanage службы диспетчера StorSimple hello

## <a name="overview"></a>Обзор
Записи управления доступом (ACR) позволяют toospecify, какие узлы могут подключаться tooa тома на устройстве StorSimple hello. Записи контроля доступа задаются tooa томов и содержать hello iSCSI (IQN) полные имена узлов hello. Когда узел пытается tooconnect tooa тома, устройство hello проверяет hello контроля доступа, связанной с этим томом hello IQN-имя и если имеется соответствие, то hello подключения. Здравствуйте, записи управления доступом в hello **конфигурации** части колонки службы вашего устройства StorSimple отобразить все записи управления доступом hello с hello соответствующее IQN узлов hello.

В этом учебнике описано следующие общие задачи, связанные с ACR hello:

* Добавление записи контроля доступа
* Изменение записи контроля доступа
* Удаление записи контроля доступа

> [!IMPORTANT]
> * При назначении томе tooa контроля доступа, будьте внимательны, что тома hello не имеет доступа к одновременно более чем одного некластеризованного узла, так как это может повредить том hello.
> * При удалении записи управления Доступом из тома, убедитесь, что соответствующий узел, hello не имеет доступа к hello тома, так как hello удаление может привести к прерыванию чтения и записи.

## <a name="get-hello-iqn"></a>Получение IQN hello

Выполните следующие шаги tooget hello IQN узла Windows под управлением Windows Server 2012 hello.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>Добавление записи контроля доступа
Использовать hello **конфигурации** раздел в колонке службы tooadd записи контроля доступа для hello устройства StorSimple. Как правило, одной записи контроля доступа соответствует один том.

Выполните hello, выполнив шаги tooadd записи управления Доступом.

#### <a name="tooadd-an-acr"></a>tooadd запись контроля доступа

1. Go tooyour службы диспетчера StorSimple устройство, дважды щелкните hello имя службы и затем в hello **конфигурации** щелкните **записи управления доступом**.
2. В hello **записи управления доступом** колонка, щелкните **+ добавить запись контроля доступа**.

    ![Щелкните "Добавить запись контроля доступа"](./media/storsimple-8000-manage-acrs/createacr1.png)

3. В hello **Добавление ACR** колонке hello следующие действия:

    1. Введите имя для записи контроля доступа.
    
    2. Укажите имя hello IQN узла Windows Server в поле **имя инициатора (IQN) iSCSI**.

    3. Нажмите кнопку **добавить** toocreate hello контроля доступа.

        ![Щелкните "Добавить запись контроля доступа"](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  Hello недавно добавленный ACR будут отображаться в табличном списке записей контроля доступа hello.

    ![Щелкните "Добавить запись контроля доступа"](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>Изменение записи контроля доступа
Использовать hello **конфигурации** раздел в колонке службы tooedit записи контроля доступа для hello устройства StorSimple.

> [!NOTE]
> Мы рекомендуем изменять только те записи, которые сейчас не используются. tooedit записи управления Доступом, ассоциированный с томом, который используется в настоящий момент, сначала нужно hello том вне сети.

Выполните hello, выполнив шаги tooedit записи управления Доступом.

#### <a name="tooedit-an-access-control-record"></a>tooedit записи управления доступом
1.  Go tooyour службы диспетчера StorSimple устройство, дважды щелкните hello имя службы и затем в hello **конфигурации** щелкните **записи управления доступом**.

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/createacr1.png)

2. В hello табличном списке записей управления доступом hello, щелкните и выберите записи контроля доступа, что вы хотите toomodify hello.

    ![Изменение записей контроля доступа](./media/storsimple-8000-manage-acrs/editacr1.png)

3. В hello **редактирование записи контроля доступа** колонки, укажите другой узел соответствующий tooanother IQN.

    ![Изменение записей контроля доступа](./media/storsimple-8000-manage-acrs/editacr2.png)

4. Щелкните **Сохранить**. При появлении запроса на подтверждение нажмите кнопку **Да**. 

    ![Изменение записей контроля доступа](./media/storsimple-8000-manage-acrs/editacr3.png)

5. Уведомляются при обновлении hello контроля доступа. Табличный список Hello также обновляет tooreflect hello изменений.

   
## <a name="delete-an-access-control-record"></a>Удаление записи контроля доступа
Использовать hello **конфигурации** раздел в колонке службы toodelete записи контроля доступа для hello устройства StorSimple.

> [!NOTE]
> Можно удалять только те записи контроля доступа, которые в настоящее время не используются. toodelete записи управления Доступом, ассоциированный с томом, который используется в настоящий момент, сначала нужно hello том вне сети.

Выполните hello, выполнив шаги toodelete записи управления доступом.

#### <a name="toodelete-an-access-control-record"></a>toodelete записи управления доступом
1.  Go tooyour службы диспетчера StorSimple устройство, дважды щелкните hello имя службы и затем в hello **конфигурации** щелкните **записи управления доступом**.

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/createacr1.png)

2. В hello табличном списке записей управления доступом hello, щелкните и выберите записи контроля доступа, что вы хотите toodelete hello.

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Щелкните правой кнопкой мыши tooinvoke hello контекстное меню и выберите **удалить**.

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. При появлении запроса на подтверждение, просмотрите сведения hello и нажмите кнопку **удалить**.

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. Вы будете оповещены, после завершения удаления hello. Табличный список Hello является обновленные tooreflect hello удаления.

    ![Go tooaccess управления записей](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше об [управлении томами StorSimple](storsimple-8000-manage-volumes-u2.md).
* Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-8000-manager-service-administration.md).

