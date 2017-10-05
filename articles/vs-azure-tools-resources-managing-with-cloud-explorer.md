---
title: "Управление ресурсами Azure с помощью Cloud Explorer | Документация Майкрософт"
description: "Узнайте, как использовать Cloud Explorer для просмотра ресурсов Azure и управления ими в Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 6e6d8d559f0251b71bfa6d529ead82a246cb3235
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="0e392-103">Управление ресурсами, связанными с учетными записями Azure, с помощью Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0e392-103">Manage the resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="0e392-104">Cloud Explorer позволяет просматривать ресурсы и группы ресурсов Azure, проверять их свойства и выполнять основные диагностические действия разработчика в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e392-104">Cloud Explorer enables you to view your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="0e392-105">Приложение Cloud Explorer, как и [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), основано на стеке Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0e392-105">Like the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on the Azure Resource Manager stack.</span></span> <span data-ttu-id="0e392-106">Благодаря этому Cloud Explorer распознает ресурсы (например, группы ресурсов Azure) и службы Azure (например, Logic Apps и API-приложения), а также поддерживает [управление доступом на основе ролей](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="0e392-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0e392-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0e392-107">Prerequisites</span></span>
- <span data-ttu-id="0e392-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) с выбранной **рабочей нагрузкой Azure** или более ранняя версия Visual Studio с пакетом [Microsoft Azure SDK для .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="0e392-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **Azure workload** selected, or an earlier version of Visual Studio with the [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="0e392-109">Учетная запись Azure. Если у вас ее нет, [зарегистрируйтесь для работы с бесплатной пробной версией](http://go.microsoft.com/fwlink/?LinkId=623901) или [активируйте преимущества для подписчиков Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="0e392-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="0e392-110">Чтобы открыть Cloud Explorer, выберите в меню **Представление** > **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0e392-110">To view Cloud Explorer, select **View** > **Cloud Explorer** on the menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-to-cloud-explorer"></a><span data-ttu-id="0e392-111">Добавление учетной записи Azure в Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0e392-111">Add an Azure account to Cloud Explorer</span></span>
<span data-ttu-id="0e392-112">Чтобы просмотреть ресурсы, связанные с учетной записью Azure, сначала необходимо добавить учетную запись в Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="0e392-112">To view the resources associated with an Azure account, you must first add the account to Cloud Explorer.</span></span> 

1. <span data-ttu-id="0e392-113">В **Cloud Explorer** выберите раздел **Параметры учетной записи Azure**.</span><span class="sxs-lookup"><span data-stu-id="0e392-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Значок параметров учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="0e392-115">Выберите **Добавить новую учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="0e392-115">Select **Add new account**.</span></span> 

    ![Ссылка для добавления учетной записи в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="0e392-117">Войдите в учетную запись Azure, ресурсы которой хотите просмотреть.</span><span class="sxs-lookup"><span data-stu-id="0e392-117">Log in to the Azure account whose resources you want to browse.</span></span> 

1. <span data-ttu-id="0e392-118">Войдя в учетную запись Azure, вы увидите подписки, связанные с этой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="0e392-118">Once logged in to an Azure account, the subscriptions associated with that account display.</span></span> <span data-ttu-id="0e392-119">Установите флажки для тех подписок учетной записи, которые вы хотите просмотреть, а затем выберите **Применить**.</span><span class="sxs-lookup"><span data-stu-id="0e392-119">Select the check boxes for the account subscriptions you want to browse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer: выбор подписок Azure для отображения](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="0e392-121">Когда вы завершите выбор нужных подписок, в Cloud Explorer отобразятся все ресурсы этих подписок.</span><span class="sxs-lookup"><span data-stu-id="0e392-121">After selecting the subscriptions whose resources you want to browse, those subscriptions and resources display in the Cloud Explorer.</span></span>

    ![Список ресурсов для учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="0e392-123">Удаление учетной записи Azure в Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0e392-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="0e392-124">В **Cloud Explorer** выберите раздел **Параметры учетной записи Azure**.</span><span class="sxs-lookup"><span data-stu-id="0e392-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Значок параметров учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="0e392-126">Рядом с приложением, которое вы хотите удалить, выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="0e392-126">Next to the account you want to remove, select **Remove**.</span></span>

    ![Значок параметров учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="0e392-128">Просмотр типов или групп ресурсов</span><span class="sxs-lookup"><span data-stu-id="0e392-128">View resource types or resource groups</span></span>
<span data-ttu-id="0e392-129">Для просмотра ресурсов Azure вы можете выбрать представление **Типы ресурсов** или **Группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="0e392-129">To view your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="0e392-130">В **Cloud Explorer** выберите раскрывающийся список представления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0e392-130">In **Cloud Explorer**, select the resource view dropdown.</span></span>

    ![Раскрывающийся список Cloud Explorer, который позволяет выбрать нужное представление ресурсов](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="0e392-132">В контекстном меню выберите нужное представление:</span><span class="sxs-lookup"><span data-stu-id="0e392-132">From the context menu, select the desired view:</span></span> 

    - <span data-ttu-id="0e392-133">Представление **Типы ресурсов**, которое часто используется на [портале Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), отображает ресурсы Azure с упорядочением по типам (веб-приложения, виртуальные машины, учетные записи хранения и т. п.).</span><span class="sxs-lookup"><span data-stu-id="0e392-133">**Resource Types** view - The common view used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="0e392-134">Представление **Группы ресурсов** упорядочивает ресурсы Azure по группам ресурсов Azure, с которыми они связаны.</span><span class="sxs-lookup"><span data-stu-id="0e392-134">**Resource Groups** view - Categorizes Azure resources by the Azure resource group with which they're associated.</span></span> <span data-ttu-id="0e392-135">Группа ресурсов представляет собой набор ресурсов Azure, обычно используемых в конкретном приложении.</span><span class="sxs-lookup"><span data-stu-id="0e392-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="0e392-136">Дополнительные сведения о группах ресурсов Azure см. в статье [Общие сведения о диспетчере ресурсов Azure](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e392-136">To learn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="0e392-137">На следующем рисунке для сравнения изображены оба представления ресурсов:</span><span class="sxs-lookup"><span data-stu-id="0e392-137">The following image shows a comparison of the two resource views:</span></span>

    ![Сравнение представлений ресурсов в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="0e392-139">Просмотр и поиск ресурсов в Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0e392-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="0e392-140">В Cloud Explorer вы можете перейти к ресурсу Azure, чтобы просмотреть связанные сведения. Для этого разверните тип ресурса или группу, к которой он относится, и выберите в списке нужный ресурс.</span><span class="sxs-lookup"><span data-stu-id="0e392-140">To navigate to an Azure resource and view its information in Cloud Explorer, expand the item's type or associated resource group and then select the resource.</span></span> <span data-ttu-id="0e392-141">Когда вы выберете ресурс, информация о нем появится на двух вкладках в нижней части Cloud Explorer — **Действия** и **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="0e392-141">When you select a resource, information appears in the two tabs - **Actions** and **Properties** - at the bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="0e392-142">На вкладке **Действия** отображаются действия, которые можно выполнить в Cloud Explorer для выбранного ресурса.</span><span class="sxs-lookup"><span data-stu-id="0e392-142">**Actions** tab - Lists the actions you can take in Cloud Explorer for the selected resource.</span></span> <span data-ttu-id="0e392-143">Эти же варианты действий можно получить в контекстном меню ресурса, которое открывается по щелчку на ресурсе правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="0e392-143">You can also view these options by right-clicking the resource to view its context menu.</span></span>

- <span data-ttu-id="0e392-144">На вкладке **Свойства** отображаются свойства ресурса, например его тип, язык и региональные стандарты и группа ресурсов, с которой связан ресурс.</span><span class="sxs-lookup"><span data-stu-id="0e392-144">**Properties** tab - Shows the properties of the resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="0e392-145">На следующем рисунке для сравнения представлены сведения, отображаемые на каждой вкладке для службы приложений:</span><span class="sxs-lookup"><span data-stu-id="0e392-145">The following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="0e392-146">Для каждого ресурса доступно действие **Открыть на портале**.</span><span class="sxs-lookup"><span data-stu-id="0e392-146">Every resource has the action **Open in portal**.</span></span> <span data-ttu-id="0e392-147">При выборе этого действия приложение Cloud Explorer отобразит выбранный ресурс на [портале Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="0e392-147">When you choose this action, Cloud Explorer displays the selected resource in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="0e392-148">Функция **Открыть на портале** особенно удобна для перехода к ресурсам с глубоким уровнем вложенности.</span><span class="sxs-lookup"><span data-stu-id="0e392-148">The **Open in portal** feature is handy for navigating to deeply nested resources.</span></span>

<span data-ttu-id="0e392-149">Также для конкретных ресурсов Azure могут отображаться другие действия и свойства.</span><span class="sxs-lookup"><span data-stu-id="0e392-149">Additional actions and property values may also appear based on the Azure resource.</span></span> <span data-ttu-id="0e392-150">Например, для веб-приложений и приложений логики, помимо стандартного действия **Открыть на портале**, также доступны действия **Открыть в браузере** и **Подключить отладчик**.</span><span class="sxs-lookup"><span data-stu-id="0e392-150">For example, web apps and logic apps also have the actions **Open in browser** and **Attach debugger** in addition to **Open in portal**.</span></span> <span data-ttu-id="0e392-151">При выборе больших двоичных объектов учетной записи хранения, очередей или таблиц отображаются действия их открытия в редакторах.</span><span class="sxs-lookup"><span data-stu-id="0e392-151">Actions to open editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="0e392-152">У приложений Azure есть свойства **URL-адрес** и **Состояние**, а для ресурсов хранилища в свойствах указаны ключ доступа и строка подключения.</span><span class="sxs-lookup"><span data-stu-id="0e392-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="0e392-153">Поиск ресурсов в Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0e392-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="0e392-154">Чтобы найти в подписках учетной записи Azure ресурс с известным именем, введите это имя в поле **Поиск** в Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="0e392-154">To locate resources with a specific name in your Azure account subscriptions, enter the name in the **Search** box in Cloud Explorer.</span></span>

![Поиск ресурсов в обозревателе облака](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="0e392-156">По мере ввода символов в поле **Поиск** в дереве ресурсов остаются только те ресурсы, имена которых соответствуют этим символам.</span><span class="sxs-lookup"><span data-stu-id="0e392-156">As you enter characters in the **Search** box, only resources that match those characters appear in the resource tree.</span></span>
