---
title: "Разрешить приложениям получать секреты в хранилище ключей Azure стек | Документы Microsoft"
description: "Использование примера приложения для работы с хранилищем ключей Azure стека"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3748b719-e269-4b48-8d7d-d75a84b0e1e5
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2017
ms.author: sngun
ms.openlocfilehash: 7cfb78cc5219d4adab5ceddc9d7eb8d1fc71b678
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sample-application-that-uses-keys-and-secrets-stored-in-a-key-vault"></a>Пример приложения, использующего ключи и секретные данные, хранящиеся в хранилище ключей

В этой статье мы показано, как запустить образец приложения (HelloKeyVault), который получает ключи и секретные данные из хранилища ключей Azure стека.

## <a name="prerequisites"></a>Предварительные требования 

Выполнить следующие предварительные требования, либо из [Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).  
* Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md). 

## <a name="create-and-get-the-key-vault-and-application-settings"></a>Создание и хранилище ключей, а также параметры приложения

Во-первых необходимо создание хранилища ключей Azure стека и зарегистрировать приложение в Azure Active Directory (Azure AD). Можно создать и зарегистрировать в хранилищах ключей с помощью портала Azure или PowerShell. В этой статье показан способ PowerShell для выполнения задач. По умолчанию этот сценарий PowerShell создает новое приложение в Active Directory. Тем не менее вы можете воспользоваться одним из существующих приложений. Убедитесь в том предоставить значение для `aadTenantName` и `applicationPassword` переменных. Если не указать значение для `applicationPassword` переменной, этот скрипт создает случайный пароль. 

```powershell
$vaultName           = 'myVault'
$resourceGroupName   = 'myResourceGroup'
$applicationName     = 'myApp'
$location            = 'local' 

# Password for the application. If not specified, this script will generate a random password during app creation.
$applicationPassword = '' 
                         
# Function to generate a random password for the application.
Function GenerateSymmetricKey()
{
    $key = New-Object byte[](32)
    $rng = [System.Security.Cryptography.RNGCryptoServiceProvider]::Create()
    $rng.GetBytes($key)
    return [System.Convert]::ToBase64String($key)
}

Write-Host 'Please log into your Azure Stack user environment' -foregroundcolor Green

$tenantARM = "https://management.local.azurestack.external"
$aadTenantName = "PLEASE FILL THIS IN WITH YOUR AAD TENANT NAME. FOR EXAMPLE: myazurestack.onmicrosoft.com"

# Configure the Azure Stack operator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackUser" `
  -ArmEndpoint $tenantARM

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $aadTenantName `
  -EnvironmentName AzureStackUser

# Sign in to the user portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackUser" `
  -TenantId $TenantID `
  
$now = [System.DateTime]::Now
$oneYearFromNow = $now.AddYears(1)

$applicationPassword = GenerateSymmetricKey
    
# Create a new Azure AD application.
$identifierUri = [string]::Format("http://localhost:8080/{0}",[Guid]::NewGuid().ToString("N"))
$homePage = "http://contoso.com"

Write-Host "Creating a new AAD Application"
$ADApp = New-AzureRmADApplication `
  -DisplayName $applicationName `
  -HomePage $homePage `
  -IdentifierUris $identifierUri `
  -StartDate $now `
  -EndDate $oneYearFromNow `
  -Password $applicationPassword

Write-Host "Creating a new AAD service principal"
$servicePrincipal = New-AzureRmADServicePrincipal `
  -ApplicationId $ADApp.ApplicationId

# Create a new resource group and a key vault within that resource group.
New-AzureRmResourceGroup `
  -Name $resourceGroupName `
  -Location $location   

Write-Host "Creating vault $vaultName"
$vault = New-AzureRmKeyVault -VaultName $vaultName `
  -ResourceGroupName $resourceGroupName `
  -Sku standard `
  -Location $location

# Specify full privileges to the vault for the application.
Write-Host "Setting access policy"
Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName `
  -ObjectId $servicePrincipal.Id `
  -PermissionsToKeys all `
  -PermissionsToSecrets all

Write-Host "Paste the following settings into the app.config file for the HelloKeyVault project:"
'<add key="VaultUrl" value="' + $vault.VaultUri + '"/>'
'<add key="AuthClientId" value="' + $servicePrincipal.ApplicationId + '"/>'
'<add key="AuthClientSecret" value="' + $applicationPassword + '"/>'
Write-Host

``` 

На следующем рисунке показан вывод предыдущего сценария:

![Конфигурация приложения](media/azure-stack-kv-sample-app/settingsoutput.png)

Запомните или запишите **VaultUrl**, **AuthClientId**, и **AuthClientSecret** значения, возвращаемые в предыдущем сценарии. Чтобы запустить приложение HelloKeyVault использовать эти значения.

## <a name="download-and-run-the-sample-application"></a>Загрузите и запустите образец приложения

Загрузить образец хранилища ключей Azure [образцы клиента хранилища ключей](https://www.microsoft.com/en-us/download/details.aspx?id=45343) страницы. Извлеките содержимое ZIP-файл на рабочей станции разработки. Существует два образца в папке примеров. В этом разделе мы используем HellpKeyVault образца. Перейдите к **Microsoft.Azure.KeyVault.Samples** > **образцы** > **HelloKeyVault** папку и открыть приложение HelloKeyVault в Visual Studio. 

Откройте файл HelloKeyVault\App.config и замените значения <appSettings> элемент с **VaultUrl**, **AuthClientId**, и **AuthClientSecret** значения Возвращает предыдущий сценарий. Обратите внимание, что по умолчанию файл App.config содержит заполнитель для *AuthCertThumbprint*, но использовать *AuthClientSecret* вместо него. После замены параметров Перестройте решение и запустить приложение.

![Параметры приложения](media/azure-stack-kv-sample-app/appconfig.png)
 
Приложение входит в Azure AD, а затем использует этот маркер для проверки подлинности в хранилище ключей Azure стека. Приложение выполняет операции, как создать, зашифровать, перенос и удалить ключи и секретные данные из хранилища ключей. Можно также передавать определенные параметры например *шифрования* и *расшифровать* приложению, которой гарантирует, что приложение выполняет эти операции с хранилищем. 


## <a name="next-steps"></a>Дальнейшие действия
[Развертывание виртуальной машины с помощью пароля из хранилища ключей](azure-stack-kv-deploy-vm-with-secret.md)

[Развертывание виртуальной Машины с помощью хранилища ключей сертификата](azure-stack-kv-push-secret-into-vm.md)



