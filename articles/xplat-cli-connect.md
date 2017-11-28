---
title: "Вход в Azure из интерфейса командной строки | Документация Майкрософт"
description: "Подключение к подписке Azure из интерфейса командной строки Azure (Azure CLI) на компьютерах Mac, Linux и Windows"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 31efab60690b54faf7992251fcd01e307c4464f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="log-in-to-azure-from-the-azure-cli"></a><span data-ttu-id="334ef-103">Войдите в Azure из командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="334ef-103">Log in to Azure from the Azure CLI</span></span>
<span data-ttu-id="334ef-104">Интерфейс командной строки Azure представляет собой набор межплатформенных команд с открытым кодом для работы с ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="334ef-104">The Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="334ef-105">В этой статье описываются различные способы предоставления учетных данных для подключения к подписке Azure из интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="334ef-105">This article describes the different ways to provide your Azure account credentials to connect the Azure CLI to your Azure subscription:</span></span>

* <span data-ttu-id="334ef-106">Выполните команду `azure login` для проверки подлинности с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="334ef-106">Run the `azure login` CLI command to authenticate through Azure Active Directory.</span></span> <span data-ttu-id="334ef-107">Этот метод предоставляет доступ к командам в обоих [режимах команд](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="334ef-107">This method gives you access to CLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="334ef-108">При выполнении команды без дополнительных параметров `azure login` предложит выполнить вход интерактивно с помощью веб-портала.</span><span class="sxs-lookup"><span data-stu-id="334ef-108">When you run the command without additional options, `azure login` prompts you to continue logging in interactively through a web portal.</span></span> <span data-ttu-id="334ef-109">Для получения сведений о дополнительных параметрах команды `azure login` обратитесь к сценариям, представленным в этой статье, или введите `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="334ef-109">For additional `azure login` command options, see the scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="334ef-110">Если необходимы только команды для режима управления службами Azure (не рекомендуется для наиболее развертываний), можно скачать и установить файл параметров публикации на компьютере.</span><span class="sxs-lookup"><span data-stu-id="334ef-110">If you only need to use Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="334ef-111">Если вы еще не установили интерфейс командной строки Azure, см. раздел [Установка интерфейса командной строки Azure](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="334ef-111">If you haven't already installed the CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="334ef-112">Если у вас нет подписки Azure, то всего за несколько минут можно создать [бесплатную учетную запись](http://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="334ef-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="334ef-113">Основные сведения о различных удостоверениях учетной записи и подписках Azure см. в разделе [Как подписки Azure связаны с Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="334ef-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="334ef-114">Сценарий 1. Интерактивный вход в Azure</span><span class="sxs-lookup"><span data-stu-id="334ef-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="334ef-115">Для определенных учетных записей в интерфейсе командной строки требуется запустить `azure login`, а затем продолжить процесс входа в систему в веб-портал в браузере. Этот процесс называется *интерактивным входом в систему*.</span><span class="sxs-lookup"><span data-stu-id="334ef-115">With certain accounts, the CLI requires you to run `azure login` and then continue the login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="334ef-116">Наиболее частая причина в том, что у вас есть рабочая или учебная учетная запись (также называемая *учетной записью организации*), для которой включено требование многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="334ef-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up to require multifactor authentication.</span></span> <span data-ttu-id="334ef-117">Также используйте интерактивный вход в систему с учетной записью Майкрософт в том случае, если вы хотите использовать режим команд Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="334ef-117">Also use interactive login with your Microsoft account, when you want to use Resource Manager mode commands.</span></span>

<span data-ttu-id="334ef-118">Для интерактивного входа в систему просто наберите `azure login` без параметров, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="334ef-118">Interactive login is easy: type `azure login` -- without any options -- as shown in the following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="334ef-119">Результаты должны быть примерно следующими.</span><span class="sxs-lookup"><span data-stu-id="334ef-119">The output appears something like the following:</span></span>

```         
info:    Executing command login
info:    To sign in, use a web browser to open the page http://aka.ms/devicelogin. Enter the code XXXXXXXXX to authenticate.
```
<span data-ttu-id="334ef-120">Скопируйте код в выходных данных команды и откройте в браузере адрес http://aka.ms/devicelogin или другую страницу, если она указана.</span><span class="sxs-lookup"><span data-stu-id="334ef-120">Copy the code offered to you in the command output, and open a browser to http://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="334ef-121">(Браузер можно открыть на том же компьютере или на другом компьютере или устройстве.) Введите код, и вам будет предложено ввести имя пользователя и пароль для удостоверения, которое нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="334ef-121">(You can open a browser on the same computer, or on a different computer or device.) Enter the code, and then you are prompted to enter the username and password for the identity you want to use.</span></span> <span data-ttu-id="334ef-122">По завершении этого процесса командная оболочка завершит процедуру входа в систему.</span><span class="sxs-lookup"><span data-stu-id="334ef-122">When that process completes, the command shell completes the login.</span></span> <span data-ttu-id="334ef-123">Это будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="334ef-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="334ef-124">При интерактивном входе в систему проверка подлинности и авторизация выполняются с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="334ef-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="334ef-125">При входе с удостоверением учетной записи Майкрософт осуществляется вход в домен Azure Active Directory по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="334ef-125">If you use a Microsoft account identity, the login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="334ef-126">(Если вы зарегистрировались для получения бесплатной учетной записи Azure, в Azure Active Directory создается домен по умолчанию для вашей учетной записи.)</span><span class="sxs-lookup"><span data-stu-id="334ef-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="334ef-127">Сценарий 2. Вход в Azure с именем пользователя и паролем</span><span class="sxs-lookup"><span data-stu-id="334ef-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="334ef-128">Если вам нужна рабочая или учебная учетная запись, не требующая многофакторной проверки подлинности, используйте для аутентификации команду `azure login` , указав параметр имени пользователя (`-u`).</span><span class="sxs-lookup"><span data-stu-id="334ef-128">Use the `azure login` command with the username (`-u`) parameter to authenticate when you want to use a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="334ef-129">Вам будет предложено ввести пароль в командной строке пароль (или при необходимости пароль можно передать как дополнительный параметр команды `azure login`).</span><span class="sxs-lookup"><span data-stu-id="334ef-129">You are prompted at the command line for the password (or you can optionally pass the password as an additional parameter of the `azure login` command).</span></span> <span data-ttu-id="334ef-130">В следующем примере передается имя пользователя учетной записи организации:</span><span class="sxs-lookup"><span data-stu-id="334ef-130">The following example passes the username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="334ef-131">Затем вам будет предложено ввести пароль.</span><span class="sxs-lookup"><span data-stu-id="334ef-131">You are then prompted to enter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="334ef-132">После этого вход в систему будет завершен.</span><span class="sxs-lookup"><span data-stu-id="334ef-132">The login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="334ef-133">Если учетные данные используются для входа в систему впервые, вам предложат указать, нужно ли кэшировать маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="334ef-133">If this is your first time logging in with these credentials, you are asked to verify that you wish to cache an authentication token.</span></span> <span data-ttu-id="334ef-134">Аналогичный запрос появляется также в том случае, если ранее вы использовали команду `azure logout` (описана далее в этой статье).</span><span class="sxs-lookup"><span data-stu-id="334ef-134">This prompt also occurs if you previously used the `azure logout` command (described later in the article).</span></span> <span data-ttu-id="334ef-135">Чтобы пропустить этот запрос в сценариях автоматизации, добавьте к команде `azure login` параметр `-q`.</span><span class="sxs-lookup"><span data-stu-id="334ef-135">To bypass this prompt for automation scenarios, run `azure login` with the `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="334ef-136">Сценарий 3. Вход в Azure с субъектом-службой</span><span class="sxs-lookup"><span data-stu-id="334ef-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="334ef-137">Если вы создали субъект-службу для приложения Active Directory, и у субъекта-службы есть разрешения для использования вашей подписки, можно выполнить команду `azure login` для проверки подлинности субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="334ef-137">If you create a service principal for an Active Directory application, and the service principal has permissions on your subscription, you can use the `azure login` command to authenticate the service principal.</span></span> <span data-ttu-id="334ef-138">В зависимости от сценария учетные данные субъекта-службы можно передавать в качестве явных параметров команды `azure login`.</span><span class="sxs-lookup"><span data-stu-id="334ef-138">Depending on your scenario, you could provide the credentials of the service principal as explicit parameters of the `azure login` command.</span></span> <span data-ttu-id="334ef-139">Например следующая команда передает имя субъекта-службы и идентификатор клиента Active Directory:</span><span class="sxs-lookup"><span data-stu-id="334ef-139">For example, the following command passes the service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="334ef-140">Затем вам будет предложено ввести пароль.</span><span class="sxs-lookup"><span data-stu-id="334ef-140">You are then prompted to provide the password.</span></span> <span data-ttu-id="334ef-141">Учетные данные также можно указать в командной строке или в коде приложения или воспользоваться сертификатом для проверки подлинности субъекта-службы в неинтерактивном режиме в сценариях автоматизации.</span><span class="sxs-lookup"><span data-stu-id="334ef-141">You can also provide the credentials through a CLI script or application code, or use a certificate to authenticate the service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="334ef-142">Дополнительные сведения и примеры см. в статье [Проверка подлинности субъекта-службы в Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="334ef-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="334ef-143">Сценарий 4. Использование файла параметров публикации</span><span class="sxs-lookup"><span data-stu-id="334ef-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="334ef-144">Если вам требуются только команды интерфейса командной строки режима управления службами Azure (например, для развертывания виртуальных машин Azure с помощью классической модели), то для подключения можно использовать файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="334ef-144">If you only need to use the Azure Service Management mode CLI commands (for example, to deploy Azure VMs in the classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="334ef-145">В этом методе на локальном компьютере устанавливается сертификат, который позволяет выполнять задачи управления до тех пор, пока подписка и сертификат действительны.</span><span class="sxs-lookup"><span data-stu-id="334ef-145">This method installs a certificate on your local computer that allows you to perform management tasks for as long as the subscription and the certificate are valid.</span></span>

* <span data-ttu-id="334ef-146">**Чтобы скачать файл параметров публикации** для своей учетной записи, переключите интерфейс командной строки в режим управления службами, набрав `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="334ef-146">**To download the publish settings file** for your account, ensure that the CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="334ef-147">Затем выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="334ef-147">Then run the following command:</span></span>

        azure account download

<span data-ttu-id="334ef-148">После этого откроется браузер по умолчанию и появится запрос на вход в [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="334ef-148">This opens your default browser and prompts you to sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="334ef-149">После входа в систему загрузится файл `.publishsettings` .</span><span class="sxs-lookup"><span data-stu-id="334ef-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="334ef-150">Запишите место сохранения этого файла.</span><span class="sxs-lookup"><span data-stu-id="334ef-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="334ef-151">Если ваша учетная запись связана с несколькими клиентами Azure Active Directory, может появиться запрос на выбор службы Active Directory, для которой следует загрузить файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="334ef-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted to select which Active Directory you wish to download a publish settings file for.</span></span>
>
>

<span data-ttu-id="334ef-152">После выбора на странице загрузки или на классическом портале Azure соответствующая служба Active Directory становится службой каталогов по умолчанию, которая будет использоваться на классическом портале и странице загрузки.</span><span class="sxs-lookup"><span data-stu-id="334ef-152">Once selected using the download page, or by visiting the Azure classic portal, the selected Active Directory becomes the default used by the classic portal and download page.</span></span> <span data-ttu-id="334ef-153">После определения службы каталогов по умолчанию в верхней части страницы загрузки появится текст "**щелкните здесь, чтобы вернуться на страницу выбора**".</span><span class="sxs-lookup"><span data-stu-id="334ef-153">Once a default has been established, you see the text '**click here to return to the selection page**' at the top of the download page.</span></span> <span data-ttu-id="334ef-154">Используйте предоставленную ссылку, чтобы вернуться на страницу выбора.</span><span class="sxs-lookup"><span data-stu-id="334ef-154">Use the provided link to return to the selection page.</span></span>

* <span data-ttu-id="334ef-155">Чтобы **импортировать файл параметров публикации**, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="334ef-155">**To import the publish settings file**, run the following command:</span></span>

        azure account import <path to your .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="334ef-156">После импорта параметров публикации файл `.publishsettings` необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="334ef-156">After importing your publish settings, you should delete the `.publishsettings` file.</span></span> <span data-ttu-id="334ef-157">Он больше не требуется интерфейсу Azure CLI и создает угрозу безопасности, поскольку может быть использован для получения доступа к подписке.</span><span class="sxs-lookup"><span data-stu-id="334ef-157">It is no longer required by the Azure CLI and presents a security risk as it could be used to gain access to your subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="334ef-158">Режимы команд CLI</span><span class="sxs-lookup"><span data-stu-id="334ef-158">CLI command modes</span></span>
<span data-ttu-id="334ef-159">Azure CLI предоставляет два режима команд для работы с ресурсами Azure, включающих разные наборы команд:</span><span class="sxs-lookup"><span data-stu-id="334ef-159">The Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="334ef-160">**Режим Resource Manager** — для работы с ресурсами Azure в модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="334ef-160">**Resource Manager mode** - for working with Azure resources in the Resource Manager deployment model.</span></span> <span data-ttu-id="334ef-161">Чтобы установить этот режим, выполните командлет `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="334ef-161">To set this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="334ef-162">**Режим управления службами** — для работы с ресурсами Azure в классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="334ef-162">**Service Management mode** - for working with Azure resources in the classic deployment model.</span></span> <span data-ttu-id="334ef-163">Чтобы установить этот режим, выполните командлет `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="334ef-163">To set this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="334ef-164">При первой установке текущего выпуска интерфейс командной строки находится в режиме Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="334ef-164">When first installed, the current release of the CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="334ef-165">Режим Resource Manager и режим управления службами являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="334ef-165">The Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="334ef-166">То есть ресурсами, созданными в одном из режимов, нельзя управлять из другого режима.</span><span class="sxs-lookup"><span data-stu-id="334ef-166">That is, resources created in one mode cannot be managed from the other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="334ef-167">Несколько подписок</span><span class="sxs-lookup"><span data-stu-id="334ef-167">Multiple subscriptions</span></span>
<span data-ttu-id="334ef-168">Если у вас есть несколько подписок Azure, то при подключении к Azure вы получаете доступ ко всем подпискам, связанным с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="334ef-168">If you have multiple Azure subscriptions, connecting to Azure grants access to all subscriptions associated with your credentials.</span></span> <span data-ttu-id="334ef-169">При этом одна подписка выбирается по умолчанию и используется для выполнения операций в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="334ef-169">One subscription is selected as the default, and used by the Azure CLI when performing operations.</span></span> <span data-ttu-id="334ef-170">Для просмотра подписок, включая текущую подписку по умолчанию, выполните команду `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="334ef-170">You can view the subscriptions, including the current default subscription, using the `azure account list` command.</span></span> <span data-ttu-id="334ef-171">Эта команда возвращает сведения следующего вида:</span><span class="sxs-lookup"><span data-stu-id="334ef-171">This command returns information similar to the following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="334ef-172">В приведенном выше списке в столбце **Текущая** указана текущая подписка по умолчанию — Azure-sub-1.</span><span class="sxs-lookup"><span data-stu-id="334ef-172">In the preceding list, the **Current** column indicates the current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="334ef-173">Для изменения подписки по умолчанию используйте команду `azure account set` , указав соответствующую подписку.</span><span class="sxs-lookup"><span data-stu-id="334ef-173">To change the default subscription, use the `azure account set` command, and specify the subscription that you wish to be the default.</span></span> <span data-ttu-id="334ef-174">Например:</span><span class="sxs-lookup"><span data-stu-id="334ef-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="334ef-175">Это приведет к изменению подписки по умолчанию на Azure-sub-2.</span><span class="sxs-lookup"><span data-stu-id="334ef-175">This changes the default subscription to Azure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="334ef-176">Изменение подписки по умолчанию вступает в силу немедленно и является глобальным изменением. При выполнении новых команд в том же или в другом экземпляре командной строки будет использоваться новая подписка по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="334ef-176">Changing the default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from the same command-line instance or a different instance, use the new default subscription.</span></span>
>
>

<span data-ttu-id="334ef-177">Если вы хотите при работе с Azure CLI использовать подписку, которая не выбрана по умолчанию, но не хотите менять текущие настройки, вы можете использовать параметр `--subscription` , указав имя подписки, которую следует использовать для данной операции.</span><span class="sxs-lookup"><span data-stu-id="334ef-177">If you wish to use a non-default subscription with the Azure CLI, but don't want to change the current default, you can use the `--subscription` option for the command and provide the name of the subscription you wish to use for the operation.</span></span>

<span data-ttu-id="334ef-178">Подключившись к подписке Azure, можно приступать к использованию команд Azure CLI для работы с ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="334ef-178">Once you are connected to your Azure subscription, you can start using the Azure CLI commands to work with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="334ef-179">Хранение параметров CLI</span><span class="sxs-lookup"><span data-stu-id="334ef-179">Storage of CLI settings</span></span>
<span data-ttu-id="334ef-180">Если для входа в систему используется команда `azure login` или импорт параметров публикации, то профиль интерфейса командной строки и журналы сохраняются в каталог `.azure`, который находится в каталоге `user`.</span><span class="sxs-lookup"><span data-stu-id="334ef-180">Whether you log in with the `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="334ef-181">Каталог `user` защищен операционной системой.</span><span class="sxs-lookup"><span data-stu-id="334ef-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="334ef-182">Тем не менее рекомендуется принять дополнительные меры для шифрования каталога `user`.</span><span class="sxs-lookup"><span data-stu-id="334ef-182">However, we recommend that you take additional steps to encrypt your `user` directory.</span></span> <span data-ttu-id="334ef-183">Это можно сделать одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="334ef-183">You can do so in the following ways:</span></span>

* <span data-ttu-id="334ef-184">В ОС Windows измените свойства каталога или используйте BitLocker.</span><span class="sxs-lookup"><span data-stu-id="334ef-184">On Windows, modify the directory properties or use BitLocker.</span></span>
* <span data-ttu-id="334ef-185">В ОС Mac включите FileVault для этого каталога.</span><span class="sxs-lookup"><span data-stu-id="334ef-185">On Mac, turn on FileVault for the directory.</span></span>
* <span data-ttu-id="334ef-186">В ОС Ubuntu используйте функцию каталога Encrypted Home.</span><span class="sxs-lookup"><span data-stu-id="334ef-186">On Ubuntu, use the Encrypted Home directory feature.</span></span> <span data-ttu-id="334ef-187">Другие дистрибутивы Linux включают аналогичные функции.</span><span class="sxs-lookup"><span data-stu-id="334ef-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="334ef-188">Выход из системы</span><span class="sxs-lookup"><span data-stu-id="334ef-188">Logging out</span></span>
<span data-ttu-id="334ef-189">Чтобы выйти из системы, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="334ef-189">To log out, use the following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="334ef-190">Если для проверки подлинности подписок, связанных с учетной записью, используется только Active Directory, при выходе из системы данные о подписке удаляются из локального профиля.</span><span class="sxs-lookup"><span data-stu-id="334ef-190">If the subscriptions associated with the account are only authenticated with Active Directory, logging out deletes the subscription information from the local profile.</span></span> <span data-ttu-id="334ef-191">Однако если вы также импортировали файл параметров публикации для подписок, то при выходе из системы из локального профиля удаляются только данные, относящиеся к Active Directory.</span><span class="sxs-lookup"><span data-stu-id="334ef-191">However, if a publish settings file was also imported for the subscriptions, logging out only deletes Active Directory related information from the local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="334ef-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="334ef-192">Next steps</span></span>
* <span data-ttu-id="334ef-193">Инструкции по работе с командами интерфейса командной строки Azure см. в статьях [Интерфейс командной строки Azure в режиме Resource Manager](virtual-machines/azure-cli-arm-commands.md) и [Интерфейс командной строки Azure в режиме управления службами](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="334ef-193">To use Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="334ef-194">Для того чтобы получить дополнительные сведения об интерфейсе командной строки Azure, скачать исходный код, сообщить о проблемах или принять участие в проекте, зайдите в [репозиторий GitHub для интерфейса командной строки Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="334ef-194">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="334ef-195">Если у вас возникли проблемы с использованием Azure CLI или Azure, посетите [форумы Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="334ef-195">If you encounter problems using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
