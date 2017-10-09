---
title: "Azure Active Directory B2C: самостоятельный сброс пароля | Документация Майкрософт"
description: "Статьи, демонстрации, переустановка tooset пароль самообслуживания для потребителей в Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="e2030-103">Azure Active Directory B2C: настройка самостоятельного сброса пароля для потребителей</span><span class="sxs-lookup"><span data-stu-id="e2030-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="e2030-104">С hello самостоятельный сброс пароля компонент, потребителей (которые зарегистрировались для локальных учетных записей) могут сбрасывать пароли самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="e2030-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="e2030-105">Это значительно уменьшает нагрузку hello на сотруднику службы поддержки, особенно в том случае, если приложение имеет миллионы потребителям, использующим ее на регулярной основе.</span><span class="sxs-lookup"><span data-stu-id="e2030-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="e2030-106">В настоящее время поддерживается только восстановление с помощью подтвержденного адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="e2030-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="e2030-107">Мы добавим в будущем hello восстановления дополнительных методов (проверенных телефонный номер, вопросы, касающиеся безопасности, т. д.).</span><span class="sxs-lookup"><span data-stu-id="e2030-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="e2030-108">Эта статья относится пароль службы tooself сброса используется в контексте hello политики входа в систему.</span><span class="sxs-lookup"><span data-stu-id="e2030-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="e2030-109">Если вам нужны полностью настраиваемые политики сброса пароля, вызываемые из вашего приложения, см. [эту статью](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="e2030-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="e2030-110">По умолчанию в каталоге самостоятельный сброс пароля отключен.</span><span class="sxs-lookup"><span data-stu-id="e2030-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="e2030-111">Используйте hello следующие шаги tooturn ее на:</span><span class="sxs-lookup"><span data-stu-id="e2030-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="e2030-112">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) как hello администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="e2030-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="e2030-113">Это hello, или же работы рабочей учетной записи или hello учетная запись Майкрософт используется toocreate вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="e2030-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="e2030-114">Перейдите toohello расширение Active Directory на панели навигации hello в левой части hello.</span><span class="sxs-lookup"><span data-stu-id="e2030-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="e2030-115">Найти в каталоге hello **каталог** и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="e2030-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="e2030-116">Нажмите кнопку hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="e2030-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="e2030-117">Прокрутите вниз toohello **политика сброса пароля пользователя** раздел и переключить hello **пользователям разрешен сброс пароля** параметр слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="e2030-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="e2030-118">Обратите внимание, что hello **запасной адрес электронной почты** флажок; оставить его состоянии.</span><span class="sxs-lookup"><span data-stu-id="e2030-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Самостоятельный сброс пароля](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="e2030-120">Нажмите кнопку **Сохранить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="e2030-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="e2030-121">Готово!</span><span class="sxs-lookup"><span data-stu-id="e2030-121">You're done!</span></span>

<span data-ttu-id="e2030-122">tootest функцию «Запуск» используйте hello на все учетное политики с локальных учетных записей, что поставщик удостоверений.</span><span class="sxs-lookup"><span data-stu-id="e2030-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="e2030-123">На hello локальной учетной записи входа в странице (где можно ввести адрес электронной почты и пароль, или имя пользователя и пароль), щелкните **не может получить доступ к вашей учетной записи?** возможности использования tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="e2030-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="e2030-124">Hello страницы сброса паролей можно настроить с помощью hello [функция фирменной символики компании](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="e2030-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

