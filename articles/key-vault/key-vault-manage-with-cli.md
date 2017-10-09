---
title: "Хранилище ключей Azure с использованием интерфейса CLI aaaManage | Документы Microsoft"
description: "Использование этого учебника tooautomate типичных задач в хранилище ключей с помощью hello CLI"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="183f6-103">Управление хранилищем ключей с помощью CLI</span><span class="sxs-lookup"><span data-stu-id="183f6-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="183f6-104">Хранилище ключей Azure доступно в большинстве регионов.</span><span class="sxs-lookup"><span data-stu-id="183f6-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="183f6-105">Дополнительные сведения см. в разделе hello [страница цен в хранилище ключей](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="183f6-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="183f6-106">Введение</span><span class="sxs-lookup"><span data-stu-id="183f6-106">Introduction</span></span>

<span data-ttu-id="183f6-107">Использовать этот учебник toohelp, вы получаете работы с хранилищем ключей Azure toocreate жесткой контейнера (хранилище) в Azure, toostore и управлять ими, криптографические ключи и секретные данные в Azure.</span><span class="sxs-lookup"><span data-stu-id="183f6-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="183f6-108">Помогает выполнить процесс с помощью интерфейса командной строки Azure кросс-платформенных toocreate hello хранилище, в котором содержится ключ или пароль, который затем можно использовать вместе с приложением Azure.</span><span class="sxs-lookup"><span data-stu-id="183f6-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="183f6-109">В нем также показано, как приложение может использовать этот ключ или пароль в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="183f6-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="183f6-110">**Предполагаемое время toocomplete:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="183f6-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="183f6-111">Этот учебник включает инструкции о том, как toowrite hello приложения Azure, в котором один из шагов hello, показывающий, как tooauthorize приложения toouse ключа или секрета в ключе hello хранилище.</span><span class="sxs-lookup"><span data-stu-id="183f6-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
> 
> <span data-ttu-id="183f6-112">В настоящее время вы не можете настроить хранилище ключей Azure hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="183f6-112">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="183f6-113">Вместо этого воспользуйтесь этими инструкциями по кроссплатформенному интерфейсу командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="183f6-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="183f6-114">Инструкции по Azure PowerShell см. в [этом руководстве](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="183f6-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="183f6-115">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="183f6-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="183f6-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="183f6-116">Prerequisites</span></span>

<span data-ttu-id="183f6-117">toocomplete этого учебника необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="183f6-117">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="183f6-118">TooMicrosoft подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="183f6-118">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="183f6-119">Если у вас нет подписки, вы можете зарегистрироваться для использования [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial);</span><span class="sxs-lookup"><span data-stu-id="183f6-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="183f6-120">Интерфейс командной строки версии 0.9.1 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="183f6-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="183f6-121">tooinstall hello последнюю версию и подключите tooyour подписки Azure в разделе [Установка и настройка hello Azure межплатформенного интерфейса командной строки](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="183f6-121">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="183f6-122">Приложение, настроенное toouse hello ключ или пароль, который создан в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="183f6-122">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="183f6-123">Образец приложения доступно из hello [центра загрузки Майкрософт](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="183f6-123">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="183f6-124">Инструкции см. в файле Readme, сопровождающие hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-124">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="183f6-125">Справка по межплатформенному интерфейсу командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="183f6-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="183f6-126">В этом учебнике предполагается, что вы знакомы с интерфейсом командной строки hello (Bash, терминалов, Командная строка)</span><span class="sxs-lookup"><span data-stu-id="183f6-126">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="183f6-127">Hello--справки или -h параметр можно использовать tooview справки для определенных команд.</span><span class="sxs-lookup"><span data-stu-id="183f6-127">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="183f6-128">Кроме того hello azure help [команда] [параметры] формата также можно использовать tooreturn hello одинаковые сведения.</span><span class="sxs-lookup"><span data-stu-id="183f6-128">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="183f6-129">Например, hello следующие команды возвращают все hello одинаковые сведения:</span><span class="sxs-lookup"><span data-stu-id="183f6-129">For example, hello following commands all return hello same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="183f6-130">В случае сомнений о hello параметров, используемых в команде ссылаться с помощью toohelp--справки, -h или azure help [команда].</span><span class="sxs-lookup"><span data-stu-id="183f6-130">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or azure help [command].</span></span>

<span data-ttu-id="183f6-131">Также можно прочитать следующие учебники tooget знакомы с помощью диспетчера ресурсов Azure в интерфейс командной строки Azure кросс-платформенных hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-131">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="183f6-132">Как tooinstall и настройка Azure кросс-платформенных командной строки</span><span class="sxs-lookup"><span data-stu-id="183f6-132">How tooinstall and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="183f6-133">Использование межплатформенного интерфейса командной строки Azure совместно с диспетчером ресурсов</span><span class="sxs-lookup"><span data-stu-id="183f6-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="183f6-134">Подключение tooyour подписки</span><span class="sxs-lookup"><span data-stu-id="183f6-134">Connect tooyour subscriptions</span></span>

<span data-ttu-id="183f6-135">toolog с помощью учетной записи организации, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="183f6-135">toolog in using an organizational account, use hello following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="183f6-136">или если требуется toolog в интерактивном режиме введите</span><span class="sxs-lookup"><span data-stu-id="183f6-136">or if you want toolog in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="183f6-137">метод входа Hello работает только с учетной записью организации.</span><span class="sxs-lookup"><span data-stu-id="183f6-137">hello login method only works with organizational account.</span></span> <span data-ttu-id="183f6-138">Учетная запись организации — это пользователь, который управляется вашей организацией и определен в клиенте Azure Active Directory организации.</span><span class="sxs-lookup"><span data-stu-id="183f6-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="183f6-139">Если в настоящее время не имеют учетной записи организации и используется учетная запись Майкрософт toolog в tooyour подписки Azure, можно легко создать ее, используя hello следующие действия.</span><span class="sxs-lookup"><span data-stu-id="183f6-139">If you do not currently have an organizational account, and are using a Microsoft account toolog in tooyour Azure subscription, you can easily create one using hello following steps.</span></span>

1. <span data-ttu-id="183f6-140">Toohello входа toohello входа [портала управления Azure](https://manage.windowsazure.com/)и нажмите кнопку на основе Active Directory.</span><span class="sxs-lookup"><span data-stu-id="183f6-140">Login toohello Login toohello [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="183f6-141">Если каталог не существует, выберите создать каталог и предоставьте hello затребовал информацию.</span><span class="sxs-lookup"><span data-stu-id="183f6-141">If no directory exists, select Create your directory and provide hello requested information.</span></span>
3. <span data-ttu-id="183f6-142">Выберите каталог и добавьте нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="183f6-142">Select your directory and add a new user.</span></span> <span data-ttu-id="183f6-143">Этот пользователь будет представлять учетную запись организации.</span><span class="sxs-lookup"><span data-stu-id="183f6-143">This new user is an organizational account.</span></span> <span data-ttu-id="183f6-144">Во время создания hello hello пользователя будут предоставляться с адресом электронной почты для пользователя hello и временный пароль.</span><span class="sxs-lookup"><span data-stu-id="183f6-144">During hello creation of hello user, you will be supplied with both an e-mail address for hello user and a temporary password.</span></span> <span data-ttu-id="183f6-145">Эти данные используются на следующем шаге. Сохраните их.</span><span class="sxs-lookup"><span data-stu-id="183f6-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="183f6-146">Из портала hello выберите параметры, а затем выберите администраторов.</span><span class="sxs-lookup"><span data-stu-id="183f6-146">From hello portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="183f6-147">Выберите Добавить и добавить нового пользователя hello в качестве соадминистратора.</span><span class="sxs-lookup"><span data-stu-id="183f6-147">Select Add, and add hello new user as a co-administrator.</span></span> <span data-ttu-id="183f6-148">Это позволяет учетной записи организации toomanage hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="183f6-148">This allows hello organizational account toomanage your Azure subscription.</span></span>
5. <span data-ttu-id="183f6-149">Наконец, выйдите из hello портал Azure и затем войдите снова с помощью учетной записи организации новый hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-149">Finally, log out of hello Azure portal and then log back in using hello new organizational account.</span></span> <span data-ttu-id="183f6-150">Если это hello первый раз вход с помощью этой учетной записи, будет использоваться пароля hello toochange запрос.</span><span class="sxs-lookup"><span data-stu-id="183f6-150">If this is hello first time logging in with this account, you will be prompted toochange hello password.</span></span>

<span data-ttu-id="183f6-151">Дополнительные сведения об использовании рабочей учетной записи в Microsoft Azure см. в статье [Подпишитесь на Azure как организация](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="183f6-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="183f6-152">Если есть несколько подписок и требуется toospecify конкретных один toouse для хранилища ключей Azure, введите hello, следуя toosee hello подписки для учетной записи:</span><span class="sxs-lookup"><span data-stu-id="183f6-152">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="183f6-153">Затем toospecify hello подписки toouse, тип:</span><span class="sxs-lookup"><span data-stu-id="183f6-153">Then, toospecify hello subscription toouse, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="183f6-154">Дополнительные сведения о настройке Azure межплатформенного интерфейса командной строки см. в разделе [как tooInstall и настройка интерфейса командной строки Azure кросс-платформенных](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="183f6-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How tooInstall and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-toousing-azure-resource-manager"></a><span data-ttu-id="183f6-155">Переключение toousing диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="183f6-155">Switch toousing Azure Resource Manager</span></span>
<span data-ttu-id="183f6-156">Hello хранилище ключей требуется диспетчер ресурсов Azure, поэтому введите следующий режим диспетчера ресурсов tooAzure tooswitch hello:</span><span class="sxs-lookup"><span data-stu-id="183f6-156">hello Key Vault requires Azure Resource Manager, so type hello following tooswitch tooAzure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="183f6-157">Создание новой группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="183f6-157">Create a new resource group</span></span>
<span data-ttu-id="183f6-158">При использовании диспетчера ресурсов Azure все связанные ресурсы создаются внутри группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="183f6-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="183f6-159">Для примера мы создадим новую группу ресурсов с именем ContosoResourceGroup:</span><span class="sxs-lookup"><span data-stu-id="183f6-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="183f6-160">Hello первым параметром является имя группы ресурсов, если второй параметр hello расположение hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-160">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="183f6-161">Для расположения, используйте команду hello `azure location list` tooidentify как toospecify альтернативное расположение toohello один в этом примере.</span><span class="sxs-lookup"><span data-stu-id="183f6-161">For location, use hello command `azure location list` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="183f6-162">Если вам необходима дополнительная информация, введите `azure help location`</span><span class="sxs-lookup"><span data-stu-id="183f6-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="183f6-163">Регистрация поставщика ресурсов хранилища ключей hello</span><span class="sxs-lookup"><span data-stu-id="183f6-163">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="183f6-164">Убедитесь, что поставщик ресурсов хранилища ключей зарегистрирован в вашей подписке:</span><span class="sxs-lookup"><span data-stu-id="183f6-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="183f6-165">Это достаточно выполнить один раз для каждой подписки toobe.</span><span class="sxs-lookup"><span data-stu-id="183f6-165">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="183f6-166">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="183f6-166">Create a key vault</span></span>

<span data-ttu-id="183f6-167">Используйте hello `azure keyvault create` toocreate команда хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="183f6-167">Use hello `azure keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="183f6-168">Этот сценарий имеет три обязательных параметра: имя группы ресурсов, имя хранилища ключей и географическое расположение hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-168">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="183f6-169">Например если вы используете hello хранилище с именем ContosoKeyVault hello группу ресурсов с именем ContosoResourceGroup и расположение hello Восточная Азия, введите:</span><span class="sxs-lookup"><span data-stu-id="183f6-169">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="183f6-170">выходные данные этой команды Hello отображает свойства hello хранилища ключей, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="183f6-170">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="183f6-171">Hello двух наиболее важных свойств:</span><span class="sxs-lookup"><span data-stu-id="183f6-171">hello two most important properties are:</span></span>

* <span data-ttu-id="183f6-172">**Имя**: пример hello это ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="183f6-172">**Name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="183f6-173">Вы будете использовать это имя для выполнения других командлетов хранилища ключей;</span><span class="sxs-lookup"><span data-stu-id="183f6-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="183f6-174">**vaultUri**: пример hello это https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="183f6-174">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="183f6-175">Необходимо, чтобы приложения, использующие ваше хранилище через REST API, использовали этот URI.</span><span class="sxs-lookup"><span data-stu-id="183f6-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="183f6-176">Учетная запись Azure — теперь авторизованным tooperform все операции в этот ключ в хранилище.</span><span class="sxs-lookup"><span data-stu-id="183f6-176">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="183f6-177">Пока что это недоступно для других учетных записей.</span><span class="sxs-lookup"><span data-stu-id="183f6-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="183f6-178">Добавление ключа или секрета toohello хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="183f6-178">Add a key or secret toohello key vault</span></span>

<span data-ttu-id="183f6-179">Хранилище ключей Azure toocreate программно защищенного ключа для вас, используйте hello `azure key create` команд и введите hello ниже:</span><span class="sxs-lookup"><span data-stu-id="183f6-179">If you want Azure Key Vault toocreate a software-protected key for you, use hello `azure key create` command, and type hello following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="183f6-180">Тем не менее при наличии существующего ключа в PEM-файл сохранен как локальный файл в файл с именем softkey.pem, что требуется tooupload tooAzure хранилище ключей, введите следующую tooimport hello ключ из hello hello. PEM-файла, который защищает hello с помощью программного обеспечения в hello службы хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="183f6-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="183f6-181">Теперь можно ссылаться на ключ hello, созданные или переданные tooAzure хранилище ключей с помощью URI-адрес.</span><span class="sxs-lookup"><span data-stu-id="183f6-181">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="183f6-182">Используйте **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways получения текущей версии hello и **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget этой конкретной версии.</span><span class="sxs-lookup"><span data-stu-id="183f6-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="183f6-183">tooadd секретный toohello хранилища, которой это пароль SQLPassword с именем и значением hello Pa$ $w0rd tooAzure хранилище ключей, тип hello следующие:</span><span class="sxs-lookup"><span data-stu-id="183f6-183">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="183f6-184">Теперь можно ссылаться на этот пароль добавили tooAzure хранилище ключей с помощью URI-адрес.</span><span class="sxs-lookup"><span data-stu-id="183f6-184">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="183f6-185">Используйте **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways получения текущей версии hello и **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget этой конкретной версии.</span><span class="sxs-lookup"><span data-stu-id="183f6-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="183f6-186">Позволяет просмотреть hello ключа или секрета, который вы только что создали:</span><span class="sxs-lookup"><span data-stu-id="183f6-186">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="183f6-187">tooview вашей, введите:`azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="183f6-187">tooview your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="183f6-188">tooview в тайне, тип:`azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="183f6-188">tooview your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="183f6-189">Зарегистрируйте приложение с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="183f6-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="183f6-190">Обычно этот шаг выполняет разработчик на отдельном компьютере.</span><span class="sxs-lookup"><span data-stu-id="183f6-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="183f6-191">Он не является tooAzure конкретного хранилища ключей, но указан, для обеспечения полноты.</span><span class="sxs-lookup"><span data-stu-id="183f6-191">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="183f6-192">Учебник toocomplete hello, учетная запись, хранилище hello и приложения hello, которое будет зарегистрирован на этом шаге необходимо в hello один каталог Azure.</span><span class="sxs-lookup"><span data-stu-id="183f6-192">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
> 
> 

<span data-ttu-id="183f6-193">Приложения, которые используют хранилища ключей, должны пройти аутентификацию с использованием токена Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="183f6-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="183f6-194">toodo, hello владелец приложения hello сначала необходимо зарегистрировать приложение hello в своем Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="183f6-194">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="183f6-195">В конце hello регистрации владелец приложения hello возвращает hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="183f6-195">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="183f6-196">**Идентификатор приложения** (также известный как идентификатор клиента) и **ключ проверки подлинности** (также известный как общий секрет hello).</span><span class="sxs-lookup"><span data-stu-id="183f6-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="183f6-197">приложение Hello должен представить оба этих значения tooAzure Active Directory, tooget маркер.</span><span class="sxs-lookup"><span data-stu-id="183f6-197">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="183f6-198">Как приложение hello настраивается toodo это зависит от приложения hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-198">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="183f6-199">Для hello образец приложения хранилища ключей владелец приложения hello устанавливает эти значения в файле app.config hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-199">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="183f6-200">приложение hello tooregister в Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="183f6-200">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="183f6-201">Войдите в систему toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="183f6-201">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="183f6-202">В левой части экрана приветствия щелкните **Active Directory**и выберите каталог hello, в котором будет зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="183f6-202">On hello left, click **Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="183f6-203">Необходимо выбрать hello каталоге, содержащем hello подписки Azure, в которой для создания хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="183f6-203">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="183f6-204">Если вы не знаете, какой каталог это, нажмите кнопку **параметры**идентификации hello подписки, в которой для создания хранилища ключей и Примечание hello hello directory название hello последнего столбца.</span><span class="sxs-lookup"><span data-stu-id="183f6-204">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="183f6-205">Щелкните **ПРИЛОЖЕНИЯ**.</span><span class="sxs-lookup"><span data-stu-id="183f6-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="183f6-206">Если приложения не были добавлены tooyour каталога, эта страница отобразит только hello **добавить приложение** ссылку.</span><span class="sxs-lookup"><span data-stu-id="183f6-206">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="183f6-207">Щелкните ссылку hello, или в качестве альтернативы можно щелкнуть hello **добавить** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-207">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="183f6-208">В hello **добавить приложение** мастера hello **что вам требуется toodo?** щелкните **добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="183f6-208">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="183f6-209">На hello **Расскажите о своем приложении** укажите имя для вашего приложения и выберите **веб-приложение и/или WEB API** (по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="183f6-209">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="183f6-210">Щелкните значок "следующий" hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-210">Click hello Next icon.</span></span>
6. <span data-ttu-id="183f6-211">На hello **свойства приложения** укажите hello **URL-адрес входа** и **URI идентификатора приложения** для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="183f6-211">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="183f6-212">Если в вашем приложении нет этих значений, можно придумать их для этого шага (например, можно указать http://test1.contoso.com в обоих полях).</span><span class="sxs-lookup"><span data-stu-id="183f6-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="183f6-213">Не важно, эти веб-сайты, если существует. Важно то, что URI идентификатора приложения hello для каждого приложения отличается для каждого приложения в каталоге.</span><span class="sxs-lookup"><span data-stu-id="183f6-213">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="183f6-214">каталог Hello используется этой строки tooidentify приложений.</span><span class="sxs-lookup"><span data-stu-id="183f6-214">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="183f6-215">Щелкните значок завершения toosave hello изменения в мастере hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-215">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="183f6-216">На странице быстрого запуска приветствия щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="183f6-216">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="183f6-217">Прокрутите toohello **ключей** выберите длительность hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="183f6-217">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="183f6-218">Страница приветствия обновляется и теперь отображается значение ключа.</span><span class="sxs-lookup"><span data-stu-id="183f6-218">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="183f6-219">Необходимо настроить приложение с таким значением ключа и hello **идентификатор КЛИЕНТА** значение.</span><span class="sxs-lookup"><span data-stu-id="183f6-219">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="183f6-220">(указания по этой конфигурации зависят от конкретного приложения).</span><span class="sxs-lookup"><span data-stu-id="183f6-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="183f6-221">На этой странице, который будет использоваться в hello следующий шаг tooset разрешения на ваше хранилище, скопируйте значение идентификатора клиента hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-221">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="183f6-222">Авторизовать hello приложения toouse hello ключа или секрета</span><span class="sxs-lookup"><span data-stu-id="183f6-222">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="183f6-223">tooaccess приложения hello tooauthorize hello ключа или секрета в хранилище hello, используйте hello `azure keyvault set-policy` команды.</span><span class="sxs-lookup"><span data-stu-id="183f6-223">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="183f6-224">Например если имя хранилища — ContosoKeyVault и hello приложения требуется tooauthorize имеет идентификатор клиента 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, и вы хотите toodecrypt приложения hello tooauthorize и войдите с ключами в хранилище, а затем запустите hello следующие:</span><span class="sxs-lookup"><span data-stu-id="183f6-224">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="183f6-225">При запуске в командной строке Windows следует замените одинарные и двойные кавычки и также escape-hello внутренней двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="183f6-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape hello internal double quotes.</span></span> <span data-ttu-id="183f6-226">Например: "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="183f6-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="183f6-227">Tooauthorize этой же tooread секреты приложения в хранилище, выполните следующие hello:</span><span class="sxs-lookup"><span data-stu-id="183f6-227">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="183f6-228">Если требуется, чтобы toouse аппаратный модуль безопасности (HSM)</span><span class="sxs-lookup"><span data-stu-id="183f6-228">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="183f6-229">Для повышения надежности можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM), никогда не покидают границ HSM hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="183f6-230">Hello аппаратные модули безопасности являются FIPS 140-2 уровня 2 проверки.</span><span class="sxs-lookup"><span data-stu-id="183f6-230">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="183f6-231">Если это требование не распространяется tooyou, пропустите этот раздел и перейдите слишком[удалить hello хранилища ключей и связанные ключи и секретные данные](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="183f6-231">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="183f6-232">toocreate этих ключей, защищенных HSM, необходимо иметь подписку хранилища, который поддерживает ключей, защищенных HSM.</span><span class="sxs-lookup"><span data-stu-id="183f6-232">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="183f6-233">При создании hello keyvault, добавьте параметр «Конфигурация» hello:</span><span class="sxs-lookup"><span data-stu-id="183f6-233">When you create hello keyvault, add hello 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="183f6-234">Можно добавить программно защищенных ключей (как показано выше) и хранилище ключей, защищенных HSM toothis.</span><span class="sxs-lookup"><span data-stu-id="183f6-234">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="183f6-235">toocreate Перенос аппаратно защищенного ключа набора hello назначения параметра too'HSM ":</span><span class="sxs-lookup"><span data-stu-id="183f6-235">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="183f6-236">Можно использовать следующую команду tooimport ключа из PEM-файл на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="183f6-236">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="183f6-237">Эта команда импортирует ключ hello в аппаратные модули безопасности в hello службы хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="183f6-237">This command imports hello key into HSMs in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="183f6-238">Hello следующая команда импортирует «принеси свой собственный ключ» (BYOK) пакета.</span><span class="sxs-lookup"><span data-stu-id="183f6-238">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="183f6-239">Это дает возможность создания ключа в ваш локальный HSM и передачи tooHSMs в hello службы хранилища ключей без ключа hello, оставляя границ HSM hello:</span><span class="sxs-lookup"><span data-stu-id="183f6-239">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="183f6-240">Более подробные инструкции о том, как toogenerate этот пакет BYOK разделе [как toouse HSM-Protected ключи с хранилищем ключей Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="183f6-240">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="183f6-241">Удаление хранилища ключей hello и связанные ключи и секретные данные</span><span class="sxs-lookup"><span data-stu-id="183f6-241">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="183f6-242">Если вы больше не нужна hello хранилища ключей и hello ключа или секрета, который его содержит, hello хранилища ключей можно удалить с помощью команды delete keyvault hello azure:</span><span class="sxs-lookup"><span data-stu-id="183f6-242">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="183f6-243">Или можно удалить группы весь ресурс Azure, которая включает в себя хранилище ключей hello и другие ресурсы, которые включены в эту группу:</span><span class="sxs-lookup"><span data-stu-id="183f6-243">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="183f6-244">Другие команды в межплатформенном интерфейсе командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="183f6-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="183f6-245">Вот другие команды, которые могут быть полезны при управлении хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="183f6-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="183f6-246">Эта команда перечисляет все ключи и выбранные свойства в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="183f6-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="183f6-247">Эта команда отображает полный список свойств для указанного ключа hello:</span><span class="sxs-lookup"><span data-stu-id="183f6-247">This command displays a full list of properties for hello specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="183f6-248">Эта команда перечисляет все имена секретов и выбранные свойства в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="183f6-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="183f6-249">Ниже приведен пример того, как tooremove определенного ключа:</span><span class="sxs-lookup"><span data-stu-id="183f6-249">Here's an example of how tooremove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="183f6-250">Ниже приведен пример того, как tooremove конкретных секрет:</span><span class="sxs-lookup"><span data-stu-id="183f6-250">Here's an example of how tooremove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="183f6-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="183f6-251">Next steps</span></span>
<span data-ttu-id="183f6-252">Программирование ссылки, в разделе [hello хранилище ключей Azure в руководстве разработчика](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="183f6-252">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

