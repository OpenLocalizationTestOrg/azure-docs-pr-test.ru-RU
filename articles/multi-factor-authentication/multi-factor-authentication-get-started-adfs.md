---
title: "aaaTwo шаг проверки и AD FS - многофакторной проверки Подлинности Azure | Документы Microsoft"
description: "Это страница hello Azure многофакторной проверки подлинности, описывающий, как tooget работу с Azure MFA и AD FS."
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
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="e92db-103">Приступая к работе со службой Azure Multi-Factor Authentication и службами федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="e92db-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="e92db-104"><center>![Облако](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="e92db-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="e92db-105">Если в организации создана федерация локальной службы Active Directory со службой Azure Active Directory с помощью служб федерации Active Directory, доступны два варианта использования Многофакторной идентификации Azure.</span><span class="sxs-lookup"><span data-stu-id="e92db-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="e92db-106">Защита облачных ресурсов с помощью службы Azure Multi-Factor Authentication и служб федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="e92db-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="e92db-107">Защита облачных и локальных ресурсов с помощью сервера Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e92db-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="e92db-108">Привет, в следующей таблице приведена сводка hello проверки взаимодействия между защищаемых ресурсов с помощью многофакторной проверки подлинности Azure и AD FS</span><span class="sxs-lookup"><span data-stu-id="e92db-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="e92db-109">Проверка для браузерных приложений</span><span class="sxs-lookup"><span data-stu-id="e92db-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="e92db-110">Проверка для небраузерных приложений</span><span class="sxs-lookup"><span data-stu-id="e92db-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e92db-111">Защита ресурсов Azure AD с помощью Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e92db-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="e92db-112">Первый шаг проверки Hello выполняется локально с помощью AD FS.</span><span class="sxs-lookup"><span data-stu-id="e92db-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="e92db-113">второй шаг Hello — по телефону, выполняются с помощью проверки подлинности в облаке.</span><span class="sxs-lookup"><span data-stu-id="e92db-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="e92db-114">Защита ресурсов Azure AD с помощью служб федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="e92db-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="e92db-115">Первый шаг проверки Hello выполняется локально с помощью AD FS.</span><span class="sxs-lookup"><span data-stu-id="e92db-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="e92db-116">второй шаг Hello — выполняется локально путем выполнения утверждения hello.</span><span class="sxs-lookup"><span data-stu-id="e92db-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="e92db-117">Разъяснения касательно паролей приложений для федеративных пользователей.</span><span class="sxs-lookup"><span data-stu-id="e92db-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="e92db-118">Пароли приложений проверяются с использованием облачной проверки подлинности и, следовательно, обходят федерацию.</span><span class="sxs-lookup"><span data-stu-id="e92db-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="e92db-119">Федерация активно используется только при настройке пароля приложения.</span><span class="sxs-lookup"><span data-stu-id="e92db-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="e92db-120">Параметры контроля доступа локальных клиентов не учитываются при использовании паролей приложений.</span><span class="sxs-lookup"><span data-stu-id="e92db-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="e92db-121">У вас нет возможности вести журнал локальной проверки подлинности для паролей приложений.</span><span class="sxs-lookup"><span data-stu-id="e92db-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="e92db-122">Отключение или удаление учетной записи может занять toothree часов для синхронизации каталогов, задержкой отключения/удаления пароли приложений в удостоверении облака hello.</span><span class="sxs-lookup"><span data-stu-id="e92db-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e92db-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e92db-123">Next steps</span></span>
<span data-ttu-id="e92db-124">Сведения о настройке многофакторной проверки подлинности Azure или hello сервера Azure Multi-factor Authentication с AD FS см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="e92db-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="e92db-125">Защита облачных ресурсов с помощью службы Azure Multi-Factor Authentication и служб AD FS</span><span class="sxs-lookup"><span data-stu-id="e92db-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="e92db-126">Защита облачных и локальных ресурсов с помощью сервера Azure Multi-Factor Authentication и сервера Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="e92db-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="e92db-127">Защита облачных и локальных ресурсов с помощью сервера Azure Multi-Factor Authentication и AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="e92db-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
