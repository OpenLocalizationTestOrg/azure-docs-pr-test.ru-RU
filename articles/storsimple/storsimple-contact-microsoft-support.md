---
title: "Регистрация запроса в службу поддержки для устройства StorSimple серии 8000 | Документация Майкрософт"
description: "Узнайте, как создать запрос на обслуживание и запустить сеанс поддержки на устройстве StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cecc2566b432e897b5eff0c12e66598f0518ed80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="37823-103">Обращение в службу поддержки Майкрософт по вопросам, связанным со StorSimple</span><span class="sxs-lookup"><span data-stu-id="37823-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="37823-104">Если у вас возникли проблемы с решением Microsoft Azure StorSimple, можно обратиться за помощью в службу технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="37823-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="37823-105">В ходе общения со специалистом технической поддержки также может потребоваться запустить сеанс поддержки на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="37823-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="37823-106">В этой статье описаны следующие операции.</span><span class="sxs-lookup"><span data-stu-id="37823-106">This article walks you through:</span></span>

* <span data-ttu-id="37823-107">Создание запроса на техническую поддержку.</span><span class="sxs-lookup"><span data-stu-id="37823-107">How to create a support request.</span></span>
* <span data-ttu-id="37823-108">Запуск сеанса технической поддержки из интерфейса Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="37823-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="37823-109">Перед созданием запроса на техническую поддержку ознакомьтесь с [соглашениями об уровне обслуживания и сведениями о StorSimple серии 8000](https://msdn.microsoft.com/library/mt433077.aspx) .</span><span class="sxs-lookup"><span data-stu-id="37823-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="37823-110">Создание запроса на обслуживание</span><span class="sxs-lookup"><span data-stu-id="37823-110">Create a support request</span></span>
<span data-ttu-id="37823-111">Для создания запроса на обслуживание выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="37823-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="37823-112">Для создания запроса на обслуживание выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="37823-112">To create a support request</span></span>
1. <span data-ttu-id="37823-113">На [классическом портале Azure](https://manage.windowsazure.com/)в правом верхнем углу страницы щелкните имя своей учетной записи, а затем — элемент **Обратитесь в службу технической поддержки Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="37823-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![Свяжитесь со службой технической поддержки Microsoft через портал управления](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="37823-115">Откроется новый портал Azure (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="37823-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="37823-116">Щелкните элемент **Новый запрос в службу поддержки** .</span><span class="sxs-lookup"><span data-stu-id="37823-116">Click the **New support request** tile.</span></span>
   
    ![Обращение в службу поддержки Майкрософт через новый портал](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="37823-118">В правой части экрана появится область **Новый запрос в службу поддержки** .</span><span class="sxs-lookup"><span data-stu-id="37823-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![Область "Новый запрос в службу поддержки"](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="37823-120">В диалоговом окне **Базовые** выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="37823-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="37823-121">Из раскрывающегося списка **Тип вопроса** выберите **Технический**.</span><span class="sxs-lookup"><span data-stu-id="37823-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="37823-122">Из раскрывающегося списка **Подписка** выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="37823-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="37823-123">Из раскрывающегося списка **Служба** выберите **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="37823-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="37823-124">Из раскрывающегося списка **План поддержки** выберите план поддержки.</span><span class="sxs-lookup"><span data-stu-id="37823-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="37823-125">Чтобы получить техническую поддержку, у вас должен быть платный план поддержки.</span><span class="sxs-lookup"><span data-stu-id="37823-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="37823-126">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="37823-126">Click **Next**.</span></span> <span data-ttu-id="37823-127">Откроется диалоговое окно **Проблема** .</span><span class="sxs-lookup"><span data-stu-id="37823-127">The **Problem** dialog box appears.</span></span>
   
    ![Область "Новый запрос в службу поддержки"](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="37823-129">В диалоговом окне **Проблема** выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="37823-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="37823-130">Выберите уровень **серьезности** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="37823-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="37823-131">Выберите **тип проблемы** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="37823-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="37823-132">Выберите **категорию** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="37823-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="37823-133">Кратко опишите свою проблему в поле **Сведения** .</span><span class="sxs-lookup"><span data-stu-id="37823-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="37823-134">В поле **Интервал времени** укажите дату, время и часовой пояс последнего появления ошибки.</span><span class="sxs-lookup"><span data-stu-id="37823-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="37823-135">В разделе **Отправка файла**щелкните значок папки, чтобы выбрать пакет поддержки.</span><span class="sxs-lookup"><span data-stu-id="37823-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="37823-136">Установите флажок **Share diagnostic information** (Отправлять диагностические сведения).</span><span class="sxs-lookup"><span data-stu-id="37823-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="37823-137">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="37823-137">Click **Next**.</span></span> <span data-ttu-id="37823-138">Откроется диалоговое окно **Контактные данные** .</span><span class="sxs-lookup"><span data-stu-id="37823-138">The **Contact information** dialog box appears.</span></span>
   
    ![Область "Новый запрос в службу поддержки"](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="37823-140">Введите контактные данные и выберите способ связи (по телефону или электронной почте).</span><span class="sxs-lookup"><span data-stu-id="37823-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="37823-141">Установите флажок **Save contact changes for future support requests** (Сохранить изменения контактных данных для будущих обращений в службу поддержки).</span><span class="sxs-lookup"><span data-stu-id="37823-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="37823-142">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="37823-142">Click **Create**.</span></span>

<span data-ttu-id="37823-143">После отправки запроса с вами максимально оперативно свяжется специалист службы технической поддержки для обработки вашего запроса.</span><span class="sxs-lookup"><span data-stu-id="37823-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="37823-144">Запуск сеанса поддержки в Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="37823-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="37823-145">Чтобы устранить все проблемы, которые могут возникнуть на устройстве StorSimple, необходимо связаться со службой поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="37823-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="37823-146">Для подключения к устройству специалистам службы поддержки Майкрософт может потребоваться запуск сеанса поддержки на устройстве.</span><span class="sxs-lookup"><span data-stu-id="37823-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="37823-147">Для создания сеанса поддержки выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="37823-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="37823-148">Запуск сеанса поддержки</span><span class="sxs-lookup"><span data-stu-id="37823-148">To start a support session</span></span>
1. <span data-ttu-id="37823-149">Подключитесь к устройству с помощью последовательной консоли или сеанса telnet с удаленного компьютера.</span><span class="sxs-lookup"><span data-stu-id="37823-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="37823-150">Подробные инструкции см. в разделе [Подключение к последовательной консоли устройства с помощью PuTTY](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="37823-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="37823-151">В открывшемся окне сеанса нажмите клавишу **ВВОД** , чтобы открыть командную строку.</span><span class="sxs-lookup"><span data-stu-id="37823-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="37823-152">В меню последовательной консоли выберите вариант 1 **Войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="37823-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="37823-153">При появлении запроса введите следующий пароль:</span><span class="sxs-lookup"><span data-stu-id="37823-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="37823-154">При появлении запроса введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37823-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="37823-155">На экране появится зашифрованная строка.</span><span class="sxs-lookup"><span data-stu-id="37823-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="37823-156">Скопируйте эту строку в текстовый редактор, например в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="37823-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="37823-157">Сохраните эту строку и отправьте ее по электронной почте в службу поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="37823-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="37823-158">Сеанс поддержки можно отключить, выполнив команду `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="37823-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="37823-159">Устройство StorSimple также попытается отключить сеанс поддержки на 8 часов после запуска сеанса.</span><span class="sxs-lookup"><span data-stu-id="37823-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="37823-160">Лучше всего изменить учетные данные устройства StorSimple после установления сеанса поддержки.</span><span class="sxs-lookup"><span data-stu-id="37823-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

