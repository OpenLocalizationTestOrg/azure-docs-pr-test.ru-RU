---
title: "aaaChange пароли через диспетчер устройств StorSimple | Документы Microsoft"
description: "Описывает, каким образом toouse hello toochange службы диспетчера StorSimple ваши пароли администратора диспетчера моментальных снимков StorSimple и устройства."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a>Использовать toochange службы диспетчера StorSimple hello паролей StorSimple
## <a name="overview"></a>Обзор
Здравствуйте, классический портал Azure **Настройка** страница содержит все параметры устройства hello, его необходимо настроить на устройстве StorSimple, которое управляется службой диспетчера StorSimple. В этом учебнике описано, как можно использовать hello **Настройка** страница toochange администратору устройства или пароль диспетчера моментальных снимков StorSimple.

## <a name="change-hello-device-administrator-password"></a>Пароль администратора устройства hello изменений
При использовании устройства StorSimple hello tooaccess интерфейса Windows PowerShell, их необходимо tooenter пароль администратора устройства. После регистрации первого устройства StorSimple hello со службой hello пароль по умолчанию для этого интерфейса — *Password1*. Hello безопасность данных, не требуется toochange этот пароль при hello конце процесса регистрации hello. Не удается выйти из процесса регистрации hello без изменения пароля. Дополнительные сведения см. в разделе [Step 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Hello пароль, который был сначала установлен через интерфейс Windows PowerShell hello во время регистрации может быть изменен через hello классический портал Azure. Выполните следующий пароль администратора устройства hello toochange действия hello.

#### <a name="toochange-hello-device-administrator-password"></a>пароль администратора устройства toochange hello
1. Hello классического портала щелкните **устройств** > **Настройка** для вашего устройства.
2. Прокрутите вниз toohello **пароль администратора устройства** раздела. Введите пароль администратора, содержащий от 8 too15 символов. пароль Hello должны представлять собой сочетание 3 или более верхнем регистре, нижнем регистре, цифры и специальные символы.
3. Подтверждение пароля hello.
4. Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.

пароль администратора устройства Hello теперь должен быть обновлен. Можно использовать этот интерфейс Windows PowerShell hello tooaccess измененный пароль.

## <a name="change-hello-storsimple-snapshot-manager-password"></a>Измените пароль StorSimple Snapshot Manager hello
Программное обеспечение диспетчера моментального снимка StorSimple находится на узле Windows и позволяет администраторам резервные копии toomanage устройства StorSimple в форме hello локальных и облачных моментальных снимков.

При настройке устройства диспетчера моментальных снимков StorSimple, вам будет предложено tooprovide hello tooauthenticate устройства IP адрес и пароль устройства хранения. Этот пароль изначально настраивается через интерфейс Windows PowerShell hello. Дополнительные сведения см. в разделе [Step 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Hello пароль, который был сначала установлен через интерфейс Windows PowerShell hello во время регистрации может быть изменен через hello классического портала. Выполните следующий пароль диспетчера моментальных снимков StorSimple hello toochange действия hello.

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a>пароль диспетчера моментальных снимков StorSimple toochange hello
1. Hello классического портала щелкните **устройств** > **Настройка** для вашего устройства.
2. Прокрутите вниз toohello **диспетчера моментальных снимков StorSimple** раздела. Введите пароль длиной 14–15 символов. Убедитесь, что этот пароль hello содержит сочетание 3 или верхнем регистре, нижнем регистре, цифры и специальные знаки.
3. Подтверждение пароля hello.
4. Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.

пароль диспетчера моментальных снимков StorSimple Hello теперь должен быть обновлен.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше о [безопасности StorSimple](storsimple-security.md).
* Узнайте больше об [изменении конфигурации устройства](storsimple-modify-device-config.md).
* Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).

