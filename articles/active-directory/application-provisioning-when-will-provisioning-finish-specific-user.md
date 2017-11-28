---
title: "Как определить, когда конкретный пользователь получит доступ к приложению | Документы Майкрософт"
description: "В этой статье описано, как определить, когда критически важный пользователь получит доступ к приложению, которое было настроено для подготовки пользователя в Azure AD."
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
ms.openlocfilehash: fcefb31904cfb77022db0358e9feee6a0479db81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a><span data-ttu-id="0fe10-103">Как определить, когда конкретный пользователь получит доступ к приложению</span><span class="sxs-lookup"><span data-stu-id="0fe10-103">Find out when a specific user will be able to access an application</span></span>
<span data-ttu-id="0fe10-104">При использовании автоматической подготовки пользователей Azure AD будет автоматически подготавливать и обновлять учетные записи пользователей в приложении на основе [назначений пользователей и групп](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) с установленным интервалом времени, обычно каждые 10 минут.</span><span class="sxs-lookup"><span data-stu-id="0fe10-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="0fe10-105">Сколько времени это занимает?</span><span class="sxs-lookup"><span data-stu-id="0fe10-105">How long does it take?</span></span>

<span data-ttu-id="0fe10-106">Время, необходимое для подготовки пользователя, главным образом зависит от того, была ли выполнена начальная "полная" синхронизация.</span><span class="sxs-lookup"><span data-stu-id="0fe10-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="0fe10-107">Первая синхронизация приложения с Azure AD может занять от 20 минут до нескольких часов, в зависимости от размера каталога Azure AD и количества пользователей в области подготовки.</span><span class="sxs-lookup"><span data-stu-id="0fe10-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="0fe10-108">Последующие операции синхронизации занимают меньше времени (например, 10 минут), так как служба подготовки сохраняет "водяные знаки", которые представляют состояние обеих систем после начальной синхронизации. Это позволяет повысить скорость последующих операций синхронизации.</span><span class="sxs-lookup"><span data-stu-id="0fe10-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-check-the-status-of-a-user"></a><span data-ttu-id="0fe10-109">Как проверить состояние пользователя</span><span class="sxs-lookup"><span data-stu-id="0fe10-109">How to check the status of a user</span></span>

<span data-ttu-id="0fe10-110">Чтобы просмотреть состояние подготовки для выбранного пользователя, обратитесь к журналам аудита в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe10-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span></span>

<span data-ttu-id="0fe10-111">Журналы аудита для подготовки можно открыть на портале Azure на вкладке **Azure Active Directory &gt; Корпоративные приложения &gt; \[имя приложения\] &gt; Журналы аудита**.</span><span class="sxs-lookup"><span data-stu-id="0fe10-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab.</span></span> <span data-ttu-id="0fe10-112">Чтобы просмотреть события подготовки только для этого приложения, отфильтруйте журналы по категории **Учетная запись подготовки**.</span><span class="sxs-lookup"><span data-stu-id="0fe10-112">Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span></span> <span data-ttu-id="0fe10-113">Найти пользователей можно по "идентификатору сопоставления", который был назначен для этих пользователей в сопоставлениях атрибутов.</span><span class="sxs-lookup"><span data-stu-id="0fe10-113">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span></span> 

<span data-ttu-id="0fe10-114">Например, если в качестве атрибута сопоставления в Azure AD выбраны "имя участника-пользователя" или "адрес электронной почты", и для пользователя, который не подготавливается, этот атрибут имеет значение "audrey@contoso.com", найдите "audrey@contoso.com" в журналах аудита и просмотрите результаты поиска.</span><span class="sxs-lookup"><span data-stu-id="0fe10-114">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="0fe10-115">В журналах аудита записываются все операции, которые выполняются службой подготовки, в том числе:</span><span class="sxs-lookup"><span data-stu-id="0fe10-115">The provisioning audit logs record all the operations performed by the provisioning service, including:</span></span>

* <span data-ttu-id="0fe10-116">Получение сведений о назначенных пользователях, которые находятся в области для подготовки, в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe10-116">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="0fe10-117">Получение сведений о наличии этих пользователей от целевого приложения</span><span class="sxs-lookup"><span data-stu-id="0fe10-117">Querying the target app for the existence of those users</span></span>
* <span data-ttu-id="0fe10-118">Сравнение объектов пользователя в разных системах</span><span class="sxs-lookup"><span data-stu-id="0fe10-118">Comparing the user objects between the system</span></span>
* <span data-ttu-id="0fe10-119">Добавление, обновление или отключение учетной записи пользователя в целевой системе на основе сравнения</span><span class="sxs-lookup"><span data-stu-id="0fe10-119">Adding, updating, or disabling the user account in the target system based on the comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fe10-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0fe10-120">Next steps</span></span>
<span data-ttu-id="0fe10-121">[Автоматическая подготовка пользователей и отмена подготовки для приложений SaaS в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)</span><span class="sxs-lookup"><span data-stu-id="0fe10-121">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
