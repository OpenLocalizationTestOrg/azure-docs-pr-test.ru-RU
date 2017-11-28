---
title: "Добавление фирменной символики организации для определенного языка на страницу входа в Azure Active Directory | Документы Майкрософт"
description: "Узнайте, как добавить изображения фирменной символики и текст организации для определенных языков на страницу входа Azure."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="8e0ab-103">Добавление фирменной символики организации для определенного языка на страницу входа в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e0ab-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="8e0ab-104">Чтобы избежать путаницы, многие компании используют единый стиль оформления всех веб-сайтов и служб, которыми они управляют.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="8e0ab-105">Azure Active Directory предоставляет такую возможность, позволяя настроить внешний вид страницы входа, добавив на нее логотип организации и цветовые схемы.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="8e0ab-106">Страница входа: эта страница отображается при входе в Office 365 или другие веб-приложения, использующие Azure AD в качестве поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="8e0ab-107">На этой странице вводятся учетные данные.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="8e0ab-108">Настройка страницы входа для другого языка</span><span class="sxs-lookup"><span data-stu-id="8e0ab-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="8e0ab-109">Вы можете добавить на пользовательскую страницу входа элементы, зависящие от языка, только в том случае, если вы уже создали пользовательскую страницу входа, как описано в разделе [Добавление фирменной символики организации на страницу входа](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8e0ab-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="8e0ab-110">Можно настроить по одному набору настраиваемых элементов по умолчанию для страницы входа каждого каталога.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="8e0ab-111">Настроив набор элементов страницы по умолчанию, вы сможете настроить дополнительные версии для разных языков.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="8e0ab-112">Вы также можете смешивать разные элементы.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-112">You can also mix and match various elements.</span></span> <span data-ttu-id="8e0ab-113">Например, можно выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-113">For example, you could:</span></span>

* <span data-ttu-id="8e0ab-114">Создайте **изображение для страницы входа** по умолчанию, подходящее для всех языков, а затем создайте отдельные версии для английского и русского языков.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="8e0ab-115">Когда вы настроите в браузере эти языки (один или оба), отобразится соответствующее изображение. Для всех других языков отобразится изображение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="8e0ab-116">Настройте разные логотипы для организации (например, японскую и китайскую версии).</span><span class="sxs-lookup"><span data-stu-id="8e0ab-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="8e0ab-117">Мы рекомендуем использовать небольшое количество языковых версий, чтобы не усложнять обслуживание и не понижать производительность.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="8e0ab-118">**Добавление фирменной символики компании в ваш каталог:**</span><span class="sxs-lookup"><span data-stu-id="8e0ab-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="8e0ab-119">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="8e0ab-120">Выберите **Больше служб**, введите **Пользователи и группы** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="8e0ab-122">В колонке **Пользователи и группы** выберите **Корпоративная фирменная символика**.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="8e0ab-123">В колонке **Пользователи и группы — корпоративная фирменная символика** щелкните **Добавить язык**.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![Добавление элементов фирменной символики для определенного языка](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="8e0ab-125">Измените элементы, которые нужно настроить.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="8e0ab-126">Все элементы необязательные.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-126">All elements are optional.</span></span>
6. <span data-ttu-id="8e0ab-127">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-127">Click **Save**.</span></span>

<span data-ttu-id="8e0ab-128">Применение каких-либо изменений фирменной символики страницы входа может занять до одного часа.</span><span class="sxs-lookup"><span data-stu-id="8e0ab-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e0ab-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e0ab-129">Next steps</span></span>
[<span data-ttu-id="8e0ab-130">Добавление фирменной символики организации на страницу входа</span><span class="sxs-lookup"><span data-stu-id="8e0ab-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
