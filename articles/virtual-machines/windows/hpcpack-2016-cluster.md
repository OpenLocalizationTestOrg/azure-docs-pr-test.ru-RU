---
title: "aaaHPC 2016 пакет кластера в Azure | Документы Microsoft"
description: "Узнайте, как кластер toodeploy 2016 пакета HPC в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="026bb-103">Развертывание кластера пакета HPC 2016 в Azure</span><span class="sxs-lookup"><span data-stu-id="026bb-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="026bb-104">Выполните действия hello в этой статье toodeploy [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) кластера на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="026bb-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="026bb-105">Пакет HPC — это бесплатное решение Майкрософт для высокопроизводительных вычислений, созданное на основе технологий Microsoft Azure и Windows Server, которое поддерживает широкий диапазон рабочих нагрузок высокопроизводительных вычислительных систем.</span><span class="sxs-lookup"><span data-stu-id="026bb-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="026bb-106">Используйте один из hello [шаблоны Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy кластера HPC Pack 2016 hello.</span><span class="sxs-lookup"><span data-stu-id="026bb-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="026bb-107">Есть несколько вариантов топологии кластера с разным числом головных узлов кластера и с вычислительными узлами на основе Linux или Windows.</span><span class="sxs-lookup"><span data-stu-id="026bb-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="026bb-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="026bb-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="026bb-109">Сертификат PFX</span><span class="sxs-lookup"><span data-stu-id="026bb-109">PFX certificate</span></span>

<span data-ttu-id="026bb-110">Кластер Microsoft HPC Pack 2016 требует сообщение hello toosecure сертификата обмена личной информацией (PFX) между узлы HPC hello.</span><span class="sxs-lookup"><span data-stu-id="026bb-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="026bb-111">Hello сертификат должен удовлетворять hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="026bb-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="026bb-112">Он должен иметь закрытый ключ, поддерживающий обмен ключами.</span><span class="sxs-lookup"><span data-stu-id="026bb-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="026bb-113">Для ключей используются цифровая подпись и шифрование.</span><span class="sxs-lookup"><span data-stu-id="026bb-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="026bb-114">Расширенное использование ключей включает в себя аутентификацию клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="026bb-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="026bb-115">Если у вас еще нет сертификата, соответствующий требованиям, можно запросить hello сертификата из центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="026bb-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="026bb-116">Кроме того можно использовать следующие команды toogenerate hello самозаверяющий сертификат на основе hello операционной системы, на котором вы выполните команду hello и экспортировать сертификат в формате PFX hello закрытым ключом hello.</span><span class="sxs-lookup"><span data-stu-id="026bb-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="026bb-117">**Для Windows 10 или Windows Server 2016**, запустите встроенный hello **New-SelfSignedCertificate** командлета PowerShell следующим образом:</span><span class="sxs-lookup"><span data-stu-id="026bb-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="026bb-118">**Для операционных систем более ранних, чем Windows 10 или Windows Server 2016**, загрузите hello [генератор самозаверяющий сертификат](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) из центра сценариев Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="026bb-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="026bb-119">Извлеките его содержимое и выполните следующие команды в командной строке PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="026bb-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="026bb-120">Отправка сертификата tooan хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="026bb-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="026bb-121">Перед развертыванием кластера HPC hello, отправьте сертификат tooan hello [хранилища ключей Azure](../../key-vault/index.md) как hello секретным и записи, следующую информацию для использования во время развертывания hello: **имя хранилища**,  **Группа ресурсов хранилища**, **URL-адрес сертификата**, и **отпечаток сертификата**.</span><span class="sxs-lookup"><span data-stu-id="026bb-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="026bb-122">Использует сертификат образец tooupload сценария PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="026bb-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="026bb-123">Дополнительные сведения об отправке сертификата tooan хранилища ключей Azure см. в разделе [приступить к работе с хранилищем ключей Azure](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="026bb-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="026bb-124">Поддерживаемые топологии</span><span class="sxs-lookup"><span data-stu-id="026bb-124">Supported topologies</span></span>

<span data-ttu-id="026bb-125">Выберите один из hello [шаблоны Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy кластера HPC Pack 2016 hello.</span><span class="sxs-lookup"><span data-stu-id="026bb-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="026bb-126">Ниже в общих чертах описана архитектура трех поддерживаемых топологий кластеров.</span><span class="sxs-lookup"><span data-stu-id="026bb-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="026bb-127">Топологии с высоким уровнем доступности содержат несколько головных узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="026bb-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="026bb-128">Высокодоступный кластер с доменом Active Directory</span><span class="sxs-lookup"><span data-stu-id="026bb-128">High-availability cluster with Active Directory domain</span></span>

    ![Высокодоступный кластер в домене AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="026bb-130">Высокодоступный кластер без домена Active Directory</span><span class="sxs-lookup"><span data-stu-id="026bb-130">High-availability cluster without Active Directory domain</span></span>

    ![Высокодоступный кластер без домена AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="026bb-132">Кластер с одним головным узлом</span><span class="sxs-lookup"><span data-stu-id="026bb-132">Cluster with a single head node</span></span>

   ![Кластер с одним головным узлом](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="026bb-134">Развертывание кластера</span><span class="sxs-lookup"><span data-stu-id="026bb-134">Deploy a cluster</span></span>

<span data-ttu-id="026bb-135">toocreate hello кластера, выберите шаблон и нажмите кнопку **развертывание tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="026bb-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="026bb-136">В hello [портал Azure](https://portal.azure.com), укажите параметры для шаблона hello, как описано в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="026bb-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="026bb-137">Каждый шаблон создает все ресурсы Azure, необходимые для hello инфраструктура кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="026bb-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="026bb-138">Эти ресурсы включают в себя виртуальную сеть Azure, общедоступный IP-адрес, балансировщик нагрузки (только для высокодоступного кластера), сетевые интерфейсы, группы доступности, учетные записи хранения и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="026bb-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="026bb-139">Шаг 1: Выбор подписки hello, расположение и группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="026bb-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="026bb-140">Hello **подписки** и hello **расположение** должна быть одинаковой указано, когда загруженный сертификат PFX-ФАЙЛ (см. предварительные условия).</span><span class="sxs-lookup"><span data-stu-id="026bb-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="026bb-141">Мы рекомендуем создать **группы ресурсов** hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="026bb-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="026bb-142">Шаг 2: Укажите значения параметров hello</span><span class="sxs-lookup"><span data-stu-id="026bb-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="026bb-143">Введите или измените значения для параметров шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="026bb-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="026bb-144">Щелкните параметр значок Далее hello tooeach справочных сведений.</span><span class="sxs-lookup"><span data-stu-id="026bb-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="026bb-145">Также см. руководство hello по [доступных размеров ВМ](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="026bb-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="026bb-146">Укажите значения hello, записанные в hello необходимые условия для hello следующие параметры: **имя хранилища**, **группа ресурсов хранилища**, **URL-адрес сертификата**и **Отпечаток сертификата**.</span><span class="sxs-lookup"><span data-stu-id="026bb-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="026bb-147">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="026bb-147">Step 3.</span></span> <span data-ttu-id="026bb-148">Просмотр юридических условий и создание</span><span class="sxs-lookup"><span data-stu-id="026bb-148">Review legal terms and create</span></span>
<span data-ttu-id="026bb-149">Нажмите кнопку **просмотрите условия** tooreview hello условия.</span><span class="sxs-lookup"><span data-stu-id="026bb-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="026bb-150">Если вы согласны, нажмите кнопку **покупки**, а затем нажмите кнопку **создать** toostart hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="026bb-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="026bb-151">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="026bb-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="026bb-152">После развертывания кластера HPC Pack hello go toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="026bb-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="026bb-153">Нажмите кнопку **групп ресурсов**и в какой hello кластера была развернута группа ресурсов hello поиска.</span><span class="sxs-lookup"><span data-stu-id="026bb-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="026bb-154">Можно найти hello головной узел виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="026bb-154">You can find hello head node virtual machines.</span></span>

    ![Головного узла кластера на портале hello](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="026bb-156">Щелкните один головной узел (в кластере высокой доступности, щелкните любой из головного узла hello).</span><span class="sxs-lookup"><span data-stu-id="026bb-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="026bb-157">В **Essentials**, можно найти hello общедоступный IP-адрес или полное DNS-имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="026bb-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![Параметры подключения кластера](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="026bb-159">Нажмите кнопку **Connect** toolog на tooany hello головного узлов, с помощью удаленного рабочего стола с вашим именем пользователя администратора указанного.</span><span class="sxs-lookup"><span data-stu-id="026bb-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="026bb-160">При развертывании кластера hello в домене Active Directory, имя пользователя hello имеет вид hello <privateDomainName> \<adminUsername > (например, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="026bb-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="026bb-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="026bb-161">Next steps</span></span>
* <span data-ttu-id="026bb-162">Отправка задания tooyour кластера.</span><span class="sxs-lookup"><span data-stu-id="026bb-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="026bb-163">В разделе [отправки заданий tooHPC кластере HPC Pack в Azure](hpcpack-cluster-submit-jobs.md) и [управление кластер HPC Pack 2016 в Azure с помощью Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="026bb-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

