---
title: "aaaContinuous доставки с Visual Studio Team Services в Azure и Git | Документы Microsoft"
description: "Узнайте, как tooconfigure в Visual Studio Team Services командные проекты toouse Git tooautomatically построение и развертывание компонентов toohello веб-приложения в службе приложений Azure или облачных служб."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="f7208-103">TooAzure непрерывной доставки с использованием Visual Studio Team Services и Git</span><span class="sxs-lookup"><span data-stu-id="f7208-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="f7208-104">Можно использовать Visual Studio Team Services командных проектов toohost репозитория исходного кода и автоматически построения и развертывания tooAzure веб-приложений или облачных служб при принудительной фиксации репозитория toohello.</span><span class="sxs-lookup"><span data-stu-id="f7208-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="f7208-105">Вам потребуется Visual Studio 2013 и hello установленный пакет SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="f7208-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="f7208-106">Если у вас еще нет Visual Studio 2013, загрузите ее, выбрав hello **начните бесплатно** связи [www.visualstudio.com](http://www.visualstudio.com). Здравствуйте, установка пакета Azure SDK с [здесь](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="f7208-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="f7208-107">Требуется учетная запись Visual Studio Team Services toocomplete этого учебника: вы можете [открыть учетную запись Visual Studio Team Services бесплатно](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="f7208-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="f7208-108">tooset копирование tooautomatically облачной службы построения и развертывания tooAzure с помощью Visual Studio Team Services, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f7208-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="f7208-109">1. Создание репозитория Git</span><span class="sxs-lookup"><span data-stu-id="f7208-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="f7208-110">Если у вас еще нет учетной записи Visual Studio Team Services, [создайте ее](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="f7208-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="f7208-111">При создании командного проекта выберите Git в качестве системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="f7208-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="f7208-112">Выполните инструкции hello tooconnect tooyour Visual Studio командного проекта.</span><span class="sxs-lookup"><span data-stu-id="f7208-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="f7208-113">В **Team Explorer**, выберите hello **клонировать этот репозиторий** ссылку.</span><span class="sxs-lookup"><span data-stu-id="f7208-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="f7208-114">Укажите расположение hello hello локальную копию, а затем выберите hello **клон** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f7208-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="f7208-115">2: Создание проекта и его сохранения toohello репозитория</span><span class="sxs-lookup"><span data-stu-id="f7208-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="f7208-116">В **Team Explorer**, в hello **решения** выберите hello **New** связать toocreate новый проект в локальном хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="f7208-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="f7208-117">Можно развернуть веб-приложения или облачной службы (приложение Azure), hello следующие шаги в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f7208-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="f7208-118">Создайте новый проект облачной службы Azure или новый проект MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f7208-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="f7208-119">Убедитесь, что целевых объектов проекта hello hello .NET Framework 4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f7208-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="f7208-120">Если вы создаете проект облачной службы, добавьте рабочую роль и веб-роль MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f7208-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="f7208-121">Если вы хотите toocreate веб-приложения, выберите hello **веб-приложение ASP.NET** шаблон проекта, а затем выберите **MVC**.</span><span class="sxs-lookup"><span data-stu-id="f7208-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="f7208-122">Дополнительные сведения см. в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f7208-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="f7208-123">Откройте контекстное меню hello hello решения и выберите **зафиксировать**.</span><span class="sxs-lookup"><span data-stu-id="f7208-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="f7208-124">Если это первый раз, вы уже использовали Git в Visual Studio Team Services hello потребуется tooprovide некоторые сведения tooidentify самостоятельно в Git.</span><span class="sxs-lookup"><span data-stu-id="f7208-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="f7208-125">В hello **ожидающие изменения** область **Team Explorer**введите свое имя пользователя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f7208-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="f7208-126">Введите комментарий для фиксации hello и выберите hello **фиксации** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f7208-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="f7208-127">Обратите внимание, tooinclude параметры hello или исключить определенных изменений при возврате.</span><span class="sxs-lookup"><span data-stu-id="f7208-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="f7208-128">При изменении hello, вы хотите исключаются, выберите **включить все**.</span><span class="sxs-lookup"><span data-stu-id="f7208-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="f7208-129">Вы уже теперь hello зафиксированные изменения в локальной копии репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="f7208-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="f7208-130">Затем синхронизировать изменения с сервера hello, выбрав hello **синхронизации** ссылку.</span><span class="sxs-lookup"><span data-stu-id="f7208-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="f7208-131">3: hello проекта tooAzure подключения</span><span class="sxs-lookup"><span data-stu-id="f7208-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="f7208-132">Теперь, когда репозитория в Visual Studio Team Services с помощью исходного кода, в нем используется tooconnect готовности вашей tooAzure репозитория git.</span><span class="sxs-lookup"><span data-stu-id="f7208-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="f7208-133">В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885)выберите облачной службы или веб-приложения, или создать новый, выбрав значок в левом нижнем hello и выбрав + hello **облачной службы** или **веб-приложения**и затем **быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="f7208-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="f7208-134">Для облачных служб выберите hello **Настройка публикации с использованием Visual Studio Team Services** ссылку.</span><span class="sxs-lookup"><span data-stu-id="f7208-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="f7208-135">Для веб-приложений выберите hello **настроить развертывание из системы управления версиями** ссылку.</span><span class="sxs-lookup"><span data-stu-id="f7208-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="f7208-136">В мастер hello, введите в текстовом поле hello hello имя вашей учетной записи Visual Studio Team Services и выберите hello **авторизовать теперь** ссылку.</span><span class="sxs-lookup"><span data-stu-id="f7208-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="f7208-137">Вас попросят toosign в.</span><span class="sxs-lookup"><span data-stu-id="f7208-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="f7208-138">В hello **запроса на подключение** всплывающем диалоговом окне выберите **Accept** tooauthorize Azure tooconfigure командного проекта в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f7208-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="f7208-139">После завершения авторизации появится раскрывающийся список, содержащий ваши командные проекты Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f7208-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="f7208-140">Выберите имя командного проекта, созданного на предыдущих этапах hello hello и нажмите кнопку флажок приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="f7208-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="f7208-141">Hello принудительной фиксации tooyour репозитория, Visual Studio Team Services при очередном создаст и развернет ваш проект tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f7208-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="f7208-142">4. Запуск процессов повторного построения и развертывания проекта</span><span class="sxs-lookup"><span data-stu-id="f7208-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="f7208-143">Откройте файл в Visual Studio и измените его.</span><span class="sxs-lookup"><span data-stu-id="f7208-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="f7208-144">Например, измените файл hello `_Layout.cshtml` в области представления hello\\общая папка в веб-роли MVC.</span><span class="sxs-lookup"><span data-stu-id="f7208-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="f7208-145">Изменить текст нижнего колонтитула hello hello сайта и сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="f7208-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="f7208-146">В **обозревателе решений**, откройте контекстное меню hello для hello узел решения, проекта или hello файл можно изменить и выберите **зафиксировать**.</span><span class="sxs-lookup"><span data-stu-id="f7208-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="f7208-147">Введите комментарий и нажмите кнопку **Зафиксировать**.</span><span class="sxs-lookup"><span data-stu-id="f7208-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="f7208-148">Выберите hello **синхронизации** ссылку.</span><span class="sxs-lookup"><span data-stu-id="f7208-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="f7208-149">Выберите hello **Push** связать toopush репозиторий toohello фиксации в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f7208-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="f7208-150">(Можно также использовать hello **синхронизации** кнопку toocopy репозиторий toohello фиксации.</span><span class="sxs-lookup"><span data-stu-id="f7208-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="f7208-151">Hello различие состоит в том **синхронизации** также переносит hello последние изменения из репозитория hello.)</span><span class="sxs-lookup"><span data-stu-id="f7208-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="f7208-152">Выберите hello **домашней** toohello tooreturn кнопку **Team Explorer** домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="f7208-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="f7208-153">Выберите **строит** tooview hello сборки в данный момент.</span><span class="sxs-lookup"><span data-stu-id="f7208-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="f7208-154">**Team Explorer** отображается информация о том, что для вашего возврата запущен процесс сборки.</span><span class="sxs-lookup"><span data-stu-id="f7208-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="f7208-155">tooview подробный журнал hello сборки по мере того, дважды щелкните имя hello hello построения выполняется.</span><span class="sxs-lookup"><span data-stu-id="f7208-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="f7208-156">Пока сборка hello в процессе выполнения, взгляните на определение сборки hello, который был создан при использовании tooAzure toolink приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="f7208-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="f7208-157">Откройте контекстное меню определения сборки hello hello и выберите **Редактировать определение построения**.</span><span class="sxs-lookup"><span data-stu-id="f7208-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="f7208-158">В hello **триггер** вкладку, вы увидите, определение сборки hello toobuild на каждом возврате по умолчанию имеет значение.</span><span class="sxs-lookup"><span data-stu-id="f7208-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="f7208-159">(Для облачной службы, Visual Studio Team Services строит и развертывает toohello hello главную ветвь, автоматически промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="f7208-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="f7208-160">Вы по-прежнему иметь toodo ручной шаг сайт динамической toodeploy toohello.</span><span class="sxs-lookup"><span data-stu-id="f7208-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="f7208-161">Для веб-приложения, у которого нет промежуточной среде она развертывает hello главную ветвь, напрямую toohello работающий узел.</span><span class="sxs-lookup"><span data-stu-id="f7208-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="f7208-162">В hello **процесс** вкладку, вы увидите установки среды развертывания hello toohello имя облачной службы или веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f7208-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="f7208-163">Укажите значения для свойств hello различных значений, чем значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f7208-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="f7208-164">Hello свойства для публикации Azure находятся в hello **развертывания** раздела, а также могут потребоваться tooset параметры MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f7208-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="f7208-165">Например, в проект облачной службы toospecify конфигурации службы, отличное от «Облака», задайте параметры MSbuild hello слишком`/p:TargetProfile=[YourProfile]` где *[YourProfile]* соответствующий файл конфигурации службы с именем, например ServiceConfiguration. *YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="f7208-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="f7208-166">Hello следующей таблице показаны доступные свойства hello в hello **развертывания** раздела:</span><span class="sxs-lookup"><span data-stu-id="f7208-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="f7208-167">Свойство</span><span class="sxs-lookup"><span data-stu-id="f7208-167">Property</span></span> | <span data-ttu-id="f7208-168">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="f7208-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f7208-169">Разрешить недоверенные сертификаты</span><span class="sxs-lookup"><span data-stu-id="f7208-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="f7208-170">Если установлено значение false, то SSL-сертификаты должны быть подписаны корневым центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="f7208-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="f7208-171">Разрешить обновление</span><span class="sxs-lookup"><span data-stu-id="f7208-171">Allow Upgrade</span></span> |<span data-ttu-id="f7208-172">Позволяет tooupdate развертывания hello существующего развертывания вместо создания нового.</span><span class="sxs-lookup"><span data-stu-id="f7208-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="f7208-173">Сохраняет hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f7208-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="f7208-174">Не удалять</span><span class="sxs-lookup"><span data-stu-id="f7208-174">Do Not Delete</span></span> |<span data-ttu-id="f7208-175">Если установлено значение true, не разрешена перезапись существующего несвязанного развертывания (обновление разрешено).</span><span class="sxs-lookup"><span data-stu-id="f7208-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="f7208-176">Путь tooDeployment параметры</span><span class="sxs-lookup"><span data-stu-id="f7208-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="f7208-177">Hello путь tooyour pubxml-файл для веб-приложения, относительного toohello корневой папки репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="f7208-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="f7208-178">Для облачных служб игнорируется.</span><span class="sxs-lookup"><span data-stu-id="f7208-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="f7208-179">Среда развертывания Sharepoint</span><span class="sxs-lookup"><span data-stu-id="f7208-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="f7208-180">Здравствуйте таким же, как имя службы hello.</span><span class="sxs-lookup"><span data-stu-id="f7208-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="f7208-181">Среда развертывания Azure</span><span class="sxs-lookup"><span data-stu-id="f7208-181">Azure Deployment Environment</span></span> |<span data-ttu-id="f7208-182">Hello имя веб-приложения или облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f7208-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="f7208-183">К этому моменту процесс построения должен быть успешно завершен.</span><span class="sxs-lookup"><span data-stu-id="f7208-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="f7208-184">Если дважды щелкнуть имя сборки hello, Visual Studio отображает **сводки построения**, включая результатов теста из связанных проектов модульных тестов.</span><span class="sxs-lookup"><span data-stu-id="f7208-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="f7208-185">В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885), вы можете просмотреть связанные hello развертывания на hello **развертываний** вкладке при выборе hello в промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="f7208-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="f7208-186">URL-адрес сайта tooyour обзора.</span><span class="sxs-lookup"><span data-stu-id="f7208-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="f7208-187">Для веб-приложения, просто выберите hello **Обзор** кнопку hello портала.</span><span class="sxs-lookup"><span data-stu-id="f7208-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="f7208-188">Для облачной службы, выберите URL-адрес hello в hello **быстрый обзор** раздел hello **мониторинга** страницы, отображающей hello промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="f7208-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="f7208-189">Развертывания с непрерывной интеграции для облачных служб — опубликованных toohello промежуточной среды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f7208-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="f7208-190">Это можно изменить, установка hello **альтернативное окружение облачной службы** свойство слишком**рабочей**.</span><span class="sxs-lookup"><span data-stu-id="f7208-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="f7208-191">Здесь находится URL-адрес сайта hello на странице панели мониторинга hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f7208-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="f7208-192">На новой вкладке браузера откроется tooreveal выполнение веб-узла.</span><span class="sxs-lookup"><span data-stu-id="f7208-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="f7208-193">При внесении другие изменения tooyour проекта, то триггер более строит и накапливаются несколько развертываний.</span><span class="sxs-lookup"><span data-stu-id="f7208-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="f7208-194">Здравствуйте, последняя версия один помечен как активный.</span><span class="sxs-lookup"><span data-stu-id="f7208-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="f7208-195">5. Повторное развертывание предыдущей сборки</span><span class="sxs-lookup"><span data-stu-id="f7208-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="f7208-196">Этот шаг не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="f7208-196">This step is optional.</span></span> <span data-ttu-id="f7208-197">В hello классический портал Azure, выберите более ранних развертывания и выберите **повторно развернуть** toorewind вашего сайта tooan ранее возврата.</span><span class="sxs-lookup"><span data-stu-id="f7208-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="f7208-198">Обратите внимание, что при этом в TFS будет запущен новый процесс сборки, а в историю развертывания будет добавлена новая запись.</span><span class="sxs-lookup"><span data-stu-id="f7208-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="f7208-199">6: изменение hello рабочего развертывания</span><span class="sxs-lookup"><span data-stu-id="f7208-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="f7208-200">Когда будете готовы, вы можете повысить уровень hello промежуточной toohello рабочей среды, выбрав **замены** в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f7208-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="f7208-201">вновь развернуть Hello промежуточной среды tooProduction повышенного уровня, а hello предыдущей рабочей среде, если таковые имеются, становится промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="f7208-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="f7208-202">Hello активное развертывание может быть разным для hello производственной и промежуточной сред, но История развертывания hello последних построений hello одинаково независимо от среды.</span><span class="sxs-lookup"><span data-stu-id="f7208-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="f7208-203">7. Развертывание из рабочей ветви</span><span class="sxs-lookup"><span data-stu-id="f7208-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="f7208-204">При использовании Git обычно внести изменения в рабочую ветвь и интегрировать в главную ветвь hello достижении состоянии завершения разработки.</span><span class="sxs-lookup"><span data-stu-id="f7208-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="f7208-205">Во время стадии разработки проекта hello вам требуется toobuild и развернуть ветвь tooAzure hello рабочий.</span><span class="sxs-lookup"><span data-stu-id="f7208-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="f7208-206">В **Team Explorer**, выберите hello **Главная** кнопку и выберите hello **ветви** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f7208-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="f7208-207">Выберите hello **новой ветви** ссылку.</span><span class="sxs-lookup"><span data-stu-id="f7208-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="f7208-208">Введите имя hello hello ветвь, например «работает» и выберите **создать ветвь**.</span><span class="sxs-lookup"><span data-stu-id="f7208-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="f7208-209">Будет создана новая локальная ветвь.</span><span class="sxs-lookup"><span data-stu-id="f7208-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="f7208-210">Опубликуйте ветвь hello.</span><span class="sxs-lookup"><span data-stu-id="f7208-210">Publish hello branch.</span></span> <span data-ttu-id="f7208-211">Выберите имя ветви hello в **неопубликованных ветвей**и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="f7208-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="f7208-212">По умолчанию изменяется только триггер главную ветвь toohello непрерывном режиме построения.</span><span class="sxs-lookup"><span data-stu-id="f7208-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="f7208-213">tooset копирование непрерывном режиме построения для рабочую ветвь, выберите hello **строит** страницы в **Team Explorer**и выберите **Редактировать определение построения**.</span><span class="sxs-lookup"><span data-stu-id="f7208-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="f7208-214">Откройте hello **параметры источника** вкладки. В разделе **отслеживаемые ветви для непрерывной интеграции и построения**, выберите **tooadd новой строки щелкните здесь**.</span><span class="sxs-lookup"><span data-stu-id="f7208-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="f7208-215">Укажите hello ветви, которую вы создали, например refs/heads/работа.</span><span class="sxs-lookup"><span data-stu-id="f7208-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="f7208-216">Внести изменения в коде hello Привет открыть контекстное меню для файла hello изменен, а затем выберите **зафиксировать**.</span><span class="sxs-lookup"><span data-stu-id="f7208-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="f7208-217">Выберите hello **несинхронизированные фиксации** ссылку и выберите hello **синхронизации** кнопки или hello **Push** hello toocopy ссылку изменяет toohello копию hello рабочую ветвь в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f7208-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="f7208-218">Перейдите toohello **строит** Просмотр и поиск сборки hello, есть только вызвавшей hello рабочую ветвь.</span><span class="sxs-lookup"><span data-stu-id="f7208-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7208-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7208-219">Next steps</span></span>
<span data-ttu-id="f7208-220">см. Дополнительные советы по использованию Git в Visual Studio Team Services toolearn [разработка и совместного использования кода в Git, с помощью Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) и сведения об использовании репозитория, который не находится под управлением toopublish Visual Studio Team Services tooAzure, в разделе [tooAzure непрерывного развертывания службы приложений](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f7208-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="f7208-221">Дополнительные сведения о Visual Studio Team Services см. [здесь](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="f7208-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
