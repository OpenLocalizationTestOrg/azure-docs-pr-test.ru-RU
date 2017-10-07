---
title: "обращение в службу поддержки для StorSimple серии 8000 aaaLog | Документы Microsoft"
description: "Узнайте, как запросить toocreate сотрудник службы поддержки и запустить сеанс поддержки на устройстве StorSimple."
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
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="45e1e-103">Обращение в службу поддержки Майкрософт по вопросам, связанным со StorSimple</span><span class="sxs-lookup"><span data-stu-id="45e1e-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="45e1e-104">Если у вас возникли проблемы с решением Microsoft Azure StorSimple, можно обратиться за помощью в службу технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="45e1e-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="45e1e-105">В интерактивный сеанс с сотрудником службы поддержки может также потребоваться toostart сеанс поддержки на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="45e1e-105">In an online session with your support engineer, you may also need toostart a support session on your StorSimple device.</span></span> <span data-ttu-id="45e1e-106">В этой статье описаны следующие операции.</span><span class="sxs-lookup"><span data-stu-id="45e1e-106">This article walks you through:</span></span>

* <span data-ttu-id="45e1e-107">Способ запроса toocreate технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="45e1e-107">How toocreate a support request.</span></span>
* <span data-ttu-id="45e1e-108">Как toostart сеанс поддержки в hello в интерфейсе Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="45e1e-108">How toostart a support session in hello Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="45e1e-109">Просмотрите hello [рядов поддержки StorSimple 8000 соглашений об уровне обслуживания и сведения о](https://msdn.microsoft.com/library/mt433077.aspx) перед тем как создать запрос на техническую поддержку.</span><span class="sxs-lookup"><span data-stu-id="45e1e-109">Review hello [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="45e1e-110">Создание запроса на обслуживание</span><span class="sxs-lookup"><span data-stu-id="45e1e-110">Create a support request</span></span>
<span data-ttu-id="45e1e-111">Выполните следующие шаги toocreate запрос на техническую поддержку hello.</span><span class="sxs-lookup"><span data-stu-id="45e1e-111">Perform hello following steps toocreate a support request:</span></span>

#### <a name="toocreate-a-support-request"></a><span data-ttu-id="45e1e-112">toocreate запрос на техническую поддержку</span><span class="sxs-lookup"><span data-stu-id="45e1e-112">toocreate a support request</span></span>
1. <span data-ttu-id="45e1e-113">В hello [классический портал Azure](https://manage.windowsazure.com/), hello верхний правый угол, щелкните имя вашей учетной записи и нажмите кнопку **обратитесь в службу поддержки корпорации Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="45e1e-113">In hello [Azure classic portal](https://manage.windowsazure.com/), in hello upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![Свяжитесь со службой технической поддержки Microsoft через портал управления](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="45e1e-115">Будет перенаправленный toohello новый портал Azure (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45e1e-115">You will be redirected toohello new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="45e1e-116">Нажмите кнопку hello **New поддерживает запрос** плитки.</span><span class="sxs-lookup"><span data-stu-id="45e1e-116">Click hello **New support request** tile.</span></span>
   
    ![Обращение в службу поддержки Майкрософт через новый портал](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="45e1e-118">Hello правой части экрана приветствия, hello **New поддерживает запрос** появится область.</span><span class="sxs-lookup"><span data-stu-id="45e1e-118">On hello right side of hello screen, hello **New support request** pane appears.</span></span> 
   
    ![Область "Новый запрос в службу поддержки"](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="45e1e-120">В hello **основы** диалоговое окно, полный hello следующие:</span><span class="sxs-lookup"><span data-stu-id="45e1e-120">In hello **Basics** dialog box, complete hello following:</span></span>                                
   
   1. <span data-ttu-id="45e1e-121">Из hello **выдачи типа** раскрывающемся списке выберите **технические**.</span><span class="sxs-lookup"><span data-stu-id="45e1e-121">From hello **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="45e1e-122">Выберите **подписки** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="45e1e-122">Select a **Subscription** from hello drop-down list.</span></span>
   3. <span data-ttu-id="45e1e-123">Из hello **службы** раскрывающемся списке выберите **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="45e1e-123">From hello **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="45e1e-124">Выберите **план поддержки** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="45e1e-124">Select a **Support plan** from hello drop-down list.</span></span> <span data-ttu-id="45e1e-125">Требуется платная поддержка tooenable плана, службой технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="45e1e-125">You need a paid support plan tooenable Technical Support.</span></span>
4. <span data-ttu-id="45e1e-126">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="45e1e-126">Click **Next**.</span></span> <span data-ttu-id="45e1e-127">Hello **проблема** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="45e1e-127">hello **Problem** dialog box appears.</span></span>
   
    ![Область "Новый запрос в службу поддержки"](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="45e1e-129">В hello **проблема** диалоговое окно, полный hello следующие:</span><span class="sxs-lookup"><span data-stu-id="45e1e-129">In hello **Problem** dialog box, complete hello following:</span></span>
   
   1. <span data-ttu-id="45e1e-130">Выберите **серьезность** уровня из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="45e1e-130">Select a **Severity** level from hello drop-down list.</span></span>
   2. <span data-ttu-id="45e1e-131">Выберите **тип проблемы** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="45e1e-131">Select a **Problem type** from hello drop-down list.</span></span>
   3. <span data-ttu-id="45e1e-132">Выберите **категории** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="45e1e-132">Select a **Category** from hello drop-down list.</span></span> 
   4. <span data-ttu-id="45e1e-133">В hello **сведения** введите краткое описание проблемы.</span><span class="sxs-lookup"><span data-stu-id="45e1e-133">In hello **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="45e1e-134">В hello **временные рамки** укажите, hello Дата, время и часовой пояс, соответствующий toohello последнего возникновения проблемы.</span><span class="sxs-lookup"><span data-stu-id="45e1e-134">In hello **Time frame** box, indicate hello date, time, and time zone that corresponds toohello most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="45e1e-135">В разделе **передачу файла**, щелкните пакет поддержки tooyour toobrowse значок hello папки.</span><span class="sxs-lookup"><span data-stu-id="45e1e-135">Under **File upload**, click hello folder icon toobrowse tooyour support package.</span></span>
   7. <span data-ttu-id="45e1e-136">Выберите hello **совместно использовать диагностические сведения** флажок.</span><span class="sxs-lookup"><span data-stu-id="45e1e-136">Select hello **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="45e1e-137">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="45e1e-137">Click **Next**.</span></span> <span data-ttu-id="45e1e-138">Hello **контактные данные** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="45e1e-138">hello **Contact information** dialog box appears.</span></span>
   
    ![Область "Новый запрос в службу поддержки"](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="45e1e-140">Введите контактные данные и выберите способ связи (по телефону или электронной почте).</span><span class="sxs-lookup"><span data-stu-id="45e1e-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="45e1e-141">Выберите hello **сохранить изменения контактных данных для будущих запросов на поддержку** флажок.</span><span class="sxs-lookup"><span data-stu-id="45e1e-141">Select hello **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="45e1e-142">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="45e1e-142">Click **Create**.</span></span>

<span data-ttu-id="45e1e-143">После отправки запроса сотрудник службы поддержки свяжется с вами как можно быстрее tooproceed вместе с запросом.</span><span class="sxs-lookup"><span data-stu-id="45e1e-143">After you have submitted your request, a Support engineer will contact you as soon as possible tooproceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="45e1e-144">Запуск сеанса поддержки в Windows PowerShell для StorSimple</span><span class="sxs-lookup"><span data-stu-id="45e1e-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="45e1e-145">tootroubleshoot ошибки, которые могут возникнуть с устройством StorSimple hello, вы должны будете tooengage с hello группа поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="45e1e-145">tootroubleshoot any issues that you might experience with hello StorSimple device, you will need tooengage with hello Microsoft Support team.</span></span> <span data-ttu-id="45e1e-146">Службу технической поддержки Майкрософт может потребоваться toouse toolog сеанс поддержки на устройстве tooyour.</span><span class="sxs-lookup"><span data-stu-id="45e1e-146">Microsoft Support may need toouse a support session toolog on tooyour device.</span></span> 

<span data-ttu-id="45e1e-147">Hello следующих шагов toostart сеанс поддержки:</span><span class="sxs-lookup"><span data-stu-id="45e1e-147">Perform hello following steps toostart a support session:</span></span>

#### <a name="toostart-a-support-session"></a><span data-ttu-id="45e1e-148">toostart сеанс поддержки</span><span class="sxs-lookup"><span data-stu-id="45e1e-148">toostart a support session</span></span>
1. <span data-ttu-id="45e1e-149">Устройство hello доступ непосредственно через последовательную консоль hello или сеанс telnet с удаленного компьютера.</span><span class="sxs-lookup"><span data-stu-id="45e1e-149">Access hello device directly by using hello serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="45e1e-150">toodo hello, повторите шаги, в [последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="45e1e-150">toodo this, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="45e1e-151">В открывшемся сеансе hello клавиши hello **ввод** tooget ключа командной строки.</span><span class="sxs-lookup"><span data-stu-id="45e1e-151">In hello session that opens, press hello **Enter** key tooget a command prompt.</span></span>
3. <span data-ttu-id="45e1e-152">В меню последовательной консоли hello, выберите параметр 1, **войти с полным доступом**.</span><span class="sxs-lookup"><span data-stu-id="45e1e-152">In hello serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="45e1e-153">Введите следующую hello hello следующий пароль:</span><span class="sxs-lookup"><span data-stu-id="45e1e-153">At hello prompt, type hello following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="45e1e-154">Привет введите в строке приветствия следующую команду:</span><span class="sxs-lookup"><span data-stu-id="45e1e-154">At hello prompt, type hello following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="45e1e-155">Будет выведено tooyou зашифрованную строку.</span><span class="sxs-lookup"><span data-stu-id="45e1e-155">An encrypted string will be presented tooyou.</span></span> <span data-ttu-id="45e1e-156">Скопируйте эту строку в текстовый редактор, например в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="45e1e-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="45e1e-157">Сохраните строку и отправьте его в tooMicrosoft сообщения электронной почты технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="45e1e-157">Save this string and send it in an email message tooMicrosoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="45e1e-158">Сеанс поддержки можно отключить, выполнив команду `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="45e1e-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="45e1e-159">Hello StorSimple устройство также попытается выполнить доступ к поддержке toodisable 8 часов после запуска сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="45e1e-159">hello StorSimple device will also attempt toodisable support access 8 hours after hello session was initiated.</span></span> <span data-ttu-id="45e1e-160">Это наиболее toochange рекомендаций устройства StorSimple учетных данных после инициации сеанса поддержки.</span><span class="sxs-lookup"><span data-stu-id="45e1e-160">It is a best practice toochange your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

