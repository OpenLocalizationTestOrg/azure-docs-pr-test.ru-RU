---
title: "aaaInstalling заданий эластичных баз данных | Документы Microsoft"
description: "Показывает, как установить компонент эластичного задания hello."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="c2575-103">Обзор установки заданий обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="c2575-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="c2575-104">[**Заданий эластичных баз данных** ](sql-database-elastic-jobs-overview.md) может быть выполнена с помощью PowerShell или с помощью hello классический Portal.You Azure можно получить доступ к toocreate задания и управлять ими с помощью API-интерфейса PowerShell hello только в том случае, если установить пакет PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="c2575-105">Кроме того API-интерфейсов PowerShell hello предоставляют значительно больше возможностей, чем hello портала на данный момент времени.</span><span class="sxs-lookup"><span data-stu-id="c2575-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="c2575-106">Если вы уже установили **заданий эластичных баз данных** через hello портала из существующей **эластичного пула**, hello последней предварительной версии Powershell включает в себя сценарии tooupgrade существующей установки.</span><span class="sxs-lookup"><span data-stu-id="c2575-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="c2575-107">Это настоятельно рекомендуется tooupgrade toohello вашей установки последних **заданий эластичных баз данных** компонентов в порядке tootake преимуществами новых функциональных возможностей, предоставляемых через hello API-интерфейсов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2575-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2575-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2575-108">Prerequisites</span></span>
* <span data-ttu-id="c2575-109">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="c2575-109">An Azure subscription.</span></span> <span data-ttu-id="c2575-110">Бесплатная пробная версия доступна [здесь](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2575-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c2575-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2575-111">Azure PowerShell.</span></span> <span data-ttu-id="c2575-112">Установить последнюю версию hello, с помощью hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="c2575-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="c2575-113">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c2575-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c2575-114">[Программы командной строки NuGet](https://nuget.org/nuget.exe) — пакет эластичной базы данных заданий, используется tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="c2575-115">Дополнительные сведения см. по адресу http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="c2575-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="c2575-116">Загрузите и импортируйте пакет PowerShell заданий эластичных баз данных hello</span><span class="sxs-lookup"><span data-stu-id="c2575-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="c2575-117">Запустите командное окно Microsoft Azure PowerShell и перейдите в каталог toohello, который вы загрузили служебной программы командной строки NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="c2575-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="c2575-118">Загрузите и импортируйте **заданий эластичных баз данных** пакета в текущем каталоге hello с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2575-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="c2575-119">Hello **заданий эластичных баз данных** файлы помещаются в локальном каталоге hello в папку с именем **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** где *x.x.xxxx.x* Отображает номер версии hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="c2575-120">командлеты PowerShell Hello (включая необходимых клиентских библиотек) находятся в hello **tools\ElasticDatabaseJobs** вложенный каталог hello tooinstall сценариев PowerShell, а также удалить также находятся в hello  **средства** вложенный каталог.</span><span class="sxs-lookup"><span data-stu-id="c2575-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="c2575-121">Перейти toohello средства вложенный каталог в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello, введя средства компакт-диска, например:</span><span class="sxs-lookup"><span data-stu-id="c2575-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="c2575-122">Выполнение hello.\InstallElasticDatabaseJobsCmdlets.ps1 сценария toocopy hello ElasticDatabaseJobs каталог в $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="c2575-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="c2575-123">Это также автоматически импортирует hello модуль для использования, например:</span><span class="sxs-lookup"><span data-stu-id="c2575-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="c2575-124">Установить компоненты задания hello эластичной базы данных, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2575-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="c2575-125">Запустите командную строку Microsoft Azure PowerShell и перейдите toohello \tools вложенный каталог в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello: Введите \tools компакт-диска</span><span class="sxs-lookup"><span data-stu-id="c2575-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="c2575-126">Выполнить сценарий PowerShell.\InstallElasticDatabaseJobs.ps1 hello и передают значения для запрошенного переменных.</span><span class="sxs-lookup"><span data-stu-id="c2575-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="c2575-127">Этот скрипт создает hello компонентами, описанными в [заданий эластичных баз данных компонентов и цен](sql-database-elastic-jobs-overview.md#components-and-pricing) вместе с Настройка hello облачной службы Azure tooappropriately использовать hello зависимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="c2575-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="c2575-128">При выполнении этой команды появится окно с запросом **имени пользователя** и **пароля**.</span><span class="sxs-lookup"><span data-stu-id="c2575-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="c2575-129">Это не учетные данные Azure, введите hello имя пользователя и пароль, который будет иметь учетные данные администратора hello, следует использовать toocreate для нового сервера hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="c2575-130">можно изменять параметры Hello, предоставляемые на этот образец вызова для необходимые настройки.</span><span class="sxs-lookup"><span data-stu-id="c2575-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="c2575-131">Hello ниже приведены дополнительные сведения на поведение hello каждого параметра:</span><span class="sxs-lookup"><span data-stu-id="c2575-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="c2575-132">Параметр</span><span class="sxs-lookup"><span data-stu-id="c2575-132">Parameter</span></span></th>
    <th><span data-ttu-id="c2575-133">Описание</span><span class="sxs-lookup"><span data-stu-id="c2575-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="c2575-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="c2575-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="c2575-135">Предоставляет имя группы ресурсов Azure hello, созданные toocontain hello вновь созданные компоненты Azure.</span><span class="sxs-lookup"><span data-stu-id="c2575-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="c2575-136">Этот параметр по умолчанию слишком «__ElasticDatabaseJob».</span><span class="sxs-lookup"><span data-stu-id="c2575-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="c2575-137">Это не рекомендуется toochange это значение.</span><span class="sxs-lookup"><span data-stu-id="c2575-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="c2575-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="c2575-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="c2575-139">Предоставляет toobe расположение Azure hello для hello в создаваемых компонентах Azure.</span><span class="sxs-lookup"><span data-stu-id="c2575-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="c2575-140">Этот параметр по умолчанию toohello расположение центральной части США.</span><span class="sxs-lookup"><span data-stu-id="c2575-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="c2575-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="c2575-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="c2575-142">Предоставляет номер hello tooinstall службы рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="c2575-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="c2575-143">Этот параметр по умолчанию too1.</span><span class="sxs-lookup"><span data-stu-id="c2575-143">This parameter defaults too1.</span></span> <span data-ttu-id="c2575-144">Увеличение количества рабочих процессов может быть используется tooscale out hello службы и tooprovide высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="c2575-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="c2575-145">Рекомендуется toouse «2» для развертываний, которые требуется высокий уровень доступности службы hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="c2575-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="c2575-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="c2575-147">Предоставляет hello размер виртуальной Машины для использования в пределах hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="c2575-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="c2575-148">Этот параметр по умолчанию tooA0.</span><span class="sxs-lookup"><span data-stu-id="c2575-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="c2575-149">Допустимы значения параметров из A0/A1 и A2/A3 заставляющие hello рабочей роли toouse размер очень мелкий/малого и среднего и широкого соответственно.</span><span class="sxs-lookup"><span data-stu-id="c2575-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="c2575-150">Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="c2575-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="c2575-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="c2575-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="c2575-152">Предоставляет hello целевой уровень обслуживания Standard edition.</span><span class="sxs-lookup"><span data-stu-id="c2575-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="c2575-153">Этот параметр по умолчанию tooS0.</span><span class="sxs-lookup"><span data-stu-id="c2575-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="c2575-154">Значения параметров S0 или S1 и S2 и S3 принимаются заставляющие hello базы данных SQL Azure toouse Здравствуйте, соответствующего цели уровня Обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c2575-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="c2575-155">Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="c2575-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="c2575-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="c2575-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="c2575-157">Содержит имя пользователя администратора hello для hello только что созданный сервер базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c2575-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="c2575-158">Если не указан, в окне учетные данные PowerShell будет открыта tooprompt hello учетных данных.</span><span class="sxs-lookup"><span data-stu-id="c2575-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="c2575-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="c2575-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="c2575-160">Предоставляет пароль администратора hello hello только что созданный сервер базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c2575-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="c2575-161">Если не указано, PowerShell учетных данных будет открыто окно tooprompt hello учетных данных.</span><span class="sxs-lookup"><span data-stu-id="c2575-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="c2575-162">Для систем, предназначенных для имеющих большое количество заданий, выполняемых параллельно с большим числом баз данных, рекомендуется toospecify параметров таких как: - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="c2575-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="c2575-163">Обновление существующей установки компонентов заданий обработки эластичных баз данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2575-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="c2575-164">**Задания обработки эластичных баз данных** в существующей установке можно обновить для масштабирования и высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="c2575-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="c2575-165">Этот процесс позволяет для будущих обновлений кода службы без необходимости toodrop и повторного создания базы данных системы управления hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="c2575-166">Этот процесс также может использоваться внутри hello одной версии toomodify hello службы виртуальной Машины размера или hello server число рабочих.</span><span class="sxs-lookup"><span data-stu-id="c2575-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="c2575-167">размер виртуальной Машины hello tooupdate установки, выполнения hello, выполнив сценарий с параметрами обновленные значения toohello по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="c2575-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="c2575-168">Параметр</span><span class="sxs-lookup"><span data-stu-id="c2575-168">Parameter</span></span></th>
  <th><span data-ttu-id="c2575-169">Описание</span><span class="sxs-lookup"><span data-stu-id="c2575-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="c2575-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="c2575-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="c2575-171">Указывает имя группы ресурсов Azure hello, используемое при первоначальной установке компонентов задания hello эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="c2575-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="c2575-172">Этот параметр по умолчанию слишком «__ElasticDatabaseJob».</span><span class="sxs-lookup"><span data-stu-id="c2575-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="c2575-173">Поскольку это не рекомендуется toochange это значение не должен содержать toospecify этот параметр.</span><span class="sxs-lookup"><span data-stu-id="c2575-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="c2575-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="c2575-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="c2575-175">Предоставляет номер hello tooinstall службы рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="c2575-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="c2575-176">Этот параметр по умолчанию too1.</span><span class="sxs-lookup"><span data-stu-id="c2575-176">This parameter defaults too1.</span></span>  <span data-ttu-id="c2575-177">Увеличение количества рабочих процессов может быть используется tooscale out hello службы и tooprovide высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="c2575-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="c2575-178">Рекомендуется toouse «2» для развертываний, которые требуется высокий уровень доступности службы hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="c2575-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="c2575-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="c2575-180">Предоставляет hello размер виртуальной Машины для использования в пределах hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="c2575-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="c2575-181">Этот параметр по умолчанию tooA0.</span><span class="sxs-lookup"><span data-stu-id="c2575-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="c2575-182">Допустимы значения параметров из A0/A1 и A2/A3 заставляющие hello рабочей роли toouse размер очень мелкий/малого и среднего и широкого соответственно.</span><span class="sxs-lookup"><span data-stu-id="c2575-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="c2575-183">Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="c2575-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="c2575-184">Установить компоненты задания hello эластичной базы данных, с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="c2575-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="c2575-185">После получения [создан пул эластичных](sql-database-elastic-pool-manage-portal.md), можно установить **заданий эластичных баз данных** компоненты tooenable выполнения административных задач для каждой базы данных в эластичный пул hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="c2575-186">В отличие от, когда с помощью hello **заданий эластичных баз данных** API-интерфейсов PowerShell интерфейс портала hello является в настоящее время ограничены tooonly выполняет существующий пул.</span><span class="sxs-lookup"><span data-stu-id="c2575-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="c2575-187">**Предполагаемое время toocomplete:** 10 минут.</span><span class="sxs-lookup"><span data-stu-id="c2575-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="c2575-188">Из представления панели мониторинга hello hello пула эластичных БД через hello [портала Azure](https://portal.azure.com/#) , нажмите кнопку **создать задание**.</span><span class="sxs-lookup"><span data-stu-id="c2575-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="c2575-189">При создании задания для hello впервые, необходимо установить **заданий эластичных баз данных** , щелкнув **условия предварительной версии**.</span><span class="sxs-lookup"><span data-stu-id="c2575-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="c2575-190">Примите условия hello, щелкнув hello флажок.</span><span class="sxs-lookup"><span data-stu-id="c2575-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="c2575-191">В представлении hello» установите службы» щелкните **учетные данные задания**.</span><span class="sxs-lookup"><span data-stu-id="c2575-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Установка служб hello][1]
5. <span data-ttu-id="c2575-193">Введите имя пользователя и пароль администратора базы данных. В процессе установки hello создается новый сервер базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c2575-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="c2575-194">В этом новом сервере новую базу данных, называемой базой данных управления hello и используется toocontain hello метаданные для заданий эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="c2575-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="c2575-195">Ведение журнала в базе данных системы управления toohello с целью hello используются Hello имя пользователя и пароль, созданные здесь.</span><span class="sxs-lookup"><span data-stu-id="c2575-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="c2575-196">Отдельные учетные данные используются для выполнения скриптов для баз данных hello в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![Создание имени пользователя и пароля][2]
6. <span data-ttu-id="c2575-198">Нажмите кнопку "ОК" hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-198">Click hello OK button.</span></span> <span data-ttu-id="c2575-199">компоненты Hello создаются автоматически через несколько минут, в новом [группы ресурсов](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c2575-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="c2575-200">закрепленные Hello новую группу ресурсов toohello запуск доски, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c2575-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="c2575-201">После создания, эластичной базы данных заданий (облачной службы, базы данных SQL, Service Bus и хранилище) создаются в группе hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![Группа ресурсов на начальной доске][3]
7. <span data-ttu-id="c2575-203">Если попытка toocreate или управления заданием, пока выполняется установка заданий эластичных баз данных, при предоставлении **учетные данные** вы увидите следующие сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![Развертывание еще не завершено][4]

<span data-ttu-id="c2575-205">При необходимости отмены установки, удаления группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="c2575-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="c2575-206">В разделе [как toouninstall hello эластичной базы данных задание компонентов](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="c2575-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2575-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2575-207">Next steps</span></span>
<span data-ttu-id="c2575-208">Убедитесь учетные данные с hello соответствующие права для выполнения скрипта создается для каждой базы данных в группе hello, Дополнительные сведения см. в разделе [защите базы данных SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="c2575-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="c2575-209">В разделе [Создание и управление заданиями эластичной базы данных](sql-database-elastic-jobs-create-and-manage.md) tooget работы.</span><span class="sxs-lookup"><span data-stu-id="c2575-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
