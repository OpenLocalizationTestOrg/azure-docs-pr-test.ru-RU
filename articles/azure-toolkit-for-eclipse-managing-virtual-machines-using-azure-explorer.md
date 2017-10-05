---
title: "Управление виртуальными машинами с помощью Azure Explorer для Eclipse | Документация Майкрософт"
description: "Вы можете узнать, как управлять виртуальными машинами Azure с помощью Azure Explorer для Eclipse."
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
ms.openlocfilehash: 9784e8af9c530078afee06f08a23403a44b0762f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="9da48-103">Управление виртуальными машинами с помощью Azure Explorer для Eclipse</span><span class="sxs-lookup"><span data-stu-id="9da48-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="9da48-104">Средство Azure Explorer, входящее в состав набора средств Azure для Eclipse, предоставляет разработчикам на Java удобное решение для управления виртуальными машинами в их учетной записи Azure из интегрированной среды разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9da48-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="9da48-105">Создание виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="9da48-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="9da48-106">Чтобы создать виртуальную машину с помощью Azure Explorer, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9da48-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="9da48-107">Войдите в свою учетную запись Azure, следуя [инструкциям по входу для набора средств Azure для Eclipse].</span><span class="sxs-lookup"><span data-stu-id="9da48-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="9da48-108">В представлении **Azure Explorer** разверните узел **Azure**, щелкните правой кнопкой мыши **Виртуальные машины** и выберите **Создать виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="9da48-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="9da48-109">![Команда "Создать виртуальную машину"][CR01]</span><span class="sxs-lookup"><span data-stu-id="9da48-109">![The Create VM command][CR01]</span></span>  
   <span data-ttu-id="9da48-110">Откроется мастер **создания виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="9da48-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="9da48-111">В диалоговом окне **Выбор подписки** выберите подписку и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9da48-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Диалоговое окно "Выбор подписки"][CR02]

4. <span data-ttu-id="9da48-113">В диалоговом окне **Выбор образа виртуальной машины** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="9da48-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="9da48-114">**Расположение**: указывает расположение для создания виртуальной машины (например, *Западная часть США*).</span><span class="sxs-lookup"><span data-stu-id="9da48-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="9da48-115">**Издатель**: указывает издателя, создавшего образ, который будет использоваться для создания виртуальной машины (например, *Майкрософт*).</span><span class="sxs-lookup"><span data-stu-id="9da48-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="9da48-116">**Предложение**: определяет предложение виртуальной машины выбранного издателя (например, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="9da48-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="9da48-117">**SKU**: указывает нужный номер SKU из выбранного предложения (например, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="9da48-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="9da48-118">**Номер версии**: указывает, какую версию из выбранного номера SKU нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="9da48-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

    ![Диалоговое окно "Выбор образа виртуальной машины"][CR03]

5. <span data-ttu-id="9da48-120">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9da48-120">Click **Next**.</span></span>

6. <span data-ttu-id="9da48-121">В диалоговом окне **Основные параметры виртуальной машины** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="9da48-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="9da48-122">**Имя виртуальной машины**: указывает имя новой виртуальной машины, которое должно начинаться с буквы и содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="9da48-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="9da48-123">**Размер**: указывает количество ядер и объем памяти, выделяемые для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9da48-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="9da48-124">**Имя пользователя**: указывает учетную запись администратора, создаваемую для управления виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="9da48-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="9da48-125">**Пароль** и **Подтверждение**: указывают пароль для учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="9da48-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

    ![Диалоговое окно "Основные параметры виртуальной машины"][CR04]

7. <span data-ttu-id="9da48-127">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9da48-127">Click **Next**.</span></span>

8. <span data-ttu-id="9da48-128">В окне **Создание учетной записи хранения** введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="9da48-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="9da48-129">**Группа ресурсов**: определяет группу ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9da48-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="9da48-130">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="9da48-130">Select one of the following options:</span></span>
      * <span data-ttu-id="9da48-131">**Создать**: определяет, что нужно создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9da48-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="9da48-132">**Использовать существующий**: указывает, что нужно выбрать группу ресурсов, связанную с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="9da48-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

      ![Диалоговое окно "Создание учетной записи хранения"][CR05]

   * <span data-ttu-id="9da48-134">**Учетная запись хранения**: определяет учетную запись хранения, используемую для хранения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9da48-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="9da48-135">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="9da48-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="9da48-136">**Виртуальная сеть** и **Подсеть**: определяют виртуальную сеть и подсеть, к которым будет подключена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="9da48-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="9da48-137">Вы можете выбрать имеющуюся сеть и подсеть или создать их.</span><span class="sxs-lookup"><span data-stu-id="9da48-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="9da48-138">При выборе элемента **Создать** отображается следующее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="9da48-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![Диалоговое окно "Создание виртуальной сети"][CR06]

9. <span data-ttu-id="9da48-140">В диалоговом окне **Связанные ресурсы** введите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="9da48-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="9da48-141">**Общедоступный IP-адрес**: указывает внешний IP-адрес для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9da48-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="9da48-142">Вы можете создать IP-адрес или выбрать значение **(Нет)**, если у виртуальной машины не будет общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="9da48-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="9da48-143">**Группа безопасности сети**: определяет необязательный брандмауэр для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9da48-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="9da48-144">Вы можете выбрать имеющийся брандмауэр или задать значение **(Нет)**, чтобы не использовать брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="9da48-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="9da48-145">**Группа доступности**: определяет необязательную группу доступности, в которую может входить виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="9da48-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="9da48-146">Вы можете выбрать существующую группу доступности, создать ее или задать значение **(Нет)**, если виртуальная машина не входит в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="9da48-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![Диалоговое окно "Связанные ресурсы"][CR07]

9. <span data-ttu-id="9da48-148">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="9da48-148">Click **Finish**.</span></span>  
  <span data-ttu-id="9da48-149">Новая виртуальная машина отобразится в окне средства Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="9da48-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

   ![Новая виртуальная машина][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="9da48-151">Перезапуск виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="9da48-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="9da48-152">Чтобы перезапустить виртуальную машину с помощью Azure Explorer в Eclipse, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9da48-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="9da48-153">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="9da48-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Команда перезапуска виртуальной машины][RE01]

2. <span data-ttu-id="9da48-155">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="9da48-155">In the confirmation window, click **Yes**.</span></span>

   ![Окно подтверждения перезапуска][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="9da48-157">Завершение работы виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="9da48-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="9da48-158">Чтобы завершить работу виртуальной машины с помощью Azure Explorer в Eclipse, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9da48-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="9da48-159">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Завершить работу**.</span><span class="sxs-lookup"><span data-stu-id="9da48-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Команда завершения работы виртуальной машины][SH01]

2. <span data-ttu-id="9da48-161">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="9da48-161">In the confirmation window, click **Yes**.</span></span>

   ![Окно подтверждения завершения работы виртуальной машины][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="9da48-163">Удаление виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="9da48-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="9da48-164">Чтобы удалить виртуальную машину с помощью Azure Explorer в Eclipse, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9da48-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="9da48-165">В представлении **Azure Explorer** щелкните правой кнопкой мыши виртуальную машину и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="9da48-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Команда удаления виртуальной машины][DE01]

2. <span data-ttu-id="9da48-167">В диалоговом окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="9da48-167">In the confirmation window, click **Yes**.</span></span>

   ![Окно подтверждения удаления виртуальной машины][DE02]

## <a name="next-steps"></a><span data-ttu-id="9da48-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9da48-169">Next steps</span></span>
<span data-ttu-id="9da48-170">Дополнительные сведения о размерах виртуальных машин Azure и ценах на них см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="9da48-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="9da48-171">Размеры виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="9da48-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="9da48-172">[Размеры виртуальных машин Windows в Azure]</span><span class="sxs-lookup"><span data-stu-id="9da48-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="9da48-173">[Размеры виртуальных машин Linux в Azure]</span><span class="sxs-lookup"><span data-stu-id="9da48-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="9da48-174">Цены на виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="9da48-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="9da48-175">[Цены на виртуальные машины Windows]</span><span class="sxs-lookup"><span data-stu-id="9da48-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="9da48-176">[Цены на виртуальные машины Linux]</span><span class="sxs-lookup"><span data-stu-id="9da48-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="9da48-177">Дополнительные сведения о наборах средств Azure для Java IDE см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="9da48-177">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="9da48-178">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9da48-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9da48-179">[Новые возможности набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9da48-179">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9da48-180">[Установка набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9da48-180">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9da48-181">[инструкциям по входу для набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9da48-181">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9da48-182">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9da48-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="9da48-183">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9da48-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9da48-184">[Новые возможности набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9da48-184">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9da48-185">[Установка набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9da48-185">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9da48-186">[Инструкции по входу для набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9da48-186">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9da48-187">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9da48-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="9da48-188">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="9da48-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="9da48-189">[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="9da48-189">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="9da48-190">[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="9da48-190">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="9da48-191">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="9da48-191">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="9da48-192">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="9da48-192">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="9da48-193">[Установка набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="9da48-193">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="9da48-194">[Установка набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="9da48-194">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="9da48-195">[инструкциям по входу для набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="9da48-195">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="9da48-196">[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="9da48-196">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="9da48-197">[Новые возможности набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="9da48-197">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="9da48-198">[Новые возможности набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="9da48-198">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="9da48-199">[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="9da48-199">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="9da48-200">[средств Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)</span><span class="sxs-lookup"><span data-stu-id="9da48-200">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="9da48-201">[Размеры виртуальных машин Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="9da48-201">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="9da48-202">[Размеры виртуальных машин Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="9da48-202">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="9da48-203">[Цены на виртуальные машины Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="9da48-203">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="9da48-204">[Цены на виртуальные машины Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="9da48-204">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
