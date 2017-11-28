---
title: "Настройка CHAP для устройства StorSimple серии 8000 | Документация Майкрософт"
description: "В статье описываются способы настройки протокола CHAP на устройстве StorSimple."
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
ms.openlocfilehash: 36b4e73d0336deb9560d44163fc5330d1c9d775c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="03b99-103">Настроить CHAP для устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="03b99-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="03b99-104">В этом учебнике описывается настройка CHAP для устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="03b99-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="03b99-105">Процедуры, описанные в этой статье, относятся к серии StorSimple 8000, а также к устройствам StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="03b99-105">The procedure detailed in this article applies to StorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="03b99-106">CHAP — сокращение от Challenge Handshake Authentication Protocol (протокол проверки подлинности на основе вызова).</span><span class="sxs-lookup"><span data-stu-id="03b99-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="03b99-107">Это схема проверки подлинности, используемая серверами для проверки удаленных клиентов.</span><span class="sxs-lookup"><span data-stu-id="03b99-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="03b99-108">Проверка выполняется на основе общего пароля или секрета.</span><span class="sxs-lookup"><span data-stu-id="03b99-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="03b99-109">Протокол CHAP может быть односторонним (однонаправленным) или двусторонним (двунаправленным).</span><span class="sxs-lookup"><span data-stu-id="03b99-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="03b99-110">При использовании одностороннего CHAP целевое устройство проверяет подлинность инициатора.</span><span class="sxs-lookup"><span data-stu-id="03b99-110">One-way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="03b99-111">С другой стороны, для двустороннего или обратного CHAP требуется, чтобы целевое устройство проверило подлинность инициатора, а затем инициатор проверил подлинность целевого устройства.</span><span class="sxs-lookup"><span data-stu-id="03b99-111">Mutual or reverse CHAP, on the other hand, requires that the target authenticate the initiator and then the initiator authenticate the target.</span></span> <span data-ttu-id="03b99-112">Проверку подлинности инициатора можно реализовать без проверки подлинности целевого устройства.</span><span class="sxs-lookup"><span data-stu-id="03b99-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="03b99-113">Однако проверка подлинности целевого устройства может быть реализована только в том случае, если проверка подлинности инициатора также реализована.</span><span class="sxs-lookup"><span data-stu-id="03b99-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="03b99-114">CHAP лучше всего использовать для повышения безопасности iSCSI.</span><span class="sxs-lookup"><span data-stu-id="03b99-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="03b99-115">Помните, что в настоящее время IPSEC не поддерживается на устройствах StorSimple.</span><span class="sxs-lookup"><span data-stu-id="03b99-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="03b99-116">Параметры CHAP на устройстве StorSimple можно настроить следующими способами.</span><span class="sxs-lookup"><span data-stu-id="03b99-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="03b99-117">Для однонаправленной или односторонней проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="03b99-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="03b99-118">Для двунаправленной (взаимной, или обратной) проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="03b99-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="03b99-119">В каждом из этих случаев необходимо настроить портал для устройства и программное обеспечение инициатора на сервере iSCSI.</span><span class="sxs-lookup"><span data-stu-id="03b99-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="03b99-120">Подробное описание действий для этой конфигурации приведено в следующем учебнике.</span><span class="sxs-lookup"><span data-stu-id="03b99-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="03b99-121">Для однонаправленной или односторонней проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="03b99-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="03b99-122">При однонаправленной аутентификации целевое устройство проверяет подлинность инициатора.</span><span class="sxs-lookup"><span data-stu-id="03b99-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="03b99-123">Для этой проверки необходимо настроить параметры инициатора CHAP на устройстве StorSimple и программное обеспечение инициатора iSCSI на узле.</span><span class="sxs-lookup"><span data-stu-id="03b99-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="03b99-124">Далее описаны подробные процедуры для устройства StorSimple и узла Windows.</span><span class="sxs-lookup"><span data-stu-id="03b99-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="03b99-125">Для настройки устройства для односторонней проверки подлинности выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-125">To configure your device for one-way authentication</span></span>
1. <span data-ttu-id="03b99-126">На классическом портале Azure на странице **Устройства** щелкните вкладку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="03b99-126">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![Инициатор CHAP](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="03b99-128">Прокрутите страницу вниз и в разделе **Инициатор CHAP**</span><span class="sxs-lookup"><span data-stu-id="03b99-128">Scroll down on this page, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="03b99-129">Укажите имя пользователя для инициатора CHAP.</span><span class="sxs-lookup"><span data-stu-id="03b99-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="03b99-130">Укажите пароль для инициатора CHAP.</span><span class="sxs-lookup"><span data-stu-id="03b99-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="03b99-131">Имя пользователя CHAP должно содержать меньше 233 символов.</span><span class="sxs-lookup"><span data-stu-id="03b99-131">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="03b99-132">Длина пароля CHAP должна быть от 12 до 16 символов.</span><span class="sxs-lookup"><span data-stu-id="03b99-132">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="03b99-133">Попытка использовать более длинное имя пользователя или пароль приведет к сбою проверки подлинности на узле Windows.</span><span class="sxs-lookup"><span data-stu-id="03b99-133">A longer user name or password will result in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="03b99-134">Подтвердите пароль.</span><span class="sxs-lookup"><span data-stu-id="03b99-134">Confirm the password.</span></span>
3. <span data-ttu-id="03b99-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="03b99-135">Click **Save**.</span></span> <span data-ttu-id="03b99-136">Появится сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="03b99-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="03b99-137">Нажмите кнопку **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="03b99-137">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="03b99-138">Для настройки односторонней проверки подлинности на сервере узла Windows выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-138">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="03b99-139">Запустите инициатор iSCSI на сервере узла Windows.</span><span class="sxs-lookup"><span data-stu-id="03b99-139">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="03b99-140">В окне **Свойства инициатора iSCSI** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-140">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="03b99-141">Щелкните вкладку **Обнаружение** .</span><span class="sxs-lookup"><span data-stu-id="03b99-141">Click the **Discovery** tab.</span></span>
      
       ![Свойства инициатора iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="03b99-143">Щелкните **Портал обнаружения**.</span><span class="sxs-lookup"><span data-stu-id="03b99-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="03b99-144">В диалоговом окне **Обнаружение целевого портала** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-144">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="03b99-145">Укажите IP-адрес устройства.</span><span class="sxs-lookup"><span data-stu-id="03b99-145">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="03b99-146">Нажмите кнопку **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="03b99-146">Click **Advanced**.</span></span>
      
       ![Обнаружение целевого портала](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="03b99-148">В диалоговом окне **Дополнительные параметры** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-148">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="03b99-149">Установите флажок **Разрешить проверку подлинности CHAP** .</span><span class="sxs-lookup"><span data-stu-id="03b99-149">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="03b99-150">В поле **Имя** введите имя пользователя, указанное для инициатора CHAP на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="03b99-150">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="03b99-151">В поле **Секрет целевого узла** введите пароль, указанный для инициатора CHAP на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="03b99-151">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="03b99-152">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="03b99-152">Click **OK**.</span></span>
      
       ![Расширенные параметры: общие](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="03b99-154">На вкладке **Целевые объекты** окна **iSCSI Initiator Properties** (Свойства инициатора iSCSI) состояние устройства должно измениться на **Подключено**.</span><span class="sxs-lookup"><span data-stu-id="03b99-154">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="03b99-155">Если вы используете устройство StorSimple 1200, каждый том будет подключен как целевое устройство iSCSI, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="03b99-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="03b99-156">Поэтому необходимо будет повторить шаги 3 и 4 для каждого тома.</span><span class="sxs-lookup"><span data-stu-id="03b99-156">Hence, steps  3-4 will need to be repeated for each volume.</span></span>
   
    ![Тома подключены как отдельные целевые устройства.](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="03b99-158">Если изменить имя iSCSI, то новое имя будет использоваться для новых сеансов iSCSI.</span><span class="sxs-lookup"><span data-stu-id="03b99-158">If you change the iSCSI name, the new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="03b99-159">Новые параметры не будут использоваться для существующих сеансов до выхода из системы и повторного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="03b99-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="03b99-160">Дополнительные сведения о настройке протокола CHAP на сервере узла Windows приведены в разделе [Дополнительные замечания](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="03b99-160">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="03b99-161">Двунаправленная (взаимная, или обратная) проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="03b99-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="03b99-162">При двусторонней проверке подлинности целевое устройство проверяет подлинность инициатора, а затем инициатор проверяет подлинность целевого устройства.</span><span class="sxs-lookup"><span data-stu-id="03b99-162">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="03b99-163">Для этого необходимо настроить параметры CHAP инициатора, а также параметры обратного CHAP на устройстве и программное обеспечение инициатора iSCSI на узле.</span><span class="sxs-lookup"><span data-stu-id="03b99-163">This requires the user to configure the CHAP initiator settings, as well as the reverse CHAP settings on the device and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="03b99-164">Следующие процедуры описывают шаги по настройке взаимной проверки подлинности на устройстве и на узле Windows.</span><span class="sxs-lookup"><span data-stu-id="03b99-164">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="03b99-165">Для настройки устройства для взаимной проверки подлинности выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-165">To configure your device for mutual authentication</span></span>
1. <span data-ttu-id="03b99-166">На классическом портале Azure на странице **Устройства** щелкните вкладку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="03b99-166">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![Целевое устройство CHAP](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="03b99-168">Прокрутите страницу вниз и в разделе **Целевое устройство CHAP**</span><span class="sxs-lookup"><span data-stu-id="03b99-168">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="03b99-169">Укажите **Имя пользователя обратного CHAP** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="03b99-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="03b99-170">Укажите **Пароль обратного CHAP** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="03b99-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="03b99-171">Подтвердите пароль.</span><span class="sxs-lookup"><span data-stu-id="03b99-171">Confirm the password.</span></span>
3. <span data-ttu-id="03b99-172">В разделе **Инициатор CHAP**</span><span class="sxs-lookup"><span data-stu-id="03b99-172">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="03b99-173">Укажите **имя пользователя** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="03b99-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="03b99-174">Укажите **пароль** для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="03b99-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="03b99-175">Подтвердите пароль.</span><span class="sxs-lookup"><span data-stu-id="03b99-175">Confirm the password.</span></span>
4. <span data-ttu-id="03b99-176">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="03b99-176">Click **Save**.</span></span> <span data-ttu-id="03b99-177">Появится сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="03b99-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="03b99-178">Нажмите кнопку **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="03b99-178">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="03b99-179">Для настройки двунаправленной проверки подлинности на сервере узла Windows выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-179">To configure bidirectional authentication on the Windows host server</span></span>
1. <span data-ttu-id="03b99-180">Запустите инициатор iSCSI на сервере узла Windows.</span><span class="sxs-lookup"><span data-stu-id="03b99-180">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="03b99-181">В окне **iSCSI Initiator Properties** (Свойства инициатора iSCSI) щелкните вкладку **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="03b99-181">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="03b99-182">Щелкните **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="03b99-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="03b99-183">В диалоговом окне **Секрет взаимного CHAP инициатора iSCSI**</span><span class="sxs-lookup"><span data-stu-id="03b99-183">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="03b99-184">Введите **Пароль обратного CHAP** , указанный при настройке классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="03b99-184">Type the **Reverse CHAP Password** that you configured in the Azure classic portal.</span></span>
   2. <span data-ttu-id="03b99-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="03b99-185">Click **OK**.</span></span>
      
       ![Секрет взаимного CHAP инициатора iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="03b99-187">Перейдите на вкладку **Целевые устройства** .</span><span class="sxs-lookup"><span data-stu-id="03b99-187">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="03b99-188">Нажмите кнопку **Подключение** .</span><span class="sxs-lookup"><span data-stu-id="03b99-188">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="03b99-189">В диалоговом окне **Подключение к конечному объекту** щелкните **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="03b99-189">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="03b99-190">В диалоговом окне **Дополнительные параметры** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-190">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="03b99-191">Установите флажок **Разрешить проверку подлинности CHAP** .</span><span class="sxs-lookup"><span data-stu-id="03b99-191">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="03b99-192">В поле **Имя** введите имя пользователя, указанное для инициатора CHAP на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="03b99-192">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="03b99-193">В поле **Секрет целевого узла** введите пароль, указанный для инициатора CHAP на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="03b99-193">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="03b99-194">Установите флажок **Выполнять взаимную проверку подлинности** .</span><span class="sxs-lookup"><span data-stu-id="03b99-194">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Расширенные параметры: взаимная аутентификация](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="03b99-196">Нажмите кнопку **ОК** , чтобы завершить настройку CHAP.</span><span class="sxs-lookup"><span data-stu-id="03b99-196">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="03b99-197">Дополнительные сведения о настройке протокола CHAP на сервере узла Windows приведены в разделе [Дополнительные замечания](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="03b99-197">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="03b99-198">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="03b99-198">Additional considerations</span></span>
<span data-ttu-id="03b99-199">Функция **быстрого подключения** не поддерживает подключения, использующие проверку подлинности CHAP.</span><span class="sxs-lookup"><span data-stu-id="03b99-199">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="03b99-200">При включении аутентификации CHAP нажмите кнопку **Подключение** на вкладке **Целевые объекты**.</span><span class="sxs-lookup"><span data-stu-id="03b99-200">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Подключение к целевому устройству](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="03b99-202">В открывшемся диалоговом окне **Подключение к конечному объекту** установите флажок **Добавить это подключение в список предпочитаемых конечных объектов**.</span><span class="sxs-lookup"><span data-stu-id="03b99-202">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="03b99-203">Так, каждый раз после перезагрузки системы будет предпринята попытка восстановить подключение к избранным целевым устройствам iSCSI.</span><span class="sxs-lookup"><span data-stu-id="03b99-203">This ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="03b99-204">Ошибки во время настройки</span><span class="sxs-lookup"><span data-stu-id="03b99-204">Errors during configuration</span></span>
<span data-ttu-id="03b99-205">Если конфигурация CHAP неверна, появится сообщение об ошибке **Сбой проверки подлинности** .</span><span class="sxs-lookup"><span data-stu-id="03b99-205">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="03b99-206">Проверка конфигурации CHAP</span><span class="sxs-lookup"><span data-stu-id="03b99-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="03b99-207">Чтобы проверить, что протокол CHAP используется, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-207">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="03b99-208">Для проверки конфигурации CHAP выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="03b99-208">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="03b99-209">Щелкните **Избранные целевые устройства**.</span><span class="sxs-lookup"><span data-stu-id="03b99-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="03b99-210">Выберите целевое устройство, для которого включена проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="03b99-210">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="03b99-211">Щелкните **Сведения**.</span><span class="sxs-lookup"><span data-stu-id="03b99-211">Click **Details**.</span></span>
   
    ![Свойства инициатора iSCSI: целевые устройства](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="03b99-213">В диалоговом окне **Сведения о предпочитаемом конечном объекте** запомните содержимое поля **Аутентификация**.</span><span class="sxs-lookup"><span data-stu-id="03b99-213">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="03b99-214">Если настройки верны, в нем должно быть указано **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="03b99-214">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Сведения об избранном целевом устройстве](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="03b99-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03b99-216">Next steps</span></span>
* <span data-ttu-id="03b99-217">[Узнайте о больше о безопасности StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="03b99-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="03b99-218">Узнайте больше об [использовании службы диспетчера StorSimple для администрирования устройства StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="03b99-218">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

