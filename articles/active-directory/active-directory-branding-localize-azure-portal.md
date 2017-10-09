---
title: "зависящие от языка фирменная tooyour на странице входа в Azure Active Directory hello aaaAdd | Документы Microsoft"
description: "Узнайте, как компании tooadd конкретного языка фирменной символики изображения и текст страницы tooan Azure вход"
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
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="f7366-103">Добавление фирменной символики tooyour на странице входа в Azure Active Directory hello компании конкретного языка</span><span class="sxs-lookup"><span data-stu-id="f7366-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="f7366-104">tooavoid путаницы, многие компании хотят tooapply согласованного внешнего вида и поведения во всех веб-сайтов hello и службах, которыми они управляют.</span><span class="sxs-lookup"><span data-stu-id="f7366-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="f7366-105">Azure Active Directory предоставляет эту возможность, позволяя toocustomize hello вида hello-на страницу входа с эмблемой компании и пользовательские цветовые схемы.</span><span class="sxs-lookup"><span data-stu-id="f7366-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="f7366-106">Hello входа является страница hello, отображается при входе в tooOffice 365 или другие веб-приложения, использующие Azure AD как поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f7366-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="f7366-107">Взаимодействие с этой страницы tooenter учетные данные.</span><span class="sxs-lookup"><span data-stu-id="f7366-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="f7366-108">Настройка hello-на страницу входа для другого языка</span><span class="sxs-lookup"><span data-stu-id="f7366-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="f7366-109">Элементы языка tooyour пользовательской страницы входа можно добавить только в том случае, если вы уже создали пользовательской страницы входа в систему как описано в [добавить корпоративную фирменную символику страницы входа tooyour](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f7366-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="f7366-110">Можно настроить по одному набору настраиваемых элементов по умолчанию для страницы входа каждого каталога.</span><span class="sxs-lookup"><span data-stu-id="f7366-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="f7366-111">После настройки по умолчанию hello набор элементов страницы, можно настроить дополнительные версии для разных языков.</span><span class="sxs-lookup"><span data-stu-id="f7366-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="f7366-112">Вы также можете смешивать разные элементы.</span><span class="sxs-lookup"><span data-stu-id="f7366-112">You can also mix and match various elements.</span></span> <span data-ttu-id="f7366-113">Например, можно выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="f7366-113">For example, you could:</span></span>

* <span data-ttu-id="f7366-114">Создайте **изображение для страницы входа** по умолчанию, подходящее для всех языков, а затем создайте отдельные версии для английского и русского языков.</span><span class="sxs-lookup"><span data-stu-id="f7366-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="f7366-115">При установке вашей tooone браузеров из этих двух языков hello конкретного языка изображение, а рисунке hello по умолчанию для всех языков.</span><span class="sxs-lookup"><span data-stu-id="f7366-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="f7366-116">Настройте разные логотипы для организации (например, японскую и китайскую версии).</span><span class="sxs-lookup"><span data-stu-id="f7366-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="f7366-117">Рекомендуется сохранять hello количество вариантов языка низкое значение, по соображениям производительности и обслуживания.</span><span class="sxs-lookup"><span data-stu-id="f7366-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="f7366-118">**каталог tooadd компании фирменной символики tooyour:**</span><span class="sxs-lookup"><span data-stu-id="f7366-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="f7366-119">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="f7366-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="f7366-120">Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="f7366-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="f7366-122">На hello **пользователей и групп** колонке выберите **фирменная символика компании**.</span><span class="sxs-lookup"><span data-stu-id="f7366-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="f7366-123">На hello **пользователей и групп - фирменная символика компании** колонки, выберите hello **добавить язык** команды.</span><span class="sxs-lookup"><span data-stu-id="f7366-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![Добавление элементов фирменной символики для определенного языка](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="f7366-125">Изменение элементов hello, требуется toocustomize.</span><span class="sxs-lookup"><span data-stu-id="f7366-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="f7366-126">Все элементы необязательные.</span><span class="sxs-lookup"><span data-stu-id="f7366-126">All elements are optional.</span></span>
6. <span data-ttu-id="f7366-127">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f7366-127">Click **Save**.</span></span>

<span data-ttu-id="f7366-128">Для изменения, внесенные toohello входа страницы фирменной символики tooappear может занять час tooan.</span><span class="sxs-lookup"><span data-stu-id="f7366-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7366-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7366-129">Next steps</span></span>
[<span data-ttu-id="f7366-130">Добавить корпоративную фирменную символику страницы входа tooyour</span><span class="sxs-lookup"><span data-stu-id="f7366-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
