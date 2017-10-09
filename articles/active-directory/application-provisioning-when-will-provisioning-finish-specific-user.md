---
title: "aaaFind out когда конкретного пользователя будет доступ tooaccess приложения | Документы Microsoft"
description: "Как toofind out ли критически важными пользователь быть может tooaccess приложения вы настроили для подготовки пользователей в Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a><span data-ttu-id="aaef2-103">Узнать, когда конкретного пользователя будет доступ tooaccess приложения</span><span class="sxs-lookup"><span data-stu-id="aaef2-103">Find out when a specific user will be able tooaccess an application</span></span>
<span data-ttu-id="aaef2-104">При использовании автоматической подготовки пользователей Azure AD будет автоматически подготавливать и обновлять учетные записи пользователей в приложении на основе [назначений пользователей и групп](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) с установленным интервалом времени, обычно каждые 10 минут.</span><span class="sxs-lookup"><span data-stu-id="aaef2-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="aaef2-105">Сколько времени это занимает?</span><span class="sxs-lookup"><span data-stu-id="aaef2-105">How long does it take?</span></span>

<span data-ttu-id="aaef2-106">Hello время, необходимое для данного пользователя toobe подготовить главным образом зависит ли первоначальную синхронизацию «full» уже существует.</span><span class="sxs-lookup"><span data-stu-id="aaef2-106">hello time it takes for a given user toobe provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="aaef2-107">Здравствуйте, первой синхронизации между Azure AD и приложения может занять от tooseveral часов 20 минут, в зависимости от размера каталога hello Azure AD и hello количество пользователей в области для подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="aaef2-107">hello first sync between Azure AD and an app can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="aaef2-108">Последующие синхронизации после начальной синхронизации hello выполняться быстрее (например, в течение 10 минут), как подготовка службы hello хранит водяных знаков, которые представляют Привет состояние обеих систем после начальной синхронизации hello, повышая производительность последующих синхронизаций.</span><span class="sxs-lookup"><span data-stu-id="aaef2-108">Subsequent syncs after hello initial sync be faster (e.g. within 10 minutes), as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-toocheck-hello-status-of-a-user"></a><span data-ttu-id="aaef2-109">Как toocheck hello состояния пользователя</span><span class="sxs-lookup"><span data-stu-id="aaef2-109">How toocheck hello status of a user</span></span>

<span data-ttu-id="aaef2-110">состояние подготовки hello toosee для выбранного пользователя, обратитесь к hello журналы аудита в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aaef2-110">toosee hello provisioning status for a selected user, consult hello Audit logs in Azure AD.</span></span>

<span data-ttu-id="aaef2-111">Hello подготовки журналы аудита можно получить в hello в hello портале Azure **Azure Active Directory &gt; корпоративных приложений &gt; \[имя_приложения\] &gt; журналы аудита**вкладки. Фильтр hello входе hello **подготовку учетных записей** tooonly категории разделе hello подготовки события для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="aaef2-111">hello provisioning audit logs can be accessed in hello Azure portal, in hello **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter hello logs on hello **Account Provisioning** category tooonly see hello provisioning events for that app.</span></span> <span data-ttu-id="aaef2-112">Можно выполнить поиск пользователя на основании hello «сопоставления ID», настроенную для их в сопоставления атрибутов hello.</span><span class="sxs-lookup"><span data-stu-id="aaef2-112">You can search for users based on hello “matching ID” that was configured for them in hello attribute mappings.</span></span> 

<span data-ttu-id="aaef2-113">Например, если пользователь настроил hello «имя участника-пользователя» или «адрес электронной почты» как hello сопоставления атрибута на стороне hello Azure AD и пользователя hello подготовки не имеет значение «audrey@contoso.com«, затем аудита hello поиска в журналах»audrey@contoso.com"и затем просмотрите возвращены записи.</span><span class="sxs-lookup"><span data-stu-id="aaef2-113">For example, if you configured hello “user principal name” or “email address” as hello matching attribute on hello Azure AD side, and hello user not being provisioning has a value of “audrey@contoso.com”, then search hello audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="aaef2-114">Подготовка аудита Hello регистрирует записи Здравствуйте, все операции, выполняемые hello подготовки службы, включая:</span><span class="sxs-lookup"><span data-stu-id="aaef2-114">hello provisioning audit logs record all hello operations performed by hello provisioning service, including:</span></span>

* <span data-ttu-id="aaef2-115">Получение сведений о назначенных пользователях, которые находятся в области для подготовки, в Azure AD</span><span class="sxs-lookup"><span data-stu-id="aaef2-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="aaef2-116">Запрос hello целевое приложение hello наличие этих пользователей</span><span class="sxs-lookup"><span data-stu-id="aaef2-116">Querying hello target app for hello existence of those users</span></span>
* <span data-ttu-id="aaef2-117">Сравнение объектов пользователя hello между системой hello</span><span class="sxs-lookup"><span data-stu-id="aaef2-117">Comparing hello user objects between hello system</span></span>
* <span data-ttu-id="aaef2-118">Добавление, обновление или отключение учетной записи пользователя hello в целевой системе hello, на основе сравнения hello</span><span class="sxs-lookup"><span data-stu-id="aaef2-118">Adding, updating, or disabling hello user account in hello target system based on hello comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaef2-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aaef2-119">Next steps</span></span>
<span data-ttu-id="aaef2-120">[Автоматизировать подготовку пользователей и их отзыва tooSaaS приложений с Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span><span class="sxs-lookup"><span data-stu-id="aaef2-120">[Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
