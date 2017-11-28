---
title: "aaaSign в инструкции для средств Azure для Eclipse hello | Документы Microsoft"
description: "Узнайте, как toosign в Microsoft Azure с помощью hello средств Azure для Eclipse."
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="d2c55-103">Azure входа в инструкции для hello средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="d2c55-103">Azure Sign In Instructions for hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="d2c55-104">Hello средств Azure для Eclipse предоставляет два метода для входа в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="d2c55-104">hello Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="d2c55-105">**Интерактивно** — при использовании этого метода потребуется вводить учетные данные Azure при каждом входе в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c55-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="d2c55-106">**Автоматическое** — при использовании этого метода будет создан файл учетных данных, который содержит данные участника службы, после чего можно использовать файл tooautomatically hello учетные данные входа в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c55-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use hello credentials file tooautomatically sign into your Azure account.</span></span>

<span data-ttu-id="d2c55-107">Hello в следующих разделах hello будет описано, как toouse каждого метода.</span><span class="sxs-lookup"><span data-stu-id="d2c55-107">hello steps in hello following sections will describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="d2c55-108">Интерактивный вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="d2c55-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="d2c55-109">Hello ниже будет показано, как toosign в Azure, вручную введя свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c55-109">hello following steps will illustrate how toosign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="d2c55-110">Откройте проект с помощью Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d2c55-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="d2c55-111">Выберите **Сервис**, **Azure** и затем **Войти**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Меню Eclipse для входа в систему Azure][I01]

1. <span data-ttu-id="d2c55-113">Здравствуйте, когда **входа в Azure** диалоговое окно, выберите **Interactive**и нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-113">When hello **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Диалоговое окно входа][I02]

1. <span data-ttu-id="d2c55-115">Здравствуйте, когда **журнала в Azure** диалоговое окно, введите свои учетные данные Azure и нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-115">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Диалоговое окно входа в Azure][I03]

1. <span data-ttu-id="d2c55-117">Здравствуйте, когда **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-117">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="d2c55-119">Выход из учетной записи Azure после интерактивного входа</span><span class="sxs-lookup"><span data-stu-id="d2c55-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="d2c55-120">После настройки hello действия в предыдущем разделе hello, будет выполнен автоматический выход из учетной записи Azure каждый раз, перезапустите Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d2c55-120">After you have configured hello steps in hello previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="d2c55-121">Тем не менее toosign из учетной записи Azure без перезапуска Eclipse, используйте следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="d2c55-121">However, if you want toosign out of your Azure account without restarting Eclipse, use hello following steps.</span></span>

1. <span data-ttu-id="d2c55-122">В Eclipse выберите **Сервис**, **Azure** и затем **Выйти**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Меню Eclipse для выхода из системы Azure][L01]

1. <span data-ttu-id="d2c55-124">Здравствуйте, когда **выйти Azure** диалоговое окно, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-124">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Диалоговое окно выхода][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a><span data-ttu-id="d2c55-126">Автоматически войти в учетную запись Azure и создании учетных данных файла toouse в hello будущих</span><span class="sxs-lookup"><span data-stu-id="d2c55-126">Signing into your Azure account automatically and creating a credentials file toouse in hello future</span></span>

<span data-ttu-id="d2c55-127">Hello ниже поможет вам выполнить создание файл учетных данных, который содержит данные участника службы.</span><span class="sxs-lookup"><span data-stu-id="d2c55-127">hello following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="d2c55-128">После выполнения этих действий, Eclipse будет автоматически использовать hello учетные данные файла tooautomatically входа вы в Azure каждый раз при откройте свой проект.</span><span class="sxs-lookup"><span data-stu-id="d2c55-128">Once you have completed these steps, Eclipse will automatically use hello credentials file tooautomatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="d2c55-129">Откройте проект с помощью Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d2c55-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="d2c55-130">Выберите **Сервис**, **Azure** и затем **Войти**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Меню Eclipse для входа в систему Azure][A01]

1. <span data-ttu-id="d2c55-132">Здравствуйте, когда **входа в Azure** диалоговое окно, выберите **автоматизирован**и нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-132">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Диалоговое окно входа][A02]

1. <span data-ttu-id="d2c55-134">Здравствуйте, когда **журнала в Azure** диалоговое окно, введите свои учетные данные Azure и нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-134">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Диалоговое окно входа в Azure][A03]

1. <span data-ttu-id="d2c55-136">Здравствуйте, когда **создать файлы для проверки подлинности** диалоговое окно, выберите hello подписки требуется toouse, выберите каталог назначения и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-136">When hello **Create authentication files** dialog box appears, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Диалоговое окно входа в Azure][A04]

1. <span data-ttu-id="d2c55-138">Hello **Creatation состояния субъекта-службы** отображается диалоговое окно, а после успешного создания файлов, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-138">hello **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Диалоговое окно состояния создания субъекта-службы][A05]

1. <span data-ttu-id="d2c55-140">Здравствуйте, когда **входа в Azure** диалоговое окно, нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-140">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Диалоговое окно входа в Azure][A06]

1. <span data-ttu-id="d2c55-142">Здравствуйте, когда **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-142">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="d2c55-144">Выход из учетной записи Azure после автоматического входа</span><span class="sxs-lookup"><span data-stu-id="d2c55-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="d2c55-145">После настройки hello действия в предыдущем разделе hello hello набора средств Azure будет автоматически выполняться вход в учетную запись Azure каждый раз, перезапустите Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d2c55-145">After you have configured hello steps in hello previous section, hello Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="d2c55-146">Тем не менее toosign со стороны вашей учетной записью Azure, а также запретить вход автоматически, hello используйте следующие шаги hello набора средств Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c55-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, use hello following steps.</span></span>

1. <span data-ttu-id="d2c55-147">В Eclipse выберите **Сервис**, **Azure** и затем **Выйти**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Меню Eclipse для выхода из системы Azure][L01]

1. <span data-ttu-id="d2c55-149">Здравствуйте, когда **выйти Azure** диалоговое окно, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-149">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Диалоговое окно выхода][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="d2c55-151">Автоматический вход в учетную запись Azure с помощью созданного файла учетных данных</span><span class="sxs-lookup"><span data-stu-id="d2c55-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="d2c55-152">Если при использовании Eclipse, следует выйти из Azure, необходимо будет tooreconfigure hello набора средств Azure для Eclipse toouse файл учетных данных, в которой создана перед регистрацией автоматически в ваша Azure учетная запись.</span><span class="sxs-lookup"><span data-stu-id="d2c55-152">If you sign out of Azure when you are using Eclipse, you will need tooreconfigure hello Azure Toolkit for Eclipse toouse a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="d2c55-153">Hello следующее поможет настройка набора средств Azure toouse hello существующий файл учетных данных.</span><span class="sxs-lookup"><span data-stu-id="d2c55-153">hello following steps will walk you through configuring hello Azure Toolkit toouse an existing credentials file.</span></span>

1. <span data-ttu-id="d2c55-154">Откройте проект с помощью Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d2c55-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="d2c55-155">Выберите **Сервис**, **Azure** и затем **Войти**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Меню Eclipse для входа в систему Azure][A01]

1. <span data-ttu-id="d2c55-157">Здравствуйте, когда **входа в Azure** диалоговое окно, выберите **автоматизирован**и нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-157">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Диалоговое окно входа][A02]

1. <span data-ttu-id="d2c55-159">Здравствуйте, когда **выбрать файл с проверкой подлинности** диалоговое окно, выберите файл учетных данных, которая была создана ранее и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-159">When hello **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Диалоговое окно входа][A08]

1. <span data-ttu-id="d2c55-161">Здравствуйте, когда **входа в Azure** диалоговое окно, нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-161">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Диалоговое окно входа в Azure][A06]

1. <span data-ttu-id="d2c55-163">Здравствуйте, когда **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2c55-163">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][A07]

## <a name="see-also"></a><span data-ttu-id="d2c55-165">См. также</span><span class="sxs-lookup"><span data-stu-id="d2c55-165">See Also</span></span>
<span data-ttu-id="d2c55-166">Дополнительные сведения о hello наборы инструментов Azure для Java интегрированными средами разработки. в разделе hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="d2c55-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="d2c55-167">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d2c55-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d2c55-168">[Новые возможности средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="d2c55-168">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d2c55-169">[Установка средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="d2c55-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d2c55-170">*Вход в инструкции для hello средств Azure для Eclipse (Эта статья)*</span><span class="sxs-lookup"><span data-stu-id="d2c55-170">*Sign In Instructions for hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="d2c55-171">[Создание веб-приложения Hello World для Azure в Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d2c55-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="d2c55-172">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d2c55-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d2c55-173">[Новые возможности средств Azure для IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="d2c55-173">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d2c55-174">[Установка hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d2c55-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d2c55-175">[Вход в инструкции для hello средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d2c55-175">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d2c55-176">[Создание веб-приложения Hello World для Azure в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d2c55-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="d2c55-177">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d2c55-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Hello World для Azure в Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Hello World для Azure в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Вход в инструкции для hello средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
