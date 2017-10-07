---
title: "aaaChange StorSimple паролей | Документы Microsoft"
description: "Описывает, каким образом toouse hello toochange службы диспетчера StorSimple устройство ваши пароли администратора диспетчера моментальных снимков StorSimple и устройства."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>Использовать toochange службы диспетчера StorSimple устройство hello паролей StorSimple

## <a name="overview"></a>Обзор
Здравствуйте, портал Azure **параметры устройства** параметр содержит все параметры устройств "hello", его необходимо настроить на устройстве StorSimple, которое управляется службой диспетчера StorSimple устройство. В этом учебнике описано, как можно использовать hello **безопасности** под флажком **параметры устройства** toochange администратору устройства или пароль диспетчера моментальных снимков StorSimple.

## <a name="change-hello-device-administrator-password"></a>Пароль администратора устройства hello изменений
При использовании устройства StorSimple hello tooaccess интерфейса Windows PowerShell, их необходимо tooenter пароль администратора устройства. После регистрации первого устройства StorSimple hello со службой hello пароль по умолчанию для этого интерфейса — *Password1*. Hello безопасность данных, не требуется toochange этот пароль при hello конце процесса регистрации hello. Не удается выйти из процесса регистрации hello без изменения пароля. Дополнительные сведения см. в разделе [Step 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Hello пароль, который был сначала установлен через интерфейс Windows PowerShell hello во время регистрации могут быть изменены через портал Azure hello. Выполните следующий пароль администратора устройства hello toochange действия hello.

#### <a name="toochange-hello-device-administrator-password"></a>пароль администратора устройства toochange hello
1. Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**.

2. Hello табличный список устройств, выберите и щелкните устройство hello, пароль которого планируется toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. В hello **параметры** колонке go слишком**параметры устройства > безопасности**.

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. В hello **параметры безопасности** колонка, щелкните **пароль** toochange hello пароль администратора.

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. В hello **пароль** колонки, введите пароль администратора, содержащий от 8 too15 символов. пароль Hello должны представлять собой сочетание 3 или более верхнем регистре, нижнем регистре, цифры и специальные символы.

6. Подтверждение пароля hello.

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. Щелкните **Сохранить** и при появлении запроса на подтверждение щелкните **Да**.

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

пароль администратора устройства Hello теперь должен быть обновлен. Можно использовать этот интерфейс Windows PowerShell hello tooaccess измененный пароль.

## <a name="set-hello-storsimple-snapshot-manager-password"></a>Установка пароля диспетчера моментальных снимков StorSimple hello
Программное обеспечение диспетчера моментального снимка StorSimple находится на узле Windows и позволяет администраторам резервные копии toomanage устройства StorSimple в форме hello локальных и облачных моментальных снимков.

При настройке устройства диспетчера моментальных снимков StorSimple, вам будет предложено tooprovide hello tooauthenticate устройства IP адрес и пароль устройства хранения.

Можно задать или изменить пароль hello для диспетчера моментальных снимков StorSimple через портал Azure hello. Выполните следующие шаги tooset hello или измените пароль StorSimple Snapshot Manager hello.

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>пароль диспетчера моментальных снимков StorSimple tooset hello
1. Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**.

2. Hello табличный список устройств, выберите и щелкните hello устройства диспетчера моментальных снимков StorSimple, пароль которого требуется tooset или изменить.

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. В hello **параметры** колонке go слишком**параметры устройства > безопасности**.

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. В hello **параметры безопасности** колонка, щелкните **пароль** tooset или измените пароль StorSimple Snapshot Manager hello.

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. В hello **пароль** колонки, введите пароль, состоящий из 14 или 15 символов. Убедитесь, что этот пароль hello содержит сочетание 3 или верхнем регистре, нижнем регистре, цифры и специальные знаки.

6. Подтверждение пароля hello.

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. Щелкните **Сохранить** и при появлении запроса на подтверждение щелкните **Да**.

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

пароль диспетчера моментальных снимков StorSimple Hello теперь должен быть обновлен.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше о [безопасности StorSimple](storsimple-8000-security.md).
* Узнайте больше об [изменении конфигурации устройства](storsimple-8000-modify-device-config.md).
* Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

