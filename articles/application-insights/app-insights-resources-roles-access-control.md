---
title: "Ресурсы, роли и контроль доступа в Azure Application Insights | Документация Майкрософт"
description: "Владельцы, участники и читатели Insights вашей организации."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: c979a8bfbeecacc7c0bbc112e02a4b68e874c219
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="43d85-103">Ресурсы, роли и контроль доступа в Application Insights</span><span class="sxs-lookup"><span data-stu-id="43d85-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="43d85-104">Вы можете управлять доступом на чтение и обновлять права доступа к данным в Azure [Application Insights][start], используя [Управление доступом на основе ролей в Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="43d85-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43d85-105">Вы также можете предоставлять доступ пользователям в **группе ресурсов или подписке** , к которым относится ресурс приложения, а не в самом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="43d85-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span></span> <span data-ttu-id="43d85-106">Назначьте им роль **участника компонента Application Insights** .</span><span class="sxs-lookup"><span data-stu-id="43d85-106">Assign the **Application Insights component contributor** role.</span></span> <span data-ttu-id="43d85-107">Это обеспечит универсальный контроль доступа к веб-тестам и оповещениям с помощью ресурса приложения.</span><span class="sxs-lookup"><span data-stu-id="43d85-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span></span> <span data-ttu-id="43d85-108">[Подробнее](#access).</span><span class="sxs-lookup"><span data-stu-id="43d85-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="43d85-109">Ресурсы, группы и подписки</span><span class="sxs-lookup"><span data-stu-id="43d85-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="43d85-110">Сначала рассмотрим некоторые определения:</span><span class="sxs-lookup"><span data-stu-id="43d85-110">First, some definitions:</span></span>

* <span data-ttu-id="43d85-111">**Ресурс** — это экземпляр службы Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="43d85-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="43d85-112">Ресурс Application Insights собирает, анализирует и отображает данные телеметрии, отправленные приложением.</span><span class="sxs-lookup"><span data-stu-id="43d85-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span></span>  <span data-ttu-id="43d85-113">Другие типы ресурсов Azure включают в себя веб-приложения, базы данных и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="43d85-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="43d85-114">Чтобы просмотреть свои ресурсы, откройте [портал Azure][portal], выполните вход и щелкните "Все ресурсы".</span><span class="sxs-lookup"><span data-stu-id="43d85-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="43d85-115">Чтобы найти ресурс, введите часть его имени в поле фильтра.</span><span class="sxs-lookup"><span data-stu-id="43d85-115">To find a resource, type part of its name in the filter field.</span></span>
  
    ![Список ресурсов Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="43d85-117">[**Группа ресурсов**][group] — каждый ресурс принадлежит одной группе.</span><span class="sxs-lookup"><span data-stu-id="43d85-117">[**Resource group**][group] - Every resource belongs to one group.</span></span> <span data-ttu-id="43d85-118">Создание группы — это удобный способ управления связанными ресурсами, особенно для контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="43d85-118">A group is a convenient way to manage related resources, particularly for access control.</span></span> <span data-ttu-id="43d85-119">Например, в одну группу ресурсов можно поместить веб-приложение и ресурс Application Insights для мониторинга приложения, а также ресурс хранилища для хранения экспортированных данных.</span><span class="sxs-lookup"><span data-stu-id="43d85-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span></span>

    ![Выберите «Обзор», «Группы ресурсов», а затем выберите группу](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="43d85-121">[**Подписка**](https://manage.windowsazure.com). Чтобы использовать Application Insights или другие ресурсы Azure, войдите в подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="43d85-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span></span> <span data-ttu-id="43d85-122">Каждая группа ресурсов относится к одной подписке Azure, где вы выбираете пакет по цене и, при использовании подписки для организации, выбираете участников и права доступа для них.</span><span class="sxs-lookup"><span data-stu-id="43d85-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span></span>
* <span data-ttu-id="43d85-123">[**Учетная запись Майкрософт**][account] — имя пользователя и пароль, используемые для входа в подписки Microsoft Azure, Xbox Live, Outlook.com и другие службы Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="43d85-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="43d85-124"><a name="access"></a> Контроль доступа в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="43d85-124"><a name="access"></a> Control access in the resource group</span></span>
<span data-ttu-id="43d85-125">Важно понимать, что кроме ресурса, созданного для приложения, существуют также отдельные скрытые ресурсы для оповещений и веб-тестов.</span><span class="sxs-lookup"><span data-stu-id="43d85-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="43d85-126">Они вложены в ту же [группу ресурсов](#resource-group) , что и ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="43d85-126">They are attached to the same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="43d85-127">В нее также можно поместить другие службы Azure, такие как веб-сайты или службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="43d85-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Ресурсы в Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="43d85-129">Поэтому для контроля доступа к этим ресурсам рекомендуем:</span><span class="sxs-lookup"><span data-stu-id="43d85-129">To control access to these resources it's therefore recommended to:</span></span>

* <span data-ttu-id="43d85-130">осуществлять контроль доступа на уровне **группы ресурсов или подписки** ;</span><span class="sxs-lookup"><span data-stu-id="43d85-130">Control access at the **resource group or subscription** level.</span></span>
* <span data-ttu-id="43d85-131">назначать пользователям роль **участника компонента Application Insights** .</span><span class="sxs-lookup"><span data-stu-id="43d85-131">Assign the **Application Insights Component contributor** role to users.</span></span> <span data-ttu-id="43d85-132">Это позволяет изменять веб-тесты, оповещения и ресурсы Application Insights, не предоставляя доступ к другим службам в группе.</span><span class="sxs-lookup"><span data-stu-id="43d85-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span></span>

## <a name="to-provide-access-to-another-user"></a><span data-ttu-id="43d85-133">Предоставление доступа другому пользователю</span><span class="sxs-lookup"><span data-stu-id="43d85-133">To provide access to another user</span></span>
<span data-ttu-id="43d85-134">Для этого у вас должны быть права владельца подписки или группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="43d85-134">You must have Owner rights to the subscription or the resource group.</span></span>

<span data-ttu-id="43d85-135">У пользователя должна быть [учетная запись Майкрософт][account] или доступ к [корпоративной учетной записи Майкрософт](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="43d85-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="43d85-136">Вы можете предоставлять доступ отдельным пользователям и группам пользователей, определенным в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="43d85-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-to-the-resource-group"></a><span data-ttu-id="43d85-137">Переход к группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="43d85-137">Navigate to the resource group</span></span>
<span data-ttu-id="43d85-138">Добавьте в нее пользователя.</span><span class="sxs-lookup"><span data-stu-id="43d85-138">Add the user there.</span></span>

![В колонке ресурсов приложения откройте «Основные компоненты», откройте группу ресурсов и выберите параметры или пользователей.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="43d85-141">Вы также можете перейти на уровень выше и добавить пользователя в подписку.</span><span class="sxs-lookup"><span data-stu-id="43d85-141">Or you could go up another level and add the user to the Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="43d85-142">Выбор роли</span><span class="sxs-lookup"><span data-stu-id="43d85-142">Select a role</span></span>
![Выберите роль для нового пользователя](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="43d85-144">Роль</span><span class="sxs-lookup"><span data-stu-id="43d85-144">Role</span></span> | <span data-ttu-id="43d85-145">В группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="43d85-145">In the resource group</span></span> |
| --- | --- |
| <span data-ttu-id="43d85-146">Владелец</span><span class="sxs-lookup"><span data-stu-id="43d85-146">Owner</span></span> |<span data-ttu-id="43d85-147">Можно менять любые параметры, в том числе права доступа пользователей</span><span class="sxs-lookup"><span data-stu-id="43d85-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="43d85-148">Участник</span><span class="sxs-lookup"><span data-stu-id="43d85-148">Contributor</span></span> |<span data-ttu-id="43d85-149">Можно изменять любое содержимое, в том числе любые ресурсы</span><span class="sxs-lookup"><span data-stu-id="43d85-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="43d85-150">участника компонента Application Insights</span><span class="sxs-lookup"><span data-stu-id="43d85-150">Application Insights Component contributor</span></span> |<span data-ttu-id="43d85-151">Можно изменять ресурсы, веб-тесты и оповещения Application Insights</span><span class="sxs-lookup"><span data-stu-id="43d85-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="43d85-152">Читатель</span><span class="sxs-lookup"><span data-stu-id="43d85-152">Reader</span></span> |<span data-ttu-id="43d85-153">Можно просматривать содержимое, но нельзя ничего изменять</span><span class="sxs-lookup"><span data-stu-id="43d85-153">Can view but not change anything</span></span> |

<span data-ttu-id="43d85-154">«Изменение» включает в себя создание, удаление и обновление:</span><span class="sxs-lookup"><span data-stu-id="43d85-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="43d85-155">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="43d85-155">Resources</span></span>
* <span data-ttu-id="43d85-156">Веб-тесты</span><span class="sxs-lookup"><span data-stu-id="43d85-156">Web tests</span></span>
* <span data-ttu-id="43d85-157">Оповещения</span><span class="sxs-lookup"><span data-stu-id="43d85-157">Alerts</span></span>
* <span data-ttu-id="43d85-158">непрерывный экспорт.</span><span class="sxs-lookup"><span data-stu-id="43d85-158">Continuous export</span></span>

#### <a name="select-the-user"></a><span data-ttu-id="43d85-159">Выбор пользователя</span><span class="sxs-lookup"><span data-stu-id="43d85-159">Select the user</span></span>

<span data-ttu-id="43d85-160">Если в каталоге нет необходимого пользователя, вы можете пригласить любого пользователя с учетной записью Майкрософт</span><span class="sxs-lookup"><span data-stu-id="43d85-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="43d85-161">(если он использует такие службы, как Outlook.com, OneDrive, Windows Phone или XBox Live, значит, у него есть учетная запись Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="43d85-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="43d85-162">Связанная информация</span><span class="sxs-lookup"><span data-stu-id="43d85-162">Related content</span></span>

* [<span data-ttu-id="43d85-163">Управление доступом на основе ролей в Azure</span><span class="sxs-lookup"><span data-stu-id="43d85-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
