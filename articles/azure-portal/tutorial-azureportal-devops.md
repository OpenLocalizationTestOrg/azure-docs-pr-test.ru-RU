---
title: "Учебник: DevOps с hello портал Azure | Документы Microsoft"
description: "Дополнительные сведения hello различных рабочих процессов DevOps в hello портала Azure."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a><span data-ttu-id="05936-103">Учебник: DevOps с hello портала Azure</span><span class="sxs-lookup"><span data-stu-id="05936-103">Tutorial: DevOps with hello Azure Portal</span></span>
<span data-ttu-id="05936-104">гибкие рабочие процессы DevOps полон Hello платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="05936-104">hello Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="05936-105">В этом учебнике вы узнаете, как возможности hello tooleverage toodevelop hello портал Azure, тестирования, развертывания, устранение неполадок, мониторинга и управления выполняющихся приложений.</span><span class="sxs-lookup"><span data-stu-id="05936-105">In this tutorial, you learn how tooleverage hello capabilities of hello Azure Portal toodevelop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="05936-106">Этот учебник посвящен hello следующее:</span><span class="sxs-lookup"><span data-stu-id="05936-106">This tutorial focuses on hello following:</span></span>

1. <span data-ttu-id="05936-107">Создание веб-приложения и включение непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="05936-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="05936-108">Разработка и тестирование приложений.</span><span class="sxs-lookup"><span data-stu-id="05936-108">Develop and test an app</span></span>
3. <span data-ttu-id="05936-109">Мониторинг и устранение неполадок приложений.</span><span class="sxs-lookup"><span data-stu-id="05936-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="05936-110">Общие задачи управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="05936-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="05936-111">Создание веб-приложения и включение непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="05936-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="05936-112">Создать веб-приложение с [службе приложений Azure](https://azure.microsoft.com/services/app-service/), которая будет использоваться в hello конца данного учебника.</span><span class="sxs-lookup"><span data-stu-id="05936-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in hello rest of this tutorial.</span></span> <span data-ttu-id="05936-113">Кроме того, изначально потребуется включить непрерывное развертывание из репозитория исходного кода в выполняемую среду Azure.</span><span class="sxs-lookup"><span data-stu-id="05936-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="05936-114">Здравствуйте, вход в портал Azure</span><span class="sxs-lookup"><span data-stu-id="05936-114">Sign into hello Azure Portal</span></span>
2. <span data-ttu-id="05936-115">Выберите **службы приложений** &gt; **добавить значок** и введите имя, выберите подписку и создайте новый tooserve группы ресурсов в качестве hello контейнера для службы hello.</span><span class="sxs-lookup"><span data-stu-id="05936-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group tooserve as hello container for hello service.</span></span>
   
   <span data-ttu-id="05936-116">Группы ресурсов позволяют toomanage различных аспектов решения hello, например выставление счетов, развертывания и мониторинга все как одну группу через [диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05936-116">Resource groups allow you toomanage various aspects of hello solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![рисунок 1][image1]
3. <span data-ttu-id="05936-118">Через некоторое время будет создана служба приложений.</span><span class="sxs-lookup"><span data-stu-id="05936-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="05936-119">Занять несколько минут tooexplore hello различных параметров меню для службы hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="05936-119">Take a few minutes tooexplore hello various menu options for hello service in hello portal.</span></span>
   
   ![рисунок 2][image2]    
4. <span data-ttu-id="05936-121">Щелкните URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="05936-121">Click hello URL.</span></span> <span data-ttu-id="05936-122">Обратите внимание, hello различных доступных вариантов для репозиториев и средства.</span><span class="sxs-lookup"><span data-stu-id="05936-122">Notice hello variety of available choices for tools and repositories.</span></span> <span data-ttu-id="05936-123">Можно также использовать hello языки и платформы по своему усмотрению, включая .NET, Java и Ruby.</span><span class="sxs-lookup"><span data-stu-id="05936-123">You can also use hello languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="05936-125">Hello портал Azure делает непрерывного развертывания, это простой процесс, который включает в себя несколько простых шагов.</span><span class="sxs-lookup"><span data-stu-id="05936-125">hello Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="05936-126">В hello портал Azure выберите параметры значок hello hello приложения службы, которую вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="05936-126">In hello Azure portal, choose settings from hello icon for hello app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="05936-128">Из колонки hello открывшемся hello вправо прокрутите toohello публикации раздела.</span><span class="sxs-lookup"><span data-stu-id="05936-128">From hello blade that opens on hello right, scroll toohello publishing section.</span></span>
   
   ![рисунок 5][image5]
6. <span data-ttu-id="05936-130">Настройте некоторые параметры tooenable непрерывное развертывание приложения hello.</span><span class="sxs-lookup"><span data-stu-id="05936-130">Next, configure some settings tooenable continuous deployment for hello app.</span></span> <span data-ttu-id="05936-131">Щелкните "Источник развертывания", а затем выберите "Выбор источника".</span><span class="sxs-lookup"><span data-stu-id="05936-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="05936-132">Обратите внимание, hello разнообразные параметры, вами источникам репозиториев.</span><span class="sxs-lookup"><span data-stu-id="05936-132">Notice hello variety of options you have for repository sources.</span></span>
   
   ![рисунок 6][image6]
7. <span data-ttu-id="05936-134">Для этого примера выберите источник GitHub.</span><span class="sxs-lookup"><span data-stu-id="05936-134">For this example choose GitHub.</span></span> <span data-ttu-id="05936-135">При необходимости выберите выбранный вами репозиторий hello и настроить учетные данные авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="05936-135">Optionally choose hello repository of your choice and setup hello authorization credentials.</span></span>
   
   ![рисунок 7][image7]
8. <span data-ttu-id="05936-137">После авторизации tooyour репозитория затем выберите проектов и нужно toodeploy ветви.</span><span class="sxs-lookup"><span data-stu-id="05936-137">After authorization tooyour repository, you can then choose a project and branch you wish toodeploy.</span></span> <span data-ttu-id="05936-138">Ниже приведено несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="05936-138">There are several fictitious sample examples listed below.</span></span>
   
   ![рисунок 8][image8]
9. <span data-ttu-id="05936-140">Закончив, нажмите кнопку "OК".</span><span class="sxs-lookup"><span data-stu-id="05936-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="05936-141">Необходимо запустить уведомления toosee развертывания.</span><span class="sxs-lookup"><span data-stu-id="05936-141">You should start toosee notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="05936-143">Перейдите назад tooGitHub toosee hello webhook, который был создан источник управления toointegrate hello репозитория с Azure.</span><span class="sxs-lookup"><span data-stu-id="05936-143">Navigate back tooGitHub toosee hello webhook that was created toointegrate hello source control repo with Azure.</span></span> <span data-ttu-id="05936-144">Hello портала Azure обеспечивает интеграцию с GitHub с помощью нескольких простых шагов.</span><span class="sxs-lookup"><span data-stu-id="05936-144">hello Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="05936-146">toodemonstrate непрерывного развертывания, быстро добавить некоторые toohello содержимого репозитория.</span><span class="sxs-lookup"><span data-stu-id="05936-146">toodemonstrate continuous deployment, you quickly add some content toohello repository.</span></span> <span data-ttu-id="05936-147">Простой пример добавьте пример текстового файла tooa в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="05936-147">For a simple example, add a sample text file tooa GitHub repo.</span></span> <span data-ttu-id="05936-148">Вы являетесь свободного toouse .NET, Ruby, Python или другого типа приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="05936-148">You are free toouse .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="05936-149">Чувствовать себя свободного tooadd текстовый файл, ASP.NET MVC, Java и Ruby репозитория toohello приложения по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="05936-149">Feel free tooadd a text file, ASP.NET MVC, Java, or Ruby application toohello repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="05936-151">После фиксации изменений tooyour репозитория, можно увидеть новый инициировать развертывания в области уведомлений портала hello.</span><span class="sxs-lookup"><span data-stu-id="05936-151">After committing changes tooyour repository, you see a new deployment initiate in hello portal notifications area.</span></span> <span data-ttu-id="05936-152">Нажмите кнопку синхронизации, если вы не видите быстро изменения после фиксации tooyour репозитория.</span><span class="sxs-lookup"><span data-stu-id="05936-152">Click Sync if you do not quickly see changes after committing tooyour repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="05936-154">На этом этапе Если повторите и загрузить страницу приветствия для службы приложения hello, может появиться ошибка 403.</span><span class="sxs-lookup"><span data-stu-id="05936-154">At this point, if you try and load hello page for hello app service, you may receive a 403 error.</span></span> <span data-ttu-id="05936-155">В этом примере это потому, что не настраивать документа обычно по умолчанию используется для hello страницы, например файл как index.htm или default.html.</span><span class="sxs-lookup"><span data-stu-id="05936-155">In this example, it is because there is no typical default document setup for hello page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="05936-156">Это можно быстро исправить с hello в hello портала Azure для работы с проектами.</span><span class="sxs-lookup"><span data-stu-id="05936-156">You can quickly remedy this with hello tooling in hello Azure Portal.</span></span>  <span data-ttu-id="05936-157">В портале Azure hello выберите параметры &gt; параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="05936-157">In hello Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="05936-159">Откроется колонка "Параметры приложения".</span><span class="sxs-lookup"><span data-stu-id="05936-159">A blade opens for application settings.</span></span> <span data-ttu-id="05936-160">Введите имя hello hello страницы «SamplePage.html» и нажмите кнопку Сохранить.</span><span class="sxs-lookup"><span data-stu-id="05936-160">Enter hello name of hello page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="05936-161">Занять несколько минут tooexplore hello другие параметры.</span><span class="sxs-lookup"><span data-stu-id="05936-161">Take a few minutes tooexplore hello other settings.</span></span>
    
    ![рисунок 14][image14]
15. <span data-ttu-id="05936-163">При необходимости обновите tooensure URL-адрес вашего браузера, ожидается hello изменения.</span><span class="sxs-lookup"><span data-stu-id="05936-163">Optionally refresh your browser URL tooensure you see hello expected changes.</span></span> <span data-ttu-id="05936-164">В этом случае имеется простой текст, теперь заполнение страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="05936-164">In this case, there is some simple text now populating hello page.</span></span> <span data-ttu-id="05936-165">Каждого репозитория toohello дополнительных изменений приведет к новой автоматического развертывания.</span><span class="sxs-lookup"><span data-stu-id="05936-165">Each additional change toohello repository would result in a new automatic deployment.</span></span>
    
    ![рисунок 15][image15]
    
    <span data-ttu-id="05936-167">Включение непрерывное развертывание с портала Azure hello является простой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="05936-167">Enabling continuous deployment with hello Azure Portal is an easy experience.</span></span> <span data-ttu-id="05936-168">Кроме того, можно также строить более сложные конвейеры выпуска и использовать другие методы с существующие системы управления версиями и tooAzure toodeploy непрерывной интеграции систем, таких как использование автоматизированной сборки и выпуска системы управления.</span><span class="sxs-lookup"><span data-stu-id="05936-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems toodeploy tooAzure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="05936-169">Разработка и тестирование приложений</span><span class="sxs-lookup"><span data-stu-id="05936-169">Develop and test an app</span></span>
<span data-ttu-id="05936-170">Затем внести некоторые изменения кода toohello базового и быстрое развертывание этих изменений.</span><span class="sxs-lookup"><span data-stu-id="05936-170">Next, make some changes toohello code base and rapidly deploy those changes.</span></span> <span data-ttu-id="05936-171">Будет также настроить некоторые тестирование производительности для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="05936-171">You will also setup up some performance testing for hello Web app.</span></span>

1. <span data-ttu-id="05936-172">Выберите приложение службы hello области навигации в hello портала Azure и найдите приложение службы.</span><span class="sxs-lookup"><span data-stu-id="05936-172">In hello Azure Portal choose App Services from hello navigation pane, and locate your App Service.</span></span>
   
   ![рисунок 16][image16]
2. <span data-ttu-id="05936-174">Щелкните пункт "Инструменты".</span><span class="sxs-lookup"><span data-stu-id="05936-174">Click Tools</span></span>
   
   ![рисунок 17][image17]
3. <span data-ttu-id="05936-176">Обратите внимание, hello категории в составе средств разработки.</span><span class="sxs-lookup"><span data-stu-id="05936-176">Notice hello develop category under Tools.</span></span> <span data-ttu-id="05936-177">Существует несколько полезных инструментов здесь, позволяющие toowork с приложениями, не выходя из hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="05936-177">There are several useful tools here that allow us toowork with apps without leaving hello Azure Portal.</span></span> <span data-ttu-id="05936-178">Затем щелкните пункт "Консоль".</span><span class="sxs-lookup"><span data-stu-id="05936-178">Click on Console.</span></span>
   
   ![рисунок 18][image18]
4. <span data-ttu-id="05936-180">В окне консоли hello можно будет выполнять динамическую команды для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="05936-180">In hello console window, you can issue live commands for your app.</span></span> <span data-ttu-id="05936-181">Команда dir типа hello и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="05936-181">Type hello dir command and hit enter.</span></span> <span data-ttu-id="05936-182">Обратите внимание, что здесь не работают команды, требующие повышенных привилегий.</span><span class="sxs-lookup"><span data-stu-id="05936-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![рисунок 19][image19]
5. <span data-ttu-id="05936-184">Категории разработка toohello переход назад и выберите Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="05936-184">Move back toohello Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="05936-185">Примечание. Visual Studio Online теперь называется Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="05936-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![рисунок 20][image20]
6. <span data-ttu-id="05936-187">Переключение на hello возможности редактирования в браузере для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="05936-187">Toggle on hello in-browser editing experience for your App.</span></span>
   
   ![рисунок 21][image21]
7. <span data-ttu-id="05936-189">Установите для вашего приложения веб-расширение.</span><span class="sxs-lookup"><span data-stu-id="05936-189">A web extension installs for your app.</span></span> <span data-ttu-id="05936-190">Расширения быстро и легко добавлять tooapps функциональность в Azure.</span><span class="sxs-lookup"><span data-stu-id="05936-190">Extensions quickly and easily add functionality tooapps in Azure.</span></span> <span data-ttu-id="05936-191">Обратите внимание, некоторые hello других типов расширений, доступных в снимке hello.</span><span class="sxs-lookup"><span data-stu-id="05936-191">Notice some of hello other extension types available in hello screenshot below.</span></span>
   
   ![рисунок 22][image22]
8. <span data-ttu-id="05936-193">После установки расширения Visual Studio Online hello нажмите Перейти.</span><span class="sxs-lookup"><span data-stu-id="05936-193">Once hello Visual Studio Online extension installs, click Go.</span></span>
   
   ![рисунок 23][image23]
9. <span data-ttu-id="05936-195">Браузер откроется, где вы видите разработки (IDE) непосредственно в браузере hello вкладка.</span><span class="sxs-lookup"><span data-stu-id="05936-195">A browser tab opens where you see a development IDE directly in hello browser.</span></span> <span data-ttu-id="05936-196">Обратите внимание hello представленным ниже находится в Chrome.</span><span class="sxs-lookup"><span data-stu-id="05936-196">Notice hello experience below is in Chrome.</span></span>
   
   ![рисунок 24][image24]
10. <span data-ttu-id="05936-198">Можно выполнить несколько действий, таких как редактировать файлы, добавление файлов и папок и загрузки содержимого из hello действующем сайте.</span><span class="sxs-lookup"><span data-stu-id="05936-198">You can perform several activities such as edit files, add files and folders, and download content from hello live site.</span></span> <span data-ttu-id="05936-199">Сделайте файл SamplePage.html toohello быстрого редактирования.</span><span class="sxs-lookup"><span data-stu-id="05936-199">Make a quick edit toohello SamplePage.html file.</span></span>
    
    ![рисунок 25][image25]
11. <span data-ttu-id="05936-201">Через несколько секунд hello будут автоматически сохранены.</span><span class="sxs-lookup"><span data-stu-id="05936-201">In a few moments, hello changes are automatically saved.</span></span> <span data-ttu-id="05936-202">Если перейти назад toohello страницы, можно заметить изменения hello.</span><span class="sxs-lookup"><span data-stu-id="05936-202">If you navigate back toohello page, you can see hello changes.</span></span> <span data-ttu-id="05936-203">Помните, что такие изменения в реальном времени, скорее всего, не поддерживаются в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="05936-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="05936-204">Однако средства hello его очень легко toomake быстрого внесения изменений для разработки и тестовую среду.</span><span class="sxs-lookup"><span data-stu-id="05936-204">However, hello tools make it very easy toomake quick changes for dev and test environments.</span></span>
    
    ![рисунок 26][image26]
    
    ![рисунок 27][image27]
12. <span data-ttu-id="05936-207">Переход назад toohello средства колонки и категории разработка hello щелкните тест производительности.</span><span class="sxs-lookup"><span data-stu-id="05936-207">Move back toohello tools blade and under hello Develop category, click on Performance Test.</span></span>
    
    ![рисунок 28][image28]
13. <span data-ttu-id="05936-209">Необходимо tooset учетной записи team services.</span><span class="sxs-lookup"><span data-stu-id="05936-209">You need tooset a team services account.</span></span> <span data-ttu-id="05936-210">Дополнительные сведения о создании учетной записи Team Services. см. [здесь](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="05936-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="05936-211">Щелкните новый toocreate теста производительности.</span><span class="sxs-lookup"><span data-stu-id="05936-211">Click on New toocreate a performance test.</span></span>
    
    ![рисунок 29][image29]
    
    <span data-ttu-id="05936-213">Настройка hello различные значения и нажмите кнопку Запустить тест внизу hello tooinitiate диалоговой hello теста производительности.</span><span class="sxs-lookup"><span data-stu-id="05936-213">Configure hello various values and click Run Test at hello bottom of hello dialogue tooinitiate a performance test.</span></span>
    
    ![рисунок 30][image30]
    
    ![рисунок 31][image31]
15. <span data-ttu-id="05936-216">Как только начнется выполнение теста hello, вы можете отслеживать состояние hello.</span><span class="sxs-lookup"><span data-stu-id="05936-216">Once hello test starts running, you can monitor hello state.</span></span>
    
    ![рисунок 32][image32]
    
    <span data-ttu-id="05936-218">После завершения выполнения теста hello, щелкните hello результат, чтобы отобразить дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="05936-218">Once hello test finishes, clicking on hello result shows more details.</span></span>
    
    ![рисунок 33][image33]
16. <span data-ttu-id="05936-220">В этом примере вы создали небольшой тестового запуска, поэтому существует tooanalyze только данные, но вы можно просматривать различные показатели, а также повторно выполнить тест из этого представления.</span><span class="sxs-lookup"><span data-stu-id="05936-220">In this example, you created a small test run, so there is limited data tooanalyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="05936-221">Hello портала Azure делает создание, выполнение и анализ просто веб-тестов производительности.</span><span class="sxs-lookup"><span data-stu-id="05936-221">hello Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="05936-222">снимки экрана приветствия ниже отображать данные о производительности hello.</span><span class="sxs-lookup"><span data-stu-id="05936-222">hello screenshots below display hello performance data.</span></span>
    
    ![рисунок 34][image34]
    
    ![рисунок 35][image35]
    
    ![рисунок 36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="05936-226">Мониторинг и устранение неполадок приложений.</span><span class="sxs-lookup"><span data-stu-id="05936-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="05936-227">В Azure доступно множество средств для мониторинга и устранения неполадок приложений.</span><span class="sxs-lookup"><span data-stu-id="05936-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="05936-228">В hello портала Azure для наших веб-приложения выберите инструментов.</span><span class="sxs-lookup"><span data-stu-id="05936-228">In hello Azure Portal for our Web app choose Tools.</span></span>
   
   ![рисунок 37][image37]
2. <span data-ttu-id="05936-230">Устранение неполадок категории hello Обратите внимание hello различные способы использования средств tootroubleshoot потенциальных проблем с запущенным приложением.</span><span class="sxs-lookup"><span data-stu-id="05936-230">Under hello Troubleshoot category, notice hello various choices for using tools tootroubleshoot potential issues with a running app.</span></span> <span data-ttu-id="05936-231">Здесь можно отследить динамический HTTP-трафик, включить самовосстановление, просмотреть журналы и многое другое.</span><span class="sxs-lookup"><span data-stu-id="05936-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![рисунок 38][image38]
3. <span data-ttu-id="05936-233">Выберите представление некоторых кодов HTTP-get tooquickly метрики сайта.</span><span class="sxs-lookup"><span data-stu-id="05936-233">Choose Site Metrics tooquickly get a view of some HTTP codes.</span></span>
   
   ![рисунок 39][image39]
4. <span data-ttu-id="05936-235">Щелкните "Диагностика как услуга".</span><span class="sxs-lookup"><span data-stu-id="05936-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="05936-236">Выберите тип приложения и нажмите кнопку "Запустить".</span><span class="sxs-lookup"><span data-stu-id="05936-236">Choose your application type, then choose Run.</span></span>
   
   ![рисунок 40][image40]
   
   <span data-ttu-id="05936-238">Начнется сбор данных.</span><span class="sxs-lookup"><span data-stu-id="05936-238">A collection begins.</span></span>
   
   ![рисунок 41][image41]
5. <span data-ttu-id="05936-240">Вы можете hello соответствующего журнала toodiagnose потенциальные проблемы.</span><span class="sxs-lookup"><span data-stu-id="05936-240">You may choose hello appropriate log toodiagnose potential issues.</span></span> <span data-ttu-id="05936-241">Необходимо toosee tooenable ведения журнала, все доступные данные hello параметры, такие как журналы HTTP.</span><span class="sxs-lookup"><span data-stu-id="05936-241">You need tooenable logging toosee all of hello available data options such as HTTP Logs.</span></span>
   
   ![рисунок 42][image42]
   
   <span data-ttu-id="05936-243">Щелкнув файл дампа памяти hello можно загрузить и проанализировать DebugDiag toohelp отчета анализа обнаружение возможных проблем.</span><span class="sxs-lookup"><span data-stu-id="05936-243">By clicking on hello Memory Dump file you can download and analyze a DebugDiag analysis report toohelp find potential issues.</span></span>
   
   ![рисунок 43][image43]
6. <span data-ttu-id="05936-245">tooview больше данных требуется более подробное ведение журнала tooenable.</span><span class="sxs-lookup"><span data-stu-id="05936-245">tooview more data, you need tooenable additional logging.</span></span> <span data-ttu-id="05936-246">В hello портал Azure перейдите toohello веб-приложения и выберите параметры.</span><span class="sxs-lookup"><span data-stu-id="05936-246">In hello Azure Portal, navigate toohello Web app and choose Settings.</span></span>
   
   ![рисунок 44][image44]
7. <span data-ttu-id="05936-248">Прокрутите вниз категории функций toohello и выберите журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="05936-248">Scroll down toohello features category, and choose Diagnostic logs.</span></span>
   
      ![рисунок 45][image45]
8. <span data-ttu-id="05936-250">Обратите внимание: hello различные параметры для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="05936-250">Notice hello various options for logging.</span></span> <span data-ttu-id="05936-251">Включите ведение журнала веб-сервера и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="05936-251">Toggle on Web server logging and click save.</span></span>
   
   ![рисунок 46][image46]
9. <span data-ttu-id="05936-253">Возврат toohello области средств для приложения hello выберите диагностики как услуги и нажмите кнопку выполнения toorerun hello данных коллекции.</span><span class="sxs-lookup"><span data-stu-id="05936-253">Move back toohello tools area for hello app and choose Diagnostics as a service and click Run toorerun hello data collection.</span></span>
   
   ![рисунок 47][image47]
10. <span data-ttu-id="05936-255">Параметр ведения журнала hello HTTP включен, теперь увидеть данные, собранные для журналов HTTP.</span><span class="sxs-lookup"><span data-stu-id="05936-255">With hello HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![рисунок 48][image48]
11. <span data-ttu-id="05936-257">Нажимая кнопку hello HTML файл журнала, можно создать полнофункциональный отчет на основе браузера для дальнейшего изучения.</span><span class="sxs-lookup"><span data-stu-id="05936-257">By clicking hello HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![рисунок 49][image49]
12. <span data-ttu-id="05936-259">Переместите toohello средства раздела hello портала Azure для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="05936-259">Move back toohello tools section in hello Azure Portal for hello app.</span></span> <span data-ttu-id="05936-260">Прокрутите раздел средств toohello и выберите команду Process Explorer.</span><span class="sxs-lookup"><span data-stu-id="05936-260">Scroll toohello Tools section and choose Process Explorer.</span></span>
    
    ![рисунок 50][image50]
13. <span data-ttu-id="05936-262">Параметр "Обозреватель процессов" позволяет просматривать сведения о запущенных процессах.</span><span class="sxs-lookup"><span data-stu-id="05936-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="05936-263">Обратите внимание, ниже можно детализировать процессы и даже завершать процессы из hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="05936-263">Notice below you can drill into processes and even kill processes all from hello Azure Portal.</span></span>
    
    ![рисунок 51][image51]
    
    ![рисунок 52][image52]
14. <span data-ttu-id="05936-266">Переход назад колонку параметров toohello hello левой части экрана.</span><span class="sxs-lookup"><span data-stu-id="05936-266">Move back toohello Settings blade on hello left.</span></span> <span data-ttu-id="05936-267">Щелкните "Новый запрос в службу поддержки".</span><span class="sxs-lookup"><span data-stu-id="05936-267">Click New support request.</span></span>
    
    ![рисунок 53][image53]
15. <span data-ttu-id="05936-269">Из колонки hello на правом hello заполните сведения о проблемах hello, введите контактные данные и даже Отправка диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="05936-269">From hello blade on hello right, you can fill out details about hello issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="05936-270">Hello портал Azure позволяет работать со службой поддержки Майкрософт эффективной работы.</span><span class="sxs-lookup"><span data-stu-id="05936-270">hello Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![рисунок 54][image54]
    
    ![рисунок 55][image55]
    
    <span data-ttu-id="05936-273">Hello портала Azure помогает обеспечить эффективная и привычная монитор toohelp опыт работы с проектами и устранение неполадок нашей выполняющихся приложений.</span><span class="sxs-lookup"><span data-stu-id="05936-273">hello Azure Portal helps provide powerful and familiar tooling experiences toohelp monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="05936-274">Вы также являются действие tootake может быстро, выполнив действия, такие как перезапуск процессов, включение и отключение различные коллекции данных и даже интеграция с технической поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="05936-274">You are also able tootake action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="05936-275">Общие задачи управления приложениями</span><span class="sxs-lookup"><span data-stu-id="05936-275">General Application Management</span></span>
<span data-ttu-id="05936-276">Управление приложениями, часто требуется tooperform различные действия, такие как настройка стратегии резервного копирования, реализации и управлении поставщиками удостоверений и настройки управления доступом на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="05936-276">When managing applications, you often need tooperform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="05936-277">Как с hello другие виды взаимодействия с DevOps, hello платформы Azure интегрируется эти задачи непосредственно в портал hello.</span><span class="sxs-lookup"><span data-stu-id="05936-277">As with hello other DevOps experiences, hello Azure platform integrates these tasks directly into hello portal.</span></span>

1. <span data-ttu-id="05936-278">веб-приложения hello tooensure программы от потери данных необходимы резервные tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="05936-278">tooensure you are keeping hello Web App safe from data loss you need tooconfigure backups.</span></span> <span data-ttu-id="05936-279">Перейдите в область параметров toohello для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="05936-279">Navigate toohello Settings area for your Web app.</span></span>
   
   ![рисунок 56][image56]
2. <span data-ttu-id="05936-281">В колонке hello на правом hello прокрутите вниз toohello категории функций.</span><span class="sxs-lookup"><span data-stu-id="05936-281">In hello blade on hello right, scroll down toohello Features category.</span></span>
   
    ![рисунок 57][image57]
3. <span data-ttu-id="05936-283">Выберите резервные копии; на правом hello открывается стоечный модуль.</span><span class="sxs-lookup"><span data-stu-id="05936-283">Choose Backups; a blade opens on hello right.</span></span>
   
   ![рисунок 58][image58]
4. <span data-ttu-id="05936-285">Нажмите кнопку настроить, выберите учетную запись хранения из колонки hello на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="05936-285">Click Configure, choose a storage account from hello blade on hello right.</span></span>
   
   ![рисунок 59][image59]
5. <span data-ttu-id="05936-287">Теперь создайте и выберите toohold контейнер хранения резервных копий.</span><span class="sxs-lookup"><span data-stu-id="05936-287">Now create and choose a storage container toohold your backups.</span></span> <span data-ttu-id="05936-288">Нажмите кнопку Создать hello нижней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="05936-288">Click create at hello bottom of hello blade.</span></span> <span data-ttu-id="05936-289">Выберите контейнер hello.</span><span class="sxs-lookup"><span data-stu-id="05936-289">Then select hello container.</span></span>
   
   ![рисунок 60][image60]
6. <span data-ttu-id="05936-291">После выбора контейнера hello, можно настроить расписания, а также настройки резервного копирования для баз данных.</span><span class="sxs-lookup"><span data-stu-id="05936-291">Once you have chosen hello container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="05936-292">Для этого сценария щелкните hello сохранить значок.</span><span class="sxs-lookup"><span data-stu-id="05936-292">For this scenario, click hello save icon.</span></span>
   
    ![рисунок 61][image61]
7. <span data-ttu-id="05936-294">После сохранения прокрутки колонки задней toohello слева hello для резервных копий.</span><span class="sxs-lookup"><span data-stu-id="05936-294">After saving, scroll back toohello blade on hello left for Backups.</span></span> <span data-ttu-id="05936-295">Нажмите кнопку Создать резервную копию приложения hello tooback.</span><span class="sxs-lookup"><span data-stu-id="05936-295">Click Backup Now tooback hello application.</span></span>
   
    ![рисунок 62][image62]
8. <span data-ttu-id="05936-297">Через несколько секунд появится созданная резервная копия.</span><span class="sxs-lookup"><span data-stu-id="05936-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="05936-298">Обратите внимание hello восстановить параметр на снимке экрана ниже hello.</span><span class="sxs-lookup"><span data-stu-id="05936-298">Notice hello Restore Now option on hello screen-shot below.</span></span>
   
    ![рисунок 63][image63]
9. <span data-ttu-id="05936-300">Нажмите кнопку Восстановить и просмотрите колонки toohello параметры hello на правом hello.</span><span class="sxs-lookup"><span data-stu-id="05936-300">Click on Restore Now and examine hello options toohello blade on hello right.</span></span> <span data-ttu-id="05936-301">Можно выбрать соответствующий резервного копирования и легко tooan восстановления ранее состояние при необходимости.</span><span class="sxs-lookup"><span data-stu-id="05936-301">You can choose an appropriate backup and easily restore tooan earlier state as necessary.</span></span> <span data-ttu-id="05936-302">Hello портал Azure помогли нам легко включить стратегии приложение hello простой аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="05936-302">hello Azure portal has helped us easily enable a simple disaster recovery strategy for hello app.</span></span>
   
    ![рисунок 64][image64]
10. <span data-ttu-id="05936-304">Возврат колонку параметров toohello hello левой части экрана, а также в разделе функции и выберите проверку подлинности и авторизации.</span><span class="sxs-lookup"><span data-stu-id="05936-304">Move back toohello Settings blade on hello left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![рисунок 65][image65]
11. <span data-ttu-id="05936-306">В колонке hello на hello справа выберите проверку подлинности службы приложения.</span><span class="sxs-lookup"><span data-stu-id="05936-306">In hello blade on hello right choose App Service Authentication.</span></span> <span data-ttu-id="05936-307">Обратите внимание, hello разнообразные параметры, которые можно настроить с помощью популярных поставщиков.</span><span class="sxs-lookup"><span data-stu-id="05936-307">Notice hello variety of options you can configure with popular providers.</span></span>
    
     ![рисунок 66][image66]
12. <span data-ttu-id="05936-309">Выберите hello поставщика по вашему выбору и обратите внимание hello параметры области hello.</span><span class="sxs-lookup"><span data-stu-id="05936-309">Choose hello provider of your choice and notice hello options for hello scope.</span></span> <span data-ttu-id="05936-310">Можно указать идентификатор приложения и секрет приложения и быстро включить проверку подлинности Facebook для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="05936-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for hello app.</span></span> <span data-ttu-id="05936-311">Hello портала Azure включает проверку подлинности как готовое к использованию решение для приложения.</span><span class="sxs-lookup"><span data-stu-id="05936-311">hello Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![рисунок 67][image67]
13. <span data-ttu-id="05936-313">Переход назад toohello колонку параметров и выберите пользователей, управление ресурсами категории hello.</span><span class="sxs-lookup"><span data-stu-id="05936-313">Move back toohello Settings blade and choose Users under hello Resource Management category.</span></span>
    
     ![рисунок 68][image68]
14. <span data-ttu-id="05936-315">В колонке hello на правом hello проанализировать hello различные параметры для добавления ролей и пользователей.</span><span class="sxs-lookup"><span data-stu-id="05936-315">In hello blade on hello right examine hello various options for adding roles and users.</span></span> <span data-ttu-id="05936-316">Hello портал Azure позволяет легко управлять RBAC (Управление доступом на основе ролей) для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="05936-316">hello Azure Portal lets you easily control RBAC (Role-based access control) for hello application.</span></span>
    
     ![рисунок 69][image69]

## <a name="summary"></a><span data-ttu-id="05936-318">Сводка</span><span class="sxs-lookup"><span data-stu-id="05936-318">Summary</span></span>
<span data-ttu-id="05936-319">Этот учебник рассмотренные некоторые hello питания с hello платформы Azure быстро Включение непрерывное развертывание веб-приложения, выполнение различных разработки и тестирования действий, мониторинг и устранение неполадок является динамическим приложением и наконец управлении ключами стратегии аварийного восстановления, удостоверений и управления доступом на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="05936-319">This tutorial demonstrated some of hello power with hello Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="05936-320">Hello платформы Azure обеспечивает единство подхода для этих рабочих процессов DevOps и эффективной работы всегда остается в контекст для поставленной задачи hello.</span><span class="sxs-lookup"><span data-stu-id="05936-320">hello Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for hello task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05936-321">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05936-321">Next steps</span></span>
* <span data-ttu-id="05936-322">Диспетчер ресурсов Azure важно для включения DevOps на hello платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="05936-322">Azure Resource Manager is important for enabling DevOps on hello Azure platform.</span></span>  <span data-ttu-id="05936-323">более посетите toolearn [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05936-323">toolearn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="05936-324">Дополнительные сведения о развертывании службы приложения Azure посетите toolearn [развертывание вашего приложения tooAzure службы приложений](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="05936-324">toolearn more about Azure App Service deployment visit [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
