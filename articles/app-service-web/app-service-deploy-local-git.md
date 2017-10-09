---
title: "Развертывание Git aaaLocal tooAzure службы приложений"
description: "Узнайте, как развертывание tooAzure tooenable локальный Git службы приложений."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="b76b9-103">Локальные развертывания Git tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="b76b9-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="b76b9-104">В этом учебнике показано как toodeploy приложения слишком[службе приложений Azure] из репозитория Git на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b76b9-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="b76b9-105">Службы приложений поддерживает такой подход с hello **Local Git** вариант развертывания в hello [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="b76b9-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="b76b9-106">Многие из описанных в этой статье команды Git hello выполняются автоматически при создании приложения службы приложений с помощью hello [интерфейса командной строки Azure] как описано [здесь](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b76b9-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b76b9-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b76b9-107">Prerequisites</span></span>
<span data-ttu-id="b76b9-108">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="b76b9-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="b76b9-109">Git.</span><span class="sxs-lookup"><span data-stu-id="b76b9-109">Git.</span></span> <span data-ttu-id="b76b9-110">Вы можете загрузить двоичный установки hello [здесь](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="b76b9-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="b76b9-111">Базовые знания о Git.</span><span class="sxs-lookup"><span data-stu-id="b76b9-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="b76b9-112">Учетная запись Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b76b9-112">A Microsoft Azure account.</span></span> <span data-ttu-id="b76b9-113">Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="b76b9-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="b76b9-114">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать приложение кратковременных начальный в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="b76b9-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="b76b9-115">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="b76b9-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="b76b9-116"><a name="Step1"></a>Шаг 1. Создание локального репозитория</span><span class="sxs-lookup"><span data-stu-id="b76b9-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="b76b9-117">Выполните следующие задачи toocreate новый репозиторий Git hello.</span><span class="sxs-lookup"><span data-stu-id="b76b9-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="b76b9-118">Запустите программу командной строки, например **GitBash** (Windows) или **Bash** (оболочка Unix).</span><span class="sxs-lookup"><span data-stu-id="b76b9-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="b76b9-119">В системах OS X можно обращаться из командной строки hello hello **терминалов** приложения.</span><span class="sxs-lookup"><span data-stu-id="b76b9-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="b76b9-120">Перейдите в каталог toohello, где будет располагаться содержимого toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="b76b9-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="b76b9-121">Используйте hello, следующая команда tooinitialize новый репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="b76b9-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="b76b9-122"><a name="Step2"></a>Шаг 2. Фиксация содержимого</span><span class="sxs-lookup"><span data-stu-id="b76b9-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="b76b9-123">Служба приложений поддерживает приложения, созданные с использованием различных языков программирования.</span><span class="sxs-lookup"><span data-stu-id="b76b9-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="b76b9-124">Если репозиторий уже включает содержимое пропустить эту точку при перемещении toopoint 2 ниже.</span><span class="sxs-lookup"><span data-stu-id="b76b9-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="b76b9-125">Если репозиторий пуст, заполните его статическим HTML-файлом, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b76b9-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="b76b9-126">В текстовом редакторе создайте новый файл с именем **index.html** hello корню репозитория Git hello</span><span class="sxs-lookup"><span data-stu-id="b76b9-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="b76b9-127">Добавить после текста, как содержимое hello для hello index.html файл и сохраните его hello: *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="b76b9-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="b76b9-128">Из командной строки hello убедитесь, что в корне hello репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="b76b9-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="b76b9-129">Затем используйте hello, следующая команда tooadd файлы tooyour репозитория:</span><span class="sxs-lookup"><span data-stu-id="b76b9-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="b76b9-130">Далее, фиксации hello изменения toohello репозитория с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b76b9-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="b76b9-131"><a name="Step3"></a>Шаг 3: Включение hello репозитория приложения служб приложений</span><span class="sxs-lookup"><span data-stu-id="b76b9-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="b76b9-132">Выполните следующие шаги tooenable репозитория для приложения службы приложений hello.</span><span class="sxs-lookup"><span data-stu-id="b76b9-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="b76b9-133">Войдите в toohello [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="b76b9-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="b76b9-134">В колонке приложения службы приложений выберите **Параметры > Источник развертывания**.</span><span class="sxs-lookup"><span data-stu-id="b76b9-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="b76b9-135">Щелкните **Выбрать источник**, затем выберите **Локальный репозиторий Git** и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="b76b9-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Локальный репозиторий Git](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="b76b9-137">Если это ваш первый подготовку в репозитории в Azure, для него необходимо toocreate учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="b76b9-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="b76b9-138">Используется их toolog в hello Azure репозитория и изменения из локального репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="b76b9-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="b76b9-139">В колонке приложения щелкните **Параметры > Учетные данные развертывания**, а затем настройте имя пользователя и пароль развертывания.</span><span class="sxs-lookup"><span data-stu-id="b76b9-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="b76b9-140">Закончив, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b76b9-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="b76b9-141"><a name="Step4"></a>Шаг 4. Развертывание проекта</span><span class="sxs-lookup"><span data-stu-id="b76b9-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="b76b9-142">Используйте следующие шаги toopublish hello tooApp вашего приложения службы с помощью Local Git.</span><span class="sxs-lookup"><span data-stu-id="b76b9-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="b76b9-143">В колонке приложения в hello портала Azure щелкните **параметры > свойства** для hello **URL-адрес Git**.</span><span class="sxs-lookup"><span data-stu-id="b76b9-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="b76b9-144">**URL-адрес Git** является toofrom toodeploy hello удаленную ссылку на ваш локальный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="b76b9-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="b76b9-145">Вы будете использовать этот URL-адрес в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="b76b9-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="b76b9-146">С помощью командной строки hello, убедитесь, что находятся в корне hello ваш локальный репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="b76b9-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="b76b9-147">Используйте `git remote` tooadd hello удаленную ссылку в **URL-адрес Git** из шага 1.</span><span class="sxs-lookup"><span data-stu-id="b76b9-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="b76b9-148">Команда будет выглядеть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="b76b9-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="b76b9-149">Hello **удаленного** команда добавляет в удаленном репозитории tooa именованную ссылку.</span><span class="sxs-lookup"><span data-stu-id="b76b9-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="b76b9-150">В этом примере создается ссылка с именем azure для репозитория вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b76b9-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="b76b9-151">Push вашего содержимого tooApp службы с помощью нового hello **azure** удаленного вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="b76b9-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="b76b9-152">Вы можете вернуться tooyour приложения hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="b76b9-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="b76b9-153">Запись журнала последней передачу должны отображаться в hello **развертываний** колонку.</span><span class="sxs-lookup"><span data-stu-id="b76b9-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="b76b9-154">Нажмите кнопку hello **Обзор** кнопку вверху hello приложение hello колонке tooverify hello содержимого был развернут.</span><span class="sxs-lookup"><span data-stu-id="b76b9-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="b76b9-155"><a name="Step5"></a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="b76b9-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="b76b9-156">Hello ниже приведены ошибок или проблем, обычно возникающих при использовании Git toopublish tooan приложением служб приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="b76b9-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="b76b9-157">**Симптом**: не удается tooaccess [siteURL]: не удалось выполнить tooconnect слишком [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="b76b9-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="b76b9-158">**Причина**: Эта ошибка может возникать, если приложение hello не запущен и работает.</span><span class="sxs-lookup"><span data-stu-id="b76b9-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="b76b9-159">**Разрешение**: приложения hello запуска в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="b76b9-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="b76b9-160">Развертывание Git не будет работать, пока не будет запущен приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b76b9-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="b76b9-161">**Симптом**: не удается разрешить hostname узла.</span><span class="sxs-lookup"><span data-stu-id="b76b9-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="b76b9-162">**Причина**: Эта ошибка может произойти, если ввести сведения hello адрес при создании hello удаленного «azure» неверно.</span><span class="sxs-lookup"><span data-stu-id="b76b9-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="b76b9-163">**Разрешение**: hello используйте `git remote -v` команды toolist все удаленные элементы, связанные hello URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="b76b9-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="b76b9-164">Проверьте правильность URL-адрес hello hello «azure» на удаленном.</span><span class="sxs-lookup"><span data-stu-id="b76b9-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="b76b9-165">При необходимости удалите и повторно создайте этот удаленный с помощью hello правильный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b76b9-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="b76b9-166">**Симптом**: нет ссылок и ничего не указано; ничего не выполняется.</span><span class="sxs-lookup"><span data-stu-id="b76b9-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="b76b9-167">Возможно, следует указать ветвь, например master.</span><span class="sxs-lookup"><span data-stu-id="b76b9-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="b76b9-168">**Причина**: Эта ошибка может возникать, если не указать ветви, при выполнении операции git push и иметь не набор hello push.default значение, используемое Git.</span><span class="sxs-lookup"><span data-stu-id="b76b9-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="b76b9-169">**Разрешение**: выполнить hello принудительную попытку, указав hello главную ветвь.</span><span class="sxs-lookup"><span data-stu-id="b76b9-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="b76b9-170">Например:</span><span class="sxs-lookup"><span data-stu-id="b76b9-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="b76b9-171">**Симптом**: src refspec [имя_ветви] не соответствует никакой ветви.</span><span class="sxs-lookup"><span data-stu-id="b76b9-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="b76b9-172">**Причина**: Эта ошибка может возникать при попытке toopush tooa ветвь, кроме master на hello «azure» на удаленном.</span><span class="sxs-lookup"><span data-stu-id="b76b9-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="b76b9-173">**Разрешение**: выполнить hello принудительную попытку, указав hello главную ветвь.</span><span class="sxs-lookup"><span data-stu-id="b76b9-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="b76b9-174">Например:</span><span class="sxs-lookup"><span data-stu-id="b76b9-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="b76b9-175">**Симптом**. Сбой RPC, результат — 22, код HTTP — 502.</span><span class="sxs-lookup"><span data-stu-id="b76b9-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="b76b9-176">**Причина**: Эта ошибка может возникать при попытке toopush больших репозитория по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b76b9-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="b76b9-177">**Разрешение**: изменение конфигурации git hello на hello локального компьютера toomake hello postBuffer больше</span><span class="sxs-lookup"><span data-stu-id="b76b9-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="b76b9-178">**Симптом**: ошибка - репозитория tooremote зафиксированные изменения, кроме веб-приложения не обновляется.</span><span class="sxs-lookup"><span data-stu-id="b76b9-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="b76b9-179">**Причина**: эта ошибка может возникнуть при развертывании приложения Node.js, содержащего файл package.json, в котором указаны дополнительные необходимые модули.</span><span class="sxs-lookup"><span data-stu-id="b76b9-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="b76b9-180">**Решение.** До этой ошибки должны быть зарегистрированы</span><span class="sxs-lookup"><span data-stu-id="b76b9-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="b76b9-181">должно быть toothis журнал предыдущих ошибок и может предоставить дополнительный контекст при сбое hello.</span><span class="sxs-lookup"><span data-stu-id="b76b9-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="b76b9-182">Hello следующие известные причины этой ошибки и hello соответствующий «npm ERR!»</span><span class="sxs-lookup"><span data-stu-id="b76b9-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="b76b9-183">сообщение:</span><span class="sxs-lookup"><span data-stu-id="b76b9-183">message:</span></span>

* <span data-ttu-id="b76b9-184">**Malformed package.json file**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="b76b9-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="b76b9-185">Couldn't read dependencies (не удалось прочитать зависимости).</span><span class="sxs-lookup"><span data-stu-id="b76b9-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="b76b9-186">**Собственный модуль, не имеющий двоичного дистрибутива для Windows**:</span><span class="sxs-lookup"><span data-stu-id="b76b9-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="b76b9-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="b76b9-187">npm ERR!</span></span> <span data-ttu-id="b76b9-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1 (команда cmd "/c" "node-gyp rebuild" привела к сбою с 1)</span><span class="sxs-lookup"><span data-stu-id="b76b9-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="b76b9-189">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="b76b9-189">OR</span></span>
  * <span data-ttu-id="b76b9-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="b76b9-190">npm ERR!</span></span> <span data-ttu-id="b76b9-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="b76b9-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b76b9-192">дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b76b9-192">Additional Resources</span></span>
* [<span data-ttu-id="b76b9-193">Документация по Git</span><span class="sxs-lookup"><span data-stu-id="b76b9-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="b76b9-194">Документация по проекту Kudu</span><span class="sxs-lookup"><span data-stu-id="b76b9-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="b76b9-195">TooAzure непрерывного развертывания служб приложений</span><span class="sxs-lookup"><span data-stu-id="b76b9-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="b76b9-196">Как toouse PowerShell для Azure</span><span class="sxs-lookup"><span data-stu-id="b76b9-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="b76b9-197">Как toouse hello интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b76b9-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[службе приложений Azure]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[портала Azure]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[интерфейса командной строки Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
