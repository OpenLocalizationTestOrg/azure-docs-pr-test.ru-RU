---
title: "Настройка службы управления API в Azure с помощью Git | Документация Майкрософт"
description: "Узнайте, как сохранить и настроить конфигурацию службы управления API с помощью Git."
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
ms.openlocfilehash: f5d6bb7ccbf15424e9940ccda2fac668a2af5a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="da20f-103">Сохранение и настройка конфигурации службы управления API с помощью Git</span><span class="sxs-lookup"><span data-stu-id="da20f-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="da20f-104">Каждый экземпляр службы управления API поддерживает базу данных конфигурации, содержащую сведения о конфигурации и метаданных для экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="da20f-105">Внесение изменений в экземпляр службы выполняется путем изменения параметра на портале издателя с помощью командлета PowerShell или вызова REST API.</span><span class="sxs-lookup"><span data-stu-id="da20f-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="da20f-106">Помимо этих методов для управления конфигурацией экземпляра службы можно использовать Git для реализации приведенных далее сценариев управления службой.</span><span class="sxs-lookup"><span data-stu-id="da20f-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="da20f-107">Управление версиями конфигурации — скачивание и хранение различных версий конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="da20f-108">Массовые изменения конфигурации — внесение изменений в несколько частей конфигурации службы в локальном репозитории и интеграция изменений на сервер с помощью одной операции.</span><span class="sxs-lookup"><span data-stu-id="da20f-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="da20f-109">Знакомая цепочка инструментов и рабочий процесс Git — использование знакомых средств и рабочих процессов Git.</span><span class="sxs-lookup"><span data-stu-id="da20f-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="da20f-110">На схеме ниже приведен обзор различных способов настройки экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="da20f-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Настройка с помощью Git][api-management-git-configure]

<span data-ttu-id="da20f-112">При внесении изменений в службу с использованием портала издателя, а также командлетов PowerShell или REST API управление базой данных конфигурации службы осуществляется с помощью конечной точки `https://{name}.management.azure-api.net` , как показано в правой части схемы.</span><span class="sxs-lookup"><span data-stu-id="da20f-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="da20f-113">В левой части схемы демонстрируется вариант управления конфигурацией службы с помощью Git и репозитория Git для вашей службы, расположенного в `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="da20f-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="da20f-114">Ниже приведены действия с общими сведениями по управлению экземпляром службы управления API с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="da20f-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="da20f-115">Доступ к конфигурации Git в службе</span><span class="sxs-lookup"><span data-stu-id="da20f-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="da20f-116">Сохранение базы данных конфигурации службы в репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="da20f-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="da20f-117">Клонирование репозитория Git на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="da20f-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="da20f-118">Извлечение последнего репозитория на локальном компьютере, фиксация и отправка изменений обратно в репозиторий.</span><span class="sxs-lookup"><span data-stu-id="da20f-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="da20f-119">Развертывание изменений из репозитория в базу данных конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="da20f-120">В этой статье описывается включение и использование Git для управления конфигурацией и содержатся справочные сведения о файлах и папках в репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="da20f-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="da20f-121">Доступ к конфигурации Git в службе</span><span class="sxs-lookup"><span data-stu-id="da20f-121">Access Git configuration in your service</span></span>
<span data-ttu-id="da20f-122">Чтобы быстро просмотреть состояние конфигурации Git, взгляните на значок Git в правом верхнем углу портала издателя.</span><span class="sxs-lookup"><span data-stu-id="da20f-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="da20f-123">В этом примере сообщение о состоянии указывает, что в репозитории остались несохраненные изменения.</span><span class="sxs-lookup"><span data-stu-id="da20f-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="da20f-124">Это связано с тем, что база данных конфигурации службы управления API не была сохранена в репозитории.</span><span class="sxs-lookup"><span data-stu-id="da20f-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![Состояние Git][api-management-git-icon-enable]

<span data-ttu-id="da20f-126">Чтобы просмотреть и настроить параметры конфигурации Git, щелкните значок Git или в меню **Безопасность** откройте вкладку **Репозиторий конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="da20f-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![Включение доступа к GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="da20f-128">Все секреты, которые не определены как свойства, будут сохранены в репозитории и останутся в его журнале до отключения и повторного включения доступа к Git.</span><span class="sxs-lookup"><span data-stu-id="da20f-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="da20f-129">Свойства обеспечивают безопасное управление постоянными строковыми значениями, включая секреты, во всех конфигурациях API и политиках, поэтому их не нужно хранить непосредственно в правилах политики.</span><span class="sxs-lookup"><span data-stu-id="da20f-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="da20f-130">Дополнительные сведения см. в статье [Использование свойств в политиках управления API Azure](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="da20f-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="da20f-131">См. дополнительные сведения о [включении и отключении доступа к Git с помощью REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="da20f-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="da20f-132">Сохранение конфигураций службы в репозитории Git</span><span class="sxs-lookup"><span data-stu-id="da20f-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="da20f-133">Первым действием перед клонированием репозитория является сохранение текущего состояния конфигурации службы в репозитории.</span><span class="sxs-lookup"><span data-stu-id="da20f-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="da20f-134">Щелкните **Сохранить конфигурацию в репозитории**.</span><span class="sxs-lookup"><span data-stu-id="da20f-134">Click **Save configuration to repository**.</span></span>

![Сохранение конфигурации][api-management-save-configuration]

<span data-ttu-id="da20f-136">Внесите необходимые изменения на экране подтверждения и нажмите кнопку **ОК** для их сохранения.</span><span class="sxs-lookup"><span data-stu-id="da20f-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![Сохранение конфигурации][api-management-save-configuration-confirm]

<span data-ttu-id="da20f-138">Через некоторое время конфигурация будет сохранена и отобразится состояние конфигурации репозитория, включая дату и время последнего изменения конфигурации и последней синхронизации конфигурации службы и репозитория.</span><span class="sxs-lookup"><span data-stu-id="da20f-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![Состояние конфигурации][api-management-configuration-status]

<span data-ttu-id="da20f-140">Сохраненную в репозитории конфигурацию можно клонировать.</span><span class="sxs-lookup"><span data-stu-id="da20f-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="da20f-141">Дополнительные сведения о выполнении этой операции с помощью REST API см. в статье о [фиксации конфигурации с помощью REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="da20f-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="da20f-142">Клонирование репозитория на локальный компьютер</span><span class="sxs-lookup"><span data-stu-id="da20f-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="da20f-143">Чтобы клонировать репозиторий, требуется URL-адрес репозитория, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="da20f-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="da20f-144">Имя пользователя и URL-адрес отображаются в верхней части вкладки **Репозиторий конфигурации** .</span><span class="sxs-lookup"><span data-stu-id="da20f-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![Клонирование репозитория Git][api-management-configuration-git-clone]

<span data-ttu-id="da20f-146">Пароль создается в нижней части вкладки **Репозиторий конфигурации** .</span><span class="sxs-lookup"><span data-stu-id="da20f-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![Создание пароля][api-management-generate-password]

<span data-ttu-id="da20f-148">Чтобы создать пароль, сначала убедитесь, что в строке **Срок действия** указаны нужные значения даты и времени срока действия, а затем нажмите кнопку **Создать маркер**.</span><span class="sxs-lookup"><span data-stu-id="da20f-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![Пароль][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="da20f-150">Запомните этот пароль.</span><span class="sxs-lookup"><span data-stu-id="da20f-150">Make a note of this password.</span></span> <span data-ttu-id="da20f-151">После закрытия этой страницы пароль больше не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="da20f-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="da20f-152">В следующих примерах применяется средство Git Bash из [Git для Windows](http://www.git-scm.com/downloads) , но можно использовать любое знакомое вам средство Git.</span><span class="sxs-lookup"><span data-stu-id="da20f-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="da20f-153">Откройте средство Git в нужной папке и выполните указанную ниже команду для клонирования репозитория git на локальный компьютер с помощью команды, предоставленной на портале издателя.</span><span class="sxs-lookup"><span data-stu-id="da20f-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="da20f-154">При появлении запроса введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="da20f-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="da20f-155">При появлении ошибок попробуйте изменить команду `git clone` так, чтобы она включала в себя имя пользователя и пароль, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="da20f-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="da20f-156">Если ошибка возникнет и в этом случае, попробуйте использовать кодирование URL части пароля, содержащегося в команде.</span><span class="sxs-lookup"><span data-stu-id="da20f-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="da20f-157">Чтобы быстро решить эту задачу, откройте Visual Studio и выполните следующую команду в **окне интерпретации**.</span><span class="sxs-lookup"><span data-stu-id="da20f-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="da20f-158">Чтобы открыть **окно интерпретации**, откройте любое решение или проект в Visual Studio (или создайте пустое консольное приложение), а затем выберите **Окна** и **Интерпретация** в меню **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="da20f-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="da20f-159">Зашифрованный пароль вместе с именем пользователя и расположением репозитория можно использовать для создания команды git.</span><span class="sxs-lookup"><span data-stu-id="da20f-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="da20f-160">После клонирования репозиторий доступен для просмотра и работы в локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="da20f-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="da20f-161">Дополнительные сведения см. в разделе [Справочные сведения по структуре файлов и папок локального репозитория Git](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="da20f-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="da20f-162">Обновление локального репозитория самой последней конфигурацией экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="da20f-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="da20f-163">Перед обновлением локального репозитория с помощью последних изменений необходимо сохранить изменения, вносимые в экземпляр службы управления API, на портале издателя или с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="da20f-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="da20f-164">Для этого нажмите кнопку **Сохранить конфигурацию в репозиторий** на вкладке **Репозиторий конфигурации** на портале издателя, а затем выполните следующую команду в локальном репозитории.</span><span class="sxs-lookup"><span data-stu-id="da20f-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="da20f-165">Перед выполнением `git pull` убедитесь, что выбрана папка локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="da20f-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="da20f-166">Если вы только что завершили команду `git clone` , необходимо изменить каталог на репозиторий, выполнив команду, аналогичную приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="da20f-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="da20f-167">Отправка изменений из локального репозитория в репозиторий сервера</span><span class="sxs-lookup"><span data-stu-id="da20f-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="da20f-168">Чтобы отправить изменения из локального репозитория в репозиторий сервера, необходимо зафиксировать изменения и после этого отправить их в репозиторий сервера.</span><span class="sxs-lookup"><span data-stu-id="da20f-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="da20f-169">Чтобы зафиксировать изменения, откройте командное средство Git, перейдите в каталог локального репозитория и выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="da20f-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="da20f-170">Для отправки всех фиксаций на сервер выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="da20f-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="da20f-171">Развертывание изменений конфигурации службы в экземпляре службы управления API</span><span class="sxs-lookup"><span data-stu-id="da20f-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="da20f-172">После фиксации и отправки локальных изменений в репозиторий сервера их можно развернуть в экземпляре службы управления API.</span><span class="sxs-lookup"><span data-stu-id="da20f-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![Развернуть][api-management-configuration-deploy]

<span data-ttu-id="da20f-174">Дополнительные сведения о выполнении этой операции с помощью REST API см. в статье о [развертывании изменений Git в базе данных конфигурации с помощью REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="da20f-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="da20f-175">Справочные сведения по структуре файлов и папок локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="da20f-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="da20f-176">В файлах и папках в локальном репозитории Git содержатся сведения о конфигурации для экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="da20f-177">Элемент</span><span class="sxs-lookup"><span data-stu-id="da20f-177">Item</span></span> | <span data-ttu-id="da20f-178">Описание</span><span class="sxs-lookup"><span data-stu-id="da20f-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da20f-179">Корневая папка api-management</span><span class="sxs-lookup"><span data-stu-id="da20f-179">root api-management folder</span></span> |<span data-ttu-id="da20f-180">Содержит конфигурацию верхнего уровня для экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="da20f-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="da20f-181">Папка apis</span><span class="sxs-lookup"><span data-stu-id="da20f-181">apis folder</span></span> |<span data-ttu-id="da20f-182">Содержит конфигурацию для API в экземпляре службы</span><span class="sxs-lookup"><span data-stu-id="da20f-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="da20f-183">Папка groups</span><span class="sxs-lookup"><span data-stu-id="da20f-183">groups folder</span></span> |<span data-ttu-id="da20f-184">Содержит конфигурацию для групп в экземпляре службы</span><span class="sxs-lookup"><span data-stu-id="da20f-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="da20f-185">Папка policies</span><span class="sxs-lookup"><span data-stu-id="da20f-185">policies folder</span></span> |<span data-ttu-id="da20f-186">Содержит политики в экземпляре службы</span><span class="sxs-lookup"><span data-stu-id="da20f-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="da20f-187">Папка portalStyles</span><span class="sxs-lookup"><span data-stu-id="da20f-187">portalStyles folder</span></span> |<span data-ttu-id="da20f-188">Содержит конфигурацию для настроек портала разработчика в экземпляре службы</span><span class="sxs-lookup"><span data-stu-id="da20f-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="da20f-189">Папка products</span><span class="sxs-lookup"><span data-stu-id="da20f-189">products folder</span></span> |<span data-ttu-id="da20f-190">Содержит конфигурацию для продуктов в экземпляре службы</span><span class="sxs-lookup"><span data-stu-id="da20f-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="da20f-191">Папка templates</span><span class="sxs-lookup"><span data-stu-id="da20f-191">templates folder</span></span> |<span data-ttu-id="da20f-192">Содержит конфигурацию для шаблонов электронной почты в экземпляре службы</span><span class="sxs-lookup"><span data-stu-id="da20f-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="da20f-193">В каждой папке может находиться один или несколько файлов и в некоторых случаях одна или несколько папок, например папка для каждого API, продукта или группы.</span><span class="sxs-lookup"><span data-stu-id="da20f-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="da20f-194">Файлы в каждой папке специфичны для типа сущности, описанного в имени папки.</span><span class="sxs-lookup"><span data-stu-id="da20f-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="da20f-195">Тип файла</span><span class="sxs-lookup"><span data-stu-id="da20f-195">File type</span></span> | <span data-ttu-id="da20f-196">Назначение</span><span class="sxs-lookup"><span data-stu-id="da20f-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="da20f-197">json</span><span class="sxs-lookup"><span data-stu-id="da20f-197">json</span></span> |<span data-ttu-id="da20f-198">Сведения о конфигурации соответствующей сущности</span><span class="sxs-lookup"><span data-stu-id="da20f-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="da20f-199">html</span><span class="sxs-lookup"><span data-stu-id="da20f-199">html</span></span> |<span data-ttu-id="da20f-200">Описания сущности, часто отображаемые на портале разработчика</span><span class="sxs-lookup"><span data-stu-id="da20f-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="da20f-201">xml</span><span class="sxs-lookup"><span data-stu-id="da20f-201">xml</span></span> |<span data-ttu-id="da20f-202">Правила политики</span><span class="sxs-lookup"><span data-stu-id="da20f-202">Policy statements</span></span> |
| <span data-ttu-id="da20f-203">css</span><span class="sxs-lookup"><span data-stu-id="da20f-203">css</span></span> |<span data-ttu-id="da20f-204">Таблицы стилей для настройки портала разработчика</span><span class="sxs-lookup"><span data-stu-id="da20f-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="da20f-205">Эти файлы можно создавать, удалять, изменять и контролировать в локальной файловой системе. А изменения можно снова развернуть в экземпляре службы управления API.</span><span class="sxs-lookup"><span data-stu-id="da20f-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="da20f-206">Указанные далее сущности отсутствуют в репозитории Git и не могут быть настроены с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="da20f-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="da20f-207">Пользователи</span><span class="sxs-lookup"><span data-stu-id="da20f-207">Users</span></span>
> * <span data-ttu-id="da20f-208">Подписки</span><span class="sxs-lookup"><span data-stu-id="da20f-208">Subscriptions</span></span>
> * <span data-ttu-id="da20f-209">Свойства</span><span class="sxs-lookup"><span data-stu-id="da20f-209">Properties</span></span>
> * <span data-ttu-id="da20f-210">Сущности портала разработчика, отличные от стилей</span><span class="sxs-lookup"><span data-stu-id="da20f-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="da20f-211">Корневая папка api-management</span><span class="sxs-lookup"><span data-stu-id="da20f-211">Root api-management folder</span></span>
<span data-ttu-id="da20f-212">Корневая папка `api-management` содержит файл `configuration.json` со сведениями верхнего уровня об экземпляре службы в следующем формате.</span><span class="sxs-lookup"><span data-stu-id="da20f-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

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

<span data-ttu-id="da20f-213">Первые четыре параметра (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled` и `UserRegistrationTermsConsentRequired`) соответствуют указанным далее параметрам на вкладке **Удостоверения** в разделе **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="da20f-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="da20f-214">Параметр удостоверения</span><span class="sxs-lookup"><span data-stu-id="da20f-214">Identity setting</span></span> | <span data-ttu-id="da20f-215">Соответствует параметру</span><span class="sxs-lookup"><span data-stu-id="da20f-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="da20f-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="da20f-216">RegistrationEnabled</span></span> |<span data-ttu-id="da20f-217">**Перенаправлять анонимных пользователей на страницу входа** </span><span class="sxs-lookup"><span data-stu-id="da20f-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="da20f-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="da20f-218">UserRegistrationTerms</span></span> |<span data-ttu-id="da20f-219">**Условия использования при регистрации пользователя** </span><span class="sxs-lookup"><span data-stu-id="da20f-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="da20f-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="da20f-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="da20f-221">**Показывать условия использования на странице регистрации** </span><span class="sxs-lookup"><span data-stu-id="da20f-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="da20f-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="da20f-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="da20f-223">**Требовать согласия** </span><span class="sxs-lookup"><span data-stu-id="da20f-223">**Require consent** checkbox</span></span> |

![Параметры удостоверений][api-management-identity-settings]

<span data-ttu-id="da20f-225">Следующие четыре параметра (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled` и `DelegationValidationKey`) соответствуют указанным далее параметрам на вкладке **Делегирование** в разделе **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="da20f-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="da20f-226">Параметр делегирования</span><span class="sxs-lookup"><span data-stu-id="da20f-226">Delegation setting</span></span> | <span data-ttu-id="da20f-227">Соответствует параметру</span><span class="sxs-lookup"><span data-stu-id="da20f-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="da20f-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="da20f-228">DelegationEnabled</span></span> |<span data-ttu-id="da20f-229">Флажок **Делегировать вход и регистрацию**</span><span class="sxs-lookup"><span data-stu-id="da20f-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="da20f-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="da20f-230">DelegationUrl</span></span> |<span data-ttu-id="da20f-231">**URL-адрес конечной точки делегирования** </span><span class="sxs-lookup"><span data-stu-id="da20f-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="da20f-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="da20f-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="da20f-233">**Делегировать подписку на продукт** </span><span class="sxs-lookup"><span data-stu-id="da20f-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="da20f-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="da20f-234">DelegationValidationKey</span></span> |<span data-ttu-id="da20f-235">**Делегировать ключ проверки** </span><span class="sxs-lookup"><span data-stu-id="da20f-235">**Delegate Validation Key** textbox</span></span> |

![Параметры делегирования][api-management-delegation-settings]

<span data-ttu-id="da20f-237">Последний параметр `$ref-policy`соответствует глобальному файлу правил политики для экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="da20f-238">Папка apis</span><span class="sxs-lookup"><span data-stu-id="da20f-238">apis folder</span></span>
<span data-ttu-id="da20f-239">Папка `apis` содержит папку для каждого API в экземпляре службы, в котором находятся указанные далее элементы.</span><span class="sxs-lookup"><span data-stu-id="da20f-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="da20f-240">`apis\<api name>\configuration.json` — это конфигурация для API, которая содержит сведения о серверном URL-адресе службы и операциях.</span><span class="sxs-lookup"><span data-stu-id="da20f-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="da20f-241">Это те же сведения, которые возвращаются при вызове операции [Получить определенный API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) с `export=true` в формате `application/json`.</span><span class="sxs-lookup"><span data-stu-id="da20f-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="da20f-242">`apis\<api name>\api.description.html` — это описание API, которое соответствует свойству `description` [сущности API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="da20f-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="da20f-243">`apis\<api name>\operations\` — эта папка содержит файлы `<operation name>.description.html`, соответствующие операциям в API.</span><span class="sxs-lookup"><span data-stu-id="da20f-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="da20f-244">Каждый файл содержит описание одной операции в API, которая соответствует свойству `description`[сущности operation](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) в REST API.</span><span class="sxs-lookup"><span data-stu-id="da20f-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="da20f-245">Папка groups</span><span class="sxs-lookup"><span data-stu-id="da20f-245">groups folder</span></span>
<span data-ttu-id="da20f-246">Папка `groups` содержит папку для каждой группы, определенной в экземпляре службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="da20f-247">`groups\<group name>\configuration.json` — это конфигурация для группы.</span><span class="sxs-lookup"><span data-stu-id="da20f-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="da20f-248">Это те же сведения, которые возвращаются при вызове операции [Получить определенную группу](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) .</span><span class="sxs-lookup"><span data-stu-id="da20f-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="da20f-249">`groups\<group name>\description.html` — это описание группы, которое соответствует свойству `description` [сущности group](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="da20f-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="da20f-250">Папка policies</span><span class="sxs-lookup"><span data-stu-id="da20f-250">policies folder</span></span>
<span data-ttu-id="da20f-251">Папка `policies` содержит правила политики для экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="da20f-252">`policies\global.xml` содержит политики, определенные в глобальной области для экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="da20f-253">`policies\apis\<api name>\` — если в области API определены какие-либо политики, они содержатся в этой папке.</span><span class="sxs-lookup"><span data-stu-id="da20f-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="da20f-254">Папка `policies\apis\<api name>\<operation name>\` — если в области операции определены какие-либо политики, они содержатся в этой папке в файлах `<operation name>.xml`, соответствующих правилам политики для каждой операции.</span><span class="sxs-lookup"><span data-stu-id="da20f-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="da20f-255">`policies\products\` — если в области продукта определены какие-либо политики, они содержатся в этой папке в файлах `<product name>.xml`, соответствующих правилам политики для каждого продукта.</span><span class="sxs-lookup"><span data-stu-id="da20f-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="da20f-256">Папка portalStyles</span><span class="sxs-lookup"><span data-stu-id="da20f-256">portalStyles folder</span></span>
<span data-ttu-id="da20f-257">Папка `portalStyles` содержит конфигурацию и таблицы стилей для настроек портала разработчика для экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="da20f-258">`portalStyles\configuration.json` — содержит имена таблиц стилей, используемых на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="da20f-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="da20f-259">`portalStyles\<style name>.css` — каждый файл `<style name>.css` содержит стили для портала разработчика (`Preview.css` и `Production.css` по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="da20f-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="da20f-260">Папка products</span><span class="sxs-lookup"><span data-stu-id="da20f-260">products folder</span></span>
<span data-ttu-id="da20f-261">Папка `products` содержит папку для каждого продукта, определенного в экземпляре службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="da20f-262">`products\<product name>\configuration.json` — это конфигурация для продукта.</span><span class="sxs-lookup"><span data-stu-id="da20f-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="da20f-263">Это те же сведения, которые возвращаются при вызове операции [Получить определенный продукт](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) .</span><span class="sxs-lookup"><span data-stu-id="da20f-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="da20f-264">`products\<product name>\product.description.html` — это описание продукта, которое соответствует свойству `description` [сущности product](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) в REST API.</span><span class="sxs-lookup"><span data-stu-id="da20f-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="da20f-265">шаблоны</span><span class="sxs-lookup"><span data-stu-id="da20f-265">templates</span></span>
<span data-ttu-id="da20f-266">Папка `templates` содержит конфигурацию для [шаблонов электронной почты](api-management-howto-configure-notifications.md) экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="da20f-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="da20f-267">`<template name>\configuration.json` — это конфигурация для шаблона электронной почты.</span><span class="sxs-lookup"><span data-stu-id="da20f-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="da20f-268">`<template name>\body.html` — это текст сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="da20f-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da20f-269">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="da20f-269">Next steps</span></span>
<span data-ttu-id="da20f-270">Сведения о других способах управления экземпляром службы см. в приведенных ниже статьях. </span><span class="sxs-lookup"><span data-stu-id="da20f-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="da20f-271">Управление экземпляром службы с помощью следующих командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="da20f-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="da20f-272">Справочник по командлетам PowerShell для развертывания службы</span><span class="sxs-lookup"><span data-stu-id="da20f-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="da20f-273">Справочник по командлетам PowerShell для управления службами</span><span class="sxs-lookup"><span data-stu-id="da20f-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="da20f-274">Управление экземпляром службы на портале издателя</span><span class="sxs-lookup"><span data-stu-id="da20f-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="da20f-275">Управление вашим первым API</span><span class="sxs-lookup"><span data-stu-id="da20f-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="da20f-276">Управление экземпляром службы с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="da20f-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="da20f-277">Справочник по REST API для управления API</span><span class="sxs-lookup"><span data-stu-id="da20f-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="da20f-278">Просмотр видеообзора</span><span class="sxs-lookup"><span data-stu-id="da20f-278">Watch a video overview</span></span>
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




