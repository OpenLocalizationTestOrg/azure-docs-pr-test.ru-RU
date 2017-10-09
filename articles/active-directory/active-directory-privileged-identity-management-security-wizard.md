---
title: "Мастер безопасности aaaThe Azure AD Privileged Identity Management"
description: "Hello первом использовании модуля Azure Active Directory Privileged Identity Management hello, откроется мастер, с помощью системы безопасности. В этой статье описаны шаги hello по с помощью мастера hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="59066-104">С помощью мастера безопасности hello в Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="59066-104">Using hello security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="59066-105">Если вы первый toorun лица hello управления привилегированных удостоверений Azure (PIM) для вашей организации, вам будут представлены с помощью мастера.</span><span class="sxs-lookup"><span data-stu-id="59066-105">If you're hello first person toorun Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="59066-106">Hello мастер поможет вам понять рисков безопасности hello привилегированных удостоверений и как toouse PIM tooreduce этих рисков.</span><span class="sxs-lookup"><span data-stu-id="59066-106">hello wizard helps you understand hello security risks of privileged identities and how toouse PIM tooreduce those risks.</span></span> <span data-ttu-id="59066-107">Не требуется toomake изменения назначения ролей, tooexisting в мастере приветствия при желании toodo его позже.</span><span class="sxs-lookup"><span data-stu-id="59066-107">You don't need toomake any changes tooexisting role assignments in hello wizard, if you prefer toodo it later.</span></span>

## <a name="what-tooexpect"></a><span data-ttu-id="59066-108">Какие tooexpect</span><span class="sxs-lookup"><span data-stu-id="59066-108">What tooexpect</span></span>
<span data-ttu-id="59066-109">Перед началом вашей организации с помощью PIM все назначения ролей являются постоянными: hello пользователи всегда находятся в этих ролей, даже если они не обязательно в настоящее время свои права доступа.</span><span class="sxs-lookup"><span data-stu-id="59066-109">Before your organization starts using PIM, all role assignments are permanent: hello users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="59066-110">Первый шаг Hello приветствия мастера показывает список ролей с высоким уровнем привилегий и число пользователей, в настоящее время эти роли.</span><span class="sxs-lookup"><span data-stu-id="59066-110">hello first step of hello wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="59066-111">Вы можете перейти к toolearn определенной роли tooa более о пользователях, если один или несколько из них не знакомы.</span><span class="sxs-lookup"><span data-stu-id="59066-111">You can drill in tooa particular role toolearn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="59066-112">второй шаг мастера hello Hello дает назначение ролей администратора toochange возможных сделок.</span><span class="sxs-lookup"><span data-stu-id="59066-112">hello second step of hello wizard gives you an opportunity toochange administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="59066-113">Очень важно иметь как минимум одного глобального администратора и несколько администраторов привилегированных ролей с учетной записью организации (не учетной записью Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="59066-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="59066-114">Если имеется только один администратор привилегированной роли, hello организации не будет возможности toomanage PIM, если удалить эту учетную запись.</span><span class="sxs-lookup"><span data-stu-id="59066-114">If there is only one privileged role administrator, hello organization will not be able toomanage PIM if that account is deleted.</span></span>
> <span data-ttu-id="59066-115">Кроме того имейте назначения ролей постоянной, если пользователь имеет учетную запись Майкрософт (учетная запись, как они используют toosign в tooMicrosoft служб, таких как Скайп и Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="59066-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use toosign in tooMicrosoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="59066-116">Если планируется toorequire MFA для активации для этой роли, этот пользователь будет заблокирован.</span><span class="sxs-lookup"><span data-stu-id="59066-116">If you plan toorequire MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="59066-117">После внесения изменений, мастер приветствия больше не будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="59066-117">After you have made changes, hello wizard will no longer show up.</span></span> <span data-ttu-id="59066-118">Hello очередном вы или другой привилегированной роли администратора используйте PIM, вы увидите панель мониторинга PIM hello.</span><span class="sxs-lookup"><span data-stu-id="59066-118">hello next time you or another privileged role administrator use PIM, you will see hello PIM dashboard.</span></span>  

* <span data-ttu-id="59066-119">Если бы как tooadd или удалять пользователей из ролей или измените назначения с постоянными tooeligible, ознакомьтесь с дополнительными на [как tooadd и удаление роли пользователя](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="59066-119">If you would like tooadd or remove users from roles or change assignments from permanent tooeligible, read more at [how tooadd or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="59066-120">Если вы хотите toogive больше пользователей, доступ к toomanage PIM, ознакомьтесь с дополнительными в [как toogive доступ к toomanage в PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="59066-120">If you would like toogive more users access toomanage PIM, read more at [how toogive access toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="59066-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59066-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

