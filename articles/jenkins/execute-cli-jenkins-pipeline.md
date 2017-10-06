---
title: "aaaExecute hello Azure CLI с Jenkins | Документы Microsoft"
description: "Узнайте, как Azure CLI toouse toodeploy Java веб-приложения tooAzure в конвейере Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>Развертывание службы приложений с Jenkins tooAzure и hello Azure CLI
toodeploy tooAzure Java web app, можно использовать Azure CLI в [Jenkins конвейера](https://jenkins.io/doc/book/pipeline/). В этом учебнике мы создадим конвейер CI/CD на виртуальной машине Azure, включая следующие задачи:

> [!div class="checklist"]
> * Создание виртуальной машины Jenkins
> * Настройка Jenkins
> * Создание веб-приложения в Azure
> * Подготовка репозитория GitHub
> * Создание конвейера Jenkins
> * Запустите конвейера hello и проверьте hello веб-приложения

Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии. версия toofind hello, запустите `az --version`. Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Создание и настройка экземпляра Jenkins
Если главный Jenkins еще нет начните с hello [шаблон решения](install-jenkins-solution-template.md), включающее необходимые hello [учетные данные Azure](https://plugins.jenkins.io/azure-credentials) подключаемого модуля по умолчанию. 

Подключаемый модуль Hello учетных данных Azure позволяет основной учетных данных службы Microsoft Azure toostore в Jenkins. В версии 1.2 была добавлена поддержка hello, поэтому конвейера Jenkins можно получить hello учетных данных Azure. 

Убедитесь, что у вас установлена версия 1.2 или более поздняя:
* Панели мониторинга Jenkins hello, нажмите кнопку **Jenkins управления -> подключаемого модуля диспетчера ->** и выполните поиск **учетные данные Azure**. 
* Обновление подключаемого модуля hello, если hello версия более ранняя, чем 1.2.

В базе данных master Jenkins hello также требуются Java JDK и Maven. tooinstall, войдите в базе данных master tooJenkins с помощью SSH и запустите hello, следующие команды:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Добавление учетных данных участника tooJenkins службы Azure

Учетных данных Azure — необходимые tooexecute Azure CLI.

* Панели мониторинга Jenkins hello, нажмите кнопку **учетные данные -> Система ->**. Щелкните **Global credentials (unrestricted)** (Глобальные учетные данные (неограниченные)).
* Нажмите кнопку **добавить учетные данные** tooadd [субъекта-службы Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) , заполнив hello идентификатор подписки, идентификатор клиента, секрет клиента и конечная точка маркера OAuth 2.0. Укажите идентификатор, который будет использоваться в следующем шаге.

![Добавить учетные данные](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Создание службы приложения Azure для развертывания веб-приложения Java hello

Создать план службы приложений Azure с hello **FREE** ценовой категории с помощью hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команду CLI. план служб приложений Hello определяет toohost hello физические ресурсы, используемые приложения. Все приложения, назначенный tooan план служб приложений используют эти ресурсы, позволяя toosave затрат при размещении нескольких приложений. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

При готовности плана hello hello Azure CLI показывает, как выходной toohello в следующем примере:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Создание веб-приложения Azure

 Используйте hello [создать веб-приложение az](/cli/azure/appservice/web#create) toocreate команду CLI определение web app в hello `myAppServicePlan` план служб приложений. Определение приложения Hello web предоставляет приложению tooaccess URL-адрес и настраивает некоторые параметры toodeploy tooAzure вашего кода. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Замена hello `<app_name>` заполнитель с именем собственный уникальный приложения. Это уникальное имя является частью hello имя домена по умолчанию для веб-приложения hello, поэтому hello имя должно toobe уникальным для всех приложений в Azure. Перед тем, как он tooyour пользователей можно сопоставить toohello входа пользовательского домена имя веб-приложения.

При готовности определение приложения hello web hello Azure CLI показано toohello аналогичные сведения, следующий пример: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Настройка Java 

Настройка конфигурации среды выполнения Java hello, необходимый вашему приложению hello [обновление конфигурации web appservice az](/cli/azure/appservice/web/config#update) команды.

Hello следующая команда настраивает hello web app toorun на последние Java JDK 8 и [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a>Подготовка репозитория GitHub
Откройте hello [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample) репозитория. toofork hello репозитория tooyour владельцем учетной записи GitHub, нажмите кнопку hello **вилки** кнопку в правом верхнем углу hello.

* В пользовательском веб-интерфейсе GitHub откройте файл **Jenkinsfile**. Нажмите кнопку tooedit значок карандаша hello этой группы ресурсов hello tooupdate файла и имя веб-приложения в строке, 20 и 21 соответственно.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Измените идентификатор учетных данных 23 tooupdate строки в вашем экземпляре Jenkins

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Создание конвейера Jenkins
Откройте Jenkins в веб-браузере, щелкните **New Item** (Создать элемент). 

* Укажите имя для задания hello и выберите **конвейера**. Нажмите кнопку **ОК**.
* Нажмите кнопку hello **конвейера** вкладке рядом. 
* Для параметра **Definition** (Определение) выберите значение **Pipeline script from SCM** (Сценарий конвейера из SCM).
* Для параметра **SCM** выберите значение **Git**.
* Введите hello GitHub URL-адрес для вашего разветвленного репозитория: https:\<репозиторию разветвленного\>.git
* Нажмите кнопку **Сохранить**

## <a name="test-your-pipeline"></a>Тестирование конвейера
* Go toohello конвейера, вы создали, щелкните **теперь построения**
* Сборка должна выполняться в течение нескольких секунд, и вы можете вернуться toohello построения и нажмите кнопку **вывод на консоль** toosee hello сведения

## <a name="verify-your-web-app"></a>Проверка веб-приложения
tooverify hello WAR-файл успешно развернут tooyour веб-приложения. Откройте веб-браузер:

* Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/ping  
Вот что вы увидите:

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (подставьте &lt;x > и &lt;y > с любой цифры) сумма hello tooget x и y

![Калькулятор: сложение](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>Развертывание tooAzure веб-приложения в Linux
Теперь, когда вы знаете, как конвейер toouse Azure CLI в вашей Jenkins, вы можете изменить tooan toodeploy hello скрипта веб-приложения Azure в Linux.

Веб-приложения на платформе Linux поддерживает развертывание hello toodo другим способом, который является toouse Docker. toodeploy, необходимо tooprovide Dockerfile, которая упаковывает веб-приложения в среде выполнения службы в Docker изображение. Подключаемый модуль Hello затем сборки образа hello, принудительно отправить его tooa реестра Docker и развертывания hello изображения tooyour веб-приложения.

* Выполните действия hello [здесь](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate на веб-приложения Azure, выполняемым на платформе Linux.
* Установка Docker Jenkins экземпляра в соответствии с инструкциями hello в этом [статьи](https://docs.docker.com/engine/installation/linux/ubuntu/).
* Создание реестра контейнера в hello портал Azure с помощью действия hello [здесь](/azure/container-registry/container-registry-get-started-azure-cli).
* В hello же [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample) репозитория вы разделенными, изменить hello **Jenkinsfile2** файла:
    * Строка 18-21, соответственно обновить имена toohello группы ресурсов, веб-приложения и контроля доступа. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * Строка 24, обновление \<azsrvprincipal\> tooyour идентификатор учетных данных
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Создать новый конвейер Jenkins, как это было сделано при развертывании tooAzure веб-приложения в Windows, только на этот раз используйте **Jenkinsfile2** вместо него.
* Запустите новое задание.
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
В этом учебнике вы настроили Jenkins конвейера, который извлекает hello исходного кода в репозитории GitHub. Выполняется Maven toobuild war-файл и затем использует Azure CLI toodeploy tooAzure службы приложений. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание виртуальной машины Jenkins
> * Настройка Jenkins
> * Создание веб-приложения в Azure
> * Подготовка репозитория GitHub
> * Создание конвейера Jenkins
> * Запустите конвейера hello и проверьте hello веб-приложения
