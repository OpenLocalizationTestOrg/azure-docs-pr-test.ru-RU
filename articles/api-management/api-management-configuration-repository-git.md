---
title: "aaaConfigure вашей службе управления API, с помощью Git - Azure | Документы Microsoft"
description: "Узнайте, как toosave и настройки конфигурации службы управления API, с помощью Git."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="ffad0-103">Как toosave и настройки конфигурации службы управления API, с помощью Git</span><span class="sxs-lookup"><span data-stu-id="ffad0-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="ffad0-104">Каждый экземпляр службы управления API поддерживает базу данных конфигурации, содержащий сведения о конфигурации hello и метаданных для экземпляра службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="ffad0-105">Изменения могут выполняться экземпляр службы toohello, изменив параметр в портал издателя hello, с помощью командлета PowerShell или сделав вызова интерфейса API REST.</span><span class="sxs-lookup"><span data-stu-id="ffad0-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="ffad0-106">В дополнение к этому toothese методов, можно также управлять конфигурацию экземпляра службы с помощью Git, такие как Включение сценариев управления службы:</span><span class="sxs-lookup"><span data-stu-id="ffad0-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="ffad0-107">Управление версиями конфигурации — скачивание и хранение различных версий конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="ffad0-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="ffad0-108">Массового изменения конфигурации — вносить изменения в ваш локальный репозиторий в toomultiple части конфигурации службы и интеграции сервера задней toohello hello изменения с одной операцией</span><span class="sxs-lookup"><span data-stu-id="ffad0-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="ffad0-109">Знакомых инструментов Git и рабочий процесс — использовать инструментарий Git hello и рабочие процессы, которые вы уже знакомы с</span><span class="sxs-lookup"><span data-stu-id="ffad0-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="ffad0-110">Следующая схема Hello приведен обзор способов tooconfigure hello вашего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="ffad0-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![Настройка с помощью Git][api-management-git-configure]

<span data-ttu-id="ffad0-112">При внесении изменений с помощью портала издателя hello, командлеты PowerShell или hello REST API службы tooyour вы управляете база данных конфигурации службы с помощью hello `https://{name}.management.azure-api.net` конечной точки, как показано hello правой части схемы hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="ffad0-113">Hello слева hello диаграммы показано, как можно управлять конфигурации службы с помощью Git и репозитория Git в службе, расположенный `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="ffad0-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="ffad0-114">следующие шаги Hello предоставляют Обзор управления вашего экземпляра службы управления API, с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="ffad0-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="ffad0-115">Доступ к конфигурации Git в службе</span><span class="sxs-lookup"><span data-stu-id="ffad0-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="ffad0-116">Сохранить репозиторий Git tooyour базы данных конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="ffad0-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="ffad0-117">Клонирование hello репозитория Git tooyour локального компьютера</span><span class="sxs-lookup"><span data-stu-id="ffad0-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="ffad0-118">По запросу hello последнюю репозитория вниз tooyour локального компьютера и фиксации и принудительного занесения репозитория задней tooyour изменения</span><span class="sxs-lookup"><span data-stu-id="ffad0-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="ffad0-119">Развертывание изменений hello из вашего репозитория в базу данных конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="ffad0-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="ffad0-120">В этой статье описывается как tooenable и использовать Git toomanage конфигурации службы и ссылки для hello файлов и папок в репозитории hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="ffad0-121">Доступ к конфигурации Git в службе</span><span class="sxs-lookup"><span data-stu-id="ffad0-121">Access Git configuration in your service</span></span>
<span data-ttu-id="ffad0-122">Можно быстро просмотреть состояние hello конфигурации Git, просмотрев hello Git значок в правом верхнем углу hello hello портала издателя.</span><span class="sxs-lookup"><span data-stu-id="ffad0-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="ffad0-123">В этом примере сообщение о состоянии hello указывает на наличие toohello репозитория несохраненных изменений.</span><span class="sxs-lookup"><span data-stu-id="ffad0-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="ffad0-124">Это так, как база данных конфигурации службы управления API hello еще не были сохранены toohello репозитория.</span><span class="sxs-lookup"><span data-stu-id="ffad0-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![Состояние Git][api-management-git-icon-enable]

<span data-ttu-id="ffad0-126">tooview и настроить параметры конфигурации Git, можно щелкнуть значок Git hello, или щелкните hello **безопасности** меню и перейдите toohello **репозиторий конфигураций** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ffad0-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![Включение доступа к GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="ffad0-128">Все секреты, которые не определены как свойства сохраняются в репозитории hello и будет оставаться в журнал только после отключения и повторного включения доступа Git.</span><span class="sxs-lookup"><span data-stu-id="ffad0-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="ffad0-129">Свойства предоставляют toomanage надежном месте постоянные строковые значения, включая секретные данные, для всех API конфигурации и политики, поэтому не нужно toostore их непосредственно в инструкциях политики.</span><span class="sxs-lookup"><span data-stu-id="ffad0-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="ffad0-130">Дополнительные сведения см. в разделе [как toouse свойств политики управления API Azure](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="ffad0-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="ffad0-131">Сведения по включению и отключению Git доступ с помощью hello REST API см. в разделе [разрешить или запретить доступ Git с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="ffad0-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="ffad0-132">репозиторий Git toohello конфигурации службы toosave hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="ffad0-133">Первым шагом Hello перед клонированием репозитория hello является toosave hello текущее состояние конфигурации toohello hello службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="ffad0-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="ffad0-134">Нажмите кнопку **сохранить toorepository конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="ffad0-134">Click **Save configuration toorepository**.</span></span>

![Сохранение конфигурации][api-management-save-configuration]

<span data-ttu-id="ffad0-136">Внесите необходимые изменения на экране подтверждения hello и нажмите кнопку **ОК** toosave.</span><span class="sxs-lookup"><span data-stu-id="ffad0-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![Сохранение конфигурации][api-management-save-configuration-confirm]

<span data-ttu-id="ffad0-138">Через несколько секунд hello конфигурация сохраняется и отображается состояние конфигурации hello hello репозитория, в том числе hello дату и время последнего изменения конфигурации hello и hello последней синхронизации конфигурации службы hello и hello репозиторий.</span><span class="sxs-lookup"><span data-stu-id="ffad0-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![Состояние конфигурации][api-management-configuration-status]

<span data-ttu-id="ffad0-140">После сохранения конфигурации hello toohello репозиторий можно клонировать.</span><span class="sxs-lookup"><span data-stu-id="ffad0-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="ffad0-141">Дополнительные сведения о выполнении этой операции с помощью API-интерфейса REST hello. в разделе [конфигурации фиксации моментальных снимков с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="ffad0-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="ffad0-142">tooclone hello tooyour хранилище локального компьютера</span><span class="sxs-lookup"><span data-stu-id="ffad0-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="ffad0-143">tooclone репозитория, необходимо репозитория tooyour hello URL-адрес, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="ffad0-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="ffad0-144">Hello имя пользователя и URL-адреса отображаются вверху hello hello **репозиторий конфигураций** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ffad0-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![Клонирование репозитория Git][api-management-configuration-git-clone]

<span data-ttu-id="ffad0-146">пароль Hello создается внизу hello hello **репозиторий конфигураций** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ffad0-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![Создание пароля][api-management-generate-password]

<span data-ttu-id="ffad0-148">toogenerate пароль, сначала убедитесь, что hello **срока действия** toohello требуемого Дата окончания срока действия и время, а затем нажмите кнопку **создать токен**.</span><span class="sxs-lookup"><span data-stu-id="ffad0-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![Пароль][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="ffad0-150">Запомните этот пароль.</span><span class="sxs-lookup"><span data-stu-id="ffad0-150">Make a note of this password.</span></span> <span data-ttu-id="ffad0-151">После закрытия этого пароля страницы приветствия больше не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="ffad0-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="ffad0-152">Следующие примеры использования hello Git Bash Hello средства из [Git для Windows](http://www.git-scm.com/downloads) , но можно использовать любое средство Git, вам знакомы.</span><span class="sxs-lookup"><span data-stu-id="ffad0-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="ffad0-153">Откройте ваш инструмент Git в нужной папке hello и запустите hello следующая команда tooclone hello git репозитория tooyour локального компьютера, с помощью команды hello, предоставляемые hello портала издателя.</span><span class="sxs-lookup"><span data-stu-id="ffad0-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="ffad0-154">Укажите имя пользователя hello и пароль при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="ffad0-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="ffad0-155">При появлении ошибки, попробуйте изменить ваш `git clone` команды tooinclude hello пользователя имя и пароль, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="ffad0-156">Если это обеспечивает ошибку, попробуйте hello пароль часть команды hello кодирование URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="ffad0-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="ffad0-157">Один toodo быстро это tooopen Visual Studio, и проблема hello следующие команды в hello **окна интерпретации**.</span><span class="sxs-lookup"><span data-stu-id="ffad0-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="ffad0-158">tooopen hello **окна интерпретации**, открыть все решение или проект в Visual Studio (или создайте новый пустой консольное приложение) и выберите **Windows**, **Интерпретация** из Hello **отладки** меню.</span><span class="sxs-lookup"><span data-stu-id="ffad0-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="ffad0-159">Используйте пароль в кодировке hello вместе с пользователем имя и репозитория расположение tooconstruct hello git команду.</span><span class="sxs-lookup"><span data-stu-id="ffad0-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="ffad0-160">После клонирования репозитория hello можно просматривать и работать с ними в локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="ffad0-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="ffad0-161">Дополнительные сведения см. в разделе [Справочные сведения по структуре файлов и папок локального репозитория Git](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="ffad0-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="ffad0-162">tooupdate ваш локальный репозиторий с hello последнюю конфигурацию экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="ffad0-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="ffad0-163">При внесении экземпляра службы управления API tooyour изменений в портал издателя hello или с помощью API-интерфейса REST hello репозитория toohello эти изменения необходимо сохранить перед обновлением ваш локальный репозиторий с последними изменениями hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="ffad0-164">toodo, нажмите кнопку **сохранить конфигурации toorepository** на hello **репозиторий конфигураций** в портал издателя hello, а затем выполните следующую команду в ваш локальный репозиторий hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="ffad0-165">Перед запуском `git pull` убедитесь, что вы находитесь в папке hello ваш локальный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="ffad0-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="ffad0-166">Если Вы завершили hello `git clone` команды, то необходимо изменить, выполнив команду следующего вида hello hello каталог tooyour репозитория.</span><span class="sxs-lookup"><span data-stu-id="ffad0-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="ffad0-167">изменения toopush из вашего репозитория сервера toohello локального репозитория</span><span class="sxs-lookup"><span data-stu-id="ffad0-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="ffad0-168">изменяет toopush из репозитория сервера toohello локального репозитория, необходимо сохранить изменения и отправить их toohello серверный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="ffad0-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="ffad0-169">toocommit изменения, откройте ваш Git средство командной строки, коммутатор toohello каталог локального репозитория, а проблема hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="ffad0-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="ffad0-170">toopush все hello фиксирует toohello сервером, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="ffad0-171">toodeploy любой службы конфигурации изменения toohello экземпляра службы управления API</span><span class="sxs-lookup"><span data-stu-id="ffad0-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="ffad0-172">После фиксации и внедренные toohello серверный репозиторий, локальных изменений их можно развернуть tooyour экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="ffad0-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![Развернуть][api-management-configuration-deploy]

<span data-ttu-id="ffad0-174">Дополнительные сведения о выполнении этой операции с помощью API-интерфейса REST hello. в разделе [Git развернуть изменения tooconfiguration базы данных с помощью API-интерфейса REST hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="ffad0-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="ffad0-175">Справочные сведения по структуре файлов и папок локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="ffad0-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="ffad0-176">Hello файлов и папок в локальном репозитории hello содержат hello конфигурации сведения о hello экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="ffad0-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="ffad0-177">Элемент</span><span class="sxs-lookup"><span data-stu-id="ffad0-177">Item</span></span> | <span data-ttu-id="ffad0-178">Описание</span><span class="sxs-lookup"><span data-stu-id="ffad0-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ffad0-179">Корневая папка api-management</span><span class="sxs-lookup"><span data-stu-id="ffad0-179">root api-management folder</span></span> |<span data-ttu-id="ffad0-180">Содержит конфигурации верхнего уровня для экземпляра службы hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="ffad0-181">Папка apis</span><span class="sxs-lookup"><span data-stu-id="ffad0-181">apis folder</span></span> |<span data-ttu-id="ffad0-182">Содержит настройки hello hello API-интерфейсы в экземпляре службы hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="ffad0-183">Папка groups</span><span class="sxs-lookup"><span data-stu-id="ffad0-183">groups folder</span></span> |<span data-ttu-id="ffad0-184">Содержит hello конфигурацию для группы hello в экземпляре службы hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="ffad0-185">Папка policies</span><span class="sxs-lookup"><span data-stu-id="ffad0-185">policies folder</span></span> |<span data-ttu-id="ffad0-186">Содержит политики hello в экземпляре службы hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="ffad0-187">Папка portalStyles</span><span class="sxs-lookup"><span data-stu-id="ffad0-187">portalStyles folder</span></span> |<span data-ttu-id="ffad0-188">Содержит hello конфигурации для настройки портала разработчиков hello в экземпляре службы hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="ffad0-189">Папка products</span><span class="sxs-lookup"><span data-stu-id="ffad0-189">products folder</span></span> |<span data-ttu-id="ffad0-190">Содержит настройки hello hello продуктов в экземпляре службы hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="ffad0-191">Папка templates</span><span class="sxs-lookup"><span data-stu-id="ffad0-191">templates folder</span></span> |<span data-ttu-id="ffad0-192">Содержит настройки hello hello шаблонов сообщений электронной почты в экземпляре службы hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="ffad0-193">В каждой папке может находиться один или несколько файлов и в некоторых случаях одна или несколько папок, например папка для каждого API, продукта или группы.</span><span class="sxs-lookup"><span data-stu-id="ffad0-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="ffad0-194">Hello файлов в каждой папке характерные для типа сущности hello, описываемого hello имя папки.</span><span class="sxs-lookup"><span data-stu-id="ffad0-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="ffad0-195">Тип файла</span><span class="sxs-lookup"><span data-stu-id="ffad0-195">File type</span></span> | <span data-ttu-id="ffad0-196">Назначение</span><span class="sxs-lookup"><span data-stu-id="ffad0-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="ffad0-197">json</span><span class="sxs-lookup"><span data-stu-id="ffad0-197">json</span></span> |<span data-ttu-id="ffad0-198">Сведения о соответствующей сущности hello конфигурации</span><span class="sxs-lookup"><span data-stu-id="ffad0-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="ffad0-199">html</span><span class="sxs-lookup"><span data-stu-id="ffad0-199">html</span></span> |<span data-ttu-id="ffad0-200">Описание сущности hello, часто отображается на портале разработчиков hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="ffad0-201">xml</span><span class="sxs-lookup"><span data-stu-id="ffad0-201">xml</span></span> |<span data-ttu-id="ffad0-202">Правила политики</span><span class="sxs-lookup"><span data-stu-id="ffad0-202">Policy statements</span></span> |
| <span data-ttu-id="ffad0-203">css</span><span class="sxs-lookup"><span data-stu-id="ffad0-203">css</span></span> |<span data-ttu-id="ffad0-204">Таблицы стилей для настройки портала разработчика</span><span class="sxs-lookup"><span data-stu-id="ffad0-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="ffad0-205">Эти файлы можно создать, удалить, изменить и управляются на локальной файловой системе, и изменения hello развернуты задней toohello вашего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="ffad0-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="ffad0-206">Hello следующие сущности не хранятся в репозитории hello и не может быть настроен с использованием Git.</span><span class="sxs-lookup"><span data-stu-id="ffad0-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="ffad0-207">Пользователи</span><span class="sxs-lookup"><span data-stu-id="ffad0-207">Users</span></span>
> * <span data-ttu-id="ffad0-208">Подписки</span><span class="sxs-lookup"><span data-stu-id="ffad0-208">Subscriptions</span></span>
> * <span data-ttu-id="ffad0-209">Свойства</span><span class="sxs-lookup"><span data-stu-id="ffad0-209">Properties</span></span>
> * <span data-ttu-id="ffad0-210">Сущности портала разработчика, отличные от стилей</span><span class="sxs-lookup"><span data-stu-id="ffad0-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="ffad0-211">Корневая папка api-management</span><span class="sxs-lookup"><span data-stu-id="ffad0-211">Root api-management folder</span></span>
<span data-ttu-id="ffad0-212">корневой Hello `api-management` папка содержит `configuration.json` файл со сведениями о hello экземпляру службы в кодировке hello верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="ffad0-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="ffad0-213">Здравствуйте первых четырех параметров (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, и `UserRegistrationTermsConsentRequired`) сопоставить следующие параметры на hello toohello **удостоверения** hello на вкладке **безопасности** раздела.</span><span class="sxs-lookup"><span data-stu-id="ffad0-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="ffad0-214">Параметр удостоверения</span><span class="sxs-lookup"><span data-stu-id="ffad0-214">Identity setting</span></span> | <span data-ttu-id="ffad0-215">Сопоставляет слишком</span><span class="sxs-lookup"><span data-stu-id="ffad0-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="ffad0-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="ffad0-216">RegistrationEnabled</span></span> |<span data-ttu-id="ffad0-217">**Анонимные пользователи в toosign страницы перенаправления** флажок</span><span class="sxs-lookup"><span data-stu-id="ffad0-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="ffad0-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="ffad0-218">UserRegistrationTerms</span></span> |<span data-ttu-id="ffad0-219">**Условия использования при регистрации пользователя** </span><span class="sxs-lookup"><span data-stu-id="ffad0-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="ffad0-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="ffad0-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="ffad0-221">**Показывать условия использования на странице регистрации** </span><span class="sxs-lookup"><span data-stu-id="ffad0-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="ffad0-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="ffad0-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="ffad0-223">**Требовать согласия** </span><span class="sxs-lookup"><span data-stu-id="ffad0-223">**Require consent** checkbox</span></span> |

![Параметры удостоверений][api-management-identity-settings]

<span data-ttu-id="ffad0-225">Здравствуйте следующие четыре параметры (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, и `DelegationValidationKey`) сопоставить следующие параметры на hello toohello **делегирования** hello на вкладке **безопасности** раздела.</span><span class="sxs-lookup"><span data-stu-id="ffad0-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="ffad0-226">Параметр делегирования</span><span class="sxs-lookup"><span data-stu-id="ffad0-226">Delegation setting</span></span> | <span data-ttu-id="ffad0-227">Сопоставляет слишком</span><span class="sxs-lookup"><span data-stu-id="ffad0-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="ffad0-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="ffad0-228">DelegationEnabled</span></span> |<span data-ttu-id="ffad0-229">Флажок **Делегировать вход и регистрацию**</span><span class="sxs-lookup"><span data-stu-id="ffad0-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="ffad0-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="ffad0-230">DelegationUrl</span></span> |<span data-ttu-id="ffad0-231">**URL-адрес конечной точки делегирования** </span><span class="sxs-lookup"><span data-stu-id="ffad0-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="ffad0-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="ffad0-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="ffad0-233">**Делегировать подписку на продукт** </span><span class="sxs-lookup"><span data-stu-id="ffad0-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="ffad0-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="ffad0-234">DelegationValidationKey</span></span> |<span data-ttu-id="ffad0-235">**Делегировать ключ проверки** </span><span class="sxs-lookup"><span data-stu-id="ffad0-235">**Delegate Validation Key** textbox</span></span> |

![Параметры делегирования][api-management-delegation-settings]

<span data-ttu-id="ffad0-237">Здравствуйте, Окончательная настройка `$ref-policy`, сопоставляет файл инструкций toohello глобальную политику для экземпляра службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="ffad0-238">Папка apis</span><span class="sxs-lookup"><span data-stu-id="ffad0-238">apis folder</span></span>
<span data-ttu-id="ffad0-239">Hello `apis` содержит папку для каждого API в экземпляре службы hello, содержащий hello следующих элементов.</span><span class="sxs-lookup"><span data-stu-id="ffad0-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="ffad0-240">`apis\<api name>\configuration.json`-Это hello конфигурация для hello API и содержит сведения об операции hello и URL-адрес службы hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="ffad0-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="ffad0-241">Это hello же данные, что будет возвращено, если были toocall [получить определенный API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) с `export=true` в `application/json` формате.</span><span class="sxs-lookup"><span data-stu-id="ffad0-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="ffad0-242">`apis\<api name>\api.description.html`— Это описание hello hello API, соответствует toohello `description` свойство hello [сущность API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="ffad0-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="ffad0-243">`apis\<api name>\operations\`-Эта папка содержит `<operation name>.description.html` файлы, которые toohello операции сопоставления в hello API.</span><span class="sxs-lookup"><span data-stu-id="ffad0-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="ffad0-244">Каждый файл содержит описание hello одной операции в hello API, который сопоставляет toohello `description` свойство hello [сущности операции](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) в hello REST API.</span><span class="sxs-lookup"><span data-stu-id="ffad0-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="ffad0-245">Папка groups</span><span class="sxs-lookup"><span data-stu-id="ffad0-245">groups folder</span></span>
<span data-ttu-id="ffad0-246">Hello `groups` содержит папку для каждой группы, определенные в экземпляре службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="ffad0-247">`groups\<group name>\configuration.json`-Это hello конфигурацию для группы hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="ffad0-248">Это hello же данные, что будет возвращено, если были toocall hello [получить имя конкретной группы](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) операции.</span><span class="sxs-lookup"><span data-stu-id="ffad0-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="ffad0-249">`groups\<group name>\description.html`— Это описание hello группы hello и соответствует toohello `description` свойство hello [группы сущности](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="ffad0-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="ffad0-250">Папка policies</span><span class="sxs-lookup"><span data-stu-id="ffad0-250">policies folder</span></span>
<span data-ttu-id="ffad0-251">Hello `policies` папка содержит операторы политики hello для вашего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="ffad0-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="ffad0-252">`policies\global.xml` содержит политики, определенные в глобальной области для экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="ffad0-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="ffad0-253">`policies\apis\<api name>\` — если в области API определены какие-либо политики, они содержатся в этой папке.</span><span class="sxs-lookup"><span data-stu-id="ffad0-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="ffad0-254">`policies\apis\<api name>\<operation name>\`Папка — Если у вас есть какие-либо политики, определенные в области операции, они содержатся в этой папке в `<operation name>.xml` файлы сопоставления toohello инструкций политики для каждой операции.</span><span class="sxs-lookup"><span data-stu-id="ffad0-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="ffad0-255">`policies\products\`— Если у вас есть какие-либо политики, определенные в области продукта, они содержатся в этой папке, которая содержит `<product name>.xml` файлы сопоставления toohello инструкций политики для каждого продукта.</span><span class="sxs-lookup"><span data-stu-id="ffad0-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="ffad0-256">Папка portalStyles</span><span class="sxs-lookup"><span data-stu-id="ffad0-256">portalStyles folder</span></span>
<span data-ttu-id="ffad0-257">Hello `portalStyles` папка содержит конфигурацию и стиля таблицы для настройки портала разработчиков для экземпляра службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="ffad0-258">`portalStyles\configuration.json`-содержит имена hello hello таблиц стилей, используемых портал разработчиков hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="ffad0-259">`portalStyles\<style name>.css`-каждого `<style name>.css` файл содержит стили для портала разработчиков hello (`Preview.css` и `Production.css` по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="ffad0-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="ffad0-260">Папка products</span><span class="sxs-lookup"><span data-stu-id="ffad0-260">products folder</span></span>
<span data-ttu-id="ffad0-261">Hello `products` содержит папку для каждого продукта, определенных в экземпляре службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="ffad0-262">`products\<product name>\configuration.json`-Это конфигурация hello hello продукта.</span><span class="sxs-lookup"><span data-stu-id="ffad0-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="ffad0-263">Это hello же данные, что будет возвращено, если были toocall hello [получить определенный продукт](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) операции.</span><span class="sxs-lookup"><span data-stu-id="ffad0-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="ffad0-264">`products\<product name>\product.description.html`— Это описание hello hello продукта и соответствует toohello `description` свойство hello [сущности «Продукт»](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) в hello REST API.</span><span class="sxs-lookup"><span data-stu-id="ffad0-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="ffad0-265">шаблоны</span><span class="sxs-lookup"><span data-stu-id="ffad0-265">templates</span></span>
<span data-ttu-id="ffad0-266">Hello `templates` папка содержит конфигурацию для hello [шаблоны электронной почты](api-management-howto-configure-notifications.md) hello экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="ffad0-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="ffad0-267">`<template name>\configuration.json`-Это конфигурация hello для шаблона сообщения электронной почты hello.</span><span class="sxs-lookup"><span data-stu-id="ffad0-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="ffad0-268">`<template name>\body.html`— Это текст hello hello шаблона сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="ffad0-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffad0-269">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ffad0-269">Next steps</span></span>
<span data-ttu-id="ffad0-270">Сведения о других способах toomanage вашего экземпляра службы. в разделе:</span><span class="sxs-lookup"><span data-stu-id="ffad0-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="ffad0-271">Управление Вашего экземпляра службы с помощью hello следующие командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffad0-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="ffad0-272">Справочник по командлетам PowerShell для развертывания службы</span><span class="sxs-lookup"><span data-stu-id="ffad0-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="ffad0-273">Справочник по командлетам PowerShell для управления службами</span><span class="sxs-lookup"><span data-stu-id="ffad0-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="ffad0-274">Управление экземпляр службы в портал издателя hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="ffad0-275">Управление вашим первым API</span><span class="sxs-lookup"><span data-stu-id="ffad0-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="ffad0-276">Управление Вашего экземпляра службы с помощью API-интерфейса REST hello</span><span class="sxs-lookup"><span data-stu-id="ffad0-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="ffad0-277">Справочник по REST API для управления API</span><span class="sxs-lookup"><span data-stu-id="ffad0-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="ffad0-278">Просмотр видеообзора</span><span class="sxs-lookup"><span data-stu-id="ffad0-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




