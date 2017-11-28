---
title: "Azure Active Directory B2C: самостоятельный сброс пароля | Документация Майкрософт"
description: "Статья о том, как настроить самостоятельный сброс пароля для потребителей в Azure Active Directory B2C."
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
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="11222-103">Azure Active Directory B2C: настройка самостоятельного сброса пароля для потребителей</span><span class="sxs-lookup"><span data-stu-id="11222-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="11222-104">С помощью функции самостоятельного сброса пароля ваши потребители (которые зарегистрировали локальные учетные записи) могут самостоятельно сбрасывать пароли.</span><span class="sxs-lookup"><span data-stu-id="11222-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="11222-105">Это значительно упрощает работу службы поддержки, особенно если вашим приложением регулярно пользуются миллионы клиентов.</span><span class="sxs-lookup"><span data-stu-id="11222-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="11222-106">В настоящее время поддерживается только восстановление с помощью подтвержденного адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="11222-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="11222-107">В будущем мы добавим другие способы восстановления (подтвержденный номер телефона, секретные вопросы и т. д.).</span><span class="sxs-lookup"><span data-stu-id="11222-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="11222-108">Эта статья относится к самостоятельному сбросу пароля, используемому в контексте политики входа в систему.</span><span class="sxs-lookup"><span data-stu-id="11222-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="11222-109">Если вам нужны полностью настраиваемые политики сброса пароля, вызываемые из вашего приложения, см. [эту статью](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="11222-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="11222-110">По умолчанию в каталоге самостоятельный сброс пароля отключен.</span><span class="sxs-lookup"><span data-stu-id="11222-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="11222-111">Чтобы включить его, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="11222-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="11222-112">Войдите на [классический портал Azure](https://manage.windowsazure.com/) под именем администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="11222-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="11222-113">Это рабочая или учебная учетная запись либо учетная запись Майкрософт, которая использовалась для создания каталога.</span><span class="sxs-lookup"><span data-stu-id="11222-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="11222-114">Перейдите к расширению Active Directory в области навигации слева.</span><span class="sxs-lookup"><span data-stu-id="11222-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="11222-115">Найдите свой каталог на вкладке **Каталог** и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="11222-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="11222-116">Выберите вкладку **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="11222-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="11222-117">Прокрутите вниз до раздела **Политика сброса пароля пользователя** и выберите для параметра **Пользователям разрешен сброс пароля** значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="11222-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="11222-118">Обратите внимание, что включен параметр **Запасной адрес электронной почты**. Оставьте его без изменений.</span><span class="sxs-lookup"><span data-stu-id="11222-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Самостоятельный сброс пароля](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="11222-120">В нижней части страницы нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="11222-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="11222-121">Готово!</span><span class="sxs-lookup"><span data-stu-id="11222-121">You're done!</span></span>

<span data-ttu-id="11222-122">Проверьте любую политику входа (где в качестве поставщика удостоверений используются локальные учетные записи) с помощью функции "Запустить сейчас".</span><span class="sxs-lookup"><span data-stu-id="11222-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="11222-123">На странице входа локальной учетной записи (где вы вводите электронный адрес и пароль или имя пользователя и пароль) щелкните **Не удается получить доступ к своей учетной записи?** , чтобы проверить взаимодействие с потребителем.</span><span class="sxs-lookup"><span data-stu-id="11222-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="11222-124">Страницы самостоятельного сброса пароля можно настраивать с помощью [функции фирменной символики](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="11222-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

