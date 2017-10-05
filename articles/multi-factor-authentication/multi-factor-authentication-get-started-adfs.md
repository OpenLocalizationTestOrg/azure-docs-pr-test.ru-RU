---
title: "Azure MFA: двухфакторная проверка подлинности и AD FS | Документация Майкрософт"
description: "Эта страница содержит сведения о службе Azure Multi-Factor Authentication, описывающие начало работы с Azure MFA и AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 28aede545c738137ff04257214e4a3f42792d85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="7a44a-103">Приступая к работе со службой Azure Multi-Factor Authentication и службами федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a44a-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="7a44a-104"><center>![Облако](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="7a44a-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="7a44a-105">Если в организации создана федерация локальной службы Active Directory со службой Azure Active Directory с помощью служб федерации Active Directory, доступны два варианта использования Многофакторной идентификации Azure.</span><span class="sxs-lookup"><span data-stu-id="7a44a-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="7a44a-106">Защита облачных ресурсов с помощью службы Azure Multi-Factor Authentication и служб федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a44a-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="7a44a-107">Защита облачных и локальных ресурсов с помощью сервера Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="7a44a-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="7a44a-108">В следующей таблице перечислены возможности проверки для защиты ресурсов с помощью Многофакторной идентификации Azure и служб федерации Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a44a-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="7a44a-109">Проверка для браузерных приложений</span><span class="sxs-lookup"><span data-stu-id="7a44a-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="7a44a-110">Проверка для небраузерных приложений</span><span class="sxs-lookup"><span data-stu-id="7a44a-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7a44a-111">Защита ресурсов Azure AD с помощью Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="7a44a-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="7a44a-112">Первый этап проверки выполняется локально с помощью служб федерации Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a44a-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="7a44a-113">Второй этап выполняется с использованием телефона для облачной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7a44a-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="7a44a-114">Защита ресурсов Azure AD с помощью служб федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a44a-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="7a44a-115">Первый этап проверки выполняется локально с помощью служб федерации Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a44a-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="7a44a-116">Второй этап выполняется локально путем обработки утверждения.</span><span class="sxs-lookup"><span data-stu-id="7a44a-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="7a44a-117">Разъяснения касательно паролей приложений для федеративных пользователей.</span><span class="sxs-lookup"><span data-stu-id="7a44a-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="7a44a-118">Пароли приложений проверяются с использованием облачной проверки подлинности и, следовательно, обходят федерацию.</span><span class="sxs-lookup"><span data-stu-id="7a44a-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="7a44a-119">Федерация активно используется только при настройке пароля приложения.</span><span class="sxs-lookup"><span data-stu-id="7a44a-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="7a44a-120">Параметры контроля доступа локальных клиентов не учитываются при использовании паролей приложений.</span><span class="sxs-lookup"><span data-stu-id="7a44a-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="7a44a-121">У вас нет возможности вести журнал локальной проверки подлинности для паролей приложений.</span><span class="sxs-lookup"><span data-stu-id="7a44a-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="7a44a-122">Отключение или удаление учетной записи может занять до 3 часов с учетом синхронизации каталогов, которая задерживает процесс отключения или удаления паролей приложений в облачном удостоверении.</span><span class="sxs-lookup"><span data-stu-id="7a44a-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a44a-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a44a-123">Next steps</span></span>
<span data-ttu-id="7a44a-124">Дополнительные сведения о настройке службы или сервера Многофакторной идентификации Azure с помощью служб федерации Active Directory см. в таких статьях:</span><span class="sxs-lookup"><span data-stu-id="7a44a-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span></span>

* [<span data-ttu-id="7a44a-125">Защита облачных ресурсов с помощью службы Azure Multi-Factor Authentication и служб AD FS</span><span class="sxs-lookup"><span data-stu-id="7a44a-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="7a44a-126">Защита облачных и локальных ресурсов с помощью сервера Azure Multi-Factor Authentication и сервера Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="7a44a-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="7a44a-127">Защита облачных и локальных ресурсов с помощью сервера Azure Multi-Factor Authentication и AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="7a44a-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
