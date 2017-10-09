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
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely сохранить службы диагностики ключ облачного хранилища и tooAzure Настройка непрерывной интеграции и развертывания с помощью Visual Studio Online
 Это общие исходные проекты tooopen рекомендаций в настоящее время. Сохранять секреты приложения в файлах конфигурации теперь опасно, так как утечка секретов из общедоступной системы управления версиями ставит под угрозу безопасность. Хранение секрет как открытый текст в файле в конвейере непрерывной интеграции не является безопасным либо с момента построения серверы могут быть общие ресурсы на hello облачной среде. В этой статье объясняется, каким образом Visual Studio и Visual Studio Online взлому hello обеспечения безопасности во время разработки и процесс непрерывной интеграции.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Удаление секрета ключа к хранилищу данных диагностики из файла конфигурации проекта
Расширению диагностики облачных служб необходимо хранилище Azure, чтобы сохранять результаты диагностики. Ранее строки подключения к хранилищу hello задается в файлах конфигурации (cscfg) hello облачные службы и вернуть удалось toosource управления. В последнем выпуске пакета Azure SDK hello мы изменили hello поведение tooonly хранилище строка частичного соединения с ключом hello замена маркером. Hello следующие шаги описывают, как работает hello новые инструменты облачные службы:

### <a name="1-open-hello-role-designer"></a>1. Откройте конструктор ролей hello
* Дважды щелкните или щелкните правой кнопкой мыши в конструкторе ролей tooopen роли облачных служб

![Открытие конструктора ролей][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. В разделе "Диагностика" добавлен новый флажок "Не удалять секрет ключа хранилища из файла конфигурации проекта (CSCFG-файла)"
* При использовании эмулятора локального хранилища hello, этот флажок недоступен, так как нет секретный toomanage для строки локального подключения hello, который является UseDevelopmentStorage = true.

![Строка подключения к эмулятору локального хранилища не является секретом][1]

* Если вы создаете новый проект, по умолчанию этот флажок снят. Это приводит к hello хранения основной раздел hello выбранные строки подключения к хранилищу заменяемого с маркером. Hello значение токена hello располагается в папке текущего пользователя hello AppData перемещаемых, например: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Обратите внимание, эту папку user\AppData hello является контролировать доступ, вход пользователей и считается секреты разработки toostore надежном месте.
> 
> 

![Ключ к хранилищу данных сохранен в папке профиля пользователя][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Выбор учетной записи хранения для диагностики
* Выберите учетную запись хранилища в диалоговом окне приветствия запускается через пункт меню «...» hello . Обратите внимание на то, как создается строка подключения хранилища hello не будет иметь hello ключ учетной записи хранения.
* Например, DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.    Отладка проекта hello
* F5 toostart отладки в Visual Studio. Все, что должно работать в hello таким же образом как раньше.
  ![Локальный запуск отладки][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Публикация проекта из Visual Studio
* Запуск hello диалоговое окно публикации и продолжите tooAzure applicaion hello toopublish входа в инструкции.

### <a name="6-additional-information"></a>6. Дополнительная информация
> Примечание: hello панель параметров в конструкторе ролей hello остается это сейчас. Функция секретный управления hello toouse для диагностики, перейдите вкладку toohello конфигурации.
> 
> 

![Добавление параметров][4]

> Примечание: Если параметр включен, hello Application Insights будет храниться ключ как обычный текст. Hello ключ используется только для передачи содержимого, конфиденциальные данные не будут риск раскрытия.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Создание и публикация проекта облачных служб с помощью шаблонов задач Visual Studio Online
* иллюстрирует следующие шаги Hello как проект с помощью Visual Studio online задач toosetup непрерывной интеграции для облачных служб:
  ### <a name="1----obtain-a-vso-account"></a>1.    Получение учетной записи VSO
* [Создайте учетную запись Visual Studio Online] [ Create Visual Studio Online account] Если вы их еще нет
* [Создание командного проекта] [ Create team project] своей учетной записи Visual Studio online

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Настройка системы управления версиями в Visual Studio
* Подключение tooa командного проекта

![Подключить проект tooteam][5]

![Выберите tooconnect командного проекта для][6]

* Добавить элемент управления toosource проекта

![Добавление элемента управления toosource проекта][7]

![Сопоставление папки системы управления версиями tooa проекта][8]

* Запишите проект после изменения из Team Explorer.

![Возврат управления toosource проекта][9]

### <a name="3----configure-build-process"></a>3.    Настройка процесса сборки
* Обзор tooyour командного проекта и добавьте новый процесс построения шаблонов

![Добавление новой сборки][10]

* Выберите задачу сборки.

![Добавление задачи сборки][11]

![Выбор шаблона задачи сборки в Visual Studio][12]

* Измените входные данные задачи сборки. Настраивайте hello сборки, необходимые параметры в соответствии с tooyour

![Настройка задачи сборки][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Настройте переменные сборки.

![Настройка переменных сборки.][14]

* Добавление каталога построения tooupload задач

![Выбор задачи публикации в заданном месте сборки][15]

![Настройка задачи публикации в заданном месте сборки][16]

* Запуск сборки hello

![Постановка новой сборки в очередь][17]

![Просмотр сводки сборки][18]

* При успешном построении hello вы увидите примерно toobelow результат

![Результат сборки][19]

### <a name="4----configure-release-process"></a>4.    Процесса настройки выпуска
* Создайте новый выпуск.

![Создание нового выпуска][20]

* Выберите задачу hello развертывания облачной службы Azure

![Выбор задачи развертывания облачных служб Azure][21]

* Ключ учетной записи хранения hello не отмечены в элементе управления toosource, мы необходим секретный ключ hello toospecify по заданию расширений диагностики. Разверните hello **Дополнительные параметры для создания новой службы** статьи и редактировать hello **ключи учетной записи хранения диагностики** входные параметры. Принимает входные данные в нескольких строках пара значений ключа в формате hello **[RoleName]:$(StorageAccountKey)**

> Примечание: Если вашей учетной записи хранилища диагностики hello ту же подписку для публикации приложения hello облачные службы, не tooenter hello ключ во входных данных задачи hello развертывания; Hello развертывания будет программно получить hello хранилища из подписки
> 
> 

![Настройка задачи развертывания облачных служб][22]

* Использование секрета сборки переменные toosave хранилища ключей. входные переменные toomask переменной в качестве секрета щелкните значок блокировки hello hello правой части hello

![Сохранение ключей к хранилищу данных в секретных переменных сборки][23]

* Создание выпуска и развертывания вашего проекта tooAzure

![Создание нового выпуска][24]

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о установке расширений диагностики для облачных служб Azure, см. в разделе [включение диагностики в облачных службах Azure с помощью PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]

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
