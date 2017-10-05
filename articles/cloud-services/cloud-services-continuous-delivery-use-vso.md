---
title: "Непрерывная поставка в Azure с использованием Visual Studio Team Services | Документация Майкрософт"
description: "Узнайте, как настроить командные проекты Visual Studio Team Services для автоматического выполнения сборки и развертывания в веб-приложения в службе приложений Azure и облачные службы."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="2d1e7-103">Непрерывная доставка в Azure с использованием Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="2d1e7-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="2d1e7-104">Вы можете настроить командные проекты Visual Studio Team Services для автоматического выполнения сборки и развертывания в облачные службы или веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="2d1e7-105">(Дополнительные сведения о настройке непрерывного процесса сборки и развертывания системы с использованием *локального* решения Team Foundation Server см. в статье [Непрерывная поставка для облачных служб в Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="2d1e7-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="2d1e7-106">В данном учебнике предполагается, что у вас установлены решения Visual Studio 2013 и пакет SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="2d1e7-107">Чтобы загрузить Visual Studio 2013, щелкните ссылку **Начните работу бесплатно** на сайте [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="2d1e7-108">Пакет SDK Azure можно установить по [этой ссылке](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="2d1e7-109">Для работы с этим руководством необходима учетная запись Visual Studio Team Services. Вы можете [бесплатно зарегистрировать учетную запись Visual Studio Team Services](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="2d1e7-110">Чтобы настроить автоматическое выполнение сборки и развертывания облачной службы в Azure с использованием Visual Studio Team Services, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="2d1e7-111">1. Создание командного проекта</span><span class="sxs-lookup"><span data-stu-id="2d1e7-111">1: Create a team project</span></span>
<span data-ttu-id="2d1e7-112">Следуйте указаниям, приведенным [здесь](http://go.microsoft.com/fwlink/?LinkId=512980), чтобы создать командный проект и связать его с Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="2d1e7-113">В этом руководстве в качестве системы управления версиями применяется Team Foundation Version Control (TFVC).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="2d1e7-114">Если для управления версиями вы хотите использовать Git, см. [версию этого руководства для Git](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="2d1e7-115">2. Регистрация проекта в системе управления версиями</span><span class="sxs-lookup"><span data-stu-id="2d1e7-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="2d1e7-116">В Visual Studio откройте решение, которое вы хотите развернуть, или создайте новое.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="2d1e7-117">В этом пошаговом руководстве представлены инструкции по развертыванию веб-приложения или облачной службы (приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="2d1e7-118">Чтобы создать новое решение, создайте новый проект облачной службы Azure или новый проект MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="2d1e7-119">Убедитесь, что в проекте используется платформа .NET Framework 4 или 4.5 и создается проект облачной службы, добавьте рабочую роль и веб-роль ASP.NET MVC, после чего выберите интернет-приложение для веб-роли.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="2d1e7-120">При появлении запроса выберите **Интернет-приложение**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="2d1e7-121">Чтобы создать веб-приложение, выберите шаблон проекта "Веб-приложение ASP.NET" и затем выберите MVC.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="2d1e7-122">Ознакомьтесь со сведениями в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2d1e7-123">В настоящее время Visual Studio Team Services поддерживают только развертывания непрерывной интеграции веб-приложений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="2d1e7-124">Проекты веб-сайтов выходят за эти рамки.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="2d1e7-125">Откройте контекстное меню решения и выберите **Добавить решение в систему управления версиями**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="2d1e7-126">Примите предлагаемые по умолчанию параметры или измените их, после чего нажмите кнопку **ОК** .</span><span class="sxs-lookup"><span data-stu-id="2d1e7-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="2d1e7-127">По завершении обработки в **обозревателе решений**появится значок системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="2d1e7-128">Откройте контекстное меню решения и выберите пункт **Регистрация**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="2d1e7-129">В области **Ожидающие изменения** в обозревателе **Team Explorer** введите примечание для регистрации и нажмите кнопку **Регистрация**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="2d1e7-130">Обратите внимание на варианты для включения или исключения определенных изменений при настройке.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="2d1e7-131">Если нужные изменения исключаются, нажмите ссылку **Включить все** .</span><span class="sxs-lookup"><span data-stu-id="2d1e7-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="2d1e7-132">3. Подключение проекта к Azure</span><span class="sxs-lookup"><span data-stu-id="2d1e7-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="2d1e7-133">Теперь, когда создан командный проект VS Team Services с определенным исходным кодом, вы можете подключить его к Azure.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="2d1e7-134">Войдите на [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885) и выберите существующую облачную службу или веб-приложение. Вы также можете создать новые объекты, щелкнув в нижнем левом углу значок **+**, а затем выбрав **Облачная служба** или **Веб-приложение** и **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="2d1e7-135">Щелкните ссылку **Set up publishing with Visual Studio Team Services** (Настройка публикации в Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="2d1e7-136">В мастере введите имя учетной записи Visual Studio Team Services в соответствующем поле и щелкните ссылку **Авторизовать сейчас** .</span><span class="sxs-lookup"><span data-stu-id="2d1e7-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="2d1e7-137">Может появиться запрос на вход в систему.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="2d1e7-138">Во всплывающем диалоговом окне **Connection Request** (Запрос на подключение) нажмите кнопку **Принять**, чтобы предоставить Azure полномочия для настройки командного проекта в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="2d1e7-139">После успешной авторизации появится раскрывающийся список, в котором будут представлены ваши командные проекты Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="2d1e7-140">Щелкните имя созданного на предыдущих шагах командного проекта и нажмите кнопку с галочкой в мастере.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="2d1e7-141">После привязки проекта появятся инструкции по проверке изменений в командном проекте Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="2d1e7-142">При следующем возврате данных после изменения Visual Studio Team Services выполнит сборку и развертывание вашего проекта в Azure.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="2d1e7-143">Чтобы проверить реализованное поведение, щелкните ссылку **Check In from Visual Studio** (Регистрация из Visual Studio), а затем ссылку **Launch Visual Studio** (Запустить Visual Studio) (или аналогичную кнопку **Visual Studio** в нижней части окна портала).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="2d1e7-144">4. Запуск процессов повторного построения и развертывания проекта</span><span class="sxs-lookup"><span data-stu-id="2d1e7-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="2d1e7-145">В обозревателе **Visual Studio Team Explorer** щелкните ссылку **Обозреватель управления исходным кодом**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="2d1e7-146">Перейдите к файлу решения и откройте его.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="2d1e7-147">Откройте и измените файл в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="2d1e7-148">Например, вы можете изменить файл `_Layout.cshtml` в папке Views\\Shared веб-роли MVC.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="2d1e7-149">Измените логотип сайта и сохраните этот файл с помощью клавиш **CTRL + S** .</span><span class="sxs-lookup"><span data-stu-id="2d1e7-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="2d1e7-150">В обозревателе **Team Explorer** щелкните ссылку **Ожидающие изменения**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="2d1e7-151">Введите комментарий и нажмите кнопку **Регистрация** .</span><span class="sxs-lookup"><span data-stu-id="2d1e7-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="2d1e7-152">Нажмите кнопку **Домашняя страница**, чтобы вернуться на домашнюю страницу **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="2d1e7-153">Щелкните ссылку **Сборки** , чтобы просмотреть выполняющиеся сборки.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="2d1e7-154">**Team Explorer** отображается информация о том, что для вашего возврата запущен процесс сборки.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="2d1e7-155">Дважды щелкните имя выполняемой сборки, чтобы просмотреть подробный журнал процесса построения.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="2d1e7-156">В процессе построения вы можете просмотреть определение сборки, созданное во время привязки TFS к Azure с помощью мастера.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="2d1e7-157">Откройте контекстное меню определения сборки и выберите **Редактировать определение сборки**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="2d1e7-158">На вкладке **Триггер** указывается, что в определении сборки настроено выполнение сборки по умолчанию при каждой регистрации.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="2d1e7-159">На вкладке **Процесс** указывается, что в среде разработки настроено имя ваших облачной веб-службы или веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="2d1e7-160">При работе с веб-приложениями здесь будут показаны другие свойства.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="2d1e7-161">При необходимости измените установленные по умолчанию значения свойств.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="2d1e7-162">Свойства публикации Azure находятся в разделе **Развертывание** .</span><span class="sxs-lookup"><span data-stu-id="2d1e7-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="2d1e7-163">В следующей таблице приводятся доступные свойства в разделе **Развертывание** :</span><span class="sxs-lookup"><span data-stu-id="2d1e7-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="2d1e7-164">Свойство</span><span class="sxs-lookup"><span data-stu-id="2d1e7-164">Property</span></span> | <span data-ttu-id="2d1e7-165">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2d1e7-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="2d1e7-166">Разрешить недоверенные сертификаты</span><span class="sxs-lookup"><span data-stu-id="2d1e7-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="2d1e7-167">Если установлено значение false, то SSL-сертификаты должны быть подписаны корневым центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="2d1e7-168">Разрешить обновление</span><span class="sxs-lookup"><span data-stu-id="2d1e7-168">Allow Upgrade</span></span> |<span data-ttu-id="2d1e7-169">Разрешает обновление существующего развертывания вместо создания нового.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="2d1e7-170">Сохраняет IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="2d1e7-171">Не удалять</span><span class="sxs-lookup"><span data-stu-id="2d1e7-171">Do Not Delete</span></span> |<span data-ttu-id="2d1e7-172">Если установлено значение true, не разрешена перезапись существующего несвязанного развертывания (обновление разрешено).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="2d1e7-173">Путь к параметрам развертывания</span><span class="sxs-lookup"><span data-stu-id="2d1e7-173">Path to Deployment Settings</span></span> |<span data-ttu-id="2d1e7-174">Путь к PUBXML-файлу для веб-приложения относительно корневой папки репозитория.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="2d1e7-175">Для облачных служб игнорируется.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="2d1e7-176">Среда развертывания Sharepoint</span><span class="sxs-lookup"><span data-stu-id="2d1e7-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="2d1e7-177">Совпадает с именем службы.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-177">The same as the service name.</span></span> |
    | <span data-ttu-id="2d1e7-178">Среда развертывания Azure</span><span class="sxs-lookup"><span data-stu-id="2d1e7-178">Azure Deployment Environment</span></span> |<span data-ttu-id="2d1e7-179">Имя веб-приложения или облачной службы</span><span class="sxs-lookup"><span data-stu-id="2d1e7-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="2d1e7-180">Если используется несколько конфигураций служб (CSCFG-файлов), можно указать желаемую конфигурацию службы в параметрах **Сборка, Дополнительно, Аргументы MSBuild** .</span><span class="sxs-lookup"><span data-stu-id="2d1e7-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="2d1e7-181">Например, чтобы использовать файл ServiceConfiguration.Test.cscfg, задайте аргумент командной строки MSBuild `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="2d1e7-182">К этому моменту процесс построения должен быть успешно завершен.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="2d1e7-183">Если дважды щелкнуть имя сборки, Visual Studio отобразит **сводку сборки**, включающую все результаты тестирования из соответствующих проектов модульного теста.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="2d1e7-184">На [классическом портале Azure](http://go.microsoft.com/fwlink/?LinkID=213885)можно увидеть соответствующее развертывание на вкладке **Развертывания** , выбрав промежуточную среду.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="2d1e7-185">Перейдите по URL-адресу вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-185">Browse to your site's URL.</span></span> <span data-ttu-id="2d1e7-186">Для веб-приложения достаточно нажать кнопку **Обзор** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="2d1e7-187">Для облачной службы выберите URL-адрес в разделе **Сводка** на странице **Панель мониторинга**, где отображается промежуточная среда для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="2d1e7-188">Развертывания из решений непрерывной интеграции для облачных служб по умолчанию публикуются в промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="2d1e7-189">Чтобы изменить это поведение, присвойте свойству **Альтернативная среда облачной службы** значение **Рабочая среда**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="2d1e7-190">На этом снимке экрана показано местонахождение URL-адреса сайта на странице панели мониторинга облачной службы:</span><span class="sxs-lookup"><span data-stu-id="2d1e7-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="2d1e7-191">Сайт откроется на новой вкладке браузера.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="2d1e7-192">При внесении других изменений в проект для облачных служб запускаются дополнительные процессы построения, в результате чего создается несколько развертываний,</span><span class="sxs-lookup"><span data-stu-id="2d1e7-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="2d1e7-193">последнее из которых отмечается как активное.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="2d1e7-194">5. Повторное развертывание предыдущей сборки</span><span class="sxs-lookup"><span data-stu-id="2d1e7-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="2d1e7-195">Этот шаг необязателен и применяется к облачным службам.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="2d1e7-196">Чтобы восстановить состояние сайта на момент более ранней версии, выберите на классическом портале Azure какое-либо предыдущее развертывание и нажмите кнопку **Повторное развертывание** .</span><span class="sxs-lookup"><span data-stu-id="2d1e7-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="2d1e7-197">Обратите внимание, что при этом в TFS будет запущен новый процесс сборки, а в историю развертывания будет добавлена новая запись.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="2d1e7-198">6. Изменение развертывания в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="2d1e7-198">6: Change the Production deployment</span></span>
<span data-ttu-id="2d1e7-199">Этот шаг применяется только к облачным службам и недоступен для веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="2d1e7-200">Выполнив все необходимые действия, можно повысить промежуточную среду до рабочей с помощью кнопки **Переключить** классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="2d1e7-201">Вновь развернутая промежуточная среда повышается до уровня рабочей, а ранее установленная рабочая среда становится промежуточной.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="2d1e7-202">Рабочая и промежуточная среды могут использовать разные активные развертывания, однако история развертывания последних сборок будет содержать одинаковые записи независимо от выбранной среды.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="2d1e7-203">7. Выполнение модульных тестов</span><span class="sxs-lookup"><span data-stu-id="2d1e7-203">7: Run unit tests</span></span>
<span data-ttu-id="2d1e7-204">Этот шаг применяется только к веб-приложениям, не облачным службам.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="2d1e7-205">Чтобы поместить условия качества вашего развертывания, можно выполнять модульные тесты и, если они не могут остановить развертывание.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="2d1e7-206">В Visual Studio добавьте проект модульного теста.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="2d1e7-207">Добавление ссылки на проект в проект, который требуется проверить.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="2d1e7-208">Добавьте модульные тесты.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-208">Add some unit tests.</span></span> <span data-ttu-id="2d1e7-209">Сначала попробуйте фиктивный тест, который всегда выдает положительный результат.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-209">To get started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="2d1e7-210">Измените определение сборки, выберите вкладку **Процесс** и разверните узел **Test**.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="2d1e7-211">Установите для параметра **Завершить сборку при ошибке теста** значение True.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="2d1e7-212">Это означает, что развертывание не будет происходить, если тест не будет пройден положительно.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="2d1e7-213">Поставьте новую сборку в очередь.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="2d1e7-214">По мере обработки сборки проверяйте ход выполнения.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="2d1e7-215">По завершению сборки проверьте результаты теста.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="2d1e7-216">Попробуйте создать тест, который выдаст отрицательный результат.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-216">Try creating a test that will fail.</span></span> <span data-ttu-id="2d1e7-217">Добавьте новый тест путем копирования первой, переименовать его и закомментируйте строку кода, о том, что NotImplementedException является ожидаемое исключение.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="2d1e7-218">Примените изменения, чтобы поставить в очередь новую сборку.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="2d1e7-219">Просмотрите результаты теста и подробности отрицательного результата.</span><span class="sxs-lookup"><span data-stu-id="2d1e7-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="2d1e7-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2d1e7-220">Next steps</span></span>
<span data-ttu-id="2d1e7-221">Дополнительные сведения о модульном тестировании в Visual Studio Team Services см. в разделе [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474) (Выполнение тестов в процессе сборки).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="2d1e7-222">При использовании Git см. статьи с описанием [совместного использования кода в Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) и [непрерывного развертывания в службе приложений Azure](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="2d1e7-223">Дополнительные сведения о Visual Studio Team Services см. [здесь](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="2d1e7-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
