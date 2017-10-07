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
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="d0e48-103">Использовать toochange службы диспетчера StorSimple устройство hello паролей StorSimple</span><span class="sxs-lookup"><span data-stu-id="d0e48-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="d0e48-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d0e48-104">Overview</span></span>
<span data-ttu-id="d0e48-105">Здравствуйте, портал Azure **параметры устройства** параметр содержит все параметры устройств "hello", его необходимо настроить на устройстве StorSimple, которое управляется службой диспетчера StorSimple устройство.</span><span class="sxs-lookup"><span data-stu-id="d0e48-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="d0e48-106">В этом учебнике описано, как можно использовать hello **безопасности** под флажком **параметры устройства** toochange администратору устройства или пароль диспетчера моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d0e48-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="d0e48-107">Пароль администратора устройства hello изменений</span><span class="sxs-lookup"><span data-stu-id="d0e48-107">Change hello device administrator password</span></span>
<span data-ttu-id="d0e48-108">При использовании устройства StorSimple hello tooaccess интерфейса Windows PowerShell, их необходимо tooenter пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="d0e48-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="d0e48-109">После регистрации первого устройства StorSimple hello со службой hello пароль по умолчанию для этого интерфейса — *Password1*.</span><span class="sxs-lookup"><span data-stu-id="d0e48-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="d0e48-110">Hello безопасность данных, не требуется toochange этот пароль при hello конце процесса регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="d0e48-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="d0e48-111">Не удается выйти из процесса регистрации hello без изменения пароля.</span><span class="sxs-lookup"><span data-stu-id="d0e48-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="d0e48-112">Дополнительные сведения см. в разделе [Step 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="d0e48-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="d0e48-113">Hello пароль, который был сначала установлен через интерфейс Windows PowerShell hello во время регистрации могут быть изменены через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d0e48-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="d0e48-114">Выполните следующий пароль администратора устройства hello toochange действия hello.</span><span class="sxs-lookup"><span data-stu-id="d0e48-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="d0e48-115">пароль администратора устройства toochange hello</span><span class="sxs-lookup"><span data-stu-id="d0e48-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="d0e48-116">Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**.</span><span class="sxs-lookup"><span data-stu-id="d0e48-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="d0e48-117">Hello табличный список устройств, выберите и щелкните устройство hello, пароль которого планируется toochange.</span><span class="sxs-lookup"><span data-stu-id="d0e48-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="d0e48-118">В hello **параметры** колонке go слишком**параметры устройства > безопасности**.</span><span class="sxs-lookup"><span data-stu-id="d0e48-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="d0e48-119">В hello **параметры безопасности** колонка, щелкните **пароль** toochange hello пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="d0e48-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="d0e48-120">В hello **пароль** колонки, введите пароль администратора, содержащий от 8 too15 символов.</span><span class="sxs-lookup"><span data-stu-id="d0e48-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="d0e48-121">пароль Hello должны представлять собой сочетание 3 или более верхнем регистре, нижнем регистре, цифры и специальные символы.</span><span class="sxs-lookup"><span data-stu-id="d0e48-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="d0e48-122">Подтверждение пароля hello.</span><span class="sxs-lookup"><span data-stu-id="d0e48-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="d0e48-123">Щелкните **Сохранить** и при появлении запроса на подтверждение щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="d0e48-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="d0e48-124">пароль администратора устройства Hello теперь должен быть обновлен.</span><span class="sxs-lookup"><span data-stu-id="d0e48-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="d0e48-125">Можно использовать этот интерфейс Windows PowerShell hello tooaccess измененный пароль.</span><span class="sxs-lookup"><span data-stu-id="d0e48-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="d0e48-126">Установка пароля диспетчера моментальных снимков StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="d0e48-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="d0e48-127">Программное обеспечение диспетчера моментального снимка StorSimple находится на узле Windows и позволяет администраторам резервные копии toomanage устройства StorSimple в форме hello локальных и облачных моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="d0e48-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="d0e48-128">При настройке устройства диспетчера моментальных снимков StorSimple, вам будет предложено tooprovide hello tooauthenticate устройства IP адрес и пароль устройства хранения.</span><span class="sxs-lookup"><span data-stu-id="d0e48-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="d0e48-129">Можно задать или изменить пароль hello для диспетчера моментальных снимков StorSimple через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d0e48-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="d0e48-130">Выполните следующие шаги tooset hello или измените пароль StorSimple Snapshot Manager hello.</span><span class="sxs-lookup"><span data-stu-id="d0e48-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="d0e48-131">пароль диспетчера моментальных снимков StorSimple tooset hello</span><span class="sxs-lookup"><span data-stu-id="d0e48-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="d0e48-132">Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**.</span><span class="sxs-lookup"><span data-stu-id="d0e48-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="d0e48-133">Hello табличный список устройств, выберите и щелкните hello устройства диспетчера моментальных снимков StorSimple, пароль которого требуется tooset или изменить.</span><span class="sxs-lookup"><span data-stu-id="d0e48-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="d0e48-134">В hello **параметры** колонке go слишком**параметры устройства > безопасности**.</span><span class="sxs-lookup"><span data-stu-id="d0e48-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="d0e48-135">В hello **параметры безопасности** колонка, щелкните **пароль** tooset или измените пароль StorSimple Snapshot Manager hello.</span><span class="sxs-lookup"><span data-stu-id="d0e48-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="d0e48-136">В hello **пароль** колонки, введите пароль, состоящий из 14 или 15 символов.</span><span class="sxs-lookup"><span data-stu-id="d0e48-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="d0e48-137">Убедитесь, что этот пароль hello содержит сочетание 3 или верхнем регистре, нижнем регистре, цифры и специальные знаки.</span><span class="sxs-lookup"><span data-stu-id="d0e48-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="d0e48-138">Подтверждение пароля hello.</span><span class="sxs-lookup"><span data-stu-id="d0e48-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="d0e48-139">Щелкните **Сохранить** и при появлении запроса на подтверждение щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="d0e48-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="d0e48-140">пароль диспетчера моментальных снимков StorSimple Hello теперь должен быть обновлен.</span><span class="sxs-lookup"><span data-stu-id="d0e48-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0e48-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0e48-141">Next steps</span></span>
* <span data-ttu-id="d0e48-142">Узнайте больше о [безопасности StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="d0e48-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="d0e48-143">Узнайте больше об [изменении конфигурации устройства](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="d0e48-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="d0e48-144">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d0e48-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

