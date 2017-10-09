---
title: "Хранилище ключей Azure с использованием интерфейса CLI aaaManage | Документы Microsoft"
description: "Использование этого учебника tooautomate типичных задач в хранилище ключей с помощью hello CLI 2.0"
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
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="dc27f-103">Управление Key Vault с помощью интерфейса командной строки 2.0</span><span class="sxs-lookup"><span data-stu-id="dc27f-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="dc27f-104">Хранилище ключей Azure доступно в большинстве регионов.</span><span class="sxs-lookup"><span data-stu-id="dc27f-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="dc27f-105">Дополнительные сведения см. в разделе hello [страница цен в хранилище ключей](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="dc27f-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="dc27f-106">Введение</span><span class="sxs-lookup"><span data-stu-id="dc27f-106">Introduction</span></span>
<span data-ttu-id="dc27f-107">Использовать этот учебник toohelp, вы получаете работы с хранилищем ключей Azure toocreate жесткой контейнера (хранилище) в Azure, toostore и управлять ими, криптографические ключи и секретные данные в Azure.</span><span class="sxs-lookup"><span data-stu-id="dc27f-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="dc27f-108">Помогает выполнить процесс с помощью интерфейса командной строки Azure кросс-платформенных toocreate hello хранилище, в котором содержится ключ или пароль, который затем можно использовать вместе с приложением Azure.</span><span class="sxs-lookup"><span data-stu-id="dc27f-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="dc27f-109">В нем также показано, как приложение может использовать этот ключ или пароль в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="dc27f-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="dc27f-110">**Предполагаемое время toocomplete:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="dc27f-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="dc27f-111">Этот учебник включает инструкции о том, как toowrite hello приложения Azure, в котором один из шагов hello, показывающий, как tooauthorize приложения toouse ключа или секрета в ключе hello хранилище.</span><span class="sxs-lookup"><span data-stu-id="dc27f-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="dc27f-112">В этом учебнике используется hello последнюю 2.0 Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="dc27f-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="dc27f-113">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="dc27f-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc27f-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dc27f-114">Prerequisites</span></span>
<span data-ttu-id="dc27f-115">toocomplete этого учебника необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="dc27f-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="dc27f-116">TooMicrosoft подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="dc27f-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="dc27f-117">Если у вас нет подписки, вы можете зарегистрироваться для использования [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial);</span><span class="sxs-lookup"><span data-stu-id="dc27f-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="dc27f-118">Интерфейс командной строки версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dc27f-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="dc27f-119">tooinstall hello последнюю версию и подключите tooyour подписки Azure в разделе [Установка и настройка hello Azure 2.0 интерфейс командной строки кросс-платформенных](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dc27f-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="dc27f-120">Приложение, настроенное toouse hello ключ или пароль, который создан в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="dc27f-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="dc27f-121">Образец приложения доступно из hello [центра загрузки Майкрософт](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="dc27f-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="dc27f-122">Инструкции см. в файле Readme, сопровождающие hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="dc27f-123">Справка по межплатформенному интерфейсу командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="dc27f-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="dc27f-124">В этом учебнике предполагается, что вы знакомы с интерфейсом командной строки hello (Bash, терминалов, Командная строка)</span><span class="sxs-lookup"><span data-stu-id="dc27f-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="dc27f-125">Hello--справки или -h параметр можно использовать tooview справки для определенных команд.</span><span class="sxs-lookup"><span data-stu-id="dc27f-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="dc27f-126">Кроме того hello azure help [команда] [параметры] формата также можно использовать tooreturn hello одинаковые сведения.</span><span class="sxs-lookup"><span data-stu-id="dc27f-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="dc27f-127">Например, hello следующие команды возвращают все hello одинаковые сведения:</span><span class="sxs-lookup"><span data-stu-id="dc27f-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="dc27f-128">В случае сомнений о hello параметров, используемых в команде ссылаться с помощью toohelp--Справка "," -h "или" az help [команда].</span><span class="sxs-lookup"><span data-stu-id="dc27f-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="dc27f-129">Также можно прочитать следующие учебники tooget знакомы с помощью диспетчера ресурсов Azure в интерфейс командной строки Azure кросс-платформенных hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="dc27f-130">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dc27f-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* <span data-ttu-id="dc27f-131">[Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) (Приступая к работе с Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="dc27f-131">[Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)</span></span>

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="dc27f-132">Подключение tooyour подписки</span><span class="sxs-lookup"><span data-stu-id="dc27f-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="dc27f-133">toolog с помощью учетной записи организации, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dc27f-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="dc27f-134">или если требуется toolog в интерактивном режиме введите</span><span class="sxs-lookup"><span data-stu-id="dc27f-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="dc27f-135">Если есть несколько подписок и требуется toospecify конкретных один toouse для хранилища ключей Azure, введите hello, следуя toosee hello подписки для учетной записи:</span><span class="sxs-lookup"><span data-stu-id="dc27f-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="dc27f-136">Затем toospecify hello подписки toouse, тип:</span><span class="sxs-lookup"><span data-stu-id="dc27f-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="dc27f-137">Дополнительные сведения о настройке кроссплатформенного интерфейса командной строки Azure см. в разделе [Установка Azure CLI 1.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dc27f-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="dc27f-138">Создание новой группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="dc27f-138">Create a new resource group</span></span>
<span data-ttu-id="dc27f-139">При использовании диспетчера ресурсов Azure все связанные ресурсы создаются внутри группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dc27f-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="dc27f-140">Для примера мы создадим новую группу ресурсов с именем ContosoResourceGroup:</span><span class="sxs-lookup"><span data-stu-id="dc27f-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="dc27f-141">Hello первым параметром является имя группы ресурсов, если второй параметр hello расположение hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="dc27f-142">Для расположения, используйте команду hello `az account list-locations` tooidentify как toospecify альтернативное расположение toohello один в этом примере.</span><span class="sxs-lookup"><span data-stu-id="dc27f-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="dc27f-143">Если вам необходима дополнительная информация, введите `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="dc27f-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="dc27f-144">Регистрация поставщика ресурсов хранилища ключей hello</span><span class="sxs-lookup"><span data-stu-id="dc27f-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="dc27f-145">Убедитесь, что поставщик ресурсов хранилища ключей зарегистрирован в вашей подписке:</span><span class="sxs-lookup"><span data-stu-id="dc27f-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="dc27f-146">Это достаточно выполнить один раз для каждой подписки toobe.</span><span class="sxs-lookup"><span data-stu-id="dc27f-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="dc27f-147">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="dc27f-147">Create a key vault</span></span>
<span data-ttu-id="dc27f-148">Используйте hello `az keyvault create` toocreate команда хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="dc27f-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="dc27f-149">Этот сценарий имеет три обязательных параметра: имя группы ресурсов, имя хранилища ключей и географическое расположение hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="dc27f-150">Например если вы используете hello хранилище с именем ContosoKeyVault hello группу ресурсов с именем ContosoResourceGroup и расположение hello Восточная Азия, введите:</span><span class="sxs-lookup"><span data-stu-id="dc27f-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="dc27f-151">выходные данные этой команды Hello отображает свойства hello хранилища ключей, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="dc27f-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="dc27f-152">Hello двух наиболее важных свойств:</span><span class="sxs-lookup"><span data-stu-id="dc27f-152">hello two most important properties are:</span></span>

* <span data-ttu-id="dc27f-153">**имя**: пример hello это ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="dc27f-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="dc27f-154">Вы будете использовать это имя для выполнения других команд Key Vault.</span><span class="sxs-lookup"><span data-stu-id="dc27f-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="dc27f-155">**vaultUri**: пример hello это https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="dc27f-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="dc27f-156">Необходимо, чтобы приложения, использующие ваше хранилище через REST API, использовали этот URI.</span><span class="sxs-lookup"><span data-stu-id="dc27f-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="dc27f-157">Учетная запись Azure — теперь авторизованным tooperform все операции в этот ключ в хранилище.</span><span class="sxs-lookup"><span data-stu-id="dc27f-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="dc27f-158">Пока что это недоступно для других учетных записей.</span><span class="sxs-lookup"><span data-stu-id="dc27f-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="dc27f-159">Добавление ключа или секрета toohello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="dc27f-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="dc27f-160">Хранилище ключей Azure toocreate программно защищенного ключа для вас, используйте hello `az key create` команд и введите hello ниже:</span><span class="sxs-lookup"><span data-stu-id="dc27f-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="dc27f-161">Тем не менее при наличии существующего ключа в PEM-файл сохранен как локальный файл в файл с именем softkey.pem, что требуется tooupload tooAzure хранилище ключей, введите следующую tooimport hello ключ из hello hello. PEM-файла, который защищает hello с помощью программного обеспечения в hello службы хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="dc27f-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="dc27f-162">Теперь можно ссылаться на ключ hello, созданные или переданные tooAzure хранилище ключей с помощью URI-адрес.</span><span class="sxs-lookup"><span data-stu-id="dc27f-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="dc27f-163">Используйте **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways получения текущей версии hello и **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget этой конкретной версии.</span><span class="sxs-lookup"><span data-stu-id="dc27f-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="dc27f-164">tooadd секретный toohello хранилища, которой это пароль SQLPassword с именем и значением hello Pa$ $w0rd tooAzure хранилище ключей, тип hello следующие:</span><span class="sxs-lookup"><span data-stu-id="dc27f-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="dc27f-165">Теперь можно ссылаться на этот пароль добавили tooAzure хранилище ключей с помощью URI-адрес.</span><span class="sxs-lookup"><span data-stu-id="dc27f-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="dc27f-166">Используйте **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways получения текущей версии hello и **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget этой конкретной версии.</span><span class="sxs-lookup"><span data-stu-id="dc27f-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="dc27f-167">Позволяет просмотреть hello ключа или секрета, который вы только что создали:</span><span class="sxs-lookup"><span data-stu-id="dc27f-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="dc27f-168">tooview вашей, введите:`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="dc27f-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="dc27f-169">tooview в тайне, тип:`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="dc27f-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="dc27f-170">Зарегистрируйте приложение с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc27f-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="dc27f-171">Обычно этот шаг выполняет разработчик на отдельном компьютере.</span><span class="sxs-lookup"><span data-stu-id="dc27f-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="dc27f-172">Он не является tooAzure конкретного хранилища ключей, но указан, для обеспечения полноты.</span><span class="sxs-lookup"><span data-stu-id="dc27f-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc27f-173">Учебник toocomplete hello, учетная запись, хранилище hello и приложения hello, которое будет зарегистрирован на этом шаге необходимо в hello один каталог Azure.</span><span class="sxs-lookup"><span data-stu-id="dc27f-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="dc27f-174">Приложения, которые используют хранилища ключей, должны пройти аутентификацию с использованием токена Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc27f-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="dc27f-175">toodo, hello владелец приложения hello сначала необходимо зарегистрировать приложение hello в своем Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc27f-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="dc27f-176">В конце hello регистрации владелец приложения hello возвращает hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="dc27f-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="dc27f-177">**Идентификатор приложения** (также известный как идентификатор клиента) и **ключ проверки подлинности** (также известный как общий секрет hello).</span><span class="sxs-lookup"><span data-stu-id="dc27f-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="dc27f-178">приложение Hello должен представить оба этих значения tooAzure Active Directory, tooget маркер.</span><span class="sxs-lookup"><span data-stu-id="dc27f-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="dc27f-179">Как приложение hello настраивается toodo это зависит от приложения hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="dc27f-180">Для hello образец приложения хранилища ключей владелец приложения hello устанавливает эти значения в файле app.config hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="dc27f-181">приложение hello tooregister в Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="dc27f-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="dc27f-182">Войдите в систему toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dc27f-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="dc27f-183">В левой части экрана приветствия щелкните **Azure Active Directory**и выберите каталог hello, в котором будет зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="dc27f-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="dc27f-184">Необходимо выбрать hello каталоге, содержащем hello подписки Azure, в которой для создания хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="dc27f-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="dc27f-185">Если вы не знаете, какой каталог это, нажмите кнопку **параметры**идентификации hello подписки, в которой для создания хранилища ключей и Примечание hello hello directory название hello последнего столбца.</span><span class="sxs-lookup"><span data-stu-id="dc27f-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="dc27f-186">Щелкните **ПРИЛОЖЕНИЯ**.</span><span class="sxs-lookup"><span data-stu-id="dc27f-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="dc27f-187">Если приложения не были добавлены tooyour каталога, эта страница отобразит только hello **добавить приложение** ссылку.</span><span class="sxs-lookup"><span data-stu-id="dc27f-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="dc27f-188">Щелкните ссылку hello, или в качестве альтернативы можно щелкнуть hello **добавить** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="dc27f-189">В hello **добавить приложение** мастера hello **что вам требуется toodo?** щелкните **добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="dc27f-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="dc27f-190">На hello **Расскажите о своем приложении** укажите имя для вашего приложения и выберите **веб-приложение и/или WEB API** (по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="dc27f-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="dc27f-191">Щелкните значок "следующий" hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="dc27f-192">На hello **свойства приложения** укажите hello **URL-адрес входа** и **URI идентификатора приложения** для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="dc27f-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="dc27f-193">Если в вашем приложении нет этих значений, можно придумать их для этого шага (например, можно указать http://test1.contoso.com в обоих полях).</span><span class="sxs-lookup"><span data-stu-id="dc27f-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="dc27f-194">Не важно, эти веб-сайты, если существует. Важно то, что URI идентификатора приложения hello для каждого приложения отличается для каждого приложения в каталоге.</span><span class="sxs-lookup"><span data-stu-id="dc27f-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="dc27f-195">каталог Hello используется этой строки tooidentify приложений.</span><span class="sxs-lookup"><span data-stu-id="dc27f-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="dc27f-196">Щелкните значок завершения toosave hello изменения в мастере hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="dc27f-197">На странице быстрого запуска приветствия щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="dc27f-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="dc27f-198">Прокрутите toohello **ключей** выберите длительность hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dc27f-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="dc27f-199">Страница приветствия обновляется и теперь отображается значение ключа.</span><span class="sxs-lookup"><span data-stu-id="dc27f-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="dc27f-200">Необходимо настроить приложение с таким значением ключа и hello **идентификатор КЛИЕНТА** значение.</span><span class="sxs-lookup"><span data-stu-id="dc27f-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="dc27f-201">(указания по этой конфигурации зависят от конкретного приложения).</span><span class="sxs-lookup"><span data-stu-id="dc27f-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="dc27f-202">На этой странице, который будет использоваться в hello следующий шаг tooset разрешения на ваше хранилище, скопируйте значение идентификатора клиента hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="dc27f-203">Авторизовать hello приложения toouse hello ключа или секрета</span><span class="sxs-lookup"><span data-stu-id="dc27f-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="dc27f-204">tooaccess приложения hello tooauthorize hello ключа или секрета в хранилище hello, используйте hello `az keyvault set-policy` команды.</span><span class="sxs-lookup"><span data-stu-id="dc27f-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="dc27f-205">Например если имя хранилища — ContosoKeyVault и hello приложения требуется tooauthorize имеет идентификатор клиента 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, и вы хотите toodecrypt приложения hello tooauthorize и войдите с ключами в хранилище, а затем запустите hello следующие:</span><span class="sxs-lookup"><span data-stu-id="dc27f-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="dc27f-206">Tooauthorize этой же tooread секреты приложения в хранилище, выполните следующие hello:</span><span class="sxs-lookup"><span data-stu-id="dc27f-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="dc27f-207">Если требуется, чтобы toouse аппаратный модуль безопасности (HSM)</span><span class="sxs-lookup"><span data-stu-id="dc27f-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="dc27f-208">Для повышения надежности можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM), никогда не покидают границ HSM hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="dc27f-209">Hello аппаратные модули безопасности являются FIPS 140-2 уровня 2 проверки.</span><span class="sxs-lookup"><span data-stu-id="dc27f-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="dc27f-210">Если это требование не распространяется tooyou, пропустите этот раздел и перейдите слишком[удалить hello хранилища ключей и связанные ключи и секретные данные](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="dc27f-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="dc27f-211">toocreate этих ключей, защищенных HSM, необходимо иметь подписку хранилища, который поддерживает ключей, защищенных HSM.</span><span class="sxs-lookup"><span data-stu-id="dc27f-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="dc27f-212">При создании hello keyvault, добавьте параметр «Конфигурация» hello:</span><span class="sxs-lookup"><span data-stu-id="dc27f-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="dc27f-213">Можно добавить программно защищенных ключей (как показано выше) и хранилище ключей, защищенных HSM toothis.</span><span class="sxs-lookup"><span data-stu-id="dc27f-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="dc27f-214">toocreate Перенос аппаратно защищенного ключа набора hello назначения параметра too'HSM ":</span><span class="sxs-lookup"><span data-stu-id="dc27f-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="dc27f-215">Можно использовать следующую команду tooimport ключа из PEM-файл на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="dc27f-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="dc27f-216">Эта команда импортирует ключ hello в аппаратные модули безопасности в hello службы хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="dc27f-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="dc27f-217">Hello следующая команда импортирует «принеси свой собственный ключ» (BYOK) пакета.</span><span class="sxs-lookup"><span data-stu-id="dc27f-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="dc27f-218">Это дает возможность создания ключа в ваш локальный HSM и передачи tooHSMs в hello службы хранилища ключей без ключа hello, оставляя границ HSM hello:</span><span class="sxs-lookup"><span data-stu-id="dc27f-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="dc27f-219">Более подробные инструкции о том, как toogenerate этот пакет BYOK разделе [как toouse HSM-Protected ключи с хранилищем ключей Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="dc27f-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="dc27f-220">Удаление хранилища ключей hello и связанные ключи и секретные данные</span><span class="sxs-lookup"><span data-stu-id="dc27f-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="dc27f-221">Если вы больше не нужна hello хранилища ключей и hello ключа или секрета, который его содержит, можно удалить hello хранилища ключей с помощью hello `az keyvault delete` команды:</span><span class="sxs-lookup"><span data-stu-id="dc27f-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="dc27f-222">Или можно удалить группы весь ресурс Azure, которая включает в себя хранилище ключей hello и другие ресурсы, которые включены в эту группу:</span><span class="sxs-lookup"><span data-stu-id="dc27f-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="dc27f-223">Другие команды в межплатформенном интерфейсе командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="dc27f-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="dc27f-224">Вот другие команды, которые могут быть полезны при управлении хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="dc27f-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="dc27f-225">Эта команда перечисляет все ключи и выбранные свойства в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="dc27f-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="dc27f-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="dc27f-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="dc27f-227">Эта команда отображает полный список свойств для указанного ключа hello:</span><span class="sxs-lookup"><span data-stu-id="dc27f-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="dc27f-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="dc27f-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="dc27f-229">Эта команда перечисляет все имена секретов и выбранные свойства в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="dc27f-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="dc27f-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="dc27f-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="dc27f-231">Ниже приведен пример того, как tooremove определенного ключа:</span><span class="sxs-lookup"><span data-stu-id="dc27f-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="dc27f-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="dc27f-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="dc27f-233">Ниже приведен пример того, как tooremove конкретных секрет:</span><span class="sxs-lookup"><span data-stu-id="dc27f-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="dc27f-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="dc27f-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="dc27f-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc27f-235">Next steps</span></span>
<span data-ttu-id="dc27f-236">Полное описание команд Azure CLI для Key Vault доступно в [справочнике по интерфейсу командной строки Key Vault](/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="dc27f-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="dc27f-237">Программирование ссылки, в разделе [hello хранилище ключей Azure в руководстве разработчика](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="dc27f-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
