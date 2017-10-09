---
title: "aaaContinuous доставки с Visual Studio Team Services в Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure в Visual Studio Team Services командные проекты tooautomatically построение и развертывание компонентов toohello веб-приложения в службе приложений Azure или облачных служб."
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
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a><span data-ttu-id="99a9a-103">TooAzure непрерывной поставки с помощью Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="99a9a-103">Continuous delivery tooAzure using Visual Studio Team Services</span></span>
<span data-ttu-id="99a9a-104">Можно настроить сборку tooautomatically командных проектов Visual Studio Team Services и развернуть tooAzure веб-приложений или облачных служб.</span><span class="sxs-lookup"><span data-stu-id="99a9a-104">You can configure your Visual Studio Team Services team projects tooautomatically build and deploy tooAzure web apps or cloud services.</span></span>  <span data-ttu-id="99a9a-105">(Дополнительные сведения о предоставлении tooset вверх непрерывное построение и развертывание с помощью системы *локальной* Team Foundation Server. в разделе [непрерывная доставка для облачных служб в Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="99a9a-105">(For information on how tooset up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="99a9a-106">В учебнике предполагается, что у вас есть Visual Studio 2013 и hello установленный пакет SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="99a9a-106">This tutorial assumes you have Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="99a9a-107">Если у вас еще нет Visual Studio 2013, загрузите ее, выбрав hello **начните бесплатно** связи [www.visualstudio.com](http://www.visualstudio.com). Здравствуйте, установка пакета Azure SDK с [здесь](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="99a9a-107">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="99a9a-108">Требуется учетная запись Visual Studio Team Services toocomplete этого учебника: вы можете [открыть учетную запись Visual Studio Team Services бесплатно](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="99a9a-108">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="99a9a-109">tooset копирование tooautomatically облачной службы построения и развертывания tooAzure с помощью Visual Studio Team Services, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="99a9a-109">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="99a9a-110">1. Создание командного проекта</span><span class="sxs-lookup"><span data-stu-id="99a9a-110">1: Create a team project</span></span>
<span data-ttu-id="99a9a-111">Следуйте инструкциям hello [здесь](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate вашего командного проекта и связать его tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="99a9a-111">Follow hello instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate your team project and link it tooVisual Studio.</span></span> <span data-ttu-id="99a9a-112">В этом руководстве в качестве системы управления версиями применяется Team Foundation Version Control (TFVC).</span><span class="sxs-lookup"><span data-stu-id="99a9a-112">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="99a9a-113">Если требуется toouse Git для управления версиями. в разделе [hello Git версию данного пошагового руководства](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="99a9a-113">If you want toouse Git for version control, see [hello Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-toosource-control"></a><span data-ttu-id="99a9a-114">2: проверка в элементе управления toosource проекта</span><span class="sxs-lookup"><span data-stu-id="99a9a-114">2: Check in a project toosource control</span></span>
1. <span data-ttu-id="99a9a-115">В Visual Studio откройте решение hello toodeploy, или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="99a9a-115">In Visual Studio, open hello solution you want toodeploy, or create a new one.</span></span>
   <span data-ttu-id="99a9a-116">Можно развернуть веб-приложения или облачной службы (приложение Azure), hello следующие шаги в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="99a9a-116">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span>
   <span data-ttu-id="99a9a-117">Если вы хотите toocreate новое решение, создайте новый проект облачной службы Azure или новый проект ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="99a9a-117">If you want toocreate a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="99a9a-118">Проверьте правильность hello нацелен проект .NET Framework 4 или 4.5 и при создании проекта облачной службы, добавьте веб-роль ASP.NET MVC и рабочей роли и выберите веб-приложение hello веб-роли.</span><span class="sxs-lookup"><span data-stu-id="99a9a-118">Make sure that hello project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for hello web role.</span></span> <span data-ttu-id="99a9a-119">При появлении запроса выберите **Интернет-приложение**.</span><span class="sxs-lookup"><span data-stu-id="99a9a-119">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="99a9a-120">Если вы хотите toocreate веб-приложения, выбрав шаблон проекта веб-приложения ASP.NET hello и выберите MVC.</span><span class="sxs-lookup"><span data-stu-id="99a9a-120">If you want toocreate a web app, choose hello ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="99a9a-121">Ознакомьтесь со сведениями в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="99a9a-121">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="99a9a-122">В настоящее время Visual Studio Team Services поддерживают только развертывания непрерывной интеграции веб-приложений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99a9a-122">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="99a9a-123">Проекты веб-сайтов выходят за эти рамки.</span><span class="sxs-lookup"><span data-stu-id="99a9a-123">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="99a9a-124">Откройте контекстное меню решения hello hello и выберите **tooSource добавить решение управления**.</span><span class="sxs-lookup"><span data-stu-id="99a9a-124">Open hello context menu for hello solution, and choose **Add Solution tooSource Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="99a9a-125">Принять или изменить значения по умолчанию hello и выбрать hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="99a9a-125">Accept or change hello defaults and choose hello **OK** button.</span></span> <span data-ttu-id="99a9a-126">После завершения процесса hello значки системы управления версиями появляются в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="99a9a-126">Once hello process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="99a9a-127">Откройте контекстное меню hello hello решения и выберите **вернуть**.</span><span class="sxs-lookup"><span data-stu-id="99a9a-127">Open hello shortcut menu for hello solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="99a9a-128">В hello **ожидающие изменения** область **Team Explorer**, введите комментарий для возврата hello и выберите hello **вернуть** кнопки.</span><span class="sxs-lookup"><span data-stu-id="99a9a-128">In hello **Pending Changes** area of **Team Explorer**, type a comment for hello check-in and choose hello **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="99a9a-129">Обратите внимание, tooinclude параметры hello или исключить определенных изменений при возврате.</span><span class="sxs-lookup"><span data-stu-id="99a9a-129">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="99a9a-130">При необходимости изменения исключаются выберите hello **включить все** ссылку.</span><span class="sxs-lookup"><span data-stu-id="99a9a-130">If desired changes are excluded, choose hello **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="99a9a-131">3: hello проекта tooAzure подключения</span><span class="sxs-lookup"><span data-stu-id="99a9a-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="99a9a-132">Теперь, когда командного проекта VS Team Services с помощью исходного кода, в нем используется готов tooconnect командного проекта tooAzure.</span><span class="sxs-lookup"><span data-stu-id="99a9a-132">Now that you have a VS Team Services team project with some source code in it, you are ready tooconnect your team project tooAzure.</span></span>  <span data-ttu-id="99a9a-133">В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885)выберите облачной службы или веб-приложения, или создать новый, выбрав hello  **+**  значок в левом нижнем hello и выбрав **облачной службы** или **веб-приложения** и затем **быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="99a9a-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello **+** icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="99a9a-134">Выберите hello **Настройка публикации с использованием Visual Studio Team Services** ссылку.</span><span class="sxs-lookup"><span data-stu-id="99a9a-134">Choose hello **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="99a9a-135">В мастере hello, введите в текстовом поле hello hello имя вашей учетной записи Visual Studio Team Services, а затем нажмите кнопку hello **авторизовать теперь** ссылку.</span><span class="sxs-lookup"><span data-stu-id="99a9a-135">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and click hello **Authorize Now** link.</span></span> <span data-ttu-id="99a9a-136">Вас попросят toosign в.</span><span class="sxs-lookup"><span data-stu-id="99a9a-136">You might be asked toosign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="99a9a-137">В hello **запроса на подключение** всплывающем диалоговом окне выберите hello **Accept** tooauthorize кнопку Azure tooconfigure командного проекта в VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="99a9a-137">In hello **Connection Request** pop-up dialog, choose hello **Accept** button tooauthorize Azure tooconfigure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="99a9a-138">После успешной авторизации появится раскрывающийся список, в котором будут представлены ваши командные проекты Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="99a9a-138">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="99a9a-139">Выберите имя командного проекта, созданного на предыдущих этапах hello hello и нажмите кнопку флажок приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="99a9a-139">Choose  hello name of team project that you created in hello previous steps, and then choose hello wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="99a9a-140">После связывания проекта, вы увидите некоторые инструкции по возврату изменений tooyour Visual Studio Team Services командного проекта.</span><span class="sxs-lookup"><span data-stu-id="99a9a-140">After your project is linked, you will see some instructions for checking in changes tooyour Visual Studio Team Services team project.</span></span>  <span data-ttu-id="99a9a-141">На следующем возвратом Visual Studio Team Services создаст и развернет ваш проект tooAzure.</span><span class="sxs-lookup"><span data-stu-id="99a9a-141">On your next check-in, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>  <span data-ttu-id="99a9a-142">Попробуйте сейчас, щелкнув hello **возврата из Visual Studio** связь, а затем hello **запуска Visual Studio** ссылки (или эквивалентное hello **Visual Studio** кнопку внизу hello Hello экрана портала).</span><span class="sxs-lookup"><span data-stu-id="99a9a-142">Try this now by clicking hello **Check In from Visual Studio** link, and then hello **Launch Visual Studio** link (or hello equivalent **Visual Studio** button at hello bottom of hello portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="99a9a-143">4. Запуск процессов повторного построения и развертывания проекта</span><span class="sxs-lookup"><span data-stu-id="99a9a-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="99a9a-144">В Visual Studio **Team Explorer**, выберите hello **обозревателя управления исходным кодом** ссылку.</span><span class="sxs-lookup"><span data-stu-id="99a9a-144">In Visual Studio's **Team Explorer**, choose hello **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="99a9a-145">Файл решения tooyour перейдите и откройте его.</span><span class="sxs-lookup"><span data-stu-id="99a9a-145">Navigate tooyour solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="99a9a-146">Откройте и измените файл в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="99a9a-146">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="99a9a-147">Например, измените файл hello `_Layout.cshtml` в области представления hello\\общая папка в веб-роли MVC.</span><span class="sxs-lookup"><span data-stu-id="99a9a-147">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="99a9a-148">Эмблема hello hello сайта и затем выберите **Ctrl + S** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="99a9a-148">Edit hello logo for hello site and choose **Ctrl+S** toosave hello file.</span></span>
   
    ![][18]
5. <span data-ttu-id="99a9a-149">В **Team Explorer**, выберите hello **ожидающие изменения** ссылку.</span><span class="sxs-lookup"><span data-stu-id="99a9a-149">In **Team Explorer**, choose hello **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="99a9a-150">Введите комментарий и нажмите кнопку hello **вернуть** кнопки.</span><span class="sxs-lookup"><span data-stu-id="99a9a-150">Enter a comment and then choose hello **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="99a9a-151">Выберите hello **домашней** toohello tooreturn кнопку **Team Explorer** домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="99a9a-151">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="99a9a-152">Выберите hello **строит** hello tooview ссылка сборки в данный момент.</span><span class="sxs-lookup"><span data-stu-id="99a9a-152">Choose hello **Builds** link tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="99a9a-153">**Team Explorer** отображается информация о том, что для вашего возврата запущен процесс сборки.</span><span class="sxs-lookup"><span data-stu-id="99a9a-153">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="99a9a-154">Дважды щелкните имя hello построения hello в ход выполнения tooview подробный журнал hello процессе построения.</span><span class="sxs-lookup"><span data-stu-id="99a9a-154">Double-click hello name of hello build in progress tooview a detailed log as hello build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="99a9a-155">Пока сборка hello в процессе выполнения, взгляните на определение сборки hello, который был создан при компоновке TFS tooAzure с помощью мастера hello.</span><span class="sxs-lookup"><span data-stu-id="99a9a-155">While hello build is in-progress, take a look at hello build definition that was created when you linked TFS tooAzure by using hello wizard.</span></span>  <span data-ttu-id="99a9a-156">Откройте контекстное меню определения сборки hello hello и выберите **Редактировать определение построения**.</span><span class="sxs-lookup"><span data-stu-id="99a9a-156">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="99a9a-157">В hello **триггер** вкладку, вы увидите, определение сборки hello toobuild на каждом возврате по умолчанию имеет значение.</span><span class="sxs-lookup"><span data-stu-id="99a9a-157">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="99a9a-158">В hello **процесс** вкладку, вы увидите установки среды развертывания hello toohello имя облачной службы или веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="99a9a-158">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span> <span data-ttu-id="99a9a-159">При работе с веб-приложения hello свойства, отображаемые будет отличаться от тех, которые здесь показаны.</span><span class="sxs-lookup"><span data-stu-id="99a9a-159">If you are working with web apps, hello properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="99a9a-160">Укажите значения для свойств hello различных значений, чем значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="99a9a-160">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="99a9a-161">Hello свойства для публикации Azure находятся в hello **развертывания** раздела.</span><span class="sxs-lookup"><span data-stu-id="99a9a-161">hello properties for Azure publishing are in hello **Deployment** section.</span></span>
    
     <span data-ttu-id="99a9a-162">Hello следующей таблице показаны доступные свойства hello в hello **развертывания** раздела:</span><span class="sxs-lookup"><span data-stu-id="99a9a-162">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="99a9a-163">Свойство</span><span class="sxs-lookup"><span data-stu-id="99a9a-163">Property</span></span> | <span data-ttu-id="99a9a-164">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="99a9a-164">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="99a9a-165">Разрешить недоверенные сертификаты</span><span class="sxs-lookup"><span data-stu-id="99a9a-165">Allow Untrusted Certificates</span></span> |<span data-ttu-id="99a9a-166">Если установлено значение false, то SSL-сертификаты должны быть подписаны корневым центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="99a9a-166">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="99a9a-167">Разрешить обновление</span><span class="sxs-lookup"><span data-stu-id="99a9a-167">Allow Upgrade</span></span> |<span data-ttu-id="99a9a-168">Позволяет tooupdate развертывания hello существующего развертывания вместо создания нового.</span><span class="sxs-lookup"><span data-stu-id="99a9a-168">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="99a9a-169">Сохраняет hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="99a9a-169">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="99a9a-170">Не удалять</span><span class="sxs-lookup"><span data-stu-id="99a9a-170">Do Not Delete</span></span> |<span data-ttu-id="99a9a-171">Если установлено значение true, не разрешена перезапись существующего несвязанного развертывания (обновление разрешено).</span><span class="sxs-lookup"><span data-stu-id="99a9a-171">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="99a9a-172">Путь tooDeployment параметры</span><span class="sxs-lookup"><span data-stu-id="99a9a-172">Path tooDeployment Settings</span></span> |<span data-ttu-id="99a9a-173">Hello путь tooyour pubxml-файл для веб-приложения, относительного toohello корневой папки репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="99a9a-173">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="99a9a-174">Для облачных служб игнорируется.</span><span class="sxs-lookup"><span data-stu-id="99a9a-174">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="99a9a-175">Среда развертывания Sharepoint</span><span class="sxs-lookup"><span data-stu-id="99a9a-175">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="99a9a-176">Здравствуйте таким же, как имя службы hello.</span><span class="sxs-lookup"><span data-stu-id="99a9a-176">hello same as hello service name.</span></span> |
    | <span data-ttu-id="99a9a-177">Среда развертывания Azure</span><span class="sxs-lookup"><span data-stu-id="99a9a-177">Azure Deployment Environment</span></span> |<span data-ttu-id="99a9a-178">Hello имя веб-приложения или облачной службы.</span><span class="sxs-lookup"><span data-stu-id="99a9a-178">hello web app or cloud service name.</span></span> |
12. <span data-ttu-id="99a9a-179">Если вы используете несколько конфигураций службы (cscfg-файлы), можно указать hello соответствующей конфигурации в hello **сборки, Дополнительно, Аргументы MSBuild** параметр.</span><span class="sxs-lookup"><span data-stu-id="99a9a-179">If you are using multiple service configurations (.cscfg files), you can specify hello desired service configuration in hello **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="99a9a-180">Например, toouse ServiceConfiguration.Test.cscfg, задайте аргументы MSBuild параметр строки `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="99a9a-180">For example, toouse ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="99a9a-181">К этому моменту процесс построения должен быть успешно завершен.</span><span class="sxs-lookup"><span data-stu-id="99a9a-181">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="99a9a-182">Если дважды щелкнуть имя сборки hello, Visual Studio отображает **сводки построения**, включая результатов теста из связанных проектов модульных тестов.</span><span class="sxs-lookup"><span data-stu-id="99a9a-182">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="99a9a-183">В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885), вы можете просмотреть связанные hello развертывания на hello **развертываний** вкладке при выборе hello в промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="99a9a-183">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="99a9a-184">URL-адрес сайта tooyour обзора.</span><span class="sxs-lookup"><span data-stu-id="99a9a-184">Browse tooyour site's URL.</span></span> <span data-ttu-id="99a9a-185">Для веб-приложения, просто щелкните hello **Обзор** кнопки на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="99a9a-185">For a web app, just click hello **Browse** button on hello command bar.</span></span> <span data-ttu-id="99a9a-186">Для облачной службы, выберите URL-адрес hello в hello **быстрый обзор** раздел hello **мониторинга** страницы, отображающей hello промежуточной среде для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="99a9a-186">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment for a cloud service.</span></span> <span data-ttu-id="99a9a-187">Развертывания с непрерывной интеграции для облачных служб — опубликованных toohello промежуточной среды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="99a9a-187">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="99a9a-188">Это можно изменить, установка hello **альтернативное окружение облачной службы** свойство слишком**рабочей**.</span><span class="sxs-lookup"><span data-stu-id="99a9a-188">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="99a9a-189">Этом снимке экрана показана там, где hello URL-адрес сайта находится на странице панели мониторинга hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="99a9a-189">This screenshot shows where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="99a9a-190">На новой вкладке браузера откроется tooreveal выполнение веб-узла.</span><span class="sxs-lookup"><span data-stu-id="99a9a-190">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="99a9a-191">Для облачных служб при внесении других изменений tooyour проекта, то триггер более строит и накапливаются несколько развертываний.</span><span class="sxs-lookup"><span data-stu-id="99a9a-191">For cloud services, if you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="99a9a-192">Hello последнего помечен как активный.</span><span class="sxs-lookup"><span data-stu-id="99a9a-192">hello latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="99a9a-193">5. Повторное развертывание предыдущей сборки</span><span class="sxs-lookup"><span data-stu-id="99a9a-193">5: Redeploy an earlier build</span></span>
<span data-ttu-id="99a9a-194">Этот шаг применяется toocloud службы и является необязательным.</span><span class="sxs-lookup"><span data-stu-id="99a9a-194">This step applies toocloud services and is optional.</span></span> <span data-ttu-id="99a9a-195">В hello классический портал Azure, выберите более ранних развертывания и выберите hello **повторно развернуть** кнопку toorewind вашего сайта tooan ранее возврата.</span><span class="sxs-lookup"><span data-stu-id="99a9a-195">In hello Azure classic portal, choose an earlier deployment and then choose hello **Redeploy** button toorewind your site tooan earlier check-in.</span></span>  <span data-ttu-id="99a9a-196">Обратите внимание, что при этом в TFS будет запущен новый процесс сборки, а в историю развертывания будет добавлена новая запись.</span><span class="sxs-lookup"><span data-stu-id="99a9a-196">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="99a9a-197">6: изменение hello рабочего развертывания</span><span class="sxs-lookup"><span data-stu-id="99a9a-197">6: Change hello Production deployment</span></span>
<span data-ttu-id="99a9a-198">Этот шаг применяется только toocloud службы, не веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="99a9a-198">This step applies only toocloud services, not web apps.</span></span> <span data-ttu-id="99a9a-199">Когда будете готовы, вы можете повысить уровень hello промежуточной toohello рабочей среды, выбрав hello **замены** кнопку в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="99a9a-199">When you are ready, you can promote hello Staging environment toohello production environment by choosing hello **Swap** button in hello Azure classic portal.</span></span> <span data-ttu-id="99a9a-200">вновь развернуть Hello промежуточной среды tooProduction повышенного уровня, а hello предыдущей рабочей среде, если таковые имеются, становится промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="99a9a-200">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="99a9a-201">Hello активное развертывание может быть разным для hello производственной и промежуточной сред, но История развертывания hello последних построений hello одинаково независимо от среды.</span><span class="sxs-lookup"><span data-stu-id="99a9a-201">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="99a9a-202">7. Выполнение модульных тестов</span><span class="sxs-lookup"><span data-stu-id="99a9a-202">7: Run unit tests</span></span>
<span data-ttu-id="99a9a-203">Этот шаг применяется только tooweb приложения, не облачных служб.</span><span class="sxs-lookup"><span data-stu-id="99a9a-203">This step applies only tooweb apps, not cloud services.</span></span> <span data-ttu-id="99a9a-204">tooput условия качества вашего развертывания, можно выполнять модульные тесты, и если они завершаются с ошибкой, можно остановить развертывание hello.</span><span class="sxs-lookup"><span data-stu-id="99a9a-204">tooput a quality gate on your deployment, you can run unit tests and if they fail, you can stop hello deployment.</span></span>

1. <span data-ttu-id="99a9a-205">В Visual Studio добавьте проект модульного теста.</span><span class="sxs-lookup"><span data-stu-id="99a9a-205">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="99a9a-206">Добавьте проект toohello ссылки проекта, требуется tootest.</span><span class="sxs-lookup"><span data-stu-id="99a9a-206">Add project references toohello project you want tootest.</span></span>
   
   ![][40]
3. <span data-ttu-id="99a9a-207">Добавьте модульные тесты.</span><span class="sxs-lookup"><span data-stu-id="99a9a-207">Add some unit tests.</span></span> <span data-ttu-id="99a9a-208">tooget запущена, попробуйте пустой тест, который всегда будет передавать.</span><span class="sxs-lookup"><span data-stu-id="99a9a-208">tooget started, try a dummy test that will always pass.</span></span>
   
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
4. <span data-ttu-id="99a9a-209">Измените определение сборки hello, выберите hello **процесс** и разверните hello **тест** узла.</span><span class="sxs-lookup"><span data-stu-id="99a9a-209">Edit hello build definition, choose hello **Process** tab, and expand hello **Test** node.</span></span>
5. <span data-ttu-id="99a9a-210">Набор hello **сбой сборки при ошибке теста** tooTrue.</span><span class="sxs-lookup"><span data-stu-id="99a9a-210">Set hello **Fail build on test failure** tooTrue.</span></span> <span data-ttu-id="99a9a-211">Это означает, что развертывание hello не появляется, если hello тесты проходят успешно.</span><span class="sxs-lookup"><span data-stu-id="99a9a-211">This means that hello deployment won't occur unless hello tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="99a9a-212">Поставьте новую сборку в очередь.</span><span class="sxs-lookup"><span data-stu-id="99a9a-212">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="99a9a-213">Во время построения hello продолжить, проверки хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="99a9a-213">While hello build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="99a9a-214">После завершения построения hello, проверьте результаты теста hello.</span><span class="sxs-lookup"><span data-stu-id="99a9a-214">When hello build is done, check hello test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="99a9a-215">Попробуйте создать тест, который выдаст отрицательный результат.</span><span class="sxs-lookup"><span data-stu-id="99a9a-215">Try creating a test that will fail.</span></span> <span data-ttu-id="99a9a-216">Добавьте новый тест, скопировав hello первый, переименовать его и закомментируйте строку hello кода о том, что NotImplementedException является ожидаемое исключение.</span><span class="sxs-lookup"><span data-stu-id="99a9a-216">Add a new test by copying hello first one, rename it, and comment out hello line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="99a9a-217">Возврат изменений tooqueue hello новую сборку.</span><span class="sxs-lookup"><span data-stu-id="99a9a-217">Check in hello change tooqueue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="99a9a-218">Просмотр hello toosee сведения о результатах теста о сбое hello.</span><span class="sxs-lookup"><span data-stu-id="99a9a-218">View hello test results toosee details about hello failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="99a9a-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="99a9a-219">Next steps</span></span>
<span data-ttu-id="99a9a-220">Дополнительные сведения о модульном тестировании в Visual Studio Team Services см. в разделе [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474) (Выполнение тестов в процессе сборки).</span><span class="sxs-lookup"><span data-stu-id="99a9a-220">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="99a9a-221">Если вы используете Git, см. раздел [совместного использования кода в Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) и [tooAzure непрерывного развертывания службы приложений](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="99a9a-221">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="99a9a-222">Дополнительные сведения о Visual Studio Team Services см. [здесь](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="99a9a-222">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
