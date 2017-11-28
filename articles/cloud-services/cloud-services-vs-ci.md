---
title: "Непрерывная отправка для облачных служб с помощью Visual Studio Online | Документация Майкрософт"
description: "Настройка непрерывной доставки для облачных приложений Azure без сохранения ключа к хранилищу данных диагностики в файлах конфигурации службы"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="64682-103">Безопасное сохранение ключа к хранилищу данных диагностики облачных служб и настройка непрерывной интеграции и развертывания в Azure с помощью Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="64682-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="64682-104">В настоящее время этот подход часто используется в проектах с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="64682-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="64682-105">Сохранять секреты приложения в файлах конфигурации теперь опасно, так как утечка секретов из общедоступной системы управления версиями ставит под угрозу безопасность.</span><span class="sxs-lookup"><span data-stu-id="64682-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="64682-106">Сохранять секрет виде открытого текста в файле конвейера непрерывной интеграции тоже рискованно, так как серверы сборки могут быть общими ресурсами в облачной среде.</span><span class="sxs-lookup"><span data-stu-id="64682-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="64682-107">В этой статье объясняется, как с помощью Visual Studio и Visual Studio Online устранить угрозы безопасности во время разработки и непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="64682-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="64682-108">Удаление секрета ключа к хранилищу данных диагностики из файла конфигурации проекта</span><span class="sxs-lookup"><span data-stu-id="64682-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="64682-109">Расширению диагностики облачных служб необходимо хранилище Azure, чтобы сохранять результаты диагностики.</span><span class="sxs-lookup"><span data-stu-id="64682-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="64682-110">Раньше строка подключения к хранилищу указывалась в файлах конфигурации (CSCFG) облачных служб, и ее можно было увидеть в системе управления версиями.</span><span class="sxs-lookup"><span data-stu-id="64682-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="64682-111">В последнем выпуске пакета SDK для Azure сохраняется только частичная строка подключения с маркером вместо ключа.</span><span class="sxs-lookup"><span data-stu-id="64682-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="64682-112">Следующие инструкции объясняют, как работают новые средства облачных служб.</span><span class="sxs-lookup"><span data-stu-id="64682-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="64682-113">1. Открытие конструктора ролей</span><span class="sxs-lookup"><span data-stu-id="64682-113">1. Open the Role designer</span></span>
* <span data-ttu-id="64682-114">Чтобы открыть конструктор ролей, дважды щелкните или щелкните правой кнопкой мыши роль облачных служб.</span><span class="sxs-lookup"><span data-stu-id="64682-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![Открытие конструктора ролей][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="64682-116">2. В разделе "Диагностика" добавлен новый флажок "Не удалять секрет ключа хранилища из файла конфигурации проекта (CSCFG-файла)"</span><span class="sxs-lookup"><span data-stu-id="64682-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="64682-117">Если вы используете эмулятор локального хранилища, этот флажок недоступен, так как для строки локального подключения UseDevelopmentStorage = true отсутствует секрет, которым можно управлять.</span><span class="sxs-lookup"><span data-stu-id="64682-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![Строка подключения к эмулятору локального хранилища не является секретом][1]

* <span data-ttu-id="64682-119">Если вы создаете новый проект, по умолчанию этот флажок снят.</span><span class="sxs-lookup"><span data-stu-id="64682-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="64682-120">В результате раздел ключа к хранилищу данных в выбранной строке подключения заменяется маркером.</span><span class="sxs-lookup"><span data-stu-id="64682-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="64682-121">Значение маркера находится в папке AppData\Roaming текущего пользователя (например, C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService).</span><span class="sxs-lookup"><span data-stu-id="64682-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="64682-122">Обратите внимание, что доступ к папке user\AppData контролируется с помощью входа пользователя и она считается надежным местом для хранения конфиденциальных данных разработки.</span><span class="sxs-lookup"><span data-stu-id="64682-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![Ключ к хранилищу данных сохранен в папке профиля пользователя][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="64682-124">3. Выбор учетной записи хранения для диагностики</span><span class="sxs-lookup"><span data-stu-id="64682-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="64682-125">Нажмите кнопку "…" и в открывшемся диалоговом окне выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="64682-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="64682-126">.</span><span class="sxs-lookup"><span data-stu-id="64682-126">button.</span></span> <span data-ttu-id="64682-127">Обратите внимание, что создаваемая строка подключения к хранилищу не будет содержать ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="64682-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="64682-128">Например, DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="64682-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="64682-129">4.    Отладка проекта</span><span class="sxs-lookup"><span data-stu-id="64682-129">4.    Debugging the project</span></span>
* <span data-ttu-id="64682-130">Нажмите клавишу F5, чтобы запустить отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="64682-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="64682-131">Все должно работать, как раньше.</span><span class="sxs-lookup"><span data-stu-id="64682-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="64682-132">![Локальный запуск отладки][3]</span><span class="sxs-lookup"><span data-stu-id="64682-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="64682-133">5. Публикация проекта из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64682-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="64682-134">Откройте диалоговое окно публикации и следуйте инструкциям, чтобы войти и опубликовать приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="64682-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="64682-135">6. Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="64682-135">6. Additional information</span></span>
> <span data-ttu-id="64682-136">Примечание. На панели параметров конструктор ролей пока что будет оставаться без изменений.</span><span class="sxs-lookup"><span data-stu-id="64682-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="64682-137">Если вы хотите использовать функцию управления секретом для диагностики, перейдите на вкладку конфигурации.</span><span class="sxs-lookup"><span data-stu-id="64682-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![Добавление параметров][4]

> <span data-ttu-id="64682-139">Примечание. Если ключ Application Insights включен, он будет храниться как обычный текст.</span><span class="sxs-lookup"><span data-stu-id="64682-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="64682-140">Этот ключ используется только для передачи содержимого, поэтому риск раскрытия конфиденциальных данных отсутствует.</span><span class="sxs-lookup"><span data-stu-id="64682-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="64682-141">Создание и публикация проекта облачных служб с помощью шаблонов задач Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="64682-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="64682-142">Ниже показано, как настроить непрерывную интеграцию для проекта облачных служб с помощью задач Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="64682-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="64682-143">1.    Получение учетной записи VSO</span><span class="sxs-lookup"><span data-stu-id="64682-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="64682-144">[Создайте учетную запись Visual Studio Online] [ Create Visual Studio Online account] Если вы их еще нет</span><span class="sxs-lookup"><span data-stu-id="64682-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="64682-145">[Создание командного проекта] [ Create team project] своей учетной записи Visual Studio online</span><span class="sxs-lookup"><span data-stu-id="64682-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="64682-146">2.    Настройка системы управления версиями в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64682-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="64682-147">Подключитесь к командному проекту.</span><span class="sxs-lookup"><span data-stu-id="64682-147">Connect to a team project</span></span>

![Подключение к командному проекту][5]

![Выбор командного проекта для подключения][6]

* <span data-ttu-id="64682-150">Добавьте проект в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="64682-150">Add your project to source control</span></span>

![Добавление проекта в систему управления версиями][7]

![Сопоставление проекта с папкой системы управления версиями][8]

* <span data-ttu-id="64682-153">Запишите проект после изменения из Team Explorer.</span><span class="sxs-lookup"><span data-stu-id="64682-153">Check in your project from Team Explorer</span></span>

![Запись проекта после изменения в систему управления версиями][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="64682-155">3.    Настройка процесса сборки</span><span class="sxs-lookup"><span data-stu-id="64682-155">3.    Configure Build process</span></span>
* <span data-ttu-id="64682-156">Откройте командный проект и добавьте новые шаблоны процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="64682-156">Browse to your team project and add a new build process Templates</span></span>

![Добавление новой сборки][10]

* <span data-ttu-id="64682-158">Выберите задачу сборки.</span><span class="sxs-lookup"><span data-stu-id="64682-158">Select build task</span></span>

![Добавление задачи сборки][11]

![Выбор шаблона задачи сборки в Visual Studio][12]

* <span data-ttu-id="64682-161">Измените входные данные задачи сборки.</span><span class="sxs-lookup"><span data-stu-id="64682-161">Edit build task input.</span></span> <span data-ttu-id="64682-162">Настройте параметры сборки по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="64682-162">Please customize the build parameters according to your need</span></span>

![Настройка задачи сборки][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="64682-164">Настройте переменные сборки.</span><span class="sxs-lookup"><span data-stu-id="64682-164">Configure build variables</span></span>

![Настройка переменных сборки.][14]

* <span data-ttu-id="64682-166">Добавьте задачу отправки в заданное место сборки.</span><span class="sxs-lookup"><span data-stu-id="64682-166">Add a task to upload build drop</span></span>

![Выбор задачи публикации в заданном месте сборки][15]

![Настройка задачи публикации в заданном месте сборки][16]

* <span data-ttu-id="64682-169">Запустите сборку.</span><span class="sxs-lookup"><span data-stu-id="64682-169">Run the build</span></span>

![Постановка новой сборки в очередь][17]

![Просмотр сводки сборки][18]

* <span data-ttu-id="64682-172">Если сборка выполнена успешно, вы увидите примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="64682-172">if the build is successful you will see a result similar to below</span></span>

![Результат сборки][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="64682-174">4.    Процесса настройки выпуска</span><span class="sxs-lookup"><span data-stu-id="64682-174">4.    Configure Release process</span></span>
* <span data-ttu-id="64682-175">Создайте новый выпуск.</span><span class="sxs-lookup"><span data-stu-id="64682-175">Create a new release</span></span>

![Создание нового выпуска][20]

* <span data-ttu-id="64682-177">Выберите задачу развертывания облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="64682-177">Select the Azure Cloud Services Deployment task</span></span>

![Выбор задачи развертывания облачных служб Azure][21]

* <span data-ttu-id="64682-179">Так как ключ учетной записи хранения не записан после изменения в систему управления версиями, необходимо указать секретный ключ для настройки расширений диагностики.</span><span class="sxs-lookup"><span data-stu-id="64682-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="64682-180">Разверните раздел **Дополнительные параметры для создания новой службы** и измените входные данные параметра **Diagnostics Storage Account Keys** (Ключи учетной записи хранения диагностических данных).</span><span class="sxs-lookup"><span data-stu-id="64682-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="64682-181">Эти выходные данные включают несколько строк пары "ключ — значение" в формате **[имя_роли]:$(ключ_учетной_записи_хранения)**.</span><span class="sxs-lookup"><span data-stu-id="64682-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="64682-182">Примечание. Если ваша учетная запись хранения диагностических данных находится в подписке, в которой будет опубликовано приложение облачных служб, не нужно указывать ключ во входных данных задачи развертывания. Развертывание программно получит информацию о хранилище из подписки.</span><span class="sxs-lookup"><span data-stu-id="64682-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![Настройка задачи развертывания облачных служб][22]

* <span data-ttu-id="64682-184">Используйте секретные переменные сборки, чтобы сохранить ключи к хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="64682-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="64682-185">Чтобы маскировать переменную как секрет, щелкните значок блокировки справа от входных данных переменных.</span><span class="sxs-lookup"><span data-stu-id="64682-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![Сохранение ключей к хранилищу данных в секретных переменных сборки][23]

* <span data-ttu-id="64682-187">Создайте выпуск и разверните проект в Azure</span><span class="sxs-lookup"><span data-stu-id="64682-187">Create a release and deploy your project to Azure</span></span>

![Создание нового выпуска][24]

## <a name="next-steps"></a><span data-ttu-id="64682-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64682-189">Next steps</span></span>
<span data-ttu-id="64682-190">Дополнительные сведения о настройке расширений диагностики для облачных служб Azure см. в разделе [включение диагностики в облачных службах Azure с помощью PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="64682-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
