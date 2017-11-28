---
title: "Развертывание в режиме фокус-тестирования (бета-тестирование) в службе приложений Azure"
description: "Из этого учебника вы узнаете, как выполнять фокус-тестирование новых функций в приложении или бета-тестирование обновлений. Этот режим тестирования объединяет такие функции службы приложений, как непрерывная публикация, управление слотами, маршрутизация трафика и интеграция с Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: 83e3247310461ac148fff3c4ade3aa7216478537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="977bb-104">Развертывание в режиме фокус-тестирования (бета-тестирование) в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="977bb-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="977bb-105">В этом учебнике показано, как выполнить *развертывание для фокус-тестирования*, интегрируя различные возможности [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) и [Azure Application Insights](/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="977bb-105">This tutorial shows you how to do *flighting deployments* by integrating the various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="977bb-106">*Фокус-тестирование* — это процесс развертывания, в ходе которого выполняется проверка новой функции или внесенного изменения с привлечением ограниченного количества реальных клиентов. В рабочих сценариях это основной режим тестирования.</span><span class="sxs-lookup"><span data-stu-id="977bb-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="977bb-107">Он аналогичен режиму бета-тестирования и иногда называется управляемым фокус-тестированием.</span><span class="sxs-lookup"><span data-stu-id="977bb-107">It is akin to beta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="977bb-108">Многие крупные предприятия, обозначившие свое веб-присутствие, используют этот подход для выполнения ранней проверки обновлений своих приложений в рамках методологии [гибкой разработки](https://en.wikipedia.org/wiki/Agile_software_development).</span><span class="sxs-lookup"><span data-stu-id="977bb-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="977bb-109">Служба приложений Azure позволяет включить тестирование в рабочую среду с непрерывной публикацией, а служба Application Insights — реализацию того же сценария DevOps.</span><span class="sxs-lookup"><span data-stu-id="977bb-109">Azure App Service enables you to integrate test in production with continous publishing and Application Insights to implement the same DevOps scenario.</span></span> <span data-ttu-id="977bb-110">Этот подход отличается следующими преимуществами.</span><span class="sxs-lookup"><span data-stu-id="977bb-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="977bb-111">**Получение реальных данных *перед* выпуском обновлений в рабочей среде**. Разумеется, вы можете получить отклик сразу же после выпуска продукта. Но будет лучше, если это произойдет до выпуска.</span><span class="sxs-lookup"><span data-stu-id="977bb-111">**Gain real feedback *before* updates are released to production** - The only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="977bb-112">Вы можете тестировать обновления с привлечением текущего пользовательского трафика и на основе поведения пользователей на любом (даже самом раннем) этапе жизненного цикла продукта.</span><span class="sxs-lookup"><span data-stu-id="977bb-112">You can test updates with real user traffic and behaviors as early as you desire in the product life cycle.</span></span>
* <span data-ttu-id="977bb-113">**Оптимизация [непрерывной разработки на основе тестирования (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**. Непрерывная интеграция в рабочую среду процессов тестирования и инструментирования средствами Application Insights делает возможным раннюю автоматическую проверку с привлечением пользователей, выполняемую на требуемом этапе жизненного цикла продукта.</span><span class="sxs-lookup"><span data-stu-id="977bb-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="977bb-114">Это помогает сократить временные затраты при выполнении тестирования вручную.</span><span class="sxs-lookup"><span data-stu-id="977bb-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="977bb-115">**Оптимизация процесса тестирования**. Автоматизация тестирования в рабочей среде методом непрерывного наблюдательного инструментирования позволяет с высокой долей вероятности решить задачи, которые ставятся перед разными типами тестирования, в рамках единого процесса. Эти задачи включают в себя тестирование [интеграции](https://en.wikipedia.org/wiki/Integration_testing), [регрессии](https://en.wikipedia.org/wiki/Regression_testing), [удобства использования](https://en.wikipedia.org/wiki/Usability_testing), доступности, локализации, [производительности](https://en.wikipedia.org/wiki/Software_performance_testing), [безопасности](https://en.wikipedia.org/wiki/Security_testing) и [приемки](https://en.wikipedia.org/wiki/Acceptance_testing).</span><span class="sxs-lookup"><span data-stu-id="977bb-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish the goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="977bb-116">Развертывание в режиме фокус-тестирования используется не только для маршрутизации текущего трафика.</span><span class="sxs-lookup"><span data-stu-id="977bb-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="977bb-117">При таком развертывании предполагается максимально быстрое получение информации, включая сведения о непредвиденной ошибке, снижении производительности или проблемах взаимодействия с пользователями.</span><span class="sxs-lookup"><span data-stu-id="977bb-117">In such a deployment you want to gain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="977bb-118">Помните: вы имеете дело с реальными пользователями.</span><span class="sxs-lookup"><span data-stu-id="977bb-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="977bb-119">И чтобы все сделать правильно, убедитесь, что вы настроили параметры фокус-тестирования для сбора всех данных, необходимых для принятия обоснованного решения перед выполнением следующего шага.</span><span class="sxs-lookup"><span data-stu-id="977bb-119">So to do it right, you must make sure that you have set up your flighting deployment to gather all the data you need in order to make an informed decision for your next step.</span></span> <span data-ttu-id="977bb-120">В этом учебнике показано, как собирать данные с помощью Application Insights. Кроме того, вы можете использовать средство New Relic или другие подходящие вам технологии.</span><span class="sxs-lookup"><span data-stu-id="977bb-120">This tutorial shows you how to collect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="977bb-121">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="977bb-121">What you will do</span></span>
<span data-ttu-id="977bb-122">Из этого учебника вы узнаете, как использовать следующие сценарии для тестирования приложения службы приложений в рабочей среде:</span><span class="sxs-lookup"><span data-stu-id="977bb-122">In this tutorial, you will learn how to bring the following scenarios together to test your App Service app in production:</span></span>

* <span data-ttu-id="977bb-123">[Маршрутизация рабочего трафика](app-service-web-test-in-production-get-start.md) в бета-версию приложения.</span><span class="sxs-lookup"><span data-stu-id="977bb-123">[Route production traffic](app-service-web-test-in-production-get-start.md) to your beta app</span></span>
* <span data-ttu-id="977bb-124">[Инструментирование приложения](../application-insights/app-insights-web-track-usage.md) для получения полезных метрик.</span><span class="sxs-lookup"><span data-stu-id="977bb-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) to obtain useful metrics</span></span>
* <span data-ttu-id="977bb-125">Непрерывное развертывание бета-версии приложения с отслеживанием метрик в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="977bb-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="977bb-126">Сравнение метрик рабочего приложения и бета-версии приложения для оценки того, как изменения кода преобразуются в результаты.</span><span class="sxs-lookup"><span data-stu-id="977bb-126">Compare metrics between the production app and the beta app to see how code changes translate to results</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="977bb-127">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="977bb-127">What you will need</span></span>
* <span data-ttu-id="977bb-128">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="977bb-128">An Azure account</span></span>
* <span data-ttu-id="977bb-129">Учетная запись [GitHub](https://github.com/) .</span><span class="sxs-lookup"><span data-stu-id="977bb-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="977bb-130">Visual Studio 2015 — вы можете скачать выпуск [Community Edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="977bb-130">Visual Studio 2015 - you can download the [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="977bb-131">Оболочка Git Shell (устанавливается вместе с [GitHub для Windows](https://windows.github.com/)) — позволяет запускать команды PowerShell и Git в рамках одного сеанса.</span><span class="sxs-lookup"><span data-stu-id="977bb-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you to run both the Git and PowerShell commands in the same session</span></span>
* <span data-ttu-id="977bb-132">Последняя версия [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) .</span><span class="sxs-lookup"><span data-stu-id="977bb-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="977bb-133">Базовые знания таких компонентов.</span><span class="sxs-lookup"><span data-stu-id="977bb-133">Basic understanding of the following:</span></span>
  * <span data-ttu-id="977bb-134">Развертывание шаблона [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (ознакомьтесь также с разделом [Предсказуемое развертывание сложного приложения в Azure](app-service-deploy-complex-application-predictably.md)).</span><span class="sxs-lookup"><span data-stu-id="977bb-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="977bb-135">Git.</span><span class="sxs-lookup"><span data-stu-id="977bb-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="977bb-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="977bb-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="977bb-137">Для работы с этим учебником требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="977bb-137">You need an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="977bb-138">Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/) — вы получаете кредиты, которые можно использовать для опробования платных служб Azure, и даже после израсходования кредитов вы сохраняете учетную запись и возможность использовать бесплатные службы Azure, такие как веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="977bb-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="977bb-139">Вы можете [активировать преимущества подписчика Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) — каждый месяц ваша подписка Visual Studio предоставляет вам кредиты, которые можно использовать для оплаты служб Azure.</span><span class="sxs-lookup"><span data-stu-id="977bb-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="977bb-140">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="977bb-140">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="977bb-141">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="977bb-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="977bb-142">Настройка рабочего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="977bb-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="977bb-143">Сценарий, используемый в этом учебнике, автоматически настроит непрерывную публикацию из репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="977bb-143">The script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="977bb-144">Для этого необходимо, чтобы учетные данные GitHub уже хранились в Azure. Иначе при попытке настроить параметры системы управления версиями для веб-приложений произойдет сбой развертывания, заложенного в сценарий.</span><span class="sxs-lookup"><span data-stu-id="977bb-144">This requires that your GitHub credentials are already stored in Azure, otherwise the scripted deployment will fail when attempting to configure source control settings for the web apps.</span></span>
>
> <span data-ttu-id="977bb-145">Чтобы сохранить учетные данные GitHub в Azure, создайте веб-приложение на [портале Azure](https://portal.azure.com/) и [настройте развертывание GitHub](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="977bb-145">To store your GitHub credentials in Azure, create a web app in the [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="977bb-146">Это нужно сделать только один раз.</span><span class="sxs-lookup"><span data-stu-id="977bb-146">You only need to do this once.</span></span>
>
>

<span data-ttu-id="977bb-147">В типичном сценарии DevOps у вас есть приложение, которое работает в Azure, и вам нужно внести в него изменения с помощью непрерывной публикации.</span><span class="sxs-lookup"><span data-stu-id="977bb-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want to make changes to it through continuous publishing.</span></span> <span data-ttu-id="977bb-148">В этом сценарии вам нужно будет развернуть в рабочей среде разработанный и протестированный шаблон.</span><span class="sxs-lookup"><span data-stu-id="977bb-148">In this scenario, you will deploy to production a template that you have developed and tested.</span></span>

1. <span data-ttu-id="977bb-149">Создайте разветвление в репозитории [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp).</span><span class="sxs-lookup"><span data-stu-id="977bb-149">Create your own fork of the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="977bb-150">Дополнительные сведения о создании разветвления см. в статье [Fork a Repo](https://help.github.com/articles/fork-a-repo/) (Разветвление репозитория).</span><span class="sxs-lookup"><span data-stu-id="977bb-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="977bb-151">После создания разветвления его можно просматривать в браузере.</span><span class="sxs-lookup"><span data-stu-id="977bb-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="977bb-152">Откройте сеанс Git Shell.</span><span class="sxs-lookup"><span data-stu-id="977bb-152">Open a Git Shell session.</span></span> <span data-ttu-id="977bb-153">Если у вас нет Git Shell, установите [GitHub для Windows](https://windows.github.com/) .</span><span class="sxs-lookup"><span data-stu-id="977bb-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="977bb-154">Создайте локальный клон разветвления, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="977bb-154">Create a local clone of your fork by executing the following command:</span></span>

     <span data-ttu-id="977bb-155">git clone https://github.com/<разветвление>/ToDoApp.git</span><span class="sxs-lookup"><span data-stu-id="977bb-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="977bb-156">Создав локальный клон, перейдите в каталог *&lt;корень_репозитория>*\ARMTemplates и запустите сценарий deploy.ps1 с уникальным суффиксом, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="977bb-156">Once you have your local clone, navigate to *&lt;repository_root>*\ARMTemplates, and run the deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="977bb-157">.\deploy.ps1 –RepoUrl https://github.com/<разветвление>/todoapp.git -ResourceGroupSuffix <суффикс></span><span class="sxs-lookup"><span data-stu-id="977bb-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="977bb-158">При появлении запроса введите желаемое имя пользователя и пароль для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="977bb-158">When prompted, type in the desired username and password for database access.</span></span> <span data-ttu-id="977bb-159">Запомните учетные данные базы данных, так как вам нужно будет еще раз указать их при обновлении группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="977bb-159">Remember your database credentials because you will need to specify them again when updating the resource group.</span></span>

   <span data-ttu-id="977bb-160">Вы увидите ход подготовки различных ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="977bb-160">You should see the provisioning progress of various Azure resources.</span></span> <span data-ttu-id="977bb-161">После завершения развертывания скрипт запустит приложение в браузере и сообщит вам об этом с помощью звукового сигнала.</span><span class="sxs-lookup"><span data-stu-id="977bb-161">When deployment completes, the script will launch the application in the browser and give you a friendly beep.</span></span>
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="977bb-162">Вернитесь в сеанс Git Shell и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="977bb-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="977bb-163">.\swap –Name ToDoApp<суффикс></span><span class="sxs-lookup"><span data-stu-id="977bb-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="977bb-164">После выполнения сценария вернитесь назад и перейдите по адресу внешнего интерфейса (http://ToDoApp*&lt;ваш_суффикс>*master.azurewebsites.net/), чтобы посмотреть на работу приложения в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="977bb-164">When the script finishes, go back to browse to the frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) to see the application running in production.</span></span>
8. <span data-ttu-id="977bb-165">Перейдите на [портале Azure](https://portal.azure.com/) и посмотрите на результаты.</span><span class="sxs-lookup"><span data-stu-id="977bb-165">Log into the [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="977bb-166">Вы увидите два веб-приложения в одной группе ресурсов. Имя одного из них будет содержать суффикс `Api`.</span><span class="sxs-lookup"><span data-stu-id="977bb-166">You should be able to see two web apps in the same resource group, one with the `Api` suffix in the name.</span></span> <span data-ttu-id="977bb-167">Если вы посмотрите на представление группы ресурсов, вы также увидите базу данных SQL и сервер, план службы приложений и промежуточные слоты для веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="977bb-167">If you look at the resource group view, you will also see the SQL Database and server, the App Service plan, and the staging slots for the web apps.</span></span> <span data-ttu-id="977bb-168">Просмотрите различные ресурсы и сравните их с файлом *&lt;repository_root>*\ARMTemplates\ProdAndStage.json, чтобы узнать, как они настроены в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="977bb-168">Browse through the different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json to see how they are configured in the template.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="977bb-169">Вы настроили рабочее приложение.</span><span class="sxs-lookup"><span data-stu-id="977bb-169">You have set up the production app.</span></span>  <span data-ttu-id="977bb-170">Теперь представим, что вы получили негативный отзыв об удобстве использования приложения.</span><span class="sxs-lookup"><span data-stu-id="977bb-170">Now, let's imagine that you receive feedback that usability is poor for the app.</span></span> <span data-ttu-id="977bb-171">Нужно разобраться, в чем проблема.</span><span class="sxs-lookup"><span data-stu-id="977bb-171">So you decide to investigate.</span></span> <span data-ttu-id="977bb-172">Вам нужно инструментировать приложение, чтобы узнать, в чем дело.</span><span class="sxs-lookup"><span data-stu-id="977bb-172">You're going to instrument your app to give you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="977bb-173">Анализ: инструментирование клиентского приложения для мониторинга метрик</span><span class="sxs-lookup"><span data-stu-id="977bb-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="977bb-174">Откройте в Visual Studio файл *&lt;корень_репозитория>*\src\MultiChannelToDo.sln.</span><span class="sxs-lookup"><span data-stu-id="977bb-174">Open *&lt;repository_root>*\src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="977bb-175">Восстановите все пакеты NuGet, щелкнув правой кнопкой мыши нужное решение и выбрав **Управление пакетами NuGet для решения** > **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="977bb-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="977bb-176">Щелкните правой кнопкой мыши **MultiChannelToDo** и выберите >  **Добавить телеметрию Application Insights** > **Настройка параметров**. После этого измените группу ресурсов на ToDoApp*&lt;ваш_суффикс>* и щелкните >  **Добавить Application Insights в проект**.</span><span class="sxs-lookup"><span data-stu-id="977bb-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
4. <span data-ttu-id="977bb-177">На портале Azure откройте колонку для ресурса Application Insight **MultiChannelToDo.Web** .</span><span class="sxs-lookup"><span data-stu-id="977bb-177">In the Azure Portal, open the blade for the **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="977bb-178">Затем в части **Работоспособность приложения** щелкните **Дополнительные сведения о сборе данных о загрузке страниц браузера** и скопируйте код.</span><span class="sxs-lookup"><span data-stu-id="977bb-178">Then in the **Application health** part, click **Learn how to collect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="977bb-179">Добавьте скопированный код инструментирования JS в файл *&lt;корень_репозитория>*\src\MultiChannelToDo.Web\app\Index.cshtml непосредственно перед закрывающим тегом `<heading>`.</span><span class="sxs-lookup"><span data-stu-id="977bb-179">Add the copied JS instrumentation code to *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, just before the closing `<heading>` tag.</span></span> <span data-ttu-id="977bb-180">Он должен содержать уникальный ключ инструментирования вашего ресурса Application Insight.</span><span class="sxs-lookup"><span data-stu-id="977bb-180">It should contain the unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="977bb-181">Настройте отправку пользовательских событий щелчка мыши в Application Insights, добавив следующий код в конец блока:</span><span class="sxs-lookup"><span data-stu-id="977bb-181">Send custom events to Application Insights for mouse clicks by adding the following code to the bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="977bb-182">Этот фрагмент кода JavaScript отправляет пользовательское событие в Application Insights каждый раз, когда пользователь щелкает в любом месте веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="977bb-182">This JavaScript snippet sends a custom event to Application Insights every time a user clicks anywhere in the web app.</span></span>
7. <span data-ttu-id="977bb-183">В Git Shell зафиксируйте и отправьте внесенные изменения в разветвление GitHub.</span><span class="sxs-lookup"><span data-stu-id="977bb-183">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="977bb-184">Дождитесь, пока клиенты обновят браузер.</span><span class="sxs-lookup"><span data-stu-id="977bb-184">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="977bb-185">Перенесите изменения, внесенные в развернутое приложение, в рабочую среду:</span><span class="sxs-lookup"><span data-stu-id="977bb-185">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="977bb-186">.\swap –Name ToDoApp<суффикс></span><span class="sxs-lookup"><span data-stu-id="977bb-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="977bb-187">Перейдите к настроенному ресурсу Application Insights.</span><span class="sxs-lookup"><span data-stu-id="977bb-187">Browse to the Application Insights resource that you configured.</span></span> <span data-ttu-id="977bb-188">Щелкните «Настраиваемые события».</span><span class="sxs-lookup"><span data-stu-id="977bb-188">Click Custom events.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="977bb-189">Если вы не видите метрик, характеризующих пользовательские события, подождите несколько минут и щелкните **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="977bb-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="977bb-190">Предположим, что вы видите диаграмму, похожую на представленную ниже:</span><span class="sxs-lookup"><span data-stu-id="977bb-190">Suppose you see a chart like below:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="977bb-191">Под этой диаграммой отображена сетка событий:</span><span class="sxs-lookup"><span data-stu-id="977bb-191">And the event grid below it:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="977bb-192">Согласно коду приложения ToDoApp событие **BUTTON** соответствует кнопке отправки, а событие **INPUT** — текстовому полю.</span><span class="sxs-lookup"><span data-stu-id="977bb-192">According to your ToDoApp application code, the **BUTTON** event corresponds to the submit button, and the **INPUT** event corresponds to the textbox.</span></span> <span data-ttu-id="977bb-193">С этим все понятно.</span><span class="sxs-lookup"><span data-stu-id="977bb-193">So far, things make sense.</span></span> <span data-ttu-id="977bb-194">Однако похоже на то, что из всего количества щелчков (а их довольно много) только некоторые относятся к элементам списка дел (события **LI** ).</span><span class="sxs-lookup"><span data-stu-id="977bb-194">However, it looks like there's a good amount of clicks and very few clicks on the to-do items (the **LI** events).</span></span>

<span data-ttu-id="977bb-195">На основе этого можно предположить, что некоторые пользователи не всегда могут определить, какие части пользовательского интерфейса являются интерактивными. Причина — при наведении на элементы списка и соответствующие значки курсор выглядит как средство для выделения текста.</span><span class="sxs-lookup"><span data-stu-id="977bb-195">Based on this, you form your hypothesis that some users are confused which part of the UI is clickable and it is because the cursor is styled for text selection when it hovers on the list items and their icons.</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="977bb-196">Этот пример может выглядеть несколько надуманным.</span><span class="sxs-lookup"><span data-stu-id="977bb-196">This might be a contrived example.</span></span> <span data-ttu-id="977bb-197">Тем не менее вам нужно улучшить приложение, а затем выполнить развертывание в режиме фокус-тестирования, чтобы получить отзывы реальных клиентов об удобстве использования.</span><span class="sxs-lookup"><span data-stu-id="977bb-197">Nevertheless, you're going to make an improvement to your app, and then perform a flighting deployment to get usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="977bb-198">Инструментирование серверного приложения для получения метрик и для мониторинга</span><span class="sxs-lookup"><span data-stu-id="977bb-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="977bb-199">Эта тема будет освещена вкратце, так как в описываемых в учебнике сценариях используется только клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="977bb-199">This is a tangent since the scenario demonstrated in this tutorial only deals with the client app.</span></span> <span data-ttu-id="977bb-200">Однако для полноты картины мы настроим также и серверное приложение.</span><span class="sxs-lookup"><span data-stu-id="977bb-200">However, for completeness you will set up the server-side app.</span></span>

1. <span data-ttu-id="977bb-201">Щелкните правой кнопкой мыши **MultiChannelToDo** и выберите >  **Добавить телеметрию Application Insights** > **Настройка параметров**. После этого измените группу ресурсов на ToDoApp*&lt;ваш_суффикс>* и щелкните >  **Добавить Application Insights в проект**.</span><span class="sxs-lookup"><span data-stu-id="977bb-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
2. <span data-ttu-id="977bb-202">В Git Shell зафиксируйте и отправьте внесенные изменения в разветвление GitHub.</span><span class="sxs-lookup"><span data-stu-id="977bb-202">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="977bb-203">Дождитесь, пока клиенты обновят браузер.</span><span class="sxs-lookup"><span data-stu-id="977bb-203">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="977bb-204">Перенесите изменения, внесенные в развернутое приложение, в рабочую среду:</span><span class="sxs-lookup"><span data-stu-id="977bb-204">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="977bb-205">.\swap –Name ToDoApp<суффикс></span><span class="sxs-lookup"><span data-stu-id="977bb-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="977bb-206">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="977bb-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-to-your-client-app-metrics"></a><span data-ttu-id="977bb-207">Анализ: добавление связанных со слотом тегов к метрикам клиентского приложения</span><span class="sxs-lookup"><span data-stu-id="977bb-207">Investigate: Add slot-specific tags to your client app metrics</span></span>
<span data-ttu-id="977bb-208">В этом разделе вы настроите разные слоты развертывания для отправки связанных со слотом данных телеметрии в один ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="977bb-208">In this section, you will configure the different deployment slots to send slot-specific telemetry to the same Application Insights resource.</span></span> <span data-ttu-id="977bb-209">Таким образом вы сможете сравнить данные телеметрии через призму трафика из разных слотов (сред развертывания), чтобы увидеть результат изменений, внесенных в приложение.</span><span class="sxs-lookup"><span data-stu-id="977bb-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) to easily see the effect of your app changes.</span></span> <span data-ttu-id="977bb-210">Кроме того, вы сможете отделить рабочий трафик от остального, при необходимости продолжая наблюдать за рабочим приложением.</span><span class="sxs-lookup"><span data-stu-id="977bb-210">At the same time, you can separate the production traffic from the rest so you can continue to monitor your production app as needed.</span></span>

<span data-ttu-id="977bb-211">Так как вы собираете данные о поведении клиента, вам нужно [добавить в код JavaScript инициализатор телеметрии](../application-insights/app-insights-api-filtering-sampling.md) в файле index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="977bb-211">Since you're gathering data on client behavior, you will [add a telemetry initializer to your JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="977bb-212">А чтобы выполнить тестирование производительности на стороне сервера, вы сможете выполнить эти же действия с серверным кодом (ознакомьтесь со статьей [API Application Insights для пользовательских событий и метрик](../application-insights/app-insights-api-custom-events-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="977bb-212">If you want to test server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="977bb-213">Во-первых, вставьте код между двумя комментариями `//` в блоке JavaScript ниже, который вы ранее добавили к тегу `<heading>`.</span><span class="sxs-lookup"><span data-stu-id="977bb-213">First, add the code bewteen the two `//` comments below in the JavaScript block that you added to the `<heading>` tag earlier.</span></span>

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    <span data-ttu-id="977bb-214">Этот код инициализатора вызывает объект `appInsights` для добавления пользовательского свойства с именем `Environment` ко всем отправляемым элементам телеметрии.</span><span class="sxs-lookup"><span data-stu-id="977bb-214">This initializer code causes the `appInsights` object to add the a custom property called `Environment` to every piece of telemetry it sends.</span></span>
2. <span data-ttu-id="977bb-215">Затем добавьте это пользовательское свойство как [параметр слота](web-sites-staged-publishing.md#AboutConfiguration) для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="977bb-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="977bb-216">Чтобы сделать это, выполните следующую команду в оболочке Git Shell.</span><span class="sxs-lookup"><span data-stu-id="977bb-216">To do this, run the following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="977bb-217">Файл Web.config в проекте уже определяет параметр `environment` приложения.</span><span class="sxs-lookup"><span data-stu-id="977bb-217">The Web.config in your project already defines the `environment` app setting.</span></span> <span data-ttu-id="977bb-218">С этим параметром при локальном тестировании приложения метрики будут помечаться как `VS Debugger`.</span><span class="sxs-lookup"><span data-stu-id="977bb-218">With this setting, when you test the app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="977bb-219">Однако, если изменения отправляются в Azure, вместо этого будет найден и использован параметр приложения `environment` в конфигурации веб-приложения, а метрики будут обозначены тегом `Production`.</span><span class="sxs-lookup"><span data-stu-id="977bb-219">However, when you push your changes to Azure, Azure will find and use the `environment` app setting in the web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="977bb-220">Зафиксируйте и отправьте изменения кода в разветвление на GitHub и подождите, пока пользователи начнут использовать новое приложение (необходимо обновить браузер).</span><span class="sxs-lookup"><span data-stu-id="977bb-220">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="977bb-221">Чтобы новое свойство отобразилось в ресурсе `MultiChannelToDo.Web` Application Insights, требуется около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="977bb-221">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for client app"
        git push origin master
4. <span data-ttu-id="977bb-222">Теперь снова перейдите к колонке **Пользовательские события** и отфильтруйте метрики по `Environment=Production`.</span><span class="sxs-lookup"><span data-stu-id="977bb-222">Now, go to the **Custom events** blade again and filter the metrics on `Environment=Production`.</span></span> <span data-ttu-id="977bb-223">Применив этот фильтр, вы сможете увидеть все новые пользовательские события в рабочем слоте.</span><span class="sxs-lookup"><span data-stu-id="977bb-223">You should now be able to see all the new custom events in the production slot with this filter.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="977bb-224">Нажмите кнопку **Избранное**, чтобы сохранить текущие параметры обозревателя метрик с именем наподобие **Пользовательские события: рабочая среда**.</span><span class="sxs-lookup"><span data-stu-id="977bb-224">Click the **Favorites** button to save the current Metrics Explorer settings to something like **Custom events: Production**.</span></span> <span data-ttu-id="977bb-225">Позже вы сможете легко переключаться между этим представлением и представлением слота развертывания.</span><span class="sxs-lookup"><span data-stu-id="977bb-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="977bb-226">Если вам нужны более мощные средства аналитики, рассмотрите возможность [интеграции ресурса Application Insights с Power BI](../application-insights/app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="977bb-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-to-your-server-app-metrics"></a><span data-ttu-id="977bb-227">Добавление связанных со слотом тегов к метрикам серверного приложения</span><span class="sxs-lookup"><span data-stu-id="977bb-227">Add slot-specific tags to your server app metrics</span></span>
<span data-ttu-id="977bb-228">Снова-таки, для полноты картины мы настроим также серверное приложение.</span><span class="sxs-lookup"><span data-stu-id="977bb-228">Again, for completeness you will set up the server-side app.</span></span> <span data-ttu-id="977bb-229">В отличие от клиентского приложения, которое инструментируется в JavaScript, связанные со слотом теги для серверного приложения инструментируются с помощью кода .NET.</span><span class="sxs-lookup"><span data-stu-id="977bb-229">Unlike the client app which is instrumented in JavaScript, slot-specific tags for the server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="977bb-230">Откройте файл *&lt;корень_репозитория>*\src\MultiChannelToDo\Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="977bb-230">Open *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="977bb-231">Вставьте следующий блок кода непосредственно перед закрывающей фигурной скобкой пространства имен.</span><span class="sxs-lookup"><span data-stu-id="977bb-231">Add the code block below, just before the closing namespace curly brace.</span></span>

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. <span data-ttu-id="977bb-232">Исправьте ошибки разрешения имен, добавив следующие инструкции `using` в начало файла:</span><span class="sxs-lookup"><span data-stu-id="977bb-232">Correct the name resolution errors by adding the `using` statements below to the beginning of the file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="977bb-233">Добавьте следующий код в начало метода `Application_Start()` :</span><span class="sxs-lookup"><span data-stu-id="977bb-233">Add the code below to the beginning of the `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="977bb-234">Зафиксируйте и отправьте изменения кода в разветвление на GitHub и подождите, пока пользователи начнут использовать новое приложение (необходимо обновить браузер).</span><span class="sxs-lookup"><span data-stu-id="977bb-234">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="977bb-235">Чтобы новое свойство отобразилось в ресурсе `MultiChannelToDo` Application Insights, требуется около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="977bb-235">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="977bb-236">Обновление: настройка ветви бета-версии</span><span class="sxs-lookup"><span data-stu-id="977bb-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="977bb-237">Откройте файл *&lt;корень_репозитория>*\ARMTemplates\ProdAndStagetest.json и найдите ресурсы `appsettings` (выполните поиск `"name": "appsettings"`).</span><span class="sxs-lookup"><span data-stu-id="977bb-237">Open *&lt;repository_root>*\ARMTemplates\ProdAndStagetest.json and find the `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="977bb-238">Существует 4 таких ресурса, по одному для каждого слота.</span><span class="sxs-lookup"><span data-stu-id="977bb-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="977bb-239">Для каждого ресурса `appsettings` добавьте параметр приложения `"environment": "[parameters('slotName')]"` в конец массива `properties`.</span><span class="sxs-lookup"><span data-stu-id="977bb-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting to the end of the `properties` array.</span></span> <span data-ttu-id="977bb-240">Не забудьте завершить предыдущую строку запятой.</span><span class="sxs-lookup"><span data-stu-id="977bb-240">Don't forget to end the previous line with a comma.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="977bb-241">Вы только что добавили параметр приложения `environment` для всех слотов в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="977bb-241">You have just added the `environment` app setting to all the slots in the template.</span></span>
3. <span data-ttu-id="977bb-242">В этом же файле найдите ресурсы `slotconfignames` (выполните поиск `"name": "slotconfignames"`).</span><span class="sxs-lookup"><span data-stu-id="977bb-242">In the same file, find the `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="977bb-243">Существует 2 таких ресурса, по одному для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="977bb-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="977bb-244">Для каждого ресурса `slotconfignames` добавьте `"environment"` в конец массива `appSettingNames`.</span><span class="sxs-lookup"><span data-stu-id="977bb-244">For each `slotconfignames` resource, add `"environment"` to the end of the `appSettingNames` array.</span></span> <span data-ttu-id="977bb-245">Не забудьте завершить предыдущую строку запятой.</span><span class="sxs-lookup"><span data-stu-id="977bb-245">Don't forget to end the previous line with a comma.</span></span>

    <span data-ttu-id="977bb-246">Вы только что связали параметр приложения `environment` с соответствующим слотом развертывания для двух приложений.</span><span class="sxs-lookup"><span data-stu-id="977bb-246">You have just made the `environment` app setting stick to its respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="977bb-247">В сеансе Git Shell выполните следующие команды с тем же суффиксом группы ресурсов, который вы использовали ранее.</span><span class="sxs-lookup"><span data-stu-id="977bb-247">In your Git Shell session, run the following commands with the same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="977bb-248">При появлении запроса укажите учетные данные базы данных SQL, как и ранее.</span><span class="sxs-lookup"><span data-stu-id="977bb-248">When prompted, specify the same SQL database credentials as before.</span></span> <span data-ttu-id="977bb-249">Затем при появлении запроса на обновление группы ресурсов введите `Y` и `ENTER`.</span><span class="sxs-lookup"><span data-stu-id="977bb-249">Then, when asked to update the resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="977bb-250">После завершения скрипта все ресурсы в исходной группе ресурсов будут сохранены. При этом в ней будет создан новый слот с именем beta с такой же конфигурацией, как и у промежуточного слота, который был создан в начале.</span><span class="sxs-lookup"><span data-stu-id="977bb-250">Once the script finishes, all your resources in the original resource group are retained, but a new slot named "beta" is created in it with the same configuration as the "Staging" slot that was created in the beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="977bb-251">Этот метод создания разных сред развертывания отличается от метода [гибкой разработки программного обеспечения с помощью службы приложений Azure](app-service-agile-software-development.md).</span><span class="sxs-lookup"><span data-stu-id="977bb-251">This method of creating different deployment environments is different from the method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="977bb-252">Он предполагает создание сред развертывания со слотами развертывания — как если бы вы создавали среды развертывания с группами ресурсов.</span><span class="sxs-lookup"><span data-stu-id="977bb-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="977bb-253">Управление средами развертывания с помощью групп ресурсов среды ограничивает доступ к рабочей среде для разработчиков. И хотя выполнять тестирование в рабочей среде сложно, вы можете легко решить эту задачу с помощью слотов.</span><span class="sxs-lookup"><span data-stu-id="977bb-253">Managing deployment environments with resource groups enables you to keep the production environment off-limits to developers, but it's not easy to do testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="977bb-254">При желании вы можете создать альфа-версию приложения, запустив следующий код:</span><span class="sxs-lookup"><span data-stu-id="977bb-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="977bb-255">Этот учебник предполагает использование бета-версии приложения.</span><span class="sxs-lookup"><span data-stu-id="977bb-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-to-the-beta-app"></a><span data-ttu-id="977bb-256">Обновление: отправка обновлений в бета-версию приложения</span><span class="sxs-lookup"><span data-stu-id="977bb-256">Update: Push your updates to the beta app</span></span>
<span data-ttu-id="977bb-257">Перейдите к приложению, которое нужно улучшить.</span><span class="sxs-lookup"><span data-stu-id="977bb-257">Back to your app that you want to improve.</span></span>

1. <span data-ttu-id="977bb-258">Убедитесь, что вы находитесь в ветке бета-версии.</span><span class="sxs-lookup"><span data-stu-id="977bb-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="977bb-259">В файле *&lt;корень_репозитория>*\src\MultiChannelToDo.Web\app\Index.cshtml найдите тег `<li>` и добавьте атрибут `style="cursor:pointer"`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="977bb-259">In *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, find the `<li>` tag and add the `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="977bb-260">Зафиксируйте изменение и отправьте его в Azure.</span><span class="sxs-lookup"><span data-stu-id="977bb-260">commit and push to Azure.</span></span>
4. <span data-ttu-id="977bb-261">Убедитесь, что изменение теперь отображается в слоте бета-версии, перейдя по адресу http://todoapp*&lt;ваш_суффикс>*-beta.azurewebsites.net/.</span><span class="sxs-lookup"><span data-stu-id="977bb-261">Verify that the change is now reflected in the beta slot by navigating to http://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="977bb-262">Если изменение еще не отображается, обновите браузер для получения нового кода javascript.</span><span class="sxs-lookup"><span data-stu-id="977bb-262">If you don't see the change yet, refresh your browser to get the new javascript code.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="977bb-263">Теперь, когда изменение в слоте бета-версии запущено, можно выполнить развертывание в режиме фокус-тестирования.</span><span class="sxs-lookup"><span data-stu-id="977bb-263">Now that you have your change running in the beta slot, you are ready to perform a flighting deployment.</span></span>

## <a name="validate-route-traffic-to-the-beta-app"></a><span data-ttu-id="977bb-264">Проверка: маршрутизация трафика в бета-версию приложения</span><span class="sxs-lookup"><span data-stu-id="977bb-264">Validate: Route traffic to the beta app</span></span>
<span data-ttu-id="977bb-265">В этом разделе будет выполнена маршрутизация трафика в бета-версию приложения.</span><span class="sxs-lookup"><span data-stu-id="977bb-265">In this section, you will route traffic to the beta app.</span></span> <span data-ttu-id="977bb-266">Для наглядности вы выполните маршрутизацию значительной части пользовательского трафика.</span><span class="sxs-lookup"><span data-stu-id="977bb-266">For sake of clarity of demonstration, you're going to route a significant portion of the user traffic to it.</span></span> <span data-ttu-id="977bb-267">В реальности объем перенаправляемого трафика будет зависеть от конкретной ситуации.</span><span class="sxs-lookup"><span data-stu-id="977bb-267">In reality, the amount of traffic you want to route will depend on your specific situation.</span></span> <span data-ttu-id="977bb-268">Например, если у вас сайт масштаба microsoft.com, для получения полезных данных вам потребуется менее 1 % от всего трафика.</span><span class="sxs-lookup"><span data-stu-id="977bb-268">For example, if your site is at the scale of microsoft.com, then you may need less than one percent of your total traffic in order to gain useful data.</span></span>

1. <span data-ttu-id="977bb-269">В сеансе Git Shell выполните следующие команды для маршрутизации половины рабочего трафика в слот бета-версии:</span><span class="sxs-lookup"><span data-stu-id="977bb-269">In your Git Shell session, run the following commands to route half of the production traffic to the beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="977bb-270">Свойство `ReroutePercentage=50` указывает на то, что 50 % рабочего трафика будет перенаправлено на URL-адрес бета-версии приложения (определяется свойством `ActionHostName`).</span><span class="sxs-lookup"><span data-stu-id="977bb-270">The `ReroutePercentage=50` property specifies that 50% of the production traffic will be routed to the beta app's URL (specified by the `ActionHostName` property).</span></span>
2. <span data-ttu-id="977bb-271">Теперь перейдите по адресу http://ToDoApp*&lt;ваш-суффикс>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="977bb-271">Now navigate to http://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="977bb-272">50 % трафика теперь будет перенаправляться в слот бета-версии.</span><span class="sxs-lookup"><span data-stu-id="977bb-272">50% of the traffic should now be redirected to the beta slot.</span></span>
3. <span data-ttu-id="977bb-273">В ресурсе Application Insights примените к метрикам следующий фильтр: environment="beta".</span><span class="sxs-lookup"><span data-stu-id="977bb-273">In your Application Insights resource, filter the metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="977bb-274">Сохранив это отфильтрованное представление в избранном, вы сможете легко переключаться в обозревателе метрик между представлением рабочей версии и бета-версии.</span><span class="sxs-lookup"><span data-stu-id="977bb-274">If you save this filtered view as another favorite, then you can easily flip the metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="977bb-275">Предположим, что в Application Insights вы увидите что-то подобное:</span><span class="sxs-lookup"><span data-stu-id="977bb-275">Suppose in Application Insights you see something similar to the following:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="977bb-276">Эти значения демонстрируют не просто небольшое увеличение количества щелчков тегов `<li>`, но и резкий подъем активности в отношении тега `<li>`.</span><span class="sxs-lookup"><span data-stu-id="977bb-276">Not only is this showing that there are many more clicks on the `<li>` tags, but there seems to be a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="977bb-277">Из этого можно заключить, что пользователи обнаружили новые интерактивные теги `<li>` и теперь обозначают все ранее завершенные задачи в приложении как выполненные.</span><span class="sxs-lookup"><span data-stu-id="977bb-277">You can then conclude that people have discovered the new `<li>` tags are clickable and are now clearing all their previously-completed tasks in the app.</span></span>

<span data-ttu-id="977bb-278">На основе данных развертывания в режиме фокус-тестирования вы можете решить, что новый пользовательский интерфейс готов к выпуску.</span><span class="sxs-lookup"><span data-stu-id="977bb-278">Based on the data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="977bb-279">Ввод в эксплуатацию: перенос нового кода в рабочую среду</span><span class="sxs-lookup"><span data-stu-id="977bb-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="977bb-280">Теперь вы готовы применить обновления в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="977bb-280">You're now ready to move your update to production.</span></span> <span data-ttu-id="977bb-281">У вас есть преимущество — вы уже знаете, что обновление проверено *перед* отправкой в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="977bb-281">What's great is that now you know that your update has already been validated *before* it is pushed to production.</span></span> <span data-ttu-id="977bb-282">Теперь его можно с уверенностью развернуть.</span><span class="sxs-lookup"><span data-stu-id="977bb-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="977bb-283">После внесения обновления в клиентское приложение AngularJS вам остается только проверить код на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="977bb-283">Since you made an update to the AngularJS client app, you only validated the client-side code.</span></span> <span data-ttu-id="977bb-284">Если вы внесли изменения во внутреннее приложение веб-API, эти изменения вы сможете проверить так же легко и просто.</span><span class="sxs-lookup"><span data-stu-id="977bb-284">If you were to make changes to the back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="977bb-285">В оболочке Git Shell удалите правило маршрутизации трафика, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="977bb-285">In Git Shell, remove the traffic routing rule by running the following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="977bb-286">Выполните команды Git:</span><span class="sxs-lookup"><span data-stu-id="977bb-286">Run the Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="977bb-287">Подождите несколько минут, пока новый код будет развернут в промежуточный слот, а затем запустите сайт http://ToDoApp*&lt;ваш_суффикс>*-staging.azurewebsites.net и убедитесь, что новое обновление активировано в промежуточном слоте.</span><span class="sxs-lookup"><span data-stu-id="977bb-287">Wait for a few minutes for the new code to be deployed to the staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net to verify that the new update is warmed up in the staging slot.</span></span> <span data-ttu-id="977bb-288">Помните, что главная ветвь разветвления связана с промежуточным слотом приложения.</span><span class="sxs-lookup"><span data-stu-id="977bb-288">Remember that the your fork's master branch is linked to the staging slot of your app.</span></span>
4. <span data-ttu-id="977bb-289">Теперь переключите промежуточный слот в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="977bb-289">Now, swap the staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="977bb-290">Сводка</span><span class="sxs-lookup"><span data-stu-id="977bb-290">Summary</span></span>
<span data-ttu-id="977bb-291">Служба приложений Azure упрощает процесс тестирования приложений для клиентов малого и среднего бизнеса в рабочей среде — сценарий, который традиционно реализовывался в крупных организациях.</span><span class="sxs-lookup"><span data-stu-id="977bb-291">Azure App Service makes it easy for small- to medium-sized businesses to test their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="977bb-292">Мы надеемся, что приведенная в этом учебнике информация поможет вам использовать службу приложений наряду с Application Insights для развертывании в режиме фокус-тестирования и реализации других сценариев тестирования в рабочей среде в рамках DevOps.</span><span class="sxs-lookup"><span data-stu-id="977bb-292">Hopefully, this tutorial has given you the knowledge you need to bring together App Service and Application Insights to make possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="977bb-293">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="977bb-293">More resources</span></span>
* [<span data-ttu-id="977bb-294">Гибкая разработка программного обеспечения с помощью службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="977bb-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="977bb-295">Настройка промежуточных сред для веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="977bb-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="977bb-296">Предсказуемое развертывание сложного приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="977bb-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="977bb-297">Создание шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="977bb-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="977bb-298">JSONLint — проверяющий элемент управления JSON</span><span class="sxs-lookup"><span data-stu-id="977bb-298">JSONLint - The JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="977bb-299">Ветвление Git — основные ветвления и слияния</span><span class="sxs-lookup"><span data-stu-id="977bb-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="977bb-300">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="977bb-300">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="977bb-301">Вики-сайт проекта Kudu</span><span class="sxs-lookup"><span data-stu-id="977bb-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)
