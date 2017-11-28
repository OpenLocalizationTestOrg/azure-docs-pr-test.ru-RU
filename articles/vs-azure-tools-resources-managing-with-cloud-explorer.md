---
title: "aaaManaging Azure ресурсы с Cloud Explorer | Документы Microsoft"
description: "Узнайте, как toobrowse Cloud Explorer toouse и настраивать ресурсы Azure в Visual Studio."
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
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="32cb6-103">Управление hello ресурсы, связанные с учетными записями Azure в Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="32cb6-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="32cb6-104">Cloud Explorer позволяет вам tooview ресурсами Azure и группы ресурсов, проверьте их свойства и выполнять действия диагностики ключа разработчика в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="32cb6-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="32cb6-105">Как hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer строится hello стеке диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="32cb6-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="32cb6-106">Благодаря этому Cloud Explorer распознает ресурсы (например, группы ресурсов Azure) и службы Azure (например, Logic Apps и API-приложения), а также поддерживает [управление доступом на основе ролей](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="32cb6-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="32cb6-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="32cb6-107">Prerequisites</span></span>
- <span data-ttu-id="32cb6-108">[Visual Studio 2017 г](https://www.visualstudio.com/downloads/) с hello **рабочей нагрузки Azure** выбран, или более ранней версии Visual Studio с hello [Microsoft Azure SDK для .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="32cb6-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="32cb6-109">Учетная запись Azure. Если у вас ее нет, [зарегистрируйтесь для работы с бесплатной пробной версией](http://go.microsoft.com/fwlink/?LinkId=623901) или [активируйте преимущества для подписчиков Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="32cb6-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="32cb6-110">Выберите tooview Cloud Explorer **представление** > **Cloud Explorer** hello меню.</span><span class="sxs-lookup"><span data-stu-id="32cb6-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="32cb6-111">Добавьте учетную запись Azure tooCloud обозревателя</span><span class="sxs-lookup"><span data-stu-id="32cb6-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="32cb6-112">tooview hello ресурсы, связанные с учетной записью Azure, необходимо сначала добавить tooCloud учетной записи hello обозревателя.</span><span class="sxs-lookup"><span data-stu-id="32cb6-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="32cb6-113">В **Cloud Explorer** выберите раздел **Параметры учетной записи Azure**.</span><span class="sxs-lookup"><span data-stu-id="32cb6-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Значок параметров учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="32cb6-115">Выберите **Добавить новую учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="32cb6-115">Select **Add new account**.</span></span> 

    ![Ссылка для добавления учетной записи в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="32cb6-117">Вход toohello учетная запись Azure, ресурсы которого вы хотите toobrowse.</span><span class="sxs-lookup"><span data-stu-id="32cb6-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="32cb6-118">После входа в учетную запись Azure tooan отображения hello подписок, связанных с этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="32cb6-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="32cb6-119">Здравствуйте, установите флажки для подписок hello toobrowse и затем выберите **применить**.</span><span class="sxs-lookup"><span data-stu-id="32cb6-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer: выберите toodisplay подписок Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="32cb6-121">После выбора подписки hello, ресурсы которого требуется toobrowse, эти подписки и ресурсы отображения в Cloud Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="32cb6-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Список ресурсов для учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="32cb6-123">Удаление учетной записи Azure в Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="32cb6-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="32cb6-124">В **Cloud Explorer** выберите раздел **Параметры учетной записи Azure**.</span><span class="sxs-lookup"><span data-stu-id="32cb6-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Значок параметров учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="32cb6-126">Выберите Далее toohello счета, tooremove, **удалить**.</span><span class="sxs-lookup"><span data-stu-id="32cb6-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Значок параметров учетной записи Azure в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="32cb6-128">Просмотр типов или групп ресурсов</span><span class="sxs-lookup"><span data-stu-id="32cb6-128">View resource types or resource groups</span></span>
<span data-ttu-id="32cb6-129">tooview ресурсы Azure, вы также можете выбрать **типов ресурсов** или **групп ресурсов** представления.</span><span class="sxs-lookup"><span data-stu-id="32cb6-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="32cb6-130">В **Cloud Explorer**, выберите hello раскрывающийся список представление ресурса.</span><span class="sxs-lookup"><span data-stu-id="32cb6-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Облако раскрывающемся списке tooselect hello требуемого ресурсы обозревателя](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="32cb6-132">Hello контекстном меню выберите представление требуемого hello:</span><span class="sxs-lookup"><span data-stu-id="32cb6-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="32cb6-133">**Типы ресурсов** представление — используется на hello общее представление hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), показывает ресурсов Azure категории по своему типу, например веб-приложений, учетные записи хранилища и виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="32cb6-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="32cb6-134">**Группы ресурсов** представление - Azure распределяет ресурсы по hello группы ресурсов Azure, с которым они связаны.</span><span class="sxs-lookup"><span data-stu-id="32cb6-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="32cb6-135">Группа ресурсов представляет собой набор ресурсов Azure, обычно используемых в конкретном приложении.</span><span class="sxs-lookup"><span data-stu-id="32cb6-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="32cb6-136">toolearn Дополнительные сведения о группах ресурсов Azure в разделе [Обзор диспетчера ресурсов Azure](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32cb6-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="32cb6-137">Hello следующий рисунок показывает сравнение hello два представления ресурсов:</span><span class="sxs-lookup"><span data-stu-id="32cb6-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Сравнение представлений ресурсов в Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="32cb6-139">Просмотр и поиск ресурсов в Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="32cb6-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="32cb6-140">toonavigate tooan ресурсов Azure и просмотра его информации в Cloud Explorer разверните hello элемента типа или группы связанных ресурсов и затем выберите hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32cb6-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="32cb6-141">При выборе ресурса информация отображается на вкладках hello двух - **действия** и **свойства** - внизу hello Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="32cb6-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="32cb6-142">**Действия** вкладке - списки hello действия в Cloud Explorer для hello выбранного ресурса.</span><span class="sxs-lookup"><span data-stu-id="32cb6-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="32cb6-143">Можно также просмотреть этих параметров щелкните правой кнопкой мыши ресурс tooview hello его контекстное меню.</span><span class="sxs-lookup"><span data-stu-id="32cb6-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="32cb6-144">**Свойства** вкладке - показывает свойства hello hello ресурсов, например его тип, языкового стандарта и ресурсов группы, с которым он связан.</span><span class="sxs-lookup"><span data-stu-id="32cb6-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="32cb6-145">Hello иллюстрации показан пример сравнение отображаемые на каждой вкладке для приложения службы.</span><span class="sxs-lookup"><span data-stu-id="32cb6-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="32cb6-146">Каждый ресурс имеет действие hello **открыть на портале**.</span><span class="sxs-lookup"><span data-stu-id="32cb6-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="32cb6-147">При выборе этого действия Cloud Explorer отображает hello выбранных ресурсов в hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="32cb6-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="32cb6-148">Hello **открыть на портале** функция удобно для перемещения по toodeeply вложенных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32cb6-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="32cb6-149">Дополнительные действия и значения свойств, также появляются основании hello ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="32cb6-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="32cb6-150">Например, веб-приложений и логика приложения также необходим hello действия **открыть в браузере** и **присоединить отладчик** Кроме слишком**открыть на портале**.</span><span class="sxs-lookup"><span data-stu-id="32cb6-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="32cb6-151">Редакторы tooopen действия появляются, если выбрать BLOB-объекта учетной записи хранилища, очередей или таблиц.</span><span class="sxs-lookup"><span data-stu-id="32cb6-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="32cb6-152">У приложений Azure есть свойства **URL-адрес** и **Состояние**, а для ресурсов хранилища в свойствах указаны ключ доступа и строка подключения.</span><span class="sxs-lookup"><span data-stu-id="32cb6-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="32cb6-153">Поиск ресурсов в Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="32cb6-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="32cb6-154">ресурсы toolocate с определенным именем в подписках Azure учетной записи, введите имя hello в hello **поиска** поле в Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="32cb6-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![Поиск ресурсов в обозревателе облака](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="32cb6-156">По мере ввода символов в hello **поиска** поле только те ресурсы, которые соответствуют эти символы отображаются в дереве ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="32cb6-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
