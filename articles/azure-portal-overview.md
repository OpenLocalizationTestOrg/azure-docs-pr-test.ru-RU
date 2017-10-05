---
title: "Обзор портала Azure | Документация Майкрософт"
description: "Узнайте, как пользоваться порталом Microsoft Azure."
services: 
documentationcenter: 
author: davidwrede
manager: erikre
editor: jimbe
ms.assetid: 53cb9df1-c96a-4f4e-b022-18336cd3d697
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/16/2015
ms.author: dwrede
ms.openlocfilehash: 71820306716c6297085a29f3ceab89b55396bfe6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-azure-portal-overview"></a><span data-ttu-id="0719c-103">Обзор портала Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0719c-103">Microsoft Azure portal overview</span></span>
<span data-ttu-id="0719c-104">Портал Microsoft Azure — это централизованное место, где можно подготавливать ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="0719c-104">The Microsoft Azure portal is a central place where you can provision and manage your Azure resources.</span></span>  <span data-ttu-id="0719c-105">Это руководство поможет вам ознакомиться с порталом и узнать, как использовать некоторые его ключевые возможности.</span><span class="sxs-lookup"><span data-stu-id="0719c-105">This tutorial will familiarize you with the portal and show you how to use some of these key capabilities:</span></span>

* <span data-ttu-id="0719c-106">В **универсальном магазине Marketplace** представлены тысячи продуктов от корпорации Майкрософт и других поставщиков, и каждый из этих продуктов можно приобрести и подготовить.</span><span class="sxs-lookup"><span data-stu-id="0719c-106">A **comprehensive marketplace** that lets you browse through thousands of items from Microsoft and other vendors that can be purchased and/or provisioned.</span></span>
* <span data-ttu-id="0719c-107">**Единая масштабируемая система** позволяет легко находить нужные ресурсы и выполнять различные операции по управлению.</span><span class="sxs-lookup"><span data-stu-id="0719c-107">A **unified and scalable browse experience** that makes it easy to find the resources you care about and perform various management operations.</span></span>
* <span data-ttu-id="0719c-108">**Согласованные страницы управления** (так называемые колонки) дают возможность управлять самыми разнообразными службами Azure, используя унифицированную систему отображения параметров, действий, данных для выставления счетов, сведений о работоспособности и использовании и т. д.</span><span class="sxs-lookup"><span data-stu-id="0719c-108">**Consistent management pages** (or blades) that let you manage Azure’s wide variety of services through a consistent way of exposing settings, actions, billing information, health monitoring and usage data, and much more.</span></span>
* <span data-ttu-id="0719c-109">**Возможности персонализации** позволяют создать собственный начальный экран, на котором после входа в систему будет отображаться информация, которая нужна именно вам.</span><span class="sxs-lookup"><span data-stu-id="0719c-109">A **personal experience** that lets you create a customized start screen that shows the information that you want to see whenever you log in.</span></span>  <span data-ttu-id="0719c-110">Кроме того, вы можете настроить под себя любую колонку управления с плитками.</span><span class="sxs-lookup"><span data-stu-id="0719c-110">You can also customize any of the management blades that contain tiles.</span></span>
  
  ![Знакомство с пользовательским интерфейсом портала Azure][UIOrientation]

## <a name="before-you-get-started"></a><span data-ttu-id="0719c-112">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="0719c-112">Before you get started</span></span>
<span data-ttu-id="0719c-113">Для прохождения этого учебника вам потребуется действительная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="0719c-113">You will need a valid Azure subscription to go through this tutorial.</span></span>  <span data-ttu-id="0719c-114">Если у вас ее нет, [зарегистрируйтесь в бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/) прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="0719c-114">If you don’t have one, then [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/) today.</span></span>  <span data-ttu-id="0719c-115">Оформив подписку, войдите на портал по адресу <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="0719c-115">Once you have a subscription, you can access the portal at <https://portal.azure.com>.</span></span>

## <a name="how-to-create-a-resource"></a><span data-ttu-id="0719c-116">Как создавать ресурсы</span><span class="sxs-lookup"><span data-stu-id="0719c-116">How to create a resource</span></span>
<span data-ttu-id="0719c-117">Azure Marketplace — это магазин, в котором на выбор предложены тысячи элементов, которые можно создавать, не выходя из него.</span><span class="sxs-lookup"><span data-stu-id="0719c-117">Azure has a marketplace with thousands of items that you can create from one place.</span></span>  <span data-ttu-id="0719c-118">Предположим, вам нужно создать виртуальную машину Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="0719c-118">Let’s say you want to create a new Windows Server 2012 VM.</span></span>  <span data-ttu-id="0719c-119">Нажав кнопку «+СОЗДАТЬ», вы откроете набор рекомендованных категорий магазина.</span><span class="sxs-lookup"><span data-stu-id="0719c-119">The +NEW hub is your entry point into a curated set of featured categories from the marketplace.</span></span>  <span data-ttu-id="0719c-120">В каждой категории есть некоторое количество готовых элементов и ссылка на полный каталог, в котором представлены все категории и окно поиска.</span><span class="sxs-lookup"><span data-stu-id="0719c-120">Each category has a small set of featured items along with a link to the full marketplace that shows all categories and search.</span></span> <span data-ttu-id="0719c-121">Чтобы создать виртуальную машину Windows Server 2012, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0719c-121">To create that new Windows Server 2012 VM, perform the following actions:</span></span>  

1. <span data-ttu-id="0719c-122">Windows Server 2012 — рекомендуемый элемент, поэтому просто выберите его в категории «Среда выполнения приложений».</span><span class="sxs-lookup"><span data-stu-id="0719c-122">Windows Server 2012 is featured, so you can select it from the Compute category.</span></span>  
2. <span data-ttu-id="0719c-123">Укажите в форме некоторые основные данные.</span><span class="sxs-lookup"><span data-stu-id="0719c-123">Fill out some basic inputs on a form.</span></span>
3. <span data-ttu-id="0719c-124">Нажмите кнопку «Создать», после чего сразу же начнется подготовка виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0719c-124">Click ‘Create’ and your VM will begin to provision immediately.</span></span>

<span data-ttu-id="0719c-125">Когда ресурс будет создан, в концентраторе уведомлений появится соответствующее сообщение и откроется колонка управления. (Ресурсы можно просмотреть в любой момент.)</span><span class="sxs-lookup"><span data-stu-id="0719c-125">The notifications hub will alert you when your resource has been created and a management blade will open (you can always browse to resources later).</span></span>

![Категории портала][PortalCategories]

## <a name="how-to-find-your-resources"></a><span data-ttu-id="0719c-127">Как найти свои ресурсы</span><span class="sxs-lookup"><span data-stu-id="0719c-127">How to find your resources</span></span>
<span data-ttu-id="0719c-128">Часто используемые ресурсы можно закрепить на начальной панели, но иногда возникает необходимость найти то, чем вы пользуетесь редко.</span><span class="sxs-lookup"><span data-stu-id="0719c-128">You can always pin frequently accessed resources to your startboard, but you might need to browse to something that you don’t frequently access.</span></span>  <span data-ttu-id="0719c-129">Показанная на рисунке ниже страница обзора позволяет просматривать все ваши ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0719c-129">The browse hub shown below is your way to get to all of your resources.</span></span>  <span data-ttu-id="0719c-130">Вы можете отфильтровать их по подписке, выбрать столбцы и изменить их размер, а также перейти в колонку управления, щелкнув отдельные элементы.</span><span class="sxs-lookup"><span data-stu-id="0719c-130">You can filter by subscription, choose/resize columns, and navigate to the management blades by clicking on individual items.</span></span>

![Обзор концентратора][BrowseHub]

## <a name="how-to-manage-and-delegate-access-to-a-resource"></a><span data-ttu-id="0719c-132">Как управлять ресурсами и предоставлять права доступа к ним</span><span class="sxs-lookup"><span data-stu-id="0719c-132">How to manage and delegate access to a resource</span></span>
<span data-ttu-id="0719c-133">В этой колонке вы можете подключаться к виртуальной машине с помощью удаленного рабочего стола, отслеживать ключевые метрики производительности, управлять доступом к виртуальной машине, используя роли пользователей, изменять настройки виртуальной машины и выполнять другие важный задачи управления.</span><span class="sxs-lookup"><span data-stu-id="0719c-133">From this blade you can connect to the virtual machine using remote desktop, monitor key performance metrics, control access to this VM using role based access (RBAC), configure the VM, and perform other important management tasks.</span></span>  <span data-ttu-id="0719c-134">Предоставление доступа на основе роли — очень важный инструмент управления в средах с большим количеством пользователей.</span><span class="sxs-lookup"><span data-stu-id="0719c-134">Delegating access based on role is critical to managing at scale.</span></span>  <span data-ttu-id="0719c-135">Дополнительные сведения см. [здесь](active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0719c-135">Click [here](active-directory/role-based-access-control-configure.md) to learn more about it.</span></span> <span data-ttu-id="0719c-136">Чтобы предоставить пользователю доступ к ресурсу, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0719c-136">To delegate access to a resource, perform the following actions:</span></span>

1. <span data-ttu-id="0719c-137">Перейдите к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="0719c-137">Browse to your resource.</span></span>
2. <span data-ttu-id="0719c-138">В разделе «Основные сведения» нажмите кнопку «Все параметры».</span><span class="sxs-lookup"><span data-stu-id="0719c-138">Click ‘All settings’ in the Essentials section.</span></span>
3. <span data-ttu-id="0719c-139">В списке параметров щелкните «Пользователи».</span><span class="sxs-lookup"><span data-stu-id="0719c-139">Click ‘Users’ in the settings list.</span></span>
4. <span data-ttu-id="0719c-140">На панели команд нажмите кнопку «Добавить».</span><span class="sxs-lookup"><span data-stu-id="0719c-140">Click ‘Add’ in the command bar.</span></span>
5. <span data-ttu-id="0719c-141">Выберите пользователя и роль.</span><span class="sxs-lookup"><span data-stu-id="0719c-141">Choose a user and a role.</span></span>

![Управление ресурсом][ManageResource]

## <a name="how-to-get-help"></a><span data-ttu-id="0719c-143">Как получить справку</span><span class="sxs-lookup"><span data-stu-id="0719c-143">How to get help</span></span>
<span data-ttu-id="0719c-144">Если у вас возникнут какие-либо трудности, вы всегда можете обратиться к нам.</span><span class="sxs-lookup"><span data-stu-id="0719c-144">If you ever have a problem, we’re here for you.</span></span>  <span data-ttu-id="0719c-145">На портале есть страница справки и поддержки, которая поможет вам решить возникшую проблему.</span><span class="sxs-lookup"><span data-stu-id="0719c-145">The portal has a help and support page that can point you in the right direction.</span></span>  <span data-ttu-id="0719c-146">Кроме того, прямо на портале можно создавать запросы в службу поддержки (зависит от вашего [плана поддержки](https://azure.microsoft.com/support/plans/)).</span><span class="sxs-lookup"><span data-stu-id="0719c-146">Depending on your [support plan](https://azure.microsoft.com/support/plans/), you can also create support tickets directly in the portal.</span></span>  <span data-ttu-id="0719c-147">После создания запроса вы можете управлять его жизненным циклом, не покидая портал.</span><span class="sxs-lookup"><span data-stu-id="0719c-147">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span> <span data-ttu-id="0719c-148">Чтобы открыть страницу справки и поддержки, последовательно щелкните «Обзор» и «Справка + поддержка».</span><span class="sxs-lookup"><span data-stu-id="0719c-148">You can get to the help and support page by navigating to Browse -> Help + support.</span></span>  

![Справка и поддержка][HelpSupport]

## <a name="summary"></a><span data-ttu-id="0719c-150">Сводка</span><span class="sxs-lookup"><span data-stu-id="0719c-150">Summary</span></span>
<span data-ttu-id="0719c-151">Давайте подытожим, что вы узнали из этого руководства.</span><span class="sxs-lookup"><span data-stu-id="0719c-151">Let’s review what you learned in this tutorial:</span></span>

* <span data-ttu-id="0719c-152">Вы узнали, как зарегистрироваться в системе, оформить подписку и перейти на портал.</span><span class="sxs-lookup"><span data-stu-id="0719c-152">You learned how to sign up, get a subscription, and browse to the portal</span></span>
* <span data-ttu-id="0719c-153">Вы ознакомились с пользовательским интерфейсом портала, а также научились создавать и просматривать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0719c-153">You got oriented with the portal UI and learned how to create and browse resources</span></span>
* <span data-ttu-id="0719c-154">Вы узнали, как создавать и просматривать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0719c-154">You learned how to create a resource and browse resources</span></span>
* <span data-ttu-id="0719c-155">Вы изучили структуру колонок управления и научились согласованно управлять различными типами ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0719c-155">You learned about the structure or management blades and how you can consistently manage different types of resources</span></span>
* <span data-ttu-id="0719c-156">Мы рассказали вам, как настроить портал, чтобы важная для вас информация всегда была на виду.</span><span class="sxs-lookup"><span data-stu-id="0719c-156">You learned how to customize the portal to bring the information you care about to the front and center</span></span>
* <span data-ttu-id="0719c-157">Мы также объяснили вам, как контролировать доступ к ресурсам с помощью управления доступом на основе ролей (RBAC).</span><span class="sxs-lookup"><span data-stu-id="0719c-157">You learned how to control access to resources using role based access (RBAC)</span></span>
* <span data-ttu-id="0719c-158">Вы узнали, как можно получить справку и поддержку.</span><span class="sxs-lookup"><span data-stu-id="0719c-158">You learned how to get help and support</span></span>

<span data-ttu-id="0719c-159">Портал Microsoft Azure кардинально упрощает создание приложений в облаке и управление ими.</span><span class="sxs-lookup"><span data-stu-id="0719c-159">The Microsoft Azure portal radically simplifies building and managing your applications in the cloud.</span></span>  <span data-ttu-id="0719c-160">Чтобы всегда быть в курсе всех изменений и нововведений, подпишитесь на [блог по управлению](https://azure.microsoft.com/blog/topics/management/). Мы постоянно следим за [отзывами пользователей](https://feedback.azure.com/forums/223579-azure-preview-portal/) и реагируем на них.</span><span class="sxs-lookup"><span data-stu-id="0719c-160">Take a look at the [management blog](https://azure.microsoft.com/blog/topics/management/) to keep up to date as we’re constantly [listening to feedback](https://feedback.azure.com/forums/223579-azure-preview-portal/) and making improvements.</span></span>  <span data-ttu-id="0719c-161">Еще одним замечательным ресурсом, предоставляющим новости об Azure, является [блог ScottGu](http://weblogs.asp.net/scottgu).</span><span class="sxs-lookup"><span data-stu-id="0719c-161">[ScottGu’s blog](http://weblogs.asp.net/scottgu) is another great place to look for all Azure updates.</span></span>

[UIOrientation]: ./media/azure-portal-how-to-use/azure_portal_1.png
[PortalCategories]: ./media/azure-portal-how-to-use/azure_portal_2.png
[BrowseHub]: ./media/azure-portal-how-to-use/azure_portal_3.png
[ManageResource]: ./media/azure-portal-how-to-use/azure_portal_4.png
[CustomizeBlades]: ./media/azure-portal-how-to-use/azure_portal_5.png
[HelpSupport]: ./media/azure-portal-how-to-use/azure_portal_6.png
