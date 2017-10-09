---
title: "aaaDeploy tooAzure службы приложений с помощью подключаемого модуля Jenkins | Документы Microsoft"
description: "Узнайте, как toouse Jenkins службы приложения Azure toodeploy Java для подключаемого модуля веб-приложения tooAzure в Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>Развертывание tooAzure службы приложений с помощью подключаемого модуля Jenkins 
toodeploy tooAzure Java web app, можно использовать Azure CLI в [конвейера Jenkins](/azure/jenkins/execute-cli-jenkins-pipeline) либо можно использовать hello [подключаемый модуль Azure приложение службы Jenkins](https://plugins.jenkins.io/azure-app-service). Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Настройка tooAzure toodeploy Jenkins службы приложений по протоколу FTP 
> * Настройка tooAzure toodeploy Jenkins службы приложений на платформе Linux через Docker 

## <a name="create-and-configure-jenkins-instance"></a>Создание и настройка экземпляра Jenkins
Если главный Jenkins еще нет начните с hello [шаблон решения](install-jenkins-solution-template.md), включая JDK8 и hello следующие необходимые подключаемые модули:

* [подключаемый модуль Jenkins клиента Git](https://plugins.jenkins.io/git-client) версии 2.4.6; 
* [подключаемый модуль Docker Commons](https://plugins.jenkins.io/docker-commons) версии 1.4.0;
* [учетные данные Azure](https://plugins.jenkins.io/azure-credentials) версии 1.2;
* [служба приложений Azure](https://plugins.jenkins.io/azure-app-server) версии 0.1.

Можно использовать hello toodeploy службы приложения подключаемого модуля веб-приложения на всех языках (например, C#, PHP, Java и node.js и т.д.), поддерживаемых службой приложения Azure. В этом учебнике мы используем hello пример приложения Java, [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample). toofork hello репозитория tooyour владельцем учетной записи GitHub, нажмите кнопку hello **вилки** кнопку в правом верхнем углу hello.  

Для построения проекта Java hello требуются Java JDK и Maven. Убедитесь, что компоненты hello в образец hello Jenkins или hello агент виртуальной Машины при использовании одного непрерывной интеграции. 

tooinstall, войдите в экземпляре toohello Jenkins, с помощью SSH и запустите hello, следующие команды:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

Для развертывания tooApp службы в Linux, необходимо также tooinstall Docker в образец Jenkins hello или hello агента виртуальной Машины, используемого для построения. См. в статье toothis tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-toojenkins-credential"></a>Добавление учетных данных участника tooJenkins службы Azure

Участник службы Azure является необходимые toodeploy tooAzure. 

<ol>
<li>Используйте [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) или [портал Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate участника-службы Azure</li>
<li>Панели мониторинга Jenkins hello, нажмите кнопку **учетные данные -> Система ->**. Щелкните **Global credentials (unrestricted)** (Глобальные учетные данные (неограниченные)).</li>
<li>Нажмите кнопку **добавить учетные данные** tooadd субъекта-службы Microsoft Azure, заполнив hello идентификатор подписки, идентификатор клиента, секрет клиента и конечная точка маркера OAuth 2.0. Укажите идентификатор, **mySp**, который будет использоваться в следующем шаге.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Подключаемый модуль службы приложений Azure

V1.0 подключаемый модуль Azure службы приложений поддерживает tooAzure непрерывного развертывания веб-приложения через:

* Git и FTP;
* Docker для веб-приложения в Linux.

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>Настройка Jenkins toodeploy веб-приложения по протоколу FTP, с помощью панели мониторинга hello Jenkins

toodeploy tooAzure вашего проекта веб-приложения можно отправить на артефактов сборки (например, файл .war в Java) с использованием Git или FTP.

Перед настройкой задания hello в Jenkins, требуется план службы приложений Azure и веб-приложения для запущенного приложения Java hello.


1. Создать план службы приложений Azure с hello **FREE** ценовой категории с помощью hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команду CLI. план служб приложений Hello определяет toohost hello физические ресурсы, используемые приложения. Все приложения, назначенный tooan план служб приложений используют эти ресурсы, позволяя toosave затрат при размещении нескольких приложений.
2. Создайте веб-приложение. Можно либо использовать hello [портал Azure](/azure/app-service-web/web-sites-configure) или hello используйте следующую команду Az CLI:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Убедитесь, что настройка конфигурации среды выполнения Java hello, необходимый вашему приложению. следующую команду Azure CLI Hello настраивает hello web app toorun на последние Java JDK 8 и [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>Настройка задания hello Jenkins


1. Создайте **универсальный** проект на панели мониторинга Jenkins.
2. Настройка **управление исходным кодом** toouse локального ветвления [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample) , предоставляя hello **URL-адрес репозитория**. Например: http://github.com/&lt;yourID>/javawebappsample.
3. Добавьте проект hello toobuild шаг построения, с помощью Maven. Для этого добавьте **оболочку выполнения**. В этом примере мы должны hello *.war дополнительный шаг toorename файл в целевой папке tooROOT.war.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Добавьте действие после сборки, выбрав **Publish an Azure Web App** (Публикация веб-приложения Azure).
5. Питания, «mySp», участника службы Azure hello, хранящихся в предыдущем шаге.
6. В **Конфигурация приложения** выберите группу и веб-приложение hello ресурсов в вашей подписке. Hello подключаемого модуля автоматически определяет, является ли hello веб-приложения Windows или Linux. Для веб-приложения на основе Windows представлен hello параметр «Опубликовать файлы».
7. Заливка в файлах hello требуется toodeploy (например, war пакет, если вы используете Java.) Исходный и целевой каталоги являются необязательными. Параметры Hello разрешить toospecify исходной и конечной папки при отправке файлов. Веб-приложение Java в Azure выполняется на сервере Tomcat. Поэтому пакет в формате WAR передается в папку веб-приложений. В этом примере значение **исходный каталог** слишком «target» и ввести «веб-приложений» **целевой каталог**.
8. Следует toodeploy tooa слот, отличные от производственной можно также задать **слот** имя.
9. Сохраните проект hello и постройте его. Веб-приложения — развернутой tooAzure после завершения построения.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Развертывание веб-приложения по протоколу FTP с помощью конвейера Jenkins

Подключаемый модуль Hello — готовых конвейера. Можно обратиться пример tooa в репозитории GitHub hello.

1. В пользовательском веб-интерфейсе GitHub откройте файл **Jenkinsfile_ftp_plugin**. Нажмите кнопку tooedit значок карандаша hello этой группы ресурсов hello tooupdate файла и имя веб-приложения в строке 11 и 12 соответственно.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Измените идентификатор учетных данных 14 tooupdate строки в вашем экземпляре Jenkins.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Создание конвейера Jenkins

1. Откройте Jenkins в веб-браузере, щелкните **New Item** (Создать элемент).
2. Укажите имя для задания hello и выберите **конвейера**. Нажмите кнопку **ОК**.
3. Нажмите кнопку hello **конвейера** вкладке рядом.
4. Для параметра **Definition** (Определение) выберите значение **Pipeline script from SCM** (Сценарий конвейера из SCM).
5. Для параметра **SCM** выберите значение **Git**. Введите hello GitHub URL-адрес для вашего разветвленного репозитория: https:&lt;репозиторию разветвленного > .git
6. Обновление **путь к скрипту** слишком «Jenkinsfile_ftp_plugin»
7. Нажмите кнопку **Сохранить** и hello выполнения задания.

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>Настройка Jenkins toodeploy веб-приложения на платформе Linux через Docker

Помимо Git и FTP веб-приложение в Linux поддерживает развертывания с помощью Docker. с помощью Docker, toodeploy необходимо tooprovide Dockerfile, которая упаковывает веб-приложения в среде выполнения службы в docker изображение. Затем подключаемый модуль hello построения образа hello, отправляющий ее tooa реестра docker и развертывает hello изображения tooyour веб-приложения.

Веб-приложения на платформе Linux также поддерживают традиционные способы, такие как Git и FTP, но только для встроенных языков (.NET Core, Node.js, PHP и Ruby). Для других языков требуется toopackage выполнения кода и службы приложения вместе с помощью образа docker и использовать docker toodeploy.

Перед настройкой задания hello в Jenkins, необходимо в качестве службы приложения Azure Linux. Реестр контейнера также необходимые toostore и управление образами закрытый контейнер Docker. Вы можете использовать DockerHub. В этом примере используется реестр контейнеров Azure.

* Выполните действия hello [здесь](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate веб-приложения в Linux 
* Azure реестр контейнера является управляемый [Docker реестра] службы (https://docs.docker.com/registry/) на основании hello 2.0 реестра Docker открытым исходным кодом. Выполните действия hello [здесь] (/ azure/container-registry/container-registry-get-started-azure-cli) Дополнительные рекомендации о том, как toodo так. Кроме того, можно использовать DockerHub.

### <a name="toodeploy-using-docker"></a>с помощью docker toodeploy:

1. Создайте универсальный проект на панели мониторинга Jenkins.
2. Настройка **управление исходным кодом** toouse локального ветвления [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample) , предоставляя hello **URL-адрес репозитория**. Например: http://github.com/&lt;yourid>/javawebappsample.
Добавьте проект hello toobuild шаг построения, с помощью Maven. Сделать, добавив **выполнение оболочки** и добавить следующие строки в hello **команды**:    
```bash
mvn clean package
```

3. Добавьте действие после сборки, выбрав **Publish an Azure Web App** (Публикация веб-приложения Azure).
4. Укажите, **mySp**, хранящихся в предыдущем шаге, учетные данные Azure участника службы Azure hello.
5. В **Конфигурация приложения** выберите группу ресурсов hello и веб-приложения Linux в вашей подписке.
6. Выберите публикацию через Docker.
7. Заполните путь **Dockerfile**. Можно сохранить по умолчанию hello «/ Dockerfile» для **URL-адрес реестра Docker**указывайте в формате https:// hello&lt;myRegistry >. azurecr.io при использовании реестра контейнера Azure. Не указывайте его при использовании DockerHub.
8. Для **учетные данные реестра**, добавьте hello учетные данные для hello реестра контейнера Azure. Hello идентификатор пользователя и пароль можно получить, выполнив следующие команды в Azure CLI hello. Первая команда Hello включает hello учетной записи администратора.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. Здравствуйте, имя образа docker и тег в **Дополнительно** вкладке являются необязательными. По умолчанию имя образа получается из образа hello имя, указанное в теге hello Azure портала (в контейнер Docker параметр.) создается на основе $BUILD_NUMBER. Убедитесь в том, укажите имя образа hello либо портале Azure или задать значение для **образа Docker** в **Дополнительно** вкладки. В этом примере укажите &lt;yourRegistry >.azurecr.io/calculator в качестве значения для **образа Docker** и не указывайте **тег образа Docker**.
10. Примечание. Развертывание завершается сбоем, если использовать параметр встроенного образа Docker. Убедитесь, что изменение docker config toouse настраиваемого изображения в контейнер Docker параметр на портале Azure. Для встроенного изображения используется toodeploy подход передачи файла.
11. Аналогичный подход toofile передачи, можно выбрать другой слот, отличные от рабочей.
12. Сохраните и постройте проект hello. Вы увидите образ контейнера помещается tooyour реестра и развернуть веб-приложения.

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>Развертывание приложения на платформе Linux через Docker с помощью конвейера Jenkins tooWeb

1. В пользовательском веб-интерфейсе GitHub откройте файл **Jenkinsfile_container_plugin**. Нажмите кнопку tooedit значок карандаша hello этой группы ресурсов hello tooupdate файла и имя веб-приложения в строке 11 и 12 соответственно.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Изменение строки 13 tooyour контейнер реестра сервера    
```java
def registryServer = '<registryURL>'
```    

3. Измените идентификатор учетных данных 16 tooupdate строки в вашем экземпляре Jenkins    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Создание конвейера Jenkins    

1. Откройте Jenkins в веб-браузере, щелкните **New Item** (Создать элемент).
2. Укажите имя для задания hello и выберите **конвейера**. Нажмите кнопку **ОК**.
3. Нажмите кнопку hello **конвейера** вкладке рядом.
4. Для параметра **Definition** (Определение) выберите значение **Pipeline script from SCM** (Сценарий конвейера из SCM).
5. Для параметра **SCM** выберите значение **Git**.
6. Введите hello GitHub URL-адрес для вашего разветвленного репозитория: https:&lt;репозиторию разветвленного > .git</li>
Обновление 7, **путь к скрипту** слишком «Jenkinsfile_container_plugin»
8. Нажмите кнопку **Сохранить** и hello выполнения задания.

## <a name="verify-your-web-app"></a>Проверка веб-приложения

1. tooverify hello WAR-файл успешно развернут tooyour веб-приложения. Откройте веб-браузер.
2. Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/ping отображается:    
     Вас приветствует tooJava веб-приложения!!! Это обновленная версия!
   17 июня, воскресенье, 16:39:10 UTC, 2017 г.
3. Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (подставьте &lt;x > и &lt;y > с любой цифры) сумма hello tooget x и y        
    ![Калькулятор: сложение](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Для службы приложений под управлением Linux

* tooverify, в Azure CLI, выполните:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    Вы получаете hello следующий результат:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/ping. Отображается сообщение hello: 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (подставьте &lt;x > и &lt;y > с любой цифры) сумма hello tooget x и y
    
## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике используется tooAzure toodeploy подключаемого модуля службы приложений Azure hello.

Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Настройка Jenkins toodeploy службе приложений Azure по протоколу FTP 
> * Настройка tooAzure toodeploy Jenkins службы приложений на платформе Linux через Docker 
