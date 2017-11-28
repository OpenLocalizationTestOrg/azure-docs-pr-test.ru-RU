---
title: "Здравствуйте, aaaManage виртуальных машин с помощью обозревателя Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как toomanage виртуальных машин Azure с помощью hello обозреватель Azure для Eclipse."
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="31c7c-103">Управление виртуальными машинами с помощью hello обозреватель Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="31c7c-103">Manage virtual machines by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="31c7c-104">Hello Explorer Azure, который является частью hello средств Azure для Eclipse, предоставляет разработчикам Java с помощью решения для использования в управлении виртуальными машинами свою учетную запись в Azure из внутри hello Eclipse интегрированной среды разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="31c7c-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="31c7c-105">Создание виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="31c7c-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="31c7c-106">toocreate виртуальной машины с помощью обозревателя Azure hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="31c7c-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="31c7c-107">Войдите в tooyour учетная запись Azure с использованием hello [входа в инструкции для средств Azure для Eclipse hello].</span><span class="sxs-lookup"><span data-stu-id="31c7c-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="31c7c-108">В hello **обозреватель Azure** , разверните узел hello **Azure** узел, щелкните правой кнопкой мыши **виртуальные машины**и нажмите кнопку **создания виртуальной Машины**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="31c7c-109">![Hello команда создания виртуальной Машины][CR01]</span><span class="sxs-lookup"><span data-stu-id="31c7c-109">![hello Create VM command][CR01]</span></span>  
   <span data-ttu-id="31c7c-110">Hello **Создание новой виртуальной машины** откроется мастер.</span><span class="sxs-lookup"><span data-stu-id="31c7c-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="31c7c-111">В hello **выберите подписку** окно, выберите подписку и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Выберите окно подписки Hello][CR02]

4. <span data-ttu-id="31c7c-113">В hello **выберите образ виртуальной машины** окно, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="31c7c-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="31c7c-114">**Расположение**: указывает расположение для создания виртуальной машины (например, *Западная часть США*).</span><span class="sxs-lookup"><span data-stu-id="31c7c-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="31c7c-115">**Издатель**: указывает hello издателя, создавшего образ hello, используемой toocreate вашей виртуальной машины (например, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="31c7c-115">**Publisher**: Specifies hello publisher that created hello image you'll use toocreate your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="31c7c-116">**Предложить**: указывает hello виртуальной машины предложения toouse hello выбранного издателя (например, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="31c7c-116">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="31c7c-117">**SKU**: указывает toouse единица складского учета hello из выбранного предложения hello (например, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="31c7c-117">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="31c7c-118">**Версия #**: Указывает, какую версию выбранного hello SKU toouse.</span><span class="sxs-lookup"><span data-stu-id="31c7c-118">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

    ![Hello выбора образа виртуальной машины окна][CR03]

5. <span data-ttu-id="31c7c-120">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-120">Click **Next**.</span></span>

6. <span data-ttu-id="31c7c-121">В hello **основные параметры виртуальной машины** окно, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="31c7c-121">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="31c7c-122">**Имя виртуальной машины**: Указывает имя hello для новой виртуальной машины, которой должно начинаться с буквы и содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="31c7c-122">**Virtual Machine Name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="31c7c-123">**Размер**: указывает hello количество ядер и памяти tooallocate для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="31c7c-123">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="31c7c-124">**Имя пользователя**: указывает hello toocreate учетной записи администратора для управления виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="31c7c-124">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="31c7c-125">**Пароль** и **Подтверждение**: указывает hello пароль для учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="31c7c-125">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

    ![окно Hello основные параметры виртуальной машины][CR04]

7. <span data-ttu-id="31c7c-127">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-127">Click **Next**.</span></span>

8. <span data-ttu-id="31c7c-128">В hello **создать новую учетную запись хранения** окно, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="31c7c-128">In hello **Create New Storage Account** window, enter hello following information:</span></span>

   * <span data-ttu-id="31c7c-129">**Группа ресурсов**: указывает hello группу ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="31c7c-129">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="31c7c-130">Выберите один из следующих вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="31c7c-130">Select one of hello following options:</span></span>
      * <span data-ttu-id="31c7c-131">**Создать новый**: Указывает, что toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="31c7c-131">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="31c7c-132">**Использовать существующие**: Указывает, что tooselect группы ресурсов, который должен быть связан с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="31c7c-132">**Use existing**: Specifies that you want tooselect a resource group that is already associated with your Azure account.</span></span>

      ![диалоговое окно «Создание новой учетной записи хранилища Hello»][CR05]

   * <span data-ttu-id="31c7c-134">**Учетная запись хранения**: указывает hello toouse учетной записи хранилища для хранения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="31c7c-134">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="31c7c-135">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="31c7c-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="31c7c-136">**Виртуальная сеть** и **подсети**: задает hello виртуальной сети и подсети, в которой будут подключаться к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="31c7c-136">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="31c7c-137">Вы можете выбрать имеющуюся сеть и подсеть или создать их.</span><span class="sxs-lookup"><span data-stu-id="31c7c-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="31c7c-138">При выборе **создать новый**, отображается следующая диалоговое окно приветствия:</span><span class="sxs-lookup"><span data-stu-id="31c7c-138">If you select **Create new**, hello following dialog box is displayed:</span></span>

      ![диалоговое окно создания новой виртуальной сети Hello][CR06]

9. <span data-ttu-id="31c7c-140">В hello **связанные ресурсы** окно, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="31c7c-140">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="31c7c-141">**Общедоступный IP-адрес**: указывает внешний IP-адрес для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="31c7c-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="31c7c-142">Вы можете toocreate новый IP-адрес или, если виртуальная машина не будет иметь общедоступный IP-адрес, можно выбрать **(нет)**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-142">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="31c7c-143">**Группа безопасности сети**: определяет необязательный брандмауэр для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="31c7c-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="31c7c-144">Вы можете выбрать имеющийся брандмауэр или задать значение **(Нет)**, чтобы не использовать брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="31c7c-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="31c7c-145">**Группа доступности**: определяет необязательную группу доступности, в которую может входить виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="31c7c-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="31c7c-146">Можно выбрать существующий набор доступности или создать новую группу доступности или, если виртуальная машина не будет принадлежать tooan набор доступности, можно выбрать **(нет)**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong tooan availability set, you can select **(None)**.</span></span>

   ![окно Hello связанные ресурсы][CR07]

9. <span data-ttu-id="31c7c-148">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="31c7c-148">Click **Finish**.</span></span>  
  <span data-ttu-id="31c7c-149">В окне инструментов обозревателя Azure hello отображается на новую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="31c7c-149">Your new virtual machine is displayed in hello Azure Explorer tool window.</span></span>

   ![Новая виртуальная машина][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="31c7c-151">Перезапуск виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="31c7c-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="31c7c-152">toorestart виртуальной машины с помощью hello обозреватель Azure в Eclipse, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="31c7c-152">toorestart a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="31c7c-153">В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-153">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![команды перезапуска виртуальной машины Hello][RE01]

2. <span data-ttu-id="31c7c-155">В окне подтверждения hello, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-155">In hello confirmation window, click **Yes**.</span></span>

   ![окно подтверждения перезапуска Hello][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="31c7c-157">Завершение работы виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="31c7c-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="31c7c-158">tooshut вниз работающей виртуальной машины с помощью hello обозреватель Azure в Eclipse, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="31c7c-158">tooshut down a running virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="31c7c-159">В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-159">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![Здравствуйте, команда завершения работы виртуальной машины][SH01]

2. <span data-ttu-id="31c7c-161">В окне подтверждения hello, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-161">In hello confirmation window, click **Yes**.</span></span>

   ![окно подтверждения Hello завершение работы виртуальной машины][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="31c7c-163">Удаление виртуальной машины в Eclipse</span><span class="sxs-lookup"><span data-stu-id="31c7c-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="31c7c-164">toodelete виртуальной машины с помощью hello обозреватель Azure в Eclipse, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="31c7c-164">toodelete a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="31c7c-165">В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-165">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![команда удаления виртуальной машины Hello][DE01]

2. <span data-ttu-id="31c7c-167">В окне подтверждения hello, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="31c7c-167">In hello confirmation window, click **Yes**.</span></span>

   ![окно подтверждения удаления виртуальной машины Hello][DE02]

## <a name="next-steps"></a><span data-ttu-id="31c7c-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31c7c-169">Next steps</span></span>
<span data-ttu-id="31c7c-170">Дополнительные сведения об Azure размеры виртуальных машин и ценах см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="31c7c-170">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="31c7c-171">Размеры виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="31c7c-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="31c7c-172">[Размеры виртуальных машин Windows в Azure]</span><span class="sxs-lookup"><span data-stu-id="31c7c-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="31c7c-173">[Размеры виртуальных машин Linux в Azure]</span><span class="sxs-lookup"><span data-stu-id="31c7c-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="31c7c-174">Цены на виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="31c7c-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="31c7c-175">[Цены на виртуальные машины Windows]</span><span class="sxs-lookup"><span data-stu-id="31c7c-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="31c7c-176">[Цены на виртуальные машины Linux]</span><span class="sxs-lookup"><span data-stu-id="31c7c-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="31c7c-177">Дополнительные сведения о hello наборы инструментов Azure для Java интегрированные среды разработки см. следующие ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="31c7c-177">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="31c7c-178">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="31c7c-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="31c7c-179">[Новые возможности средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="31c7c-179">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="31c7c-180">[Установка средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="31c7c-180">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="31c7c-181">[входа в инструкции для средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="31c7c-181">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="31c7c-182">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]</span><span class="sxs-lookup"><span data-stu-id="31c7c-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="31c7c-183">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="31c7c-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="31c7c-184">[Новые возможности средств Azure для IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="31c7c-184">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="31c7c-185">[Установка hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="31c7c-185">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="31c7c-186">[Вход инструкции для hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="31c7c-186">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="31c7c-187">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="31c7c-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="31c7c-188">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="31c7c-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[входа в инструкции для средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Вход инструкции для hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[средств Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

[Размеры виртуальных машин Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры виртуальных машин Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Цены на виртуальные машины Windows]: /pricing/details/virtual-machines/windows/
[Цены на виртуальные машины Linux]: /pricing/details/virtual-machines/linux/

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
