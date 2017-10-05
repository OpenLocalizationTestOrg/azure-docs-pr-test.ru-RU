---
title: "С помощью базы данных SQL Azure стек | Документы Microsoft"
description: "Дополнительные сведения о развертывании баз данных SQL как служба Azure стека и быстрых действий, чтобы развернуть адаптер поставщика ресурсов SQL Server"
services: azure-stack
documentationCenter: 
author: JeffGoldner
manager: bradleyb
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: JeffGo
ms.openlocfilehash: 018d556d52aa1a1f436460d9811c43f9b45bd440
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="3994d-103">Использование баз данных SQL Microsoft Azure стеке</span><span class="sxs-lookup"><span data-stu-id="3994d-103">Use SQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="3994d-104">Используется адаптером поставщика ресурсов SQL Server для предоставления баз данных SQL, как служба Azure стека.</span><span class="sxs-lookup"><span data-stu-id="3994d-104">Use the SQL Server resource provider adapter to expose SQL databases as a service of Azure Stack.</span></span> <span data-ttu-id="3994d-105">После установки поставщика ресурсов и подключите его к один или несколько экземпляров SQL Server, вас и ваших пользователей можно создавать базы данных для рабочих нагрузок, основанных на SQL без необходимости подготовки (виртуальной машины, облако в собственном коде приложений и веб-сайтов, которые основаны на SQL Виртуальная машина), на котором размещается SQL Server каждый раз.</span><span class="sxs-lookup"><span data-stu-id="3994d-105">After you install the resource provider and connect it to one or more SQL Server instances, you and your users can create databases for cloud-native apps, websites that are based on SQL, and workloads that are based on SQL without having to provision a virtual machine (VM) that hosts SQL Server each time.</span></span>

<span data-ttu-id="3994d-106">Поставщик ресурсов не поддерживает все возможности управления базами данных из [базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="3994d-106">The resource provider does not support all the database management capabilities of [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).</span></span> <span data-ttu-id="3994d-107">Например пулы эластичных баз данных и возможность масштабирования производительности базы данных не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="3994d-107">For example, elastic database pools and the ability to scale database performance aren't supported.</span></span> <span data-ttu-id="3994d-108">API-Интерфейс несовместим с баз данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3994d-108">The API is not compatible with SQL DB.</span></span>


## <a name="sql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="3994d-109">Архитектура адаптера поставщика ресурсов SQL Server</span><span class="sxs-lookup"><span data-stu-id="3994d-109">SQL Server Resource Provider Adapter architecture</span></span>
<span data-ttu-id="3994d-110">Поставщик ресурсов не основан на, а также его есть все базы данных возможности управления базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3994d-110">The resource provider is not based on, nor does it offer all the database management capabilities of Azure SQL Database.</span></span> <span data-ttu-id="3994d-111">Например недоступны пулы эластичных баз данных и возможности подключения автоматически производительность базы данных вверх и вниз.</span><span class="sxs-lookup"><span data-stu-id="3994d-111">For example, elastic database pools and the ability to dial database performance up and down automatically aren't available.</span></span> <span data-ttu-id="3994d-112">Тем не менее ресурс поставщик поддерживает аналогичные создания, чтения, обновления и удаления (CRUD).</span><span class="sxs-lookup"><span data-stu-id="3994d-112">However, the resource provider does support similar create, read, update, and delete (CRUD) operations.</span></span>

<span data-ttu-id="3994d-113">Поставщик ресурсов состоит из трех компонентов:</span><span class="sxs-lookup"><span data-stu-id="3994d-113">The resource provider is made up of three components:</span></span>

- <span data-ttu-id="3994d-114">**Адаптер поставщика ресурсов SQL виртуальной Машины**, который является виртуальной машине, где запущены службы поставщика.</span><span class="sxs-lookup"><span data-stu-id="3994d-114">**The SQL resource provider adapter VM**, which is a Windows virtual machine running the provider services.</span></span>
- <span data-ttu-id="3994d-115">**Поставщик ресурсов**, который обрабатывает запросы на подготовку, и предоставляет доступ к базе данных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3994d-115">**The resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="3994d-116">**Серверы, на которых размещаются SQL Server**, предоставляющие емкости для баз данных, называемые серверами размещения.</span><span class="sxs-lookup"><span data-stu-id="3994d-116">**Servers that host SQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="3994d-117">Этот выпуск больше не создает экземпляр SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3994d-117">This release no longer creates a SQL instance.</span></span> <span data-ttu-id="3994d-118">Необходимо создать один (или несколько) и/или предоставления доступа к внешней экземпляры SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3994d-118">You must create one (or more) and/or provide access to external SQL instances.</span></span> <span data-ttu-id="3994d-119">Существует несколько параметров, доступных шаблонов в том числе [коллекции быстрый запуск Azure стека](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) и элементы Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3994d-119">There are a number of options available to you including templates in the [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) and Marketplace items.</span></span> 

>[!NOTE]
<span data-ttu-id="3994d-120">Если вы загрузили какие-либо элементы SQL Marketplace, убедитесь, что также загрузить расширения SQL IaaS или они не будут развернуты.</span><span class="sxs-lookup"><span data-stu-id="3994d-120">If you have downloaded any SQL Marketplace items, make sure you also download the SQL IaaS Extension or these will not deploy.</span></span>


## <a name="deploy-the-resource-provider"></a><span data-ttu-id="3994d-121">Разверните поставщик ресурсов</span><span class="sxs-lookup"><span data-stu-id="3994d-121">Deploy the resource provider</span></span>

1. <span data-ttu-id="3994d-122">Если вы еще не сделали регистрации вашего пакета средств разработки и загрузить образ Windows Server 2016 EVAL загружаемых посредством управления Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3994d-122">If you have not already done so, register your development kit and download the Windows Server 2016 EVAL image downloadable through Marketplace Management.</span></span> <span data-ttu-id="3994d-123">Можно также использовать сценарий для создания [образа Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span><span class="sxs-lookup"><span data-stu-id="3994d-123">You can also use a script to create a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span> <span data-ttu-id="3994d-124">Среда выполнения .NET 3.5 больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="3994d-124">The .NET 3.5 runtime is no longer required.</span></span>

2. <span data-ttu-id="3994d-125">[Загрузите файл двоичных файлов поставщика ресурсов SQL](https://aka.ms/azurestacksqlrp) и извлеките его на узле разработки пакета.</span><span class="sxs-lookup"><span data-stu-id="3994d-125">[Download the SQL resource provider binaries file](https://aka.ms/azurestacksqlrp) and extract it on the development kit host.</span></span>

3. <span data-ttu-id="3994d-126">Войдите в узел комплект средств для разработки и извлеките файл установщика SQL RP во временный каталог.</span><span class="sxs-lookup"><span data-stu-id="3994d-126">Sign in to the development kit host and extract the SQL RP installer file to a temporary directory.</span></span>

4. <span data-ttu-id="3994d-127">Стек Azure корневой сертификат извлекается и самозаверяющий сертификат создается как часть этого процесса.</span><span class="sxs-lookup"><span data-stu-id="3994d-127">The Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="3994d-128">__Необязательно:__ Если необходимо предоставить собственную, Подготовка сертификатов и скопировать в локальный каталог, если вы хотите настроить сертификаты (передачи в сценарий установки).</span><span class="sxs-lookup"><span data-stu-id="3994d-128">__Optional:__ If you need to provide your own, prepare the certificates and copy to a local directory if you wish to customize the certificates (passed to the installation script).</span></span> <span data-ttu-id="3994d-129">Требуются следующие сертификаты:</span><span class="sxs-lookup"><span data-stu-id="3994d-129">You need the following certificates:</span></span>

    <span data-ttu-id="3994d-130">а.</span><span class="sxs-lookup"><span data-stu-id="3994d-130">a.</span></span> <span data-ttu-id="3994d-131">Сертификатом с подстановочными символами для *.dbadapter. \<область\>.\< полного доменного имени\>.</span><span class="sxs-lookup"><span data-stu-id="3994d-131">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="3994d-132">Этот сертификат должен быть доверенным, такие как будет выдан центром сертификации (то есть цепочку доверия должен существовать без промежуточных сертификатов.) (Один сайт сертификат можно использовать с явной имя виртуальной Машины, указываемые во время установки.)</span><span class="sxs-lookup"><span data-stu-id="3994d-132">This certificate must be trusted, such as would be issued by a certificate authority (that is, the chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with the explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="3994d-133">b.</span><span class="sxs-lookup"><span data-stu-id="3994d-133">b.</span></span> <span data-ttu-id="3994d-134">Корневой сертификат, используемый диспетчером ресурсов Azure для экземпляра Azure стека.</span><span class="sxs-lookup"><span data-stu-id="3994d-134">The root certificate used by the Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="3994d-135">Если он не найден, будет получен корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="3994d-135">If it is not found, the root certificate will be retrieved.</span></span>


5. <span data-ttu-id="3994d-136">Откройте **новый** с повышенными привилегиями консоль PowerShell и изменения в каталоге, где были извлечены файлы.</span><span class="sxs-lookup"><span data-stu-id="3994d-136">Open a **new** elevated PowerShell console and change to the directory where you extracted the files.</span></span> <span data-ttu-id="3994d-137">Используйте новое окно, чтобы избежать проблемы, которые могут быть вызваны неверные модули PowerShell, которые уже загружены в системе.</span><span class="sxs-lookup"><span data-stu-id="3994d-137">Use a new window to avoid problems that may arise from incorrect PowerShell modules already loaded on the system.</span></span>

6. <span data-ttu-id="3994d-138">После установки любой версии AzureRm или AzureStack PowerShell модулей, кроме 1.2.9 или 1.2.10, вам будет предложено удалить их или установку не удастся.</span><span class="sxs-lookup"><span data-stu-id="3994d-138">If you have installed any versions of the AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted to remove them or the install will not proceed.</span></span> <span data-ttu-id="3994d-139">Сюда входят версии 1.3 или выше.</span><span class="sxs-lookup"><span data-stu-id="3994d-139">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="3994d-140">Запустите сценарий DeploySqlProvider.ps1 с перечисленными ниже параметрами.</span><span class="sxs-lookup"><span data-stu-id="3994d-140">Run the DeploySqlProvider.ps1 script with the parameters listed below.</span></span>

<span data-ttu-id="3994d-141">Скрипт выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3994d-141">The script performs these steps:</span></span>

* <span data-ttu-id="3994d-142">При необходимости, загрузите совместимую версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3994d-142">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="3994d-143">Учетная запись хранения в комплекте Azure для передачи сертификаты и другие артефакты.</span><span class="sxs-lookup"><span data-stu-id="3994d-143">Upload the certificates and other artifacts to a storage account on your Azure Stack.</span></span>
* <span data-ttu-id="3994d-144">Опубликуйте пакеты коллекции, чтобы выполнить развертывание базы данных SQL из коллекции.</span><span class="sxs-lookup"><span data-stu-id="3994d-144">Publish gallery packages so that you can deploy SQL databases through the gallery.</span></span>
* <span data-ttu-id="3994d-145">Развертывание виртуальной Машины с помощью образа Windows Server 2016, созданной на шаге 1 и установка поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3994d-145">Deploy a VM using the Windows Server 2016 image created in step 1 and install the resource provider.</span></span>
* <span data-ttu-id="3994d-146">Зарегистрируйте локальный DNS-запись, сопоставляемый с поставщиком ресурсов виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3994d-146">Register a local DNS record that maps to your resource provider VM.</span></span>
* <span data-ttu-id="3994d-147">Регистрация поставщика ресурсов с помощью локального диспетчера ресурсов Azure (клиента и администратора).</span><span class="sxs-lookup"><span data-stu-id="3994d-147">Register your resource provider with the local Azure Resource Manager (Tenant and Admin).</span></span>

> [!NOTE]
> <span data-ttu-id="3994d-148">Если установка занимает более 90 минут, может произойти сбой вы видите сообщение об ошибке на экране и в файле журнала, а развертывание повторяется с шага сбоя.</span><span class="sxs-lookup"><span data-stu-id="3994d-148">If the installation takes more than 90 minutes, it may fail and you see a failure message on the screen and in the log file, but the deployment is retried from the failing step.</span></span> <span data-ttu-id="3994d-149">Системы, не соответствует рекомендуемым характеристикам памяти и основных компонентов не может иметь возможность развернуть SQL RP.</span><span class="sxs-lookup"><span data-stu-id="3994d-149">Systems that do not meet the recommended memory and core specifications may not be able to deploy the SQL RP.</span></span>
>

<span data-ttu-id="3994d-150">Ниже приведен пример, можно запустить из PowerShell запрашивать (но при необходимости изменить конечные точки сведения и портала учетной записи):</span><span class="sxs-lookup"><span data-stu-id="3994d-150">Here's an example you can run from the PowerShell prompt (but change the account information and portal endpoints as needed):</span></span>

```
# Install the AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports the API Version Profile required by Azure Stack into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download the Azure Stack Tools from GitHub and set the environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use the following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace the previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory to the folder where you extracted the installation files 
# and adjust the endpoints
<extracted file directory>\DeploySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "SqlRPRG" -VmName "SqlVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass
 ```

### <a name="deploysqlproviderps1-parameters"></a><span data-ttu-id="3994d-151">Параметры DeploySqlProvider.ps1</span><span class="sxs-lookup"><span data-stu-id="3994d-151">DeploySqlProvider.ps1 parameters</span></span>
<span data-ttu-id="3994d-152">Эти параметры можно указать в командной строке.</span><span class="sxs-lookup"><span data-stu-id="3994d-152">You can specify these parameters in the command line.</span></span> <span data-ttu-id="3994d-153">Если этого не сделать, или происходит сбой проверки параметров, вам будет предложено предоставить необходимые методы.</span><span class="sxs-lookup"><span data-stu-id="3994d-153">If you do not, or any parameter validation fails, you are prompted to provide the required ones.</span></span>

| <span data-ttu-id="3994d-154">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3994d-154">Parameter Name</span></span> | <span data-ttu-id="3994d-155">Описание</span><span class="sxs-lookup"><span data-stu-id="3994d-155">Description</span></span> | <span data-ttu-id="3994d-156">Комментарий или значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3994d-156">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3994d-157">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="3994d-157">**DirectoryTenantID**</span></span> | <span data-ttu-id="3994d-158">Azure и каталог служб федерации Active Directory с Идентификатором (guid).</span><span class="sxs-lookup"><span data-stu-id="3994d-158">The Azure or ADFS Directory ID (guid).</span></span> | <span data-ttu-id="3994d-159">_Обязательно_</span><span class="sxs-lookup"><span data-stu-id="3994d-159">_required_</span></span> |
| <span data-ttu-id="3994d-160">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="3994d-160">**AzCredential**</span></span> | <span data-ttu-id="3994d-161">Учетные данные для учетной записи администратора служб Azure стека.</span><span class="sxs-lookup"><span data-stu-id="3994d-161">Provide the credentials for the Azure Stack Service Admin account.</span></span> <span data-ttu-id="3994d-162">Необходимо использовать те же учетные данные используются для развертывания Azure стека).</span><span class="sxs-lookup"><span data-stu-id="3994d-162">You must use the same credentials as you used for deploying Azure Stack).</span></span> | <span data-ttu-id="3994d-163">_Обязательно_</span><span class="sxs-lookup"><span data-stu-id="3994d-163">_required_</span></span> |
| <span data-ttu-id="3994d-164">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="3994d-164">**VMLocalCredential**</span></span> | <span data-ttu-id="3994d-165">Укажите учетные данные учетной записи локального администратора поставщика ресурсов SQL виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3994d-165">Define the credentials for the local administrator account of the SQL resource provider VM.</span></span> <span data-ttu-id="3994d-166">Этот пароль также используется для SQL **sa** учетной записи.</span><span class="sxs-lookup"><span data-stu-id="3994d-166">This password is also used for the SQL **sa** account.</span></span> | <span data-ttu-id="3994d-167">_Обязательно_</span><span class="sxs-lookup"><span data-stu-id="3994d-167">_required_</span></span> |
| <span data-ttu-id="3994d-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="3994d-168">**ResourceGroupName**</span></span> | <span data-ttu-id="3994d-169">Определите имя для группы ресурсов, в котором будут храниться элементы, созданный этим сценарием.</span><span class="sxs-lookup"><span data-stu-id="3994d-169">Define a name for a Resource Group in which items created by this script will be stored.</span></span> <span data-ttu-id="3994d-170">Например *SqlRPRG*.</span><span class="sxs-lookup"><span data-stu-id="3994d-170">For example, *SqlRPRG*.</span></span> |  <span data-ttu-id="3994d-171">_Обязательно_</span><span class="sxs-lookup"><span data-stu-id="3994d-171">_required_</span></span> |
| <span data-ttu-id="3994d-172">**VmName**</span><span class="sxs-lookup"><span data-stu-id="3994d-172">**VmName**</span></span> | <span data-ttu-id="3994d-173">Укажите имя виртуальной машины, на котором требуется установить поставщик ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3994d-173">Define the name of the virtual machine on which to install the resource provider.</span></span> <span data-ttu-id="3994d-174">Например *SqlVM*.</span><span class="sxs-lookup"><span data-stu-id="3994d-174">For example, *SqlVM*.</span></span> |  <span data-ttu-id="3994d-175">_Обязательно_</span><span class="sxs-lookup"><span data-stu-id="3994d-175">_required_</span></span> |
| <span data-ttu-id="3994d-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="3994d-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="3994d-177">Файлы сертификата должен быть помещен в этот каталог также.</span><span class="sxs-lookup"><span data-stu-id="3994d-177">Your certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="3994d-178">_Необязательный_</span><span class="sxs-lookup"><span data-stu-id="3994d-178">_optional_</span></span> |
| <span data-ttu-id="3994d-179">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="3994d-179">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="3994d-180">Пароль для PFX-сертификата</span><span class="sxs-lookup"><span data-stu-id="3994d-180">The password for the .pfx certificate</span></span> | <span data-ttu-id="3994d-181">_Обязательно_</span><span class="sxs-lookup"><span data-stu-id="3994d-181">_required_</span></span> |
| <span data-ttu-id="3994d-182">**Значение параметра MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="3994d-182">**MaxRetryCount**</span></span> | <span data-ttu-id="3994d-183">Определите сколько раз повторить каждой операции, если имеется ошибка.</span><span class="sxs-lookup"><span data-stu-id="3994d-183">Define how many times you want to retry each operation if there is a failure.</span></span>| <span data-ttu-id="3994d-184">2</span><span class="sxs-lookup"><span data-stu-id="3994d-184">2</span></span> |
| <span data-ttu-id="3994d-185">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="3994d-185">**RetryDuration**</span></span> | <span data-ttu-id="3994d-186">Укажите время ожидания между повторными попытками в секундах.</span><span class="sxs-lookup"><span data-stu-id="3994d-186">Define the timeout between retries, in seconds.</span></span> | <span data-ttu-id="3994d-187">120</span><span class="sxs-lookup"><span data-stu-id="3994d-187">120</span></span> |
| <span data-ttu-id="3994d-188">**Удаление**</span><span class="sxs-lookup"><span data-stu-id="3994d-188">**Uninstall**</span></span> | <span data-ttu-id="3994d-189">Удалить поставщик ресурсов и все связанные ресурсы (см. примечания ниже)</span><span class="sxs-lookup"><span data-stu-id="3994d-189">Remove the resource provider and all associated resources (see notes below)</span></span> | <span data-ttu-id="3994d-190">Нет</span><span class="sxs-lookup"><span data-stu-id="3994d-190">No</span></span> |
| <span data-ttu-id="3994d-191">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="3994d-191">**DebugMode**</span></span> | <span data-ttu-id="3994d-192">Предотвращает автоматическую очистку в случае ошибки</span><span class="sxs-lookup"><span data-stu-id="3994d-192">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="3994d-193">Нет</span><span class="sxs-lookup"><span data-stu-id="3994d-193">No</span></span> |


## <a name="verify-the-deployment-using-the-azure-stack-portal"></a><span data-ttu-id="3994d-194">Проверка развертывания на портале Azure стека</span><span class="sxs-lookup"><span data-stu-id="3994d-194">Verify the deployment using the Azure Stack Portal</span></span>

> [!NOTE]
>  <span data-ttu-id="3994d-195">После завершения сценария установки, необходимо будет обновить портал для см. в колонке администратора.</span><span class="sxs-lookup"><span data-stu-id="3994d-195">After the installation script completes, you will need to refresh the portal to see the admin blade.</span></span>


1. <span data-ttu-id="3994d-196">На рабочем столе виртуальной Машины в консоли щелкните **стека портал Microsoft Azure** и выполните вход на портал администратора службы.</span><span class="sxs-lookup"><span data-stu-id="3994d-196">On the Console VM desktop, click **Microsoft Azure Stack Portal** and sign in to the portal as the service administrator.</span></span>

2. <span data-ttu-id="3994d-197">Проверьте успешность развертывания.</span><span class="sxs-lookup"><span data-stu-id="3994d-197">Verify that the deployment succeeded.</span></span> <span data-ttu-id="3994d-198">Нажмите кнопку **групп ресурсов** &gt; щелкните группы ресурсов, который использовался, а затем убедитесь, что компонент essentials колонке (верхняя половина) операции чтения  **_даты_ (успешно)**.</span><span class="sxs-lookup"><span data-stu-id="3994d-198">Click **Resource Groups** &gt; click the resource group you used and then make sure that the essentials part of the blade (upper half) reads **_date_ (Succeeded)**.</span></span>

      ![Проверка развертывания SQL RP](./media/azure-stack-sql-rp-deploy/sqlrp-verify.png)


## <a name="provide-capacity-by-connecting-to-a-hosting-sql-server"></a><span data-ttu-id="3994d-200">Укажите емкость, подключившись к серверу управления SQL</span><span class="sxs-lookup"><span data-stu-id="3994d-200">Provide capacity by connecting to a hosting SQL server</span></span>

1. <span data-ttu-id="3994d-201">Войдите в портал администрирования стек Azure как администратор службы</span><span class="sxs-lookup"><span data-stu-id="3994d-201">Sign in to the Azure Stack admin portal as a service admin</span></span>

2. <span data-ttu-id="3994d-202">Создание виртуальной машины SQL, если таковая имеется уже доступны.</span><span class="sxs-lookup"><span data-stu-id="3994d-202">Create a SQL virtual machine, unless you have one already available.</span></span> <span data-ttu-id="3994d-203">Marketplace управления предлагает некоторые возможности для развертывания виртуальных машин SQL.</span><span class="sxs-lookup"><span data-stu-id="3994d-203">Marketplace Management offers some options for deploying SQL VMs.</span></span>

3. <span data-ttu-id="3994d-204">Нажмите кнопку **поставщиков ресурсов** &gt; **SQLAdapter** &gt; **серверы размещения** &gt; **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="3994d-204">Click **Resource Providers** &gt; **SQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="3994d-205">**Серверов размещения SQL** колонка находится где поставщика ресурсов SQL Server могут подключаться к фактических экземпляров SQL Server, используемые в качестве серверной части поставщик ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3994d-205">The **SQL Hosting Servers** blade is where you can connect the SQL Server Resource Provider to actual instances of SQL Server that serve as the resource provider’s backend.</span></span>

    ![Серверы размещения](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.PNG)

4. <span data-ttu-id="3994d-207">Заполнение формы данные подключения к экземпляру SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3994d-207">Fill the form with the connection details of your SQL Server instance.</span></span>

    ![Новый сервер размещения](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

    > [!NOTE]
    > <span data-ttu-id="3994d-209">До тех пор, пока экземпляр SQL может осуществляться клиента и администратора диспетчера ресурсов Azure, можно поместить в группе управления поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3994d-209">As long as the SQL instance can be accessed by the tenant and admin Azure Resource Manager, it can be placed under control of the resource provider.</span></span> <span data-ttu-id="3994d-210">Экземпляр SQL __должен__ выделить исключительно для RP.</span><span class="sxs-lookup"><span data-stu-id="3994d-210">The SQL instance __must__ be allocated exclusively to the RP.</span></span>

5. <span data-ttu-id="3994d-211">При добавлении серверов, их необходимо назначить новую или существующую номера SKU для различения предложения услуг.</span><span class="sxs-lookup"><span data-stu-id="3994d-211">As you add servers, you must assign them to a new or existing SKU to differentiate service offerings.</span></span> <span data-ttu-id="3994d-212">Например может иметь экземпляр SQL Enterprise, предоставляя объем базы данных и автоматическое резервное копирование, зарезервировать высокопроизводительных серверов для отдельных подразделений и т. д. Имя SKU должны отражать свойства, чтобы соответствующим образом клиентов можно размещать свои базы данных и все серверы размещения в номере SKU должен иметь те же возможности.</span><span class="sxs-lookup"><span data-stu-id="3994d-212">For example, you could have a SQL Enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. The SKU name should reflect the properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have the same capabilities.</span></span>

    <span data-ttu-id="3994d-213">Пример:</span><span class="sxs-lookup"><span data-stu-id="3994d-213">An example:</span></span>

    ![Номера SKU](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

>[!NOTE]
<span data-ttu-id="3994d-215">Номера SKU может занять до часа должен отображаться на портале.</span><span class="sxs-lookup"><span data-stu-id="3994d-215">SKUs can take up to an hour to be visible in the portal.</span></span> <span data-ttu-id="3994d-216">Невозможно создать базу данных, пока не будет создан SKU.</span><span class="sxs-lookup"><span data-stu-id="3994d-216">You cannot create a database until the SKU is created.</span></span>


## <a name="create-your-first-sql-database-to-test-your-deployment"></a><span data-ttu-id="3994d-217">Создание первой базы данных SQL для тестирования развертывания</span><span class="sxs-lookup"><span data-stu-id="3994d-217">Create your first SQL database to test your deployment</span></span>

1. <span data-ttu-id="3994d-218">Войдите в портал администрирования стек Azure как администратора службы.</span><span class="sxs-lookup"><span data-stu-id="3994d-218">Sign in to the Azure Stack admin portal as service admin.</span></span>

2. <span data-ttu-id="3994d-219">Нажмите кнопку **+ создать** &gt; **данные + хранилище»** &gt; **базы данных SQL Server (Предварительная версия)** &gt; **добавить**.</span><span class="sxs-lookup"><span data-stu-id="3994d-219">Click **+ New** &gt;**Data + Storage"** &gt; **SQL Server Database (preview)** &gt; **Add**.</span></span>

3. <span data-ttu-id="3994d-220">Заполните форму с сведения о базе данных, включая **имя базы данных**, **максимальный размер**и при необходимости измените другие параметры.</span><span class="sxs-lookup"><span data-stu-id="3994d-220">Fill in the form with database details, including a **Database Name**, **Maximum Size**, and change the other parameters as necessary.</span></span> <span data-ttu-id="3994d-221">Вам будет предложено выбрать SKU для базы данных.</span><span class="sxs-lookup"><span data-stu-id="3994d-221">You are asked to pick a SKU for your database.</span></span> <span data-ttu-id="3994d-222">По мере добавления серверов размещения они назначаются SKU и базы данных создаются в этом пуле размещения серверов, которые составляют SKU.</span><span class="sxs-lookup"><span data-stu-id="3994d-222">As hosting servers are added, they are assigned a SKU and databases are created in that pool of hosting servers that make up the SKU.</span></span>

    ![Новая база данных](./media/azure-stack-sql-rp-deploy/newsqldb.png)


4. <span data-ttu-id="3994d-224">Заполните параметры входа: **входа базы данных**, и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="3994d-224">Fill in the Login Settings: **Database login**, and **Password**.</span></span> <span data-ttu-id="3994d-225">Это учетные данные проверки подлинности SQL, созданный для доступа к этой базе данных только.</span><span class="sxs-lookup"><span data-stu-id="3994d-225">This is a SQL Authentication credential that is created for your access to this database only.</span></span> <span data-ttu-id="3994d-226">Имя пользователя должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="3994d-226">The login user name must be globally unique.</span></span> <span data-ttu-id="3994d-227">Создайте новый параметр имени входа или выберите существующий.</span><span class="sxs-lookup"><span data-stu-id="3994d-227">Either create a new login setting or select an existing one.</span></span> <span data-ttu-id="3994d-228">Можно повторно использовать параметры входа для других баз данных с помощью того же SKU.</span><span class="sxs-lookup"><span data-stu-id="3994d-228">You can reuse login settings for other databases using the same SKU.</span></span>

    ![Создать новое имя входа базы данных](./media/azure-stack-sql-rp-deploy/create-new-login.png)


5. <span data-ttu-id="3994d-230">Отправить форму и ожидания для завершения развертывания.</span><span class="sxs-lookup"><span data-stu-id="3994d-230">Submit the form and wait for the deployment to complete.</span></span>

    <span data-ttu-id="3994d-231">В колонке полученный Обратите внимание, поле «Строка соединения».</span><span class="sxs-lookup"><span data-stu-id="3994d-231">In the resulting blade, notice the “Connection string” field.</span></span> <span data-ttu-id="3994d-232">В комплекте Azure можно использовать этой строки в любое приложение, которое требуется доступ к SQL Server (например, веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="3994d-232">You can use that string in any application that requires SQL Server access (for example, a web app) in your Azure Stack.</span></span>

    ![Получить строку подключения](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="add-capacity"></a><span data-ttu-id="3994d-234">Добавить емкость</span><span class="sxs-lookup"><span data-stu-id="3994d-234">Add capacity</span></span>

<span data-ttu-id="3994d-235">Добавление емкости путем добавления дополнительных узлов SQL на портале Azure стека и связать их с соответствующий номер SKU.</span><span class="sxs-lookup"><span data-stu-id="3994d-235">Add capacity by adding additional SQL hosts in the Azure Stack portal and associate them with an appropriate SKU.</span></span> <span data-ttu-id="3994d-236">Если вы хотите использовать другой экземпляр SQL Server вместо того, установлен на поставщика виртуальной Машины, нажмите кнопку **поставщиков ресурсов** &gt; **SQLAdapter** &gt; **размещения SQL Серверы** &gt; **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="3994d-236">If you wish to use another instance of SQL instead of the one installed on the provider VM, click **Resource Providers** &gt; **SQLAdapter** &gt; **SQL Hosting Servers** &gt; **+Add**.</span></span>

## <a name="making-sql-databases-available-to-tenants"></a><span data-ttu-id="3994d-237">Предоставление клиентам баз данных SQL</span><span class="sxs-lookup"><span data-stu-id="3994d-237">Making SQL databases available to tenants</span></span>

<span data-ttu-id="3994d-238">Создайте планы и предложения для предоставления базы данных SQL для клиентов.</span><span class="sxs-lookup"><span data-stu-id="3994d-238">Create plans and offers to make SQL databases available for tenants.</span></span> <span data-ttu-id="3994d-239">Необходимо создать план, добавьте службу Microsoft.SqlAdapter к плану и добавить существующую квоту или создать новую.</span><span class="sxs-lookup"><span data-stu-id="3994d-239">You must create a plan, add the Microsoft.SqlAdapter service to the plan, and add an existing Quota, or create a new one.</span></span> <span data-ttu-id="3994d-240">При создании квоты, можно указать возможность разрешить клиента.</span><span class="sxs-lookup"><span data-stu-id="3994d-240">If you create a quota, you can specify the capacity to allow the tenant.</span></span>
    <span data-ttu-id="3994d-241">![Создание планов и предложения для включения базы данных](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span><span class="sxs-lookup"><span data-stu-id="3994d-241">![Create plans and offers to include databases](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span></span>

## <a name="tenant-usage-of-the-resource-provider"></a><span data-ttu-id="3994d-242">Использование клиента поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="3994d-242">Tenant usage of the Resource Provider</span></span>

<span data-ttu-id="3994d-243">Самообслуживания баз данных доступны через интерфейс портала клиента.</span><span class="sxs-lookup"><span data-stu-id="3994d-243">Self-service databases are provided through the tenant portal experience.</span></span>

## <a name="removing-the-sql-adapter-resource-provider"></a><span data-ttu-id="3994d-244">Удаление поставщика ресурсов адаптера SQL</span><span class="sxs-lookup"><span data-stu-id="3994d-244">Removing the SQL Adapter Resource Provider</span></span>

<span data-ttu-id="3994d-245">Чтобы удалить поставщик ресурсов, необходимо сначала удалить все зависимости.</span><span class="sxs-lookup"><span data-stu-id="3994d-245">In order to remove the resource provider, it is essential to first remove any dependencies.</span></span>

1. <span data-ttu-id="3994d-246">Убедитесь, что у вас есть исходный пакет развертывания, загруженный для этой версии поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3994d-246">Ensure you have the original deployment package that you downloaded for this version of the Resource Provider.</span></span>

2. <span data-ttu-id="3994d-247">Все базы данных клиента, необходимо удалить из поставщика ресурсов (это не удалит данные).</span><span class="sxs-lookup"><span data-stu-id="3994d-247">All tenant databases must be deleted from the resource provider (this will not delete the data).</span></span> <span data-ttu-id="3994d-248">Это следует выполнять с сами клиенты.</span><span class="sxs-lookup"><span data-stu-id="3994d-248">This should be performed by the tenants themselves.</span></span>

3. <span data-ttu-id="3994d-249">Администратор должен удалить серверы размещения из адаптера SQL</span><span class="sxs-lookup"><span data-stu-id="3994d-249">Administrator must delete the hosting servers from the SQL Adapter</span></span>

4. <span data-ttu-id="3994d-250">Администратор должен удалить все планы, которые ссылаются на адаптере SQL.</span><span class="sxs-lookup"><span data-stu-id="3994d-250">Administrator must delete any plans that reference the SQL Adapter.</span></span>

5. <span data-ttu-id="3994d-251">Администратору необходимо удалить все номера SKU и квоты, связанные с адаптера SQL.</span><span class="sxs-lookup"><span data-stu-id="3994d-251">Administrator must delete any SKUs and quotas associated to the SQL Adapter.</span></span>

6. <span data-ttu-id="3994d-252">Снова запустите скрипт развертывания с удалить параметр, конечные точки диспетчера ресурсов Azure, DirectoryTenantID и учетные данные для учетной записи администратора службы.</span><span class="sxs-lookup"><span data-stu-id="3994d-252">Rerun the deployment script with the -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for the service administrator account.</span></span>



## <a name="next-steps"></a><span data-ttu-id="3994d-253">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3994d-253">Next steps</span></span>


<span data-ttu-id="3994d-254">Попробуйте другой [служб PaaS](azure-stack-tools-paas-services.md) как [поставщик ресурсов MySQL Server](azure-stack-mysql-resource-provider-deploy.md) и [поставщик ресурсов службы приложений](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3994d-254">Try other [PaaS services](azure-stack-tools-paas-services.md) like the [MySQL Server resource provider](azure-stack-mysql-resource-provider-deploy.md) and the [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
