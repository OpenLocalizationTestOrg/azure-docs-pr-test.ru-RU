---
title: "Здравствуйте, aaaManage учетные записи хранения с помощью обозревателя Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как toomanage службе хранилища Azure учетных записей с помощью hello обозреватель Azure для Eclipse."
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
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="3f4d1-103">Управление учетными записями хранилища с помощью hello обозреватель Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f4d1-103">Manage storage accounts by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="3f4d1-104">Hello Explorer Azure, который является частью hello средств Azure для Eclipse, предоставляет разработчикам решения для использования в Java для управления учетными записями хранения в учетную запись Azure с внутри hello Eclipse интегрированной среды разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="3f4d1-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="3f4d1-105">Создание учетной записи хранения в Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f4d1-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="3f4d1-106">toocreate учетной записи хранилища с помощью обозревателя Azure hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="3f4d1-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="3f4d1-107">Войдите в tooyour учетная запись Azure с использованием hello [входа в инструкции для средств Azure для Eclipse hello].</span><span class="sxs-lookup"><span data-stu-id="3f4d1-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="3f4d1-108">В hello **обозреватель Azure** , разверните узел hello **Azure** узел, щелкните правой кнопкой мыши **учетные записи хранения**и нажмите кнопку **создать учетную запись хранилища**.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Команда "Создать учетную запись хранения"][CS01]

3. <span data-ttu-id="3f4d1-110">В hello **создать учетную запись хранилища** диалоговом окне укажите hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="3f4d1-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![Диалоговое окно "Создание учетной записи хранения"][CS02]

   * <span data-ttu-id="3f4d1-112">**Имя**: Указывает имя новой учетной записи хранения hello hello.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="3f4d1-113">**Подписки**: указывает hello подписки Azure, чтобы получить toouse hello новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-113">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="3f4d1-114">**Группа ресурсов**: указывает hello группу ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-114">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="3f4d1-115">Выберите один из следующих вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-115">Select one of hello following options:</span></span>
      * <span data-ttu-id="3f4d1-116">**Создать новое**: Указывает, что toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-116">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="3f4d1-117">**Использовать существующий**: указывает, что вы выберете группу ресурсов, связанную с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="3f4d1-118">**Область**: указывает hello место для создания учетной записи хранения (например, «West US»).</span><span class="sxs-lookup"><span data-stu-id="3f4d1-118">**Region**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="3f4d1-119">**Учетная запись kind**: Определяет тип hello toocreate учетной записи хранилища (например, «больших двоичных объектов хранилища»).</span><span class="sxs-lookup"><span data-stu-id="3f4d1-119">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="3f4d1-120">Дополнительные сведения см. в статье [Об учетных записях хранения Azure].</span><span class="sxs-lookup"><span data-stu-id="3f4d1-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="3f4d1-121">**Производительность**: Указывает, какую учетную запись хранения, предложения toouse hello выбранного издателя (например, «Premium»).</span><span class="sxs-lookup"><span data-stu-id="3f4d1-121">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="3f4d1-122">Дополнительные сведения см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="3f4d1-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="3f4d1-123">**Репликация**: указывает hello репликации для учетной записи хранения hello (например, «избыточное в пределах зоны»).</span><span class="sxs-lookup"><span data-stu-id="3f4d1-123">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="3f4d1-124">Дополнительные сведения см. в статье [Репликация службы хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="3f4d1-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="3f4d1-125">При указании hello предыдущих параметров щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-125">When you have specified all of hello preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="3f4d1-126">Создание контейнера хранилища в Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f4d1-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="3f4d1-127">Контейнер хранилища с помощью обозревателя Azure hello toocreate hello следующие:</span><span class="sxs-lookup"><span data-stu-id="3f4d1-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="3f4d1-128">В hello **обозреватель Azure** просмотра щелкните правой кнопкой мыши учетную запись хранения hello где вы toocreate контейнера и нажмите кнопку **создать контейнер больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-128">In hello **Azure Explorer** view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![Команда "Создать контейнер BLOB-объектов"][CC01]

2. <span data-ttu-id="3f4d1-130">В hello **создать контейнер больших двоичных объектов** диалоговое окно, укажите имя hello для контейнера и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="3f4d1-131">Дополнительные сведения об именовании контейнеров хранилища см. в статье [Naming and Referencing Containers, Blobs, and Metadata] (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них).</span><span class="sxs-lookup"><span data-stu-id="3f4d1-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Диалоговое окно "Создание контейнера BLOB-объектов"][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="3f4d1-133">Удаление контейнера хранилища в Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f4d1-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="3f4d1-134">Контейнер хранилища с помощью обозревателя Azure hello toodelete hello следующие:</span><span class="sxs-lookup"><span data-stu-id="3f4d1-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="3f4d1-135">В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши контейнер хранилища hello и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-135">In hello **Azure Explorer** view, right-click hello storage container, and then click **Delete**.</span></span>

   ![Команда "Удалить контейнер хранилища"][DC01]

2. <span data-ttu-id="3f4d1-137">В окне подтверждения hello, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-137">In hello confirmation window, click **OK**.</span></span>

   ![Окно подтверждения удаления контейнера хранилища][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="3f4d1-139">Удаление учетной записи хранения в Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f4d1-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="3f4d1-140">toodelete учетной записи хранилища с помощью обозревателя Azure hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="3f4d1-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="3f4d1-141">В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши учетную запись хранения hello и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-141">In hello **Azure Explorer** view, right-click hello storage account, and then click **Delete**.</span></span>

   ![Команда "Удалить учетную запись хранения"][DS01]

2. <span data-ttu-id="3f4d1-143">В окне подтверждения hello, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3f4d1-143">In hello confirmation window, click **OK**.</span></span>

   ![Окно подтверждения удаления учетной записи хранения][DS02]

## <a name="next-steps"></a><span data-ttu-id="3f4d1-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3f4d1-145">Next steps</span></span>
<span data-ttu-id="3f4d1-146">Дополнительные сведения об учетных записях хранения Azure размеров и цен, см. следующие ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="3f4d1-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="3f4d1-147">[Введение tooMicrosoft хранилища Azure]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="3f4d1-148">[Об учетных записях хранения Azure]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="3f4d1-149">Размеры учетных записей хранения Azure</span><span class="sxs-lookup"><span data-stu-id="3f4d1-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="3f4d1-150">[Размеры учетных записей хранения Windows в Azure]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="3f4d1-151">[Размеры учетных записей хранения Linux в Azure]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="3f4d1-152">Цены на учетные записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="3f4d1-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="3f4d1-153">[Windows storage-account pricing] (Цены на учетные записи хранения Windows)</span><span class="sxs-lookup"><span data-stu-id="3f4d1-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="3f4d1-154">[Linux storage-account pricing] (Цены на учетные записи хранения Linux)</span><span class="sxs-lookup"><span data-stu-id="3f4d1-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="3f4d1-155">Дополнительные сведения о наборы инструментов Azure для Java интегрированные среды разработки см. следующие ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="3f4d1-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="3f4d1-156">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f4d1-157">[Новые возможности средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f4d1-158">[Установка средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f4d1-159">[входа в инструкции для средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f4d1-160">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="3f4d1-161">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f4d1-162">[Новые возможности средств Azure для IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f4d1-163">[Установка hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f4d1-164">[Вход инструкции для hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f4d1-165">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f4d1-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="3f4d1-166">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="3f4d1-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

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

[Введение tooMicrosoft хранилища Azure]: /azure/storage/storage-introduction
[Об учетных записях хранения Azure]: /azure/storage/storage-create-storage-account
[Репликация службы хранилища Azure]: /azure/storage/storage-redundancy
[Целевые показатели масштабируемости и производительности службы хранилища Azure]: /azure/storage/storage-scalability-targets
[Naming and Referencing Containers, Blobs, and Metadata]: http://go.microsoft.com/fwlink/?LinkId=255555 (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них)

[Размеры учетных записей хранения Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры учетных записей хранения Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/ (Цены на учетные записи хранения Windows)
[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/ (Цены на учетные записи хранения Linux)

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
