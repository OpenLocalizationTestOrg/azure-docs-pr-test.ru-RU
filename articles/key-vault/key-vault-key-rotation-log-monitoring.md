---
title: "aaaSet копирование хранилища ключей Azure с начала до конца смены ключей и аудит | Документы Microsoft"
description: "Используйте это как tootoohelp, получить настраиваются с помощью мониторинга журналы хранилища ключей и смены ключей."
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
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="accc4-103">Настройка полной смены ключей и аудита в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="accc4-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="accc4-104">Введение</span><span class="sxs-lookup"><span data-stu-id="accc4-104">Introduction</span></span>
<span data-ttu-id="accc4-105">После создания хранилища ключей, будет может toostart ключи и секретные коды, с помощью этого toostore хранилища.</span><span class="sxs-lookup"><span data-stu-id="accc4-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="accc4-106">Приложения больше не нужна toopersist ключей или секретные данные, но вместо этого будет запрашивать их из хранилища ключей hello при необходимости.</span><span class="sxs-lookup"><span data-stu-id="accc4-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="accc4-107">Это позволяет вам tooupdate ключи и секретные коды без влияния на поведение приложения, который открывает разнообразные возможности вокруг ключ и секретный управления hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="accc4-108">В этой статье рассматриваются пример использования toostore хранилище ключей Azure секрета, в этом случае ключ учетной записи хранилища Azure, доступ к которому приложение.</span><span class="sxs-lookup"><span data-stu-id="accc4-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="accc4-109">Здесь также описан процесс плановой смены этого ключа.</span><span class="sxs-lookup"><span data-stu-id="accc4-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="accc4-110">Наконец он проходит через демонстрацию как toomonitor hello журналы аудита хранилища ключей и создавать оповещения при внесении непредвиденные запросы.</span><span class="sxs-lookup"><span data-stu-id="accc4-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="accc4-111">Этот учебник не предполагаемого tooexplain детализации hello начальной настройки хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="accc4-112">Соответствующие сведения см. в статье [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="accc4-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="accc4-113">Инструкции по кроссплатформенному интерфейсу командной строки см. в статье [Управление хранилищем ключей с помощью CLI](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="accc4-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="accc4-114">Настройка хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="accc4-114">Set up Key Vault</span></span>
<span data-ttu-id="accc4-115">tooenable приложения tooretrieve секрета из хранилища ключей, необходимо сначала создать секрет hello и отправьте его tooyour хранилища.</span><span class="sxs-lookup"><span data-stu-id="accc4-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="accc4-116">Это можно сделать, запустите сеанс Azure PowerShell и вход tooyour учетная запись Azure с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="accc4-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="accc4-117">В hello всплывающем окне браузера введите имя пользователя учетной записи Azure и пароль.</span><span class="sxs-lookup"><span data-stu-id="accc4-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="accc4-118">PowerShell получит все подписки hello, связанные с этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="accc4-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="accc4-119">Использует PowerShell hello первый из них по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="accc4-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="accc4-120">Если у вас несколько подписок, может потребоваться toospecify hello, входящая в используемых toocreate хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="accc4-121">Введите hello, следуя toosee hello подписки для учетной записи:</span><span class="sxs-lookup"><span data-stu-id="accc4-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="accc4-122">toospecify hello подписки, связанной с хранилищем ключей hello, которые можно выполнять вход, введите:</span><span class="sxs-lookup"><span data-stu-id="accc4-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="accc4-123">Так как в этой статье в качестве секрета используется ключ учетной записи хранения, вам необходимо получить его.</span><span class="sxs-lookup"><span data-stu-id="accc4-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="accc4-124">После получения ваш секрет (в данном случае ключ учетной записи хранилища), необходимо преобразовать этой защищенной строки tooa и создайте секрета с соответствующими значениями в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="accc4-125">Затем следует получите hello URI для hello секрета, который был создан.</span><span class="sxs-lookup"><span data-stu-id="accc4-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="accc4-126">Используется в дальнейшем при вызове hello хранилища ключей tooretrieve ваш секрет.</span><span class="sxs-lookup"><span data-stu-id="accc4-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="accc4-127">Выполните следующую команду PowerShell hello и запишите значение идентификатора hello, которое является hello секрет URI.</span><span class="sxs-lookup"><span data-stu-id="accc4-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="accc4-128">Настройка приложения hello</span><span class="sxs-lookup"><span data-stu-id="accc4-128">Set up hello application</span></span>
<span data-ttu-id="accc4-129">Теперь, когда секретов, хранимых можно использовать tooretrieve код и использовать его.</span><span class="sxs-lookup"><span data-stu-id="accc4-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="accc4-130">Существуют несколько шагов, необходимых tooachieve это.</span><span class="sxs-lookup"><span data-stu-id="accc4-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="accc4-131">Hello первый и самый важный шаг является зарегистрировать приложение в Azure Active Directory и затем о том, хранилище ключей информации о приложениях, чтобы его можно разрешить запросы от приложения.</span><span class="sxs-lookup"><span data-stu-id="accc4-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="accc4-132">Приложения должны быть созданы на hello же клиент Azure Active Directory в качестве хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="accc4-133">Перейдите на вкладку приложения hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="accc4-133">Open hello applications tab of Azure Active Directory.</span></span>

![Вкладка "Приложения" в Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="accc4-135">Выберите **добавить** tooadd tooyour приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="accc4-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![Выбор пункта "Добавить"](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="accc4-137">Оставьте тип приложения hello как **веб-приложение и/или WEB API** и присвойте имя приложения.</span><span class="sxs-lookup"><span data-stu-id="accc4-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Имя hello приложения](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="accc4-139">Укажите нужные значения в полях **URL-адрес входа** и **URI идентификатора приложения**.</span><span class="sxs-lookup"><span data-stu-id="accc4-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="accc4-140">Для этого примера можно указать любые значения. Позже их можно изменить.</span><span class="sxs-lookup"><span data-stu-id="accc4-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Предоставление необходимых URI](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="accc4-142">После добавления приложения hello tooAzure Active Directory, то будут введены в страницы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="accc4-143">Нажмите кнопку hello **Настройка** вкладку и затем найдите и скопируйте hello **идентификатор клиента** значение.</span><span class="sxs-lookup"><span data-stu-id="accc4-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="accc4-144">Запишите идентификатор hello клиента для выполнения следующих действий.</span><span class="sxs-lookup"><span data-stu-id="accc4-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="accc4-145">Далее создайте ключ для вашего приложения, чтобы оно могло взаимодействовать с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="accc4-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="accc4-146">Это можно создать в группе hello **ключей** раздела hello **конфигурации** вкладки. Запишите hello вновь созданный ключ из приложения Azure Active Directory для использования в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="accc4-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Ключи приложения Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="accc4-148">Перед установкой каких-либо вызовов из приложения в хранилище ключей hello, hello хранилища ключей необходимо сообщить о приложении и его разрешения.</span><span class="sxs-lookup"><span data-stu-id="accc4-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="accc4-149">Hello следующая команда получает имя хранилища hello и hello идентификатор клиента из приложения Azure Active Directory и предоставляет **получить** хранилища ключей tooyour доступа для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="accc4-150">На этом этапе вы являются готов toostart построение приложение вызывает.</span><span class="sxs-lookup"><span data-stu-id="accc4-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="accc4-151">В приложении необходимо установить toointeract необходимые пакеты NuGet hello с хранилищем ключей Azure и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="accc4-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="accc4-152">Из консоли диспетчера пакетов Visual Studio hello введите следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="accc4-153">Hello написания данной статьи, hello текущей версии пакета hello Azure Active Directory является 3.10.305231913, поэтому может требуется последняя версия tooconfirm hello и соответствующим образом обновить.</span><span class="sxs-lookup"><span data-stu-id="accc4-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="accc4-154">В коде приложения создайте метод hello toohold класс для проверки подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="accc4-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="accc4-155">В этом примере ему присвоено имя **Utils**.</span><span class="sxs-lookup"><span data-stu-id="accc4-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="accc4-156">Добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="accc4-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="accc4-157">Добавьте следующую токен JWT hello tooretrieve метода из Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="accc4-158">Для удобства обслуживания можно жестко заданная строка значений toomove hello в конфигурацию сети или приложения.</span><span class="sxs-lookup"><span data-stu-id="accc4-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="accc4-159">Добавить необходимый код hello toocall хранилище ключей и получить ваш секретное значение.</span><span class="sxs-lookup"><span data-stu-id="accc4-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="accc4-160">Сначала необходимо добавить следующие hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="accc4-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="accc4-161">Добавить tooinvoke вызовы метода hello хранилища ключей и получить ваш секрет.</span><span class="sxs-lookup"><span data-stu-id="accc4-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="accc4-162">В этом методе предоставляют hello секрет URI, который был сохранен на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="accc4-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="accc4-163">Обратите внимание на использование hello hello **GetToken** метод hello **Utils** ранее созданного класса.</span><span class="sxs-lookup"><span data-stu-id="accc4-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="accc4-164">При запуске приложения, вы должны теперь проходят проверку подлинности tooAzure Active Directory, а затем получение вашего секретное значение из хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="accc4-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="accc4-165">Смена ключей с помощью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="accc4-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="accc4-166">Реализовать смену значений секретов в хранилище ключей Azure можно разными способами.</span><span class="sxs-lookup"><span data-stu-id="accc4-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="accc4-167">Их можно сменить вручную, программным методом с помощью вызовов API или с использованием скрипта службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="accc4-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="accc4-168">В целях hello этой статьи можно с помощью Azure PowerShell в сочетании с toochange автоматизации Azure ключ доступа учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="accc4-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="accc4-169">Затем с помощью нового ключа вы обновите секрет хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="accc4-170">tooallow автоматизации Azure tooset значения секрета в хранилище ключей, необходимо получить идентификатор клиента hello hello подключения с именем AzureRunAsConnection, который был создан при установке экземпляра службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="accc4-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="accc4-171">Это значение можно получить в окне **Активы** в экземпляре службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="accc4-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="accc4-172">После этого выберите **подключений** , а затем выберите hello **AzureRunAsConnection** участника службы.</span><span class="sxs-lookup"><span data-stu-id="accc4-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="accc4-173">Запишите hello **идентификатор приложения**.</span><span class="sxs-lookup"><span data-stu-id="accc4-173">Take note of hello **Application ID**.</span></span>

![Идентификатор клиента службы автоматизации Azure](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="accc4-175">В окне **Активы** выберите пункт **Модули**.</span><span class="sxs-lookup"><span data-stu-id="accc4-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="accc4-176">Из **модули**выберите **коллекции**и выполните поиск и **импорта** обновленные версии hello следующие модули:</span><span class="sxs-lookup"><span data-stu-id="accc4-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="accc4-177">В hello написания данной статьи, hello toobe было отмечено выше модули, необходимые обновляется только для hello, выполнив сценарий.</span><span class="sxs-lookup"><span data-stu-id="accc4-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="accc4-178">Если задание по автоматизации завершится сбоем, убедитесь, что вы импортировали все необходимые модули и зависимости.</span><span class="sxs-lookup"><span data-stu-id="accc4-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="accc4-179">После получения идентификатора приложения hello для подключения к службе автоматизации Azure необходимо сообщить хранилища ключей, что это приложение имеет доступ tooupdate секреты в хранилище.</span><span class="sxs-lookup"><span data-stu-id="accc4-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="accc4-180">Это можно сделать с помощью hello следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="accc4-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="accc4-181">В экземпляре службы автоматизации Azure выберите пункт **Модули Runbook**, а затем — **Добавить Runbook**.</span><span class="sxs-lookup"><span data-stu-id="accc4-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="accc4-182">Выберите **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="accc4-182">Select **Quick Create**.</span></span> <span data-ttu-id="accc4-183">Имя модуля runbook и выберите **PowerShell** как тип runbook hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="accc4-184">У вас есть параметр tooadd hello описание.</span><span class="sxs-lookup"><span data-stu-id="accc4-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="accc4-185">Наконец, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="accc4-185">Finally, click **Create**.</span></span>

![Создание модуля Runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="accc4-187">Вставьте следующий сценарий PowerShell hello область редактора для новый модуль runbook hello:</span><span class="sxs-lookup"><span data-stu-id="accc4-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
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

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="accc4-188">Панели редактора hello выберите **области тестов** tootest сценария.</span><span class="sxs-lookup"><span data-stu-id="accc4-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="accc4-189">После hello сценарий выполняется без ошибок, можно выбрать **публикации**, и примените расписание для runbook hello обратно в область конфигурации hello runbook.</span><span class="sxs-lookup"><span data-stu-id="accc4-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="accc4-190">Конвейер аудита для хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="accc4-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="accc4-191">При настройке хранилища ключей можно включить аудит toocollect журналы на запросы доступа toohello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="accc4-192">Эти журналы хранятся в назначенной учетной записи службы хранилища Azure. Их можно извлекать, отслеживать и анализировать.</span><span class="sxs-lookup"><span data-stu-id="accc4-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="accc4-193">Hello следующий сценарий использует функций Azure, Azure логику приложения и toocreate журналы аудита хранилища ключей toosend конвейера сообщение электронной почты при приложения, которое соответствует идентификатор приложения hello веб-приложения hello извлекает секретные данные из хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="accc4-194">Сначала нужно включить ведение журнала в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="accc4-195">Это можно сделать с помощью следующих команд PowerShell hello (полные сведения отображаются на [ключ хранилища ведения журнала](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="accc4-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="accc4-196">После включения это журналы аудита начала сбор в hello, назначенные учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="accc4-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="accc4-197">В этих журналах содержатся сведения о том, кто, как и когда осуществлял доступ к хранилищам ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="accc4-198">Данные ведения журнала можно открыть 10 минут после операции hello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="accc4-199">Обычно они доступны даже раньше.</span><span class="sxs-lookup"><span data-stu-id="accc4-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="accc4-200">Hello следующим шагом является слишком[Создание очереди служебной шины Azure](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="accc4-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="accc4-201">Туда будут помещаться журналы аудита хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="accc4-202">Если hello очереди сообщений в журнале аудита hello, приложение hello логику их собирают и работает с ними.</span><span class="sxs-lookup"><span data-stu-id="accc4-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="accc4-203">Создание служебной шины с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="accc4-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="accc4-204">Создание пространства имен Service Bus (если это уже сделано, который будет toouse для этого пропустите tooStep 2).</span><span class="sxs-lookup"><span data-stu-id="accc4-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="accc4-205">Обзор toohello служебной шины в hello портал Azure и выберите приветствия имен toocreate hello очереди в требуемый.</span><span class="sxs-lookup"><span data-stu-id="accc4-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="accc4-206">Выберите **New** и выберите **Service Bus > очереди** и введите сведения о необходимых hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="accc4-207">Выберите сведения о соединении Service Bus hello путем выбора имен hello и щелкнув **сведения о соединении**.</span><span class="sxs-lookup"><span data-stu-id="accc4-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="accc4-208">Эти сведения понадобятся для следующего раздела hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="accc4-209">Далее, [создать Azure функцию](../azure-functions/functions-create-first-azure-function.md) toopoll хранилища ключей в hello учетной записи хранилища и журналы получают новые события.</span><span class="sxs-lookup"><span data-stu-id="accc4-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="accc4-210">Эта функция будет запускаться по расписанию.</span><span class="sxs-lookup"><span data-stu-id="accc4-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="accc4-211">Выберите toocreate функцию Azure **Создать > функции приложения** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="accc4-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="accc4-212">Можно использовать для этого действующий план размещения или создать новый.</span><span class="sxs-lookup"><span data-stu-id="accc4-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="accc4-213">Кроме того, можно использовать динамическое размещение.</span><span class="sxs-lookup"><span data-stu-id="accc4-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="accc4-214">Дополнительные сведения о функции вариантов размещения можно найти в [как tooscale функции Azure](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="accc4-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="accc4-215">При создании hello Azure функция tooit перейдите и выберите таймер, функции и C\#.</span><span class="sxs-lookup"><span data-stu-id="accc4-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="accc4-216">Затем щелкните **Создать эту функцию**.</span><span class="sxs-lookup"><span data-stu-id="accc4-216">Then click **Create this function**.</span></span>

![Начальная колонка функций Azure](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="accc4-218">На hello **разработка** вкладки, замените код run.csx hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="accc4-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

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
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
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

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
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

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="accc4-219">Создайте переменные hello tooreplace убедиться, что предшествующий учетной записи хранилища tooyour toopoint код которой записи журналов хранилища ключей hello, hello hello служебной шины, который был создан ранее, и hello журналы хранения определенный путь toohello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="accc4-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="accc4-220">функции Hello собирают hello последний файл журнала из учетной записи хранения hello где hello хранилища ключей журналы записываются, грабс hello последние события из этого файла и помещает в очередь Service Bus tooa.</span><span class="sxs-lookup"><span data-stu-id="accc4-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="accc4-221">Так как один файл может иметь несколько событий, необходимо создать файл sync.txt, который также отслеживает функции hello toodetermine hello отметку времени последнего события hello, который был выбран.</span><span class="sxs-lookup"><span data-stu-id="accc4-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="accc4-222">Это гарантирует, что не push hello того же события несколько раз.</span><span class="sxs-lookup"><span data-stu-id="accc4-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="accc4-223">Этот файл sync.txt содержит отметку времени для последнего события обнаружен hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="accc4-224">Hello журналов, при загрузке имеют toobe сортируются на основе в неправильном порядке tooensure timestamp hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="accc4-225">Для этой функции мы ссылаться на несколько дополнительных библиотек, которые недоступны в соответствующем hello в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="accc4-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="accc4-226">tooinclude, нам нужно функции Azure toopull их с помощью NuGet.</span><span class="sxs-lookup"><span data-stu-id="accc4-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="accc4-227">Выберите hello **Просмотр файлов** параметр.</span><span class="sxs-lookup"><span data-stu-id="accc4-227">Choose hello **View Files** option.</span></span>

![Элемент "Просмотреть файлы"](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="accc4-229">Затем добавьте новый файл project.json со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="accc4-229">And add a file called project.json with following content:</span></span>

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
<span data-ttu-id="accc4-230">После **Сохранить**, функции Azure будут загружать необходимые hello двоичных файлов.</span><span class="sxs-lookup"><span data-stu-id="accc4-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="accc4-231">Переключение toohello **Интеграция** вкладку и предоставьте параметр таймера hello toouse понятное имя в пределах функции hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="accc4-232">В hello предшествующий код, ожидается, что называется toobe таймера hello *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="accc4-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="accc4-233">Укажите [выражение CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) следующим образом: 0 \* \* \* \* \* для hello таймер, который вызовет toorun функции hello раз в минуту.</span><span class="sxs-lookup"><span data-stu-id="accc4-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="accc4-234">На hello же **Интеграция** добавьте входные данные типа hello **хранилища больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="accc4-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="accc4-235">Это будет указывать toohello sync.txt файл, который содержит hello отметка времени последнего события hello рассказывали функцией hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="accc4-236">Он будет доступен в рамках функции hello по имени параметра hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="accc4-237">В предыдущих кода hello, входные данные для хранилища больших двоичных объектов hello ожидает toobe имя параметра hello *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="accc4-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="accc4-238">Выберите учетную запись хранения hello, где будет находиться файл sync.txt hello (это может быть hello же или другую учетную запись хранения).</span><span class="sxs-lookup"><span data-stu-id="accc4-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="accc4-239">В поля "путь" hello укажите путь hello, где находятся файл hello в формате hello {container-name}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="accc4-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="accc4-240">Добавление выходных данных типа hello *хранилища больших двоичных объектов* выходных данных.</span><span class="sxs-lookup"><span data-stu-id="accc4-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="accc4-241">Указывает файл sync.txt toohello, заданных в hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="accc4-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="accc4-242">Это значение используется hello функция toowrite hello отметка времени последнего события hello рассмотрены.</span><span class="sxs-lookup"><span data-stu-id="accc4-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="accc4-243">Hello предыдущий код ожидает, что этот параметр, toobe вызывается *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="accc4-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="accc4-244">На этом этапе функция hello готов.</span><span class="sxs-lookup"><span data-stu-id="accc4-244">At this point, hello function is ready.</span></span> <span data-ttu-id="accc4-245">Сделать задней toohello убедиться, что tooswitch **разработка** вкладку и сохранение кода hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="accc4-246">Проверьте hello в окне вывода ошибок компиляции и исправьте их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="accc4-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="accc4-247">При компиляции кода hello, кода hello должны теперь проверять хранилище ключей журналы hello каждую минуту, и помещает новые события на hello определенные очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="accc4-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="accc4-248">Должны появиться сведения о ведении журнала, которые записывают окно журнала toohello каждый раз при запуске функции hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="accc4-249">Приложение логики Azure</span><span class="sxs-lookup"><span data-stu-id="accc4-249">Azure logic app</span></span>
<span data-ttu-id="accc4-250">Далее необходимо создать приложение Azure логику, забирает hello событий, что функции hello внедряет toohello очереди Service Bus, выполняет синтаксический анализ содержимого hello и отправляет сообщение электронной почты, на основе условия сравниваемыми.</span><span class="sxs-lookup"><span data-stu-id="accc4-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="accc4-251">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md) перейдя слишком**Создать > приложения логики**.</span><span class="sxs-lookup"><span data-stu-id="accc4-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="accc4-252">После создания приложения hello логики tooit перейдите и выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="accc4-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="accc4-253">Выбрать в редакторе логику приложения hello **очередь Service Bus** и введите ваш tooconnect учетные данные шины обслуживания его toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="accc4-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Служебная шина приложения логики Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="accc4-255">Затем выберите команду **Добавить условие**.</span><span class="sxs-lookup"><span data-stu-id="accc4-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="accc4-256">В условии hello переключения toohello расширенный редактор и введите hello после кода, заменив APP_ID hello фактическое APP_ID веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="accc4-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="accc4-257">По сути, это выражение возвращает **false** Если hello *appid* из hello не hello входящего события (который является текст hello сообщения hello Service Bus) *appid* из hello приложение.</span><span class="sxs-lookup"><span data-stu-id="accc4-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="accc4-258">Теперь создайте действие в разделе **If no, do nothing…** (Если нет, ничего не предпринимать).</span><span class="sxs-lookup"><span data-stu-id="accc4-258">Now, create an action under **If no, do nothing**.</span></span>

![Выбор действия приложения логики Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="accc4-260">Действие hello выберите **Office 365 — отправлять по электронной почте**.</span><span class="sxs-lookup"><span data-stu-id="accc4-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="accc4-261">Заполните поля toocreate hello toosend электронной почты при hello определено условие возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="accc4-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="accc4-262">Если у вас Office 365, вам увидеть альтернативы tooachieve hello одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="accc4-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="accc4-263">В этот момент у вас есть окончания tooend конвейера, который ищет новые журналы аудита хранилища ключей, раз в минуту.</span><span class="sxs-lookup"><span data-stu-id="accc4-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="accc4-264">Он помещает новые журналы, он находит tooa очередь service bus.</span><span class="sxs-lookup"><span data-stu-id="accc4-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="accc4-265">приложения логики Hello срабатывает, когда новое сообщение попадает в очередь hello.</span><span class="sxs-lookup"><span data-stu-id="accc4-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="accc4-266">Если hello *appid* внутри hello событий не соответствует идентификатор приложения hello вызов приложения hello, он отправляет сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="accc4-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
