---
title: "Настройка страницы входа в Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как добавить фирменную символику организации на страницу входа в Azure."
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
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="50abb-103">Добавление фирменной символики организации на страницу входа в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50abb-103">Add company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="50abb-104">Чтобы избежать путаницы, многие компании используют единый стиль оформления всех веб-сайтов и служб, которыми они управляют.</span><span class="sxs-lookup"><span data-stu-id="50abb-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="50abb-105">Azure Active Directory предоставляет такую возможность, позволяя настроить внешний вид страницы входа, добавив на нее логотип организации и цветовые схемы.</span><span class="sxs-lookup"><span data-stu-id="50abb-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="50abb-106">Страница входа: эта страница отображается при входе в Office 365 или другие веб-приложения, использующие Azure AD в качестве поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="50abb-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="50abb-107">На этой странице вводятся учетные данные.</span><span class="sxs-lookup"><span data-stu-id="50abb-107">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="50abb-108">Если вы хотите показать фирменную символику, цвета и другие настраиваемые элементы на этой странице, изучите следующие изображения, чтобы понять разницу между двумя интерфейсами.</span><span class="sxs-lookup"><span data-stu-id="50abb-108">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="50abb-109">На следующем снимке экрана приведен пример страницы входа в Office 365 на настольном компьютере **перед** настройкой.</span><span class="sxs-lookup"><span data-stu-id="50abb-109">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Страница входа в службу Office 365 перед настройкой](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="50abb-111">На следующем снимке экрана приведен пример страницы входа в Office 365 на настольном компьютере **после** настройки.</span><span class="sxs-lookup"><span data-stu-id="50abb-111">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Страница входа в службу Office 365 после настройки](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="50abb-113">Настройка страницы входа</span><span class="sxs-lookup"><span data-stu-id="50abb-113">Customizing the sign-in page</span></span>
<span data-ttu-id="50abb-114">Как правило, страница входа используется для доступа через веб-браузер к облачным приложениям и службам, на которые у вашей организации есть подписка.</span><span class="sxs-lookup"><span data-stu-id="50abb-114">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="50abb-115">Когда вы что-то меняете на странице входа, может потребоваться до одного часа, чтобы эти изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="50abb-115">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="50abb-116">Страница входа с фирменной символикой отображается, только если службу посещают с помощью URL-адреса конкретного клиента, например https://outlook.com/**contoso**.com или https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="50abb-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="50abb-117">Если службу посещают без URL-адресов конкретного клиента (например, https://mail.office365.com), отображается страница входа без фирменной символики.</span><span class="sxs-lookup"><span data-stu-id="50abb-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="50abb-118">Символика появится, когда вы введете идентификатор пользователя или выберете элемент пользователя.</span><span class="sxs-lookup"><span data-stu-id="50abb-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="50abb-119">Для доменного имени в части портала Azure **Домены**, в которой была настроена фирменная символика, должно отображаться состояние "Активно".</span><span class="sxs-lookup"><span data-stu-id="50abb-119">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="50abb-120">Дополнительные сведения см. в статье [Добавление имени личного домена в предварительной версии Azure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50abb-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="50abb-121">Фирменная символика страницы входа не применяется к странице входа пользователя корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="50abb-121">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="50abb-122">Если вы входите с использованием учетной записи Майкрософт, то вы можете увидеть список элементов пользователей с фирменной символикой, отображаемый в Azure AD. Но к странице входа в учетную запись Майкрософт это оформление применяться не будет.</span><span class="sxs-lookup"><span data-stu-id="50abb-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="50abb-123">Если на странице входа установить флажок **Оставаться в системе**,пользователь сможет остаться в системе, даже когда он закроет и повторно откроет браузер.</span><span class="sxs-lookup"><span data-stu-id="50abb-123">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![Оставаться в системе](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="50abb-125">Он не влияет на время существования сеанса.</span><span class="sxs-lookup"><span data-stu-id="50abb-125">It does not effect session lifetime.</span></span> <span data-ttu-id="50abb-126">Этот флажок можно скрыть на странице входа в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="50abb-126">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="50abb-127">Для этого используется параметр **Возможность оставаться в системе отключена**.</span><span class="sxs-lookup"><span data-stu-id="50abb-127">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![Оставаться в системе](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="50abb-129">Чтобы скрыть флажок, задайте для этого параметра значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="50abb-129">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="50abb-130">Некоторые функции SharePoint Online и Office 2010 зависят от возможности пользователей установить этот флажок.</span><span class="sxs-lookup"><span data-stu-id="50abb-130">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="50abb-131">Если вы скроете этот параметр, пользователи могут получать дополнительные или непредвиденные запросы на вход в систему.</span><span class="sxs-lookup"><span data-stu-id="50abb-131">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="50abb-132">**Добавление фирменной символики компании в ваш каталог:**</span><span class="sxs-lookup"><span data-stu-id="50abb-132">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="50abb-133">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="50abb-133">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="50abb-134">Выберите **Больше служб**, введите **Пользователи и группы** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="50abb-134">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="50abb-136">В колонке **Пользователи и группы** выберите **Корпоративная фирменная символика**.</span><span class="sxs-lookup"><span data-stu-id="50abb-136">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="50abb-137">В колонке **Корпоративная фирменная символика** щелкните **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="50abb-137">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![Изменение пользовательской фирменной символики](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="50abb-139">Измените элементы, которые нужно настроить.</span><span class="sxs-lookup"><span data-stu-id="50abb-139">Modify the elements you want to customize.</span></span> <span data-ttu-id="50abb-140">Все элементы необязательные.</span><span class="sxs-lookup"><span data-stu-id="50abb-140">All elements are optional.</span></span>
6. <span data-ttu-id="50abb-141">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="50abb-141">Click **Save**.</span></span>

<span data-ttu-id="50abb-142">Применение каких-либо изменений фирменной символики страницы входа может занять до одного часа.</span><span class="sxs-lookup"><span data-stu-id="50abb-142">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50abb-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50abb-143">Next steps</span></span>
[<span data-ttu-id="50abb-144">Добавление фирменной символики компании для конкретного языка</span><span class="sxs-lookup"><span data-stu-id="50abb-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
