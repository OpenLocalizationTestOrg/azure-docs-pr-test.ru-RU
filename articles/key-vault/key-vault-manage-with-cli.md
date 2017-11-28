---
title: "Управление Azure Key Vault с помощью интерфейса командной строки | Документы Майкрософт"
description: "Из этого учебника вы узнаете об автоматизации основных задач в хранилище ключей с использованием CLI"
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
ms.openlocfilehash: c2565a742ce4f6ab5f7639a54c4a475f00cbc260
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="cc3fe-103">Управление хранилищем ключей с помощью CLI</span><span class="sxs-lookup"><span data-stu-id="cc3fe-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="cc3fe-104">Хранилище ключей Azure доступно в большинстве регионов.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="cc3fe-105">Дополнительные сведения см. на странице [цен на хранилище ключей](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="cc3fe-106">Введение</span><span class="sxs-lookup"><span data-stu-id="cc3fe-106">Introduction</span></span>

<span data-ttu-id="cc3fe-107">Этот учебник поможет вам начать работу с хранилищем ключей Azure. В нем содержится информация о создании зафиксированного контейнера (хранилища), хранении криптографических ключей и секретов, а также об управлении ими в Azure.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="cc3fe-108">Он представляет собой пошаговое руководство по использованию межплатформенного интерфейса командной строки Azure для создания хранилища, содержащего ключ или пароль, который вы сможете использовать с приложением Azure.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="cc3fe-109">В нем также показано, как приложение может использовать этот ключ или пароль в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="cc3fe-110">**Предполагаемое время выполнения:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="cc3fe-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="cc3fe-111">В этом учебнике нет указаний по написанию приложения Azure, что предусматривает один из шагов, но показано, как авторизовать приложение для использования ключей или секретов в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="cc3fe-112">В настоящее время нельзя настроить хранилище ключей Azure на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="cc3fe-113">Вместо этого воспользуйтесь этими инструкциями по кроссплатформенному интерфейсу командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="cc3fe-114">Инструкции по Azure PowerShell см. в [этом руководстве](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="cc3fe-115">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="cc3fe-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc3fe-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cc3fe-116">Prerequisites</span></span>

<span data-ttu-id="cc3fe-117">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-117">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="cc3fe-118">подписка на Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-118">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="cc3fe-119">Если у вас нет подписки, вы можете зарегистрироваться для использования [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial);</span><span class="sxs-lookup"><span data-stu-id="cc3fe-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="cc3fe-120">Интерфейс командной строки версии 0.9.1 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="cc3fe-121">Сведения об установке последней версии и связывании ее с подпиской Azure можно найти в разделе [Установка и настройка межплатформенного интерфейса командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="cc3fe-122">приложение, для которого вы будете настраивать использование ключа или пароля, созданного по этому учебнику.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-122">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="cc3fe-123">Пример приложения доступен в [Центре загрузки Майкрософт](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="cc3fe-124">Указания см. в сопутствующем файле Readme.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-124">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="cc3fe-125">Справка по межплатформенному интерфейсу командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="cc3fe-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="cc3fe-126">В этом учебнике предполагается, что вы знакомы с интерфейсом командной строки (Bash, терминал, командная строка)</span><span class="sxs-lookup"><span data-stu-id="cc3fe-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="cc3fe-127">Параметр --help или -h может использоваться для просмотра справки по определенным командам.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-127">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="cc3fe-128">Также для получения справки можно использовать команду azure help [команда] [параметры].</span><span class="sxs-lookup"><span data-stu-id="cc3fe-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="cc3fe-129">Например, все следующие команды возвращают одинаковые сведения:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-129">For example, the following commands all return the same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="cc3fe-130">Если вы сомневаетесь в том, какие параметры необходимы команде, обратитесь к справке, используя ключ --help, -h или команду azure help [команда].</span><span class="sxs-lookup"><span data-stu-id="cc3fe-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span></span>

<span data-ttu-id="cc3fe-131">Чтобы узнать, как работать с диспетчером ресурсов Azure в межплатформенном интерфейсе командной строки Azure, также прочитайте следующие руководства:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="cc3fe-132">Установка и настройка межплатформенного интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="cc3fe-132">How to install and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="cc3fe-133">Использование межплатформенного интерфейса командной строки Azure совместно с диспетчером ресурсов</span><span class="sxs-lookup"><span data-stu-id="cc3fe-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="cc3fe-134">Подключение к своим подпискам</span><span class="sxs-lookup"><span data-stu-id="cc3fe-134">Connect to your subscriptions</span></span>

<span data-ttu-id="cc3fe-135">Чтобы войти с использованием учетной записи организации, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-135">To log in using an organizational account, use the following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="cc3fe-136">Или, чтобы войти при помощи ввода данных в интерактивном режиме:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-136">or if you want to log in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="cc3fe-137">Метод входа работает только с учетной записью организации.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-137">The login method only works with organizational account.</span></span> <span data-ttu-id="cc3fe-138">Учетная запись организации — это пользователь, который управляется вашей организацией и определен в клиенте Azure Active Directory организации.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="cc3fe-139">Если вы используете для входа в подписку Azure учетную запись Microsoft, вы можете создать учетную запись организации, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span></span>

1. <span data-ttu-id="cc3fe-140">Войдите на [портал управления Azure](https://manage.windowsazure.com/)и щелкните "Active Directory".</span><span class="sxs-lookup"><span data-stu-id="cc3fe-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="cc3fe-141">Если каталог не существует, выберите Создание каталога и укажите нужные данные.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-141">If no directory exists, select Create your directory and provide the requested information.</span></span>
3. <span data-ttu-id="cc3fe-142">Выберите каталог и добавьте нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-142">Select your directory and add a new user.</span></span> <span data-ttu-id="cc3fe-143">Этот пользователь будет представлять учетную запись организации.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-143">This new user is an organizational account.</span></span> <span data-ttu-id="cc3fe-144">При создании пользователя вам будут предоставлены электронный адрес и временный пароль.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span></span> <span data-ttu-id="cc3fe-145">Эти данные используются на следующем шаге. Сохраните их.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="cc3fe-146">На портале Azure выберите "Параметры", а затем "Администраторы".</span><span class="sxs-lookup"><span data-stu-id="cc3fe-146">From the portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="cc3fe-147">Щелкните Добавить, чтобы добавить нового пользователя в качестве соадминистратора.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-147">Select Add, and add the new user as a co-administrator.</span></span> <span data-ttu-id="cc3fe-148">Это позволит использовать вашу учетную запись организации для управления подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-148">This allows the organizational account to manage your Azure subscription.</span></span>
5. <span data-ttu-id="cc3fe-149">Выйдите из портала Azure и затем войдите снова с использованием новой рабочей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span></span> <span data-ttu-id="cc3fe-150">При первом входе в учетную запись появится запрос на изменение пароля.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-150">If this is the first time logging in with this account, you will be prompted to change the password.</span></span>

<span data-ttu-id="cc3fe-151">Дополнительные сведения об использовании рабочей учетной записи в Microsoft Azure см. в статье [Подпишитесь на Azure как организация](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="cc3fe-152">Если у вас есть несколько подписок и нужно указать лишь одну из них, которая будет использоваться для хранилища ключей Azure, введите следующую команду, чтобы увидеть подписки своей учетной записи:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="cc3fe-153">Далее, чтобы указать подписку, которую нужно использовать, введите:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-153">Then, to specify the subscription to use, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="cc3fe-154">Дополнительные сведения о настройке межплатформенного интерфейса командной строки Azure можно найти в разделе [Установка и настройка межплатформенного интерфейса командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-to-using-azure-resource-manager"></a><span data-ttu-id="cc3fe-155">Переключение в режим использования диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="cc3fe-155">Switch to using Azure Resource Manager</span></span>
<span data-ttu-id="cc3fe-156">Для хранилища ключей Azure требуется диспетчер ресурсов Azure, поэтому введите следующую команду, чтобы переключиться в режим этого диспетчера:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="cc3fe-157">Создание новой группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="cc3fe-157">Create a new resource group</span></span>
<span data-ttu-id="cc3fe-158">При использовании диспетчера ресурсов Azure все связанные ресурсы создаются внутри группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="cc3fe-159">Для примера мы создадим новую группу ресурсов с именем ContosoResourceGroup:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="cc3fe-160">Первый параметр — имя группы ресурсов, а второй параметр — его расположение.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-160">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="cc3fe-161">Для параметра расположения используйте команду `azure location list` , чтобы указать альтернативное расположение группы.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="cc3fe-162">Если вам необходима дополнительная информация, введите `azure help location`</span><span class="sxs-lookup"><span data-stu-id="cc3fe-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="cc3fe-163">Регистрация поставщика ресурсов хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="cc3fe-163">Register the Key Vault resource provider</span></span>
<span data-ttu-id="cc3fe-164">Убедитесь, что поставщик ресурсов хранилища ключей зарегистрирован в вашей подписке:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="cc3fe-165">Данную операцию достаточно выполнить один раз для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-165">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="cc3fe-166">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-166">Create a key vault</span></span>

<span data-ttu-id="cc3fe-167">Для создания хранилища ключей используйте команду `azure keyvault create` .</span><span class="sxs-lookup"><span data-stu-id="cc3fe-167">Use the `azure keyvault create` command to create a key vault.</span></span> <span data-ttu-id="cc3fe-168">Этот сценарий предусматривает три обязательных параметра: имя группы ресурсов, имя хранилища ключей и географическое расположение.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="cc3fe-169">Например, если вы используете хранилище с именем ContosoKeyVault, группу ресурсов с именем ContosoResourceGroup и расположение "Восточная Азия", введите:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="cc3fe-170">В выходных данных команды будут показаны свойства хранилища ключей, которое вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-170">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="cc3fe-171">Среди всех свойств есть два самых важных:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-171">The two most important properties are:</span></span>

* <span data-ttu-id="cc3fe-172">**Имя.** В этом примере — ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-172">**Name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="cc3fe-173">Вы будете использовать это имя для выполнения других командлетов хранилища ключей;</span><span class="sxs-lookup"><span data-stu-id="cc3fe-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="cc3fe-174">**URI хранилища.** В нашем примере — это https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="cc3fe-175">Необходимо, чтобы приложения, использующие ваше хранилище через REST API, использовали этот URI.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="cc3fe-176">Теперь ваша учетная запись Azure авторизована, и вы можете выполнять любые операции в этом хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-176">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="cc3fe-177">Пока что это недоступно для других учетных записей.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="cc3fe-178">Добавьте ключ или секретный код в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-178">Add a key or secret to the key vault</span></span>

<span data-ttu-id="cc3fe-179">Если вам необходимо создать ключ с программной защитой для собственного использования с помощью хранилища ключей Azure, используйте команду `azure key create` и введите следующее:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="cc3fe-180">Однако если у вас уже есть ключ, сохраненный в виде локального PEM-файла с именем softkey.pem, который требуется загрузить в хранилище ключей Azure, воспользуйтесь следующей командой импорта ключа из PEM-файла, которая позволяет программным образом защитить ключ в службе хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="cc3fe-181">Теперь для доступа к ключу, созданному или загруженному в хранилище ключей Azure, вы сможете использовать его URI.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="cc3fe-182">Используйте адрес **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey**, чтобы всегда получать текущую версию, и адрес **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87**, чтобы получить конкретную версию.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="cc3fe-183">Чтобы добавить секрет в хранилище ключей Azure, который представляет собой пароль с именем SQLPassword и значением Pa$$w0rd, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="cc3fe-184">Теперь пароль, добавленный в хранилище ключей Azure, можно вызвать, используя его URI.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="cc3fe-185">Используйте адрес **https://ContosoVault.vault.azure.net/secrets/SQLPassword**, чтобы всегда получать текущую версию, и адрес **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d**, чтобы получить конкретную версию.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="cc3fe-186">Давайте просмотрим только что созданный ключ или секрет.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-186">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="cc3fe-187">Чтобы просмотреть свой ключ, введите `azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="cc3fe-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="cc3fe-188">Чтобы просмотреть свой секрет, введите `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="cc3fe-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="cc3fe-189">Зарегистрируйте приложение с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="cc3fe-190">Обычно этот шаг выполняет разработчик на отдельном компьютере.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="cc3fe-191">Он не относится к хранилищу ключей Azure, но включен в этот учебник для полноты картины.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-191">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc3fe-192">Чтобы завершить прохождение этого учебника, учетная запись, хранилище и приложение, которое вы будете регистрировать на этом шаге, должны находиться в одном каталоге Azure.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="cc3fe-193">Приложения, которые используют хранилища ключей, должны пройти аутентификацию с использованием токена Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="cc3fe-194">Для этого владельцу приложения необходимо сначала зарегистрировать приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="cc3fe-195">В конце регистрации владелец приложения получает следующие значения.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-195">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="cc3fe-196">**Идентификатор приложения** (также известный как идентификатор клиента) и **ключ проверки подлинности** (также известный как общий секрет).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="cc3fe-197">Для получения токена приложение должно предоставить Azure Active Directory оба этих значения.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-197">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="cc3fe-198">Настроенный способ предоставления зависит от приложения.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-198">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="cc3fe-199">В примере приложения, использующего хранилище ключей, владелец задает эти значения в файле app.config.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="cc3fe-200">Чтобы зарегистрировать приложение в Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-200">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="cc3fe-201">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-201">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="cc3fe-202">Слева щелкните **Active Directory**, а затем выберите каталог, в котором вам необходимо зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="cc3fe-203">Вам необходимо выбрать каталог, содержащий подписку Azure, которую вы использовали для создания хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-203">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="cc3fe-204">Если вам не известно, какой это каталог, щелкните **Параметры**, найдите подписку, использованную для создания хранилища ключей, и запишите имя каталога, отображающегося в последнем столбце.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="cc3fe-205">Щелкните **ПРИЛОЖЕНИЯ**.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="cc3fe-206">Если в каталоге нет добавленных приложений, на этой странице отобразится только ссылка **Добавить приложение** .</span><span class="sxs-lookup"><span data-stu-id="cc3fe-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="cc3fe-207">Щелкните ссылку или, как вариант, можно щелкнуть **ДОБАВИТЬ** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="cc3fe-208">В мастере **Добавление приложения** на странице **What do you want to do?** (Что необходимо сделать?) щелкните **Добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="cc3fe-209">На странице **Расскажите о своем приложении** укажите имя своего приложения и выберите **Веб-приложение и/или веб-API** (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="cc3fe-210">Щелкните значок "Далее".</span><span class="sxs-lookup"><span data-stu-id="cc3fe-210">Click the Next icon.</span></span>
6. <span data-ttu-id="cc3fe-211">На странице **Свойства приложения** укажите данные в полях **URL-адрес входа** и **URI кода приложения** для своего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="cc3fe-212">Если в вашем приложении нет этих значений, можно придумать их для этого шага (например, можно указать http://test1.contoso.com в обоих полях).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="cc3fe-213">Не важно, существуют ли эти сайты. Важно то, что URI кода приложения отличается для каждого приложения в каталоге.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="cc3fe-214">Каталог использует эту строку для идентификации приложения.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-214">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="cc3fe-215">Щелкните значок "Готово", чтобы сохранить изменения в мастере.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-215">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="cc3fe-216">На странице «Быстрый запуск» щелкните **НАСТРОИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-216">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="cc3fe-217">Прокрутите страницу до раздела **Ключи**, выберите длительность и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="cc3fe-218">Страница обновится и отобразится значение ключа.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-218">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="cc3fe-219">Необходимо настроить приложение, указав это значение ключа и **идентификатор клиента**</span><span class="sxs-lookup"><span data-stu-id="cc3fe-219">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="cc3fe-220">(указания по этой конфигурации зависят от конкретного приложения).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="cc3fe-221">Скопируйте значение идентификатора клиента на этой странице. Вы будете использовать его на следующем шаге, чтобы задать разрешения в своем хранилище.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="cc3fe-222">Разрешите приложению использовать ключ или секретный код.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-222">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="cc3fe-223">Чтобы авторизовать приложение для получения доступа к ключу или секрету в хранилище, используйте команду `azure keyvault set-policy` .</span><span class="sxs-lookup"><span data-stu-id="cc3fe-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="cc3fe-224">Например, если имя хранилища — ContosoKeyVault, а идентификатор клиента приложения — 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, и нужно авторизовать это приложение для расшифровки и подписи с использованием ключей в вашем хранилище, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="cc3fe-225">При выполнении команды в командной строке Windows замените одинарные кавычки на двойные, а также экранируйте внутренние двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span></span> <span data-ttu-id="cc3fe-226">Например: "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="cc3fe-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="cc3fe-227">Если этому же приложению необходимо разрешить читать секретные данные в хранилище, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-227">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="cc3fe-228">Использование аппаратного модуля безопасности</span><span class="sxs-lookup"><span data-stu-id="cc3fe-228">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="cc3fe-229">Чтобы обеспечить более высокий уровень защиты, можно импортировать ключи или создать их в аппаратных модулях безопасности (ключи никогда не покидают их пределов).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="cc3fe-230">В качестве аппаратных модулей безопасности используются модули FIPS 140-2 с проверкой уровня 2.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-230">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="cc3fe-231">Если это требование вас не касается, пропустите этот подраздел и перейдите к подразделу [Удаление хранилища ключей, а также связанных ключей и секретов](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="cc3fe-232">Чтобы создать ключи, защищенные аппаратным модулем безопасности, у вас должна быть подписка на хранилище, которая поддерживает ключи, защищенные аппаратным модулем безопасности.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="cc3fe-233">При создании хранилища добавьте параметр sku:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-233">When you create the keyvault, add the 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="cc3fe-234">В это хранилище можно добавлять ключи с программной защитой (как показано выше) и ключи, защищенные аппаратным модулем безопасности.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="cc3fe-235">Чтобы создать ключ, защищенный аппаратным модулем безопасности, задайте значение HSM для параметра Destination:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="cc3fe-236">Вы можете использовать следующую команду для импорта ключа из PEM-файла на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-236">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="cc3fe-237">Эта команда импортирует ключ в аппаратные модули безопасности в службе хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-237">This command imports the key into HSMs in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="cc3fe-238">Следующая команда импортирует пакет собственного ключа клиента (BYOK).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-238">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="cc3fe-239">Это дает возможность создать ключ в своем локальном аппаратном модуле безопасности и передать его в аппаратные модули безопасности в службе хранилища ключей так, чтобы ключ не покидал их пределы:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="cc3fe-240">Более подробные инструкции по созданию пакета BYOK см. в статье [Создание ключей, защищенных аппаратным модулем безопасности, и их передача в хранилище ключей Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="cc3fe-241">Удаление хранилища ключей, а также связанных ключей и секретов</span><span class="sxs-lookup"><span data-stu-id="cc3fe-241">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="cc3fe-242">Если больше нет необходимости в хранилище ключей и содержащемся в нем ключе или секрете, можно удалить его, используя команду azure keyvault delete:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="cc3fe-243">Как вариант, можно удалить всю группу ресурсов Azure, которая включает в себя хранилище ключей и другие ресурсы, которые вы добавили в эту группу:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="cc3fe-244">Другие команды в межплатформенном интерфейсе командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="cc3fe-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="cc3fe-245">Вот другие команды, которые могут быть полезны при управлении хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="cc3fe-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="cc3fe-246">Эта команда перечисляет все ключи и выбранные свойства в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="cc3fe-247">Эта команда отображает полный список свойств для указанного ключа:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-247">This command displays a full list of properties for the specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="cc3fe-248">Эта команда перечисляет все имена секретов и выбранные свойства в виде таблицы:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="cc3fe-249">Пример удаления конкретного ключа:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-249">Here's an example of how to remove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="cc3fe-250">Пример удаления конкретного секрета:</span><span class="sxs-lookup"><span data-stu-id="cc3fe-250">Here's an example of how to remove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="cc3fe-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc3fe-251">Next steps</span></span>
<span data-ttu-id="cc3fe-252">Справочные материалы по программированию см. в статье [Руководство разработчика хранилища ключей Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="cc3fe-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

