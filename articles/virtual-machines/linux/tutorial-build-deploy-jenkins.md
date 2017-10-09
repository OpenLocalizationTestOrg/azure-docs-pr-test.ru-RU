---
title: "aaaCI/CD из Jenkins tooAzure виртуальных машин с Team Services | Документы Microsoft"
description: "Настройка непрерывной интеграции (CI) и непрерывного развертывания (CD) с помощью виртуальных машин tooAzure Jenkins из управления выпусками в Visual Studio Team Services (VSTS) или Microsoft Team Foundation Server (TFS) приложение Node.js"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>Развертывание вашего приложения tooLinux виртуальных машин с помощью Jenkins и Team Services

Непрерывная интеграция (CI) и непрерывное развертывание (CD) представляют собой конвейер, с помощью которого можно выполнить сборку, выпустить и развернуть свой код. Team Services предоставляет полный, полнофункциональный набор средств автоматизации CI или компакт-диска для развертывания tooAzure. Jenkins — это популярный серверный инструмент CI и CD стороннего поставщика, который также обеспечивает автоматизацию этих процессов. Можно использовать оба вместе toocustomize способ доставки облачного приложения или службы.

В этом учебнике используется Jenkins toobuild **веб-приложение Node.js**и Visual Studio Team Services toodeploy его tooa [Группа развертывания](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) содержащий виртуальных машин Linux.

Вы сможете выполнять следующие задачи:

> [!div class="checklist"]
> * Выполнение сборки приложения в Jenkins.
> * Настройка Jenkins для интеграции с Team Services.
> * Создание группы развертывания для hello виртуальных машинах Azure
> * Создание определения выпуска, который настраивает hello виртуальных машин и развертывает приложение hello

## <a name="before-you-begin"></a>Перед началом работы

* Требуется учетная запись доступа к tooa Jenkins. Если вы еще не создали сервер Jenkins, ознакомьтесь с [документацией по Jenkins](https://jenkins.io/doc/). 

* Войдите в учетную запись Team Services tooyour (`https://{youraccount}.visualstudio.com`). 
  Вы можете получить [бесплатную учетную запись Team Services](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).

  > [!NOTE]
  > Дополнительные сведения см. в разделе [подключения служб tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).

* Создайте личный маркер доступа (PAT) в своей учетной записи Team Services, если у вас его еще нет. Jenkins требуется этот tooaccess сведения учетной записи Team Services.
  Чтение [как создать личный маркер доступа для Team Services и TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn как toogenerate один.

## <a name="get-hello-sample-app"></a>Получите пример приложения hello

Вы должны toodeploy приложения, хранятся в репозитории.
В данном руководстве мы рекомендуем использовать [этот пример приложения с сайта GitHub](https://github.com/azooinmyluggage/fabrikam-node).

1. Создайте вилку это приложение и запишите расположение hello (URL) для использования в последующих шагах данного учебника.

1. Сделать вилки hello **открытый** toosimplify подключения tooGitHub позднее.

> [!NOTE]
> Дополнительные сведения см. в разделах [Fork A Repo](https://help.github.com/articles/fork-a-repo/) (Создание вилки репозитория) и [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/) (Как сделать частный репозиторий общедоступным).

> [!NOTE]
> приложение Hello был создан с помощью [Yeoman](http://yeoman.io/learning/index.html); он использует **Express**, **bower**, и **grunt**; и он обладает некоторыми **npm**пакетов в качестве зависимости.
> Пример приложения Hello содержит набор [шаблоны Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) , используемые toodynamically создаются hello виртуальных машин для развертывания в Azure. Эти шаблоны используются в задачах hello [определение выпуска Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).
> основной шаблон Hello создает группу безопасности сети, виртуальной машины и виртуальной сети. Он назначает общедоступный IP-адрес и открывает входящий порт 80. Он также добавляет тег, который используется hello развертывания группы слишком выберите hello машины tooreceive hello развертыванием.
>
> Образец Hello также содержит скрипт, который настраивает Nginx и развертывает приложение hello. Он выполняется на всех виртуальных машинах hello. В частности hello скрипт устанавливает узла, Nginx и PM2; Настраивает Nginx и PM2; затем запускает приложение hello узла.

## <a name="configure-jenkins-plugins"></a>Настройка подключаемых модулей Jenkins

Сначала необходимо настроить два подключаемых модуля Jenkins для **NodeJS** и **интеграции с Team Services**.

1. Откройте учетную запись Jenkins и выберите **Manage Jenkins** (Управление Jenkins).

1. В hello **управления Jenkins** выберите **управление подключаемыми модулями**.

1. Список toolocate фильтра hello hello **NodeJS** подключаемого модуля и установить его без перезапуска.

   ![Добавление подключаемого модуля tooJenkins hello NodeJS](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. Список toofind фильтра hello hello **Team Foundation Server** подключаемого модуля и установить его. (Этот подключаемый модуль подходит и для Team Services, и для Team Foundation Server.) Перезапускать Jenkins не обязательно.

## <a name="configure-jenkins-build-for-nodejs"></a>Настройка сборки Jenkins для Node.js

Создайте в Jenkins проект сборки и настройте его следующим образом.

1. В hello **Общие** введите имя для сборки проекта.

1. В hello **управление исходным кодом** выберите **Git** и введите сведения о hello репозитория hello и hello ветвь, содержащая код приложения.

   ![Добавление сборки tooyour репозитория](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > Если репозиторий не является открытым, выберите **добавить** и предоставить tooit tooconnect учетные данные.

1. В hello **сборки триггеров** выберите **SCM опроса** и введите hello расписания `H/03 * * * *` toopoll hello репозитории для изменения каждые три минуты. 

1. В hello **среду сборки среды** выберите **предоставляют узел &amp; npm bin / путь к папке** и введите `NodeJS` для hello значение узла JS установки. Для параметра **npmrc file** (NPMRC-файл) оставьте значение "use system default" (Использовать системное значение по умолчанию).

1. В hello **построения** , введите команду hello `npm install` tooensure, обновляются все зависимости.

## <a name="configure-jenkins-for-team-services-integration"></a>Настройка Jenkins для интеграции с Team Services.

1. В hello **действия после построения** вкладке для **tooarchive файлы**, введите `**/*` tooinclude все файлы.

1. Для **выпуска в TFS и Team Services**, введите полный URL-адрес hello, учетной записи (например, `https://your-account-name.visualstudio.com`), hello имя проекта, для определения выпуска hello (создано в более поздней версии), имя и hello учетной записи tooyour tooconnect учетные данные.
   Требуется имя пользователя и hello МАРИЯ, созданного ранее. 

   ![Настройка действий после сборки Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. Сохраните проект сборки hello.

## <a name="create-a-jenkins-service-endpoint"></a>Создание конечной точки службы Jenkins

Конечная точка службы позволяет tooJenkins tooconnect Team Services.

1. Откройте hello **службы** страницы в Team Services, откройте hello **новую конечную точку службы** , а затем выберите **Jenkins**.

   ![Добавление конечной точки Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. Введите имя, будет использовать toorefer toothis соединения.

1. Введите адрес URL сервера Jenkins hello и деления hello **принимать недоверенные сертификаты SSL** параметр.

1. Введите hello имя пользователя и пароль для учетной записи Jenkins.

1. Выберите **Проверка подключения** toocheck, hello сведения верны.

1. Выберите **ОК** конечной точки службы toocreate hello.

## <a name="create-a-deployment-group"></a>Создание группы развертывания

Требуется [Группа развертывания](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) слишком содержат hello виртуальных машин.

1. Привет открыть **выпуски** вкладка hello **построения &amp; выпуска** концентратора, а затем откройте hello **группы развертывания** и кнопку **+ создать**.

1. Введите имя для группы развертывания hello и необязательное описание.
   Щелкните **Создать**.

Задача развертывания группы ресурсов Azure Hello создает и регистрирует hello виртуальных машин, когда оно выполняется с помощью шаблона Azure Resource Manager hello.
Не нужны toocreate и зарегистрироваться в hello виртуальных машин.

## <a name="create-a-release-definition"></a>Создание определения выпуска

Определение выпуска указывает, что процесс hello Team Services будет выполняться приложение hello toodeploy.
Определение выпуска toocreate hello в Team Services:

1. Откройте hello **выпуски** вкладка hello **построения &amp; выпуска** концентратора, откройте hello  **+**  раскрывающегося списка в список hello определения выпуска, а затем выберите Hello **создать определение выпуска**. 

1. Выберите hello **пустой** шаблона и выберите **Далее**.

1. В hello **артефакты** щелкните **ссылку артефакта** и выберите **Jenkins**. Выберите подключение к конечной точке службы Jenkins. Затем выберите задание источника Jenkins hello и выберите **создать**. 

1. В новых hello определение выпуска, выберите **+ добавить задачи** и добавьте **развертывания группы ресурсов Azure** среды по умолчанию toohello задач.

1. Выберите hello раскрывающийся список стрелку Далее toohello **+ добавить задачи** ссылку и добавьте определение toohello этап развертывания группы.

   ![Добавление этапа группы развертывания](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. В каталоге hello задач, откройте hello **программы** раздел и добавить экземпляр hello **сценарий** задачи.

1. шаблон параметров Hello, используемый в задачу развертывания группы ресурсов Azure hello задает hello администратора пароль, используемый tooconnect toohello виртуальных машин.
   Укажите этот пароль с переменной hello **$(adminpassword)**:
   
   - Откройте hello **переменных** вкладке и в hello **переменных** введите имя hello `adminpassword`.

   - Введите пароль администратора hello.

   - Выберите hello «замка» значок Далее toohello значение текстового поля tooprotect hello пароль. 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>Настроить задачу hello развертывания группы ресурсов Azure

Hello **развертывания группы ресурсов Azure** задача — Группа развертывания используется toocreate hello. Настройте его следующим образом.

* **Подписка Azure:** выберите соединение из списка hello **доступных подключений службы Azure**. 
  Если подключения не отображается, выберите **управление**выберите **новую конечную точку службы** затем **диспетчера ресурсов Azure**и следуйте появляющимся на hello.
  Возвращает определение tooyour выпуска, обновления hello **AzureRM подписки** список и выберите hello подключения, вы создали.

* **Группа ресурсов**: Введите имя группы ресурсов hello, созданного ранее.

* **Расположение**: Выберите регион для развертывания hello.

  ![Создание новой группы ресурсов](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **Расположение шаблона**: `URL of hello file`.

* **Ссылка на шаблон**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`.

* **Ссылка на параметры шаблона**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`.

* **Переопределение параметров шаблона**: список hello переопределения значений, например: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.<br />Вставьте особые значения для hello {заполнители}. 

* **Включить необходимые компоненты**: `Configure with Deployment Group agent`.

* **Конечная точка TFS и VSTS**: выберите **добавить** и в диалоговом окне «Добавить новое подключение службы Team Foundation Server и Team» hello, выберите **токена проверки подлинности на основе**. Введите имя соединения, hello и hello URL-адрес командного проекта. Создает и введите [маркера личных доступа (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello подключения tooyour командного проекта.

  ![Создание личного маркера доступа](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Командный проект**: выберите свой текущий проект.

* **Группа развертывания**: Введите hello одинаковые имена групп развертывания, используемого для hello **группы ресурсов** параметра.

параметры по умолчанию Hello для развертывания группы ресурсов Azure задачу hello toocreate или поэтому добавочное обновление ресурсов и toodo. Задача Hello создает hello виртуальных машин hello первый раз, он выполняется и впоследствии изменить их.

## <a name="configure-hello-shell-script-task"></a>Настройка задачи «Сценарий» hello

Hello **сценарий** задач является конфигурацией hello используется tooprovide toorun скрипт на каждый сервер tooinstall Node.js и запустите приложение hello. Настройте его следующим образом.

* **Путь к скрипту**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`.

* **Указать рабочий каталог**: `Checked`.

* **Рабочий каталог**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`.
   
## <a name="rename-and-save-hello-release-definition"></a>Переименовать и сохранить определение выпуска hello

1. Измените имя hello hello определения выпуска toohello имя, указанное в **действия после построения** вкладке сборки hello в Jenkins. При обновлении источника артефактов hello, Jenkins требует может tootrigger каталога toobe это имя нового выпуска.

1. При необходимости измените имя hello среды hello, щелкнув имя hello. 

1. Щелкните **Сохранить** и нажмите кнопку **ОК**.

## <a name="start-a-manual-deployment"></a>Запуск развертывания вручную

1. Щелкните **+ Release** (+ Выпуск) и выберите **Создать выпуск**.

1. Щелкните завершения построения hello в hello выделенного раскрывающегося списка и выберите **создать**.

1. Выберите ссылку выпуска hello в всплывающее сообщение hello. Пример: Создан выпуск **Release-1**.

1. Откройте hello **журналы** вкладке вывод на консоль выпуска toowatch hello.

1. В браузере, откройте hello URL-адрес одного из серверов hello добавлена группа tooyour развертывания. Например, введите `http://{your-server-ip-address}`.

## <a name="start-a-cicd-deployment"></a>Запуск непрерывной интеграции или непрерывного развертывания

1. Определение выпуска hello, снимите флажок hello **включено** флажок в hello **параметры управления** hello параметров для развертывания группы ресурсов Azure задачу hello.
   Для будущих развертываний toohello существующего развертывания группы не требуется toore-выполнения этой задачи.

1. Репозиторий Git источника toohello вернуться и изменить содержимое hello hello **h1** заголовок в файле hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).

1. Зафиксируйте изменения.

1. Через несколько минут вы увидите новый выпуск, созданный в hello **выпуски** страница Team Services или TFS. Откройте hello выпуска toosee hello развертывания происходит. Поздравляем!

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике автоматизировать развертывание hello tooAzure приложения с помощью сборки Jenkins и Team Services для выпуска. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Выполнение сборки приложения в Jenkins.
> * Настройка Jenkins для интеграции с Team Services.
> * Создание группы развертывания для hello виртуальных машинах Azure
> * Создание определения выпуска, который настраивает hello виртуальных машин и развертывает приложение hello

Дополнительные сведения о как стек LAMP (Linux, Apache, MySQL и PHP) toodeploy приращения Далее учебника toolearn toohello.

> [!div class="nextstepaction"]
> [Развертывание стека LAMP](tutorial-lamp-stack.md)