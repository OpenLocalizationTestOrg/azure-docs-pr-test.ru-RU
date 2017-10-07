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
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a>Установить и настроить для использования со стеком Azure CLI

В этом документе мы выполнения процесса hello использования ресурсов Azure стека Development Kit toomanage Azure интерфейс командной строки (CLI) из клиентских платформ Mac и Linux. 

## <a name="export-hello-azure-stack-ca-root-certificate"></a>Экспортируйте сертификат корневого ЦС стек Azure hello

При использовании CLI из виртуальной машины, на котором выполняется в среде Azure стека Development Kit hello hello Azure стека корневой сертификат уже установлены hello виртуальной машине, можно получить непосредственно. А если используется CLI с рабочей станции за пределами пакета средств разработки hello, необходимо экспортировать сертификат корневого ЦС стек Azure hello из пакета средств разработки hello и добавить его хранилище рабочей станции разработки (внешние Mac или Linux платформы сертификатов toohello Python ). 

Войдите в пакет средств разработки tooyour и запустите следующий сценарий tooexport hello Azure стека корневой сертификат в формате PEM hello.

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

## <a name="install-cli"></a>Установка CLI

Далее необходимо войти на рабочей станции разработки tooyour и установить CLI. Стек Azure требуется версия hello 2.0 Azure CLI, который можно установить с помощью hello действия, описанные в hello [установить CLI Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) статьи. tooverify Если hello установка прошла успешно, откройте терминала или окно командной строки и выполнения hello следующую команду:

```azurecli
az --version
```

Вы увидите версия hello Azure CLI и другие зависимые библиотеки, которые установлены на компьютере.

## <a name="trust-hello-azure-stack-ca-root-certificate"></a>Доверять сертификату корневого ЦС стек Azure hello

tootrust Здравствуйте корневой сертификат ЦС Azure стека, можно добавить toohello существующего сертификата python. При выполнении CLI из компьютере Linux, который создается в среде Azure стека hello следующие выполнения hello bash команды:

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

При выполнении CLI из машины вне среды Azure Sack hello, необходимо сначала настроить [tooAzure подключения VPN стека](azure-stack-connect-azure-stack.md). Теперь скопируйте ранее экспортированный на рабочей станции разработки сертификат PEM hello и выполните следующие команды в зависимости от операционной системы рабочей станции разработки, hello:

### <a name="linux"></a>Linux

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="macos"></a>macOS

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="windows"></a>Windows

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

## <a name="set-up-hello-virtual-machine-aliases-endpoint"></a>Настройка конечной точки псевдонимы hello виртуальной машины

До пользователи могут создавать виртуальные машины с помощью CLI, облака Здравствуйте, администратор должен настроен общедоступный конечной точки, в которой содержится псевдонимы образ виртуальной машины и зарегистрировать эту конечную точку с облаком hello. Hello `endpoint-vm-image-alias-doc` параметр в hello `az cloud register` команда используется для этой цели. Администраторов облака необходимо загрузить hello изображения toohello стека Azure marketplace, перед их добавлением конечной точки tooimage псевдонимы.
   
Например, Azure содержит использует следующую URI: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json. Здравствуйте, администратор облака следует настроить конечную точку как для стека Azure с образами hello, доступных на рынке hello Azure стека.

## <a name="connect-tooazure-stack"></a>Подключение tooAzure стека

Используйте следующие шаги tooconnect tooAzure стека hello.

1. Зарегистрируйте среду Azure стек, выполнив команду register облака az hello.
   
   а. tooregister hello **администратора облака** среды, используйте:

   ```azurecli
   az cloud register \ 
     -n AzureStackAdmin \ 
     --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

   b. tooregister hello **пользователя** среды, используйте:

   ```azurecli
   az cloud register \ 
     -n AzureStackUser \ 
     --endpoint-resource-manager "https://management.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

2. Набор hello активной среды с помощью hello, следующие команды:

   а. Для hello **администратора облака** среды, используйте:

   ```azurecli
   az cloud set \
     -n AzureStackAdmin
   ```

   b. Для hello **пользователя** среды, используйте:

   ```azurecli
   az cloud set \
     -n AzureStackUser
   ```

3. Обновление конфигурации hello toouse стека Azure конкретного API версии профиля вашей среды. tooupdate hello, выполнения конфигурации hello следующую команду:

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. Войдите в среду Azure стека tooyour с использованием hello **входа az** команды. Вы можете войти в среду Azure стека toohello имени пользователя или как [участника-службы](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects). 

   * Войдите как **пользователя**: можно указать hello имя пользователя и пароль непосредственно в команду входа az hello или проверки подлинности с помощью браузера. Потребовалось бы toodo hello последнее, если у вас есть многофакторная проверка подлинности включена.

   ```azurecli
   az login \
     -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
   ```

   > [!NOTE]
   > Если ваша учетная запись пользователя имеет многофакторную проверку подлинности включена, команда hello az входа без указания параметра -u hello. Выполнение команды hello предоставляет URL-адрес и код, необходимо использовать tooauthenticate.
   
   * Войдите как **участника-службы**: перед входом, [Создание субъекта-службы через портал Azure hello](azure-stack-create-service-principals.md) или CLI и назначьте их роли. Теперь войдите с помощью hello следующую команду:

   ```azurecli
   az login \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
     --service-principal \
     -u <Application Id of hello Service Principal> \
     -p <Key generated for hello Service Principal>
   ```

## <a name="test-hello-connectivity"></a>Проверка подключения hello

Теперь, когда у нас есть все настройки, воспользуемся CLI toocreate ресурсов в Azure стека. Например можно создать группу ресурсов для приложения и добавить виртуальную машину. Hello используется следующая команда toocreate группу ресурсов с именем «MyResourceGroup»:

```azurecli
az group create \
  -n MyResourceGroup -l local
```

Если создана группа ресурсов hello hello предыдущая команда выводит hello следующие свойства созданного hello ресурса:

![Создание группы ресурсов выходных данных](media/azure-stack-connect-cli/image1.png)

Существуют некоторые известные проблемы при использовании CLI 2.0 в Azure стека, toolearn об этих проблемах см. в разделе hello [известные проблемы в Azure CLI стека](azure-stack-troubleshooting.md#cli) раздела. 

## <a name="next-steps"></a>Дальнейшие действия

[Развертывание шаблонов с помощью интерфейса командной строки Azure](azure-stack-deploy-template-command-line.md)

[Подключение с помощью PowerShell](azure-stack-connect-powershell.md)

[Управление разрешениями пользователей](azure-stack-manage-permissions.md)

