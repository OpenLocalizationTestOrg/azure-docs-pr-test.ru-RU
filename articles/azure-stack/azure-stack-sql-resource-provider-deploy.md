---
title: "базы данных aaaUsing SQL стек Azure | Документы Microsoft"
description: "Дополнительные сведения о развертывании баз данных SQL как служба в Azure стека и hello hello toodeploy Быстрые действия SQL Server адаптер поставщика ресурсов"
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
ms.openlocfilehash: 01418ce7cd708ca8f9e302d6bcd2a43ad33df93f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="6be1c-103">Использование баз данных SQL Microsoft Azure стеке</span><span class="sxs-lookup"><span data-stu-id="6be1c-103">Use SQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="6be1c-104">Используйте hello ресурсов поставщика адаптера tooexpose SQL базы данных SQL Server в качестве службы Azure стека.</span><span class="sxs-lookup"><span data-stu-id="6be1c-104">Use hello SQL Server resource provider adapter tooexpose SQL databases as a service of Azure Stack.</span></span> <span data-ttu-id="6be1c-105">После установки поставщика ресурсов hello и подключите его tooone или более экземпляров SQL Server, вас и ваших пользователей можно создавать базы данных для рабочих нагрузок, основанных на SQL без необходимости виртуальной tooprovision, облако в собственном коде приложений и веб-сайтов, которые основаны на SQL машины (VM), на котором размещается SQL Server каждый раз.</span><span class="sxs-lookup"><span data-stu-id="6be1c-105">After you install hello resource provider and connect it tooone or more SQL Server instances, you and your users can create databases for cloud-native apps, websites that are based on SQL, and workloads that are based on SQL without having tooprovision a virtual machine (VM) that hosts SQL Server each time.</span></span>

<span data-ttu-id="6be1c-106">поставщик ресурсов Hello не поддерживает все возможности управления базами данных hello объекта [базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="6be1c-106">hello resource provider does not support all hello database management capabilities of [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).</span></span> <span data-ttu-id="6be1c-107">Например пулы эластичных баз данных и производительность базы данных tooscale hello возможности не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="6be1c-107">For example, elastic database pools and hello ability tooscale database performance aren't supported.</span></span> <span data-ttu-id="6be1c-108">Hello API не совместим с баз данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be1c-108">hello API is not compatible with SQL DB.</span></span>


## <a name="sql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="6be1c-109">Архитектура адаптера поставщика ресурсов SQL Server</span><span class="sxs-lookup"><span data-stu-id="6be1c-109">SQL Server Resource Provider Adapter architecture</span></span>
<span data-ttu-id="6be1c-110">поставщик ресурсов Hello не основан на, а также предоставляют все возможности управления базами данных hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6be1c-110">hello resource provider is not based on, nor does it offer all hello database management capabilities of Azure SQL Database.</span></span> <span data-ttu-id="6be1c-111">Например пулы эластичных баз данных и производительность базы данных hello возможность toodial вверх и вниз автоматически недоступны.</span><span class="sxs-lookup"><span data-stu-id="6be1c-111">For example, elastic database pools and hello ability toodial database performance up and down automatically aren't available.</span></span> <span data-ttu-id="6be1c-112">Тем не менее hello ресурсов поставщик поддерживает аналогичные создания, чтения, обновления и удаления (CRUD).</span><span class="sxs-lookup"><span data-stu-id="6be1c-112">However, hello resource provider does support similar create, read, update, and delete (CRUD) operations.</span></span>

<span data-ttu-id="6be1c-113">поставщик ресурсов Hello состоит из трех компонентов:</span><span class="sxs-lookup"><span data-stu-id="6be1c-113">hello resource provider is made up of three components:</span></span>

- <span data-ttu-id="6be1c-114">**поставщик ресурсов адаптера виртуальной Машины для Hello SQL**, который является виртуальной машине под управлением служб поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-114">**hello SQL resource provider adapter VM**, which is a Windows virtual machine running hello provider services.</span></span>
- <span data-ttu-id="6be1c-115">**поставщик ресурсов Hello сам**, который обрабатывает запросы на подготовку, и предоставляет доступ к базе данных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6be1c-115">**hello resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="6be1c-116">**Серверы, на которых размещаются SQL Server**, предоставляющие емкости для баз данных, называемые серверами размещения.</span><span class="sxs-lookup"><span data-stu-id="6be1c-116">**Servers that host SQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="6be1c-117">Этот выпуск больше не создает экземпляр SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be1c-117">This release no longer creates a SQL instance.</span></span> <span data-ttu-id="6be1c-118">Необходимо создать один (или несколько) и/или предоставления доступа tooexternal экземпляров SQL.</span><span class="sxs-lookup"><span data-stu-id="6be1c-118">You must create one (or more) and/or provide access tooexternal SQL instances.</span></span> <span data-ttu-id="6be1c-119">Существует ряд tooyou доступные параметры, включая шаблоны в hello [коллекции быстрый запуск Azure стека](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) и элементы Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6be1c-119">There are a number of options available tooyou including templates in hello [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) and Marketplace items.</span></span> 

>[!NOTE]
<span data-ttu-id="6be1c-120">Если вы загрузили какие-либо элементы SQL Marketplace, убедитесь, что также загрузить расширения SQL IaaS hello, или они не будут развернуты.</span><span class="sxs-lookup"><span data-stu-id="6be1c-120">If you have downloaded any SQL Marketplace items, make sure you also download hello SQL IaaS Extension or these will not deploy.</span></span>


## <a name="deploy-hello-resource-provider"></a><span data-ttu-id="6be1c-121">Разверните hello поставщик ресурсов</span><span class="sxs-lookup"><span data-stu-id="6be1c-121">Deploy hello resource provider</span></span>

1. <span data-ttu-id="6be1c-122">Если вы еще не сделали регистрации вашего пакета средств разработки и загрузите образ Windows Server 2016 EVAL hello загружаемых посредством управления Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6be1c-122">If you have not already done so, register your development kit and download hello Windows Server 2016 EVAL image downloadable through Marketplace Management.</span></span> <span data-ttu-id="6be1c-123">Можно также использовать сценарий toocreate [образа Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span><span class="sxs-lookup"><span data-stu-id="6be1c-123">You can also use a script toocreate a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span> <span data-ttu-id="6be1c-124">Среда выполнения Hello .NET 3.5 больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="6be1c-124">hello .NET 3.5 runtime is no longer required.</span></span>

2. <span data-ttu-id="6be1c-125">[Загрузите файл двоичных файлов поставщика ресурсов SQL hello](https://aka.ms/azurestacksqlrp) и извлеките его на узел комплект средств для разработки hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-125">[Download hello SQL resource provider binaries file](https://aka.ms/azurestacksqlrp) and extract it on hello development kit host.</span></span>

3. <span data-ttu-id="6be1c-126">Войдите в узел комплект средств для разработки toohello и извлечь hello временный каталог файла установщика tooa SQL RP.</span><span class="sxs-lookup"><span data-stu-id="6be1c-126">Sign in toohello development kit host and extract hello SQL RP installer file tooa temporary directory.</span></span>

4. <span data-ttu-id="6be1c-127">Hello Azure стека корневой сертификат извлекается и самозаверяющий сертификат создается как часть этого процесса.</span><span class="sxs-lookup"><span data-stu-id="6be1c-127">hello Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="6be1c-128">__Необязательно:__ при необходимости tooprovide на собственные, подготовьте сертификаты hello и копирования tooa локальный каталог при желании toocustomize сертификаты hello (сценарий установки переданный toohello).</span><span class="sxs-lookup"><span data-stu-id="6be1c-128">__Optional:__ If you need tooprovide your own, prepare hello certificates and copy tooa local directory if you wish toocustomize hello certificates (passed toohello installation script).</span></span> <span data-ttu-id="6be1c-129">Требуется hello следующие сертификаты:</span><span class="sxs-lookup"><span data-stu-id="6be1c-129">You need hello following certificates:</span></span>

    <span data-ttu-id="6be1c-130">а.</span><span class="sxs-lookup"><span data-stu-id="6be1c-130">a.</span></span> <span data-ttu-id="6be1c-131">Сертификатом с подстановочными символами для *.dbadapter. \<область\>.\< полного доменного имени\>.</span><span class="sxs-lookup"><span data-stu-id="6be1c-131">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="6be1c-132">Этот сертификат должен быть доверенным, такие как будет выдан центром сертификации (то есть hello цепочка доверия должен существовать без промежуточных сертификатов.) (Можно использовать сертификат один сайт с именем виртуальной Машины явную hello, предоставленные во время установки.)</span><span class="sxs-lookup"><span data-stu-id="6be1c-132">This certificate must be trusted, such as would be issued by a certificate authority (that is, hello chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with hello explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="6be1c-133">b.</span><span class="sxs-lookup"><span data-stu-id="6be1c-133">b.</span></span> <span data-ttu-id="6be1c-134">Hello корневой сертификат, используемый hello Azure Resource Manager для конкретного экземпляра Azure стека.</span><span class="sxs-lookup"><span data-stu-id="6be1c-134">hello root certificate used by hello Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="6be1c-135">Если он не найден, извлекается hello корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="6be1c-135">If it is not found, hello root certificate will be retrieved.</span></span>


5. <span data-ttu-id="6be1c-136">Откройте **новый** повышенными PowerShell консоли и измените toohello каталог, где были извлечены файлы hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-136">Open a **new** elevated PowerShell console and change toohello directory where you extracted hello files.</span></span> <span data-ttu-id="6be1c-137">Используйте новые проблемы tooavoid окна, которые могут быть вызваны неверные модули PowerShell, которые уже загружены в системе hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-137">Use a new window tooavoid problems that may arise from incorrect PowerShell modules already loaded on hello system.</span></span>

6. <span data-ttu-id="6be1c-138">После установки любой версии hello AzureRm или модули AzureStack PowerShell 1.2.9 или 1.2.10 будет запрашиваемые tooremove их или hello установка не продолжится.</span><span class="sxs-lookup"><span data-stu-id="6be1c-138">If you have installed any versions of hello AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted tooremove them or hello install will not proceed.</span></span> <span data-ttu-id="6be1c-139">Сюда входят версии 1.3 или выше.</span><span class="sxs-lookup"><span data-stu-id="6be1c-139">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="6be1c-140">Запустите hello DeploySqlProvider.ps1 сценария с параметрами hello перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="6be1c-140">Run hello DeploySqlProvider.ps1 script with hello parameters listed below.</span></span>

<span data-ttu-id="6be1c-141">Hello скрипт выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6be1c-141">hello script performs these steps:</span></span>

* <span data-ttu-id="6be1c-142">При необходимости, загрузите совместимую версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6be1c-142">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="6be1c-143">Передача сертификатов hello и другим учетным записям хранения артефактов tooa в комплекте Azure.</span><span class="sxs-lookup"><span data-stu-id="6be1c-143">Upload hello certificates and other artifacts tooa storage account on your Azure Stack.</span></span>
* <span data-ttu-id="6be1c-144">Опубликуйте пакеты коллекции, чтобы выполнить развертывание баз данных SQL с помощью коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-144">Publish gallery packages so that you can deploy SQL databases through hello gallery.</span></span>
* <span data-ttu-id="6be1c-145">Развертывание виртуальной Машины с помощью образа Windows Server 2016 hello, созданной на шаге 1 и установить поставщик ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-145">Deploy a VM using hello Windows Server 2016 image created in step 1 and install hello resource provider.</span></span>
* <span data-ttu-id="6be1c-146">Зарегистрируйте локальный DNS-запись сопоставляет tooyour поставщика ресурсов виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="6be1c-146">Register a local DNS record that maps tooyour resource provider VM.</span></span>
* <span data-ttu-id="6be1c-147">Регистрация поставщика ресурсов с hello локального диспетчера ресурсов Azure (клиента и администратора).</span><span class="sxs-lookup"><span data-stu-id="6be1c-147">Register your resource provider with hello local Azure Resource Manager (Tenant and Admin).</span></span>

> [!NOTE]
> <span data-ttu-id="6be1c-148">Если установка hello занимает более 90 минут, может произойти сбой вы видите сообщение об ошибке на экране приветствия и в файле журнала hello, а развертывания hello повторяется с ошибками шаг hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-148">If hello installation takes more than 90 minutes, it may fail and you see a failure message on hello screen and in hello log file, but hello deployment is retried from hello failing step.</span></span> <span data-ttu-id="6be1c-149">Систем, которые не соответствуют hello Рекомендуемый объем памяти и основных характеристик может оказаться может toodeploy hello SQL RP.</span><span class="sxs-lookup"><span data-stu-id="6be1c-149">Systems that do not meet hello recommended memory and core specifications may not be able toodeploy hello SQL RP.</span></span>
>

<span data-ttu-id="6be1c-150">Ниже приведен пример, можно запустить из hello PowerShell запрашивать (но при необходимости изменить конечные точки сведения и портала учетной записи hello):</span><span class="sxs-lookup"><span data-stu-id="6be1c-150">Here's an example you can run from hello PowerShell prompt (but change hello account information and portal endpoints as needed):</span></span>

```
# Install hello AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports hello API Version Profile required by Azure Stack into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download hello Azure Stack Tools from GitHub and set hello environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use hello following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace hello previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeploySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "SqlRPRG" -VmName "SqlVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass
 ```

### <a name="deploysqlproviderps1-parameters"></a><span data-ttu-id="6be1c-151">Параметры DeploySqlProvider.ps1</span><span class="sxs-lookup"><span data-stu-id="6be1c-151">DeploySqlProvider.ps1 parameters</span></span>
<span data-ttu-id="6be1c-152">Эти параметры можно указать в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-152">You can specify these parameters in hello command line.</span></span> <span data-ttu-id="6be1c-153">Если этого не сделать, или происходит сбой проверки параметров, будет предложено tooprovide hello необходимые объекты.</span><span class="sxs-lookup"><span data-stu-id="6be1c-153">If you do not, or any parameter validation fails, you are prompted tooprovide hello required ones.</span></span>

| <span data-ttu-id="6be1c-154">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="6be1c-154">Parameter Name</span></span> | <span data-ttu-id="6be1c-155">Описание</span><span class="sxs-lookup"><span data-stu-id="6be1c-155">Description</span></span> | <span data-ttu-id="6be1c-156">Комментарий или значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6be1c-156">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6be1c-157">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="6be1c-157">**DirectoryTenantID**</span></span> | <span data-ttu-id="6be1c-158">Hello Azure или каталог служб федерации Active Directory с Идентификатором (guid).</span><span class="sxs-lookup"><span data-stu-id="6be1c-158">hello Azure or ADFS Directory ID (guid).</span></span> | <span data-ttu-id="6be1c-159">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="6be1c-159">_required_</span></span> |
| <span data-ttu-id="6be1c-160">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="6be1c-160">**AzCredential**</span></span> | <span data-ttu-id="6be1c-161">Укажите hello учетные данные для учетной записи администратора служб Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-161">Provide hello credentials for hello Azure Stack Service Admin account.</span></span> <span data-ttu-id="6be1c-162">Необходимо использовать hello же учетные данные используются для развертывания Azure стека).</span><span class="sxs-lookup"><span data-stu-id="6be1c-162">You must use hello same credentials as you used for deploying Azure Stack).</span></span> | <span data-ttu-id="6be1c-163">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="6be1c-163">_required_</span></span> |
| <span data-ttu-id="6be1c-164">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="6be1c-164">**VMLocalCredential**</span></span> | <span data-ttu-id="6be1c-165">Укажите учетные данные hello hello учетной записи локального администратора поставщика ресурсов SQL hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="6be1c-165">Define hello credentials for hello local administrator account of hello SQL resource provider VM.</span></span> <span data-ttu-id="6be1c-166">Этот пароль также используется для hello SQL **sa** учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6be1c-166">This password is also used for hello SQL **sa** account.</span></span> | <span data-ttu-id="6be1c-167">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="6be1c-167">_required_</span></span> |
| <span data-ttu-id="6be1c-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="6be1c-168">**ResourceGroupName**</span></span> | <span data-ttu-id="6be1c-169">Определите имя для группы ресурсов, в котором будут храниться элементы, созданный этим сценарием.</span><span class="sxs-lookup"><span data-stu-id="6be1c-169">Define a name for a Resource Group in which items created by this script will be stored.</span></span> <span data-ttu-id="6be1c-170">Например *SqlRPRG*.</span><span class="sxs-lookup"><span data-stu-id="6be1c-170">For example, *SqlRPRG*.</span></span> |  <span data-ttu-id="6be1c-171">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="6be1c-171">_required_</span></span> |
| <span data-ttu-id="6be1c-172">**VmName**</span><span class="sxs-lookup"><span data-stu-id="6be1c-172">**VmName**</span></span> | <span data-ttu-id="6be1c-173">Определите имя hello hello виртуальной машины на какой поставщик ресурсов tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-173">Define hello name of hello virtual machine on which tooinstall hello resource provider.</span></span> <span data-ttu-id="6be1c-174">Например *SqlVM*.</span><span class="sxs-lookup"><span data-stu-id="6be1c-174">For example, *SqlVM*.</span></span> |  <span data-ttu-id="6be1c-175">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="6be1c-175">_required_</span></span> |
| <span data-ttu-id="6be1c-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="6be1c-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="6be1c-177">Файлы сертификата должен быть помещен в этот каталог также.</span><span class="sxs-lookup"><span data-stu-id="6be1c-177">Your certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="6be1c-178">_необязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="6be1c-178">_optional_</span></span> |
| <span data-ttu-id="6be1c-179">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="6be1c-179">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="6be1c-180">Hello пароль для PFX-файл сертификата hello</span><span class="sxs-lookup"><span data-stu-id="6be1c-180">hello password for hello .pfx certificate</span></span> | <span data-ttu-id="6be1c-181">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="6be1c-181">_required_</span></span> |
| <span data-ttu-id="6be1c-182">**Значение параметра MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="6be1c-182">**MaxRetryCount**</span></span> | <span data-ttu-id="6be1c-183">Определите количество повторений tooretry каждой операции при наличии сбоя.</span><span class="sxs-lookup"><span data-stu-id="6be1c-183">Define how many times you want tooretry each operation if there is a failure.</span></span>| <span data-ttu-id="6be1c-184">2</span><span class="sxs-lookup"><span data-stu-id="6be1c-184">2</span></span> |
| <span data-ttu-id="6be1c-185">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="6be1c-185">**RetryDuration**</span></span> | <span data-ttu-id="6be1c-186">Определите hello время ожидания между повторными попытками в секундах.</span><span class="sxs-lookup"><span data-stu-id="6be1c-186">Define hello timeout between retries, in seconds.</span></span> | <span data-ttu-id="6be1c-187">120</span><span class="sxs-lookup"><span data-stu-id="6be1c-187">120</span></span> |
| <span data-ttu-id="6be1c-188">**Удаление**</span><span class="sxs-lookup"><span data-stu-id="6be1c-188">**Uninstall**</span></span> | <span data-ttu-id="6be1c-189">Удалить поставщик ресурсов hello и все связанные ресурсы (см. примечания ниже)</span><span class="sxs-lookup"><span data-stu-id="6be1c-189">Remove hello resource provider and all associated resources (see notes below)</span></span> | <span data-ttu-id="6be1c-190">Нет</span><span class="sxs-lookup"><span data-stu-id="6be1c-190">No</span></span> |
| <span data-ttu-id="6be1c-191">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="6be1c-191">**DebugMode**</span></span> | <span data-ttu-id="6be1c-192">Предотвращает автоматическую очистку в случае ошибки</span><span class="sxs-lookup"><span data-stu-id="6be1c-192">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="6be1c-193">Нет</span><span class="sxs-lookup"><span data-stu-id="6be1c-193">No</span></span> |


## <a name="verify-hello-deployment-using-hello-azure-stack-portal"></a><span data-ttu-id="6be1c-194">Проверка развертывания hello, с помощью портала Azure стека hello</span><span class="sxs-lookup"><span data-stu-id="6be1c-194">Verify hello deployment using hello Azure Stack Portal</span></span>

> [!NOTE]
>  <span data-ttu-id="6be1c-195">После завершения сценария установки hello, вам потребуется toorefresh hello портала toosee hello admin колонку.</span><span class="sxs-lookup"><span data-stu-id="6be1c-195">After hello installation script completes, you will need toorefresh hello portal toosee hello admin blade.</span></span>


1. <span data-ttu-id="6be1c-196">На рабочем столе hello консоли виртуальной Машины, нажмите кнопку **стека портал Microsoft Azure** и войдите в портал toohello как Здравствуйте, администратор службы.</span><span class="sxs-lookup"><span data-stu-id="6be1c-196">On hello Console VM desktop, click **Microsoft Azure Stack Portal** and sign in toohello portal as hello service administrator.</span></span>

2. <span data-ttu-id="6be1c-197">Проверьте успешность развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-197">Verify that hello deployment succeeded.</span></span> <span data-ttu-id="6be1c-198">Нажмите кнопку **групп ресурсов** &gt; щелкните hello группы ресурсов, можно использовать и убедитесь, часть essentials hello hello колонке (верхняя половина) считывает  **_даты_ (успешноевыполнение)**.</span><span class="sxs-lookup"><span data-stu-id="6be1c-198">Click **Resource Groups** &gt; click hello resource group you used and then make sure that hello essentials part of hello blade (upper half) reads **_date_ (Succeeded)**.</span></span>

      ![Проверка развертывания hello SQL RP](./media/azure-stack-sql-rp-deploy/sqlrp-verify.png)


## <a name="provide-capacity-by-connecting-tooa-hosting-sql-server"></a><span data-ttu-id="6be1c-200">Предоставляют емкость, подключив tooa, где размещен SQL server</span><span class="sxs-lookup"><span data-stu-id="6be1c-200">Provide capacity by connecting tooa hosting SQL server</span></span>

1. <span data-ttu-id="6be1c-201">Войдите в toohello портал администрирования стек Azure как администратор службы</span><span class="sxs-lookup"><span data-stu-id="6be1c-201">Sign in toohello Azure Stack admin portal as a service admin</span></span>

2. <span data-ttu-id="6be1c-202">Создание виртуальной машины SQL, если таковая имеется уже доступны.</span><span class="sxs-lookup"><span data-stu-id="6be1c-202">Create a SQL virtual machine, unless you have one already available.</span></span> <span data-ttu-id="6be1c-203">Marketplace управления предлагает некоторые возможности для развертывания виртуальных машин SQL.</span><span class="sxs-lookup"><span data-stu-id="6be1c-203">Marketplace Management offers some options for deploying SQL VMs.</span></span>

3. <span data-ttu-id="6be1c-204">Нажмите кнопку **поставщиков ресурсов** &gt; **SQLAdapter** &gt; **серверы размещения** &gt; **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="6be1c-204">Click **Resource Providers** &gt; **SQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="6be1c-205">Hello **серверов размещения SQL** колонка находится где могут подключаться hello поставщика ресурсов SQL Server tooactual экземпляров SQL Server, выступающие в качестве hello серверной части поставщик ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6be1c-205">hello **SQL Hosting Servers** blade is where you can connect hello SQL Server Resource Provider tooactual instances of SQL Server that serve as hello resource provider’s backend.</span></span>

    ![Серверы размещения](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.PNG)

4. <span data-ttu-id="6be1c-207">Заполнение формы hello hello сведения о подключении вашего экземпляра SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6be1c-207">Fill hello form with hello connection details of your SQL Server instance.</span></span>

    ![Новый сервер размещения](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

    > [!NOTE]
    > <span data-ttu-id="6be1c-209">До тех пор, пока экземпляр SQL hello может осуществляться hello клиента и администратора диспетчера ресурсов Azure, можно поместить в группе управления hello поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6be1c-209">As long as hello SQL instance can be accessed by hello tenant and admin Azure Resource Manager, it can be placed under control of hello resource provider.</span></span> <span data-ttu-id="6be1c-210">экземпляр SQL Hello __должен__ выделить исключительно toohello RP.</span><span class="sxs-lookup"><span data-stu-id="6be1c-210">hello SQL instance __must__ be allocated exclusively toohello RP.</span></span>

5. <span data-ttu-id="6be1c-211">При добавлении серверов, их необходимо назначить tooa новый или существующий SKU toodifferentiate предложения услуг.</span><span class="sxs-lookup"><span data-stu-id="6be1c-211">As you add servers, you must assign them tooa new or existing SKU toodifferentiate service offerings.</span></span> <span data-ttu-id="6be1c-212">Например может иметь экземпляр SQL Enterprise, предоставляя объем базы данных и автоматическое резервное копирование, зарезервировать высокопроизводительных серверов для каждого конкретного отдела, т. д. имя SKU hello должны отражать hello свойства, чтобы клиентов можно размещать свои базы данных соответствующим образом и должны иметь все серверы размещения в номере SKU hello те же возможности.</span><span class="sxs-lookup"><span data-stu-id="6be1c-212">For example, you could have a SQL Enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. hello SKU name should reflect hello properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have hello same capabilities.</span></span>

    <span data-ttu-id="6be1c-213">Пример:</span><span class="sxs-lookup"><span data-stu-id="6be1c-213">An example:</span></span>

    ![Номера SKU](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

>[!NOTE]
<span data-ttu-id="6be1c-215">Номера SKU может занять toobe час tooan видны на портале hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-215">SKUs can take up tooan hour toobe visible in hello portal.</span></span> <span data-ttu-id="6be1c-216">Невозможно создать базу данных до создания SKU hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-216">You cannot create a database until hello SKU is created.</span></span>


## <a name="create-your-first-sql-database-tootest-your-deployment"></a><span data-ttu-id="6be1c-217">Создайте развертывание вашего первого tootest базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="6be1c-217">Create your first SQL database tootest your deployment</span></span>

1. <span data-ttu-id="6be1c-218">Войдите в toohello портала администратора Azure стека учетной записью администратора службы.</span><span class="sxs-lookup"><span data-stu-id="6be1c-218">Sign in toohello Azure Stack admin portal as service admin.</span></span>

2. <span data-ttu-id="6be1c-219">Нажмите кнопку **+ создать** &gt; **данные + хранилище»** &gt; **базы данных SQL Server (Предварительная версия)** &gt; **добавить**.</span><span class="sxs-lookup"><span data-stu-id="6be1c-219">Click **+ New** &gt;**Data + Storage"** &gt; **SQL Server Database (preview)** &gt; **Add**.</span></span>

3. <span data-ttu-id="6be1c-220">Заполните форму hello с сведения о базе данных, включая **имя базы данных**, **максимальный размер**, и изменения других параметров hello при необходимости.</span><span class="sxs-lookup"><span data-stu-id="6be1c-220">Fill in hello form with database details, including a **Database Name**, **Maximum Size**, and change hello other parameters as necessary.</span></span> <span data-ttu-id="6be1c-221">Вы просили toopick SKU базы данных.</span><span class="sxs-lookup"><span data-stu-id="6be1c-221">You are asked toopick a SKU for your database.</span></span> <span data-ttu-id="6be1c-222">По мере добавления серверов размещения они назначаются SKU и базы данных создаются в этом пуле размещения серверов, которые составляют hello SKU.</span><span class="sxs-lookup"><span data-stu-id="6be1c-222">As hosting servers are added, they are assigned a SKU and databases are created in that pool of hosting servers that make up hello SKU.</span></span>

    ![Новая база данных](./media/azure-stack-sql-rp-deploy/newsqldb.png)


4. <span data-ttu-id="6be1c-224">Заполните параметры входа hello: **входа базы данных**, и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="6be1c-224">Fill in hello Login Settings: **Database login**, and **Password**.</span></span> <span data-ttu-id="6be1c-225">Это учетные данные проверки подлинности SQL, создается только базы данных access toothis.</span><span class="sxs-lookup"><span data-stu-id="6be1c-225">This is a SQL Authentication credential that is created for your access toothis database only.</span></span> <span data-ttu-id="6be1c-226">Привет, имя пользователя должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="6be1c-226">hello login user name must be globally unique.</span></span> <span data-ttu-id="6be1c-227">Создайте новый параметр имени входа или выберите существующий.</span><span class="sxs-lookup"><span data-stu-id="6be1c-227">Either create a new login setting or select an existing one.</span></span> <span data-ttu-id="6be1c-228">Параметры входа можно использовать для других баз данных с помощью hello одним SKU.</span><span class="sxs-lookup"><span data-stu-id="6be1c-228">You can reuse login settings for other databases using hello same SKU.</span></span>

    ![Создать новое имя входа базы данных](./media/azure-stack-sql-rp-deploy/create-new-login.png)


5. <span data-ttu-id="6be1c-230">Отправьте форму hello и дождитесь toocomplete развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-230">Submit hello form and wait for hello deployment toocomplete.</span></span>

    <span data-ttu-id="6be1c-231">В колонке полученный hello Обратите внимание, поле «Строка подключения» hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-231">In hello resulting blade, notice hello “Connection string” field.</span></span> <span data-ttu-id="6be1c-232">В комплекте Azure можно использовать этой строки в любое приложение, которое требуется доступ к SQL Server (например, веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="6be1c-232">You can use that string in any application that requires SQL Server access (for example, a web app) in your Azure Stack.</span></span>

    ![Получить строку подключения hello](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="add-capacity"></a><span data-ttu-id="6be1c-234">Добавить емкость</span><span class="sxs-lookup"><span data-stu-id="6be1c-234">Add capacity</span></span>

<span data-ttu-id="6be1c-235">Добавление емкости путем добавления дополнительных узлов SQL на портале Azure стека hello и связать их с соответствующий номер SKU.</span><span class="sxs-lookup"><span data-stu-id="6be1c-235">Add capacity by adding additional SQL hosts in hello Azure Stack portal and associate them with an appropriate SKU.</span></span> <span data-ttu-id="6be1c-236">Toouse другой экземпляр SQL Server вместо hello установлена на поставщик hello виртуальной Машины, нажмите кнопку **поставщиков ресурсов** &gt; **SQLAdapter** &gt; **размещения SQL Серверы** &gt; **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="6be1c-236">If you wish toouse another instance of SQL instead of hello one installed on hello provider VM, click **Resource Providers** &gt; **SQLAdapter** &gt; **SQL Hosting Servers** &gt; **+Add**.</span></span>

## <a name="making-sql-databases-available-tootenants"></a><span data-ttu-id="6be1c-237">Сделать доступной tootenants баз данных SQL</span><span class="sxs-lookup"><span data-stu-id="6be1c-237">Making SQL databases available tootenants</span></span>

<span data-ttu-id="6be1c-238">Создайте планы и предложения toomake баз данных SQL, доступных для клиентов.</span><span class="sxs-lookup"><span data-stu-id="6be1c-238">Create plans and offers toomake SQL databases available for tenants.</span></span> <span data-ttu-id="6be1c-239">Необходимо создать план, добавить план toohello службы Microsoft.SqlAdapter hello и добавить существующую квоту или создать новую.</span><span class="sxs-lookup"><span data-stu-id="6be1c-239">You must create a plan, add hello Microsoft.SqlAdapter service toohello plan, and add an existing Quota, or create a new one.</span></span> <span data-ttu-id="6be1c-240">При создании квоты, клиент можно указать hello емкость tooallow hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-240">If you create a quota, you can specify hello capacity tooallow hello tenant.</span></span>
    <span data-ttu-id="6be1c-241">![Создание планов и предложения tooinclude баз данных](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span><span class="sxs-lookup"><span data-stu-id="6be1c-241">![Create plans and offers tooinclude databases](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span></span>

## <a name="tenant-usage-of-hello-resource-provider"></a><span data-ttu-id="6be1c-242">Использование клиента hello поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="6be1c-242">Tenant usage of hello Resource Provider</span></span>

<span data-ttu-id="6be1c-243">Самообслуживания баз данных обеспечивается взаимодействие портала клиента hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-243">Self-service databases are provided through hello tenant portal experience.</span></span>

## <a name="removing-hello-sql-adapter-resource-provider"></a><span data-ttu-id="6be1c-244">Удаление hello поставщика ресурсов адаптера SQL</span><span class="sxs-lookup"><span data-stu-id="6be1c-244">Removing hello SQL Adapter Resource Provider</span></span>

<span data-ttu-id="6be1c-245">В поставщике ресурсов hello tooremove заказа, очень важно toofirst удалите все зависимости.</span><span class="sxs-lookup"><span data-stu-id="6be1c-245">In order tooremove hello resource provider, it is essential toofirst remove any dependencies.</span></span>

1. <span data-ttu-id="6be1c-246">Убедитесь, что у вас есть hello исходного развертывания пакет, загруженный для этой версии hello поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6be1c-246">Ensure you have hello original deployment package that you downloaded for this version of hello Resource Provider.</span></span>

2. <span data-ttu-id="6be1c-247">Все базы данных клиента, необходимо удалить из поставщика ресурсов hello (это не удалит данные hello).</span><span class="sxs-lookup"><span data-stu-id="6be1c-247">All tenant databases must be deleted from hello resource provider (this will not delete hello data).</span></span> <span data-ttu-id="6be1c-248">Это следует выполнять с сами клиенты hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-248">This should be performed by hello tenants themselves.</span></span>

3. <span data-ttu-id="6be1c-249">Администратор должен удалить серверы из hello адаптера SQL размещения hello</span><span class="sxs-lookup"><span data-stu-id="6be1c-249">Administrator must delete hello hosting servers from hello SQL Adapter</span></span>

4. <span data-ttu-id="6be1c-250">Администратор должен удалить все планы, которые ссылаются на hello адаптера SQL.</span><span class="sxs-lookup"><span data-stu-id="6be1c-250">Administrator must delete any plans that reference hello SQL Adapter.</span></span>

5. <span data-ttu-id="6be1c-251">Администратор должен удалить номера SKU и квоты связанные toohello адаптера SQL.</span><span class="sxs-lookup"><span data-stu-id="6be1c-251">Administrator must delete any SKUs and quotas associated toohello SQL Adapter.</span></span>

6. <span data-ttu-id="6be1c-252">Снова запустите скрипт развертывания hello с hello - удалить параметр, конечные точки диспетчера ресурсов Azure, DirectoryTenantID и учетные данные для учетной записи администратора службы hello.</span><span class="sxs-lookup"><span data-stu-id="6be1c-252">Rerun hello deployment script with hello -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for hello service administrator account.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6be1c-253">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6be1c-253">Next steps</span></span>


<span data-ttu-id="6be1c-254">Попробуйте другой [служб PaaS](azure-stack-tools-paas-services.md) как hello [поставщик ресурсов MySQL Server](azure-stack-mysql-resource-provider-deploy.md) и hello [поставщик ресурсов службы приложений](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6be1c-254">Try other [PaaS services](azure-stack-tools-paas-services.md) like hello [MySQL Server resource provider](azure-stack-mysql-resource-provider-deploy.md) and hello [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
