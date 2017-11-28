---
title: "aaaManage виртуальных машин с помощью hello обозреватель Azure для IntelliJ | Документы Microsoft"
description: "Узнайте, как toomanage виртуальных машин Azure с помощью hello обозреватель Azure для IntelliJ."
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
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="d53ba-103">Управление виртуальными машинами с помощью hello обозреватель Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d53ba-103">Manage virtual machines by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="d53ba-104">Hello Explorer Azure, который является частью набора средств Azure для IntelliJ hello, предоставляет разработчикам Java с помощью решения для использования в управлении виртуальными машинами свою учетную запись в Azure из внутри hello IntelliJ интегрированной среды разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="d53ba-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="d53ba-105">Создание виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d53ba-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="d53ba-106">toocreate виртуальной машины с помощью обозревателя Azure hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d53ba-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span> 

1. <span data-ttu-id="d53ba-107">Войдите в tooyour учетная запись Azure с помощью действия hello в hello [входа в инструкции для hello Azure Toolkit для IntelliJ] статьи.</span><span class="sxs-lookup"><span data-stu-id="d53ba-107">Sign in tooyour Azure account by using hello steps in hello [Sign-in instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="d53ba-108">В hello **обозреватель Azure** , разверните узел hello **Azure** узел, щелкните правой кнопкой мыши **виртуальные машины**и нажмите кнопку **создания виртуальной Машины**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="d53ba-109">![Hello команда создания виртуальной Машины][CR01]</span><span class="sxs-lookup"><span data-stu-id="d53ba-109">![hello Create VM command][CR01]</span></span>  
    <span data-ttu-id="d53ba-110">Hello **Создание новой виртуальной машины** откроется мастер.</span><span class="sxs-lookup"><span data-stu-id="d53ba-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="d53ba-111">В hello **выберите подписку** окно, выберите подписку и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Выберите окно подписки Hello][CR02]

4. <span data-ttu-id="d53ba-113">В hello **выберите образ виртуальной машины** окно, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="d53ba-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="d53ba-114">**Расположение**: указывает расположение для создания виртуальной машины (например, *Западная часть США*).</span><span class="sxs-lookup"><span data-stu-id="d53ba-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="d53ba-115">**Recommended Image** (Рекомендуемый образ): указывает, что вы выберете образ из сокращенного списка часто используемых образов.</span><span class="sxs-lookup"><span data-stu-id="d53ba-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="d53ba-116">**Пользовательский образ**: Указывает, будет выбрать пользовательский образ, предоставляя hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="d53ba-116">**Custom image**: Specifies that you will choose a custom image by providing hello following information:</span></span>

      * <span data-ttu-id="d53ba-117">**Издатель**: указывает издателю hello hello образа, который будет использоваться для виртуальной машины (например, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="d53ba-117">**Publisher**: Specifies hello publisher that created hello image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="d53ba-118">**Предложить**: указывает hello виртуальной машины предложения toouse hello выбранного издателя (например, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="d53ba-118">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="d53ba-119">**SKU**: указывает toouse единица складского учета hello из выбранного предложения hello (например, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="d53ba-119">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="d53ba-120">**Версия #**: Указывает, какую версию выбранного hello SKU toouse.</span><span class="sxs-lookup"><span data-stu-id="d53ba-120">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

   ![Hello выбора образа виртуальной машины окна][CR03]

5. <span data-ttu-id="d53ba-122">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-122">Click **Next**.</span></span> 

6. <span data-ttu-id="d53ba-123">В hello **основные параметры виртуальной машины** окно, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="d53ba-123">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="d53ba-124">**Имя виртуальной машины**: Указывает имя hello для новой виртуальной машины, которой должно начинаться с буквы и содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="d53ba-124">**Virtual machine name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="d53ba-125">**Размер**: указывает hello количество ядер и памяти tooallocate для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d53ba-125">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="d53ba-126">**Имя пользователя**: указывает hello toocreate учетной записи администратора для управления виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d53ba-126">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="d53ba-127">**Пароль** и **Подтверждение**: указывает hello пароль для учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="d53ba-127">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

   ![окно Hello основные параметры виртуальной машины][CR04]

7. <span data-ttu-id="d53ba-129">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-129">Click **Next**.</span></span> 

8. <span data-ttu-id="d53ba-130">В hello **связанные ресурсы** окно, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="d53ba-130">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="d53ba-131">**Группа ресурсов**: указывает hello группу ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d53ba-131">**Resource group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="d53ba-132">Выберите один из следующих вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="d53ba-132">Select one of hello following options:</span></span>
      * <span data-ttu-id="d53ba-133">**Создать новый**: Указывает, что toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d53ba-133">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="d53ba-134">**Использовать существующие**: Указывает, что tooselect из списка групп ресурсов, которые связаны с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="d53ba-134">**Use existing**: Specifies that you want tooselect from a list of resource groups that are associated with your Azure account.</span></span>

       ![окно Hello связанные ресурсы][CR07]

   * <span data-ttu-id="d53ba-136">**Учетная запись хранения**: указывает hello toouse учетной записи хранилища для хранения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d53ba-136">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="d53ba-137">Вы можете выбрать имеющуюся учетную запись хранения или создать ее.</span><span class="sxs-lookup"><span data-stu-id="d53ba-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="d53ba-138">При выборе **создать новый**, появится следующая диалоговое окно приветствия:</span><span class="sxs-lookup"><span data-stu-id="d53ba-138">If you choose **Create New**, hello following dialog box appears:</span></span>

      ![Создание учетной записи хранилища Hello-диалоговое окно][CR05]

   * <span data-ttu-id="d53ba-140">**Виртуальная сеть** и **подсети**: задает hello виртуальной сети и подсети, в которой будут подключаться к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d53ba-140">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="d53ba-141">Вы можете выбрать имеющуюся сеть и подсеть или создать их.</span><span class="sxs-lookup"><span data-stu-id="d53ba-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="d53ba-142">При выборе **создать новый**, появится следующая диалоговое окно приветствия:</span><span class="sxs-lookup"><span data-stu-id="d53ba-142">If you select **Create new**, hello following dialog box appears:</span></span>

      ![Создание виртуальной сети Hello-диалоговое окно][CR06]

   * <span data-ttu-id="d53ba-144">**Общедоступный IP-адрес**: указывает внешний IP-адрес для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d53ba-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="d53ba-145">Вы можете toocreate новый IP-адрес или, если виртуальная машина не будет иметь общедоступный IP-адрес, можно выбрать **(нет)**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-145">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="d53ba-146">**Группа безопасности сети**: определяет необязательный брандмауэр для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d53ba-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="d53ba-147">Вы можете выбрать имеющийся брандмауэр или задать значение **(Нет)**, чтобы не использовать брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="d53ba-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="d53ba-148">**Группа доступности**: определяет необязательную группу доступности, в которую может входить виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="d53ba-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="d53ba-149">Можно выбрать существующий набор доступности, создать новую группу доступности или, если виртуальная машина не будет принадлежать tooan набора доступности, выберите **(нет)**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong tooan availability set, select **(None)**.</span></span>

9. <span data-ttu-id="d53ba-150">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="d53ba-150">Click **Finish**.</span></span>  
    <span data-ttu-id="d53ba-151">В окне инструментов обозревателя Azure hello появляется на новую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d53ba-151">Your new virtual machine appears in hello Azure Explorer tool window.</span></span> 

   ![Новая виртуальная машина в Azure обозревателя hello][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="d53ba-153">Перезапуск виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d53ba-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="d53ba-154">toorestart виртуальной машины с помощью обозревателя Azure hello в IntelliJ, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d53ba-154">toorestart a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="d53ba-155">В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-155">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![команды перезапуска виртуальной машины Hello][RE01]

2. <span data-ttu-id="d53ba-157">В окне подтверждения hello, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-157">In hello confirmation window, click **Yes**.</span></span> 

   ![Hello перезагрузите окно подтверждения виртуальной машины][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="d53ba-159">Завершение работы виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d53ba-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="d53ba-160">tooshut вниз работающей виртуальной машины с помощью обозревателя Azure hello в IntelliJ, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d53ba-160">tooshut down a running virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="d53ba-161">В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-161">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![Здравствуйте, команда завершения работы виртуальной машины][SH01]

2. <span data-ttu-id="d53ba-163">В окне подтверждения hello, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-163">In hello confirmation window, click **Yes**.</span></span> 

   ![Завершите работу виртуальной машины окно подтверждения Hello][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="d53ba-165">Удаление виртуальной машины в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d53ba-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="d53ba-166">toodelete виртуальной машины с помощью обозревателя Azure hello в IntelliJ, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d53ba-166">toodelete a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="d53ba-167">В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-167">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![команда удаления виртуальной машины Hello][DE01]

2. <span data-ttu-id="d53ba-169">В окне подтверждения hello, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="d53ba-169">In hello confirmation window, click **Yes**.</span></span> 

   ![Hello удалить окно подтверждения виртуальной машины][DE02]

## <a name="next-steps"></a><span data-ttu-id="d53ba-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d53ba-171">Next steps</span></span>
<span data-ttu-id="d53ba-172">Дополнительные сведения об Azure размеры виртуальных машин и ценах см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="d53ba-172">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="d53ba-173">Размеры виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="d53ba-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="d53ba-174">[Размеры виртуальных машин Windows в Azure]</span><span class="sxs-lookup"><span data-stu-id="d53ba-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="d53ba-175">[Размеры виртуальных машин Linux в Azure]</span><span class="sxs-lookup"><span data-stu-id="d53ba-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="d53ba-176">Цены на виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="d53ba-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="d53ba-177">[Цены на виртуальные машины Windows]</span><span class="sxs-lookup"><span data-stu-id="d53ba-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="d53ba-178">[Цены на виртуальные машины Linux]</span><span class="sxs-lookup"><span data-stu-id="d53ba-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="d53ba-179">Дополнительные сведения о hello наборы инструментов Azure для Java интегрированные среды разработки см. следующие ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="d53ba-179">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="d53ba-180">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d53ba-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d53ba-181">[Новые возможности средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="d53ba-181">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d53ba-182">[Установка средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="d53ba-182">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d53ba-183">[Инструкции вход для hello средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d53ba-183">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d53ba-184">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d53ba-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="d53ba-185">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d53ba-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d53ba-186">[Новые возможности средств Azure для IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="d53ba-186">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d53ba-187">[Установка hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d53ba-187">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d53ba-188">[входа в инструкции для hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d53ba-188">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d53ba-189">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d53ba-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="d53ba-190">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d53ba-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Инструкции вход для hello средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[входа в инструкции для hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[средств Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

[Размеры виртуальных машин Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры виртуальных машин Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Цены на виртуальные машины Windows]: /pricing/details/virtual-machines/windows/
[Цены на виртуальные машины Linux]: /pricing/details/virtual-machines/linux/


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
