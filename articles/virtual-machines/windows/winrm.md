---
title: "aaaSet доступа для удаленного управления Windows для ВМ Azure | Документы Microsoft"
description: "Настройка WinRM доступ для использования с виртуальной машины Azure создаются в модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>Настройка доступа WinRM для виртуальных машин в Azure Resource Manager
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>WinRM в управлении службами Azure или Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* Общие сведения о hello диспетчера ресурсов Azure, см. в разделе это [статьи](../../azure-resource-manager/resource-group-overview.md)
* Сведения о различиях между управлением службами Azure и Azure Resource Manager см. в этой [статье](../../resource-manager-deployment-model.md).

Hello ключевое различие в настройке конфигурации WinRM между двумя стеками hello происходит сертификат hello возвращает Установка hello виртуальной Машины. В стеке диспетчера ресурсов Azure hello сертификаты hello моделируются как ресурсы, управляемые hello поставщика ресурсов хранилища ключей. Таким образом пользователь hello должен tooprovide свой собственный сертификат и отправить tooa хранилище ключей перед их использованием в виртуальной Машине.

Ниже приведены шаги hello необходимо tooset tootake ВМ с подключением удаленного управления Windows

1. создать хранилище ключей;
2. Создание самозаверяющего сертификата
3. Отправьте ваш tooKey самозаверяющий сертификат хранилища
4. Получение URL-адреса hello самозаверяющего сертификата в хранилище ключей hello
5. сослаться на URL-адрес самозаверяющего сертификата при создании виртуальной машины.

## <a name="step-1-create-a-key-vault"></a>Шаг 1. Создание хранилища ключей
Можно использовать hello ниже команда toocreate hello хранилища ключей

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>Шаг 2. Создание самозаверяющего сертификата
Можно создать самозаверяющий сертификат с помощью этого сценария PowerShell.

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>Шаг 3: Отправка вашей toohello самозаверяющий сертификат хранилища ключей
Перед созданием отправка сертификата hello toohello хранилища ключей на шаге 1, в формате hello, понимали, поставщик ресурсов Microsoft.Compute ему tooconverted. Разрешает Hello ниже сценарий PowerShell, необходимо

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>Шаг 4: Получение hello URL-адреса для самозаверяющего сертификата в хранилище ключей hello
Hello поставщике ресурсов Microsoft.Compute должен секрета toohello URL-адрес внутри hello хранилища ключей во время подготовки hello виртуальной Машины. Это позволяет hello Microsoft.Compute ресурсов поставщика toodownload hello секрета и создайте сертификат эквивалентные hello hello виртуальной Машины.

> [!NOTE]
> URL-адрес Hello hello секрет должен также версия hello tooinclude. Пример URL-адреса выглядит так: https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve
> 
> 

#### <a name="templates"></a>Шаблоны
URL-адрес toohello hello ссылки можно получить в шаблон hello, используя hello ниже код

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
Вы можете получить этот URL-адрес, используя hello ниже команды PowerShell

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>Шаг 5. Создание ссылки на URL-адрес самозаверяющего сертификата при создании виртуальной машины
#### <a name="azure-resource-manager-templates"></a>Шаблоны Azure Resource Manager
При создании ВМ с помощью шаблонов, сертификат hello возвращает ссылаться секреты hello и разделов winRM hello, как показано ниже:

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

Образец шаблона для hello выше приведены ниже в [201-vm-winrm-keyvault — windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

Исходный код для этого шаблона можно найти на портале [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>Шаг 6: Подключение toohello виртуальной Машины
Перед подключением toohello виртуальной Машины необходимо убедиться, что компьютер настроен для удаленного управления WinRM toomake. Запустите PowerShell с правами администратора и выполните hello ниже команда toomake том, что настройки нужных параметров.

    Enable-PSRemoting -Force

> [!NOTE]
> Может потребоваться toomake том, что hello служба WinRM работает в том случае, если выше hello не работает. Это можно сделать с помощью команды `Get-Service WinRM`
> 
> 

После завершения установки hello toohello ВМ можно подключиться с помощью hello ниже команды

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
