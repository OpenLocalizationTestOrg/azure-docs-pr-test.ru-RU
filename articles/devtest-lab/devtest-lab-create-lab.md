---
title: "Создание лаборатории в Azure DevTest Labs | Документация Майкрософт"
description: "Создание лаборатории в Azure DevTest Labs для виртуальных машин"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 265a968f902f53c7561c8c7e937f8eacfdb37167
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="bcb76-103">Создание лаборатории в лаборатории для разработки и тестирования Azure</span><span class="sxs-lookup"><span data-stu-id="bcb76-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="bcb76-104">Azure DevTest Labs — это инфраструктура, которая содержит группу ресурсов, таких как виртуальные машины, позволяющую более эффективно управлять этими ресурсами за счет установки ограничений и квот.</span><span class="sxs-lookup"><span data-stu-id="bcb76-104">A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="bcb76-105">В этой статье показано, как создать лабораторию с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb76-105">This article walks you through the process of creating a lab using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcb76-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bcb76-106">Prerequisites</span></span>
<span data-ttu-id="bcb76-107">Чтобы создать лабораторию, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="bcb76-107">To create a lab, you need:</span></span>

* <span data-ttu-id="bcb76-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb76-108">An Azure subscription.</span></span> <span data-ttu-id="bcb76-109">Дополнительные сведения о вариантах приобретения Azure см. на страницах [Как приобрести Azure](https://azure.microsoft.com/pricing/purchase-options/) и [Бесплатный ознакомительный период в один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bcb76-109">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="bcb76-110">Для создания лаборатории необходимо быть владельцем подписки.</span><span class="sxs-lookup"><span data-stu-id="bcb76-110">You must be the owner of the subscription to create the lab.</span></span>

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="bcb76-111">Создание лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bcb76-111">Steps to create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="bcb76-112">Ниже показано, как с помощью портала Azure создать лабораторию в Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="bcb76-112">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="bcb76-113">Выполните вход на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="bcb76-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="bcb76-114">В главном меню слева выберите **Больше служб** (в нижней части списка).</span><span class="sxs-lookup"><span data-stu-id="bcb76-114">From the main menu on the left side, select **More Services** (at the bottom of the list).</span></span>

    ![Пункт меню "Больше служб"](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="bcb76-116">В списке доступных служб выберите **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="bcb76-116">From the list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="bcb76-117">В колонке **DevTest Labs** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bcb76-117">On the **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Добавление лаборатории](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="bcb76-119">В колонке **Создание лаборатории для разработки и тестирования** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="bcb76-119">On the **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="bcb76-120">Введите **имя лаборатории** .</span><span class="sxs-lookup"><span data-stu-id="bcb76-120">Enter a **Lab Name** for the new lab.</span></span>
    2. <span data-ttu-id="bcb76-121">Выберите **подписку** , которую необходимо связать с лабораторией.</span><span class="sxs-lookup"><span data-stu-id="bcb76-121">Select the **Subscription** to associate with the lab.</span></span>
    3. <span data-ttu-id="bcb76-122">Выберите **расположение** , в котором будет храниться лаборатория.</span><span class="sxs-lookup"><span data-stu-id="bcb76-122">Select a **Location** in which to store the lab.</span></span>
    4. <span data-ttu-id="bcb76-123">Выберите **Автоматическое завершение работы** , чтобы включить и определить параметры автоматического завершения работы всех виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="bcb76-123">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span></span> <span data-ttu-id="bcb76-124">Компонент автоматического завершения работы предназначен главным образом для экономии затрат. При этом вы можете указать, когда следует автоматически завершать работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bcb76-124">The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down.</span></span> <span data-ttu-id="bcb76-125">Вы можете изменить настройки автоматического завершения работы после создания лаборатории. Для этого нужно выполнить инструкции из раздела [Настройка автоматического завершения работы](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="bcb76-125">You can change auto-shutdown settings after creating the lab by following the steps outlined in the article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="bcb76-126">Выберите **Закрепить на панели мониторинга**, чтобы отобразить ярлык лаборатории на панели мониторинга портала.</span><span class="sxs-lookup"><span data-stu-id="bcb76-126">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span></span>
    6. <span data-ttu-id="bcb76-127">Выберите **Параметры автоматизации**, чтобы получить шаблоны Azure Resource Manager для автоматизации настройки.</span><span class="sxs-lookup"><span data-stu-id="bcb76-127">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="bcb76-128">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bcb76-128">Select **Create**.</span></span> <span data-ttu-id="bcb76-129">После того как вы нажмете кнопку **Создать**, откроется колонка **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="bcb76-129">After selecting **Create**, the **DevTest Labs** blade displays.</span></span> <span data-ttu-id="bcb76-130">Вы можете отслеживать состояние создания лаборатории в области **Уведомления**.</span><span class="sxs-lookup"><span data-stu-id="bcb76-130">You can monitor the status of the lab creation process by watching the **Notifications** area.</span></span> <span data-ttu-id="bcb76-131">После завершения процесса обновите страницу, чтобы увидеть только что созданную лабораторию в списке лабораторий.</span><span class="sxs-lookup"><span data-stu-id="bcb76-131">Once completed, refresh the page to see the newly created lab in the list of labs.</span></span>  
    
    ![Колонка создания лаборатории](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="bcb76-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bcb76-133">Next steps</span></span>
<span data-ttu-id="bcb76-134">Создав лабораторию, можно выполнить дальнейшие действия, приведенные ниже.</span><span class="sxs-lookup"><span data-stu-id="bcb76-134">Once you've created your lab, here are some next steps to consider:</span></span>

* <span data-ttu-id="bcb76-135">[Безопасный доступ к лаборатории](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="bcb76-135">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="bcb76-136">[Определение политик лаборатории](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="bcb76-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="bcb76-137">[Создание шаблона лаборатории](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="bcb76-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="bcb76-138">[Создание пользовательских артефактов для виртуальных машин](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="bcb76-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="bcb76-139">[Добавление виртуальной машины с артефактами в лабораторию](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="bcb76-139">[Add a VM with artifacts to a lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

