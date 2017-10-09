---
title: "aaaLog в tooAzure из hello CLI | Документы Microsoft"
description: "Подключение tooyour подписки Azure из hello Azure командной строки (CLI Azure) для Mac, Linux и Windows"
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
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a><span data-ttu-id="b4717-103">Войдите в tooAzure из hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4717-103">Log in tooAzure from hello Azure CLI</span></span>
<span data-ttu-id="b4717-104">Hello Azure CLI — это набор открытым исходным кодом, кросс платформенных команды для работы с ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="b4717-104">hello Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="b4717-105">Этой статье описывается tooprovide различными способами hello вашей tooyour Azure CLI hello tooconnect учетные данные учетной записи Azure подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="b4717-105">This article describes hello different ways tooprovide your Azure account credentials tooconnect hello Azure CLI tooyour Azure subscription:</span></span>

* <span data-ttu-id="b4717-106">Запустите hello `azure login` tooauthenticate команд CLI из Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b4717-106">Run hello `azure login` CLI command tooauthenticate through Azure Active Directory.</span></span> <span data-ttu-id="b4717-107">Это дает метод, можно получить доступ к командам tooCLI в обоих [команда режимы](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="b4717-107">This method gives you access tooCLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="b4717-108">При выполнении команды hello без дополнительных параметров, `azure login` предложит toocontinue ведения журналов в интерактивном режиме веб-портале.</span><span class="sxs-lookup"><span data-stu-id="b4717-108">When you run hello command without additional options, `azure login` prompts you toocontinue logging in interactively through a web portal.</span></span> <span data-ttu-id="b4717-109">Для дополнительных `azure login` параметров см. в разделе сценарии hello в этой статье, или тип `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="b4717-109">For additional `azure login` command options, see hello scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="b4717-110">Если требуется только toouse режим управления службами Azure CLI команд (не рекомендуется для наиболее новых развертываний), можно загрузить и установить файл параметров публикации на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b4717-110">If you only need toouse Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="b4717-111">Если вы еще не установили hello CLI, см. раздел [Install hello Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b4717-111">If you haven't already installed hello CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="b4717-112">Если у вас нет подписки Azure, то всего за несколько минут можно создать [бесплатную учетную запись](http://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b4717-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="b4717-113">Основные сведения о различных удостоверениях учетной записи и подписках Azure см. в разделе [Как подписки Azure связаны с Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b4717-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="b4717-114">Сценарий 1. Интерактивный вход в Azure</span><span class="sxs-lookup"><span data-stu-id="b4717-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="b4717-115">С определенным учетным записям hello CLI требуется toorun `azure login` и продолжите процесс входа в систему hello веб-браузера через веб-портал, этот процесс называется *интерактивного входа в систему*.</span><span class="sxs-lookup"><span data-stu-id="b4717-115">With certain accounts, hello CLI requires you toorun `azure login` and then continue hello login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="b4717-116">Обычная причина — у вас есть рабочая или учебная учетная запись (также называется *учетную запись организации*), настроенная toorequire многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b4717-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up toorequire multifactor authentication.</span></span> <span data-ttu-id="b4717-117">Также используется интерактивный вход в систему с учетной записью Майкрософт команды режим toouse диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b4717-117">Also use interactive login with your Microsoft account, when you want toouse Resource Manager mode commands.</span></span>

<span data-ttu-id="b4717-118">Интерактивный вход в систему можно легко: тип `azure login` — без параметров, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="b4717-118">Interactive login is easy: type `azure login` -- without any options -- as shown in hello following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="b4717-119">выходные данные Hello появится примерно hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b4717-119">hello output appears something like hello following:</span></span>

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
<span data-ttu-id="b4717-120">Скопируйте код hello, предлагаемых tooyou в выходных данных команды hello и откройте toohttp://aka.ms/devicelogin браузера или другие страницы, если указано.</span><span class="sxs-lookup"><span data-stu-id="b4717-120">Copy hello code offered tooyou in hello command output, and open a browser toohttp://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="b4717-121">(Можно открыть браузер на hello же компьютере или на другом компьютере или устройстве.) Укажите код hello, а затем, запрашиваемые tooenter hello пользователя и пароль для удостоверения hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="b4717-121">(You can open a browser on hello same computer, or on a different computer or device.) Enter hello code, and then you are prompted tooenter hello username and password for hello identity you want toouse.</span></span> <span data-ttu-id="b4717-122">После завершения этого процесса командной оболочки hello завершения входа hello.</span><span class="sxs-lookup"><span data-stu-id="b4717-122">When that process completes, hello command shell completes hello login.</span></span> <span data-ttu-id="b4717-123">Это будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="b4717-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="b4717-124">При интерактивном входе в систему проверка подлинности и авторизация выполняются с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b4717-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="b4717-125">При использовании с удостоверением учетной записи Майкрософт, процесс входа в систему hello обращается к Azure Active Directory домена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b4717-125">If you use a Microsoft account identity, hello login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="b4717-126">(Если вы зарегистрировались для получения бесплатной учетной записи Azure, в Azure Active Directory создается домен по умолчанию для вашей учетной записи.)</span><span class="sxs-lookup"><span data-stu-id="b4717-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="b4717-127">Сценарий 2. Вход в Azure с именем пользователя и паролем</span><span class="sxs-lookup"><span data-stu-id="b4717-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="b4717-128">Используйте hello `azure login` команду с именем пользователя hello (`-u`) параметр tooauthenticate toouse рабочую или учебную учетную запись, которая не требует многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b4717-128">Use hello `azure login` command with hello username (`-u`) parameter tooauthenticate when you want toouse a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="b4717-129">Появится hello командной строки для пароля hello (или при необходимости можно передать пароль hello как дополнительный параметр hello `azure login` команды).</span><span class="sxs-lookup"><span data-stu-id="b4717-129">You are prompted at hello command line for hello password (or you can optionally pass hello password as an additional parameter of hello `azure login` command).</span></span> <span data-ttu-id="b4717-130">Hello следующий пример передает hello имя пользователя учетной записи организации:</span><span class="sxs-lookup"><span data-stu-id="b4717-130">hello following example passes hello username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="b4717-131">Вы получаете запрос tooenter пароль:</span><span class="sxs-lookup"><span data-stu-id="b4717-131">You are then prompted tooenter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="b4717-132">завершает процесс входа в систему Hello.</span><span class="sxs-lookup"><span data-stu-id="b4717-132">hello login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="b4717-133">Если это ваш первый время вход с помощью этих учетных данных, будет предложено tooverify обратиться toocache маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b4717-133">If this is your first time logging in with these credentials, you are asked tooverify that you wish toocache an authentication token.</span></span> <span data-ttu-id="b4717-134">Это предупреждение также возникает, если вы ранее использовали hello `azure logout` команда (описывается далее в статье hello).</span><span class="sxs-lookup"><span data-stu-id="b4717-134">This prompt also occurs if you previously used hello `azure logout` command (described later in hello article).</span></span> <span data-ttu-id="b4717-135">Запустите этот запрос для сценариев автоматизации toobypass `azure login` с hello `-q` параметра.</span><span class="sxs-lookup"><span data-stu-id="b4717-135">toobypass this prompt for automation scenarios, run `azure login` with hello `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="b4717-136">Сценарий 3. Вход в Azure с субъектом-службой</span><span class="sxs-lookup"><span data-stu-id="b4717-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="b4717-137">Если создание субъекта-службы для приложения Active Directory, а hello участника-службы имеет разрешения на свою подписку, воспользуйтесь hello `azure login` участника-службы hello tooauthenticate команды.</span><span class="sxs-lookup"><span data-stu-id="b4717-137">If you create a service principal for an Active Directory application, and hello service principal has permissions on your subscription, you can use hello `azure login` command tooauthenticate hello service principal.</span></span> <span data-ttu-id="b4717-138">В зависимости от вашего сценария можно предоставить учетные данные hello hello субъекта-службы как явные параметры hello `azure login` команды.</span><span class="sxs-lookup"><span data-stu-id="b4717-138">Depending on your scenario, you could provide hello credentials of hello service principal as explicit parameters of hello `azure login` command.</span></span> <span data-ttu-id="b4717-139">Например hello следующая команда передает hello имя участника-службы и идентификатор клиента Active Directory:</span><span class="sxs-lookup"><span data-stu-id="b4717-139">For example, hello following command passes hello service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="b4717-140">Вы являетесь запрашиваемые tooprovide hello пароль.</span><span class="sxs-lookup"><span data-stu-id="b4717-140">You are then prompted tooprovide hello password.</span></span> <span data-ttu-id="b4717-141">Можно предоставить учетные данные hello через интерфейс командной строки сценарий или приложение код или использовать субъекта-службы сертификатов tooauthenticate hello не в интерактивном режиме для сценариев автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b4717-141">You can also provide hello credentials through a CLI script or application code, or use a certificate tooauthenticate hello service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="b4717-142">Дополнительные сведения и примеры см. в статье [Проверка подлинности субъекта-службы в Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b4717-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="b4717-143">Сценарий 4. Использование файла параметров публикации</span><span class="sxs-lookup"><span data-stu-id="b4717-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="b4717-144">Если требуется только команды toouse hello управления службами Azure режиме CLI (например, toodeploy виртуальных машинах Azure в hello классической модели развертывания), можно подключиться с помощью файла параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="b4717-144">If you only need toouse hello Azure Service Management mode CLI commands (for example, toodeploy Azure VMs in hello classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="b4717-145">Этот метод устанавливает сертификат на локальном компьютере, который позволяет tooperform задачи управления для до тех пор, пока hello подписке и сертификате hello являются допустимыми.</span><span class="sxs-lookup"><span data-stu-id="b4717-145">This method installs a certificate on your local computer that allows you tooperform management tasks for as long as hello subscription and hello certificate are valid.</span></span>

* <span data-ttu-id="b4717-146">**файл параметров публикации toodownload hello** для вашей учетной записи убедитесь, что hello CLI находится в режиме управления службой, введя `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="b4717-146">**toodownload hello publish settings file** for your account, ensure that hello CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="b4717-147">Затем выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b4717-147">Then run hello following command:</span></span>

        azure account download

<span data-ttu-id="b4717-148">Это открывает в браузере по умолчанию и предлагает toosign в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b4717-148">This opens your default browser and prompts you toosign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="b4717-149">После входа в систему загрузится файл `.publishsettings` .</span><span class="sxs-lookup"><span data-stu-id="b4717-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="b4717-150">Запишите место сохранения этого файла.</span><span class="sxs-lookup"><span data-stu-id="b4717-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="b4717-151">Если ваша учетная запись связана с несколькими клиентами Azure Active Directory, может быть tooselect запрос, который вы хотите toodownload параметры публикации Active Directory в файле.</span><span class="sxs-lookup"><span data-stu-id="b4717-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted tooselect which Active Directory you wish toodownload a publish settings file for.</span></span>
>
>

<span data-ttu-id="b4717-152">После выбора с помощью страницы загрузки hello, или посетите hello классический портал Azure, hello выбранного Active Directory становится hello по умолчанию используется классический портал hello и страницы загрузки.</span><span class="sxs-lookup"><span data-stu-id="b4717-152">Once selected using hello download page, or by visiting hello Azure classic portal, hello selected Active Directory becomes hello default used by hello classic portal and download page.</span></span> <span data-ttu-id="b4717-153">После установки по умолчанию, вы видите текст hello "**tooreturn toohello на странице щелкните здесь**" вверху hello hello загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="b4717-153">Once a default has been established, you see hello text '**click here tooreturn toohello selection page**' at hello top of hello download page.</span></span> <span data-ttu-id="b4717-154">Используйте предоставляет ссылку tooreturn toohello выбора страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="b4717-154">Use hello provided link tooreturn toohello selection page.</span></span>

* <span data-ttu-id="b4717-155">**файл параметров публикации tooimport hello**, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b4717-155">**tooimport hello publish settings file**, run hello following command:</span></span>

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="b4717-156">После импорта вашего параметры публикации, следует удалить hello `.publishsettings` файла.</span><span class="sxs-lookup"><span data-stu-id="b4717-156">After importing your publish settings, you should delete hello `.publishsettings` file.</span></span> <span data-ttu-id="b4717-157">Он больше не требуется hello Azure CLI и представляет угрозу безопасности, как он может быть tooyour подписки используется toogain доступа.</span><span class="sxs-lookup"><span data-stu-id="b4717-157">It is no longer required by hello Azure CLI and presents a security risk as it could be used toogain access tooyour subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="b4717-158">Режимы команд CLI</span><span class="sxs-lookup"><span data-stu-id="b4717-158">CLI command modes</span></span>
<span data-ttu-id="b4717-159">Hello Azure CLI обеспечивает два режима команды для работы с ресурсами Azure, с различные наборы команд:</span><span class="sxs-lookup"><span data-stu-id="b4717-159">hello Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="b4717-160">**Режим диспетчера ресурсов** — для работы с ресурсами Azure в модель развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="b4717-160">**Resource Manager mode** - for working with Azure resources in hello Resource Manager deployment model.</span></span> <span data-ttu-id="b4717-161">tooset этот режим, выполните `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="b4717-161">tooset this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="b4717-162">**Режим управления службами** — для работы с ресурсами Azure в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="b4717-162">**Service Management mode** - for working with Azure resources in hello classic deployment model.</span></span> <span data-ttu-id="b4717-163">tooset этот режим, выполните `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="b4717-163">tooset this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="b4717-164">При первой установке hello в текущем выпуске hello CLI находится в режим диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b4717-164">When first installed, hello current release of hello CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="b4717-165">Диспетчер ресурсов Hello и режим управления службами являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="b4717-165">hello Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="b4717-166">То есть ресурсы, созданные в режиме не могут управляться из hello другим режимом.</span><span class="sxs-lookup"><span data-stu-id="b4717-166">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="b4717-167">Несколько подписок</span><span class="sxs-lookup"><span data-stu-id="b4717-167">Multiple subscriptions</span></span>
<span data-ttu-id="b4717-168">Если у вас несколько подписок Azure, подключение tooAzure предоставляет доступ tooall подписок, связанных с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="b4717-168">If you have multiple Azure subscriptions, connecting tooAzure grants access tooall subscriptions associated with your credentials.</span></span> <span data-ttu-id="b4717-169">Одна подписка по умолчанию hello и используемые hello Azure CLI, при выполнении операций.</span><span class="sxs-lookup"><span data-stu-id="b4717-169">One subscription is selected as hello default, and used by hello Azure CLI when performing operations.</span></span> <span data-ttu-id="b4717-170">Можно просмотреть подписки hello, включая текущую подписку по умолчанию hello, с помощью hello `azure account list` команды.</span><span class="sxs-lookup"><span data-stu-id="b4717-170">You can view hello subscriptions, including hello current default subscription, using hello `azure account list` command.</span></span> <span data-ttu-id="b4717-171">Эта команда возвращает аналогичные toohello следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="b4717-171">This command returns information similar toohello following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="b4717-172">В hello списка, hello **текущей** столбец показывает текущую подписку по умолчанию hello Azure-sub-1.</span><span class="sxs-lookup"><span data-stu-id="b4717-172">In hello preceding list, hello **Current** column indicates hello current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="b4717-173">Подписка по умолчанию hello toochange, используйте hello `azure account set` команду и укажите, нужно по умолчанию hello toobe подписки hello.</span><span class="sxs-lookup"><span data-stu-id="b4717-173">toochange hello default subscription, use hello `azure account set` command, and specify hello subscription that you wish toobe hello default.</span></span> <span data-ttu-id="b4717-174">Например:</span><span class="sxs-lookup"><span data-stu-id="b4717-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="b4717-175">При этом изменяется подписки по умолчанию hello tooAzure-sub-2.</span><span class="sxs-lookup"><span data-stu-id="b4717-175">This changes hello default subscription tooAzure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="b4717-176">Изменение подписки по умолчанию hello вступает в силу немедленно и глобальных изменений; новые команды Azure CLI, выполняются ли они от hello же экземпляр командной строки или в другом экземпляре, использовать новую подписку по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="b4717-176">Changing hello default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from hello same command-line instance or a different instance, use hello new default subscription.</span></span>
>
>

<span data-ttu-id="b4717-177">Если вы хотите toouse подписки не по умолчанию с hello Azure CLI, но не текущего значения по умолчанию toochange hello, можно использовать hello `--subscription` для команды hello и укажите имя hello hello подписки нужно toouse для операции hello.</span><span class="sxs-lookup"><span data-stu-id="b4717-177">If you wish toouse a non-default subscription with hello Azure CLI, but don't want toochange hello current default, you can use hello `--subscription` option for hello command and provide hello name of hello subscription you wish toouse for hello operation.</span></span>

<span data-ttu-id="b4717-178">После tooyour подключенных подписка Azure, можно запустить с помощью команды toowork hello Azure CLI с ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="b4717-178">Once you are connected tooyour Azure subscription, you can start using hello Azure CLI commands toowork with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="b4717-179">Хранение параметров CLI</span><span class="sxs-lookup"><span data-stu-id="b4717-179">Storage of CLI settings</span></span>
<span data-ttu-id="b4717-180">Ли войти hello `azure login` команды или импорт параметров публикации, профиль CLI и журналы хранятся в `.azure` каталог расположен в вашей `user` каталога.</span><span class="sxs-lookup"><span data-stu-id="b4717-180">Whether you log in with hello `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="b4717-181">Каталог `user` защищен операционной системой.</span><span class="sxs-lookup"><span data-stu-id="b4717-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="b4717-182">Тем не менее, рекомендуется выполнить дополнительные шаги tooencrypt вашей `user` каталога.</span><span class="sxs-lookup"><span data-stu-id="b4717-182">However, we recommend that you take additional steps tooencrypt your `user` directory.</span></span> <span data-ttu-id="b4717-183">Это можно сделать в hello следующих способов:</span><span class="sxs-lookup"><span data-stu-id="b4717-183">You can do so in hello following ways:</span></span>

* <span data-ttu-id="b4717-184">В Windows измените свойства directory hello или с помощью BitLocker.</span><span class="sxs-lookup"><span data-stu-id="b4717-184">On Windows, modify hello directory properties or use BitLocker.</span></span>
* <span data-ttu-id="b4717-185">На Mac включите FileVault hello каталога.</span><span class="sxs-lookup"><span data-stu-id="b4717-185">On Mac, turn on FileVault for hello directory.</span></span>
* <span data-ttu-id="b4717-186">В Ubuntu — команду используйте функцию каталог Encrypted домашней hello.</span><span class="sxs-lookup"><span data-stu-id="b4717-186">On Ubuntu, use hello Encrypted Home directory feature.</span></span> <span data-ttu-id="b4717-187">Другие дистрибутивы Linux включают аналогичные функции.</span><span class="sxs-lookup"><span data-stu-id="b4717-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="b4717-188">Выход из системы</span><span class="sxs-lookup"><span data-stu-id="b4717-188">Logging out</span></span>
<span data-ttu-id="b4717-189">toolog out hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b4717-189">toolog out, use hello following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="b4717-190">Если hello подписки, связанные с учетной записи hello только проверка подлинности выполняется с Active Directory, ведение журнала операции удаления сведений подписки hello из hello локальный профиль.</span><span class="sxs-lookup"><span data-stu-id="b4717-190">If hello subscriptions associated with hello account are only authenticated with Active Directory, logging out deletes hello subscription information from hello local profile.</span></span> <span data-ttu-id="b4717-191">Тем не менее если файл параметров публикации также был импортирован hello подписок, выход только для удаления Active Directory сведений о связанных с локальным профилем hello.</span><span class="sxs-lookup"><span data-stu-id="b4717-191">However, if a publish settings file was also imported for hello subscriptions, logging out only deletes Active Directory related information from hello local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4717-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4717-192">Next steps</span></span>
* <span data-ttu-id="b4717-193">команды toouse Azure CLI, см. [команды Azure CLI в режим диспетчера ресурсов](virtual-machines/azure-cli-arm-commands.md) и [Azure CLI команд в режиме управления службой](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b4717-193">toouse Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="b4717-194">toolearn Дополнительные сведения о hello Azure CLI Загрузка исходного кода, сообщения о проблемах, или передавать toohello проекта см. hello [репозиторий GitHub для hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="b4717-194">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="b4717-195">Если возникли проблемы при использовании hello Azure CLI или Azure, посетите hello [форумы Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="b4717-195">If you encounter problems using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
