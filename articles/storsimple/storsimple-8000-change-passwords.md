---
title: "Изменение паролей StorSimple | Документация Майкрософт"
description: "В этой статье показано, как использовать службу диспетчера устройств StorSimple для изменения паролей Snapshot Manager и администратора устройств StorSimple."
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
ms.openlocfilehash: 7762f8499c67672f0a2ffed99e98baea4c940fa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-change-your-storsimple-passwords"></a><span data-ttu-id="16c44-103">Изменение паролей StorSimple с помощью службы диспетчера устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="16c44-103">Use the StorSimple Device Manager service to change your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="16c44-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="16c44-104">Overview</span></span>
<span data-ttu-id="16c44-105">В разделе **Параметры устройства** на портале Azure указаны все параметры, которые можно настроить на устройстве StorSimple, контролируемом службой диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="16c44-105">The Azure portal **Device settings** option contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="16c44-106">В этом руководстве показано, как использовать элемент **Безопасность** в разделе **Параметры устройства**, чтобы изменить в StorSimple пароль администратора устройства или пароль Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="16c44-106">This tutorial explains how you can use the **Security** option under **Device settings** to change your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-the-device-administrator-password"></a><span data-ttu-id="16c44-107">Изменение пароля администратора устройства</span><span class="sxs-lookup"><span data-stu-id="16c44-107">Change the device administrator password</span></span>
<span data-ttu-id="16c44-108">При использовании интерфейса Windows PowerShell для доступа к устройству StorSimple вам потребуется ввести пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="16c44-108">When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="16c44-109">После регистрации первого устройства StorSimple в службе пароль по умолчанию для этого интерфейса — *Password1*.</span><span class="sxs-lookup"><span data-stu-id="16c44-109">When the first StorSimple device is registered with a service, the default password for this interface is *Password1*.</span></span> <span data-ttu-id="16c44-110">Для обеспечения безопасности ваших данных необходимо изменить этот пароль в конце регистрации.</span><span class="sxs-lookup"><span data-stu-id="16c44-110">For the security of your data, you are required to change this password at the end of the registration process.</span></span> <span data-ttu-id="16c44-111">Закончить регистрацию, не изменив пароль, невозможно.</span><span class="sxs-lookup"><span data-stu-id="16c44-111">You cannot exit from the registration process without changing this password.</span></span> <span data-ttu-id="16c44-112">Дополнительные сведения см. в разделе [Шаг 3. Настройка и регистрация устройства средствами Windows PowerShell для StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="16c44-112">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="16c44-113">Пароль, который устанавливается через интерфейс Windows PowerShell во время регистрации, можно изменить позднее на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="16c44-113">The password that was first set through the Windows PowerShell interface during registration can be changed later via the Azure portal.</span></span> <span data-ttu-id="16c44-114">Чтобы изменить пароль администратора устройства, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="16c44-114">Perform the following steps to change the device administrator password.</span></span>

#### <a name="to-change-the-device-administrator-password"></a><span data-ttu-id="16c44-115">Изменение пароля администратора устройства</span><span class="sxs-lookup"><span data-stu-id="16c44-115">To change the device administrator password</span></span>
1. <span data-ttu-id="16c44-116">В службе диспетчера устройств StorSimple выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="16c44-116">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="16c44-117">В табличном списке устройств выберите и щелкните устройство, для которого требуется изменить пароль.</span><span class="sxs-lookup"><span data-stu-id="16c44-117">From the tabular listing of devices, select and click the device whose password you intend to change.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="16c44-118">В колонке **Параметры** выберите **Параметры устройства > Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="16c44-118">In the **Settings** blade, go to **Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="16c44-119">В колонке **Параметры безопасности** щелкните **Пароль**, чтобы изменить пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="16c44-119">In the **Security settings** blade, click **Password** to change the device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="16c44-120">В колонке **Пароль** введите пароль администратора длиной от 8 до 15 символов.</span><span class="sxs-lookup"><span data-stu-id="16c44-120">In the **Password** blade, provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="16c44-121">Пароль должен содержать не менее 3 букв в верхнем и нижнем регистре, цифр и специальных символов.</span><span class="sxs-lookup"><span data-stu-id="16c44-121">The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="16c44-122">Подтвердите пароль.</span><span class="sxs-lookup"><span data-stu-id="16c44-122">Confirm the password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="16c44-123">Щелкните **Сохранить** и при появлении запроса на подтверждение щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="16c44-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="16c44-124">Теперь пароль администратора устройства изменен.</span><span class="sxs-lookup"><span data-stu-id="16c44-124">The device administrator password should now be updated.</span></span> <span data-ttu-id="16c44-125">Этот новый пароль можно использовать для доступа к интерфейсу Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16c44-125">You can use this modified password to access the Windows PowerShell interface.</span></span>

## <a name="set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="16c44-126">Настройка пароля Snapshot Manager для StorSimple</span><span class="sxs-lookup"><span data-stu-id="16c44-126">Set the StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="16c44-127">Программное обеспечение диспетчера моментальных снимков StorSimple находится на узле Windows и позволяет администраторам управлять созданием резервных копий для устройства StorSimple в виде локальных и облачных моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="16c44-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.</span></span>

<span data-ttu-id="16c44-128">При настройке устройства в диспетчере моментальных снимков StorSimple вас попросят указать IP-адрес и пароль устройства для проверки подлинности устройства для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="16c44-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device.</span></span>

<span data-ttu-id="16c44-129">Вы можете задать или изменить пароль Snapshot Manager для StorSimple через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="16c44-129">You can set or change the password for StorSimple Snapshot Manager via the Azure portal.</span></span> <span data-ttu-id="16c44-130">Чтобы задать или изменить пароль Snapshot Manager для StorSimple, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="16c44-130">Perform the following steps to set or change the StorSimple Snapshot Manager password.</span></span>

#### <a name="to-set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="16c44-131">Настройка пароля Snapshot Manager для StorSimple</span><span class="sxs-lookup"><span data-stu-id="16c44-131">To set the StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="16c44-132">В службе диспетчера устройств StorSimple выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="16c44-132">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="16c44-133">В табличном списке устройств выберите и щелкните устройство StorSimple, для которого требуется изменить пароль Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="16c44-133">From the tabular listing of devices, select and click the device whose StorSimple Snapshot Manager password you intend to set or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="16c44-134">В колонке **Параметры** выберите **Параметры устройства > Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="16c44-134">In the **Settings** blade, go to **Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="16c44-135">В колонке **Параметры безопасности** щелкните **Пароль**, чтобы задать или изменить пароль Snapshot Manager для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="16c44-135">In the **Security settings** blade, click **Password** to set or change the StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="16c44-136">В колонке **Пароль** введите пароль длиной 14 или 15 символов.</span><span class="sxs-lookup"><span data-stu-id="16c44-136">In the **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="16c44-137">Убедитесь в том, что пароль состоит не менее чем из 3 букв в верхнем и нижнем регистре, цифр и специальных символов.</span><span class="sxs-lookup"><span data-stu-id="16c44-137">Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="16c44-138">Подтвердите пароль.</span><span class="sxs-lookup"><span data-stu-id="16c44-138">Confirm the password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="16c44-139">Щелкните **Сохранить** и при появлении запроса на подтверждение щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="16c44-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="16c44-140">Теперь пароль диспетчера моментальных снимков StorSimple должен быть обновлен.</span><span class="sxs-lookup"><span data-stu-id="16c44-140">The StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c44-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16c44-141">Next steps</span></span>
* <span data-ttu-id="16c44-142">Узнайте больше о [безопасности StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="16c44-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="16c44-143">Узнайте больше об [изменении конфигурации устройства](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="16c44-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="16c44-144">Узнайте больше об [использовании службы диспетчера устройств StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="16c44-144">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

