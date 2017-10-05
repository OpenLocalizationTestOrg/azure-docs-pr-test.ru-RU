---
title: "Установка набора средств Azure для IntelliJ | Документация Майкрософт"
description: "Узнайте, как установить набор средств Azure для IntelliJ IDEA."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bf11a8580500f78c4a96a02953f221501eeffe6c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="eea17-103">Установка набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="eea17-103">Installing the Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="eea17-104">В набор средств Azure для IntelliJ входят шаблоны и функциональные возможности для простого создания, разработки, тестирования и развертывания приложений Azure с помощью среды разработки IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="eea17-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the IntelliJ IDEA development environment.</span></span> <span data-ttu-id="eea17-105">Набор средств Azure для IntelliJ — это проект с открытым кодом, исходный код которого доступен по лицензии MIT на сайте проекта в GitHub по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="eea17-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span>

<span data-ttu-id="eea17-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="eea17-106"><https://github.com/microsoft/azure-tools-for-java></span></span>

<span data-ttu-id="eea17-107">Набор средств Azure для IntelliJ можно установить двумя способами — из диалогового окна "Параметры" и их меню "Настройка" на начальном экране; оба способа установки будут продемонстрированы ниже.</span><span class="sxs-lookup"><span data-stu-id="eea17-107">There are two methods of installing the Azure Toolkit for IntelliJ, from the Settings dialog box and from the Configure menu on the start screen; both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="eea17-108">Установка набора средств Azure для IntelliJ из диалогового окна параметров</span><span class="sxs-lookup"><span data-stu-id="eea17-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>
1. <span data-ttu-id="eea17-109">Запустите IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="eea17-109">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="eea17-110">Когда откроется IntelliJ IDEA, щелкните **Файл** и выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="eea17-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
    ![Откройте диалоговое окно параметров IntelliJ IDEA][01a]
3. <span data-ttu-id="eea17-112">В диалоговом окне "Параметры" нажмите кнопку **Подключаемые модули**, а затем **Browse repositories** (Обзор репозиториев).</span><span class="sxs-lookup"><span data-stu-id="eea17-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
    ![Диалоговое окно параметров IntelliJ IDEA][02a]
4. <span data-ttu-id="eea17-114">В диалоговом окне **Обзор репозиториев** введите "Azure" в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="eea17-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="eea17-115">Выделите **Azure Toolkit for IntelliJ** (Набор средств Azure для IntelliJ) и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="eea17-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![Поиск набора средств Azure для IntelliJ][03]
   
    <span data-ttu-id="eea17-117">Ход установки IntelliJ IDEA отобразится в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="eea17-117">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![Ход установки][04]
5. <span data-ttu-id="eea17-119">После завершения установки нажмите кнопку **Перезапуск IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="eea17-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![Перезапуск IntelliJ IDEA][05]
6. <span data-ttu-id="eea17-121">Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно параметров.</span><span class="sxs-lookup"><span data-stu-id="eea17-121">Click **OK** to close the Settings dialog box.</span></span>
   
    ![Закройте диалоговое окно параметров IntelliJ IDEA][06]
7. <span data-ttu-id="eea17-123">При появлении запроса на перезапуск или приостановку IntelliJ IDEA нажмите кнопку **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="eea17-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![Перезапуск IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="eea17-125">Установка набора средств Azure для IntelliJ с начального экрана</span><span class="sxs-lookup"><span data-stu-id="eea17-125">To install the Azure Toolkit for IntelliJ from the start screen</span></span>
1. <span data-ttu-id="eea17-126">Запустите IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="eea17-126">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="eea17-127">Когда откроется начальный экран IntelliJ IDEA, нажмите кнопку **Настройка** и выберите **Подключаемые модули**.</span><span class="sxs-lookup"><span data-stu-id="eea17-127">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
    ![Подключаемые модули IntelliJ IDEA][01b]
3. <span data-ttu-id="eea17-129">В диалоговом окне **Подключаемые модули** нажмите кнопку **Browse repositories** (Обзор репозиториев).</span><span class="sxs-lookup"><span data-stu-id="eea17-129">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
    ![Обзор репозиториев подключаемых модулей IntelliJ IDEA][02b]
4. <span data-ttu-id="eea17-131">В диалоговом окне **Обзор репозиториев** введите "Azure" в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="eea17-131">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="eea17-132">Выделите **Azure Toolkit for IntelliJ** (Набор средств Azure для IntelliJ) и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="eea17-132">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![Поиск набора средств Azure для IntelliJ][03]
   
    <span data-ttu-id="eea17-134">Ход установки IntelliJ IDEA отобразится в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="eea17-134">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![Ход установки][04]
5. <span data-ttu-id="eea17-136">После завершения установки нажмите кнопку **Перезапуск IntelliJ IDEA**.</span><span class="sxs-lookup"><span data-stu-id="eea17-136">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![Перезапуск IntelliJ IDEA][05]
6. <span data-ttu-id="eea17-138">При появлении запроса на перезапуск или приостановку IntelliJ IDEA нажмите кнопку **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="eea17-138">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![Перезапуск IntelliJ IDEA][07]

## <a name="see-also"></a><span data-ttu-id="eea17-140">См. также</span><span class="sxs-lookup"><span data-stu-id="eea17-140">See Also</span></span>
<span data-ttu-id="eea17-141">Дополнительные сведения о наборах средств Azure для Java IDE см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="eea17-141">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="eea17-142">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eea17-142">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="eea17-143">[Новые возможности набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eea17-143">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="eea17-144">[Установка набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eea17-144">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="eea17-145">[Инструкции по входу для набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eea17-145">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="eea17-146">[Создание веб-приложения Hello World для Azure в Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eea17-146">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="eea17-147">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="eea17-147">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="eea17-148">[Новые возможности набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="eea17-148">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="eea17-149">*Установка набора средств Azure для IntelliJ (в этой статье)*</span><span class="sxs-lookup"><span data-stu-id="eea17-149">*Installing the Azure Toolkit for IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="eea17-150">[Инструкции по входу для набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="eea17-150">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="eea17-151">[Создание веб-приложения Hello World для Azure в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="eea17-151">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="eea17-152">Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure].</span><span class="sxs-lookup"><span data-stu-id="eea17-152">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="eea17-153">[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="eea17-153">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="eea17-154">[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="eea17-154">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="eea17-155">[Создание веб-приложения Hello World для Azure в Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="eea17-155">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="eea17-156">[Создание веб-приложения Hello World для Azure в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="eea17-156">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="eea17-157">[Установка набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="eea17-157">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
<span data-ttu-id="eea17-158">[Инструкции по входу для набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="eea17-158">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="eea17-159">[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="eea17-159">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="eea17-160">[Новые возможности набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="eea17-160">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="eea17-161">[Новые возможности набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="eea17-161">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="eea17-162">[Центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="eea17-162">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01a]: ./media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: ./media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: ./media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: ./media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: ./media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: ./media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: ./media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: ./media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: ./media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
