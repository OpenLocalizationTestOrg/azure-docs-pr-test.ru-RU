---
title: "aaaSign в инструкции для hello Azure Toolkit для IntelliJ | Документы Microsoft"
description: "Узнайте, как toosign в tooMicrosoft Azure с помощью hello Azure Toolkit для IntelliJ."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="8dac5-103">Вход инструкции для hello Azure Toolkit для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8dac5-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="8dac5-104">набор средств Azure для IntelliJ Hello предоставляет два метода для входа в учетную запись Azure tooyour:</span><span class="sxs-lookup"><span data-stu-id="8dac5-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="8dac5-105">**Интерактивный**: Введите учетные данные Azure при каждом входе в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8dac5-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="8dac5-106">**Автоматическое**: Создание файла учетных данных, можно использовать tooautomatically входа в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8dac5-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="8dac5-107">Hello ниже описано, как toouse каждого метода.</span><span class="sxs-lookup"><span data-stu-id="8dac5-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="8dac5-108">Интерактивного входа в учетную запись Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="8dac5-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="8dac5-109">toosign в tooAzure, вручную введя свои учетные данные Azure hello следующие:</span><span class="sxs-lookup"><span data-stu-id="8dac5-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="8dac5-110">Откройте проект с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="8dac5-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="8dac5-111">Нажмите кнопку **средства**, слишком точки**Azure**, а затем нажмите кнопку **входа в Azure**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Hello команда IntelliJ входа в Azure][I01]

3. <span data-ttu-id="8dac5-113">В hello **входа в Azure** выберите **Interactive**, а затем нажмите кнопку **входа в**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Hello входа в Azure окно с выбранной Interactive][I02]

4. <span data-ttu-id="8dac5-115">В hello **журнала в Azure** диалоговое окно, введите свои учетные данные Azure и нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Hello Azure входа диалоговое окно][I03]

5. <span data-ttu-id="8dac5-117">В hello **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![диалоговое окно Выбор подписки Hello][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="8dac5-119">Выход из учетной записи Azure после интерактивного входа</span><span class="sxs-lookup"><span data-stu-id="8dac5-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="8dac5-120">После настройки учетной записи с помощью hello в предыдущих шагах, будет автоматически выполнен из учетной записи Azure каждый раз при перезапуске IntelliJ ИДЕЯ.</span><span class="sxs-lookup"><span data-stu-id="8dac5-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="8dac5-121">Тем не менее если вам нужны toosign учетной записью Azure *без* перезапуска ИДЕЯ IntelliJ hello следующие.</span><span class="sxs-lookup"><span data-stu-id="8dac5-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="8dac5-122">В ПОНЯТИЕ IntelliJ, hello **средства** меню точки слишком**Azure**и нажмите кнопку **выйти Azure**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Hello IntelliJ Azure входа с выходом-команда][L01]

2. <span data-ttu-id="8dac5-124">В hello **выйти Azure** окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Hello Azure выйти окно подтверждения][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="8dac5-126">Автоматический вход tooyour учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="8dac5-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="8dac5-127">В этом разделе показано, как создать файл учетных данных, содержащий данные субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="8dac5-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="8dac5-128">После завершения этого процесса Eclipse использует hello учетные данные файла tooautomatically выхода в tooAzure каждый раз при откройте свой проект.</span><span class="sxs-lookup"><span data-stu-id="8dac5-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="8dac5-129">Откройте проект с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="8dac5-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="8dac5-130">На hello **средства** меню выберите пункт слишком**Azure**и нажмите кнопку **входа в Azure**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Hello команда IntelliJ входа в Azure][A01]

3. <span data-ttu-id="8dac5-132">В hello **входа в Azure** выберите **автоматизирован**, а затем нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Вход в Azure окна Hello с выбран автоматический][A02]

4. <span data-ttu-id="8dac5-134">В hello **диалоговое окно входа Azure** окно, введите свои учетные данные Azure и нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Hello Azure входа диалоговое окно][A03]

5. <span data-ttu-id="8dac5-136">В hello **создать файлы для проверки подлинности** окно, выберите hello подписки требуется toouse, выберите каталог назначения и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Создание файлов для проверки подлинности окна Hello][A04]

6. <span data-ttu-id="8dac5-138">В hello **состояние создания участника службы** диалоговое окно, после успешного создания файлов, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![диалоговое окно состояния создания участника службы Hello][A05]

7. <span data-ttu-id="8dac5-140">В hello **входа в Azure** окно, нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Диалоговое окно входа в Azure][A06]

8. <span data-ttu-id="8dac5-142">В hello **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![диалоговое окно Выбор подписки Hello][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="8dac5-144">Выход из учетной записи Azure после автоматического входа</span><span class="sxs-lookup"><span data-stu-id="8dac5-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="8dac5-145">После настройки учетной записи с помощью предыдущих шагах hello hello набора средств Azure автоматически вход в tooyour при каждом перезапуске IntelliJ ИДЕЯ учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8dac5-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="8dac5-146">Тем не менее, toosign со стороны вашей учетной записью Azure и предотвратить hello набора средств Azure из автоматического входа, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="8dac5-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="8dac5-147">В ПОНЯТИЕ IntelliJ, hello **средства** меню точки слишком**Azure**и нажмите кнопку **выйти Azure**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Hello IntelliJ Azure входа с выходом-команда][L01]

2. <span data-ttu-id="8dac5-149">В hello **выйти Azure** окне подтверждения нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Hello Azure выйти окно подтверждения][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="8dac5-151">Автоматический вход в систему tooyour учетная запись Azure с помощью существующего файла учетных данных</span><span class="sxs-lookup"><span data-stu-id="8dac5-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="8dac5-152">Если при использовании IntelliJ ИДЕЯ, следует выйти из учетной записи Azure, необходимо использовать знак tooautomatically файл существующие учетные данные обратно в toohello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8dac5-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="8dac5-153">hello tooconfigure набора средств Azure для Eclipse toouse существующий файл учетных данных, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="8dac5-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="8dac5-154">Откройте проект с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="8dac5-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="8dac5-155">На hello **средства** меню выберите пункт слишком**Azure**и нажмите кнопку **входа в Azure**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Hello команда IntelliJ входа в Azure][A01]

3. <span data-ttu-id="8dac5-157">В hello **входа в Azure** выберите **автоматизирован**, а затем нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Вход в Azure окна Hello с выбран автоматический][A02]

4. <span data-ttu-id="8dac5-159">В hello **выберите файл проверки подлинности** диалоговое окно, выберите файл ранее созданные учетные данные и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Выберите файл проверки подлинности Hello-диалоговое окно][A08]

5. <span data-ttu-id="8dac5-161">В hello **входа в Azure** окно, нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Вход в Azure окна Hello с выбран автоматический][A06]

6. <span data-ttu-id="8dac5-163">В hello **подписки выберите** диалоговое окно, выберите hello подписки требуется toouse и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8dac5-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![диалоговое окно Выбор подписки Hello][A07]

## <a name="next-steps"></a><span data-ttu-id="8dac5-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8dac5-165">Next steps</span></span>
<span data-ttu-id="8dac5-166">Дополнительные сведения о hello наборы инструментов Azure для Java интегрированными средами разработки. в разделе hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="8dac5-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="8dac5-167">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8dac5-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8dac5-168">[Новые возможности средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="8dac5-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8dac5-169">[Установка средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="8dac5-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8dac5-170">[Инструкции вход для hello средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8dac5-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8dac5-171">[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8dac5-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="8dac5-172">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8dac5-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8dac5-173">[Новые возможности средств Azure для IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="8dac5-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8dac5-174">[Установка hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8dac5-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8dac5-175">*Вход инструкции для hello Azure Toolkit для IntelliJ* (Эта статья)</span><span class="sxs-lookup"><span data-stu-id="8dac5-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="8dac5-176">[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8dac5-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="8dac5-177">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="8dac5-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Инструкции вход для hello средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

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
