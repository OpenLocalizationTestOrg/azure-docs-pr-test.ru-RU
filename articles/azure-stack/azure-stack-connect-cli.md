---
title: "aaaConnect tooAzure стек с CLI | Документы Microsoft"
description: "Узнайте, как toouse hello toomanage межплатформенного интерфейса командной строки (CLI) и развертывания ресурсов в стек Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: ffb1ffd2b7784e188487bef98fe5b2add8e96784
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a><span data-ttu-id="9f00f-103">Установить и настроить для использования со стеком Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9f00f-103">Install and configure CLI for use with Azure Stack</span></span>

<span data-ttu-id="9f00f-104">В этом документе мы выполнения процесса hello использования ресурсов Azure стека Development Kit toomanage Azure интерфейс командной строки (CLI) из клиентских платформ Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="9f00f-104">In this document, we guide you through hello process of using Azure Command-line Interface (CLI) toomanage Azure Stack Development Kit resources from Linux and Mac client platforms.</span></span> 

## <a name="export-hello-azure-stack-ca-root-certificate"></a><span data-ttu-id="9f00f-105">Экспортируйте сертификат корневого ЦС стек Azure hello</span><span class="sxs-lookup"><span data-stu-id="9f00f-105">Export hello Azure Stack CA root certificate</span></span>

<span data-ttu-id="9f00f-106">При использовании CLI из виртуальной машины, на котором выполняется в среде Azure стека Development Kit hello hello Azure стека корневой сертификат уже установлены hello виртуальной машине, можно получить непосредственно.</span><span class="sxs-lookup"><span data-stu-id="9f00f-106">If you are using CLI from a virtual machine that is running within hello Azure Stack Development Kit environment, hello Azure Stack root certificate is already installed within hello virtual machine so you can directly retrieve.</span></span> <span data-ttu-id="9f00f-107">А если используется CLI с рабочей станции за пределами пакета средств разработки hello, необходимо экспортировать сертификат корневого ЦС стек Azure hello из пакета средств разработки hello и добавить его хранилище рабочей станции разработки (внешние Mac или Linux платформы сертификатов toohello Python ).</span><span class="sxs-lookup"><span data-stu-id="9f00f-107">Whereas if you are use CLI from a workstation outside hello development kit, you must export hello Azure Stack CA root certificate from hello development kit and add it toohello Python certificate store of your development workstation(external Linux or Mac platform).</span></span> 

<span data-ttu-id="9f00f-108">Войдите в пакет средств разработки tooyour и запустите следующий сценарий tooexport hello Azure стека корневой сертификат в формате PEM hello.</span><span class="sxs-lookup"><span data-stu-id="9f00f-108">Sign in tooyour development kit and run hello following script tooexport hello Azure Stack root certificate in PEM format:</span></span>

```powershell
   $label = "AzureStackSelfSignedRootCert"
   Write-Host "Getting certificate from hello current user trusted store with subject CN=$label"
   $root = Get-ChildItem Cert:\CurrentUser\Root | Where-Object Subject -eq "CN=$label" | select -First 1
   if (-not $root)
   {
       Log-Error "Cerficate with subject CN=$label not found"
       return
   }

   Write-Host "Exporting certificate"
   Export-Certificate -Type CERT -FilePath root.cer -Cert $root

   Write-Host "Converting certificate tooPEM format"
   certutil -encode root.cer root.pem
```

## <a name="install-cli"></a><span data-ttu-id="9f00f-109">Установка CLI</span><span class="sxs-lookup"><span data-stu-id="9f00f-109">Install CLI</span></span>

<span data-ttu-id="9f00f-110">Далее необходимо войти на рабочей станции разработки tooyour и установить CLI.</span><span class="sxs-lookup"><span data-stu-id="9f00f-110">Next you should sign in tooyour development workstation and install CLI.</span></span> <span data-ttu-id="9f00f-111">Стек Azure требуется версия hello 2.0 Azure CLI, который можно установить с помощью hello действия, описанные в hello [установить CLI Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) статьи.</span><span class="sxs-lookup"><span data-stu-id="9f00f-111">Azure Stack requires hello 2.0 version of Azure CLI, which you can install by using hello steps described in hello [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) article.</span></span> <span data-ttu-id="9f00f-112">tooverify Если hello установка прошла успешно, откройте терминала или окно командной строки и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9f00f-112">tooverify if hello installation was successful, open a terminal or a command prompt window and run hello following command:</span></span>

```azurecli
az --version
```

<span data-ttu-id="9f00f-113">Вы увидите версия hello Azure CLI и другие зависимые библиотеки, которые установлены на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9f00f-113">You should see hello version of Azure CLI and other dependent libraries that are installed on your computer.</span></span>

## <a name="trust-hello-azure-stack-ca-root-certificate"></a><span data-ttu-id="9f00f-114">Доверять сертификату корневого ЦС стек Azure hello</span><span class="sxs-lookup"><span data-stu-id="9f00f-114">Trust hello Azure Stack CA root certificate</span></span>

<span data-ttu-id="9f00f-115">tootrust Здравствуйте корневой сертификат ЦС Azure стека, можно добавить toohello существующего сертификата python.</span><span class="sxs-lookup"><span data-stu-id="9f00f-115">tootrust hello Azure Stack CA root certificate, you should append it toohello existing python certificate.</span></span> <span data-ttu-id="9f00f-116">При выполнении CLI из компьютере Linux, который создается в среде Azure стека hello следующие выполнения hello bash команды:</span><span class="sxs-lookup"><span data-stu-id="9f00f-116">If you are running CLI from a Linux machine that is created within hello Azure Stack environment, run hello following bash command:</span></span>

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

<span data-ttu-id="9f00f-117">При выполнении CLI из машины вне среды Azure Sack hello, необходимо сначала настроить [tooAzure подключения VPN стека](azure-stack-connect-azure-stack.md).</span><span class="sxs-lookup"><span data-stu-id="9f00f-117">If you are running CLI from a machine outside hello Azure Sack environment, you must first set up [VPN connectivity tooAzure Stack](azure-stack-connect-azure-stack.md).</span></span> <span data-ttu-id="9f00f-118">Теперь скопируйте ранее экспортированный на рабочей станции разработки сертификат PEM hello и выполните следующие команды в зависимости от операционной системы рабочей станции разработки, hello:</span><span class="sxs-lookup"><span data-stu-id="9f00f-118">Now copy hello PEM certificate that you exported earlier onto your development workstation and run hello following commands depending on your development workstation's OS,:</span></span>

### <a name="linux"></a><span data-ttu-id="9f00f-119">Linux</span><span class="sxs-lookup"><span data-stu-id="9f00f-119">Linux</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="macos"></a><span data-ttu-id="9f00f-120">macOS</span><span class="sxs-lookup"><span data-stu-id="9f00f-120">macOS</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="windows"></a><span data-ttu-id="9f00f-121">Windows</span><span class="sxs-lookup"><span data-stu-id="9f00f-121">Windows</span></span>

```powershell
$pemFile = "<Fully qualified path toohello PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from hello cert file"
$md5Hash=(Get-FileHash -Path $pemFile -Algorithm MD5).Hash.ToLower()
$sha1Hash=(Get-FileHash -Path $pemFile -Algorithm SHA1).Hash.ToLower()
$sha256Hash=(Get-FileHash -Path $pemFile -Algorithm SHA256).Hash.ToLower()

$issuerEntry = [string]::Format("# Issuer: {0}", $root.Issuer)
$subjectEntry = [string]::Format("# Subject: {0}", $root.Subject)
$labelEntry = [string]::Format("# Label: {0}", $root.Subject.Split('=')[-1])
$serialEntry = [string]::Format("# Serial: {0}", $root.GetSerialNumberString().ToLower())
$md5Entry = [string]::Format("# MD5 Fingerprint: {0}", $md5Hash)
$sha1Entry  = [string]::Format("# SHA1 Finterprint: {0}", $sha1Hash)
$sha256Entry = [string]::Format("# SHA256 Fingerprint: {0}", $sha256Hash)
$certText = (Get-Content -Path root.pem -Raw).ToString().Replace("`r`n","`n")

$rootCertEntry = "`n" + $issuerEntry + "`n" + $subjectEntry + "`n" + $labelEntry + "`n" + `
$serialEntry + "`n" + $md5Entry + "`n" + $sha1Entry + "`n" + $sha256Entry + "`n" + $certText

Write-Host "Adding hello certificate content tooPython Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing hello azure stack CA root certificate"
```

## <a name="set-up-hello-virtual-machine-aliases-endpoint"></a><span data-ttu-id="9f00f-122">Настройка конечной точки псевдонимы hello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9f00f-122">Set up hello virtual machine aliases endpoint</span></span>

<span data-ttu-id="9f00f-123">До пользователи могут создавать виртуальные машины с помощью CLI, облака Здравствуйте, администратор должен настроен общедоступный конечной точки, в которой содержится псевдонимы образ виртуальной машины и зарегистрировать эту конечную точку с облаком hello.</span><span class="sxs-lookup"><span data-stu-id="9f00f-123">Before users can create virtual machines by using CLI, hello cloud administrator should set up a publicly accessible endpoint that contains virtual machine image aliases and register this endpoint with hello cloud.</span></span> <span data-ttu-id="9f00f-124">Hello `endpoint-vm-image-alias-doc` параметр в hello `az cloud register` команда используется для этой цели.</span><span class="sxs-lookup"><span data-stu-id="9f00f-124">hello `endpoint-vm-image-alias-doc` parameter in hello `az cloud register` command is used for this purpose.</span></span> <span data-ttu-id="9f00f-125">Администраторов облака необходимо загрузить hello изображения toohello стека Azure marketplace, перед их добавлением конечной точки tooimage псевдонимы.</span><span class="sxs-lookup"><span data-stu-id="9f00f-125">Cloud administrators must download hello image toohello Azure Stack marketplace before they add it tooimage aliases endpoint.</span></span>
   
<span data-ttu-id="9f00f-126">Например, Azure содержит использует следующую URI: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json.</span><span class="sxs-lookup"><span data-stu-id="9f00f-126">For example, Azure contains uses following URI: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json.</span></span> <span data-ttu-id="9f00f-127">Здравствуйте, администратор облака следует настроить конечную точку как для стека Azure с образами hello, доступных на рынке hello Azure стека.</span><span class="sxs-lookup"><span data-stu-id="9f00f-127">hello cloud administrator should set up a similar endpoint for Azure Stack with hello images that are available in hello Azure Stack marketplace.</span></span>

## <a name="connect-tooazure-stack"></a><span data-ttu-id="9f00f-128">Подключение tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="9f00f-128">Connect tooAzure Stack</span></span>

<span data-ttu-id="9f00f-129">Используйте следующие шаги tooconnect tooAzure стека hello.</span><span class="sxs-lookup"><span data-stu-id="9f00f-129">Use hello following steps tooconnect tooAzure Stack:</span></span>

1. <span data-ttu-id="9f00f-130">Зарегистрируйте среду Azure стек, выполнив команду register облака az hello.</span><span class="sxs-lookup"><span data-stu-id="9f00f-130">Register your Azure Stack environment by running hello az cloud register command.</span></span>
   
   <span data-ttu-id="9f00f-131">а.</span><span class="sxs-lookup"><span data-stu-id="9f00f-131">a.</span></span> <span data-ttu-id="9f00f-132">tooregister hello **администратора облака** среды, используйте:</span><span class="sxs-lookup"><span data-stu-id="9f00f-132">tooregister hello **cloud administrative** environment, use:</span></span>

   ```azurecli
   az cloud register \ 
     -n AzureStackAdmin \ 
     --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

   <span data-ttu-id="9f00f-133">b.</span><span class="sxs-lookup"><span data-stu-id="9f00f-133">b.</span></span> <span data-ttu-id="9f00f-134">tooregister hello **пользователя** среды, используйте:</span><span class="sxs-lookup"><span data-stu-id="9f00f-134">tooregister hello **user** environment, use:</span></span>

   ```azurecli
   az cloud register \ 
     -n AzureStackUser \ 
     --endpoint-resource-manager "https://management.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

2. <span data-ttu-id="9f00f-135">Набор hello активной среды с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="9f00f-135">Set hello active environment by using hello following commands:</span></span>

   <span data-ttu-id="9f00f-136">а.</span><span class="sxs-lookup"><span data-stu-id="9f00f-136">a.</span></span> <span data-ttu-id="9f00f-137">Для hello **администратора облака** среды, используйте:</span><span class="sxs-lookup"><span data-stu-id="9f00f-137">For hello **cloud administrative** environment, use:</span></span>

   ```azurecli
   az cloud set \
     -n AzureStackAdmin
   ```

   <span data-ttu-id="9f00f-138">b.</span><span class="sxs-lookup"><span data-stu-id="9f00f-138">b.</span></span> <span data-ttu-id="9f00f-139">Для hello **пользователя** среды, используйте:</span><span class="sxs-lookup"><span data-stu-id="9f00f-139">For hello **user** environment, use:</span></span>

   ```azurecli
   az cloud set \
     -n AzureStackUser
   ```

3. <span data-ttu-id="9f00f-140">Обновление конфигурации hello toouse стека Azure конкретного API версии профиля вашей среды.</span><span class="sxs-lookup"><span data-stu-id="9f00f-140">Update your environment configuration toouse hello Azure Stack specific API version profile.</span></span> <span data-ttu-id="9f00f-141">tooupdate hello, выполнения конфигурации hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9f00f-141">tooupdate hello configuration, run hello following command:</span></span>

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. <span data-ttu-id="9f00f-142">Войдите в среду Azure стека tooyour с использованием hello **входа az** команды.</span><span class="sxs-lookup"><span data-stu-id="9f00f-142">Sign in tooyour Azure Stack environment by using hello **az login** command.</span></span> <span data-ttu-id="9f00f-143">Вы можете войти в среду Azure стека toohello имени пользователя или как [участника-службы](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects).</span><span class="sxs-lookup"><span data-stu-id="9f00f-143">You can sign in toohello Azure Stack environment either as a user or as a [service principal](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects).</span></span> 

   * <span data-ttu-id="9f00f-144">Войдите как **пользователя**: можно указать hello имя пользователя и пароль непосредственно в команду входа az hello или проверки подлинности с помощью браузера.</span><span class="sxs-lookup"><span data-stu-id="9f00f-144">Sign in as a **user**: You can either specify hello username and password directly within hello az login command or authenticate using a browser.</span></span> <span data-ttu-id="9f00f-145">Потребовалось бы toodo hello последнее, если у вас есть многофакторная проверка подлинности включена.</span><span class="sxs-lookup"><span data-stu-id="9f00f-145">You would have toodo hello latter, if your account has multi-factor authentication enabled.</span></span>

   ```azurecli
   az login \
     -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
   ```

   > [!NOTE]
   > <span data-ttu-id="9f00f-146">Если ваша учетная запись пользователя имеет многофакторную проверку подлинности включена, команда hello az входа без указания параметра -u hello.</span><span class="sxs-lookup"><span data-stu-id="9f00f-146">If your user account has Multi factor authentication enabled, you can use hello az login command without providing hello -u parameter.</span></span> <span data-ttu-id="9f00f-147">Выполнение команды hello предоставляет URL-адрес и код, необходимо использовать tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="9f00f-147">Running hello command gives you a URL and a code that you must use tooauthenticate.</span></span>
   
   * <span data-ttu-id="9f00f-148">Войдите как **участника-службы**: перед входом, [Создание субъекта-службы через портал Azure hello](azure-stack-create-service-principals.md) или CLI и назначьте их роли.</span><span class="sxs-lookup"><span data-stu-id="9f00f-148">Sign in as a **service principal**: Before you sign in, [Create a service principal through hello Azure portal](azure-stack-create-service-principals.md) or CLI and assign it a role.</span></span> <span data-ttu-id="9f00f-149">Теперь войдите с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9f00f-149">Now, log in by using hello following command:</span></span>

   ```azurecli
   az login \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
     --service-principal \
     -u <Application Id of hello Service Principal> \
     -p <Key generated for hello Service Principal>
   ```

## <a name="test-hello-connectivity"></a><span data-ttu-id="9f00f-150">Проверка подключения hello</span><span class="sxs-lookup"><span data-stu-id="9f00f-150">Test hello connectivity</span></span>

<span data-ttu-id="9f00f-151">Теперь, когда у нас есть все настройки, воспользуемся CLI toocreate ресурсов в Azure стека.</span><span class="sxs-lookup"><span data-stu-id="9f00f-151">Now that we've got everything setup, let's use CLI toocreate resources within Azure Stack.</span></span> <span data-ttu-id="9f00f-152">Например можно создать группу ресурсов для приложения и добавить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="9f00f-152">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="9f00f-153">Hello используется следующая команда toocreate группу ресурсов с именем «MyResourceGroup»:</span><span class="sxs-lookup"><span data-stu-id="9f00f-153">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```azurecli
az group create \
  -n MyResourceGroup -l local
```

<span data-ttu-id="9f00f-154">Если создана группа ресурсов hello hello предыдущая команда выводит hello следующие свойства созданного hello ресурса:</span><span class="sxs-lookup"><span data-stu-id="9f00f-154">If hello resource group is created successfully, hello previous command outputs hello following properties of hello newly created resource:</span></span>

![Создание группы ресурсов выходных данных](media/azure-stack-connect-cli/image1.png)

<span data-ttu-id="9f00f-156">Существуют некоторые известные проблемы при использовании CLI 2.0 в Azure стека, toolearn об этих проблемах см. в разделе hello [известные проблемы в Azure CLI стека](azure-stack-troubleshooting.md#cli) раздела.</span><span class="sxs-lookup"><span data-stu-id="9f00f-156">There are some known issues when using CLI 2.0 in Azure Stack, toolearn about these issues, see hello [Known issues in Azure Stack CLI](azure-stack-troubleshooting.md#cli) topic.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9f00f-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f00f-157">Next steps</span></span>

[<span data-ttu-id="9f00f-158">Развертывание шаблонов с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="9f00f-158">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="9f00f-159">Подключение с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f00f-159">Connect with PowerShell</span></span>](azure-stack-connect-powershell.md)

[<span data-ttu-id="9f00f-160">Управление разрешениями пользователей</span><span class="sxs-lookup"><span data-stu-id="9f00f-160">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

