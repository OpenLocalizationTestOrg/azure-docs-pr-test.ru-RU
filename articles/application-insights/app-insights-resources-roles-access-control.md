---
title: "aaaResources, ролей и управление доступом в Azure Application Insights | Документы Microsoft"
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
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="d1d92-103">Ресурсы, роли и контроль доступа в Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d92-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="d1d92-104">Можно управлять, чтение и обновление данных tooyour доступа в Azure [Application Insights][start], с помощью [управление доступом на основе ролей в Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d1d92-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1d92-105">Назначить доступ toousers в hello **группу ресурсов или подписку** toowhich - не в сам ресурс hello принадлежит ресурс приложения.</span><span class="sxs-lookup"><span data-stu-id="d1d92-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="d1d92-106">Назначить hello **участника компонента Application Insights** роли.</span><span class="sxs-lookup"><span data-stu-id="d1d92-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="d1d92-107">Это обеспечивает универсальный элемент управления доступа tooweb тестов и оповещения вместе с приложением ресурс.</span><span class="sxs-lookup"><span data-stu-id="d1d92-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="d1d92-108">[Подробнее](#access).</span><span class="sxs-lookup"><span data-stu-id="d1d92-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="d1d92-109">Ресурсы, группы и подписки</span><span class="sxs-lookup"><span data-stu-id="d1d92-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="d1d92-110">Сначала рассмотрим некоторые определения:</span><span class="sxs-lookup"><span data-stu-id="d1d92-110">First, some definitions:</span></span>

* <span data-ttu-id="d1d92-111">**Ресурс** — это экземпляр службы Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d1d92-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="d1d92-112">Ресурс Application Insights собирает и анализирует отображает hello данные телеметрии, отправленные из приложения.</span><span class="sxs-lookup"><span data-stu-id="d1d92-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="d1d92-113">Другие типы ресурсов Azure включают в себя веб-приложения, базы данных и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="d1d92-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="d1d92-114">toosee ресурсов, откройте hello [портала Azure][portal], войдите и выберите все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d1d92-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="d1d92-115">toofind ресурса, тип часть его имени в поле фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="d1d92-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Список ресурсов Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="d1d92-117">[**Группа ресурсов** ] [ group] -каждый ресурс принадлежит tooone группы.</span><span class="sxs-lookup"><span data-stu-id="d1d92-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="d1d92-118">Группа не является удобным способом toomanage связанных ресурсов, особенно для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="d1d92-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="d1d92-119">Например в один ресурс группы, можно поместить веб-приложения, приложения hello toomonitor ресурса Application Insights и tookeep ресурсов хранения экспортированных данных.</span><span class="sxs-lookup"><span data-stu-id="d1d92-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![Выберите «Обзор», «Группы ресурсов», а затем выберите группу](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="d1d92-121">[**Подписки** ](https://manage.windowsazure.com) -toouse Application Insights или другим ресурсам Azure, вход tooan подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d1d92-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="d1d92-122">Каждая группа ресурсов принадлежит tooone подписки Azure, где выберите пакет цены, если подписка на организации, выберите hello членов и разрешений доступа.</span><span class="sxs-lookup"><span data-stu-id="d1d92-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="d1d92-123">[**Учетная запись Майкрософт** ] [ account] -hello имени пользователя и пароля, используемых в tooMicrosoft Azure toosign подписок, XBox Live, Outlook.com и другие службы Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d1d92-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="d1d92-124"><a name="access"></a>Управление доступом в группе ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="d1d92-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="d1d92-125">Это важные toounderstand, что в сложения toohello созданный ресурс для приложения, существует также разделения скрытые ресурсы для оповещений и веб-тестов.</span><span class="sxs-lookup"><span data-stu-id="d1d92-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="d1d92-126">Они являются вложенного toohello же [группы ресурсов](#resource-group) с приложением.</span><span class="sxs-lookup"><span data-stu-id="d1d92-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="d1d92-127">В нее также можно поместить другие службы Azure, такие как веб-сайты или службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="d1d92-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Ресурсы в Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="d1d92-129">ресурсы toothese toocontrol доступа, поэтому рекомендуется для:</span><span class="sxs-lookup"><span data-stu-id="d1d92-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="d1d92-130">Управление доступом на hello **группу ресурсов или подписку** уровне.</span><span class="sxs-lookup"><span data-stu-id="d1d92-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="d1d92-131">Назначить hello **участника компонента аналитики приложений** toousers роли.</span><span class="sxs-lookup"><span data-stu-id="d1d92-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="d1d92-132">Это позволяет им tooedit веб-тесты, оповещения и ресурсы Application Insights, без предоставления доступа tooany другие службы в группе hello.</span><span class="sxs-lookup"><span data-stu-id="d1d92-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="d1d92-133">tooprovide доступа tooanother пользователей</span><span class="sxs-lookup"><span data-stu-id="d1d92-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="d1d92-134">Необходимо иметь подписку toohello права владельца или группа ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="d1d92-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="d1d92-135">Hello пользователь должен иметь [учетную запись Майкрософт][account], или доступ к tootheir [учетная запись организации Microsoft](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="d1d92-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="d1d92-136">Чтобы обеспечить доступ tooindividuals и toouser группы, определенные в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1d92-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="d1d92-137">Перейдите в группу ресурсов toohello</span><span class="sxs-lookup"><span data-stu-id="d1d92-137">Navigate toohello resource group</span></span>
<span data-ttu-id="d1d92-138">Добавьте hello пользователя существует.</span><span class="sxs-lookup"><span data-stu-id="d1d92-138">Add hello user there.</span></span>

![В колонке ресурсов приложения откройте Essentials, откройте группу ресурсов hello и существует выберите параметры и пользователей.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="d1d92-141">Или можно перейти вверх другого уровня и добавить пользователя hello toohello подписки.</span><span class="sxs-lookup"><span data-stu-id="d1d92-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="d1d92-142">Выбор роли</span><span class="sxs-lookup"><span data-stu-id="d1d92-142">Select a role</span></span>
![Выберите роль для нового пользователя hello](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="d1d92-144">Роль</span><span class="sxs-lookup"><span data-stu-id="d1d92-144">Role</span></span> | <span data-ttu-id="d1d92-145">В группе ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="d1d92-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="d1d92-146">Владелец</span><span class="sxs-lookup"><span data-stu-id="d1d92-146">Owner</span></span> |<span data-ttu-id="d1d92-147">Можно менять любые параметры, в том числе права доступа пользователей</span><span class="sxs-lookup"><span data-stu-id="d1d92-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="d1d92-148">Участник</span><span class="sxs-lookup"><span data-stu-id="d1d92-148">Contributor</span></span> |<span data-ttu-id="d1d92-149">Можно изменять любое содержимое, в том числе любые ресурсы</span><span class="sxs-lookup"><span data-stu-id="d1d92-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="d1d92-150">участника компонента Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d92-150">Application Insights Component contributor</span></span> |<span data-ttu-id="d1d92-151">Можно изменять ресурсы, веб-тесты и оповещения Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d92-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="d1d92-152">Читатель</span><span class="sxs-lookup"><span data-stu-id="d1d92-152">Reader</span></span> |<span data-ttu-id="d1d92-153">Можно просматривать содержимое, но нельзя ничего изменять</span><span class="sxs-lookup"><span data-stu-id="d1d92-153">Can view but not change anything</span></span> |

<span data-ttu-id="d1d92-154">«Изменение» включает в себя создание, удаление и обновление:</span><span class="sxs-lookup"><span data-stu-id="d1d92-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="d1d92-155">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="d1d92-155">Resources</span></span>
* <span data-ttu-id="d1d92-156">Веб-тесты</span><span class="sxs-lookup"><span data-stu-id="d1d92-156">Web tests</span></span>
* <span data-ttu-id="d1d92-157">Оповещения</span><span class="sxs-lookup"><span data-stu-id="d1d92-157">Alerts</span></span>
* <span data-ttu-id="d1d92-158">непрерывный экспорт.</span><span class="sxs-lookup"><span data-stu-id="d1d92-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="d1d92-159">Выберите пользователя hello</span><span class="sxs-lookup"><span data-stu-id="d1d92-159">Select hello user</span></span>

<span data-ttu-id="d1d92-160">Если hello пользователя отсутствует в каталоге hello, вы можете пригласить любой пользователь с учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d1d92-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="d1d92-161">(если он использует такие службы, как Outlook.com, OneDrive, Windows Phone или XBox Live, значит, у него есть учетная запись Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="d1d92-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="d1d92-162">Связанная информация</span><span class="sxs-lookup"><span data-stu-id="d1d92-162">Related content</span></span>

* [<span data-ttu-id="d1d92-163">Управление доступом на основе ролей в Azure</span><span class="sxs-lookup"><span data-stu-id="d1d92-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
