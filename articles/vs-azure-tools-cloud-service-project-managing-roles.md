---
title: "aaaManaging роли в Azure облачными службами с помощью Visual Studio | Документы Microsoft"
description: "Дополнительные сведения об tooadd и удаление ролей в Azure облачных служб с помощью Visual Studio."
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
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="5f8fd-103">Управление ролями в облачных службах Azure с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5f8fd-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="5f8fd-104">После создания облачной службы Azure, можно добавить новый tooit роли или удалить из него существующие роли.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="5f8fd-105">Также можно импортировать существующий проект и преобразовать его tooa роли.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="5f8fd-106">Например, можно импортировать веб-приложение ASP.NET и использовать его в качестве веб-роли.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="5f8fd-107">Добавление роли tooan облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="5f8fd-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="5f8fd-108">Привет, выполнив действия позволят вам добавить веб- или рабочей роли tooan проекта облачной службы Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5f8fd-109">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5f8fd-110">В **обозревателе решений**, разверните узел проекта hello</span><span class="sxs-lookup"><span data-stu-id="5f8fd-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="5f8fd-111">Щелкните правой кнопкой мыши hello **ролей** контекстное меню узла toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="5f8fd-112">Hello контекстном меню, выберите **добавить**, выберите существующий веб-роли или рабочей роли из текущего решения hello, или создайте проект веб- или рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="5f8fd-113">Вы также можете выбрать соответствующий проект, например проект веб-приложения ASP.NET, и связать его с проектом роли.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Параметры меню tooadd роли tooan проекта облачной службы Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="5f8fd-115">Удаление роли из облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="5f8fd-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="5f8fd-116">Hello следующие шаги описывают удаление рабочих и веб-роли из проекта облачной службы Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5f8fd-117">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="5f8fd-118">В **обозревателе решений**, разверните узел проекта hello</span><span class="sxs-lookup"><span data-stu-id="5f8fd-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="5f8fd-119">Разверните hello **ролей** узла.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="5f8fd-120">Щелкните правой кнопкой мыши узел hello tooremove и, hello контекстном меню, выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![Параметры меню tooadd tooan роли облачной службы Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="5f8fd-122">Повторное добавление роли tooan проекта облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="5f8fd-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="5f8fd-123">Если удалить роль из проекта облачной службы, но позднее tooadd hello роль обратно toohello проект, только декларация роли hello и основные атрибуты, такие как конечные точки и диагностические сведения, будут добавлены.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="5f8fd-124">Дополнительные ресурсы или ссылки не будут добавлены toohello `ServiceDefinition.csdef` файл или toohello `ServiceConfiguration.cscfg` файл.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="5f8fd-125">Если вы хотите tooadd эти сведения, необходимые toomanually добавьте его обратно в эти файлы.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="5f8fd-126">Например можно удалить роль веб-службы и позднее tooadd эту роль обратно в ваше решение.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="5f8fd-127">Если это сделать, то произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-127">If you do this, an error occurs.</span></span> <span data-ttu-id="5f8fd-128">tooprevent эту ошибку, у вас есть tooadd hello `<LocalResources>` элемент, показанный в следующие hello XML обратно в hello `ServiceDefinition.csdef` файла.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="5f8fd-129">Используйте имя hello hello веб-службы роли, который вы добавили обратно в проект hello как часть атрибута имени hello hello  **<LocalStorage>**  элемента.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="5f8fd-130">В этом примере hello hello веб-служба роли называется **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="5f8fd-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5f8fd-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f8fd-131">Next steps</span></span>
- [<span data-ttu-id="5f8fd-132">Настройка ролей hello для облачной службы Azure с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5f8fd-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
