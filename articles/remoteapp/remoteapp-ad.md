---
title: "aaaAzure AD + требования Active Directory для Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooset копирование toowork Active Directory с Azure RemoteApp."
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
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="a5961-103">Требования Azure AD + Active Directory для Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a5961-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a5961-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="a5961-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a5961-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="a5961-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a5961-106">Для вашей коллекции Azure RemoteApp гибридного или облачной коллекции, которые должны toofederate, с помощью AD Connect необходимо следующее toodo hello.</span><span class="sxs-lookup"><span data-stu-id="a5961-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="a5961-107">Подключите Azure AD и Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5961-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="a5961-108">Если требуется tooconnect вашего клиента Azure AD и вашей локальной среде Active Directory, используйте AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a5961-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="a5961-109">Он будет открыт только [4 щелчков](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello двух каталогов.</span><span class="sxs-lookup"><span data-stu-id="a5961-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="a5961-110">Примечание. Для гибридных коллекций требуется синхронизация службы каталогов.</span><span class="sxs-lookup"><span data-stu-id="a5961-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="a5961-111">Проверка соответствия @domain.com</span><span class="sxs-lookup"><span data-stu-id="a5961-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="a5961-112">Перед началом работы убедитесь, что hello имени участника-пользователя для вашей локальной совпадений леса hello суффикс домена Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5961-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="a5961-113">После настройки hello суффикс домена UPN в Azure AD, все пользователи, входящие в Azure RemoteApp будет войдите в систему как «пользователь @<hello suffix you set up>.»</span><span class="sxs-lookup"><span data-stu-id="a5961-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="a5961-114">Убедитесь, что пользователи могут также войти hello же user@suffix в локальном домене hello.</span><span class="sxs-lookup"><span data-stu-id="a5961-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="a5961-115">В некоторых случаях можно задать одно доменное имя в Azure AD с указанием разных доменный суффикс для hello пользователя в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="a5961-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="a5961-116">В этом случае пользователи не будет возможности tooconnect tooany к домену компьютеры или ресурсы с помощью Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a5961-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="a5961-117">Например, если настройка вашей суффикс домена UPN в Azure Active Directory как contoso.com, но некоторым пользователям на локальном или AD не настроенный toolog с @contoso.uk, то эти пользователи не смогут использовать toocorrectly может войти в коллекцию ARA hello.</span><span class="sxs-lookup"><span data-stu-id="a5961-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="a5961-118">Пользователям должно быть имя участника-пользователя в AAD и AD hello одинаково для возможных toobe входа hello»</span><span class="sxs-lookup"><span data-stu-id="a5961-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="a5961-119">Создайте объекты для Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a5961-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="a5961-120">Необходимо также toocreate hello следующие объекты в локальной среде Active Directory:</span><span class="sxs-lookup"><span data-stu-id="a5961-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="a5961-121">Учетная запись tooprovide доступа toodomain ресурсов службы для программ удаленных приложений RemoteApp, соединяя RDSH конечных точек toohello локальному домену.</span><span class="sxs-lookup"><span data-stu-id="a5961-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="a5961-122">Организационное подразделение (OU) toocontain RemoteApp объектов компьютера.</span><span class="sxs-lookup"><span data-stu-id="a5961-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="a5961-123">Hello Подразделения используются учетные записи hello tooisolate рекомендуется (но не обязательно) и политик, которые будут использоваться с RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a5961-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="a5961-124">Нужны оба этих объектов при создании коллекции RemoteApp, поэтому возвратят toodo убедиться, что следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a5961-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>

