---
title: "Изменение пароля администратора устройства виртуального массива StorSimple | Документация Майкрософт"
description: "В статье описано, как с помощью портала Azure или веб-интерфейса виртуального массива StorSimple изменить пароль администратора устройства."
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
ms.openlocfilehash: 260a23003d705e6598da8c51bb5a96f2539a0014
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="67755-103">Изменение пароля администратора для устройства виртуального массива StorSimple с помощью диспетчера устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="67755-103">Change the StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="67755-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="67755-104">Overview</span></span>

<span data-ttu-id="67755-105">При использовании интерфейса Windows PowerShell для доступа к виртуальному массиву StorSimple вам потребуется ввести пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="67755-105">When you use the Windows PowerShell interface to access the StorSimple Virtual Array, you are required to enter a device administrator password.</span></span> <span data-ttu-id="67755-106">Если подготовка и запуск устройства StorSimple выполняются впервые, по умолчанию используется пароль *Password1*.</span><span class="sxs-lookup"><span data-stu-id="67755-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span></span> <span data-ttu-id="67755-107">Для защиты ваших данных пароль по умолчанию становится недействительным после первого входа в систему и его необходимо будет изменить.</span><span class="sxs-lookup"><span data-stu-id="67755-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span></span>

<span data-ttu-id="67755-108">После развертывания устройства в рабочей среде можно в любой момент изменить пароль администратора устройства с помощью локального веб-интерфейса или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="67755-108">You can also use either the local web UI or the Azure portal to change the device administrator password at any time after the device is deployed in your production environment.</span></span> <span data-ttu-id="67755-109">Каждая из этих процедур описана в статье.</span><span class="sxs-lookup"><span data-stu-id="67755-109">Each of these procedures is described in this article.</span></span>

 ![Колонка "Устройства"](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-the-azure-portal-to-change-the-password"></a><span data-ttu-id="67755-111">Изменение пароля с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="67755-111">Use the Azure portal to change the password</span></span>

<span data-ttu-id="67755-112">Чтобы изменить пароль администратора устройства с помощью портала Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="67755-112">Perform the following steps to change the device administrator password through the Azure portal.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-azure-portal"></a><span data-ttu-id="67755-113">Изменение пароля администратора устройства с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="67755-113">To change the device administrator password via the Azure portal</span></span>

1. <span data-ttu-id="67755-114">На главной странице служб выберите службу, дважды щелкните ее имя, а затем в разделе **Управление** щелкните **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="67755-114">On the service landing page, select your service, double-click the service name, and then within the **Management** section, click **Devices**.</span></span> <span data-ttu-id="67755-115">Откроется колонка **Устройства**, в которой перечислены все устройства виртуального массива StorSimple.</span><span class="sxs-lookup"><span data-stu-id="67755-115">This opens the **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="67755-116">В колонке **Устройства** дважды щелкните устройство, для которого нужно изменить пароль.</span><span class="sxs-lookup"><span data-stu-id="67755-116">In the **Devices** blade, double-click the device that requires a change of password.</span></span>

3. <span data-ttu-id="67755-117">В колонке **Параметры** для устройства щелкните **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="67755-117">In the **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="67755-118">В колонке **Параметры безопасности** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="67755-118">In the **Security Settings** blade, do the following:</span></span>
   
   1. <span data-ttu-id="67755-119">Прокрутите экран вниз, к разделу **Пароль администратора устройства** .</span><span class="sxs-lookup"><span data-stu-id="67755-119">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="67755-120">Укажите пароль администратора длиной от 8 до 15 символов.</span><span class="sxs-lookup"><span data-stu-id="67755-120">Provide an administrator password that contains from 8 to 15 characters.</span></span>
   2. <span data-ttu-id="67755-121">Подтвердите пароль.</span><span class="sxs-lookup"><span data-stu-id="67755-121">Confirm the password.</span></span>
   3. <span data-ttu-id="67755-122">Щелкните **Сохранить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="67755-122">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="67755-123">Теперь пароль администратора устройства изменен.</span><span class="sxs-lookup"><span data-stu-id="67755-123">The device administrator password is now updated.</span></span> <span data-ttu-id="67755-124">Этот новый пароль можно использовать для локального доступа к устройству.</span><span class="sxs-lookup"><span data-stu-id="67755-124">You can use this modified password to access the device locally.</span></span>

![Колонка "Параметры безопасности"](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-the-local-web-ui-to-change-the-password"></a><span data-ttu-id="67755-126">Изменение пароля с помощью локального веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="67755-126">Use the local web UI to change the password</span></span>

<span data-ttu-id="67755-127">Чтобы изменить пароль администратора устройства с помощью локального веб-интерфейса, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="67755-127">Perform the following steps to change the device administrator password through the local web UI.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a><span data-ttu-id="67755-128">Изменение пароля администратора устройства с помощью локального веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="67755-128">To change the device administrator password via the local web UI</span></span>

1. <span data-ttu-id="67755-129">В локальном веб-интерфейсе щелкните **Обслуживание** > **Изменение пароля** для своего устройства.</span><span class="sxs-lookup"><span data-stu-id="67755-129">In the local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![изменить password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="67755-131">Введите **текущий пароль**.</span><span class="sxs-lookup"><span data-stu-id="67755-131">Enter the **Current password**.</span></span>
3. <span data-ttu-id="67755-132">Укажите **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="67755-132">Provide a **New Password**.</span></span> <span data-ttu-id="67755-133">Пароль должен содержать не менее 8 символов.</span><span class="sxs-lookup"><span data-stu-id="67755-133">The password must be at least 8 characters long.</span></span> <span data-ttu-id="67755-134">При этом он должен содержать как минимум три вида символов из следующих четырех: прописные буквы, строчные буквы, цифры и специальные символы.</span><span class="sxs-lookup"><span data-stu-id="67755-134">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="67755-135">Обратите внимание, что текущий пароль не должен совпадать с 24 предыдущими.</span><span class="sxs-lookup"><span data-stu-id="67755-135">Note that your password cannot be the same as the last 24 passwords.</span></span>
4. <span data-ttu-id="67755-136">Повторно введите пароль для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="67755-136">Reenter the password to confirm it.</span></span>
   
    ![изменить password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="67755-138">В нижней части страницы нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="67755-138">At the bottom of the page, click **Apply**.</span></span> <span data-ttu-id="67755-139">Теперь новый пароль применен.</span><span class="sxs-lookup"><span data-stu-id="67755-139">The new password is now applied.</span></span> <span data-ttu-id="67755-140">Если изменение пароля не произошло, появится следующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="67755-140">If the password change is not successful, you see the following error:</span></span>
   
    ![ошибочный пароль](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="67755-142">После успешного обновления пароля вы получите соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="67755-142">After the password is successfully updated, you are notified.</span></span> <span data-ttu-id="67755-143">Теперь новый пароль можно использовать для локального доступа к устройству.</span><span class="sxs-lookup"><span data-stu-id="67755-143">You can then use this modified password to access the device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="67755-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67755-144">Next steps</span></span>
<span data-ttu-id="67755-145">Узнайте, как [администрировать виртуальный массив StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="67755-145">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

