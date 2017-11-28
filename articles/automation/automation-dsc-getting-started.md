---
title: "Приступая к работе с Azure Automation DSC | Документация Майкрософт"
description: "Описание и примеры самых распространенных задач по настройке требуемого состояния службы автоматизации Azure"
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
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="0c013-103">Приступая к работе с DSC службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0c013-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="0c013-104">В этом разделе объясняется, как выполнять самые распространенные задачи с помощью Desired State Configuration (DSC) службы автоматизации Azure, например создание, импорт и компилирование конфигураций, подключение компьютеров для управления, а также просмотр отчетов.</span><span class="sxs-lookup"><span data-stu-id="0c013-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="0c013-105">Общие сведения о DSC службы автоматизации Azure см. в [этой статье](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0c013-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="0c013-106">Документацию по DSC см. в статье [Общие сведения о службе настройки требуемого состояния Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="0c013-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="0c013-107">В этом разделе содержатся пошаговые инструкции по использованию DSC службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="0c013-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="0c013-108">Если необходим пример среды, настроенной без выполнения действий, описанных в этом разделе, можно использовать [следующий шаблон ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="0c013-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="0c013-109">Этот шаблон позволяет настроить полнофункциональную среду DSC службы автоматизации Azure, в том числе виртуальную машину Azure, которой управляет DSC соответствующей службы.</span><span class="sxs-lookup"><span data-stu-id="0c013-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c013-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0c013-110">Prerequisites</span></span>
<span data-ttu-id="0c013-111">Для выполнения примеров в этом разделе необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="0c013-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="0c013-112">Учетная запись службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="0c013-112">An Azure Automation account.</span></span> <span data-ttu-id="0c013-113">Указания по созданию учетной записи запуска от имени пользователя для службы автоматизации Azure см. в статье [Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="0c013-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="0c013-114">Виртуальная машина Azure Resource Manager (неклассическая) под управлением Windows Server 2008 R2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0c013-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="0c013-115">Инструкции по созданию виртуальной машины см. в статье [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0c013-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="0c013-116">Создание конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="0c013-116">Creating a DSC configuration</span></span>
<span data-ttu-id="0c013-117">Мы создадим простую [конфигурацию DSC](https://msdn.microsoft.com/powershell/dsc/configurations) , которая обеспечивает наличие или отсутствие компонента Windows **веб-сервера** (IIS) в зависимости от назначения узлов.</span><span class="sxs-lookup"><span data-stu-id="0c013-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="0c013-118">Запустите интегрированную среду сценариев Windows PowerShell (или любой текстовый редактор).</span><span class="sxs-lookup"><span data-stu-id="0c013-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="0c013-119">Введите следующий текст:</span><span class="sxs-lookup"><span data-stu-id="0c013-119">Type the following text:</span></span>
   
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
3. <span data-ttu-id="0c013-120">Сохраните файл как `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="0c013-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="0c013-121">При этой конфигурации в каждом блоке узла вызывается один ресурс, [ресурс WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), что обеспечивает наличие или отсутствие компонента **веб-сервера** .</span><span class="sxs-lookup"><span data-stu-id="0c013-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="0c013-122">Импорт конфигурации в службу автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0c013-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="0c013-123">Теперь мы импортируем конфигурацию в учетную запись службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="0c013-124">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-125">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-126">В колонке **Учетная запись службы автоматизации** щелкните **Конфигурации DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="0c013-127">В колонке **Конфигурации DSC** щелкните **Добавить конфигурацию**.</span><span class="sxs-lookup"><span data-stu-id="0c013-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="0c013-128">В колонке **Импорт конфигурации** перейдите к файлу `TestConfig.ps1` на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="0c013-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![Снимок экрана: колонка **Импорт конфигурации**](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="0c013-130">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0c013-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="0c013-131">Просмотр конфигурации в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0c013-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="0c013-132">После импорта конфигурацию можно просмотреть на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0c013-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="0c013-133">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-134">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-135">В колонке **Учетная запись службы автоматизации** щелкните **Конфигурации DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="0c013-136">В колонке **Конфигурации DSC** щелкните **TestConfig** (это имя конфигурации, импортированной при выполнении предыдущей процедуры).</span><span class="sxs-lookup"><span data-stu-id="0c013-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="0c013-137">В колонке **Настройка TestConfig** щелкните **Просмотреть источник конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="0c013-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Снимок экрана: колонка "TestConfig configuration" (Конфигурация TestConfig)](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="0c013-139">Откроется колонка **Источник конфигурации TestConfig** , в которой будет отображаться код PowerShell для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0c013-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="0c013-140">Компилирование конфигурации в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0c013-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="0c013-141">Прежде чем применить требуемое состояние к узлу, конфигурацию DSC, определяющую это состояние, следует компилировать в одну или несколько конфигураций узла (MOF-документы) и разместить на опрашивающем сервере Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="0c013-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="0c013-142">Подробное описание компилирования конфигураций в Azure Automation DSC см. в [этой статье](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="0c013-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="0c013-143">Дополнительные сведения о компилировании конфигураций см. в статье [Конфигурации DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="0c013-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="0c013-144">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-145">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-146">В колонке **Учетная запись службы автоматизации** щелкните **Конфигурации DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="0c013-147">В колонке **Конфигурации DSC** щелкните **TestConfig** (имя импортированной ранее конфигурации).</span><span class="sxs-lookup"><span data-stu-id="0c013-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="0c013-148">В колонке **Настройка TestConfig** щелкните **Скомпилировать**, а затем нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="0c013-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="0c013-149">Запустится задание компиляции.</span><span class="sxs-lookup"><span data-stu-id="0c013-149">This starts a compilation job.</span></span>
   
    ![Снимок экрана: колонка "TestConfig configuration" (Конфигурация TestConfig) с выделенной кнопкой "Скомпилировать"](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="0c013-151">Во время компилирования конфигурации в службе автоматизации Azure MOF-файлы любой созданной конфигурации узла автоматически развертываются на опрашивающем сервере.</span><span class="sxs-lookup"><span data-stu-id="0c013-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="0c013-152">Просмотр задания компиляции</span><span class="sxs-lookup"><span data-stu-id="0c013-152">Viewing a compilation job</span></span>
<span data-ttu-id="0c013-153">После запуска компиляции задание можно просмотреть на плитке **Задания компиляции** в колонке **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="0c013-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="0c013-154">На плитке **Задания компиляции** отображаются выполняющиеся, выполненные и невыполненные задания.</span><span class="sxs-lookup"><span data-stu-id="0c013-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="0c013-155">При открытии колонки задания компиляции отображаются сведения об этом задании, в том числе все обнаруженные ошибки или предупреждения, входные параметры, используемые в конфигурации, и журналы компиляции.</span><span class="sxs-lookup"><span data-stu-id="0c013-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="0c013-156">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-157">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-158">В колонке **Учетная запись службы автоматизации** щелкните **Конфигурации DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="0c013-159">В колонке **Конфигурации DSC** щелкните **TestConfig** (имя импортированной ранее конфигурации).</span><span class="sxs-lookup"><span data-stu-id="0c013-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="0c013-160">На плитке **Задания компиляции** колонки **Настройка TestConfig** щелкните одно из перечисленных заданий.</span><span class="sxs-lookup"><span data-stu-id="0c013-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="0c013-161">Откроется колонка **Задание компиляции** с датой начала задания компиляции.</span><span class="sxs-lookup"><span data-stu-id="0c013-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![Снимок экрана: колонка "Задание компиляции"](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="0c013-163">Щелкните любую плитку в колонке **Задание компиляции** , чтобы просмотреть дополнительные сведения о задании.</span><span class="sxs-lookup"><span data-stu-id="0c013-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="0c013-164">Просмотр конфигураций узлов</span><span class="sxs-lookup"><span data-stu-id="0c013-164">Viewing node configurations</span></span>
<span data-ttu-id="0c013-165">При успешном выполнении задания компиляции создается одна или несколько конфигураций узлов.</span><span class="sxs-lookup"><span data-stu-id="0c013-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="0c013-166">Конфигурация узла — это MOF-документ, который развертывается на опрашивающем сервере и готов к извлечению и применению одним или несколькими узлами.</span><span class="sxs-lookup"><span data-stu-id="0c013-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="0c013-167">Конфигурации узлов можно просмотреть в учетной записи службы автоматизации в колонке **Конфигурации узла DSC** .</span><span class="sxs-lookup"><span data-stu-id="0c013-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="0c013-168">Имя конфигурации узла имеет следующий формат: *имя_конфигурации*.*имя_узла*.</span><span class="sxs-lookup"><span data-stu-id="0c013-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="0c013-169">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-170">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-171">В колонке **Учетная запись службы автоматизации** щелкните **Конфигурации узла DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Снимок экрана: колонка "Конфигурации узла DSC"](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="0c013-173">Подключение виртуальной машины Azure для управления с использованием DSC службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="0c013-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="0c013-174">DSC службы автоматизации Azure можно применять для управления виртуальными машинами Azure (классическими или Resource Manager), локальными виртуальными машинами, компьютерами Linux, виртуальными машинами AWS и локальными физическими компьютерами.</span><span class="sxs-lookup"><span data-stu-id="0c013-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="0c013-175">В этом разделе рассматривается подключение только виртуальных машин Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0c013-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="0c013-176">Дополнительные сведения о подключении машин других типов см. в статье [Подключение компьютеров для управления с помощью Azure Automation DSC](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="0c013-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="0c013-177">Чтобы подключить виртуальную машину Azure Resource Manager для управления с помощью DSC службы автоматизации Azure, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="0c013-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="0c013-178">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-179">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-180">В колонке **Учетная запись службы автоматизации** щелкните **Узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="0c013-181">В колонке **Узлы DSC** щелкните **Добавить виртуальную машину Azure**.</span><span class="sxs-lookup"><span data-stu-id="0c013-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Снимок экрана: колонка "Узлы DSC" с выделенной кнопкой "Добавить виртуальную машину Azure"](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="0c013-183">В колонке**Добавить виртуальные машины Azure** щелкните **Выберите виртуальную машину для присоединения**.</span><span class="sxs-lookup"><span data-stu-id="0c013-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="0c013-184">В колонке **Выбрать виртуальные машины** выберите нужную виртуальную машину и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0c013-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0c013-185">Это должна быть виртуальная машина Azure Resource Manager под управлением Windows Server 2008 R2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0c013-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="0c013-186">В колонке **Добавить виртуальные машины Azure** щелкните **Настроить данные регистрации**.</span><span class="sxs-lookup"><span data-stu-id="0c013-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="0c013-187">В колонке **Регистрация** в поле **Имя конфигурации узла** введите имя конфигурации узла, которую необходимо применить к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="0c013-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="0c013-188">Это имя должно совпадать с именем конфигурации узла в учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="0c013-189">На этом этапе указывать имя необязательно.</span><span class="sxs-lookup"><span data-stu-id="0c013-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="0c013-190">После подключения узла назначенную конфигурацию узла можно изменить.</span><span class="sxs-lookup"><span data-stu-id="0c013-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="0c013-191">Установите флажок **Перезагрузить узел при необходимости** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0c013-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Снимок экрана: колонка "Регистрация"](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="0c013-193">Указанная конфигурация узла будет применяться к виртуальной машине с периодичностью, указанной в поле **Частота обновления режима настройки**. Виртуальная машина будет проверять наличие обновлений для конфигурации узла с периодичностью, указанной в поле **Частота обновления**.</span><span class="sxs-lookup"><span data-stu-id="0c013-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="0c013-194">Дополнительные сведения об использовании этих значений см. в статье [Настройка локального диспетчера конфигураций](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="0c013-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="0c013-195">В колонке **Добавить виртуальные машины Azure** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0c013-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="0c013-196">Azure запустит процесс подключения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0c013-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="0c013-197">По завершении процесса виртуальная машина будет отображаться в учетной записи службы автоматизации в колонке **Узлы DSC** .</span><span class="sxs-lookup"><span data-stu-id="0c013-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="0c013-198">Просмотр списка узлов DSC</span><span class="sxs-lookup"><span data-stu-id="0c013-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="0c013-199">Список всех виртуальных машин, подключенных для управления, можно просмотреть в учетной записи службы автоматизации в колонке **Узлы DSC** .</span><span class="sxs-lookup"><span data-stu-id="0c013-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="0c013-200">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-201">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-202">В колонке **Учетная запись службы автоматизации** щелкните **Узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="0c013-203">Просмотр отчетов для узлов DSC</span><span class="sxs-lookup"><span data-stu-id="0c013-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="0c013-204">Каждый раз, когда DSC службы автоматизации Azure проверяет согласованность на управляемом узле, узел отправляет отчет о состоянии на опрашивающий сервер.</span><span class="sxs-lookup"><span data-stu-id="0c013-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="0c013-205">Вы можете просмотреть отчеты в колонке для соответствующего узла.</span><span class="sxs-lookup"><span data-stu-id="0c013-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="0c013-206">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-207">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-208">В колонке **Учетная запись службы автоматизации** щелкните **Узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="0c013-209">На плитке **Отчеты** щелкните один из отчетов в списке.</span><span class="sxs-lookup"><span data-stu-id="0c013-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![Снимок экрана: колонка отчетов](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="0c013-211">В колонке для отдельного отчета можно увидеть следующие сведения о состоянии для соответствующей проверки согласованности.</span><span class="sxs-lookup"><span data-stu-id="0c013-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="0c013-212">Состояние отчета. Находится ли узел в состоянии "Совместимый" или "Несовместимый", а конфигурация — в состоянии "Сбой" (когда для узла установлен режим **applyandmonitor**, а виртуальная машина находится не в требуемом состоянии).</span><span class="sxs-lookup"><span data-stu-id="0c013-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="0c013-213">Время начала проверки согласованности.</span><span class="sxs-lookup"><span data-stu-id="0c013-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="0c013-214">Общее время выполнения проверки согласованности.</span><span class="sxs-lookup"><span data-stu-id="0c013-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="0c013-215">Тип проверки согласованности.</span><span class="sxs-lookup"><span data-stu-id="0c013-215">The type of consistency check.</span></span>
* <span data-ttu-id="0c013-216">Все ошибки, в том числе код и сообщение ошибки.</span><span class="sxs-lookup"><span data-stu-id="0c013-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="0c013-217">Все ресурсы DSC, используемые в конфигурации, и состояние каждого ресурса (находится ли узел в требуемом состоянии для этого ресурса). Щелкните каждый ресурс, чтобы получить дополнительные сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="0c013-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="0c013-218">Имя, IP-адрес и режим конфигурации узла.</span><span class="sxs-lookup"><span data-stu-id="0c013-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="0c013-219">Кроме того, можно щелкнуть **Просмотреть необработанный отчет**, чтобы просмотреть фактические данные, которые узел отправляет на сервер.</span><span class="sxs-lookup"><span data-stu-id="0c013-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="0c013-220">Дополнительные сведения об использовании этих данных см. в статье [Использование сервера отчетов DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="0c013-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="0c013-221">После подключения узла первый отчет станет доступным через некоторое время.</span><span class="sxs-lookup"><span data-stu-id="0c013-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="0c013-222">Может пройти около 30 минут, прежде чем первый отчет станет доступным после подключения узла.</span><span class="sxs-lookup"><span data-stu-id="0c013-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="0c013-223">Переназначение узла другой конфигурации</span><span class="sxs-lookup"><span data-stu-id="0c013-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="0c013-224">Узел можно назначить для использования конфигурации, которая отличается от назначенной изначально.</span><span class="sxs-lookup"><span data-stu-id="0c013-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="0c013-225">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-226">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-227">В колонке **Учетная запись службы автоматизации** щелкните **Узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="0c013-228">В колонке **Узлы DSC** щелкните имя узла, который необходимо переназначить.</span><span class="sxs-lookup"><span data-stu-id="0c013-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="0c013-229">В колонке этого узла нажмите кнопку **Назначить узел**.</span><span class="sxs-lookup"><span data-stu-id="0c013-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![Снимок экрана: колонка "Узел" с выделенной кнопкой "Assign Node" (Назначить узел)](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="0c013-231">В колонке **Назначить конфигурацию узла** выберите конфигурацию, которой необходимо назначить узел, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0c013-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![Снимок экрана: колонка "Назначить конфигурацию узла"](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="0c013-233">Отмена регистрации узла</span><span class="sxs-lookup"><span data-stu-id="0c013-233">Unregistering a node</span></span>
<span data-ttu-id="0c013-234">Если больше не требуется управлять узлом с использованием DSC службы автоматизации Azure, можно отменить регистрацию.</span><span class="sxs-lookup"><span data-stu-id="0c013-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="0c013-235">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c013-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c013-236">В меню концентратора щелкните **Все ресурсы** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="0c013-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="0c013-237">В колонке **Учетная запись службы автоматизации** щелкните **Узлы DSC**.</span><span class="sxs-lookup"><span data-stu-id="0c013-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="0c013-238">В колонке **Узлы DSC** щелкните имя узла, регистрацию которого нужно отменить.</span><span class="sxs-lookup"><span data-stu-id="0c013-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="0c013-239">В колонке для этого узла нажмите кнопку **Отменить регистрацию**.</span><span class="sxs-lookup"><span data-stu-id="0c013-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![Снимок экрана: колонка "Узел" с выделенной кнопкой "Отменить регистрацию"](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="0c013-241">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="0c013-241">Related Articles</span></span>
* [<span data-ttu-id="0c013-242">Обзор Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="0c013-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="0c013-243">Подключение компьютеров для управления с помощью Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="0c013-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="0c013-244">Общие сведения о платформе Desired State Configuration Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c013-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="0c013-245">Командлеты Automation DSC Azure</span><span class="sxs-lookup"><span data-stu-id="0c013-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="0c013-246">Цены на Automation DSC Azure</span><span class="sxs-lookup"><span data-stu-id="0c013-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

