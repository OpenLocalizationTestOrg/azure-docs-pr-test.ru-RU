---
title: "Требования Azure AD и Active Directory для Azure RemoteApp | Документация Майкрософт"
description: "Узнайте, как настроить Active Directory для работы с Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="52974-103">Требования Azure AD + Active Directory для Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="52974-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="52974-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="52974-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="52974-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="52974-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="52974-106">Для гибридной коллекции Azure RemoteApp или для облачной коллекции, которую необходимо включить в федерацию, используя AD Connect, вам потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="52974-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="52974-107">Подключите Azure AD и Active Directory</span><span class="sxs-lookup"><span data-stu-id="52974-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="52974-108">Для подключения к клиенту Azure AD и вашей локальной среде Active Directory используйте AD Connect.</span><span class="sxs-lookup"><span data-stu-id="52974-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="52974-109">Подключение двух каталогов можно выполнить всего за [4 щелчка](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) .</span><span class="sxs-lookup"><span data-stu-id="52974-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="52974-110">Примечание. Для гибридных коллекций требуется синхронизация службы каталогов.</span><span class="sxs-lookup"><span data-stu-id="52974-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="52974-111">Проверка соответствия @domain.com</span><span class="sxs-lookup"><span data-stu-id="52974-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="52974-112">Перед началом работы убедитесь, что имя участника-пользователя для локального леса соответствует суффиксу домена Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52974-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="52974-113">После настройки доменного суффикса имени участника-пользователя в Azure AD все пользователи, выполняющие вход в Azure RemoteApp, будут входить в систему как user@<the suffix you set up>.</span><span class="sxs-lookup"><span data-stu-id="52974-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="52974-114">Убедитесь, что пользователи также могут входить с помощью аналогичного имени user@suffix в локальный домен.</span><span class="sxs-lookup"><span data-stu-id="52974-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="52974-115">В некоторых случаях можно настроить одно доменное имя в Azure AD несмотря на то, что локально для пользователя указан другой суффикс домена.</span><span class="sxs-lookup"><span data-stu-id="52974-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="52974-116">В этом случае пользователи не будет возможность подключения к компьютерам, подключенным к домену, или ресурсам через Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="52974-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="52974-117">Например, если вы настроили доменный суффикс своего имени участника-пользователя в AAD как contoso.com, однако некоторые пользователи из локальной сети или домена приложения настроены для входа в систему с помощью @contoso.uk, то они не смогут корректно войти в коллекцию ARA.</span><span class="sxs-lookup"><span data-stu-id="52974-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="52974-118">Для выполнения входа в систему имена участников-пользователей в AAD и AD должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="52974-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="52974-119">Создайте объекты для Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="52974-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="52974-120">Кроме того, необходимо создать следующие локальные объекты Active Directory:</span><span class="sxs-lookup"><span data-stu-id="52974-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="52974-121">Учетная запись службы для предоставления доступа к доменным ресурсам программ RemoteApp путем соединения конечных точек RDSH с локальным доменом.</span><span class="sxs-lookup"><span data-stu-id="52974-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="52974-122">Подразделение для хранения объектов машин RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="52974-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="52974-123">Использовать подразделение рекомендуется (но не требуется) для изолирования учетных записей и политик, которые будут использоваться с RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="52974-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="52974-124">При создании коллекции RemoteApp требуются оба этих объекта, поэтому сначала выполните указанные действия.</span><span class="sxs-lookup"><span data-stu-id="52974-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

