---
title: "пароль администратора устройства StorSimple Virtual Array aaaChange | Документы Microsoft"
description: "Описывает, каким образом toouse либо hello портала Azure или StorSimple Virtual Array toochange пользовательского интерфейса web hello пароль администратора устройства."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>Измените пароль администратора устройства StorSimple Virtual Array hello через диспетчер устройств StorSimple

## <a name="overview"></a>Обзор

При использовании tooaccess интерфейс Windows PowerShell hello hello StorSimple Virtual Array, требуется tooenter пароль администратора устройства. Устройство StorSimple hello сначала подготовленная и запущен, пароль по умолчанию hello — *Password1*. Для hello безопасность данных, пароль по умолчанию hello истечения срока действия приветствия при первом входе и вы являются обязательным toochange этот пароль.

Также можно использовать либо hello локального web пользовательского интерфейса или hello Azure портала toochange hello пароль администратора устройства в любое время после развертывания hello устройства в вашей рабочей среде. Каждая из этих процедур описана в статье.

 ![Колонка "Устройства"](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a>Используйте пароль hello Azure портала toochange hello

Выполните следующие шаги toochange hello пароль администратора через портал Azure hello hello.

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a>пароль администратора устройства toochange hello через портал Azure hello

1. На целевой странице службы hello, выберите службу, дважды щелкните hello имя службы и затем в hello **управления** щелкните **устройств**. При этом откроется hello **устройств** колонки, в которой перечислены все устройства StorSimple Virtual Array.

2. В hello **устройств** колонки, дважды щелкните устройство hello, которое требует изменения пароля.

3. В hello **параметры** колонку для устройства, нажмите кнопку **безопасности**.

4. В hello **параметры безопасности** колонке hello следующие:
   
   1. Прокрутите вниз toohello **пароль администратора устройства** раздела. Введите пароль администратора, содержащий от 8 too15 символов.
   2. Подтверждение пароля hello.
   3. Нажмите кнопку **Сохранить** hello верхней части колонки hello.

пароль администратора устройства Hello обновлены. Это устройство hello tooaccess измененный пароль можно использовать локально.

![Колонка "Параметры безопасности"](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a>Используйте hello локального web пользовательского интерфейса toochange hello пароль

Выполните следующие шаги toochange hello пароль администратора через hello локального пользовательского веб-интерфейса hello.

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a>пароль администратора устройства toochange hello через hello локального пользовательского веб-интерфейса

1. В hello локальный веб-Интерфейс, щелкните **обслуживания** > **смены пароля** для вашего устройства.
   
    ![изменить password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. Введите hello **текущий пароль**.
3. Укажите **новый пароль**. Hello пароль должен быть по крайней мере 8 символов. Он должен содержать 3 из 4 следующих hello: верхнем регистре, нижнем регистре, цифры и специальные символы.
   
    Обратите внимание, что пароль не может быть hello так же, как hello последние 24 пароля.
4. Повторно введите пароль tooconfirm hello его.
   
    ![изменить password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. Внизу hello страницы приветствия щелкните **применить**. Теперь применяется новый пароль Hello. При смене пароля hello не удалось, появится следующая ошибка hello:
   
    ![ошибочный пароль](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    После успешного обновления hello пароля пользователь получает уведомление. Затем можно использовать это устройство hello tooaccess измененный пароль локально.


## <a name="next-steps"></a>Дальнейшие действия
Узнайте, каким образом слишком[администрирования виртуального массива StorSimple](storsimple-ova-web-ui-admin.md).

