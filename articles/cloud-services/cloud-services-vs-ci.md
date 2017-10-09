---
title: "aaaContinuous доставка для облачных служб с помощью Visual Studio Online | Документы Microsoft"
description: "Узнайте, как tooset копирование непрерывная доставка для Azure облачные приложения без сохранения файлов конфигурации службы хранилища ключей toohello диагностики"
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
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a><span data-ttu-id="69d00-103">Securely сохранить службы диагностики ключ облачного хранилища и tooAzure Настройка непрерывной интеграции и развертывания с помощью Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="69d00-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment tooAzure using Visual Studio Online</span></span>
 <span data-ttu-id="69d00-104">Это общие исходные проекты tooopen рекомендаций в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="69d00-104">It is a common practice tooopen source projects nowadays.</span></span> <span data-ttu-id="69d00-105">Сохранять секреты приложения в файлах конфигурации теперь опасно, так как утечка секретов из общедоступной системы управления версиями ставит под угрозу безопасность.</span><span class="sxs-lookup"><span data-stu-id="69d00-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="69d00-106">Хранение секрет как открытый текст в файле в конвейере непрерывной интеграции не является безопасным либо с момента построения серверы могут быть общие ресурсы на hello облачной среде.</span><span class="sxs-lookup"><span data-stu-id="69d00-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on hello Cloud environment.</span></span> <span data-ttu-id="69d00-107">В этой статье объясняется, каким образом Visual Studio и Visual Studio Online взлому hello обеспечения безопасности во время разработки и процесс непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="69d00-107">This article explains how Visual Studio and Visual Studio Online mitigates hello security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="69d00-108">Удаление секрета ключа к хранилищу данных диагностики из файла конфигурации проекта</span><span class="sxs-lookup"><span data-stu-id="69d00-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="69d00-109">Расширению диагностики облачных служб необходимо хранилище Azure, чтобы сохранять результаты диагностики.</span><span class="sxs-lookup"><span data-stu-id="69d00-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="69d00-110">Ранее строки подключения к хранилищу hello задается в файлах конфигурации (cscfg) hello облачные службы и вернуть удалось toosource управления.</span><span class="sxs-lookup"><span data-stu-id="69d00-110">Formerly hello storage connection string is specified in hello Cloud Services configuration (.cscfg) files and could be checked in toosource control.</span></span> <span data-ttu-id="69d00-111">В последнем выпуске пакета Azure SDK hello мы изменили hello поведение tooonly хранилище строка частичного соединения с ключом hello замена маркером.</span><span class="sxs-lookup"><span data-stu-id="69d00-111">In hello latest Azure SDK release we changed hello behavior tooonly store a partial connection string with hello key replaced by a token.</span></span> <span data-ttu-id="69d00-112">Hello следующие шаги описывают, как работает hello новые инструменты облачные службы:</span><span class="sxs-lookup"><span data-stu-id="69d00-112">hello following steps describe how hello new Cloud Services tooling works:</span></span>

### <a name="1-open-hello-role-designer"></a><span data-ttu-id="69d00-113">1. Откройте конструктор ролей hello</span><span class="sxs-lookup"><span data-stu-id="69d00-113">1. Open hello Role designer</span></span>
* <span data-ttu-id="69d00-114">Дважды щелкните или щелкните правой кнопкой мыши в конструкторе ролей tooopen роли облачных служб</span><span class="sxs-lookup"><span data-stu-id="69d00-114">Double click or right click on a Cloud Services role tooopen Role designer</span></span>

![Открытие конструктора ролей][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="69d00-116">2. В разделе "Диагностика" добавлен новый флажок "Не удалять секрет ключа хранилища из файла конфигурации проекта (CSCFG-файла)"</span><span class="sxs-lookup"><span data-stu-id="69d00-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="69d00-117">При использовании эмулятора локального хранилища hello, этот флажок недоступен, так как нет секретный toomanage для строки локального подключения hello, который является UseDevelopmentStorage = true.</span><span class="sxs-lookup"><span data-stu-id="69d00-117">If you are using hello local storage emulator, this checkbox is disabled because there is no secret toomanage for hello local connection string, which is UseDevelopmentStorage=true.</span></span>

![Строка подключения к эмулятору локального хранилища не является секретом][1]

* <span data-ttu-id="69d00-119">Если вы создаете новый проект, по умолчанию этот флажок снят.</span><span class="sxs-lookup"><span data-stu-id="69d00-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="69d00-120">Это приводит к hello хранения основной раздел hello выбранные строки подключения к хранилищу заменяемого с маркером.</span><span class="sxs-lookup"><span data-stu-id="69d00-120">This results in hello storage key section of hello selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="69d00-121">Hello значение токена hello располагается в папке текущего пользователя hello AppData перемещаемых, например: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="69d00-121">hello value of hello token will be found under hello current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="69d00-122">Обратите внимание, эту папку user\AppData hello является контролировать доступ, вход пользователей и считается секреты разработки toostore надежном месте.</span><span class="sxs-lookup"><span data-stu-id="69d00-122">Note that hello user\AppData folder is Access Controlled by user sign-in and is considered a secure place toostore development secrets.</span></span>
> 
> 

![Ключ к хранилищу данных сохранен в папке профиля пользователя][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="69d00-124">3. Выбор учетной записи хранения для диагностики</span><span class="sxs-lookup"><span data-stu-id="69d00-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="69d00-125">Выберите учетную запись хранилища в диалоговом окне приветствия запускается через пункт меню «...» hello</span><span class="sxs-lookup"><span data-stu-id="69d00-125">Select a storage account from hello dialog launched by clicking hello “…”</span></span> <span data-ttu-id="69d00-126">.</span><span class="sxs-lookup"><span data-stu-id="69d00-126">button.</span></span> <span data-ttu-id="69d00-127">Обратите внимание на то, как создается строка подключения хранилища hello не будет иметь hello ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="69d00-127">Notice how hello storage connection string generated will not have hello storage account key.</span></span>
* <span data-ttu-id="69d00-128">Например, DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="69d00-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-hello-project"></a><span data-ttu-id="69d00-129">4.    Отладка проекта hello</span><span class="sxs-lookup"><span data-stu-id="69d00-129">4.    Debugging hello project</span></span>
* <span data-ttu-id="69d00-130">F5 toostart отладки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="69d00-130">F5 toostart debugging in Visual Studio.</span></span> <span data-ttu-id="69d00-131">Все, что должно работать в hello таким же образом как раньше.</span><span class="sxs-lookup"><span data-stu-id="69d00-131">Everything should work in hello same way as before.</span></span>
  <span data-ttu-id="69d00-132">![Локальный запуск отладки][3]</span><span class="sxs-lookup"><span data-stu-id="69d00-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="69d00-133">5. Публикация проекта из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="69d00-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="69d00-134">Запуск hello диалоговое окно публикации и продолжите tooAzure applicaion hello toopublish входа в инструкции.</span><span class="sxs-lookup"><span data-stu-id="69d00-134">Launch hello publish dialog and proceed with sign-in instructions toopublish hello applicaion tooAzure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="69d00-135">6. Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="69d00-135">6. Additional information</span></span>
> <span data-ttu-id="69d00-136">Примечание: hello панель параметров в конструкторе ролей hello остается это сейчас.</span><span class="sxs-lookup"><span data-stu-id="69d00-136">Note: hello Settings panel in hello role designer will stay as it is for now.</span></span> <span data-ttu-id="69d00-137">Функция секретный управления hello toouse для диагностики, перейдите вкладку toohello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="69d00-137">If you want toouse hello secret management feature for diagnostics, go toohello Configurations tab.</span></span>
> 
> 

![Добавление параметров][4]

> <span data-ttu-id="69d00-139">Примечание: Если параметр включен, hello Application Insights будет храниться ключ как обычный текст.</span><span class="sxs-lookup"><span data-stu-id="69d00-139">Note: If enabled, hello Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="69d00-140">Hello ключ используется только для передачи содержимого, конфиденциальные данные не будут риск раскрытия.</span><span class="sxs-lookup"><span data-stu-id="69d00-140">hello key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="69d00-141">Создание и публикация проекта облачных служб с помощью шаблонов задач Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="69d00-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="69d00-142">иллюстрирует следующие шаги Hello как проект с помощью Visual Studio online задач toosetup непрерывной интеграции для облачных служб:</span><span class="sxs-lookup"><span data-stu-id="69d00-142">hello following steps illustrates how toosetup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="69d00-143">1.    Получение учетной записи VSO</span><span class="sxs-lookup"><span data-stu-id="69d00-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="69d00-144">[Создайте учетную запись Visual Studio Online] [ Create Visual Studio Online account] Если вы их еще нет</span><span class="sxs-lookup"><span data-stu-id="69d00-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="69d00-145">[Создание командного проекта] [ Create team project] своей учетной записи Visual Studio online</span><span class="sxs-lookup"><span data-stu-id="69d00-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="69d00-146">2.    Настройка системы управления версиями в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="69d00-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="69d00-147">Подключение tooa командного проекта</span><span class="sxs-lookup"><span data-stu-id="69d00-147">Connect tooa team project</span></span>

![Подключить проект tooteam][5]

![Выберите tooconnect командного проекта для][6]

* <span data-ttu-id="69d00-150">Добавить элемент управления toosource проекта</span><span class="sxs-lookup"><span data-stu-id="69d00-150">Add your project toosource control</span></span>

![Добавление элемента управления toosource проекта][7]

![Сопоставление папки системы управления версиями tooa проекта][8]

* <span data-ttu-id="69d00-153">Запишите проект после изменения из Team Explorer.</span><span class="sxs-lookup"><span data-stu-id="69d00-153">Check in your project from Team Explorer</span></span>

![Возврат управления toosource проекта][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="69d00-155">3.    Настройка процесса сборки</span><span class="sxs-lookup"><span data-stu-id="69d00-155">3.    Configure Build process</span></span>
* <span data-ttu-id="69d00-156">Обзор tooyour командного проекта и добавьте новый процесс построения шаблонов</span><span class="sxs-lookup"><span data-stu-id="69d00-156">Browse tooyour team project and add a new build process Templates</span></span>

![Добавление новой сборки][10]

* <span data-ttu-id="69d00-158">Выберите задачу сборки.</span><span class="sxs-lookup"><span data-stu-id="69d00-158">Select build task</span></span>

![Добавление задачи сборки][11]

![Выбор шаблона задачи сборки в Visual Studio][12]

* <span data-ttu-id="69d00-161">Измените входные данные задачи сборки.</span><span class="sxs-lookup"><span data-stu-id="69d00-161">Edit build task input.</span></span> <span data-ttu-id="69d00-162">Настраивайте hello сборки, необходимые параметры в соответствии с tooyour</span><span class="sxs-lookup"><span data-stu-id="69d00-162">Please customize hello build parameters according tooyour need</span></span>

![Настройка задачи сборки][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="69d00-164">Настройте переменные сборки.</span><span class="sxs-lookup"><span data-stu-id="69d00-164">Configure build variables</span></span>

![Настройка переменных сборки.][14]

* <span data-ttu-id="69d00-166">Добавление каталога построения tooupload задач</span><span class="sxs-lookup"><span data-stu-id="69d00-166">Add a task tooupload build drop</span></span>

![Выбор задачи публикации в заданном месте сборки][15]

![Настройка задачи публикации в заданном месте сборки][16]

* <span data-ttu-id="69d00-169">Запуск сборки hello</span><span class="sxs-lookup"><span data-stu-id="69d00-169">Run hello build</span></span>

![Постановка новой сборки в очередь][17]

![Просмотр сводки сборки][18]

* <span data-ttu-id="69d00-172">При успешном построении hello вы увидите примерно toobelow результат</span><span class="sxs-lookup"><span data-stu-id="69d00-172">if hello build is successful you will see a result similar toobelow</span></span>

![Результат сборки][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="69d00-174">4.    Процесса настройки выпуска</span><span class="sxs-lookup"><span data-stu-id="69d00-174">4.    Configure Release process</span></span>
* <span data-ttu-id="69d00-175">Создайте новый выпуск.</span><span class="sxs-lookup"><span data-stu-id="69d00-175">Create a new release</span></span>

![Создание нового выпуска][20]

* <span data-ttu-id="69d00-177">Выберите задачу hello развертывания облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="69d00-177">Select hello Azure Cloud Services Deployment task</span></span>

![Выбор задачи развертывания облачных служб Azure][21]

* <span data-ttu-id="69d00-179">Ключ учетной записи хранения hello не отмечены в элементе управления toosource, мы необходим секретный ключ hello toospecify по заданию расширений диагностики.</span><span class="sxs-lookup"><span data-stu-id="69d00-179">As hello storage account key is not checked in toosource control, we need toospecify hello secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="69d00-180">Разверните hello **Дополнительные параметры для создания новой службы** статьи и редактировать hello **ключи учетной записи хранения диагностики** входные параметры.</span><span class="sxs-lookup"><span data-stu-id="69d00-180">Expand hello **Advanced Options for Creating New Service** section and edit hello **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="69d00-181">Принимает входные данные в нескольких строках пара значений ключа в формате hello **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="69d00-181">This input takes in multiple lines of key value pair in hello format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="69d00-182">Примечание: Если вашей учетной записи хранилища диагностики hello ту же подписку для публикации приложения hello облачные службы, не tooenter hello ключ во входных данных задачи hello развертывания; Hello развертывания будет программно получить hello хранилища из подписки</span><span class="sxs-lookup"><span data-stu-id="69d00-182">Note: if your diagnostics storage account is under hello same subscription as where you will publish hello Cloud Services application, you don't have tooenter hello key in hello deployment task input; hello deployment will programmatically obtain hello storage information from your subscription</span></span>
> 
> 

![Настройка задачи развертывания облачных служб][22]

* <span data-ttu-id="69d00-184">Использование секрета сборки переменные toosave хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="69d00-184">Use secret build variables toosave storage Keys.</span></span> <span data-ttu-id="69d00-185">входные переменные toomask переменной в качестве секрета щелкните значок блокировки hello hello правой части hello</span><span class="sxs-lookup"><span data-stu-id="69d00-185">toomask a variable as secret click on hello lock icon on hello right side of hello Variables input</span></span>

![Сохранение ключей к хранилищу данных в секретных переменных сборки][23]

* <span data-ttu-id="69d00-187">Создание выпуска и развертывания вашего проекта tooAzure</span><span class="sxs-lookup"><span data-stu-id="69d00-187">Create a release and deploy your project tooAzure</span></span>

![Создание нового выпуска][24]

## <a name="next-steps"></a><span data-ttu-id="69d00-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69d00-189">Next steps</span></span>
<span data-ttu-id="69d00-190">toolearn Дополнительные сведения о установке расширений диагностики для облачных служб Azure, см. в разделе [включение диагностики в облачных службах Azure с помощью PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="69d00-190">toolearn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

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
