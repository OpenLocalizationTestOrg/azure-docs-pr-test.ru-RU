---
title: "aaaGetting работы с DSC службы автоматизации Azure | Документы Microsoft"
description: "Описание и примеры использования hello наиболее распространенные задачи в Azure Automation требуемого состояния (DSC)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="5c940-103">Приступая к работе с DSC службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5c940-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="5c940-104">В этом разделе объясняется, как toodo hello наиболее распространенные задачи с Azure Automation требуемого состояния (DSC), таких как создание, Импорт и компиляции конфигурации адаптации машин слишком управлять ими и просмотр отчетов.</span><span class="sxs-lookup"><span data-stu-id="5c940-104">This topic explains how toodo hello most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines too manage, and viewing reports.</span></span> <span data-ttu-id="5c940-105">Общие сведения о DSC службы автоматизации Azure см. в [этой статье](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c940-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="5c940-106">Документацию по DSC см. в статье [Общие сведения о службе настройки требуемого состояния Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="5c940-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="5c940-107">Этот раздел содержит пошаговое руководство по toousing DSC службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5c940-107">This topic provides a step-by-step guide toousing Azure Automation DSC.</span></span> <span data-ttu-id="5c940-108">Если требуется, чтобы среде образец, в которой уже настроена без hello действий, описанных в этом разделе, можно использовать [hello следующий шаблон ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="5c940-108">If you want a sample environment that is already set up without following hello steps described in this topic, you can use [hello following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="5c940-109">Этот шаблон позволяет настроить полнофункциональную среду DSC службы автоматизации Azure, в том числе виртуальную машину Azure, которой управляет DSC соответствующей службы.</span><span class="sxs-lookup"><span data-stu-id="5c940-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c940-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c940-110">Prerequisites</span></span>
<span data-ttu-id="5c940-111">toocomplete hello примеры в этом разделе, hello требуются следующие сертификаты:</span><span class="sxs-lookup"><span data-stu-id="5c940-111">toocomplete hello examples in this topic, hello following are required:</span></span>

* <span data-ttu-id="5c940-112">Учетная запись службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5c940-112">An Azure Automation account.</span></span> <span data-ttu-id="5c940-113">Указания по созданию учетной записи запуска от имени пользователя для службы автоматизации Azure см. в статье [Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="5c940-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="5c940-114">Виртуальная машина Azure Resource Manager (неклассическая) под управлением Windows Server 2008 R2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5c940-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="5c940-115">Инструкции по созданию виртуальной Машины см. в разделе [создания первой виртуальной машине Windows в hello портал Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="5c940-115">For instructions on creating a VM, see [Create your first Windows virtual machine in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="5c940-116">Создание конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="5c940-116">Creating a DSC configuration</span></span>
<span data-ttu-id="5c940-117">Мы создадим простой [конфигурации DSC](https://msdn.microsoft.com/powershell/dsc/configurations) таким образом hello наличие или отсутствие hello **веб-сервера** Windows функция (IIS), в зависимости от того, как назначить узлы.</span><span class="sxs-lookup"><span data-stu-id="5c940-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either hello presence or absence of hello **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="5c940-118">Запустите Windows PowerShell ISE hello (или любой текстовый редактор).</span><span class="sxs-lookup"><span data-stu-id="5c940-118">Start hello Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="5c940-119">Введите следующий текст hello:</span><span class="sxs-lookup"><span data-stu-id="5c940-119">Type hello following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="5c940-120">Сохраните файл как файл hello `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="5c940-120">Save hello file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="5c940-121">Эта конфигурация вызывает один ресурс в каждом блоке узла hello [ресурс WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), таким образом hello наличие или отсутствие hello **веб-сервера** компонентов.</span><span class="sxs-lookup"><span data-stu-id="5c940-121">This configuration calls one resource in each node block, hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either hello presence or absence of hello **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="5c940-122">Импорт конфигурации в службу автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5c940-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="5c940-123">Затем мы будем импортируйте конфигурации hello в hello учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-123">Next, we'll import hello configuration into hello Automation account.</span></span>

1. <span data-ttu-id="5c940-124">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-125">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-125">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-126">На hello **учетной записи автоматизации** колонка, щелкните **конфигураций DSC**.</span><span class="sxs-lookup"><span data-stu-id="5c940-126">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="5c940-127">На hello **конфигураций DSC** колонка, щелкните **Добавление конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="5c940-127">On hello **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="5c940-128">На hello **Импорт конфигурации** колонки, обзора toohello `TestConfig.ps1` файл на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="5c940-128">On hello **Import Configuration** blade, browse toohello `TestConfig.ps1` file on your computer.</span></span>
   
    ![Снимок экрана: hello ** импорта конфигурации ** колонку](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="5c940-130">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5c940-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="5c940-131">Просмотр конфигурации в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5c940-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="5c940-132">После импорта конфигурации, его можно просмотреть в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5c940-132">After you have imported a configuration, you can view it in hello Azure portal.</span></span>

1. <span data-ttu-id="5c940-133">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-133">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-134">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-134">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-135">На hello **учетной записи автоматизации** колонка, щелкните **конфигураций DSC**</span><span class="sxs-lookup"><span data-stu-id="5c940-135">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="5c940-136">На hello **конфигураций DSC** колонка, щелкните **TestConfig** (это имя hello hello конфигурации, импортированных в предыдущей процедуре hello).</span><span class="sxs-lookup"><span data-stu-id="5c940-136">On hello **DSC Configurations** blade, click **TestConfig** (this is hello name of hello configuration you imported in hello previous procedure).</span></span>
5. <span data-ttu-id="5c940-137">На hello **конфигурации TestConfig** колонка, щелкните **источник конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="5c940-137">On hello **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Снимок экрана: колонка конфигурации TestConfig hello](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="5c940-139">Объект **источник конфигурации TestConfig** колонке откроется кода hello PowerShell для настройки hello.</span><span class="sxs-lookup"><span data-stu-id="5c940-139">A **TestConfig Configuration source** blade opens, displaying hello PowerShell code for hello configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="5c940-140">Компилирование конфигурации в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5c940-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="5c940-141">Перед установкой требуемого состояния узла tooa конфигурации DSC, определяя, состояние должно быть компилируются в одну или несколько конфигураций узла (MOF-документа) и поместить в hello опрашивающего сервера DSC службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-141">Before you can apply a desired state tooa node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on hello Automation DSC Pull Server.</span></span> <span data-ttu-id="5c940-142">Подробное описание компилирования конфигураций в Azure Automation DSC см. в [этой статье](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="5c940-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="5c940-143">Дополнительные сведения о компилировании конфигураций см. в статье [Конфигурации DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="5c940-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="5c940-144">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-144">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-145">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-145">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-146">На hello **учетной записи автоматизации** колонка, щелкните **конфигураций DSC**</span><span class="sxs-lookup"><span data-stu-id="5c940-146">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="5c940-147">На hello **конфигураций DSC** колонка, щелкните **TestConfig** (имя hello hello ранее импортированные конфигурации).</span><span class="sxs-lookup"><span data-stu-id="5c940-147">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="5c940-148">На hello **TestConfig конфигурации** колонке нажмите кнопку **компиляции**, а затем нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="5c940-148">On hello **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="5c940-149">Запустится задание компиляции.</span><span class="sxs-lookup"><span data-stu-id="5c940-149">This starts a compilation job.</span></span>
   
    ![Снимок экрана: колонка конфигурации TestConfig hello, выделение кнопки компиляции](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="5c940-151">При компиляции конфигурации в службе автоматизации Azure автоматически разворачивает любой созданный узел toohello MOF-файлы конфигурации опрашивающего сервера.</span><span class="sxs-lookup"><span data-stu-id="5c940-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs toohello pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="5c940-152">Просмотр задания компиляции</span><span class="sxs-lookup"><span data-stu-id="5c940-152">Viewing a compilation job</span></span>
<span data-ttu-id="5c940-153">После запуска компиляции, его можно просмотреть в hello **задания компиляции** плитки в hello **конфигурации** колонку.</span><span class="sxs-lookup"><span data-stu-id="5c940-153">After you start a compilation, you can view it in hello **Compilation jobs** tile in hello **Configuration** blade.</span></span> <span data-ttu-id="5c940-154">Hello **задания компиляции** плитки показывает выполняющихся, завершен, а также задания со сбоями.</span><span class="sxs-lookup"><span data-stu-id="5c940-154">hello **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="5c940-155">При открытии в колонке задания компиляции, он отображает сведения об этом задании, включая любые ошибок или предупреждений, входные параметры в конфигурации hello и компиляция журналы.</span><span class="sxs-lookup"><span data-stu-id="5c940-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in hello configuration, and compilation logs.</span></span>

1. <span data-ttu-id="5c940-156">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-157">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-157">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-158">На hello **учетной записи автоматизации** колонка, щелкните **конфигураций DSC**.</span><span class="sxs-lookup"><span data-stu-id="5c940-158">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="5c940-159">На hello **конфигураций DSC** колонка, щелкните **TestConfig** (имя hello hello ранее импортированные конфигурации).</span><span class="sxs-lookup"><span data-stu-id="5c940-159">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="5c940-160">На hello **задания компиляции** плитки приветствия **TestConfig конфигурации** колонка, щелкните любой hello заданиями.</span><span class="sxs-lookup"><span data-stu-id="5c940-160">On hello **Compilation jobs** tile of hello **TestConfig Configuration** blade, click on any of hello jobs listed.</span></span> <span data-ttu-id="5c940-161">Объект **задание компиляции** запуска открывается колонка, помеченные hello дату hello задание компиляции.</span><span class="sxs-lookup"><span data-stu-id="5c940-161">A **Compilation Job** blade opens, labeled with hello date that hello compilation job was started.</span></span>
   
    ![Снимок экрана: колонка задание компиляции hello](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="5c940-163">Щелкните одну из них hello **задание компиляции** дальнейшей toosee колонки сведений о hello задания.</span><span class="sxs-lookup"><span data-stu-id="5c940-163">Click on any tile in hello **Compilation Job** blade toosee further details about hello job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="5c940-164">Просмотр конфигураций узлов</span><span class="sxs-lookup"><span data-stu-id="5c940-164">Viewing node configurations</span></span>
<span data-ttu-id="5c940-165">При успешном выполнении задания компиляции создается одна или несколько конфигураций узлов.</span><span class="sxs-lookup"><span data-stu-id="5c940-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="5c940-166">Конфигурация узла является MOF-документ, развернутых toohello опрашивающего сервера и готов toobe извлекать и применить один или несколько узлов.</span><span class="sxs-lookup"><span data-stu-id="5c940-166">A node configuration is a MOF document that is deployed toohello pull server and ready toobe pulled and applied by one or more nodes.</span></span> <span data-ttu-id="5c940-167">Можно просмотреть конфигурацию узла hello в вашей учетной записи автоматизации в hello **конфигурации узла DSC** колонку.</span><span class="sxs-lookup"><span data-stu-id="5c940-167">You can view hello node configurations in your Automation account in hello **DSC Node Configurations** blade.</span></span> <span data-ttu-id="5c940-168">Настройка узла имеет имя, состоящее из формы hello *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="5c940-168">A node configuration has a name with hello form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="5c940-169">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-170">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-170">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-171">На hello **учетной записи автоматизации** колонка, щелкните **конфигурации узла DSC**.</span><span class="sxs-lookup"><span data-stu-id="5c940-171">On hello **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Снимок экрана: колонка hello конфигурации узла DSC](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="5c940-173">Подключение виртуальной машины Azure для управления с использованием DSC службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5c940-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="5c940-174">Можно использовать виртуальные машины Azure Automation DSC toomanage Azure (классический и диспетчера ресурсов), виртуальные машины в локальной, машины Linux, виртуальные машины AWS и локальных физических компьютеров.</span><span class="sxs-lookup"><span data-stu-id="5c940-174">You can use Azure Automation DSC toomanage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="5c940-175">В этом разделе будет рассматриваться как tooonboard только виртуальные машины диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5c940-175">In this topic, we cover how tooonboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="5c940-176">Дополнительные сведения о подключении машин других типов см. в статье [Подключение компьютеров для управления с помощью Azure Automation DSC](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="5c940-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="5c940-177">tooonboard ВМ Azure Resource Manager для управления с помощью DSC службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5c940-177">tooonboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="5c940-178">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-179">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-179">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-180">На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="5c940-180">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="5c940-181">В hello **узлы DSC** колонка, щелкните **добавить виртуальную Машину Azure**.</span><span class="sxs-lookup"><span data-stu-id="5c940-181">In hello **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Снимок экрана: колонка узлы DSC hello выделение hello виртуальной Машине Azure, добавить кнопки](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="5c940-183">В hello **добавить виртуальные машины Azure** колонка, щелкните **выберите виртуальные машины tooonboard**.</span><span class="sxs-lookup"><span data-stu-id="5c940-183">In hello **Add Azure VMs** blade, click **Select virtual machines tooonboard**.</span></span>
6. <span data-ttu-id="5c940-184">В hello **выберите виртуальные машины** колонке выберите hello ВМ tooonboard и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5c940-184">In hello **Select VMs** blade, select hello VM you want tooonboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5c940-185">Это должна быть виртуальная машина Azure Resource Manager под управлением Windows Server 2008 R2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5c940-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="5c940-186">В hello **добавить виртуальные машины Azure** колонка, щелкните **Настройка регистрационные данные**.</span><span class="sxs-lookup"><span data-stu-id="5c940-186">In hello **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="5c940-187">В hello **регистрации** колонки, введите имя hello hello узла конфигурации требуется toohello tooapply ВМ в hello **имя конфигурации узла** поле.</span><span class="sxs-lookup"><span data-stu-id="5c940-187">In hello **Registration** blade, enter hello name of hello node configuration you want tooapply toohello VM in hello **Node Configuration Name** box.</span></span> <span data-ttu-id="5c940-188">Имя конфигурации узла в учетной записи автоматизации hello hello должно совпадать.</span><span class="sxs-lookup"><span data-stu-id="5c940-188">This must exactly match hello name of a node configuration in hello Automation account.</span></span> <span data-ttu-id="5c940-189">На этом этапе указывать имя необязательно.</span><span class="sxs-lookup"><span data-stu-id="5c940-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="5c940-190">Можно изменить конфигурации узла назначен hello после адаптации hello узла.</span><span class="sxs-lookup"><span data-stu-id="5c940-190">You can change hello assigned node configuration after onboarding hello node.</span></span>
   <span data-ttu-id="5c940-191">Установите флажок **Перезагрузить узел при необходимости** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5c940-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Снимок экрана: колонка регистрации hello](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="5c940-193">Hello узел конфигурацию, заданную будет применен toohello ВМ с интервалами, указанными с hello **частота обновления режима конфигурации**, и hello виртуальной Машины будет проверять наличие обновлений конфигурации узла toohello с интервалами, указанными с hello  **Частота обновления**.</span><span class="sxs-lookup"><span data-stu-id="5c940-193">hello node configuration you specified will be applied toohello VM at intervals specified by hello **Configuration Mode Frequency**, and hello VM will check for updates toohello node configuration at intervals specified by hello **Refresh Frequency**.</span></span> <span data-ttu-id="5c940-194">Дополнительные сведения об использовании этих значений см. в разделе [hello Настройка локального диспетчера конфигураций](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="5c940-194">For more information about how these values are used, see [Configuring hello Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="5c940-195">В hello **добавить виртуальные машины Azure** колонка, щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="5c940-195">In hello **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="5c940-196">Azure будет запускаться hello процесс адаптации hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5c940-196">Azure will start hello process of onboarding hello VM.</span></span> <span data-ttu-id="5c940-197">После завершения hello виртуальной Машины будут отображаться в hello **узлы DSC** колонки в hello учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-197">When it is complete, hello VM will show up in hello **DSC Nodes** blade in hello Automation account.</span></span>

## <a name="viewing-hello-list-of-dsc-nodes"></a><span data-ttu-id="5c940-198">Просмотр списка hello узлы DSC</span><span class="sxs-lookup"><span data-stu-id="5c940-198">Viewing hello list of DSC nodes</span></span>
<span data-ttu-id="5c940-199">Можно просмотреть список hello всех компьютеров, которые были выставленных для управления в вашей учетной записи автоматизации в hello **узлы DSC** колонку.</span><span class="sxs-lookup"><span data-stu-id="5c940-199">You can view hello list of all machines that have been onboarded for management in your Automation account in hello **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="5c940-200">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-200">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-201">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-201">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-202">На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="5c940-202">On hello **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="5c940-203">Просмотр отчетов для узлов DSC</span><span class="sxs-lookup"><span data-stu-id="5c940-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="5c940-204">Каждый раз, DSC службы автоматизации Azure выполняет проверку согласованности на управляемом узле, узел hello отправляет состояние отчета задней toohello опрашивающего сервера.</span><span class="sxs-lookup"><span data-stu-id="5c940-204">Each time Azure Automation DSC performs a consistency check on a managed node, hello node sends a status report back toohello pull server.</span></span> <span data-ttu-id="5c940-205">Эти отчеты можно просматривать в колонке hello для этого узла.</span><span class="sxs-lookup"><span data-stu-id="5c940-205">You can view these reports on hello blade for that node.</span></span>

1. <span data-ttu-id="5c940-206">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-206">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-207">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-207">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-208">На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="5c940-208">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="5c940-209">На hello **отчеты** эскиза, щелкните в любом hello отчеты в списке hello.</span><span class="sxs-lookup"><span data-stu-id="5c940-209">On hello **Reports** tile, click on any of hello reports in hello list.</span></span>
   
    ![Снимок экрана: колонка hello отчета](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="5c940-211">В колонке hello для отдельного отчета можно увидеть следующие сведения о состоянии для соответствующего согласованности hello hello Проверьте:</span><span class="sxs-lookup"><span data-stu-id="5c940-211">On hello blade for an individual report, you can see hello following status information for hello corresponding consistency check:</span></span>

* <span data-ttu-id="5c940-212">Здравствуйте, отчет о состоянии — ли узел hello hello конфигурации «Сбой», «совместимый» или узел hello» не является совместимым» (если hello узел находится в **applyandmonitor** режим и hello машина не находится в состоянии требуемого hello).</span><span class="sxs-lookup"><span data-stu-id="5c940-212">hello report status — whether hello node is "Compliant", hello configuration "Failed", or hello node is "Not Compliant" (when hello node is in **applyandmonitor** mode and hello machine is not in hello desired state).</span></span>
* <span data-ttu-id="5c940-213">время начала Hello hello проверку согласованности.</span><span class="sxs-lookup"><span data-stu-id="5c940-213">hello start time for hello consistency check.</span></span>
* <span data-ttu-id="5c940-214">Проверьте Hello общего времени выполнения для обеспечения согласованности hello.</span><span class="sxs-lookup"><span data-stu-id="5c940-214">hello total runtime for hello consistency check.</span></span>
* <span data-ttu-id="5c940-215">Проверьте тип Hello согласованности.</span><span class="sxs-lookup"><span data-stu-id="5c940-215">hello type of consistency check.</span></span>
* <span data-ttu-id="5c940-216">Все ошибки, включая hello ошибка код и сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5c940-216">Any errors, including hello error code and error message.</span></span> 
* <span data-ttu-id="5c940-217">Все ресурсы DSC, в конфигурации hello и hello состояния каждого ресурса (ли hello узел находится в состоянии hello требуемого для этого ресурса), можно щелкнуть на каждый ресурс tooget более подробные сведения для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="5c940-217">Any DSC resources used in hello configuration, and hello state of each resource (whether hello node is in hello desired state for that resource) — you can click on each resource tooget more detailed information for that resource.</span></span>
* <span data-ttu-id="5c940-218">Привет, IP-адрес и режим конфигурации узла hello.</span><span class="sxs-lookup"><span data-stu-id="5c940-218">hello name, IP address, and configuration mode of hello node.</span></span>

<span data-ttu-id="5c940-219">Можно также щелкнуть **просмотра отчета** фактические данные hello toosee, который hello узел отправляет toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="5c940-219">You can also click **View raw report** toosee hello actual data that hello node sends toohello server.</span></span> <span data-ttu-id="5c940-220">Дополнительные сведения об использовании этих данных см. в статье [Использование сервера отчетов DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="5c940-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="5c940-221">Он может занять некоторое время после узла выставленных до первого отчета hello доступен.</span><span class="sxs-lookup"><span data-stu-id="5c940-221">It can take some time after a node is onboarded before hello first report is available.</span></span> <span data-ttu-id="5c940-222">Может потребоваться toowait копирование too30 минут для первого отчета hello окончании освоить узла.</span><span class="sxs-lookup"><span data-stu-id="5c940-222">You might need toowait up too30 minutes for hello first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-tooa-different-node-configuration"></a><span data-ttu-id="5c940-223">Переназначение другой узел tooa с узлом</span><span class="sxs-lookup"><span data-stu-id="5c940-223">Reassigning a node tooa different node configuration</span></span>
<span data-ttu-id="5c940-224">Можно назначить toouse узла конфигурации другому узлу не hello, начальным значением.</span><span class="sxs-lookup"><span data-stu-id="5c940-224">You can assign a node toouse a different node configuration than hello one you initially assigned.</span></span>

1. <span data-ttu-id="5c940-225">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-225">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-226">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-226">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-227">На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="5c940-227">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="5c940-228">На hello **узлы DSC** колонке нажмите имя hello hello узла требуется tooreassign.</span><span class="sxs-lookup"><span data-stu-id="5c940-228">On hello **DSC Nodes** blade, click on hello name of hello node you want tooreassign.</span></span>
5. <span data-ttu-id="5c940-229">В колонке hello для этого узла, щелкните **узел назначения**.</span><span class="sxs-lookup"><span data-stu-id="5c940-229">On hello blade for that node, click **Assign node**.</span></span>
   
    ![Снимок экрана: колонка узел hello выделение hello назначить узел кнопки](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="5c940-231">На hello **назначить конфигурацию узла** колонки, выберите hello узла конфигурации toowhich tooassign hello узел и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5c940-231">On hello **Assign Node Configuration** blade, select hello node configuration toowhich you want tooassign hello node, and then click **OK**.</span></span>
   
    ![Снимок экрана: колонка hello конфигурации узла назначения](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="5c940-233">Отмена регистрации узла</span><span class="sxs-lookup"><span data-stu-id="5c940-233">Unregistering a node</span></span>
<span data-ttu-id="5c940-234">Если вы больше не требуется toobe узла, под управлением Azure Automation DSC, можно отменить его регистрацию.</span><span class="sxs-lookup"><span data-stu-id="5c940-234">If you no longer want a node toobe managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="5c940-235">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c940-235">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5c940-236">Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5c940-236">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="5c940-237">На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="5c940-237">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="5c940-238">На hello **узлы DSC** колонке нажмите имя hello hello узла требуется toounregister.</span><span class="sxs-lookup"><span data-stu-id="5c940-238">On hello **DSC Nodes** blade, click on hello name of hello node you want toounregister.</span></span>
5. <span data-ttu-id="5c940-239">В колонке hello для этого узла, щелкните **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="5c940-239">On hello blade for that node, click **Unregister**.</span></span>
   
    ![Снимок экрана: колонка узел hello выделение кнопки Unregister hello](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="5c940-241">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="5c940-241">Related Articles</span></span>
* [<span data-ttu-id="5c940-242">Обзор Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="5c940-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="5c940-243">Подключение компьютеров для управления с помощью Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="5c940-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="5c940-244">Общие сведения о платформе Desired State Configuration Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c940-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="5c940-245">Командлеты Automation DSC Azure</span><span class="sxs-lookup"><span data-stu-id="5c940-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="5c940-246">Цены на Automation DSC Azure</span><span class="sxs-lookup"><span data-stu-id="5c940-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

