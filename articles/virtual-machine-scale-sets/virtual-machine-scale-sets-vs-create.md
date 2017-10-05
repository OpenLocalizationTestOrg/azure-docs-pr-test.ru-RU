---
title: "Развертывание масштабируемого набора виртуальных машин с помощью Visual Studio | Документация Майкрософт"
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
ms.openlocfilehash: 78a4b0c8d305f57f495402cecb92d18425ff6bff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="8d782-103">Как создать масштабируемый набор виртуальных машин с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8d782-103">How to create a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="8d782-104">В этой статье описывается развертывание шаблонов масштабируемых наборов виртуальных машин с использованием развертывания группы ресурсов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8d782-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="8d782-105">[Масштабируемые наборы виртуальных машин Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) — это вычислительный ресурс Azure для развертывания коллекций похожих виртуальных машин с автоматическим масштабированием и балансировкой нагрузки, а также для управления ею.</span><span class="sxs-lookup"><span data-stu-id="8d782-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="8d782-106">Масштабируемые наборы виртуальных машин можно подготавливать и развертывать с помощью [шаблонов Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="8d782-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="8d782-107">Шаблоны Azure Resource Manager можно развертывать с помощью Azure CLI, PowerShell, REST, а также непосредственно из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8d782-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="8d782-108">Visual Studio предоставляет набор примеров шаблонов, которые можно развернуть в рамках проекта развертывания группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8d782-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="8d782-109">Развертывания группы ресурсов Azure позволяют сгруппировать несколько связанных ресурсов Azure и опубликовать их в одной операции развертывания.</span><span class="sxs-lookup"><span data-stu-id="8d782-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="8d782-110">Дополнительные сведения о них можно получить в статье [Создание и развертывание групп ресурсов Azure с помощью Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8d782-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="8d782-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d782-111">Pre-requisites</span></span>
<span data-ttu-id="8d782-112">Чтобы приступить к развертыванию шаблонов масштабируемых наборов виртуальных машин в Visual Studio, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="8d782-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span></span>

* <span data-ttu-id="8d782-113">Visual Studio 2013 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="8d782-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="8d782-114">Пакет SDK Azure версии 2.7, 2.8 или 2.9</span><span class="sxs-lookup"><span data-stu-id="8d782-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="8d782-115">При выполнении этих инструкций предполагается, что вы используете Visual Studio с [пакетом SDK Azure версии 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="8d782-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="8d782-116">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="8d782-116">Creating a Project</span></span>
1. <span data-ttu-id="8d782-117">Создайте проект в Visual Studio, выбрав **Файл | Создать | Проект**.</span><span class="sxs-lookup"><span data-stu-id="8d782-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Создание файла][file_new]

2. <span data-ttu-id="8d782-119">В разделе **Visual C# | Облако** выберите **Azure Resource Manager**, чтобы создать проект для развертывания шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8d782-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Создание проекта][create_project]

3. <span data-ttu-id="8d782-121">В списке шаблонов выберите шаблон масштабируемых наборов виртуальных машин для Linux или Windows.</span><span class="sxs-lookup"><span data-stu-id="8d782-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Выбор шаблона][select_Template]

4. <span data-ttu-id="8d782-123">После создания проекта вы увидите сценарии развертывания PowerShell, шаблон Azure Resource Manager и файл параметров для масштабируемого набора виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8d782-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![Обозреватель решений][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="8d782-125">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="8d782-125">Customize your project</span></span>
<span data-ttu-id="8d782-126">Теперь можно изменить шаблон, настроив его в соответствии с потребностями своего приложения, например, добавить свойства расширения виртуальной машины или изменить правила балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8d782-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="8d782-127">По умолчанию шаблоны масштабируемого набора виртуальных машин настроены для развертывания расширения AzureDiagnostics, которое позволяет легко добавлять правила автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="8d782-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="8d782-128">Кроме того, развертывается подсистема балансировки нагрузки с общедоступным IP-адресом, для которого настроены правила NAT для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="8d782-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="8d782-129">Подсистема балансировки нагрузки позволяет подключаться к экземплярам виртуальных машин по протоколу SSH (Linux) или RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="8d782-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="8d782-130">Диапазон портов клиента начинается с 50000.</span><span class="sxs-lookup"><span data-stu-id="8d782-130">The front-end port range starts at 50000.</span></span> <span data-ttu-id="8d782-131">В случае с Linux это означает, что при подключении к порту 50000 по протоколу SSH, вы будете перенаправлены на порт 22 первой виртуальной машины в наборе,</span><span class="sxs-lookup"><span data-stu-id="8d782-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="8d782-132">а при подключении к порту 50001 вы будете перенаправлены на порт 22 второй виртуальной машины и т. д.</span><span class="sxs-lookup"><span data-stu-id="8d782-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="8d782-133">Удобный способ изменения шаблонов с помощью Visual Studio — использовать структуру JSON для организации параметров, переменных и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8d782-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span></span> <span data-ttu-id="8d782-134">Понимание схемы Visual Studio позволит обнаружить ошибки в шаблоне перед его развертыванием.</span><span class="sxs-lookup"><span data-stu-id="8d782-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Обозреватель JSON][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="8d782-136">Развертывание проекта</span><span class="sxs-lookup"><span data-stu-id="8d782-136">Deploy the project</span></span>
1. <span data-ttu-id="8d782-137">Чтобы создать ресурс масштабируемого набора виртуальных машин, разверните шаблон Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8d782-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="8d782-138">Щелкните узел проекта правой кнопкой мыши и выберите **Развернуть | Новое развертывание**.</span><span class="sxs-lookup"><span data-stu-id="8d782-138">Right-click on the project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Развертывание шаблона][5deploy_Template]
    
2. <span data-ttu-id="8d782-140">Выберите свою подписку в диалоговом окне "Развертывание в группе ресурсов".</span><span class="sxs-lookup"><span data-stu-id="8d782-140">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![Развертывание шаблона][6deploy_Template]

3. <span data-ttu-id="8d782-142">В нем можно создать группу ресурсов Azure, в которую следует развернуть шаблон.</span><span class="sxs-lookup"><span data-stu-id="8d782-142">From here, you can create an Azure Resource Group to deploy your Template to.</span></span>
   
    ![Создание группы ресурсов][new_resource]

4. <span data-ttu-id="8d782-144">Затем нажмите кнопку **Изменить параметры**, чтобы ввести параметры, которые будут переданы шаблону.</span><span class="sxs-lookup"><span data-stu-id="8d782-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span></span> <span data-ttu-id="8d782-145">Укажите имя пользователя и пароль для операционной системы, которые требуются для создания развертывания.</span><span class="sxs-lookup"><span data-stu-id="8d782-145">Provide the username and password for the OS, which is required to create the deployment.</span></span> <span data-ttu-id="8d782-146">Если инструменты PowerShell для Visual Studio не установлены, мы рекомендуем установить флажок **Save passwords** (Сохранить пароли), чтобы избежать скрытого запроса окна командной строки PowerShell, или использовать [поддержку keyvault](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="8d782-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Изменение параметров][edit_parameters]

5. <span data-ttu-id="8d782-148">Щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="8d782-148">Now click **Deploy**.</span></span> <span data-ttu-id="8d782-149">В окне **Вывод** отображается ход развертывания.</span><span class="sxs-lookup"><span data-stu-id="8d782-149">The **Output** window shows the deployment progress.</span></span> <span data-ttu-id="8d782-150">Обратите внимание, что действие выполняет сценарий **Deploy-AzureResourceGroup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="8d782-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Окно вывода][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="8d782-152">Изучение масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="8d782-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="8d782-153">После завершения развертывания можно просмотреть новый масштабируемый набор виртуальных машин в Visual Studio **Cloud Explorer** (обновите список).</span><span class="sxs-lookup"><span data-stu-id="8d782-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="8d782-154">Обозреватель облака позволяет управлять ресурсами Azure в Visual Studio при разработке приложений.</span><span class="sxs-lookup"><span data-stu-id="8d782-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="8d782-155">Масштабируемый набор виртуальных машин также можно просмотреть на [портале Azure](https://portal.azure.com) и в [обозревателе ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8d782-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="8d782-157">С помощью портала удобнее всего визуально управлять инфраструктурой Azure в браузере, а с помощью обозревателя ресурсов Azure — просматривать и отлаживать ресурсы Azure. Обозреватель ресурсов позволяет просматривать состояние экземпляров и использовать для отображаемых ресурсов команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d782-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explore and debug Azure resources, giving a window into the "instance view" and also showing PowerShell commands for the resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d782-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d782-158">Next steps</span></span>
<span data-ttu-id="8d782-159">После успешного развертывания масштабируемых наборов виртуальных машин с помощью Visual Studio можно выполнить дальнейшую настройку проекта в соответствии с требованиями приложения.</span><span class="sxs-lookup"><span data-stu-id="8d782-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="8d782-160">Например, можно настроить автоматическое масштабирование, добавив ресурс **Insights**, добавить инфраструктуру в шаблон в качестве автономных виртуальных машин или развернуть приложения с помощью расширения пользовательского сценария.</span><span class="sxs-lookup"><span data-stu-id="8d782-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span></span> <span data-ttu-id="8d782-161">Хорошим примером шаблонов является репозиторий [Шаблоны быстрого запуска Azure](https://github.com/Azure/azure-quickstart-templates) в GitHub (введите vmss в строке поиска).</span><span class="sxs-lookup"><span data-stu-id="8d782-161">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

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
