---
title: "aaaContinuous доставка для облачных служб с Team Foundation Server в Azure | Документы Microsoft"
description: "Дополнительные сведения об tooset копирование непрерывная доставка для Azure облачных приложений. Примеры программного кода для инструкций командной строки MSBuild и сценариев PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="4e194-104">Непрерывная доставка для облачных служб в Azure</span><span class="sxs-lookup"><span data-stu-id="4e194-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="4e194-105">Hello процесс, описанный в этой статье показано, как tooset копирование непрерывная доставка для Azure облачных приложений.</span><span class="sxs-lookup"><span data-stu-id="4e194-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="4e194-106">Этот процесс позволяет автоматически создавать пакеты и развертывание пакета tooAzure hello после каждого возврата кода.</span><span class="sxs-lookup"><span data-stu-id="4e194-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="4e194-107">Hello процесс построения пакета, описанных в этой статье — эквивалент toohello **пакета** команд в Visual Studio и публикации действия, эквивалентные toohello **публикации** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e194-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="4e194-108">Hello статье рассматриваются hello методов используется toocreate сервер сборки с помощью инструкций командной строки MSBuild и сценарии Windows PowerShell, а также показано, как toooptionally настроить Visual Studio Team Foundation Server - Team Build определения toouse hello MSBuild команд и сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e194-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="4e194-109">процесс Hello можно настраивать для построения среды и Azure целевых средах.</span><span class="sxs-lookup"><span data-stu-id="4e194-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="4e194-110">Можно также использовать Visual Studio Team Services, к версии TFS, размещенной в Azure, toodo это проще.</span><span class="sxs-lookup"><span data-stu-id="4e194-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="4e194-111">Прежде чем начать, следует опубликовать приложение из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e194-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="4e194-112">Это обеспечит, все hello ресурсы, доступные и инициализируется при попытке установить процесс публикации tooautomate hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="4e194-113">1: Настройка hello сервера построения</span><span class="sxs-lookup"><span data-stu-id="4e194-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="4e194-114">Перед созданием пакета служб Azure с помощью MSBuild hello требуется программное обеспечение и средства необходимо установить на сервере сборки hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="4e194-115">Visual Studio не требуется toobe установлен на сервере сборки hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="4e194-116">Toomanage toouse службу сборок Team Foundation ваш сервер сборки, выполните инструкции hello в hello [службу сборок Team Foundation] [ Team Foundation Build Service] документации.</span><span class="sxs-lookup"><span data-stu-id="4e194-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="4e194-117">Установите на сервере сборки hello hello [.NET Framework 4.5.2][.NET Framework 4.5.2], которая включает MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4e194-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="4e194-118">Установить последние hello [средствам разработки Azure для .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="4e194-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="4e194-119">Установка hello [библиотек Azure для .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="4e194-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="4e194-120">Копировать hello файл Microsoft.WebApplication.targets из установки Visual Studio toohello сборки сервера.</span><span class="sxs-lookup"><span data-stu-id="4e194-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="4e194-121">На компьютере с установленной среды Visual Studio, этот файл расположен в каталоге hello C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="4e194-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="4e194-122">Его необходимо скопировать toohello один каталог на сервере сборки hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="4e194-123">Установка hello [средства Azure для Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e194-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="4e194-124">2. Создание пакета с помощью команд MSBuild</span><span class="sxs-lookup"><span data-stu-id="4e194-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="4e194-125">В этом разделе описываются как tooconstruct MSBuild команды построения пакета служб Azure.</span><span class="sxs-lookup"><span data-stu-id="4e194-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="4e194-126">Выполните этот шаг на tooverify сервер сборки hello, все настроено правильно и что команда MSBuild hello делает, необходимую toodo.</span><span class="sxs-lookup"><span data-stu-id="4e194-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="4e194-127">Можно либо добавить этой командной строки tooexisting создавать сценарии на сервере сборки hello, или можно использовать командную строку hello в определение построения TFS, как описано в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="4e194-128">Дополнительные сведения о параметрах командной строки и MSBuild см. в [справочнике по командной строке MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e194-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="4e194-129">Если установлена среда Visual Studio на сервере сборки hello, найдите и выберите **командной строки Visual Studio** в hello **набора средств Visual Studio** папки в Windows.</span><span class="sxs-lookup"><span data-stu-id="4e194-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="4e194-130">Если Visual Studio не установлена на сервере сборки hello, откройте командную строку и убедитесь, что MSBuild.exe доступен по пути.</span><span class="sxs-lookup"><span data-stu-id="4e194-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="4e194-131">MSBuild устанавливается вместе с hello .NET Framework в hello пути % WINDIR %\\Microsoft.NET\\Framework\\*версии*.</span><span class="sxs-lookup"><span data-stu-id="4e194-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="4e194-132">Например для добавления переменной среды PATH toohello MSBuild.exe, если у вас установлена платформа .NET Framework 4, введите следующую команду в командной строке hello hello:</span><span class="sxs-lookup"><span data-stu-id="4e194-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="4e194-133">В командной строке hello перейдите toohello папки, содержащей файл проекта Azure, что требуется toobuild.</span><span class="sxs-lookup"><span data-stu-id="4e194-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="4e194-134">Запустите MSBuild с hello/target: параметр как следующий пример hello публикации:</span><span class="sxs-lookup"><span data-stu-id="4e194-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="4e194-135">Этот параметр можно сократить до /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="4e194-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="4e194-136">параметр /t:Publish Hello в MSBuild не следует путать с команды hello публикации, доступные в Visual Studio, при наличии приветствия установлен пакет SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="4e194-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="4e194-137">Здравствуйте, / t: публикация параметр только для сборок hello Azure пакетов.</span><span class="sxs-lookup"><span data-stu-id="4e194-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="4e194-138">Он не осуществляет развертывание пакетов hello, как команды hello публикации в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e194-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="4e194-139">При необходимости можно указать имя проекта hello как параметр MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4e194-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="4e194-140">Если не указан, используется текущий каталог hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="4e194-141">Дополнительные сведения о параметрах командной строки MSBuild см. в [справочнике по командной строке MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e194-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="4e194-142">Найдите выходные данные hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-142">Locate hello output.</span></span> <span data-ttu-id="4e194-143">По умолчанию эта команда создает каталог отношения toohello корневой папки для проекта hello, таких как *ProjectDir*\\bin\\*конфигурации* \\ App.Publish\\.</span><span class="sxs-lookup"><span data-stu-id="4e194-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="4e194-144">При построении проекта Azure создаются два файла, собственно файл пакета hello и hello, сопровождающие файла конфигурации:</span><span class="sxs-lookup"><span data-stu-id="4e194-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="4e194-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="4e194-145">Project.cspkg</span></span>
   * <span data-ttu-id="4e194-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="4e194-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="4e194-147">По умолчанию каждый проект Azure включает в себя один файл конфигурации службы (с расширением .cscfg) для локальных сборок (отладка) и еще один файл для облачных сборок (промежуточная или рабочая среда), но вы можете добавлять или удалять файлы конфигурации службы при необходимости.</span><span class="sxs-lookup"><span data-stu-id="4e194-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="4e194-148">При построении пакета в среде Visual Studio будет запрашиваться tooinclude файла конфигурации какие службы, наряду с hello пакета.</span><span class="sxs-lookup"><span data-stu-id="4e194-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="4e194-149">Укажите файл конфигурации службы hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-149">Specify hello service configuration file.</span></span> <span data-ttu-id="4e194-150">При создании пакета с помощью MSBuild, файл конфигурации локальной службы hello включается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4e194-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="4e194-151">tooinclude файл конфигурации другую службу, задайте свойство TargetProfile команды MSBuild hello, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="4e194-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="4e194-152">Укажите место hello hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4e194-152">Specify hello location for hello output.</span></span> <span data-ttu-id="4e194-153">Задает путь к hello с помощью /p:PublishDir =*каталога* \\ параметр, включая конечный разделитель обратной косой черты, как следующий пример hello hello:</span><span class="sxs-lookup"><span data-stu-id="4e194-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="4e194-154">После создания и тестирования соответствующие MSBuild командной строки toobuild проектов и объединять их в пакете служб Azure, можно добавить сценарии построения tooyour этой командной строки.</span><span class="sxs-lookup"><span data-stu-id="4e194-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="4e194-155">Если сервер сборки использует пользовательские сценарии, этот процесс будет зависеть от особенностей пользовательского процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="4e194-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="4e194-156">При использовании TFS в качестве среды разработки необходимо выполнить инструкции hello hello следующий шаг tooadd hello Azure пакет сборки tooyour процесса построения.</span><span class="sxs-lookup"><span data-stu-id="4e194-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="4e194-157">3. Создание пакета с помощью TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="4e194-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="4e194-158">Если у вас есть настроить Team Foundation Server (TFS) настроить контроллер построений и hello серверы сборки, в качестве компьютера сборки TFS, а затем при необходимости можно настроить автоматизированной сборки для пакета Azure.</span><span class="sxs-lookup"><span data-stu-id="4e194-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="4e194-159">Сведения о статье tooset копирование и использование сервера Team Foundation server в качестве системы сборки, [масштабирование системы построения][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="4e194-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="4e194-160">В частности, в следующей процедуре предполагается, что настроили ваш сервер сборки, как описано в [развертывание и настройка сервера сборки][Deploy and configure a build server], и что вы создали командный проект, создать облако проект службы в командном проекте hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="4e194-161">tooconfigure TFS toobuild Azure пакеты, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4e194-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="4e194-162">В Visual Studio на компьютере разработчика, в меню "Вид" hello, выберите **Team Explorer**, или нажмите сочетание клавиш Ctrl +\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="4e194-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="4e194-163">В командном обозревателе разверните hello **строит** узла или выберите hello **строит** странице и выберите **создать определение построения**.</span><span class="sxs-lookup"><span data-stu-id="4e194-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![Параметр "Создать определение сборки"][0]
2. <span data-ttu-id="4e194-165">Выберите hello **триггер** и укажите hello требуемого условия для при необходимости hello построен toobe пакета.</span><span class="sxs-lookup"><span data-stu-id="4e194-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="4e194-166">Например, указать **непрерывной интеграции** происходит toobuild hello пакета всякий раз, когда возврата системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="4e194-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="4e194-167">Выберите hello **параметры источника** вкладку и убедитесь, что папку проекта, перечисленные в hello **папка системы управления версиями** столбца, и находится в состоянии hello **Active**.</span><span class="sxs-lookup"><span data-stu-id="4e194-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="4e194-168">Выберите hello **сборки по умолчанию** и в списке контроллер построений убедитесь hello имя сервера построения hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="4e194-169">Кроме того, выберите параметр hello **следующие toohello выходные данные построения копирования транзитный каталог** и укажите расположение сброса требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="4e194-170">Выберите hello **процесс** вкладки. На вкладке "процесс" hello, выберите шаблон по умолчанию hello в разделе **построения**, выберите проект hello в том случае, если он еще не выбран и разверните hello **Дополнительно** раздела hello **построения**части сетки hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="4e194-171">Выберите **Аргументы MSBuild**и задать аргументы командной строки MSBuild соответствующие hello, как описано в шаге 2 выше.</span><span class="sxs-lookup"><span data-stu-id="4e194-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="4e194-172">Например, введите **/t: публикация /p:PublishDir =\\\\myserver\\удаляет\\**  toobuild пакет hello пакета и скопируйте файлы toohello расположение \\ \\myserver\\удаляет\\:</span><span class="sxs-lookup"><span data-stu-id="4e194-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![Аргументы MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="4e194-174">Копирование файлов tooa hello общей папке упрощает toomanually упрощает развертывание пакетов hello с компьютера разработчика.</span><span class="sxs-lookup"><span data-stu-id="4e194-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="4e194-175">Протестировать успех hello этапа построения путем возврата изменений tooyour проекта или очередь новую сборку.</span><span class="sxs-lookup"><span data-stu-id="4e194-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="4e194-176">tooqueue копирование новую сборку в Team Explorer, щелкните правой кнопкой мыши **определений сборок,** и выберите **новую сборку в очередь**.</span><span class="sxs-lookup"><span data-stu-id="4e194-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="4e194-177">4. Публикация пакета с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e194-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="4e194-178">В этом разделе описывается, как сценарий Windows PowerShell, который будет публиковать пакет приложения hello облака tooconstruct вывода tooAzure использование необязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="4e194-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="4e194-179">Этот сценарий может быть вызвана после шага построения hello в автоматизации настраиваемой сборки.</span><span class="sxs-lookup"><span data-stu-id="4e194-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="4e194-180">Также он может быть вызван из действий рабочего процесса шаблона процесса в Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="4e194-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="4e194-181">Установка hello [командлетов Azure PowerShell] [ Azure PowerShell cmdlets] (v0.6.1 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="4e194-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="4e194-182">Во время фазы установки командлета hello выберите tooinstall в качестве оснастки.</span><span class="sxs-lookup"><span data-stu-id="4e194-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="4e194-183">Обратите внимание, что официально поддерживаемой заменяет старую версию hello, предоставляемые через CodePlex, несмотря на то, что hello предыдущих версий были номерами 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="4e194-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="4e194-184">Запустите PowerShell Azure с помощью меню "Пуск" hello "или" Начальная страница.</span><span class="sxs-lookup"><span data-stu-id="4e194-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="4e194-185">При запуске таким образом, будут загружены hello командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e194-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="4e194-186">В командной строке PowerShell hello, проверьте загрузку hello командлеты PowerShell, введя команду частичного hello `Get-Azure` и нажав клавишу Tab для завершения операторов "hello".</span><span class="sxs-lookup"><span data-stu-id="4e194-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="4e194-187">При нажатии клавиши Tab hello многократно, вы увидите различные команды Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e194-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="4e194-188">Убедитесь, что можно подключиться tooyour подписке Azure путем импорта из файла .publishsettings hello сведений о подписке.</span><span class="sxs-lookup"><span data-stu-id="4e194-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="4e194-189">Затем введите команду hello</span><span class="sxs-lookup"><span data-stu-id="4e194-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="4e194-190">Отобразится информация о подписке.</span><span class="sxs-lookup"><span data-stu-id="4e194-190">This shows information about your subscription.</span></span> <span data-ttu-id="4e194-191">Убедитесь, что все работает правильно.</span><span class="sxs-lookup"><span data-stu-id="4e194-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="4e194-192">Сохранить шаблон скрипта hello, указанный в конце hello в этой статье в папку скриптов в c:\\сценариев\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="4e194-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="4e194-193">Прочтите раздел параметров hello hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="4e194-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="4e194-194">Добавьте или измените любые значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4e194-194">Add or modify any default values.</span></span> <span data-ttu-id="4e194-195">Эти значения можно всегда переопределить с помощью передачи явных параметров.</span><span class="sxs-lookup"><span data-stu-id="4e194-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="4e194-196">Убедитесь, существует допустимое облачной службы и учетные записи хранения в подписке, может быть целевым объектом hello скрипта публикации.</span><span class="sxs-lookup"><span data-stu-id="4e194-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="4e194-197">Учетной записи хранения (хранилище blob) будет использоваться tooupload и временного хранения hello развертывания пакета и файле конфигурации во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="4e194-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="4e194-198">toocreate новой облачной службы, может вызывать этот сценарий или используйте hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e194-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e194-199">Hello имя облачной службы будет использоваться в качестве префикса в полное доменное имя, и поэтому должен быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="4e194-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="4e194-200">toocreate новой учетной записи хранения, можно вызвать этот сценарий или используйте hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e194-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e194-201">Имя учетной записи хранения Hello будет использован в качестве префикса в полное доменное имя, и поэтому должен быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="4e194-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="4e194-202">Попробуйте использовать одинаковые имена, hello как облачную службу.</span><span class="sxs-lookup"><span data-stu-id="4e194-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="4e194-203">Вызов скрипта hello прямо из Azure PowerShell или подключить этот скрипт построения узла tooyour автоматизации toooccur после сборки пакета hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4e194-204">сценарий Hello всегда удалит или замене существующих развертываний по умолчанию, если они обнаружены.</span><span class="sxs-lookup"><span data-stu-id="4e194-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="4e194-205">Это необходимо для включения непрерывной доставки из автоматизации, где невозможно вмешательство пользователя.</span><span class="sxs-lookup"><span data-stu-id="4e194-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="4e194-206">**Пример сценария 1:** toohello непрерывного развертывания промежуточной среде службы:</span><span class="sxs-lookup"><span data-stu-id="4e194-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="4e194-207">Это обычно сопровождается тестовым запуском проверки и замены виртуального IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="4e194-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="4e194-208">swap Hello виртуальных IP-адресов можно сделать с помощью hello [портал Azure](https://portal.azure.com) или с помощью командлета Move развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="4e194-209">**Пример сценария 2:** непрерывного развертывания toohello рабочей среде служба выделенной тестирования</span><span class="sxs-lookup"><span data-stu-id="4e194-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="4e194-210">**Удаленный рабочий стол**</span><span class="sxs-lookup"><span data-stu-id="4e194-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="4e194-211">Если удаленный рабочий стол включен в проекте Azure необходимо будет tooperform дополнительные одноразовый действия tooensure приветствия правильный сертификат службы облачной отправлен tooall облачные службы мишенью для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="4e194-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="4e194-212">Найдите значения отпечатка сертификата hello, ожидаемый вашей роли.</span><span class="sxs-lookup"><span data-stu-id="4e194-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="4e194-213">Отпечаток значения видны hello сертификаты из раздела файла конфигурации облака (т. е. ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="4e194-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="4e194-214">Это также отображается в диалоговом окне Конфигурация удаленного рабочего стола hello в Visual Studio, когда Показать параметры и представление hello выбран сертификат.</span><span class="sxs-lookup"><span data-stu-id="4e194-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="4e194-215">Передавать сертификаты удаленного рабочего стола, как на этапе одноразовой настройки, с помощью hello, выполнив командлет сценария:</span><span class="sxs-lookup"><span data-stu-id="4e194-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="4e194-216">Например:</span><span class="sxs-lookup"><span data-stu-id="4e194-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="4e194-217">Кроме того, можно экспортировать файл hello сертификата PFX с закрытым ключом и передачи сертификатов tooeach целевой облачной службы с помощью [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e194-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="4e194-218">**Обновление развертывания по сравнению с удалением развертывания и \>созданием развертывания**</span><span class="sxs-lookup"><span data-stu-id="4e194-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="4e194-219">Hello по умолчанию выполняет скрипт развертывания обновления ($enableDeploymentUpgrade = 1) Если не передаются никакие параметры в или явным образом передается значение 1.</span><span class="sxs-lookup"><span data-stu-id="4e194-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="4e194-220">Для одного экземпляра это имеет преимущество, поскольку тратится меньше времени, чем на полное развертывание.</span><span class="sxs-lookup"><span data-stu-id="4e194-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="4e194-221">Для экземпляров, которые требуют высокой доступности, это также имеет преимущество hello, остаются некоторые под управлением, тогда как другие экземпляры обновляются (проходу домена обновления), а также VIP-адрес не будет удален.</span><span class="sxs-lookup"><span data-stu-id="4e194-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="4e194-222">Развертывания обновления можно отключить в скрипте hello ($enableDeploymentUpgrade = 0) или путем передачи *- enableDeploymentUpgrade 0* как параметр, который изменяет поведение toofirst сценарий удаления любого существующего развертывания, а затем создать новое развертывание.</span><span class="sxs-lookup"><span data-stu-id="4e194-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4e194-223">сценарий Hello всегда удалит или замене существующих развертываний по умолчанию, если они обнаружены.</span><span class="sxs-lookup"><span data-stu-id="4e194-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="4e194-224">Это необходимо для включения непрерывной доставки из автоматизации, где невозможно вмешательство пользователя или оператора.</span><span class="sxs-lookup"><span data-stu-id="4e194-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="4e194-225">5. Публикация пакета с помощью TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="4e194-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="4e194-226">Этот необязательный шаг подключается TFS Team Build toohello сценарий, созданный на шаге 4, обрабатывающего публикации tooAzure построения пакета hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="4e194-227">Влечет за собой изменение hello шаблон процесса используется в определении построения, чтобы он выполняет действие публикации, в конце hello hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="4e194-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="4e194-228">Hello действия публикации будет запустите команду PowerShell передача в параметры из сборки hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="4e194-229">Должен быть выведен hello MSBuild предназначен и публикации скриптов выходные данные в выходные данные построения Стандартная hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="4e194-230">Изменить определение построения, отвечающий за hello непрерывного развертывания.</span><span class="sxs-lookup"><span data-stu-id="4e194-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="4e194-231">Выберите hello **процесс** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4e194-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="4e194-232">Выполните [эти инструкции](http://msdn.microsoft.com/library/dd647551.aspx) tooadd проекта действия для hello шаблон процесса сборки, загрузить шаблон по умолчанию hello, добавьте его в проект hello и вернуть его на сервер.</span><span class="sxs-lookup"><span data-stu-id="4e194-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="4e194-233">Предоставьте новое имя, например AzureBuildProcessTemplate hello шаблон процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="4e194-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="4e194-234">Вернуть toohello **процесс** вкладку и использовать **Показать подробности** tooshow список шаблонов процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="4e194-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="4e194-235">Выберите hello **создать...**  кнопку и перейдите toohello проекта только что добавленный и возврата.</span><span class="sxs-lookup"><span data-stu-id="4e194-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="4e194-236">Найдите только что созданный шаблон hello и выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4e194-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="4e194-237">Откройте hello выбранного шаблона процесса для редактирования.</span><span class="sxs-lookup"><span data-stu-id="4e194-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="4e194-238">Можно открыть непосредственно в конструкторе рабочих процессов hello или hello toowork редактор XML с hello XAML.</span><span class="sxs-lookup"><span data-stu-id="4e194-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="4e194-239">Добавьте следующие список новые аргументы в виде отдельных элементов строки на вкладке hello аргументы конструктора рабочих процессов hello hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="4e194-240">Все аргументы должны иметь параметры direction=In и type=String.</span><span class="sxs-lookup"><span data-stu-id="4e194-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="4e194-241">Они будут используется tooflow параметров из определения построения hello в рабочем процессе hello, которой затем используется toocall hello get скрипта публикации.</span><span class="sxs-lookup"><span data-stu-id="4e194-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Список аргументов][3]

   <span data-ttu-id="4e194-243">Привет, соответствующий XAML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4e194-243">hello corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="4e194-244">Добавьте новую последовательность в конце hello выполнение в агенте:</span><span class="sxs-lookup"><span data-stu-id="4e194-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="4e194-245">Начните с добавления toocheck действия оператора If для является допустимым файлом сценария.</span><span class="sxs-lookup"><span data-stu-id="4e194-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="4e194-246">Задайте значение toothis hello условия:</span><span class="sxs-lookup"><span data-stu-id="4e194-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="4e194-247">Затем в hello регистр hello оператора If, добавьте новое действие последовательности.</span><span class="sxs-lookup"><span data-stu-id="4e194-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="4e194-248">Отображаемое имя набора hello too'Start публикации "</span><span class="sxs-lookup"><span data-stu-id="4e194-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="4e194-249">С начала публикации последовательности по-прежнему выбран hello добавьте приведенный ниже перечень новые переменные как отдельные элементы строки на вкладке "переменные" hello конструктора рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="4e194-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="4e194-250">Все переменные должны иметь тип String и Scope=Start publish.</span><span class="sxs-lookup"><span data-stu-id="4e194-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="4e194-251">Они будут используется tooflow параметров из определения построения hello в рабочий процесс, которой затем используется toocall hello get скрипта публикации.</span><span class="sxs-lookup"><span data-stu-id="4e194-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="4e194-252">SubscriptionDataFilePath типа String.</span><span class="sxs-lookup"><span data-stu-id="4e194-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="4e194-253">PublishScriptFilePath типа String.</span><span class="sxs-lookup"><span data-stu-id="4e194-253">PublishScriptFilePath, of type String</span></span>

        ![Новые переменные][4]
   4. <span data-ttu-id="4e194-255">Если вы используете TFS 2012 или более ранней версии, добавить действие ConvertWorkspaceItem в начале hello hello новой последовательности.</span><span class="sxs-lookup"><span data-stu-id="4e194-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="4e194-256">Если вы используете TFS 2013 или более поздней версии, добавить действие GetLocalPath в начале hello hello новой последовательности.</span><span class="sxs-lookup"><span data-stu-id="4e194-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="4e194-257">Для ConvertWorkspaceItem свойства hello следующим образом: направление = ServerToLocal DisplayName = «Convert опубликовать имя файла сценария,» входные данные = «PublishScriptLocation», результат = рабочей области «PublishScriptFilePath» = «Рабочую область».</span><span class="sxs-lookup"><span data-stu-id="4e194-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="4e194-258">Для операции GetLocalPath задать too'PublishScriptLocation IncomingPath свойство hello ", и результат too'PublishScriptFilePath hello".</span><span class="sxs-lookup"><span data-stu-id="4e194-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="4e194-259">Это действие преобразует hello путь toohello публикации скрипта из расположения сервера TFS (если применимо) путь tooa стандартного локального диска.</span><span class="sxs-lookup"><span data-stu-id="4e194-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="4e194-260">Если вы используете TFS 2012 или более ранней версии, добавьте еще одно действие ConvertWorkspaceItem конце hello hello новой последовательности.</span><span class="sxs-lookup"><span data-stu-id="4e194-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="4e194-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="4e194-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="4e194-262">Если вы используете TFS 2013 или более позднюю версию, добавьте еще одно действие GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="4e194-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="4e194-263">IncomingPath='SubscriptionDataFileLocation' и Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="4e194-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="4e194-264">Добавить действие InvokeProcess конце hello hello новой последовательности.</span><span class="sxs-lookup"><span data-stu-id="4e194-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="4e194-265">Это действие вызовы PowerShell.exe, с аргументами hello переданный hello определения сборки.</span><span class="sxs-lookup"><span data-stu-id="4e194-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="4e194-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="4e194-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="4e194-267">DisplayName = Выполнение сценария публикации</span><span class="sxs-lookup"><span data-stu-id="4e194-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="4e194-268">FileName = «PowerShell» (используйте кавычки hello)</span><span class="sxs-lookup"><span data-stu-id="4e194-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="4e194-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="4e194-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="4e194-270">В hello **обработать стандартный вывод** статьи текстового поля из InvokeProcess, задайте значение too'data hello текстовое поле ".</span><span class="sxs-lookup"><span data-stu-id="4e194-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="4e194-271">Это стандартный вывод данных переменной toostore hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="4e194-272">Добавить действие WriteBuildMessage под hello **обработать стандартный вывод** раздела.</span><span class="sxs-lookup"><span data-stu-id="4e194-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="4e194-273">Задать важность hello = «Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High» и сообщение hello = «данные».</span><span class="sxs-lookup"><span data-stu-id="4e194-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="4e194-274">Это гарантирует, что hello стандартные выходные данные сценария будут записанных toohello выходные данные построения.</span><span class="sxs-lookup"><span data-stu-id="4e194-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="4e194-275">В hello **обработать вывод ошибки** статьи текстового поля из InvokeProcess, задайте значение too'data hello текстовое поле ".</span><span class="sxs-lookup"><span data-stu-id="4e194-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="4e194-276">Это стандартная ошибка данных переменной toostore hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="4e194-277">Добавить действие WriteBuildError под hello **обработать вывод ошибки** раздела.</span><span class="sxs-lookup"><span data-stu-id="4e194-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="4e194-278">Задать сообщение hello = «данные».</span><span class="sxs-lookup"><span data-stu-id="4e194-278">Set hello Message='data'.</span></span> <span data-ttu-id="4e194-279">Это гарантирует, что hello стандартной погрешности hello скрипта будет получить запись toohello вывод ошибок построения.</span><span class="sxs-lookup"><span data-stu-id="4e194-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="4e194-280">Исправьте все ошибки, отмеченные синими восклицательными знаками.</span><span class="sxs-lookup"><span data-stu-id="4e194-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="4e194-281">Наведите указатель мыши tooget восклицательных знаков подсказку об ошибке hello.</span><span class="sxs-lookup"><span data-stu-id="4e194-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="4e194-282">Сохраните hello рабочего процесса, чтобы очистить ошибки.</span><span class="sxs-lookup"><span data-stu-id="4e194-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="4e194-283">конечным результатом Hello hello публикации действий будет выглядеть следующим образом в конструкторе hello рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="4e194-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![Действия рабочего процесса][5]

   <span data-ttu-id="4e194-285">конечный результат Hello hello опубликовать рабочий процесс, который действий в XAML будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4e194-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="4e194-286">Сохранение шаблона процесса построения hello и проверять в этом файле.</span><span class="sxs-lookup"><span data-stu-id="4e194-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="4e194-287">Измените определение сборки hello (Закрыть его, если он открыт) и выберите hello **New** кнопку, если вы еще не видите hello новый шаблон в списке hello шаблонов процессов.</span><span class="sxs-lookup"><span data-stu-id="4e194-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="4e194-288">Задайте значения свойств параметров hello в разделе Прочее hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4e194-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="4e194-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Это значение является производным от: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="4e194-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="4e194-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Это значение является производным от: ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="4e194-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="4e194-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="4e194-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="4e194-292">ServiceName = «mycloudservicename» *используйте hello соответствующее имя облачной службы здесь*</span><span class="sxs-lookup"><span data-stu-id="4e194-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="4e194-293">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="4e194-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="4e194-294">StorageAccountName = «mystorageaccountname» *имя учетной записи хранилища, соответствующий hello используйте здесь*</span><span class="sxs-lookup"><span data-stu-id="4e194-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="4e194-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="4e194-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="4e194-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="4e194-296">SubscriptionName = 'default'</span></span>

    ![Значения свойств параметров][6]
11. <span data-ttu-id="4e194-298">Сохраните изменения hello toohello определения сборки.</span><span class="sxs-lookup"><span data-stu-id="4e194-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="4e194-299">Очередь tooexecute сборки, оба hello номер сборки пакета и публикации.</span><span class="sxs-lookup"><span data-stu-id="4e194-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="4e194-300">Если задать tooContinuous интеграции триггер, это поведение будет выполняться на каждом возврате.</span><span class="sxs-lookup"><span data-stu-id="4e194-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="4e194-301">Шаблон сценария PublishCloudService.ps1</span><span class="sxs-lookup"><span data-stu-id="4e194-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="4e194-302">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e194-302">Next steps</span></span>
<span data-ttu-id="4e194-303">tooenable удаленную отладку при использовании непрерывной поставки разделе [включить удаленную отладку при использовании непрерывной поставки toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="4e194-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
