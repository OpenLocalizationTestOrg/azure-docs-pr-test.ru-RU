---
title: "Инструкции по входу для набора средств Azure для IntelliJ | Документация Майкрософт"
description: "Сведения о входе в Microsoft Azure с помощью набора средств Azure для IntelliJ."
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
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="02889-103">Инструкции по входу для набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="02889-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="02889-104">Набор средств Azure для IntelliJ предоставляет два метода для входа в систему с помощью учетной записи Azure:</span><span class="sxs-lookup"><span data-stu-id="02889-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="02889-105">**Интерактивный.** Учетные данные Azure необходимо вводить при каждом входе в учетную запись.</span><span class="sxs-lookup"><span data-stu-id="02889-105">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>
  * <span data-ttu-id="02889-106">**Автоматический.** Вы создаете файл учетных данных, который можно использовать для автоматического входа в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="02889-106">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>

<span data-ttu-id="02889-107">В разделах ниже описано использование каждого из методов.</span><span class="sxs-lookup"><span data-stu-id="02889-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="02889-108">Интерактивный вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="02889-108">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="02889-109">Чтобы войти в Azure, вручную введя учетные данные Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="02889-109">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="02889-110">Откройте проект с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="02889-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="02889-111">Выберите **Tools** (Средства), наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign In** (Вход в Azure).</span><span class="sxs-lookup"><span data-stu-id="02889-111">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][I01]

3. <span data-ttu-id="02889-113">В окне **Azure Sign In** (Вход в Azure) выберите **Interactive** (Интерактивный) и щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="02889-113">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Interactive (Интерактивный)][I02]

4. <span data-ttu-id="02889-115">При отображении диалогового окна **Azure Log In** (Вход в Azure) введите учетные данные и щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="02889-115">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Диалоговое окно входа Azure][I03]

5. <span data-ttu-id="02889-117">В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="02889-117">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="02889-119">Выход из учетной записи Azure после интерактивного входа</span><span class="sxs-lookup"><span data-stu-id="02889-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="02889-120">После настройки учетной записи с помощью действий, описанных в предыдущем разделе, вы будете автоматически выходить из своей учетной записи Azure при каждом перезапуске IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="02889-120">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="02889-121">Но если вы хотите выйти из учетной записи Azure, *не перезапуская* IntelliJ IDEA, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="02889-121">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="02889-122">В IntelliJ IDEA в меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign Out** (Выход из Azure).</span><span class="sxs-lookup"><span data-stu-id="02889-122">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Команда Azure Sign Out (Выход из Azure) в IntelliJ][L01]

2. <span data-ttu-id="02889-124">В диалоговом окне подтверждения **выхода из Azure** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="02889-124">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Диалоговое окно подтверждения выхода из Azure][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="02889-126">Автоматический вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="02889-126">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="02889-127">В этом разделе показано, как создать файл учетных данных, содержащий данные субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="02889-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="02889-128">После выполнения этого процесса Eclipse использует файл учетных данных для автоматического входа в Azure при каждом открытии проекта.</span><span class="sxs-lookup"><span data-stu-id="02889-128">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="02889-129">Откройте проект с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="02889-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="02889-130">В меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign In** (Вход в Azure).</span><span class="sxs-lookup"><span data-stu-id="02889-130">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][A01]

3. <span data-ttu-id="02889-132">В диалоговом окне **Azure Sign In** (Вход в Azure) выберите **Automated** (Автоматически) и щелкните **New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="02889-132">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Automated (Автоматически)][A02]

4. <span data-ttu-id="02889-134">В диалоговом окне **входа в Azure** введите учетные данные и щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="02889-134">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Диалоговое окно входа Azure][A03]

5. <span data-ttu-id="02889-136">В диалоговом окне **Create authentication files** (Создание файлов проверки подлинности) выберите нужные подписки, конечный каталог и нажмите кнопку **Start** (Начать).</span><span class="sxs-lookup"><span data-stu-id="02889-136">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Окно Create authentication files (Создание файлов проверки подлинности)][A04]

6. <span data-ttu-id="02889-138">В диалоговом окне **Service Principal Creation Status** (Состояние создания субъекта-службы) после успешного создания файлов нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="02889-138">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Диалоговое окно Service Principal Creation Status (Состояние создания субъекта-службы)][A05]

7. <span data-ttu-id="02889-140">В окне **Azure Sign In** (Вход в Azure) щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="02889-140">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Диалоговое окно входа в Azure][A06]

8. <span data-ttu-id="02889-142">В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="02889-142">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="02889-144">Выход из учетной записи Azure после автоматического входа</span><span class="sxs-lookup"><span data-stu-id="02889-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="02889-145">После настройки учетной записи с помощью действий, описанных в предыдущем разделе, набор средств Azure автоматически входит в учетную запись Azure при каждом перезапуске IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="02889-145">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="02889-146">Чтобы выйти из учетной записи Azure и предотвратить автоматический вход набора средств Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="02889-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="02889-147">В IntelliJ IDEA в меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign Out** (Выход из Azure).</span><span class="sxs-lookup"><span data-stu-id="02889-147">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Команда Azure Sign Out (Выход из Azure) в IntelliJ][L01]

2. <span data-ttu-id="02889-149">В диалоговом окне подтверждения **выхода из Azure** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="02889-149">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Диалоговое окно подтверждения выхода из Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="02889-151">Автоматический вход в учетную запись Azure с помощью имеющегося файла учетных данных</span><span class="sxs-lookup"><span data-stu-id="02889-151">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="02889-152">Если вы выходите из учетной записи Azure во время использования IntelliJ IDEA, вам потребуется использовать созданный файл учетных данных для автоматического входа в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="02889-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="02889-153">Чтобы настроить набор средств Azure для Eclipse на использование имеющегося файла учетных данных, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="02889-153">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="02889-154">Откройте проект с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="02889-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="02889-155">В меню **Tools** (Средства) наведите указатель мыши на пункт **Azure**, а затем щелкните **Azure Sign In** (Вход в Azure).</span><span class="sxs-lookup"><span data-stu-id="02889-155">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][A01]

3. <span data-ttu-id="02889-157">В диалоговом окне **Azure Sign In** (Вход в Azure) выберите **Automated** (Автоматически) и щелкните **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="02889-157">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Automated (Автоматически)][A02]

4. <span data-ttu-id="02889-159">В диалоговом окне **Select Authentication File** (Выбор файла проверки подлинности) выберите созданный ранее файл учетных данных ранее и нажмите кнопку **Select** (Выбрать).</span><span class="sxs-lookup"><span data-stu-id="02889-159">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Диалоговое окно Select Authentication File (Выбор файла проверки подлинности)][A08]

5. <span data-ttu-id="02889-161">В окне **Azure Sign In** (Вход в Azure) щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="02889-161">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным значением Automated (Автоматически)][A06]

6. <span data-ttu-id="02889-163">В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="02889-163">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][A07]

## <a name="next-steps"></a><span data-ttu-id="02889-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02889-165">Next steps</span></span>
<span data-ttu-id="02889-166">Дополнительные сведения о наборах средств Azure для Java IDE см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="02889-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="02889-167">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="02889-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="02889-168">[Новые возможности набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="02889-168">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="02889-169">[Установка набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="02889-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="02889-170">[Инструкции по входу для набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="02889-170">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="02889-171">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]</span><span class="sxs-lookup"><span data-stu-id="02889-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="02889-172">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="02889-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="02889-173">[Новые возможности набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="02889-173">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="02889-174">[Установка набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="02889-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="02889-175">*Инструкции по входу для набора средств Azure для IntelliJ (эта статья)*</span><span class="sxs-lookup"><span data-stu-id="02889-175">*Sign-in instructions for the Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="02889-176">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="02889-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="02889-177">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [инструментов Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="02889-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="02889-178">[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="02889-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="02889-179">[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="02889-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="02889-180">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="02889-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="02889-181">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="02889-181">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="02889-182">[Установка набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="02889-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="02889-183">[Установка набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="02889-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="02889-184">[Инструкции по входу для набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="02889-184">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="02889-185">[Новые возможности набора средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="02889-185">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="02889-186">[Новые возможности набора средств Azure для IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="02889-186">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="02889-187">[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="02889-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="02889-188">[инструментов Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)</span><span class="sxs-lookup"><span data-stu-id="02889-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
