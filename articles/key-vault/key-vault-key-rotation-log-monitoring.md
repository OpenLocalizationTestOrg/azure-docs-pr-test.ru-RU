---
title: "Настройка полной смены ключей и аудита в хранилище ключей Azure | Документация Майкрософт"
description: "Узнайте, как настроить смену ключей и отслеживание журналов хранилища ключей."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: 38c342802ed687985ac6f84f5a590a1a0dcc6c6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="49262-103">Настройка полной смены ключей и аудита в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="49262-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="49262-104">Введение</span><span class="sxs-lookup"><span data-stu-id="49262-104">Introduction</span></span>
<span data-ttu-id="49262-105">Созданное хранилище ключей Azure можно использовать для хранения ключей и секретов.</span><span class="sxs-lookup"><span data-stu-id="49262-105">After creating your key vault, you will be able to start using that vault to store your keys and secrets.</span></span> <span data-ttu-id="49262-106">В приложении больше не нужно сохранять ключи и секреты. При необходимости их можно получить из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-106">Your applications no longer need to persist your keys or secrets, but rather will request them from the key vault as needed.</span></span> <span data-ttu-id="49262-107">Это позволяет обновлять и администрировать ключи и секреты, не оказывая влияние на поведение приложения.</span><span class="sxs-lookup"><span data-stu-id="49262-107">This allows you to update keys and secrets without affecting the behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="49262-108">В этой статье рассматривается пример использования хранилища ключей Azure для хранения секрета (ключа учетной записи для службы хранилища Azure), к которому обращается приложение.</span><span class="sxs-lookup"><span data-stu-id="49262-108">This article walks through an example of using Azure Key Vault to store a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="49262-109">Здесь также описан процесс плановой смены этого ключа.</span><span class="sxs-lookup"><span data-stu-id="49262-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="49262-110">И в заключение мы покажем, как выполнять мониторинг журналов аудита для хранилища ключей и настройку оповещений о непредвиденных запросах.</span><span class="sxs-lookup"><span data-stu-id="49262-110">Finally, it walks through a demonstration of how to monitor the key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="49262-111">В этом руководстве не рассматривается первоначальная настройка хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-111">This tutorial is not intended to explain in detail the initial setup of your key vault.</span></span> <span data-ttu-id="49262-112">Соответствующие сведения см. в статье [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="49262-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="49262-113">Инструкции по кроссплатформенному интерфейсу командной строки см. в статье [Управление хранилищем ключей с помощью CLI](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="49262-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="49262-114">Настройка хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="49262-114">Set up Key Vault</span></span>
<span data-ttu-id="49262-115">Чтобы приложение могло получить секрет из хранилища ключей, секрет нужно создать и передать в хранилище.</span><span class="sxs-lookup"><span data-stu-id="49262-115">To enable an application to retrieve a secret from Key Vault, you must first create the secret and upload it to your vault.</span></span> <span data-ttu-id="49262-116">Для этого запустите сеанс Azure PowerShell и войдите в учетную запись Azure, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="49262-116">This can be accomplished by starting an Azure PowerShell session and signing in to your Azure account with the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="49262-117">Во всплывающем окне браузера введите имя пользователя и пароль учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="49262-117">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="49262-118">PowerShell получит все подписки, связанные с этой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="49262-118">PowerShell will get all the subscriptions that are associated with this account.</span></span> <span data-ttu-id="49262-119">По умолчанию PowerShell будет использовать первую из них.</span><span class="sxs-lookup"><span data-stu-id="49262-119">PowerShell uses the first one by default.</span></span>

<span data-ttu-id="49262-120">Если у вас есть несколько подписок, вы можете указать ту, с помощью которой вы создали хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="49262-120">If you have multiple subscriptions, you might have to specify the one that was used to create your key vault.</span></span> <span data-ttu-id="49262-121">Чтобы просмотреть подписки для своей учетной записи, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="49262-121">Enter the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="49262-122">Затем укажите подписку, связанную с хранилищем ключей, данные которого будут регистрироваться. Для этого выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="49262-122">To specify the subscription that's associated with the key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="49262-123">Так как в этой статье в качестве секрета используется ключ учетной записи хранения, вам необходимо получить его.</span><span class="sxs-lookup"><span data-stu-id="49262-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="49262-124">Преобразуйте полученный секрет (ключ учетной записи хранения) в защищенную строку, а затем создайте секрет с этим значением в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-124">After retrieving your secret (in this case, your storage account key), you must convert that to a secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="49262-125">После этого получите URI секрета, который вы создали.</span><span class="sxs-lookup"><span data-stu-id="49262-125">Next, get the URI for the secret you created.</span></span> <span data-ttu-id="49262-126">Это значение в дальнейшем позволит получить секрет из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-126">This is used in a later step when you call the key vault to retrieve your secret.</span></span> <span data-ttu-id="49262-127">Выполните следующую команду PowerShell и запишите значение идентификатора, которое используется в качестве URI секрета.</span><span class="sxs-lookup"><span data-stu-id="49262-127">Run the following PowerShell command and make note of the ID value, which is the secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-the-application"></a><span data-ttu-id="49262-128">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="49262-128">Set up the application</span></span>
<span data-ttu-id="49262-129">Теперь, когда вы сохранили секрет, можно создать код для его получения и использования.</span><span class="sxs-lookup"><span data-stu-id="49262-129">Now that you have a secret stored, you can use code to retrieve and use it.</span></span> <span data-ttu-id="49262-130">Для этого нужно выполнить несколько шагов.</span><span class="sxs-lookup"><span data-stu-id="49262-130">There are a few steps required to achieve this.</span></span> <span data-ttu-id="49262-131">Первый и самый важный — зарегистрируйте приложение в Azure Active Directory. Затем предоставьте хранилищу ключей сведения о приложении, от которого оно будет принимать запросы.</span><span class="sxs-lookup"><span data-stu-id="49262-131">The first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="49262-132">Приложение и хранилище ключей необходимо создать в одном и том же клиенте Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49262-132">Your application must be created on the same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="49262-133">Откройте вкладку "Приложения" в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49262-133">Open the applications tab of Azure Active Directory.</span></span>

![Вкладка "Приложения" в Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="49262-135">Щелкните **Добавить**, чтобы добавить приложение в клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49262-135">Choose **ADD** to add an application to your Azure Active Directory.</span></span>

![Выбор пункта "Добавить"](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="49262-137">Сохраните для параметра "Тип" значение **Веб-приложение и/или веб-API** и введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="49262-137">Leave the application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Ввод имени приложения](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="49262-139">Укажите нужные значения в полях **URL-адрес входа** и **URI идентификатора приложения**.</span><span class="sxs-lookup"><span data-stu-id="49262-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="49262-140">Для этого примера можно указать любые значения. Позже их можно изменить.</span><span class="sxs-lookup"><span data-stu-id="49262-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Предоставление необходимых URI](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="49262-142">Когда приложение будет добавлено в Azure Active Directory, откроется страница приложения.</span><span class="sxs-lookup"><span data-stu-id="49262-142">After the application is added to Azure Active Directory, you will be brought into the application page.</span></span> <span data-ttu-id="49262-143">Щелкните вкладку **Настройка**, а затем найдите и скопируйте значение **идентификатора клиента**.</span><span class="sxs-lookup"><span data-stu-id="49262-143">Click the **Configure** tab and then find and copy the **Client ID** value.</span></span> <span data-ttu-id="49262-144">Запишите это значение, так как оно понадобится для выполнения последующих действий.</span><span class="sxs-lookup"><span data-stu-id="49262-144">Make note of the client ID for later steps.</span></span>

<span data-ttu-id="49262-145">Далее создайте ключ для вашего приложения, чтобы оно могло взаимодействовать с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49262-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="49262-146">Для этого перейдите в раздел **Ключи** на вкладке **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="49262-146">You can create this under the **Keys** section in the **Configuration** tab.</span></span> <span data-ttu-id="49262-147">Запишите значение созданного ключа приложения Azure Active Directory. Оно понадобится вам на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="49262-147">Make note of the newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Ключи приложения Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="49262-149">Прежде чем отправлять вызовы из приложения в хранилище ключей, необходимо предоставить сведения о приложении и его разрешениях.</span><span class="sxs-lookup"><span data-stu-id="49262-149">Before establishing any calls from your application into the key vault, you must tell the key vault about your application and its permissions.</span></span> <span data-ttu-id="49262-150">Выполните следующую команду, указав имя хранилища и идентификатор клиента для приложения Azure Active Directory, чтобы предоставить приложению разрешение на получение данных (**Get**) из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-150">The following command takes the vault name and the client ID from your Azure Active Directory app and grants **Get** access to your key vault for the application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="49262-151">Теперь можно создавать код для вызовов из приложения.</span><span class="sxs-lookup"><span data-stu-id="49262-151">At this point, you are ready to start building your application calls.</span></span> <span data-ttu-id="49262-152">Установите в приложении пакеты NuGet, необходимые для взаимодействия с хранилищем ключей Azure и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49262-152">In your application, you must install the NuGet packages required to interact with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="49262-153">Для этого введите приведенные ниже команды в консоли диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="49262-153">From the Visual Studio Package Manager console, enter the following commands.</span></span> <span data-ttu-id="49262-154">На момент написания этой статьи версия самого свежего пакета Active Directory — 3.10.305231913. Узнайте последнюю версию пакета и при необходимости выполните соответствующие обновления.</span><span class="sxs-lookup"><span data-stu-id="49262-154">At the writing of this article, the current version of the Azure Active Directory package is 3.10.305231913, so you might want to confirm the latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="49262-155">В коде приложения создайте класс, который будет использоваться при проверке подлинности в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49262-155">In your application code, create a class to hold the method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="49262-156">В этом примере ему присвоено имя **Utils**.</span><span class="sxs-lookup"><span data-stu-id="49262-156">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="49262-157">Добавьте следующую инструкцию using:</span><span class="sxs-lookup"><span data-stu-id="49262-157">Add the following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="49262-158">Добавьте приведенный ниже метод для получения маркера JWT из Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49262-158">Next, add the following method to retrieve the JWT token from Azure Active Directory.</span></span> <span data-ttu-id="49262-159">Чтобы обеспечить поддержку, перенесите жестко заданные строковые значения в веб-конфигурацию или конфигурацию приложения.</span><span class="sxs-lookup"><span data-stu-id="49262-159">For maintainability, you may want to move the hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="49262-160">Добавьте необходимый код для обращения к хранилищу ключей и получения значения секрета.</span><span class="sxs-lookup"><span data-stu-id="49262-160">Add the necessary code to call Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="49262-161">Сначала следует добавить следующий оператор using.</span><span class="sxs-lookup"><span data-stu-id="49262-161">First you must add the following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="49262-162">Добавьте метод, который будет обращаться к хранилищу ключей и получать секрет.</span><span class="sxs-lookup"><span data-stu-id="49262-162">Add the method calls to invoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="49262-163">Добавьте в этот метод URI секрета, сохраненный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="49262-163">In this method, you provide the secret URI that you saved in a previous step.</span></span> <span data-ttu-id="49262-164">Обратите внимание, что мы используем метод **GetToken** из ранее созданного класса **Utils**.</span><span class="sxs-lookup"><span data-stu-id="49262-164">Note the use of the **GetToken** method from the **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="49262-165">Запустив приложение, вы можете выполнить проверку подлинности в Azure Active Directory и извлечь значение секрета из хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="49262-165">When you run your application, you should now be authenticating to Azure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="49262-166">Смена ключей с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="49262-166">Key rotation using Azure Automation</span></span>
<span data-ttu-id="49262-167">Реализовать смену значений секретов в хранилище ключей Azure можно разными способами.</span><span class="sxs-lookup"><span data-stu-id="49262-167">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="49262-168">Их можно сменить вручную, программным методом с помощью вызовов API или с использованием скрипта службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="49262-168">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="49262-169">В примере из этой статьи вы измените ключ доступа к учетной записи службы хранилища Azure с помощью Azure PowerShell и службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="49262-169">For the purposes of this article, you will be using Azure PowerShell combined with Azure Automation to change an Azure Storage Account access key.</span></span> <span data-ttu-id="49262-170">Затем с помощью нового ключа вы обновите секрет хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-170">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="49262-171">Чтобы служба автоматизации Azure могла задавать значения секретов в хранилище ключей, получите идентификатор клиента для подключения AzureRunAsConnection, созданный при установке экземпляра службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="49262-171">To allow Azure Automation to set secret values in your key vault, you must get the client ID for the connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="49262-172">Это значение можно получить в окне **Активы** в экземпляре службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="49262-172">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="49262-173">В этом окне выберите пункт **Подключения**, а затем щелкните субъект-службу **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="49262-173">From there, you choose **Connections** and then select the **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="49262-174">Запишите значение **идентификатора приложения**.</span><span class="sxs-lookup"><span data-stu-id="49262-174">Take note of the **Application ID**.</span></span>

![Идентификатор клиента службы автоматизации Azure](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="49262-176">В окне **Активы** выберите пункт **Модули**.</span><span class="sxs-lookup"><span data-stu-id="49262-176">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="49262-177">В окне **Модули** выберите элемент **Коллекция**, а затем найдите и **импортируйте** обновленные версии каждого из следующих модулей.</span><span class="sxs-lookup"><span data-stu-id="49262-177">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of the following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="49262-178">На момент написания этой статьи требовалось обновить только перечисленные выше модули, чтобы запустить следующий скрипт.</span><span class="sxs-lookup"><span data-stu-id="49262-178">At the writing of this article, only the previously noted modules needed to be updated for the following script.</span></span> <span data-ttu-id="49262-179">Если задание по автоматизации завершится сбоем, убедитесь, что вы импортировали все необходимые модули и зависимости.</span><span class="sxs-lookup"><span data-stu-id="49262-179">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="49262-180">Когда вы получите идентификатор приложения для подключения к службе автоматизации Azure, предоставьте приложению право обновлять секреты в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-180">After you have retrieved the application ID for your Azure Automation connection, you must tell your key vault that this application has access to update secrets in your vault.</span></span> <span data-ttu-id="49262-181">Для этого нужно выполнить следующую команду PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49262-181">This can be accomplished with the following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="49262-182">В экземпляре службы автоматизации Azure выберите пункт **Модули Runbook**, а затем — **Добавить Runbook**.</span><span class="sxs-lookup"><span data-stu-id="49262-182">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="49262-183">Выберите **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="49262-183">Select **Quick Create**.</span></span> <span data-ttu-id="49262-184">Введите имя модуля Runbook и выберите значение **PowerShell** в качестве типа модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="49262-184">Name your runbook and select **PowerShell** as the runbook type.</span></span> <span data-ttu-id="49262-185">Вы можете также добавить описание (необязательно).</span><span class="sxs-lookup"><span data-stu-id="49262-185">You have the option to add a description.</span></span> <span data-ttu-id="49262-186">Наконец, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="49262-186">Finally, click **Create**.</span></span>

![Создание модуля Runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="49262-188">В области редактора нового модуля Runbook вставьте следующий сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49262-188">Paste the following PowerShell script in the editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get the connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in to Azure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set the following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for the storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="49262-189">В области редактора выберите **Область тестирования**, чтобы выполнить тестирование сценария.</span><span class="sxs-lookup"><span data-stu-id="49262-189">From the editor pane, choose **Test pane** to test your script.</span></span> <span data-ttu-id="49262-190">Когда скрипт будет работать без ошибок, выберите параметр **Публикация** и на панели конфигурации для модуля Runbook настройте его расписание.</span><span class="sxs-lookup"><span data-stu-id="49262-190">Once the script is running without error, you can select **Publish**, and then you can apply a schedule for the runbook back in the runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="49262-191">Конвейер аудита для хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="49262-191">Key Vault auditing pipeline</span></span>
<span data-ttu-id="49262-192">При настройке хранилища ключей вы можете включить аудит, чтобы собирать журналы запросов на доступ к этому хранилищу.</span><span class="sxs-lookup"><span data-stu-id="49262-192">When you set up a key vault, you can turn on auditing to collect logs on access requests made to the key vault.</span></span> <span data-ttu-id="49262-193">Эти журналы хранятся в назначенной учетной записи службы хранилища Azure. Их можно извлекать, отслеживать и анализировать.</span><span class="sxs-lookup"><span data-stu-id="49262-193">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="49262-194">В следующем сценарии создается конвейер с помощью журналов аудита для хранилища ключей, функций Azure и Azure Logic Apps. Этот конвейер отправляет сообщения электронной почты, если секреты из хранилища получает приложение, которое не соответствует идентификатору веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="49262-194">The following scenario uses Azure functions, Azure logic apps, and key vault audit logs to create a pipeline to send an email when an app that does match the app ID of the web app retrieves secrets from the vault.</span></span>

<span data-ttu-id="49262-195">Сначала нужно включить ведение журнала в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-195">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="49262-196">Это можно сделать с помощью следующих команд PowerShell (процесс описан в статье [Ведение журнала хранилища ключей Azure](key-vault-logging.md)).</span><span class="sxs-lookup"><span data-stu-id="49262-196">This can be done via the following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="49262-197">Включенные журналы аудита начнут сбор данных в назначенную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="49262-197">After this is enabled, audit logs start collecting into the designated storage account.</span></span> <span data-ttu-id="49262-198">В этих журналах содержатся сведения о том, кто, как и когда осуществлял доступ к хранилищам ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-198">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="49262-199">Регистрируемые в журналах сведения становятся доступны через 10 минут после выполнения операции с хранилищем ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-199">You can access your logging information 10 minutes after the key vault operation.</span></span> <span data-ttu-id="49262-200">Обычно они доступны даже раньше.</span><span class="sxs-lookup"><span data-stu-id="49262-200">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="49262-201">Теперь необходимо [создать очередь служебной шины Azure](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="49262-201">The next step is to [create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="49262-202">Туда будут помещаться журналы аудита хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-202">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="49262-203">Приложение логики принимает сообщения журнала аудита, помещенные в очередь, и обрабатывает их.</span><span class="sxs-lookup"><span data-stu-id="49262-203">When the audit log messages are in the queue, the logic app picks them up and acts on them.</span></span> <span data-ttu-id="49262-204">Выполните следующие действия, чтобы создать служебную шину.</span><span class="sxs-lookup"><span data-stu-id="49262-204">Create a service bus with the following steps:</span></span>

1. <span data-ttu-id="49262-205">Создайте пространство имен для служебной шины (если оно уже создано, перейдите к шагу 2).</span><span class="sxs-lookup"><span data-stu-id="49262-205">Create a Service Bus namespace (if you already have one that you want to use for this, skip to Step 2).</span></span>
2. <span data-ttu-id="49262-206">Перейдите к служебной шине на портале Azure и выберите пространство имен, в котором нужно создать очередь.</span><span class="sxs-lookup"><span data-stu-id="49262-206">Browse to the service bus in the Azure portal and select the namespace you want to create the queue in.</span></span>
3. <span data-ttu-id="49262-207">Щелкните **Создать**, последовательно выберите **Служебная шина -> Очередь** и введите необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="49262-207">Select **New** and choose **Service Bus > Queue** and enter the required details.</span></span>
4. <span data-ttu-id="49262-208">Получите сведения о подключении к служебной шине. Для этого выберите пространство имен и щелкните **Сведения о подключении**.</span><span class="sxs-lookup"><span data-stu-id="49262-208">Select the Service Bus connection information by choosing the namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="49262-209">Эти сведения понадобятся в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="49262-209">You will need this information for the next section.</span></span>

<span data-ttu-id="49262-210">Затем [создайте функцию Azure](../azure-functions/functions-create-first-azure-function.md), которая будет опрашивать журналы хранилища ключей в учетной записи хранения и извлекать новые события.</span><span class="sxs-lookup"><span data-stu-id="49262-210">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) to poll key vault logs within the storage account and pick up new events.</span></span> <span data-ttu-id="49262-211">Эта функция будет запускаться по расписанию.</span><span class="sxs-lookup"><span data-stu-id="49262-211">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="49262-212">Чтобы создать функцию Azure, последовательно выберите **Создать -> Приложение-функция** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="49262-212">To create an Azure function, choose **New > Function App** in the Azure portal.</span></span> <span data-ttu-id="49262-213">Можно использовать для этого действующий план размещения или создать новый.</span><span class="sxs-lookup"><span data-stu-id="49262-213">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="49262-214">Кроме того, можно использовать динамическое размещение.</span><span class="sxs-lookup"><span data-stu-id="49262-214">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="49262-215">Дополнительные сведения о вариантах размещения функции см. в статье [Масштабирование функций Azure](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="49262-215">More details on Function hosting options can be found at [How to scale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="49262-216">Перейдите к созданной функции Azure и выберите функцию таймера и C\#.</span><span class="sxs-lookup"><span data-stu-id="49262-216">When the Azure function is created, navigate to it and choose a timer function and C\#.</span></span> <span data-ttu-id="49262-217">Затем щелкните **Создать эту функцию**.</span><span class="sxs-lookup"><span data-stu-id="49262-217">Then click **Create this function**.</span></span>

![Начальная колонка функций Azure](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="49262-219">На вкладке **Разработка** замените код run.csx приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="49262-219">On the **Develop** tab, replace the run.csx code with the following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting to now.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required to order by time as they may not be in the file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending to ServiceBus, use the payloadStream and set keeporiginal to true
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="49262-220">Обязательно замените в коде переменные. Они должны указывать на учетную запись хранения, в которую записываются журналы хранилища ключей, на созданную ранее служебную шину и на определенный путь к журналам хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-220">Make sure to replace the variables in the preceding code to point to your storage account where the key vault logs are written, the service bus you created earlier, and the specific path to the key vault storage logs.</span></span>
>
>

<span data-ttu-id="49262-221">Функция получает из учетной записи хранения, в которою записываются журналы хранилища ключей, последний файл журнала, извлекает из него последние события и передает их в очередь служебной шины.</span><span class="sxs-lookup"><span data-stu-id="49262-221">The function picks up the latest log file from the storage account where the key vault logs are written, grabs the latest events from that file, and pushes them to a Service Bus queue.</span></span> <span data-ttu-id="49262-222">Так как в файле может содержаться несколько событий, создайте файл sync.txt, в котором будут отображаться данные о просматриваемой функцией метке времени для последнего извлеченного события.</span><span class="sxs-lookup"><span data-stu-id="49262-222">Since a single file could have multiple events, you should create a sync.txt file that the function also looks at to determine the time stamp of the last event that was picked up.</span></span> <span data-ttu-id="49262-223">Это гарантирует, что одно и то же событие не будет отправлено в служебную шину несколько раз.</span><span class="sxs-lookup"><span data-stu-id="49262-223">This ensures that you don't push the same event multiple times.</span></span> <span data-ttu-id="49262-224">В файле sync.txt содержится метка времени для последнего обработанного события.</span><span class="sxs-lookup"><span data-stu-id="49262-224">This sync.txt file contains a timestamp for the last encountered event.</span></span> <span data-ttu-id="49262-225">Чтобы журналы были упорядочены должным образом, при загрузке их необходимо отсортировать по метке времени.</span><span class="sxs-lookup"><span data-stu-id="49262-225">The logs, when loaded, have to be sorted based on the timestamp to ensure they are ordered correctly.</span></span>

<span data-ttu-id="49262-226">Для поддержки этой возможности мы предоставили несколько дополнительных библиотек, которые недоступны по умолчанию в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="49262-226">For this function, we reference a couple of additional libraries that are not available out of the box in Azure Functions.</span></span> <span data-ttu-id="49262-227">Эти библиотеки необходимо добавить в функции Azure с помощью NuGet.</span><span class="sxs-lookup"><span data-stu-id="49262-227">To include these, we need Azure Functions to pull them using NuGet.</span></span> <span data-ttu-id="49262-228">Щелкните **Просмотреть файлы**.</span><span class="sxs-lookup"><span data-stu-id="49262-228">Choose the **View Files** option.</span></span>

![Элемент "Просмотреть файлы"](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="49262-230">Затем добавьте новый файл project.json со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="49262-230">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="49262-231">Когда вы **сохраните** изменения, функции Azure скачают необходимые двоичные файлы.</span><span class="sxs-lookup"><span data-stu-id="49262-231">Upon **Save**, Azure Functions will download the required binaries.</span></span>

<span data-ttu-id="49262-232">Перейдите на вкладку **Интеграция** и введите для параметра "Таймер" понятное имя, которое будет использоваться в функции.</span><span class="sxs-lookup"><span data-stu-id="49262-232">Switch to the **Integrate** tab and give the timer parameter a meaningful name to use within the function.</span></span> <span data-ttu-id="49262-233">В приведенном выше коде ожидается, что таймеру будет присвоено имя *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="49262-233">In the preceding code, it expects the timer to be called *myTimer*.</span></span> <span data-ttu-id="49262-234">Укажите [выражение CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) для таймера, который инициирует запуск функции каждую минуту, следующим образом: 0 \* \* \* \* \*.</span><span class="sxs-lookup"><span data-stu-id="49262-234">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for the timer that will cause the function to run once a minute.</span></span>

<span data-ttu-id="49262-235">На вкладке **Интеграция** добавьте входной параметр типа **Хранилище BLOB-объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="49262-235">On the same **Integrate** tab, add an input of the type **Azure Blob Storage**.</span></span> <span data-ttu-id="49262-236">Он указывает на файл sync.txt, содержащий метку времени для последнего события, просмотренного функцией.</span><span class="sxs-lookup"><span data-stu-id="49262-236">This will point to the sync.txt file that contains the timestamp of the last event looked at by the function.</span></span> <span data-ttu-id="49262-237">В коде функции можно получить эту информацию по имени параметра.</span><span class="sxs-lookup"><span data-stu-id="49262-237">This will be available within the function by the parameter name.</span></span> <span data-ttu-id="49262-238">В приведенном выше коде ожидается, что параметру входного хранилища BLOB-объектов Azure будет присвоено имя *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="49262-238">In the preceding code, the Azure Blob Storage input expects the parameter name to be *inputBlob*.</span></span> <span data-ttu-id="49262-239">Выберите учетную запись хранилища, в которой будет находиться файл sync.txt (это может быть та же или другая учетная запись хранения).</span><span class="sxs-lookup"><span data-stu-id="49262-239">Choose the storage account where the sync.txt file will reside (it could be the same or a different storage account).</span></span> <span data-ttu-id="49262-240">В соответствующем поле укажите путь размещения файла в формате {имя_контейнера}/путь_к_файлу/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="49262-240">In the path field, provide the path where the file lives in the format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="49262-241">Добавьте выходной параметр типа *Хранилище BLOB-объектов Azure*.</span><span class="sxs-lookup"><span data-stu-id="49262-241">Add an output of the type *Azure Blob Storage* output.</span></span> <span data-ttu-id="49262-242">Он будет указывать на файл sync.txt, определенный выше в качестве входа.</span><span class="sxs-lookup"><span data-stu-id="49262-242">This will point to the sync.txt file you defined in the input.</span></span> <span data-ttu-id="49262-243">Функция использует выходной параметр, чтобы записать метку времени для последнего просмотренного события.</span><span class="sxs-lookup"><span data-stu-id="49262-243">This is used by the function to write the timestamp of the last event looked at.</span></span> <span data-ttu-id="49262-244">В приведенном выше коде ожидается, что этому параметру будет присвоено имя *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="49262-244">The preceding code expects this parameter to be called *outputBlob*.</span></span>

<span data-ttu-id="49262-245">Теперь функция готова.</span><span class="sxs-lookup"><span data-stu-id="49262-245">At this point, the function is ready.</span></span> <span data-ttu-id="49262-246">Перейдите на вкладку **Разработка** и сохраните код.</span><span class="sxs-lookup"><span data-stu-id="49262-246">Make sure to switch back to the **Develop** tab and save the code.</span></span> <span data-ttu-id="49262-247">Если в окне вывода появились ошибки компиляции, исправьте их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="49262-247">Check the output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="49262-248">Если код скомпилируется успешно, функция сразу начнет проверять журналы хранилища ключей каждую минуту и передавать новые события в указанную очередь служебной шины.</span><span class="sxs-lookup"><span data-stu-id="49262-248">If the code compiles, then the code should now be checking the key vault logs every minute and pushing any new events onto the defined Service Bus queue.</span></span> <span data-ttu-id="49262-249">При каждом запуске функции в окне журнала будут отображаться данные журнала.</span><span class="sxs-lookup"><span data-stu-id="49262-249">You should see logging information write out to the log window every time the function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="49262-250">Приложение логики Azure</span><span class="sxs-lookup"><span data-stu-id="49262-250">Azure logic app</span></span>
<span data-ttu-id="49262-251">Сейчас вам нужно создать приложение логики Azure, которое будет получать события, отправленные функцией в очередь служебной шины, анализировать их содержимое и отправлять сообщения электронной почты при выполнении заданного условия.</span><span class="sxs-lookup"><span data-stu-id="49262-251">Next you must create an Azure logic app that picks up the events that the function is pushing to the Service Bus queue, parses the content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="49262-252">Чтобы [создать приложение логики](../logic-apps/logic-apps-create-a-logic-app.md), последовательно выберите **Создать -> Приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="49262-252">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going to **New > Logic App**.</span></span>

<span data-ttu-id="49262-253">Создав приложение логики, перейдите к нему и выберите команду **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="49262-253">Once the logic app is created, navigate to it and choose **edit**.</span></span> <span data-ttu-id="49262-254">Чтобы подключить приложение к очереди, в редакторе приложения логики выберите **Очередь служебной шины** и введите учетные данные служебной шины.</span><span class="sxs-lookup"><span data-stu-id="49262-254">Within the logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials to connect it to the queue.</span></span>

![Служебная шина приложения логики Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="49262-256">Затем выберите команду **Добавить условие**.</span><span class="sxs-lookup"><span data-stu-id="49262-256">Next choose **Add a condition**.</span></span> <span data-ttu-id="49262-257">Откройте расширенный редактор и введите следующий код, заменив параметр APP_ID реальным значением идентификатора веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="49262-257">In the condition, switch to the advanced editor and enter the following code, replacing APP_ID with the actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="49262-258">Если свойство *appid* из входящего события (текст сообщения служебной шины) не соответствует идентификатору *appid* приложения, выражение вернет значение **false**.</span><span class="sxs-lookup"><span data-stu-id="49262-258">This expression essentially returns **false** if the *appid* from the incoming event (which is the body of the Service Bus message) is not the *appid* of the app.</span></span>

<span data-ttu-id="49262-259">Теперь создайте действие в разделе **If no, do nothing…** (Если нет, ничего не предпринимать).</span><span class="sxs-lookup"><span data-stu-id="49262-259">Now, create an action under **If no, do nothing**.</span></span>

![Выбор действия приложения логики Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="49262-261">Для примера создайте действие **Office 365 — отправить электронное письмо**.</span><span class="sxs-lookup"><span data-stu-id="49262-261">For the action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="49262-262">Заполните поля, чтобы создать электронное письмо, которое будет отправляться, когда определенное условие возвращает значение **false**.</span><span class="sxs-lookup"><span data-stu-id="49262-262">Fill out the fields to create an email to send when the defined condition returns **false**.</span></span> <span data-ttu-id="49262-263">Если у вас нет Office 365, можно создать такое же действие для другой службы.</span><span class="sxs-lookup"><span data-stu-id="49262-263">If you do not have Office 365, you could look at alternatives to achieve the same results.</span></span>

<span data-ttu-id="49262-264">На этом этапе вы создали конвейер, который каждую минуту будет проверять новые записи в журналах аудита для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="49262-264">At this point, you have an end to end pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="49262-265">Он отправляет обнаруженные записи в очередь служебной шины.</span><span class="sxs-lookup"><span data-stu-id="49262-265">It pushes new logs it finds to a service bus queue.</span></span> <span data-ttu-id="49262-266">Приложение логики запускается каждый раз при появлении в очереди нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="49262-266">The logic app is triggered when a new message lands in the queue.</span></span> <span data-ttu-id="49262-267">Если параметр *appid* для нового события не совпадает с идентификатором зарегистрированного приложения, отправляется сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="49262-267">If the *appid* within the event does not match the app ID of the calling application, it sends an email.</span></span>
