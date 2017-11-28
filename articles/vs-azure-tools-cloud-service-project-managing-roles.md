---
title: "Управление ролями в облачных службах Azure с помощью Visual Studio | Документация Майкрософт"
description: "Узнайте, как добавлять и удалять роли в облачных службах Azure с помощью Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 6ed857b857cf8c14506ca39725c214a7fea4fc95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="0692b-103">Управление ролями в облачных службах Azure с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0692b-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="0692b-104">После создания облачной службы Azure можно добавить в нее новые роли или удалить из нее существующие.</span><span class="sxs-lookup"><span data-stu-id="0692b-104">After you have created your Azure cloud service, you can add new roles to it or remove existing roles from it.</span></span> <span data-ttu-id="0692b-105">Вы можете импортировать существующий проект и преобразовать его в роль.</span><span class="sxs-lookup"><span data-stu-id="0692b-105">You can also import an existing project and convert it to a role.</span></span> <span data-ttu-id="0692b-106">Например, можно импортировать веб-приложение ASP.NET и использовать его в качестве веб-роли.</span><span class="sxs-lookup"><span data-stu-id="0692b-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-to-an-azure-cloud-service"></a><span data-ttu-id="0692b-107">Добавление роли в облачную службу Azure</span><span class="sxs-lookup"><span data-stu-id="0692b-107">Adding a role to an Azure cloud service</span></span>
<span data-ttu-id="0692b-108">Ниже приведены пошаговые инструкции по добавлению веб-роли или рабочей роли в проект облачной службы Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0692b-108">The following steps guide you through adding a web or worker role to an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="0692b-109">Создайте или откройте проект облачной службы Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0692b-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="0692b-110">В **обозревателе решений** разверните узел проекта.</span><span class="sxs-lookup"><span data-stu-id="0692b-110">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="0692b-111">Щелкните правой кнопкой мыши узел **Роли**, чтобы отобразилось контекстное меню.</span><span class="sxs-lookup"><span data-stu-id="0692b-111">Right-click the **Roles** node to display the context menu.</span></span> <span data-ttu-id="0692b-112">В контекстном меню выберите команду **Добавить**, а затем выберите существующую веб-роль или рабочую роль в текущем решении либо создайте проект веб-роли или рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="0692b-112">From the context menu, select **Add**, then select an existing web role or worker role from the current solution, or create a web or worker role project.</span></span> <span data-ttu-id="0692b-113">Вы также можете выбрать соответствующий проект, например проект веб-приложения ASP.NET, и связать его с проектом роли.</span><span class="sxs-lookup"><span data-stu-id="0692b-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Параметры меню для добавления роли в проект облачной службы Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="0692b-115">Удаление роли из облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="0692b-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="0692b-116">Ниже приведены пошаговые инструкции по удалению веб-роли или рабочей роли из проекта облачной службы Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0692b-116">The following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="0692b-117">Создайте или откройте проект облачной службы Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0692b-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="0692b-118">В **обозревателе решений** разверните узел проекта.</span><span class="sxs-lookup"><span data-stu-id="0692b-118">In **Solution Explorer**, expand the project node</span></span>

1. <span data-ttu-id="0692b-119">Разверните узел **Роли**.</span><span class="sxs-lookup"><span data-stu-id="0692b-119">Expand the **Roles** node.</span></span>

1. <span data-ttu-id="0692b-120">Щелкните правой кнопкой мыши узел, который необходимо удалить, и в контекстном меню выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="0692b-120">Right-click the node you want to remove, and, from the context menu, select **Remove**.</span></span> 

    ![Параметры меню для добавления роли в облачную службу Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-to-an-azure-cloud-service-project"></a><span data-ttu-id="0692b-122">Повторное добавление роли в проект облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="0692b-122">Readding a role to an Azure cloud service project</span></span>
<span data-ttu-id="0692b-123">Если вы удалите роль из своего проекта облачной службы, но позже захотите снова добавить ее в проект, то будут добавлены только объявления роли и ее основные атрибуты, такие как сведения диагностики и информация о конечных точках.</span><span class="sxs-lookup"><span data-stu-id="0692b-123">If you remove a role from your cloud service project but later decide to add the role back to the project, only the role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="0692b-124">В файлы `ServiceDefinition.csdef` или `ServiceConfiguration.cscfg` не добавляются другие ресурсы и ссылки.</span><span class="sxs-lookup"><span data-stu-id="0692b-124">No additional resources or references are added to the `ServiceDefinition.csdef` file or to the `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="0692b-125">Если вы хотите добавить эту информацию в файлы, то придется сделать это вручную.</span><span class="sxs-lookup"><span data-stu-id="0692b-125">If you want to add this information, you need to manually add it back into these files.</span></span>

<span data-ttu-id="0692b-126">Предположим, вы удалили роль веб-службы, а затем решили вернуть ее обратно в решение.</span><span class="sxs-lookup"><span data-stu-id="0692b-126">For example, you might remove a web service role and later you decide to add this role back into your solution.</span></span> <span data-ttu-id="0692b-127">Если это сделать, то произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="0692b-127">If you do this, an error occurs.</span></span> <span data-ttu-id="0692b-128">Чтобы ее избежать, необходимо добавить элемент `<LocalResources>`, показанный в следующем XML-блоке, обратно в файл `ServiceDefinition.csdef`.</span><span class="sxs-lookup"><span data-stu-id="0692b-128">To prevent this error, you have to add the `<LocalResources>` element shown in the following XML back into the `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="0692b-129">Используйте имя роли веб-службы, добавленной в проект, в составе атрибута name в элементе **<LocalStorage>** .</span><span class="sxs-lookup"><span data-stu-id="0692b-129">Use the name of the web service role that you added back into the project as part of the name attribute for the **<LocalStorage>** element.</span></span> <span data-ttu-id="0692b-130">В этом примере используется роль веб-службы с именем **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="0692b-130">In this example, the name of the web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="0692b-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0692b-131">Next steps</span></span>
- [<span data-ttu-id="0692b-132">Настройка ролей для облачной службы Azure в среде Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0692b-132">Configure the Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
