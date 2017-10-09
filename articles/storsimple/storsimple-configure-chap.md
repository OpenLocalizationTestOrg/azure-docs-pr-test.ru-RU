---
title: "aaaConfigure CHAP для устройства серии StorSimple 8000 | Документы Microsoft"
description: "Описывает, каким образом tooconfigure hello протокол проверки пароля (CHAP) на устройстве StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="f5950-103">Настроить CHAP для устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f5950-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="f5950-104">В этом учебнике описано, как tooconfigure CHAP для устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f5950-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="f5950-105">Hello процедуры, описанной в этой статье относится tooStorSimple серии 8000, а также устройства StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="f5950-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="f5950-106">CHAP — сокращение от Challenge Handshake Authentication Protocol (протокол проверки подлинности на основе вызова).</span><span class="sxs-lookup"><span data-stu-id="f5950-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="f5950-107">Это схему проверки подлинности, используемые для идентификации hello toovalidate серверы удаленных клиентов.</span><span class="sxs-lookup"><span data-stu-id="f5950-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="f5950-108">Проверка Hello строится на общем пароле или секрете.</span><span class="sxs-lookup"><span data-stu-id="f5950-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="f5950-109">Протокол CHAP может быть односторонним (однонаправленным) или двусторонним (двунаправленным).</span><span class="sxs-lookup"><span data-stu-id="f5950-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="f5950-110">При использовании одностороннего CHAP целевой hello проверяет подлинность инициатора.</span><span class="sxs-lookup"><span data-stu-id="f5950-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="f5950-111">Взаимной или обратного CHAP, на hello другой стороны, требует hello цель проверяла подлинности инициатора hello и затем hello инициатор проверял подлинность цели hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="f5950-112">Проверку подлинности инициатора можно реализовать без проверки подлинности целевого устройства.</span><span class="sxs-lookup"><span data-stu-id="f5950-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="f5950-113">Однако проверка подлинности целевого устройства может быть реализована только в том случае, если проверка подлинности инициатора также реализована.</span><span class="sxs-lookup"><span data-stu-id="f5950-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="f5950-114">Как правило рекомендуется использовать безопасности iSCSI tooenhance CHAP.</span><span class="sxs-lookup"><span data-stu-id="f5950-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="f5950-115">Помните, что в настоящее время IPSEC не поддерживается на устройствах StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f5950-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="f5950-116">можно настроить Hello параметры CHAP на устройстве StorSimple hello в hello следующих способов:</span><span class="sxs-lookup"><span data-stu-id="f5950-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="f5950-117">Для однонаправленной или односторонней проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f5950-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="f5950-118">Для двунаправленной (взаимной, или обратной) проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f5950-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="f5950-119">В каждом из этих случаев hello портал для hello устройств и программного обеспечения инициатора iSCSI сервера hello должен toobe настроен.</span><span class="sxs-lookup"><span data-stu-id="f5950-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="f5950-120">Hello подробное описание действий для этой конфигурации описаны в следующих учебника hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="f5950-121">Для однонаправленной или односторонней проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f5950-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="f5950-122">При однонаправленной проверке подлинности целевой hello проверяет подлинность инициатора hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="f5950-123">Эта проверка подлинности требует настройки hello параметров инициатора CHAP на устройстве StorSimple hello и программного обеспечения инициатора узла hello hello iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f5950-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="f5950-124">Здравствуйте, подробное описание процедур для устройства StorSimple и сервера Windows представлено Далее.</span><span class="sxs-lookup"><span data-stu-id="f5950-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="f5950-125">tooconfigure устройства для односторонней проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f5950-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="f5950-126">В классический портал Azure, на hello hello **устройств** щелкните hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f5950-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Инициатор CHAP](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="f5950-128">Прокрутите вниз на этой странице и в hello **инициатора CHAP** раздела:</span><span class="sxs-lookup"><span data-stu-id="f5950-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="f5950-129">Укажите имя пользователя для инициатора CHAP.</span><span class="sxs-lookup"><span data-stu-id="f5950-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="f5950-130">Укажите пароль для инициатора CHAP.</span><span class="sxs-lookup"><span data-stu-id="f5950-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="f5950-131">имя пользователя CHAP Hello должно содержать менее 233 символов.</span><span class="sxs-lookup"><span data-stu-id="f5950-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="f5950-132">Привет CHAP пароль должен содержать от 12 до 16 символов.</span><span class="sxs-lookup"><span data-stu-id="f5950-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="f5950-133">Больше времени, имя пользователя или пароль приведет к сбою проверки подлинности на узле Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="f5950-134">Подтверждение пароля hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-134">Confirm hello password.</span></span>
3. <span data-ttu-id="f5950-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f5950-135">Click **Save**.</span></span> <span data-ttu-id="f5950-136">Появится сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="f5950-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="f5950-137">Нажмите кнопку **ОК** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="f5950-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="f5950-138">сервер tooconfigure односторонней проверки подлинности hello Windows</span><span class="sxs-lookup"><span data-stu-id="f5950-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="f5950-139">На сервере узла Windows hello запустите инициатор iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="f5950-140">В hello **свойства инициатора iSCSI** окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f5950-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="f5950-141">Нажмите кнопку hello **обнаружения** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f5950-141">Click hello **Discovery** tab.</span></span>
      
       ![Свойства инициатора iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="f5950-143">Щелкните **Портал обнаружения**.</span><span class="sxs-lookup"><span data-stu-id="f5950-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="f5950-144">В hello **обнаружить целевой портал** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="f5950-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="f5950-145">Укажите IP-адрес устройства hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="f5950-146">Нажмите кнопку **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="f5950-146">Click **Advanced**.</span></span>
      
       ![Обнаружение целевого портала](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="f5950-148">В hello **Дополнительные параметры** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="f5950-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="f5950-149">Выберите hello **разрешить вход CHAP** флажок.</span><span class="sxs-lookup"><span data-stu-id="f5950-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="f5950-150">В hello **имя** поле, имя пользователя hello питания, указанный для hello инициатора CHAP hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="f5950-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="f5950-151">В hello **секрет целевого объекта** поле, питания hello пароль, указанный для hello инициатора CHAP hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="f5950-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="f5950-152">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f5950-152">Click **OK**.</span></span>
      
       ![Расширенные параметры: общие](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="f5950-154">На hello **цели** вкладка hello **свойства инициатора iSCSI** окне должны отображаться состояние устройства hello как **подключен**.</span><span class="sxs-lookup"><span data-stu-id="f5950-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="f5950-155">Если вы используете устройство StorSimple 1200, каждый том будет подключен как целевое устройство iSCSI, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f5950-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="f5950-156">Таким образом шаги 3 и 4 потребуется toobe повторяется для каждого тома.</span><span class="sxs-lookup"><span data-stu-id="f5950-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![Тома подключены как отдельные целевые устройства.](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="f5950-158">При изменении имени iSCSI hello hello новое имя будет использоваться для новых сеансов iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f5950-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="f5950-159">Новые параметры не будут использоваться для существующих сеансов до выхода из системы и повторного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="f5950-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="f5950-160">Дополнительные сведения о настройке протокола CHAP на сервере узла Windows hello go слишком[Дополнительные соображения](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="f5950-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="f5950-161">Двунаправленная (взаимная, или обратная) проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="f5950-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="f5950-162">При двунаправленной проверке подлинности целевой hello проверяет подлинность инициатора hello и затем hello инициатор должен проверить подлинность целевого hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="f5950-163">Требуется параметров инициатора CHAP hello tooconfigure hello пользователя, а также hello обратного параметры CHAP на устройстве hello и hello узла программного обеспечения инициатора iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f5950-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="f5950-164">Hello следующие процедуры описывают шаги hello tooconfigure взаимной проверки подлинности на устройстве hello и на узле Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="f5950-165">tooconfigure устройства для взаимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f5950-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="f5950-166">В классический портал Azure, на hello hello **устройств** щелкните hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f5950-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Целевое устройство CHAP](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="f5950-168">Прокрутите вниз на этой странице и в hello **цель CHAP** раздела:</span><span class="sxs-lookup"><span data-stu-id="f5950-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="f5950-169">Укажите **Имя пользователя обратного CHAP** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="f5950-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="f5950-170">Укажите **Пароль обратного CHAP** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="f5950-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="f5950-171">Подтверждение пароля hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-171">Confirm hello password.</span></span>
3. <span data-ttu-id="f5950-172">В hello **инициатора CHAP** раздела:</span><span class="sxs-lookup"><span data-stu-id="f5950-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="f5950-173">Укажите **имя пользователя** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="f5950-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="f5950-174">Укажите **пароль** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="f5950-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="f5950-175">Подтверждение пароля hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-175">Confirm hello password.</span></span>
4. <span data-ttu-id="f5950-176">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f5950-176">Click **Save**.</span></span> <span data-ttu-id="f5950-177">Появится сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="f5950-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="f5950-178">Нажмите кнопку **ОК** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="f5950-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="f5950-179">сервер tooconfigure двунаправленной проверки подлинности hello Windows</span><span class="sxs-lookup"><span data-stu-id="f5950-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="f5950-180">На сервере узла Windows hello запустите инициатор iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="f5950-181">В hello **свойства инициатора iSCSI** окно, нажмите кнопку hello **конфигурации** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f5950-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="f5950-182">Щелкните **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="f5950-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="f5950-183">В hello **секрет взаимного CHAP инициатора iSCSI** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="f5950-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="f5950-184">Тип hello **пароль обратного CHAP** , настроенного в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f5950-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="f5950-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f5950-185">Click **OK**.</span></span>
      
       ![Секрет взаимного CHAP инициатора iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="f5950-187">Нажмите кнопку hello **цели** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f5950-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="f5950-188">Нажмите кнопку hello **Connect** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f5950-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="f5950-189">В hello **подключения tooTarget** диалоговое окно, нажмите кнопку **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="f5950-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="f5950-190">В hello **дополнительные свойства** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="f5950-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="f5950-191">Выберите hello **разрешить вход CHAP** флажок.</span><span class="sxs-lookup"><span data-stu-id="f5950-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="f5950-192">В hello **имя** поле, имя пользователя hello питания, указанный для hello инициатора CHAP hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="f5950-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="f5950-193">В hello **секрет целевого объекта** поле, питания hello пароль, указанный для hello инициатора CHAP hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="f5950-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="f5950-194">Выберите hello **выполнить взаимную проверку подлинности** флажок.</span><span class="sxs-lookup"><span data-stu-id="f5950-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Расширенные параметры: взаимная аутентификация](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="f5950-196">Нажмите кнопку **ОК** toocomplete hello CHAP конфигурации</span><span class="sxs-lookup"><span data-stu-id="f5950-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="f5950-197">Дополнительные сведения о настройке протокола CHAP на сервере узла Windows hello go слишком[Дополнительные соображения](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="f5950-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="f5950-198">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="f5950-198">Additional considerations</span></span>
<span data-ttu-id="f5950-199">Hello **быстрое подключение** компонент не поддерживает подключения с включенным CHAP.</span><span class="sxs-lookup"><span data-stu-id="f5950-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="f5950-200">При включении CHAP, убедитесь, что используется hello **Connect** кнопки, которая доступна на hello **цели** целевой tooa tooconnect вкладку.</span><span class="sxs-lookup"><span data-stu-id="f5950-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Подключение tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="f5950-202">В hello **подключения tooTarget** диалоговое окно, представленному, выберите hello **добавить это подключение toohello списку избранных целевых объектов** флажок.</span><span class="sxs-lookup"><span data-stu-id="f5950-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="f5950-203">Это гарантирует, что каждый раз при перезагрузке компьютера hello, попытка toorestore hello подключения toohello избранные конечные объекты iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f5950-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="f5950-204">Ошибки во время настройки</span><span class="sxs-lookup"><span data-stu-id="f5950-204">Errors during configuration</span></span>
<span data-ttu-id="f5950-205">Если настройка CHAP неверен, то, скорее всего, toosee **сбой проверки подлинности** сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="f5950-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="f5950-206">Проверка конфигурации CHAP</span><span class="sxs-lookup"><span data-stu-id="f5950-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="f5950-207">Можно проверить, что используется протокол CHAP, выполнив следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="f5950-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="f5950-208">tooverify настройки CHAP</span><span class="sxs-lookup"><span data-stu-id="f5950-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="f5950-209">Щелкните **Избранные целевые устройства**.</span><span class="sxs-lookup"><span data-stu-id="f5950-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="f5950-210">Выберите целевой hello, для которого включена проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="f5950-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="f5950-211">Щелкните **Сведения**.</span><span class="sxs-lookup"><span data-stu-id="f5950-211">Click **Details**.</span></span>
   
    ![Свойства инициатора iSCSI: целевые устройства](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="f5950-213">В hello **Избранные данные целевого объекта** диалоговое окно, обратите внимание запись hello в hello **проверки подлинности** поля.</span><span class="sxs-lookup"><span data-stu-id="f5950-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="f5950-214">Если настройка hello выполнена успешно, появится название **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="f5950-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Сведения об избранном целевом устройстве](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="f5950-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5950-216">Next steps</span></span>
* <span data-ttu-id="f5950-217">Узнайте больше о [безопасности StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="f5950-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="f5950-218">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f5950-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

