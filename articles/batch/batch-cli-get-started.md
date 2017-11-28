---
title: "Начало работы с интерфейсом командной строки пакетной службы Azure | Документация Майкрософт"
description: "Ознакомьтесь с командами интерфейса командной строки пакетной службы Azure для управления ресурсами пакетной службы Azure."
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
ms.openlocfilehash: 9bee0344ba70c50cda36a87ea617906283040ff9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="2755e-103">Управление ресурсами пакетной службы с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2755e-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="2755e-104">Azure CLI 2.0 — это новый интерфейс командной строки Azure для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="2755e-104">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="2755e-105">Его можно использовать в Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="2755e-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="2755e-106">Azure CLI 2.0 оптимизирован для администрирования ресурсов Azure и управления ими из командной строки.</span><span class="sxs-lookup"><span data-stu-id="2755e-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from the command line.</span></span> <span data-ttu-id="2755e-107">При помощи этого интерфейса вы можете управлять учетными записями пакетной службы Azure, а также такими ресурсами, как пулы, задания и задачи.</span><span class="sxs-lookup"><span data-stu-id="2755e-107">You can use the Azure CLI to manage your Azure Batch accounts and to manage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="2755e-108">Кроме того, Azure CLI позволяет создавать и выполнять скрипты для многих однотипных задач, выполняемых с помощью API-интерфейсов пакетной службы, портала Azure и командлетов PowerShell пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="2755e-108">With the Azure CLI, you can script many of the same tasks you carry out with the Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="2755e-109">В этой статье содержатся общие сведения об использовании [Azure CLI версии 2.0](https://docs.microsoft.com/cli/azure/overview) с пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="2755e-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="2755e-110">Общие сведения об использовании интерфейса командной строки с Azure см. в статье [Начало работы с Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2755e-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using the CLI with Azure.</span></span>

<span data-ttu-id="2755e-111">Корпорация Майкрософт советует использовать последнюю версию Azure CLI — версию 2.0.</span><span class="sxs-lookup"><span data-stu-id="2755e-111">Microsoft recommends using the latest version of the Azure CLI, version 2.0.</span></span> <span data-ttu-id="2755e-112">Дополнительные сведения о ней см. в записи блога о [выпуске общедоступной версии Azure CLI 2.0](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span><span class="sxs-lookup"><span data-stu-id="2755e-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-the-azure-cli"></a><span data-ttu-id="2755e-113">Настройка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2755e-113">Set up the Azure CLI</span></span>

<span data-ttu-id="2755e-114">Чтобы установить Azure CLI, используйте указания в [этой статье](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2755e-114">To install the Azure CLI, follow the steps outlined in [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="2755e-115">Рекомендуем регулярно обновлять интерфейс командной строки Azure, чтобы использовать все преимущества обновлений и улучшений службы.</span><span class="sxs-lookup"><span data-stu-id="2755e-115">We recommend that you update your Azure CLI installation frequently to take advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="2755e-116">Справка по командам</span><span class="sxs-lookup"><span data-stu-id="2755e-116">Command help</span></span>

<span data-ttu-id="2755e-117">Текст справки для каждой команды в Azure CLI можно просмотреть, добавив к ней `-h`.</span><span class="sxs-lookup"><span data-stu-id="2755e-117">You can display help text for every command in the Azure CLI by appending `-h` to the command.</span></span> <span data-ttu-id="2755e-118">Другие параметры следует опустить.</span><span class="sxs-lookup"><span data-stu-id="2755e-118">Omit any other options.</span></span> <span data-ttu-id="2755e-119">Например:</span><span class="sxs-lookup"><span data-stu-id="2755e-119">For example:</span></span>

* <span data-ttu-id="2755e-120">Чтобы получить справку по команде `az`, введите: `az -h`</span><span class="sxs-lookup"><span data-stu-id="2755e-120">To get help for the `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="2755e-121">Чтобы получить список всех команд пакетной службы в интерфейсе командной строки, используйте: `az batch -h`</span><span class="sxs-lookup"><span data-stu-id="2755e-121">To get a list of all Batch commands in the CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="2755e-122">Чтобы получить справку по созданию учетной записи пакетной службы, введите: `az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="2755e-122">To get help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="2755e-123">Если у вас возникнут сомнения, с помощью параметра командной строки `-h` вы сможете получить справку по любой из команд интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="2755e-123">When in doubt, use the `-h` command-line option to get help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="2755e-124">В предыдущих версиях Azure CLI к командам добавлялся префикс `azure`.</span><span class="sxs-lookup"><span data-stu-id="2755e-124">Earlier versions of the Azure CLI used `azure` to preface a CLI command.</span></span> <span data-ttu-id="2755e-125">В версии 2.0 все команды теперь начинаются с приставки `az`.</span><span class="sxs-lookup"><span data-stu-id="2755e-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="2755e-126">Не забудьте обновить скрипты, чтобы использовать новый синтаксис версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="2755e-126">Be sure to update your scripts to use the new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="2755e-127">Дополнительные сведения о командах Azure CLI для пакетной службы см. в [справочной документации по Azure CLI](https://docs.microsoft.com/cli/azure/batch).</span><span class="sxs-lookup"><span data-stu-id="2755e-127">Additionally, refer to the Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="2755e-128">Вход в систему и проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="2755e-128">Log in and authenticate</span></span>

<span data-ttu-id="2755e-129">Чтобы использовать Azure CLI с пакетной службой, сначала необходимо войти в систему и пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="2755e-129">To use the Azure CLI with Batch, you need to log in and authenticate.</span></span> <span data-ttu-id="2755e-130">Выполните следующие два простых действия:</span><span class="sxs-lookup"><span data-stu-id="2755e-130">There are two simple steps to follow:</span></span>

1. <span data-ttu-id="2755e-131">**Войдите в Azure.**</span><span class="sxs-lookup"><span data-stu-id="2755e-131">**Log into Azure.**</span></span> <span data-ttu-id="2755e-132">Это позволит получить доступ к командам Azure Resource Manager, в том числе командам [службы управления пакетной службой](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2755e-132">Logging into Azure gives you access to Azure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="2755e-133">**Войдите в учетную запись пакетной службы.**</span><span class="sxs-lookup"><span data-stu-id="2755e-133">**Log into your Batch account.**</span></span> <span data-ttu-id="2755e-134">Это позволит получить доступ к командам пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="2755e-134">Logging into your Batch account gives you access to Batch service commands.</span></span>   

### <a name="log-in-to-azure"></a><span data-ttu-id="2755e-135">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="2755e-135">Log in to Azure</span></span>

<span data-ttu-id="2755e-136">В Azure можно войти разными способами, описанными в статье [Вход с помощью Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="2755e-136">There are a few different ways to log into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="2755e-137">[Интерактивный вход.](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in)</span><span class="sxs-lookup"><span data-stu-id="2755e-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="2755e-138">Используйте этот способ, если вы самостоятельно выполняете команды Azure CLI из командной строки.</span><span class="sxs-lookup"><span data-stu-id="2755e-138">Log in interactively when you are running Azure CLI commands yourself from the command line.</span></span>
2. <span data-ttu-id="2755e-139">[Вход с использованием субъекта-службы.](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal)</span><span class="sxs-lookup"><span data-stu-id="2755e-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="2755e-140">Используйте этот способ, если вы выполняете команды Azure CLI из скрипта или приложения.</span><span class="sxs-lookup"><span data-stu-id="2755e-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="2755e-141">В рамках этого руководства мы покажем, как войти в Azure в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="2755e-141">For the purposes of this article, we show how to log into Azure interactively.</span></span> <span data-ttu-id="2755e-142">В окне командной строки введите [az login](https://docs.microsoft.com/cli/azure/#login):</span><span class="sxs-lookup"><span data-stu-id="2755e-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on the command line:</span></span>

```azurecli
# Log in to Azure and authenticate interactively.
az login
```

<span data-ttu-id="2755e-143">Команда `az login` возвращает токен, используемый при аутентификации, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2755e-143">The `az login` command returns a token that you can use to authenticate, as shown here.</span></span> <span data-ttu-id="2755e-144">Следуйте предоставленным указаниям, чтобы открыть веб-страницу и отправить токен в Azure:</span><span class="sxs-lookup"><span data-stu-id="2755e-144">Follow the instructions provided to open a web page and submit the token to Azure:</span></span>

![Вход в Azure](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="2755e-146">Примеры, приведенные в разделе [Примеры скриптов оболочки](#sample-shell-scripts), позволяют запустить сеанс Azure CLI после входа в Azure в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="2755e-146">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section also show how to start your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="2755e-147">После входа вы сможете вызвать команды для работы с ресурсами управления пакетной службой, в том числе учетные записи пакетной службы, ключи, пакеты приложений и квоты.</span><span class="sxs-lookup"><span data-stu-id="2755e-147">Once you have logged in, you can call commands to work with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-to-your-batch-account"></a><span data-ttu-id="2755e-148">Вход в учетную запись пакетной службы</span><span class="sxs-lookup"><span data-stu-id="2755e-148">Log in to your Batch account</span></span>

<span data-ttu-id="2755e-149">Чтобы управлять ресурсами пакетной службы, такими как пулы, задания и задачи, с помощью Azure CLI, сначала необходимо войти в учетную запись пакетной службы и пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="2755e-149">To use the Azure CLI to manage Batch resources, such as pools, jobs, and tasks, you need to log into your Batch account and authenticate.</span></span> <span data-ttu-id="2755e-150">Для этого используйте команду [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login).</span><span class="sxs-lookup"><span data-stu-id="2755e-150">To log in to the Batch service, use the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="2755e-151">Проверку подлинности в учетной записи пакетной службы можно пройти двумя способами:</span><span class="sxs-lookup"><span data-stu-id="2755e-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="2755e-152">**Проверка подлинности Azure Active Directory (Azure AD).**</span><span class="sxs-lookup"><span data-stu-id="2755e-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="2755e-153">При использовании Azure CLI с пакетной службой этот метод проверки подлинности реализован по умолчанию. Мы советуем использовать его в большинстве сценариев.</span><span class="sxs-lookup"><span data-stu-id="2755e-153">Authenticating with Azure AD is the default when you use the Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="2755e-154">При входе в Azure в интерактивном режиме, как описано в предыдущем разделе, учетные данные пользователя кэшируются. Поэтому Azure CLI может войти в учетную запись пакетной службы, используя те же учетные данные.</span><span class="sxs-lookup"><span data-stu-id="2755e-154">When you log in to Azure interactively, as described in the previous section, your credentials are cached, so the Azure CLI can log you in to your Batch account using those same credentials.</span></span> <span data-ttu-id="2755e-155">Если вы входите Azure с использованием субъекта-службы, эти учетные данные также используются для входа в учетную запись пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="2755e-155">If you log in to Azure using a service principal, those credentials are also used to log in to your Batch account.</span></span>

    <span data-ttu-id="2755e-156">Преимущество Azure AD заключается в том, что эта служба предоставляет управление доступом на основе ролей (RBAC).</span><span class="sxs-lookup"><span data-stu-id="2755e-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="2755e-157">При использовании RBAC доступ пользователя зависит от назначенной роли, а не наличия ключей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2755e-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess the account keys.</span></span> <span data-ttu-id="2755e-158">В этом случае управлять ключами не нужно. Вы просто назначаете роли RBAC, и Azure AD управляет параметрами доступа и проверки подлинности вместо вас.</span><span class="sxs-lookup"><span data-stu-id="2755e-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="2755e-159">Проверка подлинности Azure AD требуется при создании учетной записи пакетной службы с режимом выделения пула "Пользовательская подписка".</span><span class="sxs-lookup"><span data-stu-id="2755e-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set to 'User Subscription'.</span></span> 

    <span data-ttu-id="2755e-160">Чтобы войти в учетную запись пакетной службы с помощью Azure AD, вызовите команду [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login):</span><span class="sxs-lookup"><span data-stu-id="2755e-160">To log in to your Batch account using Azure AD, call the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="2755e-161">**Проверка подлинности на основе общего ключа.**</span><span class="sxs-lookup"><span data-stu-id="2755e-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="2755e-162">При использовании метода [проверки подлинности на основе общего ключа](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) проверка подлинности команд Azure CLI для пакетной службы выполняется на основе ключей доступа к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2755e-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys to authenticate Azure CLI commands for the Batch service.</span></span>

    <span data-ttu-id="2755e-163">Если вы используете скрипты Azure CLI для автоматического вызова команд пакетной службы, вы можете реализовать проверку подлинности на основе общего ключа или проверку подлинности Azure AD с использованием субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="2755e-163">If you are creating Azure CLI scripts to automate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="2755e-164">В некоторых случаях проверку подлинности на основе общего ключа реализовать проще, чем создать субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="2755e-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="2755e-165">Чтобы войти с использованием проверки подлинности на основе общего ключа, включите параметр `--shared-key-auth` в командной строке:</span><span class="sxs-lookup"><span data-stu-id="2755e-165">To log in using Shared Key authentication, include the `--shared-key-auth` option on the command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="2755e-166">В примерах, приведенных в разделе [Примеры скриптов оболочки](#sample-shell-scripts), описано, как войти в учетную запись пакетной службы с помощью Azure CLI, использую и Azure AD, и общий ключ.</span><span class="sxs-lookup"><span data-stu-id="2755e-166">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section show how to log into your Batch account with the Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="2755e-167">Использование шаблонов интерфейса командной строки для пакетной службы Azure и передачи файлов (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="2755e-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="2755e-168">Azure CLI можно использовать для запуска заданий пакетной службы без необходимости писать код.</span><span class="sxs-lookup"><span data-stu-id="2755e-168">You can use the Azure CLI to run Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="2755e-169">Файлы шаблона пакетной службы поддерживают создание пулов, заданий и задач с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2755e-169">Batch template files support creating pools, jobs, and tasks with the Azure CLI.</span></span> <span data-ttu-id="2755e-170">Вы также можете использовать Azure CLI для отправки входных файлов заданий в учетную запись хранения Azure, связанную с учетной записью пакетной службы, а также скачивания выходных файлов задания из нее.</span><span class="sxs-lookup"><span data-stu-id="2755e-170">You can also use the Azure CLI to upload job input files to the Azure Storage account associated with the Batch account, and download job output files from it.</span></span> <span data-ttu-id="2755e-171">См. дополнительные сведения об [использовании шаблонов интерфейса командной строки для пакетной службы Azure и передаче файлов (предварительная версия)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2755e-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="2755e-172">Примеры скриптов оболочки</span><span class="sxs-lookup"><span data-stu-id="2755e-172">Sample shell scripts</span></span>

<span data-ttu-id="2755e-173">Примеры скриптов в таблице ниже позволяют выполнять стандартные задачи с помощью команд Azure CLI с пакетной службой и службой управления пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="2755e-173">The sample scripts listed in the following table show how to use Azure CLI commands with the Batch service and Batch Management service to accomplish common tasks.</span></span> <span data-ttu-id="2755e-174">В этих примерах скриптов используется большинство доступных команд Azure CLI для пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="2755e-174">These sample scripts cover many of the commands available in the Azure CLI for Batch.</span></span> 

| <span data-ttu-id="2755e-175">Скрипт</span><span class="sxs-lookup"><span data-stu-id="2755e-175">Script</span></span> | <span data-ttu-id="2755e-176">Примечания</span><span class="sxs-lookup"><span data-stu-id="2755e-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2755e-177">Создание учетной записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="2755e-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="2755e-178">Создает учетную запись пакетной службы и связывает ее с учетной записью хранения.</span><span class="sxs-lookup"><span data-stu-id="2755e-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="2755e-179">Добавление приложения</span><span class="sxs-lookup"><span data-stu-id="2755e-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="2755e-180">Добавляет приложение и передает его упакованные двоичные файлы.</span><span class="sxs-lookup"><span data-stu-id="2755e-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="2755e-181">Управление пулами пакетной службы</span><span class="sxs-lookup"><span data-stu-id="2755e-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="2755e-182">Демонстрирует создание пулов, изменение размера пулов и управление ими.</span><span class="sxs-lookup"><span data-stu-id="2755e-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="2755e-183">Выполнение задания и задач с помощью пакетной службы</span><span class="sxs-lookup"><span data-stu-id="2755e-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="2755e-184">Демонстрирует выполнение задания и добавление задач.</span><span class="sxs-lookup"><span data-stu-id="2755e-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="2755e-185">JSON-файлы для создания ресурса</span><span class="sxs-lookup"><span data-stu-id="2755e-185">JSON files for resource creation</span></span>

<span data-ttu-id="2755e-186">После создания ресурсов пакетной службы, таких как пулы и задания, вы можете указать JSON-файл, содержащий конфигурацию нового ресурса, вместо того чтобы передавать его параметры в виде параметров командной строки.</span><span class="sxs-lookup"><span data-stu-id="2755e-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing the new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="2755e-187">Например:</span><span class="sxs-lookup"><span data-stu-id="2755e-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="2755e-188">Хотя большинство ресурсов пакетной службы можно создавать только с помощью параметров командной строки, для некоторых функций необходимо указать файл формата JSON, содержащий сведения о ресурсе.</span><span class="sxs-lookup"><span data-stu-id="2755e-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing the resource details.</span></span> <span data-ttu-id="2755e-189">Например, JSON-файл следует использовать, если нужно указать файлы ресурсов для задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="2755e-189">For example, you must use a JSON file if you want to specify resource files for a start task.</span></span>

<span data-ttu-id="2755e-190">Синтаксис JSON, необходимый для создания ресурса, см. в [справочной документации по REST API пакетной службы][rest_api].</span><span class="sxs-lookup"><span data-stu-id="2755e-190">To see the JSON syntax required to create a resource, refer to the [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="2755e-191">В каждой статье о добавлении *определенного типа ресурса* приведены примеры скриптов JSON для создания этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="2755e-191">Each "Add *resource type*" topic in the REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="2755e-192">Вы можете использовать эти примеры скриптов как шаблоны файлов JSON, которые можно использовать с Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2755e-192">You can use those sample JSON scripts as templates for JSON files to use with the Azure CLI.</span></span> <span data-ttu-id="2755e-193">Например, синтаксис JSON для создания пула см. в статье [Add a pool to an account][rest_add_pool] (Добавление учетной записи пула).</span><span class="sxs-lookup"><span data-stu-id="2755e-193">For example, to see the JSON syntax for pool creation, refer to [Add a pool to an account][rest_add_pool].</span></span>

<span data-ttu-id="2755e-194">Пример скрипта указания файла JSON см. в статье [Выполнение заданий в пакетной службе Azure с помощью Azure CLI](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="2755e-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2755e-195">Если при создании ресурса вы указываете JSON-файл, все остальные параметры, которые указываются в командной строке для этого ресурса, можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="2755e-195">If you specify a JSON file when you create a resource, any other parameters that you specify on the command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="2755e-196">Эффективные запросы для ресурсов пакетной службы</span><span class="sxs-lookup"><span data-stu-id="2755e-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="2755e-197">Каждый тип ресурса пакетной службы поддерживает команду `list` , которая запрашивает учетную запись пакетной службы и предоставляет списки ресурсов заданного типа.</span><span class="sxs-lookup"><span data-stu-id="2755e-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="2755e-198">Например, вы можете получить список пулов в учетной записи и задач, входящих в задание, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2755e-198">For example, you can list the pools in your account and the tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="2755e-199">При выполнении запроса к пакетной службе, используя операцию `list`, вы можете указать предложение OData, чтобы ограничить объем возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="2755e-199">When you query the Batch service with a `list` operation, you can specify an OData clause to limit the amount of data returned.</span></span> <span data-ttu-id="2755e-200">Так как фильтрация выполняется на стороне сервера, передаются только запрашиваемые данные.</span><span class="sxs-lookup"><span data-stu-id="2755e-200">Because all filtering occurs server-side, only the data you request crosses the wire.</span></span> <span data-ttu-id="2755e-201">Используйте эти предложения для экономии пропускной способности (а значит, и времени) при выполнении операций со списками.</span><span class="sxs-lookup"><span data-stu-id="2755e-201">Use these clauses to save bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="2755e-202">В таблице ниже описаны предложения OData, поддерживаемые пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="2755e-202">The following table describes the OData clauses supported by the Batch service:</span></span>

| <span data-ttu-id="2755e-203">Предложение</span><span class="sxs-lookup"><span data-stu-id="2755e-203">Clause</span></span> | <span data-ttu-id="2755e-204">Описание</span><span class="sxs-lookup"><span data-stu-id="2755e-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="2755e-205">Возвращает подмножество свойств для каждой сущности.</span><span class="sxs-lookup"><span data-stu-id="2755e-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="2755e-206">Возвращает только те сущности, которые соответствуют указанному выражению OData.</span><span class="sxs-lookup"><span data-stu-id="2755e-206">Returns only entities that match the specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="2755e-207">Получает сведения о сущности за один базовый вызов REST.</span><span class="sxs-lookup"><span data-stu-id="2755e-207">Obtains the entity information in a single underlying REST call.</span></span> <span data-ttu-id="2755e-208">Сейчас предложение expand поддерживает только свойство `stats`.</span><span class="sxs-lookup"><span data-stu-id="2755e-208">The expand clause currently supports only the `stats` property.</span></span> |

<span data-ttu-id="2755e-209">Пример скрипта с предложением OData см. в статье [Выполнение заданий в пакетной службе Azure с помощью Azure CLI](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="2755e-209">For a sample script that shows how to use an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="2755e-210">Дополнительные сведения о выполнении эффективных запросов на вывод списка с приложениями OData см. в [этой статье](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="2755e-210">For more information on performing efficient list queries with OData clauses, see [Query the Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="2755e-211">Советы по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="2755e-211">Troubleshooting tips</span></span>

<span data-ttu-id="2755e-212">Ниже приведены советы, которые могут помочь устранить проблемы с Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2755e-212">The following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="2755e-213">Используйте параметр `-h` , чтобы вывести на экран **текст справки** по любой из команд интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="2755e-213">Use `-h` to get **help text** for any CLI command</span></span>
* <span data-ttu-id="2755e-214">Чтобы отобразить выходные данные команды **verbose**, используйте `-v` и `-vv`.</span><span class="sxs-lookup"><span data-stu-id="2755e-214">Use `-v` and `-vv` to display **verbose** command output.</span></span> <span data-ttu-id="2755e-215">Когда флаг `-vv` включен, Azure CLI отображает текущие REST-запросы и ответы.</span><span class="sxs-lookup"><span data-stu-id="2755e-215">When the `-vv` flag is included, the Azure CLI displays the actual REST requests and responses.</span></span> <span data-ttu-id="2755e-216">Эти параметры удобно использовать для просмотра полного вывода ошибок.</span><span class="sxs-lookup"><span data-stu-id="2755e-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="2755e-217">Вы можете просмотреть **выходные данные команды в виде JSON** с помощью параметра `--json`.</span><span class="sxs-lookup"><span data-stu-id="2755e-217">You can view **command output as JSON** with the `--json` option.</span></span> <span data-ttu-id="2755e-218">Например, параметр `az batch pool show pool001 --json` отображает свойства элемента pool001 в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="2755e-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="2755e-219">Затем вы можете скопировать и изменить эти выходные данные для использования в параметре `--json-file` (см. выше раздел, посвященный [JSON-файлам](#json-files)).</span><span class="sxs-lookup"><span data-stu-id="2755e-219">You can then copy and modify this output to use in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting to any location.--->
* <span data-ttu-id="2755e-220">[Форум пакетной службы][batch_forum] тщательно отслеживают специалисты пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="2755e-220">The [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="2755e-221">Задавайте вопросы на форуме, если у вас возникнут проблемы или вам потребуется справочная информация по какой-либо операции.</span><span class="sxs-lookup"><span data-stu-id="2755e-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2755e-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2755e-222">Next steps</span></span>

* <span data-ttu-id="2755e-223">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2755e-223">For more information about the Azure CLI, see the [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="2755e-224">Дополнительные сведения о ресурсах пакетной службы см. в статье [Разработка решений для крупномасштабных параллельных вычислений с использованием пакетной службы](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="2755e-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="2755e-225">Дополнительные сведения о создании пулов, заданий и задач без написания кода с помощью шаблонов пакетной службы см. в руководстве по [использованию шаблонов интерфейса командной строки для пакетной службы Azure и передаче файлов (предварительная версия)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2755e-225">For more information about using Batch templates to create pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
