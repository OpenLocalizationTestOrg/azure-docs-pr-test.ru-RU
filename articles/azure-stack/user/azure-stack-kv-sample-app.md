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
# <a name="sample-application-that-uses-keys-and-secrets-stored-in-a-key-vault"></a><span data-ttu-id="5965a-103">Пример приложения, использующего ключи и секретные данные, хранящиеся в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="5965a-103">Sample application that uses keys and secrets stored in a key vault</span></span>

<span data-ttu-id="5965a-104">В этой статье мы показано, как запустить образец приложения (HelloKeyVault), который получает ключи и секретные данные из хранилища ключей Azure стека.</span><span class="sxs-lookup"><span data-stu-id="5965a-104">In this article, we show you how to run a sample application (HelloKeyVault) that retrieves keys and secrets from a key vault in Azure Stack.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5965a-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5965a-105">Prerequisites</span></span> 

<span data-ttu-id="5965a-106">Выполнить следующие предварительные требования, либо из [Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="5965a-106">Run the following prerequisites either from the [Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="5965a-107">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="5965a-107">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="5965a-108">Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="5965a-108">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="create-and-get-the-key-vault-and-application-settings"></a><span data-ttu-id="5965a-109">Создание и хранилище ключей, а также параметры приложения</span><span class="sxs-lookup"><span data-stu-id="5965a-109">Create and get the key vault and application settings</span></span>

<span data-ttu-id="5965a-110">Во-первых необходимо создание хранилища ключей Azure стека и зарегистрировать приложение в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5965a-110">First, you should create a key vault in Azure Stack, and register an application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="5965a-111">Можно создать и зарегистрировать в хранилищах ключей с помощью портала Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5965a-111">You can create and register the key vaults by using the Azure portal or PowerShell.</span></span> <span data-ttu-id="5965a-112">В этой статье показан способ PowerShell для выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="5965a-112">This article shows you the PowerShell way to do the tasks.</span></span> <span data-ttu-id="5965a-113">По умолчанию этот сценарий PowerShell создает новое приложение в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5965a-113">By default, this PowerShell script creates a new application in Active Directory.</span></span> <span data-ttu-id="5965a-114">Тем не менее вы можете воспользоваться одним из существующих приложений.</span><span class="sxs-lookup"><span data-stu-id="5965a-114">However, you can also use one of your existing applications.</span></span> <span data-ttu-id="5965a-115">Убедитесь в том предоставить значение для `aadTenantName` и `applicationPassword` переменных.</span><span class="sxs-lookup"><span data-stu-id="5965a-115">Make sure to provide a value for the `aadTenantName` and `applicationPassword` variables.</span></span> <span data-ttu-id="5965a-116">Если не указать значение для `applicationPassword` переменной, этот скрипт создает случайный пароль.</span><span class="sxs-lookup"><span data-stu-id="5965a-116">If you don't specify a value for the `applicationPassword` variable, this script generates a random password.</span></span> 

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

<span data-ttu-id="5965a-117">На следующем рисунке показан вывод предыдущего сценария:</span><span class="sxs-lookup"><span data-stu-id="5965a-117">The following screenshot shows the output of the previous script:</span></span>

![Конфигурация приложения](media/azure-stack-kv-sample-app/settingsoutput.png)

<span data-ttu-id="5965a-119">Запомните или запишите **VaultUrl**, **AuthClientId**, и **AuthClientSecret** значения, возвращаемые в предыдущем сценарии.</span><span class="sxs-lookup"><span data-stu-id="5965a-119">Make a note of the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span></span> <span data-ttu-id="5965a-120">Чтобы запустить приложение HelloKeyVault использовать эти значения.</span><span class="sxs-lookup"><span data-stu-id="5965a-120">You use these values to run the HelloKeyVault application.</span></span>

## <a name="download-and-run-the-sample-application"></a><span data-ttu-id="5965a-121">Загрузите и запустите образец приложения</span><span class="sxs-lookup"><span data-stu-id="5965a-121">Download and run the sample application</span></span>

<span data-ttu-id="5965a-122">Загрузить образец хранилища ключей Azure [образцы клиента хранилища ключей](https://www.microsoft.com/en-us/download/details.aspx?id=45343) страницы.</span><span class="sxs-lookup"><span data-stu-id="5965a-122">Download the key vault sample from the Azure [Key Vault client samples](https://www.microsoft.com/en-us/download/details.aspx?id=45343) page.</span></span> <span data-ttu-id="5965a-123">Извлеките содержимое ZIP-файл на рабочей станции разработки.</span><span class="sxs-lookup"><span data-stu-id="5965a-123">Extract the contents of the .zip file onto your development workstation.</span></span> <span data-ttu-id="5965a-124">Существует два образца в папке примеров.</span><span class="sxs-lookup"><span data-stu-id="5965a-124">There are two samples within the samples folder.</span></span> <span data-ttu-id="5965a-125">В этом разделе мы используем HellpKeyVault образца.</span><span class="sxs-lookup"><span data-stu-id="5965a-125">We use the HellpKeyVault sample in this topic.</span></span> <span data-ttu-id="5965a-126">Перейдите к **Microsoft.Azure.KeyVault.Samples** > **образцы** > **HelloKeyVault** папку и открыть приложение HelloKeyVault в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5965a-126">Browse to the **Microsoft.Azure.KeyVault.Samples** > **samples** > **HelloKeyVault** folder and open the HelloKeyVault application in Visual Studio.</span></span> 

<span data-ttu-id="5965a-127">Откройте файл HelloKeyVault\App.config и замените значения <appSettings> элемент с **VaultUrl**, **AuthClientId**, и **AuthClientSecret** значения Возвращает предыдущий сценарий.</span><span class="sxs-lookup"><span data-stu-id="5965a-127">Open the HelloKeyVault\App.config file and replace the values of the <appSettings> element with the **VaultUrl**, **AuthClientId**, and **AuthClientSecret** values returned by the previous script.</span></span> <span data-ttu-id="5965a-128">Обратите внимание, что по умолчанию файл App.config содержит заполнитель для *AuthCertThumbprint*, но использовать *AuthClientSecret* вместо него.</span><span class="sxs-lookup"><span data-stu-id="5965a-128">Note that by default the App.config contains a placeholder for *AuthCertThumbprint*, but use *AuthClientSecret* instead.</span></span> <span data-ttu-id="5965a-129">После замены параметров Перестройте решение и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="5965a-129">After you replace the settings, rebuild the solution and start the application.</span></span>

![Параметры приложения](media/azure-stack-kv-sample-app/appconfig.png)
 
<span data-ttu-id="5965a-131">Приложение входит в Azure AD, а затем использует этот маркер для проверки подлинности в хранилище ключей Azure стека.</span><span class="sxs-lookup"><span data-stu-id="5965a-131">The application signs in to Azure AD, and then uses that token to authenticate to the key vault in Azure Stack.</span></span> <span data-ttu-id="5965a-132">Приложение выполняет операции, как создать, зашифровать, перенос и удалить ключи и секретные данные из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5965a-132">The application performs operations like create, encrypt, wrap, and delete on the keys and secrets of the key vault.</span></span> <span data-ttu-id="5965a-133">Можно также передавать определенные параметры например *шифрования* и *расшифровать* приложению, которой гарантирует, что приложение выполняет эти операции с хранилищем.</span><span class="sxs-lookup"><span data-stu-id="5965a-133">You can also pass specific parameters such as *encrypt* and *decrypt* to the application, which makes sure that the application executes only those operations against the vault.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5965a-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5965a-134">Next steps</span></span>
[<span data-ttu-id="5965a-135">Развертывание виртуальной машины с помощью пароля из хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5965a-135">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="5965a-136">Развертывание виртуальной Машины с помощью хранилища ключей сертификата</span><span class="sxs-lookup"><span data-stu-id="5965a-136">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)



