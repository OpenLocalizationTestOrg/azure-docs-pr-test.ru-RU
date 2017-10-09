---
title: "Набор масштабирования виртуальных машин с помощью Visual Studio aaaDeploy | Документы Microsoft"
description: "Развертывание набора масштабирования виртуальных машин с помощью Visual Studio и шаблона Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="ee12c-103">Как toocreate набора масштабирования виртуальных машин с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee12c-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="ee12c-104">В этой статье показано, как toodeploy задать с помощью Visual Studio развертывания группы ресурсов Azure масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ee12c-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="ee12c-105">[Azure наборы масштабирования виртуальных машин](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) является toodeploy ресурсов вычислений Azure и управлять коллекцией подобных виртуальных машин с автоматически масштабировать и балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ee12c-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="ee12c-106">Масштабируемые наборы виртуальных машин можно подготавливать и развертывать с помощью [шаблонов Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="ee12c-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="ee12c-107">Шаблоны Azure Resource Manager можно развертывать с помощью Azure CLI, PowerShell, REST, а также непосредственно из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee12c-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="ee12c-108">Visual Studio предоставляет набор примеров шаблонов, которые можно развернуть в рамках проекта развертывания группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ee12c-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="ee12c-109">Развертывания группы ресурсов Azure являются toogroup способом и опубликовать набор связанных ресурсов Azure в одной операции развертывания.</span><span class="sxs-lookup"><span data-stu-id="ee12c-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="ee12c-110">Дополнительные сведения о них можно получить в статье [Создание и развертывание групп ресурсов Azure с помощью Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ee12c-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="ee12c-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ee12c-111">Pre-requisites</span></span>
<span data-ttu-id="ee12c-112">tooget при развертывании набора масштабирования виртуальной машины в Visual Studio, необходимо hello следующее:</span><span class="sxs-lookup"><span data-stu-id="ee12c-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="ee12c-113">Visual Studio 2013 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="ee12c-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="ee12c-114">Пакет SDK Azure версии 2.7, 2.8 или 2.9</span><span class="sxs-lookup"><span data-stu-id="ee12c-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="ee12c-115">При выполнении этих инструкций предполагается, что вы используете Visual Studio с [пакетом SDK Azure версии 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="ee12c-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="ee12c-116">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="ee12c-116">Creating a Project</span></span>
1. <span data-ttu-id="ee12c-117">Создайте проект в Visual Studio, выбрав **Файл | Создать | Проект**.</span><span class="sxs-lookup"><span data-stu-id="ee12c-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Создание файла][file_new]

2. <span data-ttu-id="ee12c-119">В разделе **Visual C# | Облако**, выберите **диспетчера ресурсов Azure** toocreate проекта для развертывания шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ee12c-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Создание проекта][create_project]

3. <span data-ttu-id="ee12c-121">Hello списке шаблонов выберите hello Linux или Windows шаблона набор масштабирования виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ee12c-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Выбор шаблона][select_Template]

4. <span data-ttu-id="ee12c-123">После создания проекта можно увидеть PowerShell скрипты развертывания, шаблона диспетчера ресурсов Azure и файл параметров для набора масштабирования виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="ee12c-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![Обозреватель решений][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="ee12c-125">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="ee12c-125">Customize your project</span></span>
<span data-ttu-id="ee12c-126">Теперь можно изменить шаблон toocustomize hello его для потребностей вашего приложения, такие как добавление свойств расширения виртуальной Машины или редактирования загрузить правила балансировки.</span><span class="sxs-lookup"><span data-stu-id="ee12c-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="ee12c-127">По умолчанию hello шаблоны набор масштабирования виртуальных машин, настроенных toodeploy hello AzureDiagnostics расширения, которое делает его легко tooadd правил автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="ee12c-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="ee12c-128">Кроме того, развертывается подсистема балансировки нагрузки с общедоступным IP-адресом, для которого настроены правила NAT для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="ee12c-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="ee12c-129">Hello балансировки нагрузки позволяет соединить экземпляров виртуальных Машин toohello SSH (Linux) и протокола удаленного рабочего СТОЛА (Windows).</span><span class="sxs-lookup"><span data-stu-id="ee12c-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="ee12c-130">Hello интерфейсный порт начинается с номера 50000.</span><span class="sxs-lookup"><span data-stu-id="ee12c-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="ee12c-131">Для linux это означает, что если вы SSH tooport 50000, являются перенаправленное tooport 22 из hello первая виртуальная машина в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="ee12c-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="ee12c-132">Подключение tooport 50001 — перенаправленное tooport 22 hello второй виртуальной Машины и т. д.</span><span class="sxs-lookup"><span data-stu-id="ee12c-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="ee12c-133">Tooedit хорошим способом шаблонов с помощью Visual Studio — toouse hello структуры JSON tooorganize hello параметры, переменные и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ee12c-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="ee12c-134">Изучив hello схемы Visual Studio можно указать ошибки в шаблоне перед ее развертыванием.</span><span class="sxs-lookup"><span data-stu-id="ee12c-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Обозреватель JSON][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="ee12c-136">Развертывание проекта hello</span><span class="sxs-lookup"><span data-stu-id="ee12c-136">Deploy hello project</span></span>
1. <span data-ttu-id="ee12c-137">Развертывание ресурса набора масштабирования виртуальных машин hello шаблона Azure Resource Manager toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="ee12c-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="ee12c-138">Щелкните правой кнопкой мыши узел проекта hello и выберите **развертывание | Новое развертывание**.</span><span class="sxs-lookup"><span data-stu-id="ee12c-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Развертывание шаблона][5deploy_Template]
    
2. <span data-ttu-id="ee12c-140">Выберите подписку, в диалоговом окне «TooResource развернуть группу» hello.</span><span class="sxs-lookup"><span data-stu-id="ee12c-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![Развертывание шаблона][6deploy_Template]

3. <span data-ttu-id="ee12c-142">Здесь можно создать группы ресурсов Azure toodeploy шаблоне.</span><span class="sxs-lookup"><span data-stu-id="ee12c-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![Создание группы ресурсов][new_resource]

4. <span data-ttu-id="ee12c-144">Далее щелкните **изменение параметров** tooenter параметров, передаваемых tooyour шаблона.</span><span class="sxs-lookup"><span data-stu-id="ee12c-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="ee12c-145">Укажите hello имя пользователя и пароль для hello операционной системы, который является обязательным toocreate hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="ee12c-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="ee12c-146">При отсутствии инструменты PowerShell для установки Visual Studio, рекомендуется toocheck **сохранить пароли** tooavoid скрытые PowerShell, Командная строка запроса или использовать [keyvault поддержки](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="ee12c-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Изменение параметров][edit_parameters]

5. <span data-ttu-id="ee12c-148">Щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="ee12c-148">Now click **Deploy**.</span></span> <span data-ttu-id="ee12c-149">Hello **вывода** окно показывает ход выполнения развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="ee12c-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="ee12c-150">Обратите внимание, что hello действие выполняется hello **Deploy-AzureResourceGroup.ps1** сценария.</span><span class="sxs-lookup"><span data-stu-id="ee12c-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Окно вывода][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="ee12c-152">Изучение масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="ee12c-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="ee12c-153">После завершения развертывания hello, можно просмотреть hello новый набор масштабирования виртуальных машин в Visual Studio hello **Cloud Explorer** (список hello обновления).</span><span class="sxs-lookup"><span data-stu-id="ee12c-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="ee12c-154">Обозреватель облака позволяет управлять ресурсами Azure в Visual Studio при разработке приложений.</span><span class="sxs-lookup"><span data-stu-id="ee12c-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="ee12c-155">Можно также просмотреть набор масштабирования виртуальных машин в hello [портал Azure](https://portal.azure.com) и [обозревателя ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ee12c-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="ee12c-157">Hello портал предоставляет toovisually управления Azure инфраструктурой веб-браузера, а обозревателя ресурсов Azure предоставляет простой способ tooexplore лучше всего hello и отладка ресурсы Azure, предоставляя окна в hello «Просмотр экземпляра» и демонстрируя PowerShell команды для hello ресурсы, которые вы наблюдаете.</span><span class="sxs-lookup"><span data-stu-id="ee12c-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee12c-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee12c-158">Next steps</span></span>
<span data-ttu-id="ee12c-159">После успешного развертывания наборы масштабирования виртуальной машины через Visual Studio можно выполнить дальнейшую настройку вашего проекта toosuit требований приложения.</span><span class="sxs-lookup"><span data-stu-id="ee12c-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="ee12c-160">Например, настройте автоматическое масштабирование, добавив **Insights** ресурса, добавление tooyour инфраструктуры шаблона (например, автономные виртуальные машины) или развертывании приложений с использованием hello расширение пользовательского скрипта.</span><span class="sxs-lookup"><span data-stu-id="ee12c-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="ee12c-161">Хорошим примером шаблоны можно найти в hello [шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates) репозитории GitHub (выполните поиск «vmss»).</span><span class="sxs-lookup"><span data-stu-id="ee12c-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
