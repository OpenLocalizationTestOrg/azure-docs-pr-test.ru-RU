---
title: "Уведомления о подготовке учетных записей | Документация Майкрософт"
description: "Узнайте, как гарантированно получать уведомления о проблемах, которые требуют вашего внимания, путем включения уведомления о проблемах связанных с подготовкой пользователей."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: b99037fc28eca1a3ebffefb9e99991e74f52c9a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="a379c-103">Уведомления о подготовке учетных записей</span><span class="sxs-lookup"><span data-stu-id="a379c-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="a379c-104">С помощью подготовки пользователей можно автоматизировать процесс управления пользователями в сторонних приложениях SaaS.</span><span class="sxs-lookup"><span data-stu-id="a379c-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="a379c-105">Хотя этот процесс автоматизирован, время от времени ваше участие будет необходимо.</span><span class="sxs-lookup"><span data-stu-id="a379c-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="a379c-106">Например, когда истечет срок действия пароля учетной записи, которую вы настроили для обмена данными со сторонним приложением SaaS.</span><span class="sxs-lookup"><span data-stu-id="a379c-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="a379c-107">После включения уведомлений о подготовке учетных записей вы гарантированно будете получать уведомления о проблемах, связанных с подготовкой пользователей, которые требуют вашего внимания.</span><span class="sxs-lookup"><span data-stu-id="a379c-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="a379c-108">Вы можете включить или отключить уведомления о подготовке учетных записей во время подготовки пользователей в стороннем приложении SaaS.</span><span class="sxs-lookup"><span data-stu-id="a379c-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Подготовка пользователей][1] 

<span data-ttu-id="a379c-110">Чтобы включить уведомления о подготовке учетных записей, на странице **Подтверждение** установите соответствующий флажок и введите псевдоним электронной почты получателя.</span><span class="sxs-lookup"><span data-stu-id="a379c-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![Уведомления о подготовке учетных записей][2]

<span data-ttu-id="a379c-112">В качестве получателя можно указать список рассылки. Тем не менее следует отметить, что уведомление, отправляемое по электронной почте, содержит ссылки, доступные только администраторам Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a379c-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="a379c-113">Если уведомления о подготовке учетных записей включены, вы будете получать сообщения о критических проблемах, связанных с подготовкой пользователей.</span><span class="sxs-lookup"><span data-stu-id="a379c-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="a379c-114">Чтобы не перегружать почту, вы будете получать одно уведомление в день о каждом приложении SaaS, для которого включены уведомления по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="a379c-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="a379c-115">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="a379c-115">Related Articles</span></span>
* [<span data-ttu-id="a379c-116">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a379c-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a379c-117">Автоматическая подготовка пользователей и ее отзыв для приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="a379c-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="a379c-118">Настройка сопоставления атрибутов для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="a379c-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="a379c-119">Запись выражений для сопоставления атрибутов</span><span class="sxs-lookup"><span data-stu-id="a379c-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="a379c-120">Фильтры области для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="a379c-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="a379c-121">Автоматическая подготовка пользователей и групп из Azure Active Directory в приложениях с использованием SCIM</span><span class="sxs-lookup"><span data-stu-id="a379c-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="a379c-122">Список учебников по интеграции приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="a379c-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
