---
title: "toouse aaaHow пароли приложений в Azure MFA? | Документация Майкрософт"
description: "Эта страница поможет пользователям понять, что такое пароли приложений и их использовании для учета tooAzure многофакторной проверки Подлинности."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="9ecbd-104">Что такое пароли приложений в службе Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="9ecbd-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="9ecbd-105">Некоторые приложения без браузера, такие как hello Apple собственного почтовый клиент, использующий Exchange Active Sync, в настоящее время не поддерживают многофакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="9ecbd-106">Многофакторная проверка подлинности активируется для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="9ecbd-107">Это означает, что пользователь не может использовать многофакторную проверку подлинности в таких случаях:</span><span class="sxs-lookup"><span data-stu-id="9ecbd-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="9ecbd-108">Hello пользователя включена многофакторная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="9ecbd-108">hello user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="9ecbd-109">Hello пользователь пытается toouse приложения без браузера.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-109">hello user is trying toouse a non-browser app.</span></span>

<span data-ttu-id="9ecbd-110">Пароль приложения позволяет использовать приложение hello toouse hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-110">An app password allows hello user toouse hello app.</span></span>

<span data-ttu-id="9ecbd-111">Получив пароль, используйте его вместо исходного пароля в этих приложениях без использования браузера.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="9ecbd-112">При регистрации для двухшаговой проверки ты говоришь Microsoft не toolet, любой пользователь, войдите с использованием пароля, если они не могут также выполнять проверки второй hello.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-112">When you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="9ecbd-113">Hello Apple собственного почтового клиента на ваш телефон не удается войти в ходе так как он не может запросить двухшаговую проверку.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-113">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="9ecbd-114">Hello решения toothis проблема заключается в toocreate более безопасным паролем приложения, не используйте повседневные.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-114">hello solution toothis problem is toocreate a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="9ecbd-115">Пароли приложений предназначены только для тех приложений, которые не поддерживают двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="9ecbd-116">Используйте пароль приложения hello, чтобы приложения могли обходить многофакторную проверку подлинности и продолжить toowork.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-116">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>


> [!NOTE]
> <span data-ttu-id="9ecbd-117">Все клиенты Office 2013 (включая Outlook) поддерживают новые протоколы идентификации и двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="9ecbd-118">Пароли приложений не нужно использовать с клиентами Office 2013.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="9ecbd-119">Дополнительные сведения см. в записи блога [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) (Анонсирована общедоступная предварительная версия современной службы многофакторной идентификации для Office 2013).</span><span class="sxs-lookup"><span data-stu-id="9ecbd-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="9ecbd-120">Как toouse пароли приложений</span><span class="sxs-lookup"><span data-stu-id="9ecbd-120">How toouse app passwords</span></span>
<span data-ttu-id="9ecbd-121">Ниже приведены некоторые вещи tooknow о паролях приложений.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-121">Here are some things tooknow about app passwords:</span></span>

* <span data-ttu-id="9ecbd-122">Вам не нужно придумывать пароли приложений.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-122">You don't create your own app passwords.</span></span> <span data-ttu-id="9ecbd-123">Они создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-123">They are automatically generated.</span></span>
* <span data-ttu-id="9ecbd-124">В настоящее время имеется ограничение — не более 40 паролей на пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="9ecbd-125">Если после достижения предела hello toocreate пароль приложения, потребуется toodelete одно из существующих паролей приложений перед созданием нового.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-125">If you try toocreate an app password after you have reached hello limit, you'll have toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="9ecbd-126">Мы рекомендуем использовать один пароль приложения для каждого устройства, а не для отдельных приложений.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="9ecbd-127">Например, вы можете создать один пароль приложения для ноутбука и использовать его для всех приложений на ноутбуке.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="9ecbd-128">Затем создайте второй toouse пароль приложения для всех приложений на рабочем столе.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-128">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="9ecbd-129">Можно выбрать один hello пароль приложения при первом запуске регистрации для двухшаговой проверки.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-129">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="9ecbd-130">Если потребуются дополнительные пароли, их можно создать.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="9ecbd-131">Создание и удаление паролей приложений</span><span class="sxs-lookup"><span data-stu-id="9ecbd-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="9ecbd-132">При первом входе вам предоставляется пароль приложения.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="9ecbd-133">Кроме того, позже вы можете создавать и удалять дополнительные пароли приложений.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="9ecbd-134">Как вы это будете делать, зависит от способа использования многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="9ecbd-135">Hello ответов следующие вопросы toodetermine, куда следует обратиться toomanage пароли приложений:</span><span class="sxs-lookup"><span data-stu-id="9ecbd-135">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="9ecbd-136">Вы используете двухфакторную проверку подлинности для личной учетной записи Майкрософт?</span><span class="sxs-lookup"><span data-stu-id="9ecbd-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="9ecbd-137">Если Да, вы должны обращаться toohello [пароли приложений и двухшаговую проверку](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) статьи для получения справки.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-137">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="9ecbd-138">Если нет, по-прежнему tooquestion двух.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-138">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="9ecbd-139">Итак, вы используете двухфакторную проверку подлинности для рабочей или учебной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="9ecbd-140">Вы используете его toosign в приложениях tooOffice 365?</span><span class="sxs-lookup"><span data-stu-id="9ecbd-140">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="9ecbd-141">Если Да, вы должны обращаться слишком[создать пароль приложения для Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) для справки.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-141">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="9ecbd-142">Если нет, по-прежнему tooquestion трех.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-142">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="9ecbd-143">Вы используете двухфакторную проверку подлинности для Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="9ecbd-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="9ecbd-144">Если Да, по-прежнему toohello [управление пароли приложений в hello портал Azure](#manage-app-passwords-in-the-Azure-portal) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-144">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="9ecbd-145">Если нет, по-прежнему tooquestion четырех.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-145">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="9ecbd-146">Вы не знаете, где вы используете двухфакторную проверку подлинности?</span><span class="sxs-lookup"><span data-stu-id="9ecbd-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="9ecbd-147">Продолжить toohello [управление паролями приложения с портала MyApps hello](#manage-app-passwords-with-the-myapps-portal) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-147">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="9ecbd-148">Управление паролями приложений в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9ecbd-148">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="9ecbd-149">При использовании двухшаговую проверку с помощью Azure требуется toocreate пароли приложений через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-149">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="9ecbd-150">пароли приложений toocreate в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9ecbd-150">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="9ecbd-151">Войдите в систему toohello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-151">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="9ecbd-152">Hello верхней правой кнопкой мыши имя пользователя и выберите дополнительной проверки безопасности.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-152">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="9ecbd-153">На странице приветствия proofup вверху hello выберите пароли приложений</span><span class="sxs-lookup"><span data-stu-id="9ecbd-153">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="9ecbd-154">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-154">Click **Create**.</span></span>
5. <span data-ttu-id="9ecbd-155">Введите имя для пароля приложения hello и нажмите кнопку **Далее**</span><span class="sxs-lookup"><span data-stu-id="9ecbd-155">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="9ecbd-156">Скопируйте hello пароль приложения toohello, буфер обмена и вставьте его в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-156">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![Облако](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="9ecbd-158">пароли приложений toodelete в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9ecbd-158">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="9ecbd-159">Войдите в систему toohello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="9ecbd-160">Hello верхней правой кнопкой мыши имя пользователя и выберите дополнительной проверки безопасности.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-160">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="9ecbd-161">Вверху hello, далее проверки безопасности tooadditional, выберите **пароли приложений.**</span><span class="sxs-lookup"><span data-stu-id="9ecbd-161">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="9ecbd-162">Следующий пароль приложения toohello, требуется toodelete, выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-162">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="9ecbd-163">Подтверждение удаления hello, щелкнув **Да**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-163">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="9ecbd-164">Если после удаления пароля приложения hello, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-164">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="9ecbd-165">Управление паролями приложения с портала MyApps hello.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-165">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="9ecbd-166">Если вы не уверены, как использовать многофакторную проверку подлинности, затем можно всегда создать и удалить пароли приложений через портал myapps hello.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="9ecbd-167">Здравствуйте, toocreate пароль приложения с помощью портала Myapps.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-167">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="9ecbd-168">Войдите в слишком[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="9ecbd-168">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="9ecbd-169">Щелкните свое имя в правом верхнем углу hello и выберите **профиль**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-169">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="9ecbd-170">Щелкните **Дополнительная проверка безопасности**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="9ecbd-171">![Выбор дополнительной проверки безопасности — снимок экрана](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="9ecbd-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="9ecbd-172">Выберите **Пароли приложений**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-172">Select **app passwords**.</span></span>
   <span data-ttu-id="9ecbd-173">![Выбор паролей приложений — снимок экрана](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="9ecbd-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="9ecbd-174">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-174">Click **Create**.</span></span>
6. <span data-ttu-id="9ecbd-175">Введите имя для пароля приложения hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-175">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="9ecbd-176">Скопируйте hello пароль приложения toohello, буфер обмена и вставьте его в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-176">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="9ecbd-177">![Создание пароля приложения](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="9ecbd-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="9ecbd-178">Здравствуйте, toodelete пароль приложения с помощью портала Myapps.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-178">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="9ecbd-179">Войдите в слишком[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="9ecbd-179">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="9ecbd-180">В верхней части экрана приветствия выберите профиль.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-180">At hello top, select profile.</span></span>
3. <span data-ttu-id="9ecbd-181">Щелкните **Дополнительная проверка безопасности**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-181">Select **Additional Security Verification**.</span></span>

   ![Выбор дополнительной проверки безопасности — снимок экрана](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="9ecbd-183">Выберите **Пароли приложений**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-183">Select **app passwords**.</span></span>

   ![Выбор паролей приложений — снимок экрана](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="9ecbd-185">Нажмите кнопку Далее toohello пароль требуется toodelete, **удалить**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-185">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![Удаление пароля приложения](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="9ecbd-187">Подтвердите toodelete этот пароль, щелкнув **Да**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-187">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="9ecbd-188">Если после удаления пароля приложения hello, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-188">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ecbd-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ecbd-189">Next steps</span></span>

- [<span data-ttu-id="9ecbd-190">Управление параметрами двухфакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="9ecbd-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="9ecbd-191">Испытайте hello [приложение для проверки подлинности Microsoft](microsoft-authenticator-app-how-to.md) tooverify вашего входа в систему с уведомлениями приложения, вместо получения тексты или вызовы.</span><span class="sxs-lookup"><span data-stu-id="9ecbd-191">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
