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
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="b9f5d-103">Измените пароль администратора устройства StorSimple Virtual Array hello через диспетчер устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="b9f5d-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="b9f5d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b9f5d-104">Overview</span></span>

<span data-ttu-id="b9f5d-105">При использовании tooaccess интерфейс Windows PowerShell hello hello StorSimple Virtual Array, требуется tooenter пароль администратора устройства.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="b9f5d-106">Устройство StorSimple hello сначала подготовленная и запущен, пароль по умолчанию hello — *Password1*.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="b9f5d-107">Для hello безопасность данных, пароль по умолчанию hello истечения срока действия приветствия при первом входе и вы являются обязательным toochange этот пароль.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="b9f5d-108">Также можно использовать либо hello локального web пользовательского интерфейса или hello Azure портала toochange hello пароль администратора устройства в любое время после развертывания hello устройства в вашей рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="b9f5d-109">Каждая из этих процедур описана в статье.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-109">Each of these procedures is described in this article.</span></span>

 ![Колонка "Устройства"](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="b9f5d-111">Используйте пароль hello Azure портала toochange hello</span><span class="sxs-lookup"><span data-stu-id="b9f5d-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="b9f5d-112">Выполните следующие шаги toochange hello пароль администратора через портал Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="b9f5d-113">пароль администратора устройства toochange hello через портал Azure hello</span><span class="sxs-lookup"><span data-stu-id="b9f5d-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="b9f5d-114">На целевой странице службы hello, выберите службу, дважды щелкните hello имя службы и затем в hello **управления** щелкните **устройств**.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="b9f5d-115">При этом откроется hello **устройств** колонки, в которой перечислены все устройства StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="b9f5d-116">В hello **устройств** колонки, дважды щелкните устройство hello, которое требует изменения пароля.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="b9f5d-117">В hello **параметры** колонку для устройства, нажмите кнопку **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="b9f5d-118">В hello **параметры безопасности** колонке hello следующие:</span><span class="sxs-lookup"><span data-stu-id="b9f5d-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="b9f5d-119">Прокрутите вниз toohello **пароль администратора устройства** раздела.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="b9f5d-120">Введите пароль администратора, содержащий от 8 too15 символов.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="b9f5d-121">Подтверждение пароля hello.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="b9f5d-122">Нажмите кнопку **Сохранить** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="b9f5d-123">пароль администратора устройства Hello обновлены.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="b9f5d-124">Это устройство hello tooaccess измененный пароль можно использовать локально.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-124">You can use this modified password tooaccess hello device locally.</span></span>

![Колонка "Параметры безопасности"](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="b9f5d-126">Используйте hello локального web пользовательского интерфейса toochange hello пароль</span><span class="sxs-lookup"><span data-stu-id="b9f5d-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="b9f5d-127">Выполните следующие шаги toochange hello пароль администратора через hello локального пользовательского веб-интерфейса hello.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="b9f5d-128">пароль администратора устройства toochange hello через hello локального пользовательского веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="b9f5d-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="b9f5d-129">В hello локальный веб-Интерфейс, щелкните **обслуживания** > **смены пароля** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![изменить password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="b9f5d-131">Введите hello **текущий пароль**.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="b9f5d-132">Укажите **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-132">Provide a **New Password**.</span></span> <span data-ttu-id="b9f5d-133">Hello пароль должен быть по крайней мере 8 символов.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="b9f5d-134">Он должен содержать 3 из 4 следующих hello: верхнем регистре, нижнем регистре, цифры и специальные символы.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="b9f5d-135">Обратите внимание, что пароль не может быть hello так же, как hello последние 24 пароля.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="b9f5d-136">Повторно введите пароль tooconfirm hello его.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-136">Reenter hello password tooconfirm it.</span></span>
   
    ![изменить password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="b9f5d-138">Внизу hello страницы приветствия щелкните **применить**.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="b9f5d-139">Теперь применяется новый пароль Hello.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-139">hello new password is now applied.</span></span> <span data-ttu-id="b9f5d-140">При смене пароля hello не удалось, появится следующая ошибка hello:</span><span class="sxs-lookup"><span data-stu-id="b9f5d-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![ошибочный пароль](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="b9f5d-142">После успешного обновления hello пароля пользователь получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="b9f5d-143">Затем можно использовать это устройство hello tooaccess измененный пароль локально.</span><span class="sxs-lookup"><span data-stu-id="b9f5d-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b9f5d-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9f5d-144">Next steps</span></span>
<span data-ttu-id="b9f5d-145">Узнайте, каким образом слишком[администрирования виртуального массива StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="b9f5d-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

