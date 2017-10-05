---
title: "Установка заданий обработки эластичных баз данных | Документация Майкрософт"
description: "Пошаговые инструкции по установке компонента заданий обработки эластичных баз данных."
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
ms.openlocfilehash: e7a2d6dbcefbb31d76257eaf96ccc235d7a29416
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="1af28-103">Обзор установки заданий обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="1af28-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="1af28-104">[**Задания эластичных баз данных**](sql-database-elastic-jobs-overview.md) можно установить с помощью PowerShell или классического портала Azure. Чтобы создавать задания и управлять ими только с помощью API PowerShell, необходимо установить пакет PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1af28-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span></span> <span data-ttu-id="1af28-105">Кроме того, в настоящий момент API-интерфейсы PowerShell предоставляют намного больше возможностей, чем портал.</span><span class="sxs-lookup"><span data-stu-id="1af28-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span></span>

<span data-ttu-id="1af28-106">Если вы уже установили **задания эластичных баз данных** с помощью портала из существующего **эластичного пула**, последняя предварительная версия Powershell будет включать в себя сценарии для обновления существующей установки.</span><span class="sxs-lookup"><span data-stu-id="1af28-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span></span> <span data-ttu-id="1af28-107">Настоятельно рекомендуется обновить установку до последней версии компонентов **заданий обработки эластичных баз данных** , чтобы воспользоваться новыми возможностями, доступными через API-интерфейсы PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1af28-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1af28-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1af28-108">Prerequisites</span></span>
* <span data-ttu-id="1af28-109">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="1af28-109">An Azure subscription.</span></span> <span data-ttu-id="1af28-110">Бесплатная пробная версия доступна [здесь](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1af28-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1af28-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1af28-111">Azure PowerShell.</span></span> <span data-ttu-id="1af28-112">Установите последнюю версию с помощью [установщика веб-платформы](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="1af28-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="1af28-113">Дополнительные сведения можно узнать в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1af28-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="1af28-114">[Служебная программа командной строки NuGet](https://nuget.org/nuget.exe) используется для установки пакета заданий эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="1af28-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span></span> <span data-ttu-id="1af28-115">Дополнительные сведения см. по адресу http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="1af28-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a><span data-ttu-id="1af28-116">Загрузка и импорт пакета PowerShell службы заданий обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="1af28-116">Download and import the Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="1af28-117">Откройте командную строку Microsoft Azure PowerShell и перейдите в каталог, куда была загружена служебная программа командной строки NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="1af28-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="1af28-118">Скачайте и импортируйте пакет **заданий обработки эластичных баз данных** в текущий каталог с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="1af28-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="1af28-119">Файлы **заданий эластичных баз данных** помещаются в локальный каталог в папке **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x**, где *x.x.xxxx.x* — это номер версии.</span><span class="sxs-lookup"><span data-stu-id="1af28-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span></span> <span data-ttu-id="1af28-120">Командлеты PowerShell (включая необходимые клиентские DLL-файлы) находятся в подкаталоге **tools\ElasticDatabaseJobs**, а сценарии PowerShell для установки, обновления и удаления также находятся в подкаталоге **tools**.</span><span class="sxs-lookup"><span data-stu-id="1af28-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span></span>
3. <span data-ttu-id="1af28-121">Перейдите в подкаталог tools в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x с помощью команды cd tools, например:</span><span class="sxs-lookup"><span data-stu-id="1af28-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="1af28-122">Запустите сценарий .\InstallElasticDatabaseJobsCmdlets.ps1, чтобы скопировать каталог ElasticDatabaseJobs в папку $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="1af28-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="1af28-123">При этом также будет автоматически импортирован используемый модуль, например:</span><span class="sxs-lookup"><span data-stu-id="1af28-123">This will also automatically import the module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="1af28-124">Установка компонентов заданий обработки эластичных баз данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1af28-124">Install the Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="1af28-125">Откройте командную строку Microsoft Azure PowerShell и перейдите в подкаталог \tools в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x: введите команду cd \tools</span><span class="sxs-lookup"><span data-stu-id="1af28-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="1af28-126">Запустите сценарий .\InstallElasticDatabaseJobs.ps1 PowerShell и укажите значения необходимых переменных.</span><span class="sxs-lookup"><span data-stu-id="1af28-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="1af28-127">Этот сценарий создаст компоненты, описанные в статье [Компоненты службы заданий обработки эластичных баз данных и цены](sql-database-elastic-jobs-overview.md#components-and-pricing) , и настроит облачную службу Azure для надлежащего использования зависящих компонентов.</span><span class="sxs-lookup"><span data-stu-id="1af28-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="1af28-128">При выполнении этой команды появится окно с запросом **имени пользователя** и **пароля**.</span><span class="sxs-lookup"><span data-stu-id="1af28-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="1af28-129">Это не учетные данные Azure; введите имя пользователя и пароль, которые станут учетными данными администратора нового сервера.</span><span class="sxs-lookup"><span data-stu-id="1af28-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span></span>

<span data-ttu-id="1af28-130">Параметры, указанные при вызове этого примера, можно заменить на необходимые.</span><span class="sxs-lookup"><span data-stu-id="1af28-130">The parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="1af28-131">Ниже предоставлены дополнительные сведения о поведении каждого параметра:</span><span class="sxs-lookup"><span data-stu-id="1af28-131">The following provides more information on the behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="1af28-132">Параметр</span><span class="sxs-lookup"><span data-stu-id="1af28-132">Parameter</span></span></th>
    <th><span data-ttu-id="1af28-133">Описание</span><span class="sxs-lookup"><span data-stu-id="1af28-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="1af28-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1af28-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="1af28-135">Указывает имя группы ресурсов Azure, созданной для хранения новых компонентов Azure.</span><span class="sxs-lookup"><span data-stu-id="1af28-135">Provides the Azure resource group name created to contain the newly created Azure components.</span></span> <span data-ttu-id="1af28-136">Значение по умолчанию: "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="1af28-136">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="1af28-137">Менять это значение не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="1af28-137">It is not recommended to change this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="1af28-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="1af28-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="1af28-139">Указывает расположение Azure, используемое для новых компонентов Azure.</span><span class="sxs-lookup"><span data-stu-id="1af28-139">Provides the Azure location to be used for the newly created Azure components.</span></span> <span data-ttu-id="1af28-140">По умолчанию в этом параметре указан центр США.</span><span class="sxs-lookup"><span data-stu-id="1af28-140">This parameter defaults to the Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="1af28-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="1af28-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="1af28-142">Указывает число устанавливаемых рабочих процессов службы.</span><span class="sxs-lookup"><span data-stu-id="1af28-142">Provides the number of service workers to install.</span></span> <span data-ttu-id="1af28-143">Значение по умолчанию: 1.</span><span class="sxs-lookup"><span data-stu-id="1af28-143">This parameter defaults to 1.</span></span> <span data-ttu-id="1af28-144">Повышая число рабочих процессов, можно расширять службу и обеспечивать высокую доступность.</span><span class="sxs-lookup"><span data-stu-id="1af28-144">A higher number of workers can be used to scale out the service and to provide high availability.</span></span> <span data-ttu-id="1af28-145">Значение "2" рекомендуется использовать для развертываний, требующих высокой доступности службы.</span><span class="sxs-lookup"><span data-stu-id="1af28-145">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="1af28-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="1af28-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="1af28-147">Указывает размер виртуальной машины для использования в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="1af28-147">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="1af28-148">Значение по умолчанию: A0.</span><span class="sxs-lookup"><span data-stu-id="1af28-148">This parameter defaults to A0.</span></span> <span data-ttu-id="1af28-149">Допускаются значения параметра A0/A1/A2/A3, которые указывают рабочей роли использовать размер ExtraSmall/Small/Medium/Large, соответственно.</span><span class="sxs-lookup"><span data-stu-id="1af28-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="1af28-150">Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="1af28-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="1af28-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="1af28-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="1af28-152">Указывает цель уровня обслуживания для стандартного выпуска.</span><span class="sxs-lookup"><span data-stu-id="1af28-152">Provides the service level objective for a Standard edition.</span></span> <span data-ttu-id="1af28-153">Значение по умолчанию: S0.</span><span class="sxs-lookup"><span data-stu-id="1af28-153">This parameter defaults to S0.</span></span> <span data-ttu-id="1af28-154">Допускаются значения S0/S1/S2/S3, которые указывают Базе данных SQL Azure использовать соответствующую цель уровня обслуживания (SLO).</span><span class="sxs-lookup"><span data-stu-id="1af28-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span></span> <span data-ttu-id="1af28-155">Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="1af28-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="1af28-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="1af28-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="1af28-157">Указывает имя пользователя администратора для нового сервера Базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1af28-157">Provides the admin user name for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="1af28-158">Если этот параметр не указан, откроется окно PowerShell с запросом учетных данных.</span><span class="sxs-lookup"><span data-stu-id="1af28-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="1af28-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="1af28-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="1af28-160">Указывает пароль администратора для нового сервера Базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1af28-160">Provides the admin password for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="1af28-161">Если этот параметр не указан, откроется окно PowerShell с запросом учетных данных.</span><span class="sxs-lookup"><span data-stu-id="1af28-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="1af28-162">Для систем, рассчитанных на параллельное выполнение больших количеств заданий для большого числа баз данных, рекомендуется указывать такие параметры: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="1af28-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="1af28-163">Обновление существующей установки компонентов заданий обработки эластичных баз данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1af28-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="1af28-164">**Задания обработки эластичных баз данных** в существующей установке можно обновить для масштабирования и высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="1af28-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="1af28-165">Этот процесс позволяет обновлять код службы в будущем без необходимости удаления и повторного создания управляющей базы данных.</span><span class="sxs-lookup"><span data-stu-id="1af28-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span></span> <span data-ttu-id="1af28-166">Этот процесс также можно использовать в той же версии, чтобы изменить размер виртуальных машин или число рабочих процессов сервера.</span><span class="sxs-lookup"><span data-stu-id="1af28-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span></span>

<span data-ttu-id="1af28-167">Чтобы изменить размер виртуальных машин в установке, запустите следующий сценарий, заменив значения параметров на нужные вам.</span><span class="sxs-lookup"><span data-stu-id="1af28-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="1af28-168">Параметр</span><span class="sxs-lookup"><span data-stu-id="1af28-168">Parameter</span></span></th>
  <th><span data-ttu-id="1af28-169">Описание</span><span class="sxs-lookup"><span data-stu-id="1af28-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="1af28-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1af28-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="1af28-171">Указывает имя группы ресурсов Azure, используемой при изначальной установке компонентов заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="1af28-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span></span> <span data-ttu-id="1af28-172">Значение по умолчанию: "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="1af28-172">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="1af28-173">Так как менять это значение не рекомендуется, скорее всего, указывать этот параметр не потребуется.</span><span class="sxs-lookup"><span data-stu-id="1af28-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="1af28-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="1af28-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="1af28-175">Указывает число устанавливаемых рабочих процессов службы.</span><span class="sxs-lookup"><span data-stu-id="1af28-175">Provides the number of service workers to install.</span></span>  <span data-ttu-id="1af28-176">Значение по умолчанию: 1.</span><span class="sxs-lookup"><span data-stu-id="1af28-176">This parameter defaults to 1.</span></span>  <span data-ttu-id="1af28-177">Повышая число рабочих процессов, можно расширять службу и обеспечивать высокую доступность.</span><span class="sxs-lookup"><span data-stu-id="1af28-177">A higher number of workers can be used to scale out the service and to provide high availability.</span></span>  <span data-ttu-id="1af28-178">Значение "2" рекомендуется использовать для развертываний, требующих высокой доступности службы.</span><span class="sxs-lookup"><span data-stu-id="1af28-178">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="1af28-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="1af28-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="1af28-180">Указывает размер виртуальной машины для использования в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="1af28-180">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="1af28-181">Значение по умолчанию: A0.</span><span class="sxs-lookup"><span data-stu-id="1af28-181">This parameter defaults to A0.</span></span> <span data-ttu-id="1af28-182">Допускаются значения параметра A0/A1/A2/A3, которые указывают рабочей роли использовать размер ExtraSmall/Small/Medium/Large, соответственно.</span><span class="sxs-lookup"><span data-stu-id="1af28-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="1af28-183">Чтобы узнать больше о размерах рабочей роли, ознакомьтесь с [компонентами службы заданий эластичных баз данных и ценами](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="1af28-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a><span data-ttu-id="1af28-184">Установка компонентов заданий обработки эластичных баз данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="1af28-184">Install the Elastic Database jobs components using the Portal</span></span>
<span data-ttu-id="1af28-185">[Создав эластичный пул](sql-database-elastic-pool-manage-portal.md), вы можете установить компоненты **заданий обработки эластичных баз данных**, которые позволят выполнять административные задачи для каждой базы данных в эластичном пуле.</span><span class="sxs-lookup"><span data-stu-id="1af28-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span></span> <span data-ttu-id="1af28-186">В отличие от API-интерфейсов PowerShell **заданий обработки эластичных баз данных** , интерфейс портала в данный момент позволяет выполнять задания только для существующего пула.</span><span class="sxs-lookup"><span data-stu-id="1af28-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span></span>

<span data-ttu-id="1af28-187">**Предполагаемое время выполнения:** 10 минут.</span><span class="sxs-lookup"><span data-stu-id="1af28-187">**Estimated time to complete:** 10 minutes.</span></span>

1. <span data-ttu-id="1af28-188">В представлении панели мониторинга эластичного пула на [портале Azure](https://portal.azure.com/#) щелкните **Создать задание**.</span><span class="sxs-lookup"><span data-stu-id="1af28-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="1af28-189">Если вы создаете задание впервые, вам необходимо установить **задания эластичных баз данных**, выбрав **УСЛОВИЯ ПРЕДВАРИТЕЛЬНОЙ ВЕРСИИ**.</span><span class="sxs-lookup"><span data-stu-id="1af28-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="1af28-190">Примите условия, установив соответствующий флажок.</span><span class="sxs-lookup"><span data-stu-id="1af28-190">Accept the terms by clicking the checkbox.</span></span>
4. <span data-ttu-id="1af28-191">В представлении «Установка служб» щелкните **УЧЕТНЫЕ ДАННЫЕ ДЛЯ ЗАДАНИЯ**.</span><span class="sxs-lookup"><span data-stu-id="1af28-191">In the "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Установка служб][1]
5. <span data-ttu-id="1af28-193">Введите имя пользователя и пароль администратора базы данных.</span><span class="sxs-lookup"><span data-stu-id="1af28-193">Type a user name and password for a database admin.</span></span> <span data-ttu-id="1af28-194">В процессе установки создается сервер базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1af28-194">As part of the installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="1af28-195">На этом сервере создается новая база данных, известная также как управляющая база данных, в которой хранятся метаданные для заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="1af28-195">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span></span> <span data-ttu-id="1af28-196">Созданные здесь имя пользователя и пароль используются для входа в управляющую базу данных.</span><span class="sxs-lookup"><span data-stu-id="1af28-196">The user name and password created here are used for the purpose of logging in to the control database.</span></span> <span data-ttu-id="1af28-197">Для выполнения сценариев на базах данных в пуле используются отдельные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="1af28-197">A separate credential is used for script execution against the databases within the pool.</span></span>
   
    ![Создание имени пользователя и пароля][2]
6. <span data-ttu-id="1af28-199">Нажмите кнопку «ОК».</span><span class="sxs-lookup"><span data-stu-id="1af28-199">Click the OK button.</span></span> <span data-ttu-id="1af28-200">Компоненты будут созданы через несколько минут в новой [группе ресурсов](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1af28-200">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1af28-201">Новая группа ресурсов закрепляется на начальной доске, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="1af28-201">The new resource group is pinned to the start board, as shown below.</span></span> <span data-ttu-id="1af28-202">После создания компонентов в группе будут созданы задания обработки эластичных баз данных (облачная служба, база данных SQL, служебная шина и хранилище).</span><span class="sxs-lookup"><span data-stu-id="1af28-202">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span></span>
   
    ![Группа ресурсов на начальной доске][3]
7. <span data-ttu-id="1af28-204">Если во время установки службы заданий эластичной базы данных вы попытаетесь создать или изменить какое-то задание, после ввода **учетных данных** появится следующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="1af28-204">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span></span>
   
    ![Развертывание еще не завершено][4]

<span data-ttu-id="1af28-206">Если требуется удаление, удалите группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1af28-206">If uninstallation is required, delete the resource group.</span></span> <span data-ttu-id="1af28-207">Ознакомьтесь со статьей [Удаление компонентов заданий обработки эластичных баз данных](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="1af28-207">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1af28-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1af28-208">Next steps</span></span>
<span data-ttu-id="1af28-209">Убедитесь, что в каждой базе данных группы созданы учетные данные с правами на выполнение сценариев. Дополнительные сведения см. в статье [Защита базы данных SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="1af28-209">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="1af28-210">Чтобы приступить к работе, прочитайте статью [Создание заданий обработки эластичных баз данных и управление ими](sql-database-elastic-jobs-create-and-manage.md).</span><span class="sxs-lookup"><span data-stu-id="1af28-210">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
