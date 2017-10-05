---
title: "Непрерывная поставка в Azure с использованием Visual Studio Team Services и Git | Документация Майкрософт"
description: "Узнайте, как с помощью Git настроить автоматическое создание и развертывание веб-приложений и облачных служб Azure в командных проектах Visual Studio Team Services."
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
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="1d06a-103">Непрерывная доставка в Azure с использованием Visual Studio Team Services и Git</span><span class="sxs-lookup"><span data-stu-id="1d06a-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="1d06a-104">С помощью командных проектов Visual Studio Team Services можно размещать репозиторий Git для исходного кода и выполнять автоматическое построение и развертывание в веб-приложениях Azure или в облачных службах при каждой операции фиксации в репозитории.</span><span class="sxs-lookup"><span data-stu-id="1d06a-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="1d06a-105">В данном учебнике требуются установленные Visual Studio 2013 и пакет SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="1d06a-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="1d06a-106">Чтобы загрузить Visual Studio 2013, щелкните ссылку **Начните работу бесплатно** на сайте [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="1d06a-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="1d06a-107">Пакет SDK Azure можно установить по [этой ссылке](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="1d06a-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="1d06a-108">Для работы с этим руководством необходима учетная запись Visual Studio Team Services. Вы можете [бесплатно зарегистрировать учетную запись Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="1d06a-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="1d06a-109">Чтобы настроить автоматическое выполнение сборки и развертывания облачной службы в Azure с использованием Visual Studio Team Services, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1d06a-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="1d06a-110">1. Создание репозитория Git</span><span class="sxs-lookup"><span data-stu-id="1d06a-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="1d06a-111">Если у вас еще нет учетной записи Visual Studio Team Services, [создайте ее](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="1d06a-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="1d06a-112">При создании командного проекта выберите Git в качестве системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="1d06a-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="1d06a-113">Выполните следующие инструкции для подключения Visual Studio к командному проекту.</span><span class="sxs-lookup"><span data-stu-id="1d06a-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="1d06a-114">В обозревателе **Team Explorer** выберите ссылку **Клонировать этот репозиторий**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="1d06a-115">Укажите расположение локальной копии и нажмите кнопку **Клонировать** .</span><span class="sxs-lookup"><span data-stu-id="1d06a-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="1d06a-116">2. Создание проекта и сохранение его в репозитории</span><span class="sxs-lookup"><span data-stu-id="1d06a-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="1d06a-117">В **Team Explorer** в разделе **Решения** щелкните ссылку **Создать**, чтобы создать новый проект в локальном репозитории.</span><span class="sxs-lookup"><span data-stu-id="1d06a-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="1d06a-118">В этом пошаговом руководстве представлены инструкции по развертыванию веб-приложения или облачной службы (приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="1d06a-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="1d06a-119">Создайте новый проект облачной службы Azure или новый проект MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1d06a-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="1d06a-120">Убедитесь в том, что проект предназначен для платформы .NET Framework 4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1d06a-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="1d06a-121">Если вы создаете проект облачной службы, добавьте рабочую роль и веб-роль MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1d06a-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="1d06a-122">Если вы хотите создать веб-приложение, выберите шаблон проекта **Веб-приложение ASP.NET**, а затем — **MVC**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="1d06a-123">Дополнительные сведения см. в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1d06a-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="1d06a-124">Откройте контекстное меню для этого решения и выберите пункт **Зафиксировать**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="1d06a-125">Если вы впервые используете Git в Visual Studio Team Services, необходимо предоставить некоторые сведения для вашей идентификации в Git.</span><span class="sxs-lookup"><span data-stu-id="1d06a-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="1d06a-126">В области **ожидающих изменений** в **Team Explorer** укажите свое имя пользователя и адрес почты.</span><span class="sxs-lookup"><span data-stu-id="1d06a-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="1d06a-127">Введите комментарий для фиксации, а затем нажмите кнопку **Зафиксировать** .</span><span class="sxs-lookup"><span data-stu-id="1d06a-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="1d06a-128">Обратите внимание на варианты для включения или исключения определенных изменений при настройке.</span><span class="sxs-lookup"><span data-stu-id="1d06a-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="1d06a-129">Если нужные изменения исключены, выберите **Включить все**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="1d06a-130">Теперь изменения зафиксированы в локальной копии репозитория.</span><span class="sxs-lookup"><span data-stu-id="1d06a-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="1d06a-131">Далее следует синхронизировать эти изменения с сервером. Для этого выберите ссылку **Синхронизировать**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="1d06a-132">3. Подключение проекта к Azure</span><span class="sxs-lookup"><span data-stu-id="1d06a-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="1d06a-133">Теперь, когда имеется репозиторий Git в Visual Studio Team Services, содержащий некоторый исходный код, можно подключить этот репозиторий к Azure.</span><span class="sxs-lookup"><span data-stu-id="1d06a-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="1d06a-134">Войдите на [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885) и выберите существующую облачную службу или веб-приложение. Вы также можете создать новые объекты, щелкнув в нижнем левом углу значок "+", а затем выбрав **Облачная служба** или **Веб-приложение** и **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="1d06a-135">Для облачных служб щелкните ссылку **Настройка публикации в Visual Studio Team Services** .</span><span class="sxs-lookup"><span data-stu-id="1d06a-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="1d06a-136">Для веб-приложений нажмите ссылку **Настроить развертывание из системы управления версиями** .</span><span class="sxs-lookup"><span data-stu-id="1d06a-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="1d06a-137">В мастере введите имя учетной записи Visual Studio Team Services в соответствующем поле и нажмите ссылку **Авторизовать сейчас** .</span><span class="sxs-lookup"><span data-stu-id="1d06a-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="1d06a-138">Может появиться запрос на вход в систему.</span><span class="sxs-lookup"><span data-stu-id="1d06a-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="1d06a-139">Во всплывающем диалоговом окне **Connection Request** (Запрос на подключение) нажмите кнопку **Принять**, чтобы предоставить Azure полномочия для настройки командного проекта в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1d06a-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="1d06a-140">После завершения авторизации появится раскрывающийся список, содержащий ваши командные проекты Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1d06a-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="1d06a-141">Щелкните имя созданного на предыдущих шагах командного проекта и нажмите кнопку с галочкой в мастере.</span><span class="sxs-lookup"><span data-stu-id="1d06a-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="1d06a-142">При следующей фиксации в репозитории Visual Studio Team Services будет выполнять построение и развертывание проекта в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d06a-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="1d06a-143">4. Запуск процессов повторного построения и развертывания проекта</span><span class="sxs-lookup"><span data-stu-id="1d06a-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="1d06a-144">Откройте файл в Visual Studio и измените его.</span><span class="sxs-lookup"><span data-stu-id="1d06a-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="1d06a-145">Например, вы можете изменить файл `_Layout.cshtml` в папке Views\\Shared веб-роли MVC.</span><span class="sxs-lookup"><span data-stu-id="1d06a-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="1d06a-146">Измените текст нижнего колонтитула для сайта и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="1d06a-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="1d06a-147">В **обозревателе решений** откройте контекстное меню узла решения, узла проекта или файла, который был изменен, и выберите команду **Зафиксировать**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="1d06a-148">Введите комментарий и нажмите кнопку **Зафиксировать**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="1d06a-149">Нажмите ссылку **Синхронизация** .</span><span class="sxs-lookup"><span data-stu-id="1d06a-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="1d06a-150">Нажмите ссылку **Отправить** , чтобы отправить фиксацию в репозиторий в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1d06a-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="1d06a-151">(Можно также использовать кнопку **Синхронизация** , чтобы скопировать фиксации в репозиторий.</span><span class="sxs-lookup"><span data-stu-id="1d06a-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="1d06a-152">Разница в том, что **синхронизация** также запрашивает последние изменения в репозитории.)</span><span class="sxs-lookup"><span data-stu-id="1d06a-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="1d06a-153">Нажмите кнопку **Домашняя страница**, чтобы вернуться на домашнюю страницу **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="1d06a-154">Щелкните **Сборки** , чтобы просмотреть выполняющиеся сборки.</span><span class="sxs-lookup"><span data-stu-id="1d06a-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="1d06a-155">**Team Explorer** отображается информация о том, что для вашего возврата запущен процесс сборки.</span><span class="sxs-lookup"><span data-stu-id="1d06a-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="1d06a-156">Дважды щелкните имя выполняемого построения, чтобы просмотреть подробный журнал процесса построения.</span><span class="sxs-lookup"><span data-stu-id="1d06a-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="1d06a-157">В процессе построения вы можете просмотреть определение сборки, созданное во время привязки к Azure с помощью мастера.</span><span class="sxs-lookup"><span data-stu-id="1d06a-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="1d06a-158">Откройте контекстное меню определения сборки и выберите команду **Редактировать определение сборки**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="1d06a-159">На вкладке **Триггер** вы увидите, что в определении сборки по умолчанию задано выполнение сборки при каждом возврате.</span><span class="sxs-lookup"><span data-stu-id="1d06a-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="1d06a-160">(Для облачной службы Visual Studio Team Services автоматически выполняет построение и развертывание главной ветви в промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="1d06a-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="1d06a-161">Развертывание на рабочем сайте необходимо будет выполнить вручную.</span><span class="sxs-lookup"><span data-stu-id="1d06a-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="1d06a-162">Для веб-приложения, у которого нет промежуточной среды, развертывание главной ветви выполняется непосредственно на работающем сайте.</span><span class="sxs-lookup"><span data-stu-id="1d06a-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="1d06a-163">На вкладке **Процесс** вы увидите, что в среде развертывания задано имя вашей облачной веб-службы или веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="1d06a-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="1d06a-164">При необходимости измените установленные по умолчанию значения свойств.</span><span class="sxs-lookup"><span data-stu-id="1d06a-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="1d06a-165">Свойства публикации в Azure доступны в разделе **Развертывание** ; также может потребоваться установка параметров MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1d06a-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="1d06a-166">Например, чтобы указать в проекте облачной службы конфигурацию, отличную от Cloud, установите для параметров MSbuild значение `/p:TargetProfile=[YourProfile]`, где *[YourProfile]* соответствует файлу конфигурации службы с именем типа ServiceConfiguration.*YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="1d06a-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="1d06a-167">В следующей таблице приводятся доступные свойства в разделе **Развертывание** :</span><span class="sxs-lookup"><span data-stu-id="1d06a-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="1d06a-168">Свойство</span><span class="sxs-lookup"><span data-stu-id="1d06a-168">Property</span></span> | <span data-ttu-id="1d06a-169">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1d06a-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1d06a-170">Разрешить недоверенные сертификаты</span><span class="sxs-lookup"><span data-stu-id="1d06a-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="1d06a-171">Если установлено значение false, то SSL-сертификаты должны быть подписаны корневым центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="1d06a-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="1d06a-172">Разрешить обновление</span><span class="sxs-lookup"><span data-stu-id="1d06a-172">Allow Upgrade</span></span> |<span data-ttu-id="1d06a-173">Разрешает обновление существующего развертывания вместо создания нового.</span><span class="sxs-lookup"><span data-stu-id="1d06a-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="1d06a-174">Сохраняет IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="1d06a-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="1d06a-175">Не удалять</span><span class="sxs-lookup"><span data-stu-id="1d06a-175">Do Not Delete</span></span> |<span data-ttu-id="1d06a-176">Если установлено значение true, не разрешена перезапись существующего несвязанного развертывания (обновление разрешено).</span><span class="sxs-lookup"><span data-stu-id="1d06a-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="1d06a-177">Путь к параметрам развертывания</span><span class="sxs-lookup"><span data-stu-id="1d06a-177">Path to Deployment Settings</span></span> |<span data-ttu-id="1d06a-178">Путь к PUBXML-файлу для веб-приложения относительно корневой папки репозитория.</span><span class="sxs-lookup"><span data-stu-id="1d06a-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="1d06a-179">Для облачных служб игнорируется.</span><span class="sxs-lookup"><span data-stu-id="1d06a-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="1d06a-180">Среда развертывания Sharepoint</span><span class="sxs-lookup"><span data-stu-id="1d06a-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="1d06a-181">Совпадает с именем службы.</span><span class="sxs-lookup"><span data-stu-id="1d06a-181">The same as the service name.</span></span> |
    | <span data-ttu-id="1d06a-182">Среда развертывания Azure</span><span class="sxs-lookup"><span data-stu-id="1d06a-182">Azure Deployment Environment</span></span> |<span data-ttu-id="1d06a-183">Имя веб-приложения или облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1d06a-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="1d06a-184">К этому моменту процесс построения должен быть успешно завершен.</span><span class="sxs-lookup"><span data-stu-id="1d06a-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="1d06a-185">Если дважды щелкнуть имя сборки, Visual Studio отобразит **сводку сборки**, включающую все результаты тестирования из соответствующих проектов модульного теста.</span><span class="sxs-lookup"><span data-stu-id="1d06a-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="1d06a-186">На [классическом портале Azure](http://go.microsoft.com/fwlink/?LinkID=213885)можно увидеть соответствующее развертывание на вкладке **Развертывания** , выбрав промежуточную среду.</span><span class="sxs-lookup"><span data-stu-id="1d06a-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="1d06a-187">Перейдите по URL-адресу вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="1d06a-187">Browse to your site's URL.</span></span> <span data-ttu-id="1d06a-188">Для веб-приложения достаточно нажать на портале кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="1d06a-189">Для облачной службы выберите URL-адрес в разделе **Сводка** страницы **Панель мониторинга**, показывающей промежуточную среду.</span><span class="sxs-lookup"><span data-stu-id="1d06a-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="1d06a-190">Развертывания из решений непрерывной интеграции для облачных служб по умолчанию публикуются в промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="1d06a-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="1d06a-191">Чтобы изменить это поведение, присвойте свойству **Альтернативная среда облачной службы** значение **Рабочая среда**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="1d06a-192">На этом снимке экрана показано, где на панели мониторинга облачной службы находится URL-адрес сайта:</span><span class="sxs-lookup"><span data-stu-id="1d06a-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="1d06a-193">Сайт откроется на новой вкладке браузера.</span><span class="sxs-lookup"><span data-stu-id="1d06a-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="1d06a-194">При внесении других изменений в проект запускаются дополнительные процессы построения, в результате чего создается несколько развертываний.</span><span class="sxs-lookup"><span data-stu-id="1d06a-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="1d06a-195">Последнее из них отмечается как активное.</span><span class="sxs-lookup"><span data-stu-id="1d06a-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="1d06a-196">5. Повторное развертывание предыдущей сборки</span><span class="sxs-lookup"><span data-stu-id="1d06a-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="1d06a-197">Этот шаг не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="1d06a-197">This step is optional.</span></span> <span data-ttu-id="1d06a-198">Чтобы восстановить состояние сайта на момент более раннего возврата, выберите предыдущее развертывание на классическом портале Azure и нажмите кнопку **Повторное развертывание** .</span><span class="sxs-lookup"><span data-stu-id="1d06a-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="1d06a-199">Обратите внимание, что при этом в TFS будет запущен новый процесс сборки, а в историю развертывания будет добавлена новая запись.</span><span class="sxs-lookup"><span data-stu-id="1d06a-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="1d06a-200">6. Изменение развертывания в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="1d06a-200">6: Change the Production deployment</span></span>
<span data-ttu-id="1d06a-201">Выполнив все необходимые действия, вы можете повысить промежуточную среду до рабочей с помощью кнопки **Переключить** на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="1d06a-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="1d06a-202">Вновь развернутая промежуточная среда повышается до уровня рабочей, а ранее установленная рабочая среда становится промежуточной.</span><span class="sxs-lookup"><span data-stu-id="1d06a-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="1d06a-203">Рабочая и промежуточная среды могут использовать разные активные развертывания, однако история развертывания последних сборок будет содержать одинаковые записи независимо от выбранной среды.</span><span class="sxs-lookup"><span data-stu-id="1d06a-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="1d06a-204">7. Развертывание из рабочей ветви</span><span class="sxs-lookup"><span data-stu-id="1d06a-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="1d06a-205">При использовании Git изменения обычно вносятся в рабочей ветви и интегрируются в главную ветвь, когда развертывание достигает завершенного состояния.</span><span class="sxs-lookup"><span data-stu-id="1d06a-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="1d06a-206">На этапе развертывания проекта можно выполнить построение и развертывание рабочей ветви в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d06a-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="1d06a-207">В обозревателе **Team Explorer** нажмите кнопку **Домашняя страница**, а затем — **Ветви**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="1d06a-208">Выберите ссылку **Новая ветвь** .</span><span class="sxs-lookup"><span data-stu-id="1d06a-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="1d06a-209">Введите имя ветви, например "working", и нажмите кнопку **Создать ветвь**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="1d06a-210">Будет создана новая локальная ветвь.</span><span class="sxs-lookup"><span data-stu-id="1d06a-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="1d06a-211">Опубликуйте эту ветвь.</span><span class="sxs-lookup"><span data-stu-id="1d06a-211">Publish the branch.</span></span> <span data-ttu-id="1d06a-212">Выберите имя ветви в разделе **Неопубликованные ветви** и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="1d06a-213">По умолчанию только изменения главной ветви вызывают непрерывное построение.</span><span class="sxs-lookup"><span data-stu-id="1d06a-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="1d06a-214">Чтобы настроить непрерывную сборку для рабочей ветви, перейдите на **страницу сборок** в **Team Explorer** и выберите **Редактировать определение сборки**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="1d06a-215">Перейдите на вкладку **исходных параметров** .</span><span class="sxs-lookup"><span data-stu-id="1d06a-215">Open the **Source Settings** tab.</span></span> <span data-ttu-id="1d06a-216">В разделе **Monitored branches for continuous integration and build** (Отслеживаемые ветви для сборок с непрерывной интеграцией и периодических сборок) выберите **Щелкните здесь для добавления строки**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-216">Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="1d06a-217">Укажите созданную ветвь, например, refs/heads/working.</span><span class="sxs-lookup"><span data-stu-id="1d06a-217">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="1d06a-218">Внесите изменения в код, откройте контекстное меню измененного файла и выберите команду **Зафиксировать**.</span><span class="sxs-lookup"><span data-stu-id="1d06a-218">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="1d06a-219">Выберите ссылку **Несинхронизированные фиксации** и нажмите кнопку **Синхронизировать** или выберите ссылку **Отправить**, чтобы скопировать изменения в копию рабочей ветви в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1d06a-219">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="1d06a-220">Перейдите в представление **построений** и найдите построение, которое только что было вызвано для рабочей ветви.</span><span class="sxs-lookup"><span data-stu-id="1d06a-220">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d06a-221">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d06a-221">Next steps</span></span>
<span data-ttu-id="1d06a-222">Дополнительные советы по использованию Git в Visual Studio Team Services см. в статье с описанием [совместного использования кода в Git](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017), а сведения об использовании для публикации в Azure репозитория Git, не управляемого с помощью Visual Studio Team Services, — в статье [Непрерывное развертывание в службе приложений Azure](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="1d06a-222">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="1d06a-223">Дополнительные сведения о Visual Studio Team Services см. [здесь](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="1d06a-223">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
