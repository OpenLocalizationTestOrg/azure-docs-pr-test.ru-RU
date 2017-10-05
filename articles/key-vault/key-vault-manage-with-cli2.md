---
title: "Управление Azure Key Vault с помощью интерфейса командной строки | Документация Майкрософт"
description: "В этом руководстве вы узнаете об автоматизации основных задач в Key Vault с использованием интерфейса командной строки 2.0."
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 5da9f5eceda71ac85259193e0f183c72813e1679
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="37732-103">Управление Key Vault с помощью интерфейса командной строки 2.0</span><span class="sxs-lookup"><span data-stu-id="37732-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="37732-104">Хранилище ключей Azure доступно в большинстве регионов.</span><span class="sxs-lookup"><span data-stu-id="37732-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="37732-105">Дополнительные сведения см. на странице [цен на хранилище ключей](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="37732-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="37732-106">Введение</span><span class="sxs-lookup"><span data-stu-id="37732-106">Introduction</span></span>
<span data-ttu-id="37732-107">Этот учебник поможет вам начать работу с хранилищем ключей Azure. В нем содержится информация о создании зафиксированного контейнера (хранилища), хранении криптографических ключей и секретов, а также об управлении ими в Azure.</span><span class="sxs-lookup"><span data-stu-id="37732-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="37732-108">Он представляет собой пошаговое руководство по использованию межплатформенного интерфейса командной строки Azure для создания хранилища, содержащего ключ или пароль, который вы сможете использовать с приложением Azure.</span><span class="sxs-lookup"><span data-stu-id="37732-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="37732-109">В нем также показано, как приложение может использовать этот ключ или пароль в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="37732-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="37732-110">**Предполагаемое время выполнения:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="37732-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="37732-111">В этом учебнике нет указаний по написанию приложения Azure, что предусматривает один из шагов, но показано, как авторизовать приложение для использования ключей или секретов в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="37732-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="37732-112">В этом руководстве используется последняя версия Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="37732-112">This tutorial uses the latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="37732-113">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="37732-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37732-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="37732-114">Prerequisites</span></span>
<span data-ttu-id="37732-115">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="37732-115">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="37732-116">подписка на Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="37732-116">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="37732-117">Если у вас нет подписки, вы можете зарегистрироваться для использования [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial);</span><span class="sxs-lookup"><span data-stu-id="37732-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="37732-118">Интерфейс командной строки версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="37732-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="37732-119">Сведения об установке последней версии и связывании ее с подпиской Azure можно найти в разделе [Установка Azure CLI 1.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="37732-119">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="37732-120">приложение, для которого вы будете настраивать использование ключа или пароля, созданного по этому учебнику.</span><span class="sxs-lookup"><span data-stu-id="37732-120">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="37732-121">Пример приложения доступен в [Центре загрузки Майкрософт](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="37732-121">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="37732-122">Указания см. в сопутствующем файле Readme.</span><span class="sxs-lookup"><span data-stu-id="37732-122">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="37732-123">Справка по межплатформенному интерфейсу командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="37732-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="37732-124">В этом учебнике предполагается, что вы знакомы с интерфейсом командной строки (Bash, терминал, командная строка)</span><span class="sxs-lookup"><span data-stu-id="37732-124">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="37732-125">Параметр --help или -h может использоваться для просмотра справки по определенным командам.</span><span class="sxs-lookup"><span data-stu-id="37732-125">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="37732-126">Также для получения справки можно использовать команду azure help [команда] [параметры].</span><span class="sxs-lookup"><span data-stu-id="37732-126">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="37732-127">Например, все следующие команды возвращают одинаковые сведения:</span><span class="sxs-lookup"><span data-stu-id="37732-127">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="37732-128">Если вы сомневаетесь в том, какие параметры необходимы команде, обратитесь к справке, используя параметр --help, -h или команду az help [команда].</span><span class="sxs-lookup"><span data-stu-id="37732-128">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="37732-129">Чтобы узнать, как работать с диспетчером ресурсов Azure в межплатформенном интерфейсе командной строки Azure, также прочитайте следующие руководства:</span><span class="sxs-lookup"><span data-stu-id="37732-129">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="37732-130">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="37732-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* <span data-ttu-id="37732-131">[Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) (Приступая к работе с Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="37732-131">[Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)</span></span>

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="37732-132">Подключение к своим подпискам</span><span class="sxs-lookup"><span data-stu-id="37732-132">Connect to your subscriptions</span></span>
<span data-ttu-id="37732-133">Чтобы войти с использованием учетной записи организации, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37732-133">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="37732-134">Или, чтобы войти при помощи ввода данных в интерактивном режиме:</span><span class="sxs-lookup"><span data-stu-id="37732-134">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="37732-135">Если у вас есть несколько подписок и нужно указать лишь одну из них, которая будет использоваться для хранилища ключей Azure, введите следующую команду, чтобы увидеть подписки своей учетной записи:</span><span class="sxs-lookup"><span data-stu-id="37732-135">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="37732-136">Далее, чтобы указать подписку, которую нужно использовать, введите:</span><span class="sxs-lookup"><span data-stu-id="37732-136">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="37732-137">Дополнительные сведения о настройке кроссплатформенного интерфейса командной строки Azure см. в разделе [Установка Azure CLI 1.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="37732-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="37732-138">Создание новой группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="37732-138">Create a new resource group</span></span>
<span data-ttu-id="37732-139">При использовании диспетчера ресурсов Azure все связанные ресурсы создаются внутри группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="37732-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="37732-140">Для примера мы создадим новую группу ресурсов с именем ContosoResourceGroup:</span><span class="sxs-lookup"><span data-stu-id="37732-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="37732-141">Первый параметр — имя группы ресурсов, а второй параметр — его расположение.</span><span class="sxs-lookup"><span data-stu-id="37732-141">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="37732-142">Для параметра расположения используйте команду `az account list-locations` , чтобы указать альтернативное расположение группы.</span><span class="sxs-lookup"><span data-stu-id="37732-142">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="37732-143">Если вам необходима дополнительная информация, введите `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="37732-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="37732-144">Регистрация поставщика ресурсов хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="37732-144">Register the Key Vault resource provider</span></span>
<span data-ttu-id="37732-145">Убедитесь, что поставщик ресурсов хранилища ключей зарегистрирован в вашей подписке:</span><span class="sxs-lookup"><span data-stu-id="37732-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="37732-146">Данную операцию достаточно выполнить один раз для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="37732-146">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="37732-147">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="37732-147">Create a key vault</span></span>
<span data-ttu-id="37732-148">Для создания хранилища ключей используйте команду `az keyvault create` .</span><span class="sxs-lookup"><span data-stu-id="37732-148">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="37732-149">Этот сценарий предусматривает три обязательных параметра: имя группы ресурсов, имя хранилища ключей и географическое расположение.</span><span class="sxs-lookup"><span data-stu-id="37732-149">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="37732-150">Например, если вы используете хранилище с именем ContosoKeyVault, группу ресурсов с именем ContosoResourceGroup и расположение "Восточная Азия", введите:</span><span class="sxs-lookup"><span data-stu-id="37732-150">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="37732-151">В выходных данных команды будут показаны свойства хранилища ключей, которое вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="37732-151">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="37732-152">Среди всех свойств есть два самых важных:</span><span class="sxs-lookup"><span data-stu-id="37732-152">The two most important properties are:</span></span>

* <span data-ttu-id="37732-153">**Имя**. В этом примере — ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="37732-153">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="37732-154">Вы будете использовать это имя для выполнения других команд Key Vault.</span><span class="sxs-lookup"><span data-stu-id="37732-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="37732-155">**URI хранилища.** В нашем примере — это https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="37732-155">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="37732-156">Необходимо, чтобы приложения, использующие ваше хранилище через REST API, использовали этот URI.</span><span class="sxs-lookup"><span data-stu-id="37732-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="37732-157">Теперь ваша учетная запись Azure авторизована, и вы можете выполнять любые операции в этом хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="37732-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="37732-158">Пока что это недоступно для других учетных записей.</span><span class="sxs-lookup"><span data-stu-id="37732-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="37732-159">Добавьте ключ или секретный код в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="37732-159">Add a key or secret to the key vault</span></span>
<span data-ttu-id="37732-160">Если вам необходимо создать ключ с программной защитой для собственного использования с помощью хранилища ключей Azure, используйте команду `az key create` и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="37732-160">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="37732-161">Однако если у вас уже есть ключ, сохраненный в виде локального PEM-файла с именем softkey.pem, который требуется загрузить в хранилище ключей Azure, воспользуйтесь следующей командой импорта ключа из PEM-файла, которая позволяет программным образом защитить ключ в службе хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="37732-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="37732-162">Теперь для доступа к ключу, созданному или загруженному в хранилище ключей Azure, вы сможете использовать его URI.</span><span class="sxs-lookup"><span data-stu-id="37732-162">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="37732-163">Используйте адрес **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey**, чтобы всегда получать текущую версию, и адрес **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87**, чтобы получить конкретную версию.</span><span class="sxs-lookup"><span data-stu-id="37732-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="37732-164">Чтобы добавить секрет в хранилище ключей Azure, который представляет собой пароль с именем SQLPassword и значением Pa$$w0rd, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="37732-164">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="37732-165">Теперь пароль, добавленный в хранилище ключей Azure, можно вызвать, используя его URI.</span><span class="sxs-lookup"><span data-stu-id="37732-165">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="37732-166">Используйте адрес **https://ContosoVault.vault.azure.net/secrets/SQLPassword**, чтобы всегда получать текущую версию, и адрес **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d**, чтобы получить конкретную версию.</span><span class="sxs-lookup"><span data-stu-id="37732-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="37732-167">Давайте просмотрим только что созданный ключ или секрет.</span><span class="sxs-lookup"><span data-stu-id="37732-167">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="37732-168">Чтобы просмотреть свой ключ, введите `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="37732-168">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="37732-169">Чтобы просмотреть свой секрет, введите `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="37732-169">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="37732-170">Зарегистрируйте приложение с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37732-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="37732-171">Обычно этот шаг выполняет разработчик на отдельном компьютере.</span><span class="sxs-lookup"><span data-stu-id="37732-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="37732-172">Он не относится к хранилищу ключей Azure, но включен в этот учебник для полноты картины.</span><span class="sxs-lookup"><span data-stu-id="37732-172">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37732-173">Чтобы завершить прохождение этого учебника, учетная запись, хранилище и приложение, которое вы будете регистрировать на этом шаге, должны находиться в одном каталоге Azure.</span><span class="sxs-lookup"><span data-stu-id="37732-173">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="37732-174">Приложения, которые используют хранилища ключей, должны пройти аутентификацию с использованием токена Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37732-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="37732-175">Для этого владельцу приложения необходимо сначала зарегистрировать приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37732-175">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="37732-176">В конце регистрации владелец приложения получает следующие значения.</span><span class="sxs-lookup"><span data-stu-id="37732-176">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="37732-177">**Идентификатор приложения** (также известный как идентификатор клиента) и **ключ проверки подлинности** (также известный как общий секрет).</span><span class="sxs-lookup"><span data-stu-id="37732-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="37732-178">Для получения токена приложение должно предоставить Azure Active Directory оба этих значения.</span><span class="sxs-lookup"><span data-stu-id="37732-178">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="37732-179">Настроенный способ предоставления зависит от приложения.</span><span class="sxs-lookup"><span data-stu-id="37732-179">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="37732-180">В примере приложения, использующего хранилище ключей, владелец задает эти значения в файле app.config.</span><span class="sxs-lookup"><span data-stu-id="37732-180">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="37732-181">Чтобы зарегистрировать приложение в Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="37732-181">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="37732-182">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="37732-182">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="37732-183">Слева щелкните **Azure Active Directory**, а затем выберите каталог, в котором вам необходимо зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="37732-183">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="37732-184">Вам необходимо выбрать каталог, содержащий подписку Azure, которую вы использовали для создания хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="37732-184">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="37732-185">Если вам не известно, какой это каталог, щелкните **Параметры**, найдите подписку, использованную для создания хранилища ключей, и запишите имя каталога, отображающегося в последнем столбце.</span><span class="sxs-lookup"><span data-stu-id="37732-185">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="37732-186">Щелкните **ПРИЛОЖЕНИЯ**.</span><span class="sxs-lookup"><span data-stu-id="37732-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="37732-187">Если в каталоге нет добавленных приложений, на этой странице отобразится только ссылка **Добавить приложение** .</span><span class="sxs-lookup"><span data-stu-id="37732-187">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="37732-188">Щелкните ссылку или, как вариант, можно щелкнуть **ДОБАВИТЬ** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="37732-188">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="37732-189">В мастере **Добавление приложения** на странице **What do you want to do?** (Что необходимо сделать?) щелкните **Добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="37732-189">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="37732-190">На странице **Расскажите о своем приложении** укажите имя своего приложения и выберите **Веб-приложение и/или веб-API** (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="37732-190">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="37732-191">Щелкните значок "Далее".</span><span class="sxs-lookup"><span data-stu-id="37732-191">Click the Next icon.</span></span>
6. <span data-ttu-id="37732-192">На странице **Свойства приложения** укажите данные в полях **URL-адрес входа** и **URI кода приложения** для своего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="37732-192">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="37732-193">Если в вашем приложении нет этих значений, можно придумать их для этого шага (например, можно указать http://test1.contoso.com в обоих полях).</span><span class="sxs-lookup"><span data-stu-id="37732-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="37732-194">Не важно, существуют ли эти сайты. Важно то, что URI кода приложения отличается для каждого приложения в каталоге.</span><span class="sxs-lookup"><span data-stu-id="37732-194">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="37732-195">Каталог использует эту строку для идентификации приложения.</span><span class="sxs-lookup"><span data-stu-id="37732-195">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="37732-196">Щелкните значок "Готово", чтобы сохранить изменения в мастере.</span><span class="sxs-lookup"><span data-stu-id="37732-196">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="37732-197">На странице «Быстрый запуск» щелкните **НАСТРОИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="37732-197">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="37732-198">Прокрутите страницу до раздела **Ключи**, выберите длительность и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="37732-198">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="37732-199">Страница обновится и отобразится значение ключа.</span><span class="sxs-lookup"><span data-stu-id="37732-199">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="37732-200">Необходимо настроить приложение, указав это значение ключа и **идентификатор клиента**</span><span class="sxs-lookup"><span data-stu-id="37732-200">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="37732-201">(указания по этой конфигурации зависят от конкретного приложения).</span><span class="sxs-lookup"><span data-stu-id="37732-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="37732-202">Скопируйте значение идентификатора клиента на этой странице. Вы будете использовать его на следующем шаге, чтобы задать разрешения в своем хранилище.</span><span class="sxs-lookup"><span data-stu-id="37732-202">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="37732-203">Разрешите приложению использовать ключ или секретный код.</span><span class="sxs-lookup"><span data-stu-id="37732-203">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="37732-204">Чтобы авторизовать приложение для получения доступа к ключу или секрету в хранилище, используйте команду `az keyvault set-policy` .</span><span class="sxs-lookup"><span data-stu-id="37732-204">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="37732-205">Например, если имя хранилища — ContosoKeyVault, а идентификатор клиента приложения — 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, и нужно авторизовать это приложение для расшифровки и подписи с использованием ключей в вашем хранилище, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="37732-205">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="37732-206">Если этому же приложению необходимо разрешить читать секретные данные в хранилище, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37732-206">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="37732-207">Использование аппаратного модуля безопасности</span><span class="sxs-lookup"><span data-stu-id="37732-207">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="37732-208">Чтобы обеспечить более высокий уровень защиты, можно импортировать ключи или создать их в аппаратных модулях безопасности (ключи никогда не покидают их пределов).</span><span class="sxs-lookup"><span data-stu-id="37732-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="37732-209">В качестве аппаратных модулей безопасности используются модули FIPS 140-2 с проверкой уровня 2.</span><span class="sxs-lookup"><span data-stu-id="37732-209">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="37732-210">Если это требование вас не касается, пропустите этот подраздел и перейдите к подразделу [Удаление хранилища ключей, а также связанных ключей и секретов](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="37732-210">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="37732-211">Чтобы создать ключи, защищенные аппаратным модулем безопасности, у вас должна быть подписка на хранилище, которая поддерживает ключи, защищенные аппаратным модулем безопасности.</span><span class="sxs-lookup"><span data-stu-id="37732-211">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="37732-212">При создании хранилища добавьте параметр sku:</span><span class="sxs-lookup"><span data-stu-id="37732-212">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="37732-213">В это хранилище можно добавлять ключи с программной защитой (как показано выше) и ключи, защищенные аппаратным модулем безопасности.</span><span class="sxs-lookup"><span data-stu-id="37732-213">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="37732-214">Чтобы создать ключ, защищенный аппаратным модулем безопасности, задайте значение HSM для параметра Destination:</span><span class="sxs-lookup"><span data-stu-id="37732-214">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="37732-215">Вы можете использовать следующую команду для импорта ключа из PEM-файла на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="37732-215">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="37732-216">Эта команда импортирует ключ в аппаратные модули безопасности в службе хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="37732-216">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="37732-217">Следующая команда импортирует пакет собственного ключа клиента (BYOK).</span><span class="sxs-lookup"><span data-stu-id="37732-217">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="37732-218">Это дает возможность создать ключ в своем локальном аппаратном модуле безопасности и передать его в аппаратные модули безопасности в службе хранилища ключей так, чтобы ключ не покидал их пределы:</span><span class="sxs-lookup"><span data-stu-id="37732-218">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="37732-219">Более подробные инструкции по созданию пакета BYOK см. в статье [Создание ключей, защищенных аппаратным модулем безопасности, и их передача в хранилище ключей Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="37732-219">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="37732-220">Удаление хранилища ключей, а также связанных ключей и секретов</span><span class="sxs-lookup"><span data-stu-id="37732-220">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="37732-221">Если больше нет необходимости в Key Vault и содержащемся в нем ключе или секрете, можно удалить его, используя команду `az keyvault delete`.</span><span class="sxs-lookup"><span data-stu-id="37732-221">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="37732-222">Как вариант, можно удалить всю группу ресурсов Azure, которая включает в себя хранилище ключей и другие ресурсы, которые вы добавили в эту группу:</span><span class="sxs-lookup"><span data-stu-id="37732-222">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="37732-223">Другие команды в межплатформенном интерфейсе командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="37732-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="37732-224">Вот другие команды, которые могут быть полезны при управлении хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="37732-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="37732-225">Эта команда перечисляет все ключи и выбранные свойства в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="37732-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="37732-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="37732-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="37732-227">Эта команда отображает полный список свойств для указанного ключа:</span><span class="sxs-lookup"><span data-stu-id="37732-227">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="37732-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="37732-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="37732-229">Эта команда перечисляет все имена секретов и выбранные свойства в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="37732-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="37732-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="37732-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="37732-231">Пример удаления конкретного ключа:</span><span class="sxs-lookup"><span data-stu-id="37732-231">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="37732-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="37732-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="37732-233">Пример удаления конкретного секрета:</span><span class="sxs-lookup"><span data-stu-id="37732-233">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="37732-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="37732-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="37732-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37732-235">Next steps</span></span>
<span data-ttu-id="37732-236">Полное описание команд Azure CLI для Key Vault доступно в [справочнике по интерфейсу командной строки Key Vault](/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="37732-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="37732-237">Справочные материалы по программированию см. в статье [Руководство разработчика хранилища ключей Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="37732-237">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
