---
title: "aaaGet к работе с шаблонами закрытый | Документы Microsoft"
description: "Добавить, управление и совместное использование вашей частной шаблонов с помощью портала Azure hello, hello Azure CLI или PowerShell."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="45cfa-103">Приступая к работе с частной шаблоны на портале Azure hello</span><span class="sxs-lookup"><span data-stu-id="45cfa-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="45cfa-104">[Диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md) шаблон — использовать декларативные шаблон toodefine развертывания.</span><span class="sxs-lookup"><span data-stu-id="45cfa-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="45cfa-105">Можно определить hello toodeploy ресурсы для решения и укажите параметры и переменные, позволяющие tooinput значения для различных сред.</span><span class="sxs-lookup"><span data-stu-id="45cfa-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="45cfa-106">Hello шаблон состоит из выражения, которые можно использовать и JSON tooconstruct значения для вашего развертывания.</span><span class="sxs-lookup"><span data-stu-id="45cfa-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="45cfa-107">Можно использовать новый hello **шаблоны** возможность hello [портала Azure](https://portal.azure.com) вместе с hello **Microsoft.Gallery** поставщика ресурсов как расширение hello [ Azure Marketplace](https://azure.microsoft.com/marketplace/) toocreate tooenable пользователей, управление и развертывание частного шаблоны из библиотеки личных.</span><span class="sxs-lookup"><span data-stu-id="45cfa-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="45cfa-108">В этом документе описан процесс добавления, управления и совместного использования закрытого **шаблона** с помощью портала Azure "hello".</span><span class="sxs-lookup"><span data-stu-id="45cfa-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="45cfa-109">Руководство</span><span class="sxs-lookup"><span data-stu-id="45cfa-109">Guidance</span></span>
<span data-ttu-id="45cfa-110">Hello следующие советы помогут вам воспользоваться всеми преимуществами **шаблоны** при работе с вашего решения:</span><span class="sxs-lookup"><span data-stu-id="45cfa-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="45cfa-111">**Шаблон** представляет собой инкапсулирующий ресурс, который содержит шаблон Resource Manager и дополнительные метаданные.</span><span class="sxs-lookup"><span data-stu-id="45cfa-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="45cfa-112">Оно работает почти так же tooan элемента в hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="45cfa-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="45cfa-113">Ключевое различие Hello — это закрытый элемент как противоположность toohello открытые элементы Marketplace.</span><span class="sxs-lookup"><span data-stu-id="45cfa-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="45cfa-114">Hello **шаблоны** библиотека хорошо работает для пользователей, которым необходим toocustomize их развертывания.</span><span class="sxs-lookup"><span data-stu-id="45cfa-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="45cfa-115">**Шаблоны** хорошо подходят пользователям, которым необходим простой репозиторий в Azure.</span><span class="sxs-lookup"><span data-stu-id="45cfa-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="45cfa-116">Начните работу с существующего шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45cfa-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="45cfa-117">Шаблоны можно найти на портале [GitHub](https://github.com/Azure/azure-quickstart-templates) или [экспортировать шаблон](../azure-resource-manager/resource-manager-export-template.md) из имеющейся группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="45cfa-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="45cfa-118">**Шаблоны** являетесь пользователем равноценных toohello, и публикует его.</span><span class="sxs-lookup"><span data-stu-id="45cfa-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="45cfa-119">Имя издателя Hello является видимым tooeveryone, кто имеет доступ на чтение tooit.</span><span class="sxs-lookup"><span data-stu-id="45cfa-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="45cfa-120">**Шаблоны** — это ресурсы Resource Manager. Их нельзя переименовать после публикации.</span><span class="sxs-lookup"><span data-stu-id="45cfa-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="45cfa-121">Добавление ресурса шаблона</span><span class="sxs-lookup"><span data-stu-id="45cfa-121">Add a Template resource</span></span>
<span data-ttu-id="45cfa-122">Существует два способа toocreate **шаблона** ресурса в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="45cfa-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="45cfa-123">Способ 1. Создание нового ресурса шаблона из работающей группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="45cfa-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="45cfa-124">Перейдите tooan существующую группу ресурсов на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="45cfa-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="45cfa-125">В разделе **Параметры** выберите **Export template** (Экспорт шаблона).</span><span class="sxs-lookup"><span data-stu-id="45cfa-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="45cfa-126">После экспорта шаблона диспетчера ресурсов hello использовать hello **сохранить шаблон** toosave кнопку его toohello **шаблоны** репозитория.</span><span class="sxs-lookup"><span data-stu-id="45cfa-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="45cfa-127">Дополнительные сведения об экспорте шаблона см. [здесь](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="45cfa-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="45cfa-128">
   ![Resource group export](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="45cfa-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="45cfa-129">Выберите hello **сохранить tooTemplate** кнопку команды.</span><span class="sxs-lookup"><span data-stu-id="45cfa-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="45cfa-130">Введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="45cfa-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="45cfa-131">Имя — имя объекта шаблона hello (Примечание: это имя на основе диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="45cfa-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="45cfa-132">К нему применяются все ограничения именования, и его нельзя изменить после создания).</span><span class="sxs-lookup"><span data-stu-id="45cfa-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="45cfa-133">Описание — краткая сводка о шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="45cfa-133">Description – Quick summary about hello template.</span></span>
     
     ![Сохранение шаблона](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="45cfa-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="45cfa-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="45cfa-136">Hello колонке экспорта шаблона отображения уведомлений при hello экспортированный шаблон диспетчера ресурсов содержит ошибки, но будет по-прежнему может toosave этот toohello шаблона диспетчера ресурсов шаблонов.</span><span class="sxs-lookup"><span data-stu-id="45cfa-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="45cfa-137">Убедитесь, что проверка и устранение проблемы с шаблонами любой диспетчер ресурсов, перед экспортом hello повторного развертывания шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="45cfa-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="45cfa-138">Способ 2. Добавление нового ресурса шаблона с помощью команды "Обзор"</span><span class="sxs-lookup"><span data-stu-id="45cfa-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="45cfa-139">Также можно добавить новый **шаблона** с нуля с помощью hello + добавить кнопки в **Обзор > шаблоны**.</span><span class="sxs-lookup"><span data-stu-id="45cfa-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="45cfa-140">Tooprovide нужно присвоить имя, описание и hello шаблона диспетчера ресурсов JSON.</span><span class="sxs-lookup"><span data-stu-id="45cfa-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![Добавление шаблона](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="45cfa-142">Microsoft.Gallery — это поставщик ресурсов Azure на основе клиента.</span><span class="sxs-lookup"><span data-stu-id="45cfa-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="45cfa-143">Hello ресурс шаблона — связанные toohello пользователь, создавший его.</span><span class="sxs-lookup"><span data-stu-id="45cfa-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="45cfa-144">Это не равноценных tooany конкретной подписки.</span><span class="sxs-lookup"><span data-stu-id="45cfa-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="45cfa-145">Подписка должна toobe выбран только при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="45cfa-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="45cfa-146">Просмотр ресурсов шаблонов</span><span class="sxs-lookup"><span data-stu-id="45cfa-146">View Template resources</span></span>
<span data-ttu-id="45cfa-147">Все **шаблоны** доступных tooyou можно увидеть в **Обзор > шаблоны**.</span><span class="sxs-lookup"><span data-stu-id="45cfa-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="45cfa-148">Сюда входят созданные вами **шаблоны**, а также шаблоны, к которым вам предоставлен общий доступ с различными уровнями разрешений.</span><span class="sxs-lookup"><span data-stu-id="45cfa-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="45cfa-149">Дополнительные сведения содержатся в hello [управления доступом к](#access-control-for-a-tenant-resource-provider) разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="45cfa-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Просмотр шаблона](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="45cfa-151">Вы можете просмотреть сведения hello объекта **шаблона** , щелкнув элемент в списке hello.</span><span class="sxs-lookup"><span data-stu-id="45cfa-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![Просмотр шаблона](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="45cfa-153">Изменение ресурса шаблона</span><span class="sxs-lookup"><span data-stu-id="45cfa-153">Edit a Template resource</span></span>
<span data-ttu-id="45cfa-154">Можно инициировать поток hello редактирования для **шаблона** , щелкнув правой кнопкой мыши элемент hello списке обзора hello или выбрав кнопки команды правки hello.</span><span class="sxs-lookup"><span data-stu-id="45cfa-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![Изменение шаблона](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="45cfa-156">Можно изменить описание hello или текст шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="45cfa-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="45cfa-157">Невозможно изменить имя hello, так как это имя ресурса диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="45cfa-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="45cfa-158">При редактировании шаблона диспетчера ресурсов hello JSON мы выполнит проверку tooensure, что это допустимые данные JSON.</span><span class="sxs-lookup"><span data-stu-id="45cfa-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="45cfa-159">Выберите **ОК** и затем **Сохранить** toosave обновленный шаблон.</span><span class="sxs-lookup"><span data-stu-id="45cfa-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![Изменение шаблона](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="45cfa-161">Здравствуйте, один раз **шаблона** сохраняется вы увидите подтверждение.</span><span class="sxs-lookup"><span data-stu-id="45cfa-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![Изменение шаблона](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="45cfa-163">Развертывание ресурса шаблона</span><span class="sxs-lookup"><span data-stu-id="45cfa-163">Deploy a Template resource</span></span>
<span data-ttu-id="45cfa-164">Вы можете развернуть любой **шаблон**, для которого у вас есть разрешения на **чтение**.</span><span class="sxs-lookup"><span data-stu-id="45cfa-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="45cfa-165">поток развертывания Hello запускает hello стандартный шаблон Azure развертывания колонку.</span><span class="sxs-lookup"><span data-stu-id="45cfa-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="45cfa-166">Заполните значения hello tooproceed параметры шаблона диспетчера ресурсов hello с развертыванием hello.</span><span class="sxs-lookup"><span data-stu-id="45cfa-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![Развертывание шаблона](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="45cfa-168">Совместное использование ресурса шаблона</span><span class="sxs-lookup"><span data-stu-id="45cfa-168">Share a Template resource</span></span>
<span data-ttu-id="45cfa-169">Ресурс **шаблона** можно использовать совместно с коллегами.</span><span class="sxs-lookup"><span data-stu-id="45cfa-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="45cfa-170">Совместное использование ведет себя аналогично слишком[назначение ролей для любой ресурс в Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="45cfa-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="45cfa-171">Hello **шаблона** владелец предоставляет разрешения tooother пользователей, которые могут взаимодействовать с ресурс шаблона.</span><span class="sxs-lookup"><span data-stu-id="45cfa-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="45cfa-172">Hello пользователь или группа людей используют hello **шаблона** с будет шаблона диспетчера ресурсов может toosee hello и его свойств в коллекции.</span><span class="sxs-lookup"><span data-stu-id="45cfa-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="45cfa-173">Управление доступом к ресурсам Microsoft.Gallery hello</span><span class="sxs-lookup"><span data-stu-id="45cfa-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="45cfa-174">Роль</span><span class="sxs-lookup"><span data-stu-id="45cfa-174">Role</span></span> | <span data-ttu-id="45cfa-175">Разрешения</span><span class="sxs-lookup"><span data-stu-id="45cfa-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="45cfa-176">Владелец</span><span class="sxs-lookup"><span data-stu-id="45cfa-176">Owner</span></span> |<span data-ttu-id="45cfa-177">Разрешает полный доступ на ресурс шаблона hello, включая общую папку</span><span class="sxs-lookup"><span data-stu-id="45cfa-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="45cfa-178">читатель.</span><span class="sxs-lookup"><span data-stu-id="45cfa-178">Reader</span></span> |<span data-ttu-id="45cfa-179">Разрешает чтение и Execute(Deploy) на ресурсе шаблона hello</span><span class="sxs-lookup"><span data-stu-id="45cfa-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="45cfa-180">Участник</span><span class="sxs-lookup"><span data-stu-id="45cfa-180">Contributor</span></span> |<span data-ttu-id="45cfa-181">Позволяет изменить и удалить разрешение hello ресурс шаблона.</span><span class="sxs-lookup"><span data-stu-id="45cfa-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="45cfa-182">Пользователь не могут совместно использовать hello шаблона с другими пользователями</span><span class="sxs-lookup"><span data-stu-id="45cfa-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="45cfa-183">Выберите **общего ресурса** hello Обзор элемента, щелкните правой кнопкой мыши или в колонке hello представление определенного элемента.</span><span class="sxs-lookup"><span data-stu-id="45cfa-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="45cfa-184">Так вы сможете предоставить общий доступ к ресурсу другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="45cfa-184">This launches a Share experience.</span></span>

![Совместное использование шаблона](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="45cfa-186">Теперь можно выбрать роль и пользователь или группа tooprovide доступа tooa определенной **шаблона**.</span><span class="sxs-lookup"><span data-stu-id="45cfa-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="45cfa-187">Доступные роли Hello, владельца, чтения и участника.</span><span class="sxs-lookup"><span data-stu-id="45cfa-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="45cfa-188">Дополнительные сведения содержатся в hello [управления доступом к](#access-control-for-a-tenant-resource-provider) выше.</span><span class="sxs-lookup"><span data-stu-id="45cfa-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Совместное использование шаблона](media/share-template-portal2b.png)  <br />

![Совместное использование шаблона](media/share-template-portal3b.png)  <br />

<span data-ttu-id="45cfa-191">Щелкните **Выбрать** и **ОК**.</span><span class="sxs-lookup"><span data-stu-id="45cfa-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="45cfa-192">Теперь можно увидеть hello пользователи или группы добавлены toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="45cfa-192">You can now see hello users or groups you added toohello resource.</span></span>

![Совместное использование шаблона](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="45cfa-194">Шаблон можно использовать только совместно с пользователями и группами в hello того же клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="45cfa-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="45cfa-195">Если шаблон используется совместно с адресом электронной почты, которая не находится в клиенте, приглашения будут отправляться попросить клиента hello toojoin hello пользователя как Гость.</span><span class="sxs-lookup"><span data-stu-id="45cfa-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="45cfa-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="45cfa-196">Next steps</span></span>
* <span data-ttu-id="45cfa-197">в разделе toolearn о создании шаблонов диспетчера ресурсов [разработки шаблонов](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="45cfa-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="45cfa-198">см. в шаблоне диспетчера ресурсов, можно использовать функции hello toounderstand [функции шаблонов](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="45cfa-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="45cfa-199">Рекомендации по разработке шаблонов Azure Resource Manager см. в [этой статье](../azure-resource-manager/best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="45cfa-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

