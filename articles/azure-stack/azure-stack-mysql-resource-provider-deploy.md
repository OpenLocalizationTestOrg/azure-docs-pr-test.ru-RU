---
title: "базы данных aaaUse MySQL как PaaS стек Azure | Документы Microsoft"
description: "Узнайте, как развернуть hello поставщик ресурсов MySQL и предоставить баз данных MySQL в качестве службы на стек Azure"
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
ms.openlocfilehash: 634e408eae9f3d8257a8610c60def0978ce333c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="ff4a6-103">Использование базы данных MySQL в стеке Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ff4a6-103">Use MySQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="ff4a6-104">Вы можете развернуть поставщик ресурсов MySQL в Azure стек.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-104">You can deploy a MySQL resource provider on Azure Stack.</span></span> <span data-ttu-id="ff4a6-105">После развертывания hello поставщика ресурсов, можно создать MySQL серверов и баз данных с помощью шаблонов развертывания диспетчера ресурсов Azure и предоставить баз данных MySQL в качестве службы.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-105">After you deploy hello resource provider, you can create MySQL servers and databases through Azure Resource Manager deployment templates and provide MySQL databases as a service.</span></span> <span data-ttu-id="ff4a6-106">Базы данных MySQL, которые используются на веб-сайтах, поддерживают множество платформ веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-106">MySQL databases, which are common on web sites, support many website platforms.</span></span> <span data-ttu-id="ff4a6-107">Например после развертывания hello поставщика ресурсов, можно создать веб-сайты WordPress с платформы Azure веб-приложения hello как дополнительный компонент службы (PaaS) стек Azure.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-107">As an example, after you deploy hello resource provider, you can create WordPress websites from hello Azure Web Apps platform as a service (PaaS) add-on for Azure Stack.</span></span>

<span data-ttu-id="ff4a6-108">Поставщик MySQL toodeploy hello в системе, которая не имеет доступа к Интернету, можно скопировать файл hello [mysql соединитель net 6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa локального совместное использование и предоставлять этим сетевым именем при появлении запроса (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="ff4a6-108">toodeploy hello MySQL provider on a system that does not have internet access, you can copy hello file [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa local share and provide that share name when prompted (see below).</span></span> <span data-ttu-id="ff4a6-109">Необходимо также установить hello Azure и Azure стека модули PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-109">You must also install hello Azure and Azure Stack PowerShell modules.</span></span>


## <a name="mysql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="ff4a6-110">Архитектура адаптера поставщика ресурсов MySQL Server</span><span class="sxs-lookup"><span data-stu-id="ff4a6-110">MySQL Server Resource Provider Adapter architecture</span></span>

<span data-ttu-id="ff4a6-111">поставщик ресурсов Hello состоит из трех компонентов:</span><span class="sxs-lookup"><span data-stu-id="ff4a6-111">hello resource provider is made up of three components:</span></span>

- <span data-ttu-id="ff4a6-112">**поставщик ресурсов адаптера виртуальной Машины для Hello MySQL**, который является виртуальной машине под управлением служб поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-112">**hello MySQL resource provider adapter VM**, which is a Windows virtual machine running hello provider services.</span></span>
- <span data-ttu-id="ff4a6-113">**поставщик ресурсов Hello сам**, который обрабатывает запросы на подготовку, и предоставляет доступ к базе данных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-113">**hello resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="ff4a6-114">**Серверы, на которых размещены сервер MySQL**, предоставляющие емкости для баз данных, называемые серверами размещения.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-114">**Servers that host MySQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="ff4a6-115">Этот выпуск больше не создает экземпляр MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-115">This release no longer creates a MySQL instance.</span></span> <span data-ttu-id="ff4a6-116">Необходимо создать их и/или предоставления доступа tooexternal экземпляров SQL.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-116">You must create them and/or provide access tooexternal SQL instances.</span></span> <span data-ttu-id="ff4a6-117">Вы можете посетить hello [коллекции быстрый запуск Azure стека](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) для шаблона пример, который можно создать сервер MySQL для вас или загрузить и установить сервер MySQL из hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-117">You can visit hello [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) for an example template that can create a MySQL server for you or download and deploy a MySQL Server from hello Marketplace.</span></span>

## <a name="deploy-hello-resource-provider"></a><span data-ttu-id="ff4a6-118">Разверните hello поставщик ресурсов</span><span class="sxs-lookup"><span data-stu-id="ff4a6-118">Deploy hello resource provider</span></span>

1. <span data-ttu-id="ff4a6-119">Если вы еще не сделали зарегистрировать ваш пакет средств разработки и загрузите hello Windows Server 2016 Datacenter - Eval образа загрузки через Marketplace управления.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-119">If you have not already done so, register your development kit and download hello Windows Server 2016 Datacenter - Eval image downloadable through Marketplace Management.</span></span> <span data-ttu-id="ff4a6-120">Можно также использовать сценарий toocreate [образа Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span><span class="sxs-lookup"><span data-stu-id="ff4a6-120">You can also use a script toocreate a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span>

2. <span data-ttu-id="ff4a6-121">[Загрузите файл двоичных файлов поставщика ресурсов MySQL hello](https://aka.ms/azurestackmysqlrp) и извлеките его на узел комплект средств для разработки hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-121">[Download hello MySQL resource provider binaries file](https://aka.ms/azurestackmysqlrp) and extract it on hello development kit host.</span></span>

3. <span data-ttu-id="ff4a6-122">Войдите в узел комплект средств для разработки toohello и извлечь hello временный каталог файла установщика tooa MySQL RP.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-122">Sign in toohello development kit host, and extract hello MySQL RP installer file tooa temporary directory.</span></span>

4. <span data-ttu-id="ff4a6-123">Hello Azure стека корневой сертификат извлекается и самозаверяющий сертификат создается как часть этого процесса.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-123">hello Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="ff4a6-124">__Необязательно:__ при необходимости tooprovide на собственные, подготовьте сертификаты hello и копирования tooa локальный каталог при желании toocustomize сертификаты hello (сценарий установки переданный toohello).</span><span class="sxs-lookup"><span data-stu-id="ff4a6-124">__Optional:__ If you need tooprovide your own, prepare hello certificates and copy tooa local directory if you wish toocustomize hello certificates (passed toohello installation script).</span></span> <span data-ttu-id="ff4a6-125">Требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="ff4a6-125">You need hello following:</span></span>

    <span data-ttu-id="ff4a6-126">а.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-126">a.</span></span> <span data-ttu-id="ff4a6-127">Сертификатом с подстановочными символами для *.dbadapter. \<область\>.\< полного доменного имени\>.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-127">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="ff4a6-128">Этот сертификат должен быть доверенным, такие как будет выдан центром сертификации (то есть hello цепочка доверия должен существовать без промежуточных сертификатов.) (Можно использовать сертификат один сайт с именем виртуальной Машины явную hello, предоставленные во время установки.)</span><span class="sxs-lookup"><span data-stu-id="ff4a6-128">This certificate must be trusted, such as would be issued by a certificate authority (that is, hello chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with hello explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="ff4a6-129">b.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-129">b.</span></span> <span data-ttu-id="ff4a6-130">Hello корневой сертификат, используемый hello Azure Resource Manager для конкретного экземпляра Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-130">hello root certificate used by hello Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="ff4a6-131">Если он не найден, извлекается hello корневой сертификат.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-131">If it is not found, hello root certificate will be retrieved.</span></span>

5. <span data-ttu-id="ff4a6-132">Откройте **новый** повышенными PowerShell консоли и измените toohello каталог, где были извлечены файлы hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-132">Open a **new** elevated PowerShell console and change toohello directory where you extracted hello files.</span></span> <span data-ttu-id="ff4a6-133">Используйте новые проблемы tooavoid окна, которые могут быть вызваны неверные модули PowerShell, которые уже загружены в системе hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-133">Use a new window tooavoid problems that may arise from incorrect PowerShell modules already loaded on hello system.</span></span>

6. <span data-ttu-id="ff4a6-134">После установки любой версии hello AzureRm или модули AzureStack PowerShell 1.2.9 или 1.2.10 будет запрашиваемые tooremove их или hello установка не продолжится.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-134">If you have installed any versions of hello AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted tooremove them or hello install will not proceed.</span></span> <span data-ttu-id="ff4a6-135">Сюда входят версии 1.3 или выше.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-135">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="ff4a6-136">Запустите DeployMySqlProvider.ps1.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-136">Run DeployMySqlProvider.ps1.</span></span>

<span data-ttu-id="ff4a6-137">Этот скрипт выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-137">This script performs these steps:</span></span>

* <span data-ttu-id="ff4a6-138">При необходимости, загрузите совместимую версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-138">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="ff4a6-139">Загрузите hello MySQL соединителя двоичный (это может быть предоставлен вне сети).</span><span class="sxs-lookup"><span data-stu-id="ff4a6-139">Download hello MySQL connector binary (this can be provided offline).</span></span>
* <span data-ttu-id="ff4a6-140">Отправьте сертификат hello и все другие артефакты tooan учетной записи хранилища Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-140">Upload hello certificate and all other artifacts tooan Azure Stack storage account.</span></span>
* <span data-ttu-id="ff4a6-141">Опубликуйте пакеты коллекции, чтобы выполнить развертывание баз данных MySQL с помощью коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-141">Publish gallery packages so that you can deploy MySQL databases through hello gallery.</span></span>
* <span data-ttu-id="ff4a6-142">Развертывание виртуальной машины (VM), на котором размещена поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-142">Deploy a virtual machine (VM) that hosts your resource provider.</span></span>
* <span data-ttu-id="ff4a6-143">Зарегистрируйте локальный DNS-запись сопоставляет tooyour поставщика ресурсов виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-143">Register a local DNS record that maps tooyour resource provider VM.</span></span>
* <span data-ttu-id="ff4a6-144">Регистрация поставщика ресурсов с hello локального диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-144">Register your resource provider with hello local Azure Resource Manager.</span></span>

<span data-ttu-id="ff4a6-145">Либо укажите хотя бы hello обязательных параметров в командной строке hello, так и в, если выполняется без параметров, запрашиваемые tooenter их.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-145">Either specify at least hello required parameters on hello command line, or, if you run without any parameters, you are prompted tooenter them.</span></span> 

<span data-ttu-id="ff4a6-146">Ниже приведен пример, можно запустить из hello PowerShell запрашивать (но при необходимости изменить конечные точки сведения и портала учетной записи hello):</span><span class="sxs-lookup"><span data-stu-id="ff4a6-146">Here's an example you can run from hello PowerShell prompt (but change hello account information and portal endpoints as needed):</span></span>


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
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a><span data-ttu-id="ff4a6-147">Параметры DeployMySqlProvider.ps1</span><span class="sxs-lookup"><span data-stu-id="ff4a6-147">DeployMySqlProvider.ps1 parameters</span></span>

<span data-ttu-id="ff4a6-148">Эти параметры можно указать в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-148">You can specify these parameters in hello command line.</span></span> <span data-ttu-id="ff4a6-149">Если этого не сделать, или происходит сбой проверки параметров, будет предложено tooprovide hello необходимые объекты.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-149">If you do not, or any parameter validation fails, you are prompted tooprovide hello required ones.</span></span>

| <span data-ttu-id="ff4a6-150">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="ff4a6-150">Parameter Name</span></span> | <span data-ttu-id="ff4a6-151">Описание</span><span class="sxs-lookup"><span data-stu-id="ff4a6-151">Description</span></span> | <span data-ttu-id="ff4a6-152">Комментарий или значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ff4a6-152">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ff4a6-153">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-153">**DirectoryTenantID**</span></span> | <span data-ttu-id="ff4a6-154">Hello Azure или каталог служб федерации Active Directory с Идентификатором (guid)</span><span class="sxs-lookup"><span data-stu-id="ff4a6-154">hello Azure or ADFS Directory ID (guid)</span></span> | <span data-ttu-id="ff4a6-155">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="ff4a6-155">_required_</span></span> |
| <span data-ttu-id="ff4a6-156">**ArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-156">**ArmEndpoint**</span></span> | <span data-ttu-id="ff4a6-157">Hello Azure стека администратора Azure конечную точку диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="ff4a6-157">hello Azure Stack Administrative Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="ff4a6-158">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="ff4a6-158">_required_</span></span> |
| <span data-ttu-id="ff4a6-159">**TenantArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-159">**TenantArmEndpoint**</span></span> | <span data-ttu-id="ff4a6-160">Hello Azure стек Azure Resource Manager конечной точки клиента</span><span class="sxs-lookup"><span data-stu-id="ff4a6-160">hello Azure Stack Tenant Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="ff4a6-161">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="ff4a6-161">_required_</span></span> |
| <span data-ttu-id="ff4a6-162">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-162">**AzCredential**</span></span> | <span data-ttu-id="ff4a6-163">Azure учетных данных учетной записи администратора службы стека (hello используйте учетную запись как предназначенная для развертывания Azure стека)</span><span class="sxs-lookup"><span data-stu-id="ff4a6-163">Azure Stack Service Admin account credential (use hello same account as you used for deploying Azure Stack)</span></span> | <span data-ttu-id="ff4a6-164">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="ff4a6-164">_required_</span></span> |
| <span data-ttu-id="ff4a6-165">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-165">**VMLocalCredential**</span></span> | <span data-ttu-id="ff4a6-166">Hello учетной записи локального администратора поставщика ресурсов MySQL hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="ff4a6-166">hello local administrator account of hello MySQL resource provider VM</span></span> | <span data-ttu-id="ff4a6-167">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="ff4a6-167">_required_</span></span> |
| <span data-ttu-id="ff4a6-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-168">**ResourceGroupName**</span></span> | <span data-ttu-id="ff4a6-169">Группа ресурсов для элементов hello, созданный этим сценарием</span><span class="sxs-lookup"><span data-stu-id="ff4a6-169">Resource Group for hello items created by this script</span></span> |  <span data-ttu-id="ff4a6-170">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="ff4a6-170">_required_</span></span> |
| <span data-ttu-id="ff4a6-171">**VmName**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-171">**VmName**</span></span> | <span data-ttu-id="ff4a6-172">Имя виртуальной Машины вместимость hello hello поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="ff4a6-172">Name of hello VM holding hello resource provider</span></span> |  <span data-ttu-id="ff4a6-173">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="ff4a6-173">_required_</span></span> |
| <span data-ttu-id="ff4a6-174">**AcceptLicense**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-174">**AcceptLicense**</span></span> | <span data-ttu-id="ff4a6-175">Пропускает запрос tooaccept hello hello лицензии GPL (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span><span class="sxs-lookup"><span data-stu-id="ff4a6-175">Skips hello prompt tooaccept hello GPL License  (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span></span> | |
| <span data-ttu-id="ff4a6-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="ff4a6-177">Путь tooa локальной общей папкой, содержащий [mysql соединитель net 6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span><span class="sxs-lookup"><span data-stu-id="ff4a6-177">Path tooa local share containing [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span></span> <span data-ttu-id="ff4a6-178">Если указать их в этот каталог также должны находиться файлы сертификатов.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-178">If you provide them, certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="ff4a6-179">_необязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="ff4a6-179">_optional_</span></span> |
| <span data-ttu-id="ff4a6-180">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-180">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="ff4a6-181">Hello пароль для PFX-файл сертификата hello</span><span class="sxs-lookup"><span data-stu-id="ff4a6-181">hello password for hello .pfx certificate</span></span> | <span data-ttu-id="ff4a6-182">_обязательный параметр_</span><span class="sxs-lookup"><span data-stu-id="ff4a6-182">_required_</span></span> |
| <span data-ttu-id="ff4a6-183">**Значение параметра MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-183">**MaxRetryCount**</span></span> | <span data-ttu-id="ff4a6-184">Каждая операция повторяется, если происходит сбой</span><span class="sxs-lookup"><span data-stu-id="ff4a6-184">Each operation is retried if there is a failure</span></span> | <span data-ttu-id="ff4a6-185">2</span><span class="sxs-lookup"><span data-stu-id="ff4a6-185">2</span></span> |
| <span data-ttu-id="ff4a6-186">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-186">**RetryDuration**</span></span> | <span data-ttu-id="ff4a6-187">Время ожидания между повторными попытками в секундах</span><span class="sxs-lookup"><span data-stu-id="ff4a6-187">Timeout between retries, in seconds</span></span> | <span data-ttu-id="ff4a6-188">120</span><span class="sxs-lookup"><span data-stu-id="ff4a6-188">120</span></span> |
| <span data-ttu-id="ff4a6-189">**Удаление**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-189">**Uninstall**</span></span> | <span data-ttu-id="ff4a6-190">Удалить поставщик ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="ff4a6-190">Remove hello resource provider</span></span> | <span data-ttu-id="ff4a6-191">Нет</span><span class="sxs-lookup"><span data-stu-id="ff4a6-191">No</span></span> |
| <span data-ttu-id="ff4a6-192">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="ff4a6-192">**DebugMode**</span></span> | <span data-ttu-id="ff4a6-193">Предотвращает автоматическую очистку в случае ошибки</span><span class="sxs-lookup"><span data-stu-id="ff4a6-193">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="ff4a6-194">Нет</span><span class="sxs-lookup"><span data-stu-id="ff4a6-194">No</span></span> |


<span data-ttu-id="ff4a6-195">В зависимости от скорости производительности и загрузки системы hello установка может занять всего 20 минут или долго как несколько часов.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-195">Depending on hello system performance and download speeds, installation may take as little as 20 minutes or as long as several hours.</span></span> <span data-ttu-id="ff4a6-196">Если колонке MySQLAdapter hello не доступен, необходимо обновить портал администрирования hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-196">You must refresh hello admin portal if hello MySQLAdapter blade is not available.</span></span>

> [!NOTE]
> <span data-ttu-id="ff4a6-197">Если установка hello занимает более 90 минут, может произойти сбой и появится сообщение об ошибке на экране приветствия и в файле журнала hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-197">If hello installation takes more than 90 minutes, it may fail and you will see a failure message on hello screen and in hello log file.</span></span> <span data-ttu-id="ff4a6-198">из hello сбой шаг развертывания Hello будет предпринята повторная попытка.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-198">hello deployment is retried from hello failing step.</span></span> <span data-ttu-id="ff4a6-199">Систем, которые не соответствуют hello Рекомендуемый объем памяти и основных характеристик может оказаться может toodeploy hello MySQL RP.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-199">Systems that do not meet hello recommended memory and core specifications may not be able toodeploy hello MySQL RP.</span></span>


## <a name="provide-capacity-by-connecting-tooa-mysql-hosting-server"></a><span data-ttu-id="ff4a6-200">Предоставляют емкость, подключив tooa сервер размещения MySQL</span><span class="sxs-lookup"><span data-stu-id="ff4a6-200">Provide capacity by connecting tooa MySQL hosting server</span></span>

1. <span data-ttu-id="ff4a6-201">Войдите в toohello портала Azure стека администратором службы.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-201">Sign in toohello Azure Stack portal as a service admin.</span></span>

2. <span data-ttu-id="ff4a6-202">Нажмите кнопку **поставщиков ресурсов** &gt; **MySQLAdapter** &gt; **серверы размещения** &gt; **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-202">Click **Resource Providers** &gt; **MySQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="ff4a6-203">Hello **серверы размещения MySQL** колонка находится где могут подключаться hello поставщик ресурсов MySQL Server tooactual экземпляры MySQL Server, выступающие в качестве hello серверной части поставщик ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-203">hello **MySQL Hosting Servers** blade is where you can connect hello MySQL Server Resource Provider tooactual instances of MySQL Server that serve as hello resource provider’s backend.</span></span>

    ![Серверы размещения](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. <span data-ttu-id="ff4a6-205">Заполнение формы hello hello сведения о подключении экземпляра сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-205">Fill hello form with hello connection details of your MySQL Server instance.</span></span> <span data-ttu-id="ff4a6-206">Укажите hello полное доменное имя (FQDN) или допустимый IPv4-адрес и не hello короткое имя виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-206">Provide hello fully qualified domain name (FQDN) or a valid IPv4 address, and not hello short VM name.</span></span> <span data-ttu-id="ff4a6-207">Данная установка больше не содержит экземпляр MySQL по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-207">This installation no longer provides a default MySQL instance.</span></span> <span data-ttu-id="ff4a6-208">Здравствуйте, размеры помогает поставщика ресурсов hello управление емкостью hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-208">hello size provided helps hello resource provider manage hello database capacity.</span></span> <span data-ttu-id="ff4a6-209">Его необходимо закрыть toohello физический объем hello сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-209">It should be close toohello physical capacity of hello database server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ff4a6-210">При условии, что экземпляр MySQL hello может осуществляться hello клиента и администратора диспетчера ресурсов Azure, можно поместить в группе управления hello поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-210">As long as hello MySQL instance can be accessed by hello tenant and admin Azure Resource Manager, it can be placed under control of hello resource provider.</span></span> <span data-ttu-id="ff4a6-211">экземпляр MySQL Hello __должен__ выделить исключительно toohello RP.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-211">hello MySQL instance __must__ be allocated exclusively toohello RP.</span></span>

4. <span data-ttu-id="ff4a6-212">При добавлении серверов, необходимо назначить их tooa новый или существующий SKU tooallow дифференцированных предложений услуг.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-212">As you add servers, you must assign them tooa new or existing SKU tooallow differentiation of service offerings.</span></span> <span data-ttu-id="ff4a6-213">Например может иметь установленный экземпляр enterprise, предоставляя объем базы данных и автоматическое резервное копирование, зарезервировать высокопроизводительных серверов для каждого конкретного отдела, т. д. имя SKU hello должны отражать hello свойства, чтобы клиентов можно размещать свои базы данных соответствующим образом и должны иметь все серверы размещения в номере SKU hello те же возможности.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-213">For example, you could have an enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. hello SKU name should reflect hello properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have hello same capabilities.</span></span>

    ![Создание MySQL SKU](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
<span data-ttu-id="ff4a6-215">Номера SKU может занять toobe час tooan видны на портале hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-215">SKUs can take up tooan hour toobe visible in hello portal.</span></span> <span data-ttu-id="ff4a6-216">Невозможно создать базу данных до создания SKU hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-216">You cannot create a database until hello SKU is created.</span></span>


## <a name="create-your-first-mysql-database-tootest-your-deployment"></a><span data-ttu-id="ff4a6-217">Создайте развертывание вашего первого tootest базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="ff4a6-217">Create your first MySQL database tootest your deployment</span></span>


1. <span data-ttu-id="ff4a6-218">Войдите в toohello портала Azure стека учетной записью администратора службы.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-218">Sign in toohello Azure Stack portal as service admin.</span></span>

2. <span data-ttu-id="ff4a6-219">Нажмите кнопку hello **+ создать** кнопку &gt; **данные + хранилище** &gt; **базы данных MySQL (Предварительная версия)**.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-219">Click hello **+ New** button &gt; **Data + Storage** &gt; **MySQL Database (preview)**.</span></span>

3. <span data-ttu-id="ff4a6-220">Заполните форму hello с hello сведения о базе данных.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-220">Fill in hello form with hello database details.</span></span>

    ![Создание теста базы данных MySQL](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. <span data-ttu-id="ff4a6-222">Выберите SKU.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-222">Select a SKU.</span></span>

    ![Выберите SKU](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. <span data-ttu-id="ff4a6-224">Создание параметра имени входа.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-224">Create a login setting.</span></span> <span data-ttu-id="ff4a6-225">можно повторно использовать имя входа приветствия или создать новую публикацию.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-225">hello login setting can be reused or a new one created.</span></span> <span data-ttu-id="ff4a6-226">Оно содержит hello имя пользователя и пароль для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-226">This contains hello user name and password for hello database.</span></span>

    ![Создать новое имя входа базы данных](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    <span data-ttu-id="ff4a6-228">Строка подключения Hello включает имя сервера hello реальной базы данных.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-228">hello connections string includes hello real database server name.</span></span> <span data-ttu-id="ff4a6-229">Скопируйте его с портала hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-229">Copy it from hello portal.</span></span>

    ![Получить строку hello подключения для базы данных MySQL hello](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> <span data-ttu-id="ff4a6-231">Длина Hello hello имена пользователей не может превышать 32 символов с MySQL 5.7 или 16 символов в более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-231">hello length of hello user names cannot exceed 32 characters with MySQL 5.7 or 16 characters in earlier editions.</span></span> <span data-ttu-id="ff4a6-232">Это ограничение реализаций MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-232">This is a limitation of hello MySQL implementations.</span></span>


## <a name="add-capacity"></a><span data-ttu-id="ff4a6-233">Добавить емкость</span><span class="sxs-lookup"><span data-stu-id="ff4a6-233">Add capacity</span></span>

<span data-ttu-id="ff4a6-234">Добавьте емкости путем добавления новых серверов MySQL в портале Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-234">Add capacity by adding additional MySQL servers in hello Azure Stack portal.</span></span> <span data-ttu-id="ff4a6-235">Toouse другой экземпляр MySQL, нажмите кнопку **поставщиков ресурсов** &gt; **MySQLAdapter** &gt; **серверы размещения MySQL** &gt; **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-235">If you wish toouse another instance of MySQL, click **Resource Providers** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; **+Add**.</span></span>


## <a name="making-mysql-databases-available-tootenants"></a><span data-ttu-id="ff4a6-236">Сделать доступной tootenants баз данных MySQL</span><span class="sxs-lookup"><span data-stu-id="ff4a6-236">Making MySQL databases available tootenants</span></span>
<span data-ttu-id="ff4a6-237">Создайте планы и предложения toomake баз данных MySQL, доступных для клиентов.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-237">Create plans and offers toomake MySQL databases available for tenants.</span></span> <span data-ttu-id="ff4a6-238">Добавление службы Microsoft.MySqlAdapter hello, добавьте квоты, и т. д.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-238">Add hello Microsoft.MySqlAdapter service, add a quota, etc.</span></span>

![Создание планов и предложения tooinclude баз данных](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-hello-mysql-adapter-resource-provider"></a><span data-ttu-id="ff4a6-240">Удаление hello поставщик ресурсов MySQL адаптера</span><span class="sxs-lookup"><span data-stu-id="ff4a6-240">Removing hello MySQL Adapter Resource Provider</span></span>

<span data-ttu-id="ff4a6-241">поставщик ресурсов tooremove hello, очень важно toofirst удалите все зависимости.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-241">tooremove hello resource provider, it is essential toofirst remove any dependencies.</span></span>

1. <span data-ttu-id="ff4a6-242">Убедитесь, что у вас есть hello исходного развертывания пакет, загруженный для этой версии hello поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-242">Ensure you have hello original deployment package that you downloaded for this version of hello Resource Provider.</span></span>

2. <span data-ttu-id="ff4a6-243">Все базы данных клиента, необходимо удалить из поставщика ресурсов hello (это не удалит данные hello).</span><span class="sxs-lookup"><span data-stu-id="ff4a6-243">All tenant databases must be deleted from hello resource provider (this will not delete hello data).</span></span> <span data-ttu-id="ff4a6-244">Это следует выполнять с сами клиенты hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-244">This should be performed by hello tenants themselves.</span></span>

3. <span data-ttu-id="ff4a6-245">Клиентам необходимо отменить регистрацию имен hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-245">Tenants must unregister from hello namespace.</span></span>

4. <span data-ttu-id="ff4a6-246">Администратор должен удалить серверы из hello адаптера MySQL размещения hello</span><span class="sxs-lookup"><span data-stu-id="ff4a6-246">Administrator must delete hello hosting servers from hello MySQL Adapter</span></span>

5. <span data-ttu-id="ff4a6-247">Администратор должен удалить все планы, ссылающиеся на hello адаптера MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-247">Administrator must delete any plans that reference hello MySQL Adapter.</span></span>

6. <span data-ttu-id="ff4a6-248">Администратор должен удалить любой связанный toohello квот MySQL адаптера.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-248">Administrator must delete any quotas associated toohello MySQL Adapter.</span></span>

7. <span data-ttu-id="ff4a6-249">Снова запустите скрипт развертывания hello с hello - удалить параметр, конечные точки диспетчера ресурсов Azure, DirectoryTenantID и учетные данные для учетной записи администратора службы hello.</span><span class="sxs-lookup"><span data-stu-id="ff4a6-249">Rerun hello deployment script with hello -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for hello service administrator account.</span></span>




## <a name="next-steps"></a><span data-ttu-id="ff4a6-250">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff4a6-250">Next steps</span></span>


<span data-ttu-id="ff4a6-251">Попробуйте другой [служб PaaS](azure-stack-tools-paas-services.md) как hello [поставщик ресурсов SQL Server](azure-stack-sql-resource-provider-deploy.md) и hello [поставщик ресурсов службы приложений](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff4a6-251">Try other [PaaS services](azure-stack-tools-paas-services.md) like hello [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and hello [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
