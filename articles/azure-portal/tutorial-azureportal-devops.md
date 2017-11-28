---
title: "Руководство по рабочим процессам DevOps на портале Azure | Документация Майкрософт"
description: "Узнайте о различных рабочих процессах DevOps, доступных на портале Azure."
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
ms.openlocfilehash: eec7d1402bdea4e5433c473dd713eed23aa80464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-devops-with-the-azure-portal"></a><span data-ttu-id="8b272-103">Руководство: рабочие процессы DevOps на портале Azure</span><span class="sxs-lookup"><span data-stu-id="8b272-103">Tutorial: DevOps with the Azure Portal</span></span>
<span data-ttu-id="8b272-104">Платформа Azure поддерживает множество гибких рабочих процессов разработки и операций (DevOps).</span><span class="sxs-lookup"><span data-stu-id="8b272-104">The Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="8b272-105">В этом руководстве вы узнаете, как использовать возможности портала Azure для разработки, тестирования, развертывания, устранения неполадок и мониторинга приложения, а также управления им.</span><span class="sxs-lookup"><span data-stu-id="8b272-105">In this tutorial, you learn how to leverage the capabilities of the Azure Portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="8b272-106">Здесь рассматриваются следующие вопросы.</span><span class="sxs-lookup"><span data-stu-id="8b272-106">This tutorial focuses on the following:</span></span>

1. <span data-ttu-id="8b272-107">Создание веб-приложения и включение непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="8b272-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="8b272-108">Разработка и тестирование приложений.</span><span class="sxs-lookup"><span data-stu-id="8b272-108">Develop and test an app</span></span>
3. <span data-ttu-id="8b272-109">Мониторинг и устранение неполадок приложений.</span><span class="sxs-lookup"><span data-stu-id="8b272-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="8b272-110">Общие задачи управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="8b272-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="8b272-111">Создание веб-приложения и включение непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="8b272-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="8b272-112">Чтобы выполнить действия, описанные в этом руководстве, необходимо создать веб-приложение с помощью [службы приложений Azure](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="8b272-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span></span> <span data-ttu-id="8b272-113">Кроме того, изначально потребуется включить непрерывное развертывание из репозитория исходного кода в выполняемую среду Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="8b272-114">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-114">Sign into the Azure Portal</span></span>
2. <span data-ttu-id="8b272-115">Выберите **Службы приложений** &gt; **Добавить значок**, а затем укажите имя, выберите подписку и создайте группу ресурсов для использования в качестве контейнера для службы.</span><span class="sxs-lookup"><span data-stu-id="8b272-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span></span>
   
   <span data-ttu-id="8b272-116">Группы ресурсов позволяют одновременно управлять выставлением счетов, развертыванием, отслеживанием и другими заданиями для всех ресурсов с помощью [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b272-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![рисунок 1][image1]
3. <span data-ttu-id="8b272-118">Через некоторое время будет создана служба приложений.</span><span class="sxs-lookup"><span data-stu-id="8b272-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="8b272-119">Просмотрите доступные параметры меню для этой службы на портале.</span><span class="sxs-lookup"><span data-stu-id="8b272-119">Take a few minutes to explore the various menu options for the service in the portal.</span></span>
   
   ![рисунок 2][image2]    
4. <span data-ttu-id="8b272-121">Щелкните URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8b272-121">Click the URL.</span></span> <span data-ttu-id="8b272-122">Обратите внимание на инструменты и репозитории, доступные на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-122">Notice the variety of available choices for tools and repositories.</span></span> <span data-ttu-id="8b272-123">Кроме того, вам предоставляется широкий выбор языков и платформ, включая .NET, Java и Ruby.</span><span class="sxs-lookup"><span data-stu-id="8b272-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="8b272-125">На портале Azure непрерывное развертывание можно включить всего за несколько простых шагов.</span><span class="sxs-lookup"><span data-stu-id="8b272-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="8b272-126">Щелкните значок созданной службы приложений, чтобы просмотреть доступные для нее параметры.</span><span class="sxs-lookup"><span data-stu-id="8b272-126">In the Azure portal, choose settings from the icon for the app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="8b272-128">В колонке справа прокрутите вниз к разделу публикации.</span><span class="sxs-lookup"><span data-stu-id="8b272-128">From the blade that opens on the right, scroll to the publishing section.</span></span>
   
   ![рисунок 5][image5]
6. <span data-ttu-id="8b272-130">Далее, чтобы включить для приложения непрерывное развертывание, необходимо настроить некоторые параметры.</span><span class="sxs-lookup"><span data-stu-id="8b272-130">Next, configure some settings to enable continuous deployment for the app.</span></span> <span data-ttu-id="8b272-131">Щелкните "Источник развертывания", а затем выберите "Выбор источника".</span><span class="sxs-lookup"><span data-stu-id="8b272-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="8b272-132">Обратите внимание на доступные источники репозиториев.</span><span class="sxs-lookup"><span data-stu-id="8b272-132">Notice the variety of options you have for repository sources.</span></span>
   
   ![рисунок 6][image6]
7. <span data-ttu-id="8b272-134">Для этого примера выберите источник GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b272-134">For this example choose GitHub.</span></span> <span data-ttu-id="8b272-135">При необходимости можно выбрать другой репозиторий и настроить для него учетные данные авторизации.</span><span class="sxs-lookup"><span data-stu-id="8b272-135">Optionally choose the repository of your choice and setup the authorization credentials.</span></span>
   
   ![рисунок 7][image7]
8. <span data-ttu-id="8b272-137">После авторизации в репозитории выберите проект и филиал, откуда будет проводиться развертывание.</span><span class="sxs-lookup"><span data-stu-id="8b272-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span></span> <span data-ttu-id="8b272-138">Ниже приведено несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="8b272-138">There are several fictitious sample examples listed below.</span></span>
   
   ![рисунок 8][image8]
9. <span data-ttu-id="8b272-140">Закончив, нажмите кнопку "OК".</span><span class="sxs-lookup"><span data-stu-id="8b272-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="8b272-141">После запуска будут отображаться уведомления о развертывании.</span><span class="sxs-lookup"><span data-stu-id="8b272-141">You should start to see notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="8b272-143">Вернитесь на портал GitHub, чтобы просмотреть объект webhook, созданный для интеграции репозитория системы управления версиями в Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span></span> <span data-ttu-id="8b272-144">Интеграция с GitHub на портале Azure выполняется очень просто.</span><span class="sxs-lookup"><span data-stu-id="8b272-144">The Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="8b272-146">Чтобы продемонстрировать возможности непрерывного развертывания, добавьте в репозиторий Github содержимое.</span><span class="sxs-lookup"><span data-stu-id="8b272-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span></span> <span data-ttu-id="8b272-147">Например, текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="8b272-147">For a simple example, add a sample text file to a GitHub repo.</span></span> <span data-ttu-id="8b272-148">Со службой приложений также можете использовать приложения .NET, Ruby, Python и другие.</span><span class="sxs-lookup"><span data-stu-id="8b272-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="8b272-149">В репозиторий можно добавлять текстовые файлы, а также приложения ASP.NET MVC, Java или Ruby.</span><span class="sxs-lookup"><span data-stu-id="8b272-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="8b272-151">После применения изменений в репозитории на портале в области уведомлений отобразится новое уведомление о развертывании.</span><span class="sxs-lookup"><span data-stu-id="8b272-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span></span> <span data-ttu-id="8b272-152">Если изменения не отображаются, нажмите кнопку "Синхронизировать".</span><span class="sxs-lookup"><span data-stu-id="8b272-152">Click Sync if you do not quickly see changes after committing to your repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="8b272-154">На этом этапе при загрузке страницы для службы приложений может появиться ошибка 403.</span><span class="sxs-lookup"><span data-stu-id="8b272-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span></span> <span data-ttu-id="8b272-155">Это происходит из-за того, что для страницы не задан документ по умолчанию (например, index.htm или default.html).</span><span class="sxs-lookup"><span data-stu-id="8b272-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="8b272-156">Используйте средства на портале Azure, чтобы быстро настроить для страницы документ по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8b272-156">You can quickly remedy this with the tooling in the Azure Portal.</span></span>  <span data-ttu-id="8b272-157">На портале Azure выберите "Параметры" &gt; "Параметры приложения".</span><span class="sxs-lookup"><span data-stu-id="8b272-157">In the Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="8b272-159">Откроется колонка "Параметры приложения".</span><span class="sxs-lookup"><span data-stu-id="8b272-159">A blade opens for application settings.</span></span> <span data-ttu-id="8b272-160">Укажите для страницы имя SamplePage.html и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="8b272-160">Enter the name of the page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="8b272-161">Просмотрите также другие доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="8b272-161">Take a few minutes to explore the other settings.</span></span>
    
    ![рисунок 14][image14]
15. <span data-ttu-id="8b272-163">При необходимости обновите URL-адрес браузера, чтобы убедиться, что изменения применены.</span><span class="sxs-lookup"><span data-stu-id="8b272-163">Optionally refresh your browser URL to ensure you see the expected changes.</span></span> <span data-ttu-id="8b272-164">Если это так, на странице появится текст.</span><span class="sxs-lookup"><span data-stu-id="8b272-164">In this case, there is some simple text now populating the page.</span></span> <span data-ttu-id="8b272-165">При внесении дополнительных изменений в репозитории будет выполняться автоматическое развертывание.</span><span class="sxs-lookup"><span data-stu-id="8b272-165">Each additional change to the repository would result in a new automatic deployment.</span></span>
    
    ![рисунок 15][image15]
    
    <span data-ttu-id="8b272-167">Включить непрерывное развертывание с помощью портала Azure несложно.</span><span class="sxs-lookup"><span data-stu-id="8b272-167">Enabling continuous deployment with the Azure Portal is an easy experience.</span></span> <span data-ttu-id="8b272-168">Вы также можете создать более сложные конвейеры выпуска и использовать другие методы с текущей системой управления версиями и системами непрерывной интеграции (например, использование автоматических систем управления сборкой и выпуском) для развертывания приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="8b272-169">Разработка и тестирование приложений</span><span class="sxs-lookup"><span data-stu-id="8b272-169">Develop and test an app</span></span>
<span data-ttu-id="8b272-170">Теперь нам необходимо внести некоторые изменения в базу кода и быстро развернуть их,</span><span class="sxs-lookup"><span data-stu-id="8b272-170">Next, make some changes to the code base and rapidly deploy those changes.</span></span> <span data-ttu-id="8b272-171">а также настроить тестирование производительности веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8b272-171">You will also setup up some performance testing for the Web app.</span></span>

1. <span data-ttu-id="8b272-172">В области навигации портала Azure щелкните "Службы приложений" и выберите вашу службу приложений.</span><span class="sxs-lookup"><span data-stu-id="8b272-172">In the Azure Portal choose App Services from the navigation pane, and locate your App Service.</span></span>
   
   ![рисунок 16][image16]
2. <span data-ttu-id="8b272-174">Щелкните пункт "Инструменты".</span><span class="sxs-lookup"><span data-stu-id="8b272-174">Click Tools</span></span>
   
   ![рисунок 17][image17]
3. <span data-ttu-id="8b272-176">Обратите внимание на инструменты, доступные в категории "Разработка".</span><span class="sxs-lookup"><span data-stu-id="8b272-176">Notice the develop category under Tools.</span></span> <span data-ttu-id="8b272-177">Они позволяют работать с приложениями непосредственно на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-177">There are several useful tools here that allow us to work with apps without leaving the Azure Portal.</span></span> <span data-ttu-id="8b272-178">Затем щелкните пункт "Консоль".</span><span class="sxs-lookup"><span data-stu-id="8b272-178">Click on Console.</span></span>
   
   ![рисунок 18][image18]
4. <span data-ttu-id="8b272-180">В окне консоли можно выполнять команды для приложения.</span><span class="sxs-lookup"><span data-stu-id="8b272-180">In the console window, you can issue live commands for your app.</span></span> <span data-ttu-id="8b272-181">Введите команду dir и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="8b272-181">Type the dir command and hit enter.</span></span> <span data-ttu-id="8b272-182">Обратите внимание, что здесь не работают команды, требующие повышенных привилегий.</span><span class="sxs-lookup"><span data-stu-id="8b272-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![рисунок 19][image19]
5. <span data-ttu-id="8b272-184">Вернитесь к категории "Разработка" и выберите Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="8b272-184">Move back to the Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="8b272-185">Примечание. Visual Studio Online теперь называется Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="8b272-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![рисунок 20][image20]
6. <span data-ttu-id="8b272-187">Активируйте возможность редактирования приложения в браузере.</span><span class="sxs-lookup"><span data-stu-id="8b272-187">Toggle on the in-browser editing experience for your App.</span></span>
   
   ![рисунок 21][image21]
7. <span data-ttu-id="8b272-189">Установите для вашего приложения веб-расширение.</span><span class="sxs-lookup"><span data-stu-id="8b272-189">A web extension installs for your app.</span></span> <span data-ttu-id="8b272-190">С помощью расширений можно быстро и легко добавлять функции для приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-190">Extensions quickly and easily add functionality to apps in Azure.</span></span> <span data-ttu-id="8b272-191">На снимке экрана ниже показаны другие доступные типы расширений.</span><span class="sxs-lookup"><span data-stu-id="8b272-191">Notice some of the other extension types available in the screenshot below.</span></span>
   
   ![рисунок 22][image22]
8. <span data-ttu-id="8b272-193">После установки расширения Visual Studio Online щелкните "Перейти".</span><span class="sxs-lookup"><span data-stu-id="8b272-193">Once the Visual Studio Online extension installs, click Go.</span></span>
   
   ![рисунок 23][image23]
9. <span data-ttu-id="8b272-195">Непосредственно в браузере откроется вкладка с интегрированной средой разработки.</span><span class="sxs-lookup"><span data-stu-id="8b272-195">A browser tab opens where you see a development IDE directly in the browser.</span></span> <span data-ttu-id="8b272-196">Вот как она выглядит в браузере Chrome:</span><span class="sxs-lookup"><span data-stu-id="8b272-196">Notice the experience below is in Chrome.</span></span>
   
   ![рисунок 24][image24]
10. <span data-ttu-id="8b272-198">Здесь вы можете редактировать файлы, добавлять папки и файлы, а также скачивать содержимое активного сайта.</span><span class="sxs-lookup"><span data-stu-id="8b272-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span></span> <span data-ttu-id="8b272-199">Внесите изменения в файл SamplePage.html.</span><span class="sxs-lookup"><span data-stu-id="8b272-199">Make a quick edit to the SamplePage.html file.</span></span>
    
    ![рисунок 25][image25]
11. <span data-ttu-id="8b272-201">Через несколько секунд изменения будут автоматически сохранены.</span><span class="sxs-lookup"><span data-stu-id="8b272-201">In a few moments, the changes are automatically saved.</span></span> <span data-ttu-id="8b272-202">Чтобы просмотреть их, вернитесь на страницу.</span><span class="sxs-lookup"><span data-stu-id="8b272-202">If you navigate back to the page, you can see the changes.</span></span> <span data-ttu-id="8b272-203">Помните, что такие изменения в реальном времени, скорее всего, не поддерживаются в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="8b272-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="8b272-204">Тем не менее доступные инструменты позволяют быстро и легко выполнять изменения в средах разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="8b272-204">However, the tools make it very easy to make quick changes for dev and test environments.</span></span>
    
    ![рисунок 26][image26]
    
    ![рисунок 27][image27]
12. <span data-ttu-id="8b272-207">Вернитесь к колонке "Инструменты" и в категории "Разработка" щелкните "Тест производительности".</span><span class="sxs-lookup"><span data-stu-id="8b272-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span></span>
    
    ![рисунок 28][image28]
13. <span data-ttu-id="8b272-209">Чтобы выполнить тест производительности, необходимо создать учетную запись Team Services.</span><span class="sxs-lookup"><span data-stu-id="8b272-209">You need to set a team services account.</span></span> <span data-ttu-id="8b272-210">Дополнительные сведения о создании учетной записи Team Services. см. [здесь](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="8b272-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="8b272-211">Щелкните "Создать", чтобы создать тест производительности.</span><span class="sxs-lookup"><span data-stu-id="8b272-211">Click on New to create a performance test.</span></span>
    
    ![рисунок 29][image29]
    
    <span data-ttu-id="8b272-213">Задайте различные значения и в нижней части диалогового окна нажмите кнопку "Запустить тест".</span><span class="sxs-lookup"><span data-stu-id="8b272-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span></span>
    
    ![рисунок 30][image30]
    
    ![рисунок 31][image31]
15. <span data-ttu-id="8b272-216">Во время выполнения теста можно отслеживать его состояние.</span><span class="sxs-lookup"><span data-stu-id="8b272-216">Once the test starts running, you can monitor the state.</span></span>
    
    ![рисунок 32][image32]
    
    <span data-ttu-id="8b272-218">После завершения теста щелкните результат, чтобы просмотреть дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="8b272-218">Once the test finishes, clicking on the result shows more details.</span></span>
    
    ![рисунок 33][image33]
16. <span data-ttu-id="8b272-220">Наш тест выполнялся недолго, поэтому данных для анализа совсем немного, но в открывшемся представлении можно просмотреть различные метрики и при необходимости повторно выполнить тест.</span><span class="sxs-lookup"><span data-stu-id="8b272-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="8b272-221">Создавать и выполнять тесты производительности, а также анализировать полученные результаты на портале Azure очень просто.</span><span class="sxs-lookup"><span data-stu-id="8b272-221">The Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="8b272-222">На снимках экрана ниже показаны показатели производительности, полученные после выполнения теста.</span><span class="sxs-lookup"><span data-stu-id="8b272-222">The screenshots below display the performance data.</span></span>
    
    ![рисунок 34][image34]
    
    ![рисунок 35][image35]
    
    ![рисунок 36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="8b272-226">Мониторинг и устранение неполадок приложений.</span><span class="sxs-lookup"><span data-stu-id="8b272-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="8b272-227">В Azure доступно множество средств для мониторинга и устранения неполадок приложений.</span><span class="sxs-lookup"><span data-stu-id="8b272-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="8b272-228">На портале Azure для нашего веб-приложения щелкните "Инструменты".</span><span class="sxs-lookup"><span data-stu-id="8b272-228">In the Azure Portal for our Web app choose Tools.</span></span>
   
   ![рисунок 37][image37]
2. <span data-ttu-id="8b272-230">В категории "Устранение неполадок" просмотрите доступные инструменты для устранения потенциальных неполадок с работающим приложением.</span><span class="sxs-lookup"><span data-stu-id="8b272-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span></span> <span data-ttu-id="8b272-231">Здесь можно отследить динамический HTTP-трафик, включить самовосстановление, просмотреть журналы и многое другое.</span><span class="sxs-lookup"><span data-stu-id="8b272-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![рисунок 38][image38]
3. <span data-ttu-id="8b272-233">Чтобы просмотреть некоторые коды HTTP, выберите "Метрики сайта".</span><span class="sxs-lookup"><span data-stu-id="8b272-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span></span>
   
   ![рисунок 39][image39]
4. <span data-ttu-id="8b272-235">Щелкните "Диагностика как услуга".</span><span class="sxs-lookup"><span data-stu-id="8b272-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="8b272-236">Выберите тип приложения и нажмите кнопку "Запустить".</span><span class="sxs-lookup"><span data-stu-id="8b272-236">Choose your application type, then choose Run.</span></span>
   
   ![рисунок 40][image40]
   
   <span data-ttu-id="8b272-238">Начнется сбор данных.</span><span class="sxs-lookup"><span data-stu-id="8b272-238">A collection begins.</span></span>
   
   ![рисунок 41][image41]
5. <span data-ttu-id="8b272-240">Для диагностики потенциальных неполадок можно выбрать соответствующий журнал.</span><span class="sxs-lookup"><span data-stu-id="8b272-240">You may choose the appropriate log to diagnose potential issues.</span></span> <span data-ttu-id="8b272-241">Чтобы просмотреть доступные данные (например, журналы HTTP), необходимо включить ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="8b272-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span></span>
   
   ![рисунок 42][image42]
   
   <span data-ttu-id="8b272-243">Если щелкнуть файл дампа памяти, загрузится отчет об анализе DebugDiag, с помощью которого можно определить потенциальные неполадки.</span><span class="sxs-lookup"><span data-stu-id="8b272-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span></span>
   
   ![рисунок 43][image43]
6. <span data-ttu-id="8b272-245">Чтобы получить более детальный отчет, необходимо включить дополнительные возможности ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="8b272-245">To view more data, you need to enable additional logging.</span></span> <span data-ttu-id="8b272-246">На портале Azure перейдите к веб-приложению и выберите "Параметры".</span><span class="sxs-lookup"><span data-stu-id="8b272-246">In the Azure Portal, navigate to the Web app and choose Settings.</span></span>
   
   ![рисунок 44][image44]
7. <span data-ttu-id="8b272-248">Прокрутите вниз к категории "Возможности" и выберите "Журналы диагностики".</span><span class="sxs-lookup"><span data-stu-id="8b272-248">Scroll down to the features category, and choose Diagnostic logs.</span></span>
   
      ![рисунок 45][image45]
8. <span data-ttu-id="8b272-250">Там вы увидите различные доступные параметры ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="8b272-250">Notice the various options for logging.</span></span> <span data-ttu-id="8b272-251">Включите ведение журнала веб-сервера и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="8b272-251">Toggle on Web server logging and click save.</span></span>
   
   ![рисунок 46][image46]
9. <span data-ttu-id="8b272-253">Вернитесь к области "Инструменты" приложения, выберите "Диагностика как услуга" и нажмите кнопку "Запустить", чтобы повторно запустить сбор данных.</span><span class="sxs-lookup"><span data-stu-id="8b272-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span></span>
   
   ![рисунок 47][image47]
10. <span data-ttu-id="8b272-255">Параметр "Ведение журнала HTTP" позволяет просматривать данные, собранные для журналов HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b272-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![рисунок 48][image48]
11. <span data-ttu-id="8b272-257">Щелкните файл журнала HTML, чтобы создать в браузере объемный отчет для последующего изучения.</span><span class="sxs-lookup"><span data-stu-id="8b272-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![рисунок 49][image49]
12. <span data-ttu-id="8b272-259">Вернитесь к разделу "Инструменты" для приложения на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-259">Move back to the tools section in the Azure Portal for the app.</span></span> <span data-ttu-id="8b272-260">Прокрутите вниз к разделу "Инструменты" и выберите "Обозреватель процессов".</span><span class="sxs-lookup"><span data-stu-id="8b272-260">Scroll to the Tools section and choose Process Explorer.</span></span>
    
    ![рисунок 50][image50]
13. <span data-ttu-id="8b272-262">Параметр "Обозреватель процессов" позволяет просматривать сведения о запущенных процессах.</span><span class="sxs-lookup"><span data-stu-id="8b272-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="8b272-263">На снимке экрана ниже видно, что можно просмотреть более детальные сведения о процессе и даже завершить все процессы с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-263">Notice below you can drill into processes and even kill processes all from the Azure Portal.</span></span>
    
    ![рисунок 51][image51]
    
    ![рисунок 52][image52]
14. <span data-ttu-id="8b272-266">Вернитесь к колонке "Параметры" в левой части окна.</span><span class="sxs-lookup"><span data-stu-id="8b272-266">Move back to the Settings blade on the left.</span></span> <span data-ttu-id="8b272-267">Щелкните "Новый запрос в службу поддержки".</span><span class="sxs-lookup"><span data-stu-id="8b272-267">Click New support request.</span></span>
    
    ![рисунок 53][image53]
15. <span data-ttu-id="8b272-269">В колонке справа можно добавить сведения о неполадках, контактную информацию и даже загрузить данные диагностики.</span><span class="sxs-lookup"><span data-stu-id="8b272-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="8b272-270">Портал Azure поддерживает работу со службой поддержки Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8b272-270">The Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![рисунок 54][image54]
    
    ![рисунок 55][image55]
    
    <span data-ttu-id="8b272-273">На портале Azure предоставляются эффективные привычные средства для мониторинга и устранения неполадок приложений.</span><span class="sxs-lookup"><span data-stu-id="8b272-273">The Azure Portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="8b272-274">Кроме того, здесь можно быстро принимать меры по устранению неполадок, выполняя такие задачи, как перезапуск процессов, включение и отключение разных наборов данных и даже интеграцию со службой поддержки Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8b272-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="8b272-275">Общие задачи управления приложениями</span><span class="sxs-lookup"><span data-stu-id="8b272-275">General Application Management</span></span>
<span data-ttu-id="8b272-276">Управление приложениями всегда сопряжено с выполнением самых разных задач, таких как настройка параметров резервного копирования, реализация поставщика удостоверений и управление им, а также настройка управления доступом на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="8b272-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="8b272-277">Как и другие задачи DevOps, эти задачи можно выполнять непосредственно на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span></span>

1. <span data-ttu-id="8b272-278">Чтобы защитить веб-приложение от потери данных, необходимо настроить резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="8b272-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span></span> <span data-ttu-id="8b272-279">Перейдите в область "Параметры" для вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8b272-279">Navigate to the Settings area for your Web app.</span></span>
   
   ![рисунок 56][image56]
2. <span data-ttu-id="8b272-281">В колонке справа прокрутите вниз к категории "Возможности".</span><span class="sxs-lookup"><span data-stu-id="8b272-281">In the blade on the right, scroll down to the Features category.</span></span>
   
    ![рисунок 57][image57]
3. <span data-ttu-id="8b272-283">Выберите пункт "Резервные копии". Справа откроется колонка.</span><span class="sxs-lookup"><span data-stu-id="8b272-283">Choose Backups; a blade opens on the right.</span></span>
   
   ![рисунок 58][image58]
4. <span data-ttu-id="8b272-285">Щелкните "Настроить" и в колонке справа выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="8b272-285">Click Configure, choose a storage account from the blade on the right.</span></span>
   
   ![рисунок 59][image59]
5. <span data-ttu-id="8b272-287">Затем создайте и выберите контейнер хранилища для хранения резервных копий.</span><span class="sxs-lookup"><span data-stu-id="8b272-287">Now create and choose a storage container to hold your backups.</span></span> <span data-ttu-id="8b272-288">Щелкните кнопку "Создать" в нижней части колонки,</span><span class="sxs-lookup"><span data-stu-id="8b272-288">Click create at the bottom of the blade.</span></span> <span data-ttu-id="8b272-289">а затем выберите контейнер.</span><span class="sxs-lookup"><span data-stu-id="8b272-289">Then select the container.</span></span>
   
   ![рисунок 60][image60]
6. <span data-ttu-id="8b272-291">После этого можно настроить расписания, а также резервное копирование для вашей базы данных.</span><span class="sxs-lookup"><span data-stu-id="8b272-291">Once you have chosen the container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="8b272-292">В данном случае щелкните значок "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="8b272-292">For this scenario, click the save icon.</span></span>
   
    ![рисунок 61][image61]
7. <span data-ttu-id="8b272-294">После сохранения вернитесь к колонке "Резервные копии".</span><span class="sxs-lookup"><span data-stu-id="8b272-294">After saving, scroll back to the blade on the left for Backups.</span></span> <span data-ttu-id="8b272-295">Чтобы создать резервную копию приложения, щелкните "Создать резервную копию".</span><span class="sxs-lookup"><span data-stu-id="8b272-295">Click Backup Now to back the application.</span></span>
   
    ![рисунок 62][image62]
8. <span data-ttu-id="8b272-297">Через несколько секунд появится созданная резервная копия.</span><span class="sxs-lookup"><span data-stu-id="8b272-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="8b272-298">Обратите внимание на параметр "Восстановить сейчас" на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="8b272-298">Notice the Restore Now option on the screen-shot below.</span></span>
   
    ![рисунок 63][image63]
9. <span data-ttu-id="8b272-300">Щелкните "Восстановить сейчас" и просмотрите параметры в колонке справа.</span><span class="sxs-lookup"><span data-stu-id="8b272-300">Click on Restore Now and examine the options to the blade on the right.</span></span> <span data-ttu-id="8b272-301">При необходимости можно выбрать соответствующую резервную копию и легко восстановить ее до необходимого состояния.</span><span class="sxs-lookup"><span data-stu-id="8b272-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span></span> <span data-ttu-id="8b272-302">Таким образом, мы с легкостью реализовали простую стратегию аварийного восстановления для приложения на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8b272-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span></span>
   
    ![рисунок 64][image64]
10. <span data-ttu-id="8b272-304">Вернитесь к колонке "Параметры" слева и в категории "Возможности" выберите "Аутентификация или авторизация".</span><span class="sxs-lookup"><span data-stu-id="8b272-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![рисунок 65][image65]
11. <span data-ttu-id="8b272-306">В колонке справа выберите "Проверка подлинности службы приложений".</span><span class="sxs-lookup"><span data-stu-id="8b272-306">In the blade on the right choose App Service Authentication.</span></span> <span data-ttu-id="8b272-307">Обратите внимание на различные параметры, которые можно настроить с помощью популярных поставщиков.</span><span class="sxs-lookup"><span data-stu-id="8b272-307">Notice the variety of options you can configure with popular providers.</span></span>
    
     ![рисунок 66][image66]
12. <span data-ttu-id="8b272-309">Выберите необходимого поставщика и просмотрите параметры, которые можно для него настроить.</span><span class="sxs-lookup"><span data-stu-id="8b272-309">Choose the provider of your choice and notice the options for the scope.</span></span> <span data-ttu-id="8b272-310">Указав идентификатор и секрет для приложения, можно быстро активировать проверку подлинности для него в Facebook.</span><span class="sxs-lookup"><span data-stu-id="8b272-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span></span> <span data-ttu-id="8b272-311">Портал Azure предоставляет готовое решение для проверки подлинности приложений.</span><span class="sxs-lookup"><span data-stu-id="8b272-311">The Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![рисунок 67][image67]
13. <span data-ttu-id="8b272-313">Вернитесь к колонке "Параметры" и в категории "Управление ресурсами" выберите "Пользователи".</span><span class="sxs-lookup"><span data-stu-id="8b272-313">Move back to the Settings blade and choose Users under the Resource Management category.</span></span>
    
     ![рисунок 68][image68]
14. <span data-ttu-id="8b272-315">В колонке справа просмотрите различные варианты добавления ролей и пользователей.</span><span class="sxs-lookup"><span data-stu-id="8b272-315">In the blade on the right examine the various options for adding roles and users.</span></span> <span data-ttu-id="8b272-316">Портал Azure позволяет легко управлять доступом на основе ролей к приложению.</span><span class="sxs-lookup"><span data-stu-id="8b272-316">The Azure Portal lets you easily control RBAC (Role-based access control) for the application.</span></span>
    
     ![рисунок 69][image69]

## <a name="summary"></a><span data-ttu-id="8b272-318">Сводка</span><span class="sxs-lookup"><span data-stu-id="8b272-318">Summary</span></span>
<span data-ttu-id="8b272-319">В этом руководстве содержатся сведения о некоторых возможностях платформы Azure, которые позволяют быстро включать непрерывное развертывание, выполнять разработку, тестирование, мониторинг и устранение неполадок приложений, а также управлять основными стратегиями, такими как аварийное восстановление, управление удостоверениями и доступом на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="8b272-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="8b272-320">Платформа Azure поддерживает рабочие процессы DevOps, что позволяет эффективно выполнять различные задачи непосредственно на портале.</span><span class="sxs-lookup"><span data-stu-id="8b272-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b272-321">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b272-321">Next steps</span></span>
* <span data-ttu-id="8b272-322">Чтобы включить рабочие процессы DevOps на платформе Azure, требуется Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b272-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span></span>  <span data-ttu-id="8b272-323">Дополнительные сведения см. в [обзоре Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b272-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="8b272-324">См. дополнительные сведения о [развертывании приложений в службе приложений Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8b272-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md)</span></span>

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
