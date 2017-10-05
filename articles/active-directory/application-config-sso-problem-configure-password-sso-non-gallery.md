---
title: "Проблема при настройке единого входа по паролю для приложения не из коллекции | Документы Майкрософт"
description: "Из этой статьи вы узнаете, какие проблемы возникают при настройке единого входа по паролю для пользовательских приложений не из коллекции приложений Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 9c76b6f3495e2dd759a156fcef97b57aece8d632
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ca257-103">Проблема при настройке единого входа по паролю для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="ca257-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ca257-104">Эта статья поможет понять распространенные проблемы, которые возникают при настройке **единого входа по паролю** для приложения не из коллекции.</span><span class="sxs-lookup"><span data-stu-id="ca257-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="ca257-105">Определение полей входа в систему для приложения</span><span class="sxs-lookup"><span data-stu-id="ca257-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="ca257-106">Определение полей входа в систему поддерживается только для страниц входа на основе HTML и **не поддерживается для нестандартных страниц входа**, например для тех, которые используют Flash и другие технологии не на основе HTML.</span><span class="sxs-lookup"><span data-stu-id="ca257-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="ca257-107">Существует два способа определения полей входа в систему для приложения:</span><span class="sxs-lookup"><span data-stu-id="ca257-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="ca257-108">Автоматическое определение полей входа в систему</span><span class="sxs-lookup"><span data-stu-id="ca257-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="ca257-109">Определение полей входа в систему вручную</span><span class="sxs-lookup"><span data-stu-id="ca257-109">Manual sign-in field capture</span></span>

<span data-ttu-id="ca257-110">**Автоматическое определение полей входа в систему** хорошо работает для большинства страниц входа в систему на основе HTML, если в них используются **хорошо известные идентификаторы DIV для полей имени пользователя и пароля**.</span><span class="sxs-lookup"><span data-stu-id="ca257-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="ca257-111">Оно анализирует HTML-код страницы, извлекает идентификаторы DIV, которые соответствуют определенным критериям, и сохраняет метаданные для этого приложения, чтобы воспользоваться ими впоследствии.</span><span class="sxs-lookup"><span data-stu-id="ca257-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span></span>

<span data-ttu-id="ca257-112">**Определение полей входа в систему вручную** можно использовать в том случае, если **разработчик приложения не отметил** поля, используемые для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="ca257-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span></span> <span data-ttu-id="ca257-113">Определение полей входа в систему вручную также можно использовать в том случае, если **разработчик приложения предусмотрел несколько полей**, для которых автоматическое определение не работает.</span><span class="sxs-lookup"><span data-stu-id="ca257-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="ca257-114">Azure AD может сохранить данные для любого количества полей на странице входа, если вы покажете, где находятся эти поля.</span><span class="sxs-lookup"><span data-stu-id="ca257-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="ca257-115">В общем случае, **если автоматическое определение полей входа в систему не работает, мы всегда рекомендуем попробовать определение полей вручную.**</span><span class="sxs-lookup"><span data-stu-id="ca257-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="ca257-116">Автоматическое определение полей входа в систему для приложения</span><span class="sxs-lookup"><span data-stu-id="ca257-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="ca257-117">Для настройки **единого входа в систему по паролю** для приложения с **автоматическим определением полей входа в систему** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ca257-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="ca257-118">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="ca257-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ca257-119">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="ca257-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ca257-120">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ca257-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ca257-121">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ca257-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ca257-122">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="ca257-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ca257-123">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ca257-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ca257-124">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="ca257-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="ca257-125">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="ca257-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ca257-126">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="ca257-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ca257-127">Введите **URL-адрес для входа**.</span><span class="sxs-lookup"><span data-stu-id="ca257-127">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="ca257-128">Это URL-адрес страницы, на которой пользователи вводят имена и пароли для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="ca257-128">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="ca257-129">**Убедитесь, что на странице по этому URL-адресу отображаются поля для ввода учетных данных**.</span><span class="sxs-lookup"><span data-stu-id="ca257-129">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="ca257-130">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ca257-130">Click the **Save** button.</span></span>

11. <span data-ttu-id="ca257-131">Теперь этот URL-адрес будет автоматически использоваться для ввода имени пользователя и пароля и позволит использовать Azure AD для безопасной передачи паролей в приложение с помощью панели доступа в расширении обозревателя.</span><span class="sxs-lookup"><span data-stu-id="ca257-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="ca257-132">Определение полей входа в систему для приложения вручную</span><span class="sxs-lookup"><span data-stu-id="ca257-132">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="ca257-133">Для определения полей входа в систему вручную вам потребуется установить расширение "Панель доступа" для браузера. **Не работайте в приватном режиме, режиме inPrivate или в режиме инкогнито**.</span><span class="sxs-lookup"><span data-stu-id="ca257-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="ca257-134">Чтобы установить расширение браузера, выполните действия, описанные в разделе [Как установить расширение "Панель доступа" для браузера](#i-cannot-manually-detect-sign-in-fields-for-my-application).</span><span class="sxs-lookup"><span data-stu-id="ca257-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="ca257-135">Для настройки **единого входа в систему по паролю** для приложения с **определением полей входа в систему вручную** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ca257-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="ca257-136">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="ca257-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ca257-137">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="ca257-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ca257-138">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ca257-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ca257-139">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ca257-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ca257-140">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="ca257-140">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="ca257-141">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ca257-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ca257-142">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="ca257-142">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="ca257-143">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="ca257-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ca257-144">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="ca257-144">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ca257-145">Введите **URL-адрес для входа**.</span><span class="sxs-lookup"><span data-stu-id="ca257-145">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="ca257-146">Это URL-адрес страницы, на которой пользователи вводят имена и пароли для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="ca257-146">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="ca257-147">**Убедитесь, что на странице по этому URL-адресу отображаются поля для ввода учетных данных**.</span><span class="sxs-lookup"><span data-stu-id="ca257-147">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="ca257-148">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ca257-148">Click the **Save** button.</span></span>

11. <span data-ttu-id="ca257-149">Теперь этот URL-адрес будет автоматически использоваться для ввода имени пользователя и пароля и позволит использовать Azure AD для безопасной передачи паролей в приложение с помощью панели доступа в расширении обозревателя.</span><span class="sxs-lookup"><span data-stu-id="ca257-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="ca257-150">В случае неудачи можно **изменить режим определения полей на ручной**, перейдя к шагу 12.</span><span class="sxs-lookup"><span data-stu-id="ca257-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="ca257-151">Щелкните **Настроить параметры единого входа по паролю для &lt;имя_приложения&gt;**.</span><span class="sxs-lookup"><span data-stu-id="ca257-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="ca257-152">Выберите параметр **Определить поля входа в систему вручную**.</span><span class="sxs-lookup"><span data-stu-id="ca257-152">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="ca257-153">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ca257-153">Click **Ok**.</span></span>

15. <span data-ttu-id="ca257-154">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ca257-154">Click **Save**.</span></span>

16. <span data-ttu-id="ca257-155">Следуйте указаниям на экране по использованию панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ca257-155">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="ca257-156">Появляется сообщение об ошибке "Не удалось найти ни одного поля входа в систему на этой странице"</span><span class="sxs-lookup"><span data-stu-id="ca257-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="ca257-157">Эта ошибка возникает, если не удается определить поля входа в систему автоматически.</span><span class="sxs-lookup"><span data-stu-id="ca257-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="ca257-158">Чтобы устранить эту проблему, попробуйте определить поля входа в систему вручную, выполнив действия, описанные в статье [Определение полей входа в систему для приложения вручную](#how-to-manually-capture-sign-in-fields-for-an-application).</span><span class="sxs-lookup"><span data-stu-id="ca257-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="ca257-159">Появляется сообщение об ошибке "Невозможно сохранить конфигурацию единого входа"</span><span class="sxs-lookup"><span data-stu-id="ca257-159">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="ca257-160">В редких случаях обновление конфигурации единого входа может завершиться сбоем.</span><span class="sxs-lookup"><span data-stu-id="ca257-160">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="ca257-161">Чтобы решить эту проблему, попробуйте еще раз сохранить конфигурацию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ca257-161">TO resolve this try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="ca257-162">Если проблема возникает постоянно, создайте обращение в службу поддержки и укажите в нем сведения, полученные при выполнении инструкций в разделах [Как просмотреть сведения об уведомлении портала](#i-cannot-manually-detect-sign-in-fields-for-my-application) и [Как получить помощь, отправив сведения об уведомлении инженеру службы поддержки](#how-to-get-help-by-sending-notification-details-to-a-support-engineer).</span><span class="sxs-lookup"><span data-stu-id="ca257-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="ca257-163">Не удается определить поля входа в систему вручную для моего приложения</span><span class="sxs-lookup"><span data-stu-id="ca257-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="ca257-164">Ниже перечислены некоторые сценарии, в которых определить поля входа в систему вручную не удается:</span><span class="sxs-lookup"><span data-stu-id="ca257-164">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="ca257-165">Определение, на первый взгляд, работает, но определяются неправильные поля</span><span class="sxs-lookup"><span data-stu-id="ca257-165">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="ca257-166">В ходе определения не выделяются нужные поля</span><span class="sxs-lookup"><span data-stu-id="ca257-166">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="ca257-167">В процессе определения открывается страница входа в приложение, как и ожидалось, но ничего не происходит</span><span class="sxs-lookup"><span data-stu-id="ca257-167">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="ca257-168">Определение полей вручную работает, но когда пользователи переходят к приложению из панели доступа, единого входа не выполняется.</span><span class="sxs-lookup"><span data-stu-id="ca257-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="ca257-169">При наличии любой из этих проблем проверьте следующее:</span><span class="sxs-lookup"><span data-stu-id="ca257-169">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="ca257-170">Убедитесь, что **установлена** и **включена** последняя версия расширения панели доступа. Для этого выполните действия, приведенные в разделе [Как установить расширение "Панель доступа" для браузера](#how-to-install-the-access-panel-browser-extension).</span><span class="sxs-lookup"><span data-stu-id="ca257-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="ca257-171">Убедитесь, что во время отслеживания не включены **режим инкогнито, режим inPrivate или приватный режим**.</span><span class="sxs-lookup"><span data-stu-id="ca257-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="ca257-172">Расширение панели доступа не поддерживается в этих режимах.</span><span class="sxs-lookup"><span data-stu-id="ca257-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="ca257-173">Убедитесь, что пользователи не пытаются войти в приложение с панели доступа в **режиме инкогнито, режиме inPrivate или приватном режиме**.</span><span class="sxs-lookup"><span data-stu-id="ca257-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="ca257-174">Расширение панели доступа не поддерживается в этих режимах.</span><span class="sxs-lookup"><span data-stu-id="ca257-174">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="ca257-175">Попробуйте снова определить поля вручную, убедившись, что соответствующие поля помечены красными отметками.</span><span class="sxs-lookup"><span data-stu-id="ca257-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="ca257-176">Если процесс определения полей вручную зависает или на странице входа в систему не выполняется никаких действий (случай 3 выше), попробуйте снова определить поля вручную.</span><span class="sxs-lookup"><span data-stu-id="ca257-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="ca257-177">Но на этот раз после завершения процесса нажмите кнопку **F12**, чтобы открыть консоль разработчика браузера.</span><span class="sxs-lookup"><span data-stu-id="ca257-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="ca257-178">Откройте **консоль**, введите **window.location="&lt;URL-адрес входа, указанный при настройке приложения&gt;"** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="ca257-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="ca257-179">Это вызовет принудительный переход на указанную страницу, при этом процесс определения завершится, и найденные поля будут сохранены.</span><span class="sxs-lookup"><span data-stu-id="ca257-179">This force a page redirect which end the capture process and store the fields that have been captured.</span></span>

<span data-ttu-id="ca257-180">Если ни один из этих подходов не помогает, обратитесь к нам.</span><span class="sxs-lookup"><span data-stu-id="ca257-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="ca257-181">Создайте обращение в службу поддержки и подробно опишите свои действия, а также укажите сведения, полученные при выполнении инструкций в разделах [Как просмотреть сведения об уведомлении портала](#i-cannot-manually-detect-sign-in-fields-for-my-application) и [Как получить помощь, отправив сведения об уведомлении инженеру службы поддержки](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="ca257-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="ca257-182">Установка расширения "Панель доступа" для браузера</span><span class="sxs-lookup"><span data-stu-id="ca257-182">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="ca257-183">Чтобы установить расширение "Панель доступа" для браузера, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="ca257-183">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="ca257-184">Откройте [панель доступа](https://myapps.microsoft.com) в одном из поддерживаемых браузеров и войдите в систему как **пользователь** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca257-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="ca257-185">Щелкните **password-SSO application** (приложение с единым входом по паролю) на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ca257-185">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="ca257-186">При появлении запроса на установку программного обеспечения выберите **Установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="ca257-186">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="ca257-187">Откроется страница для скачивания расширения в зависимости от вашего браузера.</span><span class="sxs-lookup"><span data-stu-id="ca257-187">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="ca257-188">**Добавьте** расширение в свой браузер.</span><span class="sxs-lookup"><span data-stu-id="ca257-188">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="ca257-189">При необходимости **включите** или **разрешите** расширение.</span><span class="sxs-lookup"><span data-stu-id="ca257-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="ca257-190">После установки **перезапустите** сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="ca257-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="ca257-191">Войдите в панель доступа и посмотрите, можете ли вы **запустить** приложения с единым входом по паролю.</span><span class="sxs-lookup"><span data-stu-id="ca257-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="ca257-192">Чтобы скачать расширение для Chrome и Firefox, воспользуйтесь следующими ссылками:</span><span class="sxs-lookup"><span data-stu-id="ca257-192">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="ca257-193">Расширение "Панель доступа" для Chrome</span><span class="sxs-lookup"><span data-stu-id="ca257-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="ca257-194">Расширение "Панель доступа" для Firefox</span><span class="sxs-lookup"><span data-stu-id="ca257-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="ca257-195">Как просмотреть сведения об уведомлении портала</span><span class="sxs-lookup"><span data-stu-id="ca257-195">How to see the details of a portal notification</span></span>

<span data-ttu-id="ca257-196">Чтобы просмотреть сведения об уведомлении на портале, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ca257-196">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="ca257-197">Щелкните значок **Уведомления** (в форме колокольчика) в правом верхнем углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ca257-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="ca257-198">Выберите любое уведомление, которое находится в состоянии **Ошибка** (с красным восклицательным знаком (!)).</span><span class="sxs-lookup"><span data-stu-id="ca257-198">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="ca257-199">!Примечание] Не следует выбирать уведомления, которые находятся в состоянии **Успешно** или **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="ca257-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="ca257-200">Откроется колонка **Сведения об уведомлении**.</span><span class="sxs-lookup"><span data-stu-id="ca257-200">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="ca257-201">Используйте представленную здесь информацию, чтобы самостоятельно исследовать проблему.</span><span class="sxs-lookup"><span data-stu-id="ca257-201">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="ca257-202">Если этого будет недостаточно, вы можете передать эти сведения инженеру службы поддержки или сотруднику группы продуктов, которые помогут вам решить возникшую проблему.</span><span class="sxs-lookup"><span data-stu-id="ca257-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="ca257-203">Щелкните **значок** **копирования** справа от текстового поля **Копировать ошибку**, чтобы скопировать в буфер обмена все сведения об уведомлении, которые затем можно будет передать инженеру службы поддержки или сотруднику группы продуктов.</span><span class="sxs-lookup"><span data-stu-id="ca257-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="ca257-204">Как получить помощь, отправив сведения об уведомлении инженеру службы поддержки</span><span class="sxs-lookup"><span data-stu-id="ca257-204">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="ca257-205">Если вам нужна помощь, вы можете ускорить этот процесс, предоставив инженеру службы поддержки **все перечисленные ниже сведения**.</span><span class="sxs-lookup"><span data-stu-id="ca257-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="ca257-206">Для этого можно **сделать снимок экрана** или щелкнуть **значок копирования ошибки**, который находится справа от текстового поля **Скопировать ошибку**.</span><span class="sxs-lookup"><span data-stu-id="ca257-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="ca257-207">Объяснение сведений об уведомлении</span><span class="sxs-lookup"><span data-stu-id="ca257-207">Notification Details Explained</span></span>

<span data-ttu-id="ca257-208">Ниже объясняется, что означает каждый из элементов сведений об уведомлениях, и приведено несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="ca257-208">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="ca257-209">Основные элементы уведомления</span><span class="sxs-lookup"><span data-stu-id="ca257-209">Essential Notification Items</span></span>

-   <span data-ttu-id="ca257-210">**Заголовок** — описательное название уведомления.</span><span class="sxs-lookup"><span data-stu-id="ca257-210">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="ca257-211">Пример: **Настройки прокси приложения**.</span><span class="sxs-lookup"><span data-stu-id="ca257-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="ca257-212">**Описание** — текст с описанием результата операции.</span><span class="sxs-lookup"><span data-stu-id="ca257-212">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="ca257-213">Пример: **Введенный внутренний URL-адрес уже используется другим приложением**.</span><span class="sxs-lookup"><span data-stu-id="ca257-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="ca257-214">**Идентификатор уведомления** — уникальный идентификатор уведомления.</span><span class="sxs-lookup"><span data-stu-id="ca257-214">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="ca257-215">Пример: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**.</span><span class="sxs-lookup"><span data-stu-id="ca257-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="ca257-216">**Идентификатор запроса клиента** — идентификатор конкретного запроса, созданного браузером.</span><span class="sxs-lookup"><span data-stu-id="ca257-216">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="ca257-217">Пример: **302fd775-3329-4670-a9f3-bea37004f0bc**.</span><span class="sxs-lookup"><span data-stu-id="ca257-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="ca257-218">**Метка времени в формате UTC** — время создания уведомления, в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="ca257-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="ca257-219">Пример: **2017-03-23T19:50:43.7583681Z**.</span><span class="sxs-lookup"><span data-stu-id="ca257-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="ca257-220">**ИД внутренней транзакции** — внутренний идентификатор, который поможет нам найти ошибку в наших системах.</span><span class="sxs-lookup"><span data-stu-id="ca257-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="ca257-221">Пример: **71a2f329-ca29-402f-aa72-bc00a7aca603**.</span><span class="sxs-lookup"><span data-stu-id="ca257-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="ca257-222">**UPN** — пользователь, который выполнил операцию.</span><span class="sxs-lookup"><span data-stu-id="ca257-222">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="ca257-223">Пример: **tperkins@f128.info**.</span><span class="sxs-lookup"><span data-stu-id="ca257-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="ca257-224">**Идентификатор клиента** — уникальный идентификатор клиента, к которому относится пользователь, выполнивший операцию.</span><span class="sxs-lookup"><span data-stu-id="ca257-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="ca257-225">Пример: **7918d4b5-0442-4a97-be2d-36f9f9962ece**.</span><span class="sxs-lookup"><span data-stu-id="ca257-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="ca257-226">**ИД объекта пользователя** — уникальный идентификатор пользователя, выполнившего операцию.</span><span class="sxs-lookup"><span data-stu-id="ca257-226">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="ca257-227">Пример: **17f84be4-51f8-483a-b533-383791227a99**.</span><span class="sxs-lookup"><span data-stu-id="ca257-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="ca257-228">Дополнительные элементы уведомления с подробными сведениями</span><span class="sxs-lookup"><span data-stu-id="ca257-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="ca257-229">**Отображаемое имя** — отображаемое имя с более подробным описанием ошибки **(может быть пустым)**</span><span class="sxs-lookup"><span data-stu-id="ca257-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="ca257-230">Пример*: **Параметры прокси приложения**</span><span class="sxs-lookup"><span data-stu-id="ca257-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="ca257-231">**Состояние** — состояние уведомления</span><span class="sxs-lookup"><span data-stu-id="ca257-231">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="ca257-232">Пример*: **Сбой**</span><span class="sxs-lookup"><span data-stu-id="ca257-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="ca257-233">**Идентификатор объекта** — идентификатор объекта, для которого выполнялась операция **(может быть пустым)**</span><span class="sxs-lookup"><span data-stu-id="ca257-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="ca257-234">Пример: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**.</span><span class="sxs-lookup"><span data-stu-id="ca257-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="ca257-235">**Подробные сведения** — подробное описание результата операции.</span><span class="sxs-lookup"><span data-stu-id="ca257-235">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="ca257-236">Пример: **Внутренний URL-адрес http://bing.com/ является недопустимым, так как он уже используется**.</span><span class="sxs-lookup"><span data-stu-id="ca257-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="ca257-237">**Копировать ошибку** — щелкните **значок копирования** справа от текстового поля **Копировать ошибку**, чтобы скопировать в буфер обмена все сведения об уведомлении, которые можно передать инженеру службы поддержки или сотруднику группы продуктов.</span><span class="sxs-lookup"><span data-stu-id="ca257-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="ca257-238">Пример: ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="ca257-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca257-239">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca257-239">Next steps</span></span>
[<span data-ttu-id="ca257-240">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="ca257-240">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

