---
title: "вход в систему страницы в Azure Active Directory hello aaaCustomize | Документы Microsoft"
description: "Узнайте, как tooadd toohello Azure вход страницы фирменной символики компании"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="7e9da-103">Добавить корпоративную фирменную символику tooyour на странице входа в Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="7e9da-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="7e9da-104">tooavoid путаницы, многие компании хотят tooapply согласованного внешнего вида и поведения во всех веб-сайтов hello и службах, которыми они управляют.</span><span class="sxs-lookup"><span data-stu-id="7e9da-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="7e9da-105">Azure Active Directory предоставляет эту возможность, позволяя toocustomize hello вида hello-на страницу входа с эмблемой компании и пользовательские цветовые схемы.</span><span class="sxs-lookup"><span data-stu-id="7e9da-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="7e9da-106">Hello входа является страница hello, отображается при входе в tooOffice 365 или другие веб-приложения, использующие Azure AD как поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7e9da-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="7e9da-107">Взаимодействие с этой страницы tooenter учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7e9da-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="7e9da-108">Если требуется tooshow фирменного стиля организации, цвета и другие настраиваемые элементы на этой странице, см. следующие образы toounderstand hello разницу между двумя интерфейсами hello hello.</span><span class="sxs-lookup"><span data-stu-id="7e9da-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="7e9da-109">Здравствуйте, следующие снимке экрана показано и пример для hello Office 365 на странице входа на настольном компьютере **перед** настройки:</span><span class="sxs-lookup"><span data-stu-id="7e9da-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Страница входа в службу Office 365 перед настройкой](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="7e9da-111">Здравствуйте, следующие снимке экрана показано и пример для hello Office 365 на странице входа на настольном компьютере **после** настройки:</span><span class="sxs-lookup"><span data-stu-id="7e9da-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Страница входа в службу Office 365 после настройки](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="7e9da-113">Настройка страницы входа hello</span><span class="sxs-lookup"><span data-stu-id="7e9da-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="7e9da-114">Как правило если вам требуется доступ на основе браузера tooyour облачных приложений и служб, которые подписана ваша организация, используйте hello-на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="7e9da-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="7e9da-115">При применении изменений tooyour на странице входа, может занять час tooan для изменения tooappear hello.</span><span class="sxs-lookup"><span data-stu-id="7e9da-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="7e9da-116">Страница входа с фирменной символикой отображается, только если службу посещают с помощью URL-адреса конкретного клиента, например https://outlook.com/**contoso**.com или https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="7e9da-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="7e9da-117">Если службу посещают без URL-адресов конкретного клиента (например, https://mail.office365.com), отображается страница входа без фирменной символики.</span><span class="sxs-lookup"><span data-stu-id="7e9da-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="7e9da-118">Символика появится, когда вы введете идентификатор пользователя или выберете элемент пользователя.</span><span class="sxs-lookup"><span data-stu-id="7e9da-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="7e9da-119">Имя домена должно иметь состояние «Активный» в hello **домены** часть hello портал Azure, в котором была настроена фирменная символика.</span><span class="sxs-lookup"><span data-stu-id="7e9da-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="7e9da-120">Дополнительные сведения см. в статье [Добавление имени личного домена в предварительной версии Azure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7e9da-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="7e9da-121">Фирменная символика страницы входа в систему не переносятся toohello входа потребителя в корпорации Майкрософт на странице.</span><span class="sxs-lookup"><span data-stu-id="7e9da-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="7e9da-122">Если выполнить вход с учетной записью Майкрософт, может появиться список плиток пользователей, подготовленный Azure AD с фирменной символикой, но hello фирменная символика организации не применяется toohello Microsoft учетную запись на странице входа.</span><span class="sxs-lookup"><span data-stu-id="7e9da-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="7e9da-123">На странице входа, hello **оставаться в системе** флажок позволяет tooremain пользователя, когда они закрыть и снова открыть браузер выполнил вход.</span><span class="sxs-lookup"><span data-stu-id="7e9da-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![Оставаться в системе](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="7e9da-125">Он не влияет на время существования сеанса.</span><span class="sxs-lookup"><span data-stu-id="7e9da-125">It does not effect session lifetime.</span></span> <span data-ttu-id="7e9da-126">Можно скрыть hello флажок на странице входа в Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="7e9da-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="7e9da-127">Должно ли отображаться флажок hello определяется параметром hello **Запомнить меня отключено**.</span><span class="sxs-lookup"><span data-stu-id="7e9da-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![Оставаться в системе](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="7e9da-129">toohide Здравствуйте флажок, настройте этот параметр, слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="7e9da-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="7e9da-130">Некоторые функции SharePoint Online и Office 2010 зависят от пользователей, это поле может toocheck.</span><span class="sxs-lookup"><span data-stu-id="7e9da-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="7e9da-131">Если задан этот параметр toohidden вашей пользователи могут видеть дополнительные и непредвиденный запрос toosign в.</span><span class="sxs-lookup"><span data-stu-id="7e9da-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="7e9da-132">**каталог tooadd компании фирменной символики tooyour:**</span><span class="sxs-lookup"><span data-stu-id="7e9da-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="7e9da-133">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="7e9da-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="7e9da-134">Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7e9da-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="7e9da-136">На hello **пользователей и групп** колонке выберите **фирменная символика компании**.</span><span class="sxs-lookup"><span data-stu-id="7e9da-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="7e9da-137">На hello **пользователей и групп - фирменная символика компании** колонки, выберите hello **изменить** команды.</span><span class="sxs-lookup"><span data-stu-id="7e9da-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![Изменение пользовательской фирменной символики](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="7e9da-139">Изменение элементов hello, требуется toocustomize.</span><span class="sxs-lookup"><span data-stu-id="7e9da-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="7e9da-140">Все элементы необязательные.</span><span class="sxs-lookup"><span data-stu-id="7e9da-140">All elements are optional.</span></span>
6. <span data-ttu-id="7e9da-141">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7e9da-141">Click **Save**.</span></span>

<span data-ttu-id="7e9da-142">Для изменения, внесенные toohello входа страницы фирменной символики tooappear может занять час tooan.</span><span class="sxs-lookup"><span data-stu-id="7e9da-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e9da-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7e9da-143">Next steps</span></span>
[<span data-ttu-id="7e9da-144">Добавление фирменной символики компании для конкретного языка</span><span class="sxs-lookup"><span data-stu-id="7e9da-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
