---
title: "aaaGet работы с Azure CLI для пакета | Документы Microsoft"
description: "Получить краткое введение toohello пакетные команды в Azure CLI для управления ресурсами Azure пакетной службы"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="b7f1a-103">Управление ресурсами пакетной службы с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b7f1a-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="b7f1a-104">Hello Azure CLI 2.0 — это новый интерфейс командной строки Azure для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-104">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="b7f1a-105">Его можно использовать в Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="b7f1a-106">Azure CLI 2.0 оптимизирована для управления и администрирования из командной строки hello ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from hello command line.</span></span> <span data-ttu-id="b7f1a-107">Можно использовать toomanage hello Azure CLI, учетными записями пакетной службы Azure и toomanage ресурсы, такие как пулы, заданий и задач.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-107">You can use hello Azure CLI toomanage your Azure Batch accounts and toomanage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="b7f1a-108">С помощью hello Azure CLI, можно создать сценарий многие hello hello такие же задачи, выполняемые с помощью API-интерфейсы пакета, портал Azure и командлеты PowerShell для пакета.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-108">With hello Azure CLI, you can script many of hello same tasks you carry out with hello Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="b7f1a-109">В этой статье содержатся общие сведения об использовании [Azure CLI версии 2.0](https://docs.microsoft.com/cli/azure/overview) с пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="b7f1a-110">В разделе [Приступая к работе с Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) Общие сведения об использовании hello CLI с Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using hello CLI with Azure.</span></span>

<span data-ttu-id="b7f1a-111">Корпорация Майкрософт рекомендует использовать последнюю версию hello hello Azure CLI, версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-111">Microsoft recommends using hello latest version of hello Azure CLI, version 2.0.</span></span> <span data-ttu-id="b7f1a-112">Дополнительные сведения о ней см. в записи блога о [выпуске общедоступной версии Azure CLI 2.0](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-hello-azure-cli"></a><span data-ttu-id="b7f1a-113">Настройка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b7f1a-113">Set up hello Azure CLI</span></span>

<span data-ttu-id="b7f1a-114">tooinstall hello Azure CLI выполните hello действия, описанные в [Install hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-114">tooinstall hello Azure CLI, follow hello steps outlined in [Install hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="b7f1a-115">Рекомендуется обновить установленную Azure CLI часто tootake преимуществами службы обновления и улучшения.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-115">We recommend that you update your Azure CLI installation frequently tootake advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="b7f1a-116">Справка по командам</span><span class="sxs-lookup"><span data-stu-id="b7f1a-116">Command help</span></span>

<span data-ttu-id="b7f1a-117">Можно отобразить текст справки для всех команд в hello Azure CLI путем добавления `-h` toohello команды.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-117">You can display help text for every command in hello Azure CLI by appending `-h` toohello command.</span></span> <span data-ttu-id="b7f1a-118">Другие параметры следует опустить.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-118">Omit any other options.</span></span> <span data-ttu-id="b7f1a-119">Например:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-119">For example:</span></span>

* <span data-ttu-id="b7f1a-120">tooget справку для hello `az` , введите:`az -h`</span><span class="sxs-lookup"><span data-stu-id="b7f1a-120">tooget help for hello `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="b7f1a-121">tooget список всех команд пакета в hello CLI, используйте:`az batch -h`</span><span class="sxs-lookup"><span data-stu-id="b7f1a-121">tooget a list of all Batch commands in hello CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="b7f1a-122">tooget справку по созданию учетной записи пакета, введите:`az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="b7f1a-122">tooget help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="b7f1a-123">Если вы сомневаетесь, использовать hello `-h` справки tooget параметр командной строки на любую команду Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-123">When in doubt, use hello `-h` command-line option tooget help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="b7f1a-124">Более ранних версиях hello Azure CLI используется `azure` toopreface команду CLI.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-124">Earlier versions of hello Azure CLI used `azure` toopreface a CLI command.</span></span> <span data-ttu-id="b7f1a-125">В версии 2.0 все команды теперь начинаются с приставки `az`.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="b7f1a-126">Быть убедиться, что tooupdate сценариев toouse hello новый синтаксис с версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-126">Be sure tooupdate your scripts toouse hello new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="b7f1a-127">Кроме того, ссылаются toohello Azure CLI справочную документацию для сведений о [команды Azure CLI для пакета](https://docs.microsoft.com/cli/azure/batch).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-127">Additionally, refer toohello Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="b7f1a-128">Вход в систему и проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="b7f1a-128">Log in and authenticate</span></span>

<span data-ttu-id="b7f1a-129">toouse hello Azure CLI с использованием пакета, нужно toolog в и проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-129">toouse hello Azure CLI with Batch, you need toolog in and authenticate.</span></span> <span data-ttu-id="b7f1a-130">Существует два простых шагов toofollow:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-130">There are two simple steps toofollow:</span></span>

1. <span data-ttu-id="b7f1a-131">**Войдите в Azure.**</span><span class="sxs-lookup"><span data-stu-id="b7f1a-131">**Log into Azure.**</span></span> <span data-ttu-id="b7f1a-132">Вход в Azure дает доступ команд tooAzure диспетчера ресурсов, включая [обновления пакета управления](batch-management-dotnet.md) команд.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-132">Logging into Azure gives you access tooAzure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="b7f1a-133">**Войдите в учетную запись пакетной службы.**</span><span class="sxs-lookup"><span data-stu-id="b7f1a-133">**Log into your Batch account.**</span></span> <span data-ttu-id="b7f1a-134">Вход в ваш пакет учетной записи позволяет получить доступ к командам tooBatch службы.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-134">Logging into your Batch account gives you access tooBatch service commands.</span></span>   

### <a name="log-in-tooazure"></a><span data-ttu-id="b7f1a-135">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="b7f1a-135">Log in tooAzure</span></span>

<span data-ttu-id="b7f1a-136">Существует несколько способов toolog в Azure, подробно описаны в [войдите с помощью Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="b7f1a-136">There are a few different ways toolog into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="b7f1a-137">[Интерактивный вход.](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in)</span><span class="sxs-lookup"><span data-stu-id="b7f1a-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="b7f1a-138">Войти интерактивном режиме при выполнении команды Azure CLI самостоятельно hello командной строке.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-138">Log in interactively when you are running Azure CLI commands yourself from hello command line.</span></span>
2. <span data-ttu-id="b7f1a-139">[Вход с использованием субъекта-службы.](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal)</span><span class="sxs-lookup"><span data-stu-id="b7f1a-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="b7f1a-140">Используйте этот способ, если вы выполняете команды Azure CLI из скрипта или приложения.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="b7f1a-141">В целях hello данной статьи мы Показать как toolog в Azure интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-141">For hello purposes of this article, we show how toolog into Azure interactively.</span></span> <span data-ttu-id="b7f1a-142">Тип [входа az](https://docs.microsoft.com/cli/azure/#login) hello в командной строке:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on hello command line:</span></span>

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

<span data-ttu-id="b7f1a-143">Hello `az login` команда возвращает токен, можно использовать tooauthenticate, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-143">hello `az login` command returns a token that you can use tooauthenticate, as shown here.</span></span> <span data-ttu-id="b7f1a-144">Следуйте инструкциям hello tooopen веб-страницы и отправка маркера tooAzure hello:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-144">Follow hello instructions provided tooopen a web page and submit hello token tooAzure:</span></span>

![Войдите в tooAzure](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="b7f1a-146">Примеры Hello, перечисленные в hello [образцы сценариев оболочки](#sample-shell-scripts) статьи также показать как toostart сеанс Azure CLI, интерактивный вход в Azure.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-146">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section also show how toostart your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="b7f1a-147">После входа, можно вызвать toowork команд с ресурсами пакета управления, включая учетные записи пакета, ключи, пакеты приложений и квоты.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-147">Once you have logged in, you can call commands toowork with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-tooyour-batch-account"></a><span data-ttu-id="b7f1a-148">Войдите в tooyour пакетной учетной записи</span><span class="sxs-lookup"><span data-stu-id="b7f1a-148">Log in tooyour Batch account</span></span>

<span data-ttu-id="b7f1a-149">toouse hello Azure CLI toomanage пакет ресурсов, таких как пулы, заданий и задач, должны toolog в вашу учетную запись пакета и пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-149">toouse hello Azure CLI toomanage Batch resources, such as pools, jobs, and tasks, you need toolog into your Batch account and authenticate.</span></span> <span data-ttu-id="b7f1a-150">использовать toolog в toohello пакетная служба hello [учетную запись для входа пакетного az](https://docs.microsoft.com/cli/azure/batch/account#login) команды.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-150">toolog in toohello Batch service, use hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="b7f1a-151">Проверку подлинности в учетной записи пакетной службы можно пройти двумя способами:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="b7f1a-152">**Проверка подлинности Azure Active Directory (Azure AD).**</span><span class="sxs-lookup"><span data-stu-id="b7f1a-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="b7f1a-153">Проверки подлинности в Azure AD является использование hello Azure CLI с использованием пакета по умолчанию hello и рекомендуется для большинства сценариев.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-153">Authenticating with Azure AD is hello default when you use hello Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="b7f1a-154">При входе в tooAzure интерактивном режиме, как описано в предыдущем разделе hello, учетные данные кэшируются, поэтому hello Azure CLI можно входа в систему tooyour пакетной учетной записи, используя те же учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-154">When you log in tooAzure interactively, as described in hello previous section, your credentials are cached, so hello Azure CLI can log you in tooyour Batch account using those same credentials.</span></span> <span data-ttu-id="b7f1a-155">При входе в tooAzure участника службы с помощью этих учетных данных, также используется toolog в tooyour пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-155">If you log in tooAzure using a service principal, those credentials are also used toolog in tooyour Batch account.</span></span>

    <span data-ttu-id="b7f1a-156">Преимущество Azure AD заключается в том, что эта служба предоставляет управление доступом на основе ролей (RBAC).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="b7f1a-157">С RBAC доступа пользователя зависит от назначенной им роли, а не того, является ли они имеют hello ключи учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess hello account keys.</span></span> <span data-ttu-id="b7f1a-158">В этом случае управлять ключами не нужно. Вы просто назначаете роли RBAC, и Azure AD управляет параметрами доступа и проверки подлинности вместо вас.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="b7f1a-159">Проверка подлинности с помощью Azure AD является обязательным, если вы создали учетной записью пакетной службы Azure с помощью режима выделения пула задать too'User подписки ".</span><span class="sxs-lookup"><span data-stu-id="b7f1a-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set too'User Subscription'.</span></span> 

    <span data-ttu-id="b7f1a-160">toolog в tooyour пакетной учетной записи с помощью Azure AD, вызовите hello [учетную запись для входа пакетного az](https://docs.microsoft.com/cli/azure/batch/account#login) команды:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-160">toolog in tooyour Batch account using Azure AD, call hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="b7f1a-161">**Проверка подлинности на основе общего ключа.**</span><span class="sxs-lookup"><span data-stu-id="b7f1a-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="b7f1a-162">[Проверка подлинности с общим ключом](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) использует tooauthenticate команды Azure CLI для hello ключи доступ к учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys tooauthenticate Azure CLI commands for hello Batch service.</span></span>

    <span data-ttu-id="b7f1a-163">При создании сценариев Azure CLI tooautomate вызывающий пакетные команды, можно использовать проверку подлинности Shared Key или основной службой Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-163">If you are creating Azure CLI scripts tooautomate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="b7f1a-164">В некоторых случаях проверку подлинности на основе общего ключа реализовать проще, чем создать субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="b7f1a-165">toolog с помощью проверки подлинности Shared Key, включают hello `--shared-key-auth` hello командной строке:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-165">toolog in using Shared Key authentication, include hello `--shared-key-auth` option on hello command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="b7f1a-166">Примеры Hello, перечисленные в hello [образцы сценариев оболочки](#sample-shell-scripts) разделе показано, как toolog в вашу учетную запись пакета с hello Azure CLI с помощью Azure AD и общим ключом.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-166">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section show how toolog into your Batch account with hello Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="b7f1a-167">Использование шаблонов интерфейса командной строки для пакетной службы Azure и передачи файлов (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="b7f1a-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="b7f1a-168">Hello Azure CLI toorun пакетного задания узел узел можно использовать без написания кода.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-168">You can use hello Azure CLI toorun Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="b7f1a-169">Пакетные файлы шаблона поддерживают создание пулов, заданий и задач с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-169">Batch template files support creating pools, jobs, and tasks with hello Azure CLI.</span></span> <span data-ttu-id="b7f1a-170">Можно также использовать входные файлы hello Azure CLI tooupload Задание учетной записи хранилища Azure toohello, связанной с hello учетная запись пакетной службы и загрузки выходных файлов задания из него.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-170">You can also use hello Azure CLI tooupload job input files toohello Azure Storage account associated with hello Batch account, and download job output files from it.</span></span> <span data-ttu-id="b7f1a-171">См. дополнительные сведения об [использовании шаблонов интерфейса командной строки для пакетной службы Azure и передаче файлов (предварительная версия)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="b7f1a-172">Примеры скриптов оболочки</span><span class="sxs-lookup"><span data-stu-id="b7f1a-172">Sample shell scripts</span></span>

<span data-ttu-id="b7f1a-173">Примеры сценариев Hello перечислены в hello после Показать таблицу как toouse Azure CLI команды с помощью пакетной службы hello и общие задачи управления пакетной службы tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-173">hello sample scripts listed in hello following table show how toouse Azure CLI commands with hello Batch service and Batch Management service tooaccomplish common tasks.</span></span> <span data-ttu-id="b7f1a-174">Эти примеры сценариев охватить многие hello команд, доступных в hello Azure CLI для пакета.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-174">These sample scripts cover many of hello commands available in hello Azure CLI for Batch.</span></span> 

| <span data-ttu-id="b7f1a-175">Скрипт</span><span class="sxs-lookup"><span data-stu-id="b7f1a-175">Script</span></span> | <span data-ttu-id="b7f1a-176">Примечания</span><span class="sxs-lookup"><span data-stu-id="b7f1a-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b7f1a-177">Создание учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b7f1a-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="b7f1a-178">Создает учетную запись пакетной службы и связывает ее с учетной записью хранения.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="b7f1a-179">Добавление приложения</span><span class="sxs-lookup"><span data-stu-id="b7f1a-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="b7f1a-180">Добавляет приложение и передает его упакованные двоичные файлы.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="b7f1a-181">Управление пулами пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b7f1a-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="b7f1a-182">Демонстрирует создание пулов, изменение размера пулов и управление ими.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="b7f1a-183">Выполнение задания и задач с помощью пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b7f1a-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="b7f1a-184">Демонстрирует выполнение задания и добавление задач.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="b7f1a-185">JSON-файлы для создания ресурса</span><span class="sxs-lookup"><span data-stu-id="b7f1a-185">JSON files for resource creation</span></span>

<span data-ttu-id="b7f1a-186">При создании пакета ресурсы, такие как пулы и задания, можно указать файл JSON, содержащий конфигурации нового ресурса hello вместо передачи его параметров в виде параметров командной строки.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing hello new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="b7f1a-187">Например:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="b7f1a-188">Вы можете создать больше всего ресурсов пакета, используя только параметры командной строки, некоторые функции требуют указывать файл формата JSON, содержащий сведения о ресурсах hello.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing hello resource details.</span></span> <span data-ttu-id="b7f1a-189">Например необходимо использовать файл JSON, если toospecify файлы ресурсов для задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-189">For example, you must use a JSON file if you want toospecify resource files for a start task.</span></span>

<span data-ttu-id="b7f1a-190">hello toosee синтаксис JSON требуется toocreate ресурса см. в toohello [Справочник по API REST пакета] [ rest_api] документации.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-190">toosee hello JSON syntax required toocreate a resource, refer toohello [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="b7f1a-191">Каждый «добавить *тип ресурса*» раздела hello Справочник по REST API содержит примеры сценариев JSON для создания этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-191">Each "Add *resource type*" topic in hello REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="b7f1a-192">Эти примеры сценариев JSON можно использовать как шаблоны для toouse файлы JSON с hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-192">You can use those sample JSON scripts as templates for JSON files toouse with hello Azure CLI.</span></span> <span data-ttu-id="b7f1a-193">Например, слишком относится hello toosee синтаксис JSON для создания пула[добавить учетную запись пула tooan][rest_add_pool].</span><span class="sxs-lookup"><span data-stu-id="b7f1a-193">For example, toosee hello JSON syntax for pool creation, refer too[Add a pool tooan account][rest_add_pool].</span></span>

<span data-ttu-id="b7f1a-194">Пример скрипта указания файла JSON см. в статье [Выполнение заданий в пакетной службе Azure с помощью Azure CLI](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b7f1a-195">При указании JSON-файла при создании ресурса, учитываются любые другие параметры, указываемые в командной строке hello для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-195">If you specify a JSON file when you create a resource, any other parameters that you specify on hello command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="b7f1a-196">Эффективные запросы для ресурсов пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b7f1a-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="b7f1a-197">Каждый тип ресурса пакетной службы поддерживает команду `list` , которая запрашивает учетную запись пакетной службы и предоставляет списки ресурсов заданного типа.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="b7f1a-198">Например можно составить список пулов hello в вашей учетной записи и hello задач задания:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-198">For example, you can list hello pools in your account and hello tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="b7f1a-199">При выполнении запроса hello пакетная служба с `list` операции, можно указать toolimit hello OData предложение объем возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-199">When you query hello Batch service with a `list` operation, you can specify an OData clause toolimit hello amount of data returned.</span></span> <span data-ttu-id="b7f1a-200">Так как все фильтрация выполняется стороне сервера, только данные hello запросов пересекает hello сети.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-200">Because all filtering occurs server-side, only hello data you request crosses hello wire.</span></span> <span data-ttu-id="b7f1a-201">Использование пропускной способности toosave этих предложений (и поэтому время) при выполнении операции списка.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-201">Use these clauses toosave bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="b7f1a-202">Hello следующей таблице описываются предложения hello OData, поддерживаемые hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-202">hello following table describes hello OData clauses supported by hello Batch service:</span></span>

| <span data-ttu-id="b7f1a-203">Предложение</span><span class="sxs-lookup"><span data-stu-id="b7f1a-203">Clause</span></span> | <span data-ttu-id="b7f1a-204">Описание</span><span class="sxs-lookup"><span data-stu-id="b7f1a-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="b7f1a-205">Возвращает подмножество свойств для каждой сущности.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="b7f1a-206">Возвращает только сущности, которые соответствуют hello указано выражение OData.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-206">Returns only entities that match hello specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="b7f1a-207">Получает сведения о сущности hello в базовой один вызов REST.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-207">Obtains hello entity information in a single underlying REST call.</span></span> <span data-ttu-id="b7f1a-208">Hello разверните предложение в настоящее время поддерживает только hello `stats` свойство.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-208">hello expand clause currently supports only hello `stats` property.</span></span> |

<span data-ttu-id="b7f1a-209">Для образца сценарии, показано, как toouse предложение OData см [запуска задания и задач с использованием пакета](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-209">For a sample script that shows how toouse an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="b7f1a-210">Дополнительные сведения о выполнении запросов эффективный списка с предложениями OData см. в разделе [эффективно запрашивать hello пакетной службы Azure](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-210">For more information on performing efficient list queries with OData clauses, see [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="b7f1a-211">Советы по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="b7f1a-211">Troubleshooting tips</span></span>

<span data-ttu-id="b7f1a-212">Hello следующие советы могут помочь при устранении неполадок Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="b7f1a-212">hello following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="b7f1a-213">Используйте `-h` tooget **текст справки** для любую команду CLI</span><span class="sxs-lookup"><span data-stu-id="b7f1a-213">Use `-h` tooget **help text** for any CLI command</span></span>
* <span data-ttu-id="b7f1a-214">Используйте `-v` и `-vv` toodisplay **verbose** выходные данные команды.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-214">Use `-v` and `-vv` toodisplay **verbose** command output.</span></span> <span data-ttu-id="b7f1a-215">Здравствуйте, когда `-vv` флаг включен, hello Azure CLI отображает hello фактических запросов и ответов REST.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-215">When hello `-vv` flag is included, hello Azure CLI displays hello actual REST requests and responses.</span></span> <span data-ttu-id="b7f1a-216">Эти параметры удобно использовать для просмотра полного вывода ошибок.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="b7f1a-217">Можно просмотреть **команды выходные данные в формате JSON** с hello `--json` параметр.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-217">You can view **command output as JSON** with hello `--json` option.</span></span> <span data-ttu-id="b7f1a-218">Например, параметр `az batch pool show pool001 --json` отображает свойства элемента pool001 в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="b7f1a-219">Можно скопировать и изменить этот toouse выходные данные в `--json-file` (см. [файлы JSON](#json-files) ранее в этой статье).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-219">You can then copy and modify this output toouse in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* <span data-ttu-id="b7f1a-220">Hello [форум по пакетной] [ batch_forum] отслеживается по членам команды в пакете.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-220">hello [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="b7f1a-221">Задавайте вопросы на форуме, если у вас возникнут проблемы или вам потребуется справочная информация по какой-либо операции.</span><span class="sxs-lookup"><span data-stu-id="b7f1a-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7f1a-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b7f1a-222">Next steps</span></span>

* <span data-ttu-id="b7f1a-223">Дополнительные сведения о hello Azure CLI см. в разделе hello [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-223">For more information about hello Azure CLI, see hello [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="b7f1a-224">Дополнительные сведения о ресурсах пакетной службы см. в статье [Разработка решений для крупномасштабных параллельных вычислений с использованием пакетной службы](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="b7f1a-225">Дополнительные сведения об использовании пулов toocreate шаблоны пакета, заданий и задач без написания кода см. в разделе [использовать шаблоны CLI пакета Azure и передача файлов (Предварительная версия)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b7f1a-225">For more information about using Batch templates toocreate pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
