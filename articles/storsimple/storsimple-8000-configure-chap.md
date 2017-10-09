---
title: "aaaConfigure CHAP для устройства серии StorSimple 8000 | Документы Microsoft"
description: "Описывает, каким образом tooconfigure hello протокол проверки пароля (CHAP) на устройстве StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="6b7ec-103">Настроить CHAP для устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="6b7ec-104">В этом учебнике описано, как tooconfigure CHAP для устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="6b7ec-105">Hello процедуры, описанной в этой статье относится устройствами серии 8000 tooStorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="6b7ec-106">CHAP — сокращение от Challenge Handshake Authentication Protocol (протокол проверки подлинности на основе вызова).</span><span class="sxs-lookup"><span data-stu-id="6b7ec-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="6b7ec-107">Это схему проверки подлинности, используемые для идентификации hello toovalidate серверы удаленных клиентов.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="6b7ec-108">Проверка Hello строится на общем пароле или секрете.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="6b7ec-109">Протокол CHAP может быть односторонним (однонаправленным) или двусторонним (двунаправленным).</span><span class="sxs-lookup"><span data-stu-id="6b7ec-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="6b7ec-110">Один из способов CHAP — когда целевой hello проверяет подлинность инициатора.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="6b7ec-111">В взаимной или обратного CHAP целевой объект hello проверяет подлинность инициатора hello и затем hello инициатор должен проверить подлинность целевого hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="6b7ec-112">Проверку подлинности инициатора можно реализовать без проверки подлинности целевого устройства.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="6b7ec-113">Однако проверка подлинности целевого устройства может быть реализована только в том случае, если проверка подлинности инициатора также реализована.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="6b7ec-114">Как правило рекомендуется использовать безопасности iSCSI tooenhance CHAP.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="6b7ec-115">Помните, что в настоящее время IPSEC не поддерживается на устройствах StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="6b7ec-116">можно настроить Hello параметры CHAP на устройстве StorSimple hello в hello следующих способов:</span><span class="sxs-lookup"><span data-stu-id="6b7ec-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="6b7ec-117">Для однонаправленной или односторонней проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6b7ec-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="6b7ec-118">Для двунаправленной (взаимной, или обратной) проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6b7ec-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="6b7ec-119">В каждом из этих случаев hello портал для hello устройств и программного обеспечения инициатора iSCSI сервера hello должен toobe настроен.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="6b7ec-120">Hello подробное описание действий для этой конфигурации описаны в следующих учебника hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="6b7ec-121">Для однонаправленной или односторонней проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6b7ec-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="6b7ec-122">При однонаправленной проверке подлинности целевой hello проверяет подлинность инициатора hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="6b7ec-123">Эта проверка подлинности требует настройки hello параметров инициатора CHAP на устройстве StorSimple hello и программного обеспечения инициатора узла hello hello iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="6b7ec-124">Здравствуйте, подробное описание процедур для устройства StorSimple и сервера Windows представлено Далее.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="6b7ec-125">tooconfigure устройства для односторонней проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6b7ec-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="6b7ec-126">В hello портал Azure перейдите tooyour службы диспетчера StorSimple устройство.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="6b7ec-127">Нажмите кнопку **устройств** щелкните устройство, нужно tooconfigure CHAP и выберите для.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="6b7ec-128">Go слишком**параметры устройства > безопасности**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="6b7ec-129">В hello **параметры безопасности** колонка, щелкните **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Инициатор CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="6b7ec-131">В hello **CHAP** колонке и в hello **инициатора CHAP** раздела:</span><span class="sxs-lookup"><span data-stu-id="6b7ec-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="6b7ec-132">Укажите имя пользователя для инициатора CHAP.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="6b7ec-133">Укажите пароль для инициатора CHAP.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="6b7ec-134">имя пользователя CHAP Hello должно содержать менее 233 символов.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="6b7ec-135">Привет CHAP пароль должен содержать от 12 до 16 символов.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="6b7ec-136">Больше времени, имя пользователя или пароль приводит к сбою проверки подлинности на узле Windows hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="6b7ec-137">Подтверждение пароля hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-137">Confirm hello password.</span></span>

       ![Инициатор CHAP](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="6b7ec-139">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-139">Click **Save**.</span></span> <span data-ttu-id="6b7ec-140">Вы увидите сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-140">A confirmation message is displayed.</span></span> <span data-ttu-id="6b7ec-141">Нажмите кнопку **ОК** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="6b7ec-142">сервер tooconfigure односторонней проверки подлинности hello Windows</span><span class="sxs-lookup"><span data-stu-id="6b7ec-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="6b7ec-143">На сервере узла Windows hello запустите инициатор iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="6b7ec-144">В hello **свойства инициатора iSCSI** окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6b7ec-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="6b7ec-145">Нажмите кнопку hello **обнаружения** вкладки.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-145">Click hello **Discovery** tab.</span></span>
      
       ![Свойства инициатора iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="6b7ec-147">Щелкните **Портал обнаружения**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="6b7ec-148">В hello **обнаружить целевой портал** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="6b7ec-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="6b7ec-149">Укажите IP-адрес устройства hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="6b7ec-150">Нажмите кнопку **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-150">Click **Advanced**.</span></span>
      
       ![Обнаружение целевого портала](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="6b7ec-152">В hello **Дополнительные параметры** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="6b7ec-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="6b7ec-153">Выберите hello **разрешить вход CHAP** флажок.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="6b7ec-154">В hello **имя** поле, имя пользователя hello питания, указанный для hello инициатора CHAP hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="6b7ec-155">В hello **секрет целевого объекта** поле, питания hello пароль, указанный для hello инициатора CHAP hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="6b7ec-156">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-156">Click **OK**.</span></span>
      
       ![Расширенные параметры: общие](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="6b7ec-158">На hello **цели** вкладка hello **свойства инициатора iSCSI** окне должны отображаться состояние устройства hello как **подключен**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="6b7ec-159">Если вы используете устройство StorSimple 1200, каждый том будет подключаться как целевое устройство iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="6b7ec-160">Таким образом шаги 3 и 4 потребуется toobe повторяется для каждого тома.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![Тома подключены как отдельные целевые устройства.](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="6b7ec-162">При изменении имени iSCSI hello hello новое имя будет использоваться для новых сеансов iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="6b7ec-163">Новые параметры не будут использоваться для существующих сеансов до выхода из системы и повторного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="6b7ec-164">Дополнительные сведения о настройке протокола CHAP на сервере узла Windows hello go слишком[Дополнительные соображения](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="6b7ec-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="6b7ec-165">Двунаправленная (взаимная, или обратная) проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="6b7ec-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="6b7ec-166">При двунаправленной проверке подлинности целевой hello проверяет подлинность инициатора hello и затем hello инициатор должен проверить подлинность целевого hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="6b7ec-167">Эта процедура требует параметров инициатора CHAP hello tooconfigure hello пользователя, обратную параметры CHAP на устройстве hello и hello узла программного обеспечения инициатора iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="6b7ec-168">Hello следующие процедуры описывают шаги hello tooconfigure взаимной проверки подлинности на устройстве hello и на узле Windows hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="6b7ec-169">tooconfigure устройства для взаимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6b7ec-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="6b7ec-170">В hello портал Azure перейдите tooyour службы диспетчера StorSimple устройство.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="6b7ec-171">Нажмите кнопку **устройств** щелкните устройство, нужно tooconfigure CHAP и выберите для.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="6b7ec-172">Go слишком**параметры устройства > безопасности**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="6b7ec-173">В hello **параметры безопасности** колонка, щелкните **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Целевое устройство CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="6b7ec-175">Прокрутите вниз на этой странице и в hello **цель CHAP** раздела:</span><span class="sxs-lookup"><span data-stu-id="6b7ec-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="6b7ec-176">Укажите **Имя пользователя обратного CHAP** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="6b7ec-177">Укажите **Пароль обратного CHAP** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="6b7ec-178">Подтверждение пароля hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-178">Confirm hello password.</span></span>
3. <span data-ttu-id="6b7ec-179">В hello **инициатора CHAP** раздела:</span><span class="sxs-lookup"><span data-stu-id="6b7ec-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="6b7ec-180">Укажите **имя пользователя** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="6b7ec-181">Укажите **пароль** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="6b7ec-182">Подтверждение пароля hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-182">Confirm hello password.</span></span>

       ![Инициатор CHAP](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="6b7ec-184">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-184">Click **Save**.</span></span> <span data-ttu-id="6b7ec-185">Вы увидите сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-185">A confirmation message is displayed.</span></span> <span data-ttu-id="6b7ec-186">Нажмите кнопку **ОК** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="6b7ec-187">сервер tooconfigure двунаправленной проверки подлинности hello Windows</span><span class="sxs-lookup"><span data-stu-id="6b7ec-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="6b7ec-188">На сервере узла Windows hello запустите инициатор iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="6b7ec-189">В hello **свойства инициатора iSCSI** окно, нажмите кнопку hello **конфигурации** вкладки.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="6b7ec-190">Щелкните **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="6b7ec-191">В hello **секрет взаимного CHAP инициатора iSCSI** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="6b7ec-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="6b7ec-192">Тип hello **пароль обратного CHAP** , настроенного в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="6b7ec-193">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-193">Click **OK**.</span></span>
      
       ![Секрет взаимного CHAP инициатора iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="6b7ec-195">Нажмите кнопку hello **цели** вкладки.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="6b7ec-196">Нажмите кнопку hello **Connect** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="6b7ec-197">В hello **подключения tooTarget** диалоговое окно, нажмите кнопку **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="6b7ec-198">В hello **дополнительные свойства** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="6b7ec-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="6b7ec-199">Выберите hello **разрешить вход CHAP** флажок.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="6b7ec-200">В hello **имя** поле, имя пользователя hello питания, указанный для hello инициатора CHAP hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="6b7ec-201">В hello **секрет целевого объекта** поле, питания hello пароль, указанный для hello инициатора CHAP hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="6b7ec-202">Выберите hello **выполнить взаимную проверку подлинности** флажок.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Расширенные параметры: взаимная аутентификация](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="6b7ec-204">Нажмите кнопку **ОК** toocomplete hello CHAP конфигурации</span><span class="sxs-lookup"><span data-stu-id="6b7ec-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="6b7ec-205">Дополнительные сведения о настройке протокола CHAP на сервере узла Windows hello go слишком[Дополнительные соображения](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="6b7ec-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="6b7ec-206">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="6b7ec-206">Additional considerations</span></span>

<span data-ttu-id="6b7ec-207">Hello **быстрое подключение** компонент не поддерживает подключения с включенным CHAP.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="6b7ec-208">При включении CHAP, убедитесь, что используется hello **Connect** кнопки, которая доступна на hello **цели** целевой tooa tooconnect вкладку.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Подключение tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="6b7ec-210">В hello **подключения tooTarget** диалоговое окно, представленному, выберите hello **добавить это подключение toohello списку избранных целевых объектов** флажок.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="6b7ec-211">Этот выбор гарантирует, что каждый раз при перезагрузке компьютера hello, попытка toorestore hello подключения toohello избранные конечные объекты iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="6b7ec-212">Ошибки во время настройки</span><span class="sxs-lookup"><span data-stu-id="6b7ec-212">Errors during configuration</span></span>

<span data-ttu-id="6b7ec-213">Если настройка CHAP неверен, то, скорее всего, toosee **сбой проверки подлинности** сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="6b7ec-214">Проверка конфигурации CHAP</span><span class="sxs-lookup"><span data-stu-id="6b7ec-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="6b7ec-215">Можно проверить, что используется протокол CHAP, выполнив следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="6b7ec-216">tooverify настройки CHAP</span><span class="sxs-lookup"><span data-stu-id="6b7ec-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="6b7ec-217">Щелкните **Избранные целевые устройства**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="6b7ec-218">Выберите целевой hello, для которого включена проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="6b7ec-219">Щелкните **Сведения**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-219">Click **Details**.</span></span>
   
    ![Свойства инициатора iSCSI: целевые устройства](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="6b7ec-221">В hello **Избранные данные целевого объекта** диалоговое окно, обратите внимание запись hello в hello **проверки подлинности** поля.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="6b7ec-222">Если настройка hello выполнена успешно, появится название **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="6b7ec-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Сведения об избранном целевом устройстве](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="6b7ec-224">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b7ec-224">Next steps</span></span>

* <span data-ttu-id="6b7ec-225">Узнайте больше о [безопасности StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="6b7ec-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="6b7ec-226">Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6b7ec-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

