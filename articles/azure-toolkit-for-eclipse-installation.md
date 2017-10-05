---
title: "Установка набора средств Azure для Eclipse | Документация Майкрософт"
description: "Узнайте, как установить набор средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="78163-103">Установка набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="78163-103">Installing the Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="78163-104">В набор средств Azure для Eclipse входят шаблоны и функциональные возможности для простого создания, разработки, тестирования и развертывания приложений Azure с помощью среды разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="78163-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="78163-105">Набор средств Azure для Eclipse является проектом с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="78163-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="78163-106">Исходный код доступен по лицензии MIT по адресу: <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="78163-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="78163-107">Ниже приведен процесс установки набора средств Azure для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="78163-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="78163-108">Установка набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="78163-108">To install the Azure Toolkit for Eclipse</span></span>
1. <span data-ttu-id="78163-109">Запустите Eclipse.</span><span class="sxs-lookup"><span data-stu-id="78163-109">Start Eclipse.</span></span>
2. <span data-ttu-id="78163-110">Щелкните меню **Help** (Справка) и выберите пункт **Install New Software** (Установить новое программное обеспечение), как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="78163-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
    ![Установка набора средств Azure для Eclipse][01]
3. <span data-ttu-id="78163-112">В диалоговом окне **Available Software** (Доступное программное обеспечение) в текстовом поле **Work with** (Работа с) введите `http://dl.microsoft.com/eclipse` и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="78163-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse` followed by the **Enter** key.</span></span>
4. <span data-ttu-id="78163-113">В области **Name** (Имя) установите флажок **Azure Toolkit for Eclipse** (Набор средств Azure для Eclipse) и снимите флажок **Contact all update sites during install to find required software** (Проверить все сайты обновления во время установки для поиска требуемого ПО).</span><span class="sxs-lookup"><span data-stu-id="78163-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="78163-114">Экран должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="78163-114">Your screen should appear similar to the following:</span></span>
   
    ![Установка набора средств Azure для Eclipse][02]
5. <span data-ttu-id="78163-116">Если вы развернете узел **Azure Toolkit for Eclipse**(Набор средств Azure для Eclipse), то увидите следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="78163-116">If you expand the **Azure Toolkit for Eclipse**, you will see the following items:</span></span>
   
   * <span data-ttu-id="78163-117">**Application Insights Plugin for Java**(Подключаемый модуль Application Insights для Java) — этот компонент позволяет использовать службы регистрации и анализа телеметрии Azure для приложений и экземпляров серверов.</span><span class="sxs-lookup"><span data-stu-id="78163-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="78163-118">**Фильтр служб контроля доcтупа Azure**— этот компонент обеспечивает поддержку проверки подлинности пользователей приложения с помощью Azure ACS, используя сценарии единого входа и перемещая логику удостоверений из приложения.</span><span class="sxs-lookup"><span data-stu-id="78163-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="78163-119">**Общий подключаемый модуль Azure**— этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.</span><span class="sxs-lookup"><span data-stu-id="78163-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="78163-120">**Обозреватель Azure для Eclipse**— этот компонент предоставляет функциональные возможности, необходимые другим компонентам набора средств.</span><span class="sxs-lookup"><span data-stu-id="78163-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="78163-121">**Подключаемый модуль Azure для Eclipse с Java**— этот компонент обеспечивает поддержку проектов, помогающих собирать, тестировать и развертывать приложения Java для облака Microsoft Azure в Eclipse и с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="78163-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="78163-122">**Подключаемый модуль веб- приложений Azure с Java**— этот компонент обеспечивает поддержку развертывания веб-приложений Java в контейнерах веб-приложений Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="78163-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="78163-123">**Драйвер Microsoft JDBC 4.2 для SQL Server**— этот компонент предоставляет API JDBC для SQL Server и Базу данных SQL Microsoft Azure для платформы Java Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="78163-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="78163-124">**Package for Apache Qpid Client Libraries for JMS**(Пакет для клиентских библиотек Apache Qpid для JMS) — этот компонент предоставляет клиентские компоненты JMS из проекта Apache Qpid, чтобы ваше приложение могло использовать обмен сообщениями на основе протокола AMQP в Azure.</span><span class="sxs-lookup"><span data-stu-id="78163-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="78163-125">**Пакет для библиотек Microsoft Azure для Java** — этот компонент предоставляет API для доступа к службам Microsoft Azure, таким как хранилище, служебная шина, среда выполнения службы и т. д.</span><span class="sxs-lookup"><span data-stu-id="78163-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>
6. <span data-ttu-id="78163-126">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="78163-126">Click **Next**.</span></span> <span data-ttu-id="78163-127">(Если при установке набора средств возникают необычные задержки, убедитесь, что снят флажок **Contact all update sites during install to find required software** [Проверить все сайты обновления во время установки для поиска требуемого ПО].)</span><span class="sxs-lookup"><span data-stu-id="78163-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>
7. <span data-ttu-id="78163-128">В диалоговом окне **Install Details** (Сведения об установке) нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="78163-128">In the **Install Details** dialog, click **Next**.</span></span>
   
    ![Просмотр сведений об установке][03]
8. <span data-ttu-id="78163-130">В диалоговом окне **Review Licenses** (Просмотр лицензий) ознакомьтесь с условиями лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="78163-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="78163-131">Если вы принимаете условия лицензионных соглашений, установите переключатель **I accept the terms of the license agreements** (Я принимаю условия лицензионных соглашений), а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="78163-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="78163-132">(В следующих действиях предполагается, что вы принимаете условия лицензионных соглашений.</span><span class="sxs-lookup"><span data-stu-id="78163-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="78163-133">Если вы не принимаете эти условия, завершите процесс установки.)</span><span class="sxs-lookup"><span data-stu-id="78163-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
    ![Review Licenses][04]
   
    <span data-ttu-id="78163-135">Eclipse скачает и установит необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="78163-135">Eclipse will download and install the requisite packages.</span></span>
   
    ![Ход установки][05]
9. <span data-ttu-id="78163-137">Если отображается запрос на перезапуск Eclipse для завершения установки, нажмите кнопку **Yes**(Да).</span><span class="sxs-lookup"><span data-stu-id="78163-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
    ![Запрос перезапуска][06]

## <a name="see-also"></a><span data-ttu-id="78163-139">См. также</span><span class="sxs-lookup"><span data-stu-id="78163-139">See Also</span></span>
<span data-ttu-id="78163-140">Дополнительные сведения о наборах средств Azure для Java IDE см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="78163-140">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="78163-141">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="78163-141">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="78163-142">[Новые возможности набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="78163-142">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="78163-143">*Установка набора средств Azure для Eclipse (в этой статье)*</span><span class="sxs-lookup"><span data-stu-id="78163-143">*Installing the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="78163-144">[Инструкции по входу для набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="78163-144">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="78163-145">[Создание веб-приложения Hello World для Azure в Eclipse]</span><span class="sxs-lookup"><span data-stu-id="78163-145">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="78163-146">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="78163-146">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="78163-147">[Новые возможности набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="78163-147">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="78163-148">[Установка набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="78163-148">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="78163-149">[Инструкции по входу для набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="78163-149">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="78163-150">[Создание веб-приложения Hello World для Azure в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="78163-150">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="78163-151">Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure].</span><span class="sxs-lookup"><span data-stu-id="78163-151">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="78163-152">[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="78163-152">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="78163-153">[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="78163-153">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="78163-154">[Создание веб-приложения Hello World для Azure в Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="78163-154">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="78163-155">[Создание веб-приложения Hello World для Azure в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="78163-155">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
<span data-ttu-id="78163-156">[Установка набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="78163-156">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="78163-157">[Инструкции по входу для набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="78163-157">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="78163-158">[Инструкции по входу для набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="78163-158">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="78163-159">[Новые возможности набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="78163-159">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="78163-160">[Новые возможности набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="78163-160">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="78163-161">[Центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="78163-161">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
