---
title: "Непрерывная отправка для облачных служб с помощью TFS в Azure | Документация Майкрософт"
description: "Узнайте, как настраивать непрерывную отправку для облачных приложений Azure. Примеры программного кода для инструкций командной строки MSBuild и сценариев PowerShell."
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
ms.openlocfilehash: 0979722b9ec715e91825c7aba74657451df6e83f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="9bd7e-104">Непрерывная доставка для облачных служб в Azure</span><span class="sxs-lookup"><span data-stu-id="9bd7e-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="9bd7e-105">Описанный в этой статье процесс показывает, как настроить непрерывную доставку для облачных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="9bd7e-106">Этот процесс позволяет автоматически создавать пакеты и развертывать их в Azure после каждого возврата кода.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="9bd7e-107">Процесс сборки пакета, представленный в этой статье, эквивалентен команде **Package** в Visual Studio. Этапы публикации эквивалентны команде **Publish** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="9bd7e-108">В статье описаны методы, которые можно использовать для создания сервера сборки с помощью инструкций командной строки MSBuild и сценариев Windows PowerShell, а также показано, как дополнительно настроить Visual Studio Team Foundation Server — определения Team Build для использования команд MSBuild и сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="9bd7e-109">Процесс можно настраивать для среды сборки и целевых сред Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="9bd7e-110">Для упрощения задачи можно также использовать службу Visual Studio Team Services — версию TFS, размещенную в Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> 

<span data-ttu-id="9bd7e-111">Прежде чем начать, следует опубликовать приложение из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="9bd7e-112">Это обеспечит доступность и инициализацию всех ресурсов при попытке автоматизировать процесс публикации.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-112">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="9bd7e-113">1. Настройка сервера сборки</span><span class="sxs-lookup"><span data-stu-id="9bd7e-113">1: Configure the Build Server</span></span>
<span data-ttu-id="9bd7e-114">Прежде чем создавать пакет Azure с помощью MSBuild, следует установить на сервере сборки необходимое программное обеспечение и инструменты.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-114">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="9bd7e-115">Visual Studio необязательно должна быть установлена на сервере сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-115">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="9bd7e-116">Если вы хотите использовать для управления сервером сборки службу сборок Team Foundation, следуйте указаниям в документации по [службе сборок Team Foundation][Team Foundation Build Service].</span><span class="sxs-lookup"><span data-stu-id="9bd7e-116">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="9bd7e-117">На сервере сборки установите платформу [.NET Framework 4.5.2][.NET Framework 4.5.2], которая включает в себя MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-117">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="9bd7e-118">Установите последнюю версию [инструментов разработки Azure Authoring Tools для .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-118">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="9bd7e-119">Установите [библиотеки Azure для .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-119">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="9bd7e-120">Скопируйте файл Microsoft.WebApplication.targets из папки с программой Visual Studio на сервер сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-120">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="9bd7e-121">На компьютере с установленной средой Visual Studio файл располагается в каталоге C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-121">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="9bd7e-122">Нужно скопировать его в тот же каталог на сервере сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-122">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="9bd7e-123">Установите [инструменты Azure для Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-123">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="9bd7e-124">2. Создание пакета с помощью команд MSBuild</span><span class="sxs-lookup"><span data-stu-id="9bd7e-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="9bd7e-125">В этом разделе описывается создание команды MSBuild, которая выполняет сборку пакета Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-125">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="9bd7e-126">Выполните этот шаг на сервере сборки, чтобы убедиться, что все правильно настроено и команда MSBuild делает то, что нужно.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-126">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="9bd7e-127">Эту командную строку можно добавить в существующие сценарии сборки на сервере сборки или использовать командную строку в определении сборки TFS, как описано в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-127">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="9bd7e-128">Дополнительные сведения о параметрах командной строки и MSBuild см. в [справочнике по командной строке MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="9bd7e-129">Если среда Visual Studio установлена на сервере сборки, то в Windows найдите и щелкните **Командная строка Visual Studio** в папке **Visual Studio Tools**.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-129">If Visual Studio is installed on the build server, locate and choose **Visual Studio Command Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="9bd7e-130">Если экземпляр Visual Studio не установлен на сервере сборки, откройте командную строку и убедитесь, что файл MSBuild.exe доступен в пути.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-130">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="9bd7e-131">MSBuild устанавливается вместе с .NET Framework по пути %WINDIR%\\Microsoft.NET\\Framework\\*версия*.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-131">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="9bd7e-132">Например, чтобы добавить файл MSBuild.exe в переменную среды PATH при наличии платформы .NET Framework 4, введите следующую команду в командной строке:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-132">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="9bd7e-133">В командной строке перейдите в папку, содержащую файл проекта Azure, который требуется создать.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-133">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="9bd7e-134">Запустите MSBuild с параметром /target:Publish, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-134">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="9bd7e-135">Этот параметр можно сократить до /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="9bd7e-136">Параметр /t:Publish в MSBuild не следует путать с командами Publish, доступными в Visual Studio при наличии установленного пакета SDK для Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-136">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="9bd7e-137">Параметр /t:Publish собирает только пакеты Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-137">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="9bd7e-138">Он не осуществляет развертывание пакетов, как команды Publish в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-138">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="9bd7e-139">Дополнительно можно указать имя проекта в качестве параметра MSBuild.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-139">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="9bd7e-140">Если не указано, используется текущий каталог.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-140">If not specified, the current directory is used.</span></span> <span data-ttu-id="9bd7e-141">Дополнительные сведения о параметрах командной строки MSBuild см. в [справочнике по командной строке MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="9bd7e-142">Найдите данные вывода.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-142">Locate the output.</span></span> <span data-ttu-id="9bd7e-143">По умолчанию команда создает каталог относительно корневой папки проекта, например *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-143">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="9bd7e-144">При сборке проекта Azure создается два файла — собственно файл пакета и сопутствующий файл конфигурации:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-144">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="9bd7e-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="9bd7e-145">Project.cspkg</span></span>
   * <span data-ttu-id="9bd7e-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="9bd7e-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="9bd7e-147">По умолчанию каждый проект Azure включает в себя один файл конфигурации службы (с расширением .cscfg) для локальных сборок (отладка) и еще один файл для облачных сборок (промежуточная или рабочая среда), но вы можете добавлять или удалять файлы конфигурации службы при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="9bd7e-148">При сборке пакета в Visual Studio вам будет предложено выбрать файл конфигурации службы для включения в пакет.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-148">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="9bd7e-149">Укажите файл конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-149">Specify the service configuration file.</span></span> <span data-ttu-id="9bd7e-150">При сборке пакета с использованием MSBuild по умолчанию включается файл конфигурации локальной службы.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-150">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="9bd7e-151">Чтобы включить другой файл конфигурации службы, задайте свойство TargetProfile команды MSBuild, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-151">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="9bd7e-152">Укажите расположение для данных вывода.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-152">Specify the location for the output.</span></span> <span data-ttu-id="9bd7e-153">Укажите путь с помощью параметра /p:PublishDir=*каталог*\\, включая конечный символ обратной косой черты в качестве разделителя, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-153">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="9bd7e-154">После создания и тестирования соответствующей командной строки MSBuild для сборки проектов и объединения их в пакет Azure можно добавить эту команду в сценарии сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-154">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="9bd7e-155">Если сервер сборки использует пользовательские сценарии, этот процесс будет зависеть от особенностей пользовательского процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="9bd7e-156">Если в качестве среды сборки используется TFS, вы можете следовать указаниям на следующем шаге, чтобы добавить пакет сборки Azure в процессе сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-156">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="9bd7e-157">3. Создание пакета с помощью TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="9bd7e-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="9bd7e-158">Если Team Foundation Server (TFS) настроен как контроллер сборки, а сервер сборки настроен как компьютер сборки TFS, вы можете дополнительно настроить автоматизированную сборку для пакета Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-158">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="9bd7e-159">Сведения о том, как настроить и использовать сервер Team Foundation в качестве системы сборки, см. в разделе [Расширение системы сборки][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="9bd7e-159">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="9bd7e-160">В частности, в следующей процедуре подразумевается, что вы настроили сервер сборки, как описано в разделе [Развертывание и настройка сервера сборки][Deploy and configure a build server], создали командный проект и создали проект облачной службы в командном проекте.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="9bd7e-161">Чтобы настроить TFS для выполнения сборки пакетов Azure, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-161">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="9bd7e-162">В Visual Studio на компьютере разработчика в меню "Вид" выберите **Team Explorer** или нажмите клавиши CTRL+\\, CTRL+M.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-162">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="9bd7e-163">В окне Team Explorer разверните узел **Сборки** или выберите **соответствующую** страницу, а затем — пункт **Создать определение сборки**.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-163">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![Параметр "Создать определение сборки"][0]
2. <span data-ttu-id="9bd7e-165">Выберите вкладку **Триггер** и укажите нужные условия для сборки пакета.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-165">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="9bd7e-166">Например, укажите **Непрерывная интеграция** для сборки пакета при каждом возврате из системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-166">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="9bd7e-167">Перейдите на вкладку **Параметры исходного кода** и убедитесь, что папка вашего проекта числится в столбце **Папка системы управления версиями**, а значение состояния — **Активно**.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-167">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="9bd7e-168">Перейдите на вкладку **Параметры сборки по умолчанию** и в разделе «Контроллер сборки» проверьте имя сервера сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-168">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="9bd7e-169">Также выберите параметр **Копировать выходные данные в следующую папку сброса** и укажите нужное расположение.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-169">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="9bd7e-170">Выберите вкладку **Процесс** . На вкладке "Процесс" выберите шаблон по умолчанию, в разделе **Сборка** выберите проект, если он еще не выбран, и разверните раздел **Дополнительно** в разделе сетки **Сборка**.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-170">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="9bd7e-171">Выберите **Аргументы MSBuild**и задайте соответствующие командной строки MSBuild, как описано в шаге 2 выше.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-171">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="9bd7e-172">Например, введите **/t:Publish /p:PublishDir=\\\\myserver\\drops\\**, чтобы собрать пакет и скопировать файлы пакета в расположение \\\\myserver\\drops\\.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![Аргументы MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="9bd7e-174">Копирование файлов в общую папку упрощает развертывание пакетов с компьютера разработчика вручную.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-174">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="9bd7e-175">Протестируйте выполнение шага сборки, проверяя изменения проекта на входе, или поставьте новую сборку в очередь.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-175">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="9bd7e-176">Чтобы поставить в очередь новую сборку, в Team Explorer щелкните правой кнопкой мыши пункт **Все определения сборки**, а затем выберите **Поставить новую сборку в очередь**.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-176">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="9bd7e-177">4. Публикация пакета с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bd7e-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="9bd7e-178">В этом разделе описывается, как создать сценарий Windows PowerShell, который будет публиковать выходные данные пакета облачного приложения в Azure, используя дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-178">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="9bd7e-179">Этот сценарий может быть вызван после шага сборки при автоматизации пользовательской сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-179">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="9bd7e-180">Также он может быть вызван из действий рабочего процесса шаблона процесса в Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="9bd7e-181">Установите [командлеты Azure PowerShell][Azure PowerShell cmdlets] (версии 0.6.1 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-181">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="9bd7e-182">Во время установки командлета выберите установку в качестве оснастки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-182">During the cmdlet setup phase, choose to install as a snap-in.</span></span> <span data-ttu-id="9bd7e-183">Обратите внимание, что эта официально поддерживаемая версия заменяет старую версию CodePlex, несмотря на то что предыдущие версии были пронумерованы 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-183">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="9bd7e-184">Запустите Azure PowerShell из меню «Пуск» или с начальной страницы.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-184">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="9bd7e-185">При запуске таким способом загружаются командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-185">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="9bd7e-186">В командной строке PowerShell убедитесь, что командлеты PowerShell загружены. Для этого введите часть команды `Get-Azure` и нажмите клавишу TAB для выполнения оператора.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-186">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="9bd7e-187">Если несколько раз нажать клавишу TAB, вы увидите различные команды Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-187">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="9bd7e-188">Проверьте возможность подключения к подписке Azure, выполнив импорт информации о подписке из PUBLISHSETTINGS-файла.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-188">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="9bd7e-189">Введите команду:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-189">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="9bd7e-190">Отобразится информация о подписке.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-190">This shows information about your subscription.</span></span> <span data-ttu-id="9bd7e-191">Убедитесь, что все работает правильно.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="9bd7e-192">Сохраните шаблон скрипта, приведенный в конце этой статьи, в папке скриптов с именем C:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-192">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="9bd7e-193">Просмотрите раздел параметров скрипта.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-193">Review the parameters section of the script.</span></span> <span data-ttu-id="9bd7e-194">Добавьте или измените любые значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-194">Add or modify any default values.</span></span> <span data-ttu-id="9bd7e-195">Эти значения можно всегда переопределить с помощью передачи явных параметров.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="9bd7e-196">Убедитесь, что созданы допустимая облачная служба и учетная запись хранения в подписке, которая может быть целевой для сценария публикации.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="9bd7e-197">Учетная запись хранения (хранилище больших двоичных объектов) будет использоваться для передачи и временного хранения файла конфигурации и пакета развертывания во время создания развертывания.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-197">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="9bd7e-198">Чтобы создать облачную службу, можно вызвать этот сценарий или воспользоваться [порталом Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-198">To create a new cloud service, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9bd7e-199">Имя облачной службы будет использоваться в качестве префикса в полном имени домена, поэтому оно должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-199">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="9bd7e-200">Чтобы создать учетную запись хранения, можно вызвать этот сценарий или воспользоваться [порталом Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-200">To create a new storage account, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9bd7e-201">Имя учетной записи хранения будет использоваться в качестве префикса в полном имени домена, поэтому должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-201">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="9bd7e-202">Попробуйте использовать то же имя, что и в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-202">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="9bd7e-203">Вызовите сценарий непосредственно из Azure PowerShell или подключите этот сценарий к автоматизации сборки узла, выполняемой после сборки пакета.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-203">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9bd7e-204">Сценарий всегда будет удалять или заменять существующие развертывания по умолчанию, если они обнаружены.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-204">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="9bd7e-205">Это необходимо для включения непрерывной доставки из автоматизации, где невозможно вмешательство пользователя.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="9bd7e-206">**Пример сценария 1.** Непрерывное развертывание в промежуточной среде службы</span><span class="sxs-lookup"><span data-stu-id="9bd7e-206">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="9bd7e-207">Это обычно сопровождается тестовым запуском проверки и замены виртуального IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="9bd7e-208">Заменить виртуальный IP-адрес можно на [портале Azure](https://portal.azure.com) или с помощью командлета Move-Deployment.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-208">The VIP swap can be done via the [Azure portal](https://portal.azure.com) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="9bd7e-209">**Пример сценария 2.** Непрерывное развертывание в рабочей среде выделенной тестовой службы</span><span class="sxs-lookup"><span data-stu-id="9bd7e-209">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="9bd7e-210">**Удаленный рабочий стол**</span><span class="sxs-lookup"><span data-stu-id="9bd7e-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="9bd7e-211">При включении удаленного рабочего стола в проекте Azure потребуется выполнить одноразовые дополнительные шаги, чтобы убедиться, что все облачные службы, являющиеся целью этого сценария, имеют правильный сертификат облачной службы.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-211">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="9bd7e-212">Найдите значения отпечатка сертификата, который ожидают роли.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-212">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="9bd7e-213">Значения отпечатков отображаются в разделе Certificates файла конфигурации облака (т.е. ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-213">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="9bd7e-214">Кроме того, он отображается в диалоговом окне «Конфигурация удаленных рабочих столов» в Visual Studio при отображении параметров и просмотре выбранного сертификата.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-214">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="9bd7e-215">Передайте сертификаты удаленного рабочего стола, как на этапе одноразовой настройки, с помощью следующего сценария командлета:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-215">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="9bd7e-216">Например:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="9bd7e-217">Кроме того, вы можете экспортировать PFX-файл сертификата с закрытым ключом и отправлять сертификаты в каждую целевую облачную службу с помощью [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-217">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="9bd7e-218">**Обновление развертывания по сравнению с удалением развертывания и \>созданием развертывания**</span><span class="sxs-lookup"><span data-stu-id="9bd7e-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="9bd7e-219">По умолчанию сценарий будет выполнять развертывание обновления ($enableDeploymentUpgrade = 1) при передаче параметра или значения «1» явным образом.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-219">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="9bd7e-220">Для одного экземпляра это имеет преимущество, поскольку тратится меньше времени, чем на полное развертывание.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="9bd7e-221">Для экземпляров, которым требуется высокий уровень доступности, преимущество состоит в сохранении работы некоторых экземпляров в то время, как другие обновляются (проходя домен обновления), а также не удаляются ваши виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-221">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="9bd7e-222">Развертывание обновления может быть отключено в сценарии ($enableDeploymentUpgrade = 0) или при передаче параметра *-enableDeploymentUpgrade 0* , который изменяет поведение сценария, сначала удаляя все существующие развертывания, а затем создавая новое развертывание.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-222">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9bd7e-223">Сценарий всегда будет удалять или заменять существующие развертывания по умолчанию, если они обнаружены.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-223">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="9bd7e-224">Это необходимо для включения непрерывной доставки из автоматизации, где невозможно вмешательство пользователя или оператора.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="9bd7e-225">5. Публикация пакета с помощью TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="9bd7e-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="9bd7e-226">На этом необязательном шаге будет выполнено подключение TFS Team Build к сценарию, созданному на шаге 4, который обрабатывает публикацию сборки пакета в Azure.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-226">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="9bd7e-227">Это влечет за собой изменение шаблона процесса, использованного определением сборки таким образом, чтобы в конце процесса выполнялось действие Publish.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-227">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="9bd7e-228">Действие Publish выполнит команду PowerShell, передавая параметры из сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-228">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="9bd7e-229">Выходные данные целевых объектов MSBuild и сценария публикации будут направлены в стандартный вывод сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-229">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="9bd7e-230">Редактирование определение сборки, ответственного за непрерывное развертывание.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-230">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="9bd7e-231">Выберите вкладку **Процесс** .</span><span class="sxs-lookup"><span data-stu-id="9bd7e-231">Select the **Process** tab.</span></span>
3. <span data-ttu-id="9bd7e-232">Выполните [эти инструкции](http://msdn.microsoft.com/library/dd647551.aspx) , чтобы добавить проект действия для шаблона процесса сборки, загрузить шаблон по умолчанию, добавить его в проект и применить.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="9bd7e-233">Присвойте шаблону процесса сборки новое имя, например AzureBuildProcessTemplate.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-233">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="9bd7e-234">Вернитесь на вкладку **Процесс** и выберите пункт **Показать сведения**, чтобы просмотреть список доступных шаблонов процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-234">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="9bd7e-235">Нажмите кнопку **Создать...** и перейдите к проекту, который был только что добавлен и зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-235">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="9bd7e-236">Найдите только что созданный шаблон и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-236">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="9bd7e-237">Откройте выбранный шаблон процесса для редактирования.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-237">Open the selected Process Template for editing.</span></span> <span data-ttu-id="9bd7e-238">Его можно открыть непосредственно в конструкторе рабочих процессов или с помощью редактора XML для работы с XAML.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-238">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="9bd7e-239">Добавьте перечисленные ниже новые аргументы в виде отдельных элементов строк на вкладке аргументов конструктора рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-239">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="9bd7e-240">Все аргументы должны иметь параметры direction=In и type=String.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="9bd7e-241">Это будет использоваться для параметров из определения сборки в рабочем процессе, который затем используется для вызова сценария публикации.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-241">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Список аргументов][3]

   <span data-ttu-id="9bd7e-243">Соответствующий код XAML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-243">The corresponding XAML looks like this:</span></span>

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
7. <span data-ttu-id="9bd7e-244">Добавьте новую последовательность в конце агента выполнения.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-244">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="9bd7e-245">Начните с добавления действия инструкции If для проверки допустимого файла сценария.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-245">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="9bd7e-246">Задайте условие для этого значения.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-246">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="9bd7e-247">Для варианта Then в инструкции If добавьте новое действие последовательности.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-247">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="9bd7e-248">Задайте в качестве отображаемого имени "Начало публикации"</span><span class="sxs-lookup"><span data-stu-id="9bd7e-248">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="9bd7e-249">Оставив выбранной последовательность начала публикации, добавьте перечисленные ниже новые переменные в виде отдельных элементов строк на вкладке «Переменные» конструктора рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-249">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="9bd7e-250">Все переменные должны иметь тип String и Scope=Start publish.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="9bd7e-251">Это будет использоваться для параметров из определения сборки в рабочем процессе, который затем используется для вызова сценария публикации.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-251">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="9bd7e-252">SubscriptionDataFilePath типа String.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="9bd7e-253">PublishScriptFilePath типа String.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-253">PublishScriptFilePath, of type String</span></span>

        ![Новые переменные][4]
   4. <span data-ttu-id="9bd7e-255">Если вы используете TFS 2012 или более раннюю версию, добавьте в начало новой последовательности действие ConvertWorkspaceItem.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="9bd7e-256">Если вы используете TFS 2013 или более позднюю версию, добавьте в начало новой последовательности действие GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-256">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="9bd7e-257">Установите свойства ля ConvertWorkspaceItem следующим образом: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-257">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="9bd7e-258">Для действия GetLocalPath задайте свойству IncomingPath значение 'PublishScriptLocation', а свойству Result — значение 'PublishScriptFilePath'.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-258">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="9bd7e-259">Это действие преобразует путь сценария публикации от расположений сервера TFS (если применимо) в стандартный локальный дисковый путь.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-259">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="9bd7e-260">Если вы используете TFS 2012 или более раннюю версию, добавьте в конец новой последовательности еще одно действие ConvertWorkspaceItem.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="9bd7e-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="9bd7e-262">Если вы используете TFS 2013 или более позднюю версию, добавьте еще одно действие GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="9bd7e-263">IncomingPath='SubscriptionDataFileLocation' и Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="9bd7e-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="9bd7e-264">Добавьте действие InvokeProcess в конце новой последовательности.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-264">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="9bd7e-265">Это действие вызывает PowerShell.exe с аргументами, переданными определением сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-265">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="9bd7e-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="9bd7e-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="9bd7e-267">DisplayName = Выполнение сценария публикации</span><span class="sxs-lookup"><span data-stu-id="9bd7e-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="9bd7e-268">FileName = "PowerShell" (включая кавычки)</span><span class="sxs-lookup"><span data-stu-id="9bd7e-268">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="9bd7e-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="9bd7e-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="9bd7e-270">В текстовом поле раздела **Обработка стандартного вывода** InvokeProcess установите значение data.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-270">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="9bd7e-271">Эта переменная предназначена для хранения данных стандартного вывода.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-271">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="9bd7e-272">Добавьте действие WriteBuildMessage прямо под разделом **Обработка стандартного вывода** .</span><span class="sxs-lookup"><span data-stu-id="9bd7e-272">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="9bd7e-273">Установите Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' и Message='data'.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-273">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="9bd7e-274">Это обеспечит запись стандартного вывода сценария в вывод сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-274">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="9bd7e-275">В поле раздела **Обработка вывода ошибки** InvokeProcess установите значение data.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-275">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="9bd7e-276">Эта переменная предназначена для хранения данных стандартной ошибки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-276">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="9bd7e-277">Добавьте действие WriteBuildError прямо под разделом **Обработка вывода ошибки** .</span><span class="sxs-lookup"><span data-stu-id="9bd7e-277">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="9bd7e-278">Установите Message='data'.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-278">Set the Message='data'.</span></span> <span data-ttu-id="9bd7e-279">Это обеспечит запись стандартных ошибок сценария в выводе данных об ошибках сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-279">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="9bd7e-280">Исправьте все ошибки, отмеченные синими восклицательными знаками.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="9bd7e-281">Наведите указатель мыши на восклицательный знак, чтобы получить подсказку по ошибке.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-281">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="9bd7e-282">Сохраните рабочий процесс, чтобы очистить ошибки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-282">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="9bd7e-283">Конечный результат действия рабочего процесса публикации будет выглядеть в конструкторе следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-283">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![Действия рабочего процесса][5]

   <span data-ttu-id="9bd7e-285">Конечный результат действия рабочего процесса публикации будет выглядеть в XAML следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-285">The final result of the publish workflow activities will look like this in XAML:</span></span>

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
8. <span data-ttu-id="9bd7e-286">Сохраните рабочий процесс шаблона процесса сборки и зарегистрируйте этот файл.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-286">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="9bd7e-287">Измените определение сборки (закройте его, если оно уже открыто) и нажмите кнопку **Создать** , если новый шаблон еще не отображается в списке шаблонов процесса.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-287">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="9bd7e-288">Задайте для значения свойств параметров в разделе "Разное" следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9bd7e-288">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="9bd7e-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Это значение является производным от: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="9bd7e-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="9bd7e-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Это значение является производным от: ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="9bd7e-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="9bd7e-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="9bd7e-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="9bd7e-292">ServiceName = "mycloudservicename" *Используйте здесь соответствующее имя облачной службы*</span><span class="sxs-lookup"><span data-stu-id="9bd7e-292">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="9bd7e-293">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="9bd7e-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="9bd7e-294">StorageAccountName = 'mystorageaccountname' *Используйте здесь соответствующее имя учетной записи хранения*</span><span class="sxs-lookup"><span data-stu-id="9bd7e-294">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="9bd7e-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="9bd7e-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="9bd7e-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="9bd7e-296">SubscriptionName = 'default'</span></span>

    ![Значения свойств параметров][6]
11. <span data-ttu-id="9bd7e-298">Сохраните изменения в определении сборки.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-298">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="9bd7e-299">Поставьте в очередь сборку для выполнения пакета сборки и публикации.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-299">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="9bd7e-300">Если есть триггер для установки непрерывного развертывания, это поведение будет выполняться при каждом возврате.</span><span class="sxs-lookup"><span data-stu-id="9bd7e-300">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="9bd7e-301">Шаблон сценария PublishCloudService.ps1</span><span class="sxs-lookup"><span data-stu-id="9bd7e-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
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
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
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

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="9bd7e-302">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9bd7e-302">Next steps</span></span>
<span data-ttu-id="9bd7e-303">Чтобы включить удаленную отладку при использовании непрерывной поставки, см. статью [Включение удаленной отладки при использовании непрерывной поставки для публикации на Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="9bd7e-303">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
