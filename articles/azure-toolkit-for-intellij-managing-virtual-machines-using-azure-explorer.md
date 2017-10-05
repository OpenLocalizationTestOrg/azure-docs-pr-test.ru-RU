---
title: "Управление виртуальными машинами с помощью Azure Explorer для IntelliJ | Документация Майкрософт"
description: "Вы можете узнать, как управлять виртуальными машинами Azure с помощью Azure Explorer для IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 9197580407b3509fbf9a842e1fee1e6348478c34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="22a62-103">Управление виртуальными машинами с помощью Azure Explorer для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="22a62-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="22a62-104">Azure Explorer, входящий в состав набора средств Azure для IntelliJ, предоставляет разработчикам на Java удобное решение для управления виртуальными машинами в их учетной записи Azure из интегрированной среды разработки IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="22a62-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="22a62-105">Создание виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="22a62-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="22a62-106">Чтобы создать виртуальную машину с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="22a62-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="22a62-107">Войдите в свою учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="22a62-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="22a62-108">В представлении **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши **Виртуальные машины** и выберите **Создать виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="22a62-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="22a62-109">![Команда "Создать виртуальную машину"][CR01]</span><span class="sxs-lookup"><span data-stu-id="22a62-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="22a62-110">Откроется мастер **создания виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="22a62-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="22a62-111">В диалоговом окне **Выбор подписки** выберите подписку и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="22a62-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Диалоговое окно "Выбор подписки"][CR02]

4. <span data-ttu-id="22a62-113">В диалоговом окне **Выбор образа виртуальной машины** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="22a62-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="22a62-114">**Расположение**: указывает расположение для создания виртуальной машины (например, *Западная часть США*).</span><span class="sxs-lookup"><span data-stu-id="22a62-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="22a62-115">**Recommended Image** (Рекомендуемый образ): указывает, что вы выберете образ из сокращенного списка часто используемых образов.</span><span class="sxs-lookup"><span data-stu-id="22a62-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="22a62-116">**Пользовательский образ**: указывает, что вы выберете пользовательский образ, указав следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="22a62-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="22a62-117">**Издатель**: указывает издателя, создавшего образ, который будет использоваться для виртуальной машины (например, *Майкрософт*).</span><span class="sxs-lookup"><span data-stu-id="22a62-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="22a62-118">**Предложение**: определяет предложение виртуальной машины выбранного издателя (например, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="22a62-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="22a62-119">**SKU**: указывает нужный номер SKU из выбранного предложения (например, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="22a62-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="22a62-120">**Номер версии**: указывает, какую версию из выбранного номера SKU нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="22a62-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Диалоговое окно "Выбор образа виртуальной машины"][CR03]

5. <span data-ttu-id="22a62-122">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="22a62-122">Click **Next**.</span></span> 

6. <span data-ttu-id="22a62-123">В диалоговом окне **Основные параметры виртуальной машины** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="22a62-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="22a62-124">**Имя виртуальной машины**: указывает имя новой виртуальной машины, которое должно начинаться с буквы и содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="22a62-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="22a62-125">**Размер**: указывает количество ядер и объем памяти, выделяемые для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="22a62-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="22a62-126">**Имя пользователя**: указывает учетную запись администратора, создаваемую для управления виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="22a62-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="22a62-127">**Пароль** и **Подтверждение**: указывают пароль для учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="22a62-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Диалоговое окно "Основные параметры виртуальной машины"][CR04]

7. <span data-ttu-id="22a62-129">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="22a62-129">Click **Next**.</span></span> 

8. <span data-ttu-id="22a62-130">В диалоговом окне **Связанные ресурсы** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="22a62-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="22a62-131">**Группа ресурсов**: указывает группу ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="22a62-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="22a62-132">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="22a62-132">Select one of the following options:</span></span>
      * <span data-ttu-id="22a62-133">**Создать**: указывает, что нужно создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="22a62-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="22a62-134">**Использовать существующий**: указывает, что нужно выбрать группу ресурсов, связанную с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="22a62-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![Диалоговое окно "Связанные ресурсы"][CR07]

   * <span data-ttu-id="22a62-136">**Учетная запись хранения**: указывает учетную запись хранения, используемую для хранения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="22a62-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="22a62-137">Вы можете выбрать имеющуюся учетную запись хранения или создать ее.</span><span class="sxs-lookup"><span data-stu-id="22a62-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="22a62-138">При выборе элемента **Создать** отображается следующее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="22a62-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![Диалоговое окно "Создание учетной записи хранения"][CR05]

   * <span data-ttu-id="22a62-140">**Виртуальная сеть** и **Подсеть**: указывают виртуальную сеть и подсеть, к которым будет подключена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="22a62-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="22a62-141">Вы можете выбрать имеющуюся сеть и подсеть или создать их.</span><span class="sxs-lookup"><span data-stu-id="22a62-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="22a62-142">При выборе элемента **Создать** отображается следующее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="22a62-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![Диалоговое окно "Создание виртуальной сети"][CR06]

   * <span data-ttu-id="22a62-144">**Общедоступный IP-адрес**: указывает внешний IP-адрес для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="22a62-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="22a62-145">Вы можете создать IP-адрес или выбрать значение **(Нет)**, если у виртуальной машины не будет общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="22a62-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="22a62-146">**Группа безопасности сети**: определяет необязательный брандмауэр для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="22a62-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="22a62-147">Вы можете выбрать имеющийся брандмауэр или задать значение **(Нет)**, чтобы не использовать брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="22a62-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="22a62-148">**Группа доступности**: указывает необязательную группу доступности, в которую может входить виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="22a62-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="22a62-149">Вы можете выбрать имеющуюся группу доступности, создать ее или задать значение **(Нет)**, если виртуальная машина не будет входить в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="22a62-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="22a62-150">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="22a62-150">Click **Finish**.</span></span>  
    <span data-ttu-id="22a62-151">Новая виртуальная машина отобразится в окне средства Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="22a62-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Новая виртуальная машина в представлении Azure Explorer][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="22a62-153">Перезапуск виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="22a62-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="22a62-154">Чтобы перезапустить виртуальную машину с помощью Azure Explorer в IntelliJ, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="22a62-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="22a62-155">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="22a62-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Команда перезапуска виртуальной машины][RE01]

2. <span data-ttu-id="22a62-157">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="22a62-157">In the confirmation window, click **Yes**.</span></span> 

   ![Диалоговое окно подтверждения перезапуска виртуальной машины][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="22a62-159">Завершение работы виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="22a62-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="22a62-160">Чтобы завершить работу виртуальной машины с помощью Azure Explorer в IntelliJ, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="22a62-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="22a62-161">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Завершить работу**.</span><span class="sxs-lookup"><span data-stu-id="22a62-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Команда завершения работы виртуальной машины][SH01]

2. <span data-ttu-id="22a62-163">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="22a62-163">In the confirmation window, click **Yes**.</span></span> 

   ![Диалоговое окно подтверждения завершения работы виртуальной машины][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="22a62-165">Удаление виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="22a62-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="22a62-166">Чтобы удалить виртуальную машину с помощью Azure Explorer в IntelliJ, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="22a62-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="22a62-167">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="22a62-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Команда удаления виртуальной машины][DE01]

2. <span data-ttu-id="22a62-169">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="22a62-169">In the confirmation window, click **Yes**.</span></span> 

   ![Диалоговое окно подтверждения удаления виртуальной машины][DE02]

## <a name="next-steps"></a><span data-ttu-id="22a62-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22a62-171">Next steps</span></span>
<span data-ttu-id="22a62-172">Дополнительные сведения о размерах виртуальных машин Azure и ценах на них см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="22a62-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="22a62-173">Размеры виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="22a62-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="22a62-174">[Размеры виртуальных машин Windows в Azure]</span><span class="sxs-lookup"><span data-stu-id="22a62-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="22a62-175">[Размеры виртуальных машин Linux в Azure]</span><span class="sxs-lookup"><span data-stu-id="22a62-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="22a62-176">Цены на виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="22a62-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="22a62-177">[Цены на виртуальные машины Windows]</span><span class="sxs-lookup"><span data-stu-id="22a62-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="22a62-178">[Цены на виртуальные машины Linux]</span><span class="sxs-lookup"><span data-stu-id="22a62-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="22a62-179">Дополнительные сведения о наборах средств Azure для Java IDE см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="22a62-179">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="22a62-180">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="22a62-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="22a62-181">[Новые возможности набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="22a62-181">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="22a62-182">[Установка набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="22a62-182">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="22a62-183">[Инструкции по входу для набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="22a62-183">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="22a62-184">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]</span><span class="sxs-lookup"><span data-stu-id="22a62-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="22a62-185">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="22a62-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="22a62-186">[Новые возможности набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="22a62-186">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="22a62-187">[Установка набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="22a62-187">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="22a62-188">[Инструкции по входу для набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="22a62-188">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="22a62-189">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="22a62-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="22a62-190">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="22a62-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="22a62-191">[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="22a62-191">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="22a62-192">[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="22a62-192">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="22a62-193">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="22a62-193">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="22a62-194">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="22a62-194">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="22a62-195">[Установка набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="22a62-195">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="22a62-196">[Установка набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="22a62-196">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="22a62-197">[Инструкции по входу для набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="22a62-197">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="22a62-198">[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="22a62-198">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="22a62-199">[Новые возможности набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="22a62-199">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="22a62-200">[Новые возможности набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="22a62-200">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="22a62-201">[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="22a62-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="22a62-202">[средств Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)</span><span class="sxs-lookup"><span data-stu-id="22a62-202">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="22a62-203">[Размеры виртуальных машин Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="22a62-203">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="22a62-204">[Размеры виртуальных машин Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="22a62-204">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="22a62-205">[Цены на виртуальные машины Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="22a62-205">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="22a62-206">[Цены на виртуальные машины Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="22a62-206">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
