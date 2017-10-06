---
title: "aaaBuild веб-приложения Java и MySQL в Azure"
description: "Узнайте, как tooget приложения Java, подключается служба базы данных MySQL в Azure toohello, работа в Azure службы приложений."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>Создание веб-приложения Java в Azure с подключением к базе данных MySQL

Этот учебник показывает, как toocreate Java веб-приложения в Azure и соедините его tooa базы данных MySQL. Когда вы выполните инструкции руководства, у вас будет приложение [Spring Boot](https://projects.spring.io/spring-boot/), данные которого хранятся в [базе данных Azure для MySQL](https://docs.microsoft.com/azure/mysql/overview), которая работает в [веб-приложениях службы приложений Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

![Приложение Java, работающее в службе приложений Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание базы данных MySQL в Azure.
> * Подключение приложения toohello образца базы данных
> * Развертывание tooAzure приложения hello
> * Обновить и повторно развернуть приложение hello
> * Потоковая передача журналов диагностики из Azure.
> * Мониторинг приложения hello в hello портал Azure


## <a name="prerequisites"></a>Предварительные требования

1. [Скачайте и установите Git](https://git-scm.com/)
1. [Загрузите и установите hello Java 7 JDK или более поздней версии](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) (этот компонент потребуется запустить) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-local-mysql"></a>Подготовка локальной базы данных MySQL 

На этом шаге создания базы данных в локальный сервер MySQL для использования в проверочных приложение hello локально на компьютере.

### <a name="connect-toomysql-server"></a>Подключение сервера tooMySQL

В окне терминала подключение tooyour локального сервера MySQL. Можно использовать это окно терминала toorun hello команды в этом учебнике.

```bash
mysql -u root -p
```

Если появится запрос пароля, введите пароль hello для hello `root` учетной записи. Если вы не помните пароль корневой учетной записи, см. раздел [MySQL: как tooReset hello пароль учетной записи Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Если команда выполнена успешно, значит, сервер MySQL уже работает. Если это не так, убедитесь в том, локальному серверу MySQL запущен из следующих hello [действий после установки MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database"></a>Создание базы данных 

В hello `mysql` запрос, создайте базу данных и таблицу для hello заданий для выполнения.

```sql
CREATE DATABASE tododb;
```

Завершите подключение к серверу, введя команду `quit`.

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>Создание и выполнение примера приложения hello 

На этом шаге клонировать загрузки Spring пример приложения, задана база данных локальной MySQL toouse hello и запустите его на компьютере. 

### <a name="clone-hello-sample"></a>Образец hello клонирования

В окне терминала hello перейдите tooa работа каталога и клонирования репозитория образец hello. 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>Настройте базу данных MySQL hello toouse приложения hello

Обновление hello `spring.datasource.password` и значение в *spring-boot-mysql-todo/src/main/resources/application.properties* с hello же корневой пароль, используемый tooopen hello MySQL строки:

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>Построение и запуск образца hello

Построение и запуск образца hello, с помощью программы-оболочки Maven hello, включенных в репозитории hello:

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

Откройте ваш браузер toohttp://localhost:8080 toosee в образце hello в действии. Добавление toohello список задач, используйте следующие команды SQL, в hello MySQL prompt tooview hello данные, хранящиеся в MySQL hello.

```SQL
use testdb;
select * from todo_item;
```

Остановить приложение hello щелчком `Ctrl` + `C` в hello терминалов. 

## <a name="create-an-azure-mysql-database"></a>Создание базы данных MySQL в Azure

На этом шаге вы создадите [базы данных Azure для MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) экземпляра, используя hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli). Настройке toouse приложения образец hello эта база данных позднее в учебнике hello.

Используйте hello Azure CLI 2.0 в окно терминала toocreate hello ресурсы, необходимые toohost приложения Java в Azure службы приложений. Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям. 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание [группы ресурсов](../azure-resource-manager/resource-group-overview.md) с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure — это логический контейнер, в котором происходит развертывание и администрирование связанных ресурсов (веб-приложений, баз данных и учетных записей хранения). 

Hello следующий пример создает группу ресурсов в Северной Европе hello:

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

Возможные значения toosee hello можно использовать для `--location`, использовать hello [az appservice список расположений](/cli/azure/appservice#list-locations) команды.

### <a name="create-a-mysql-server"></a>Создание сервера MySQL

Создать сервер базы данных Azure для MySQL (Предварительная версия) с hello [создать сервер mysql az](/cli/azure/mysql/server#create) команды.    
Замените собственное уникальное имя сервера MySQL, показывающий hello `<mysql_server_name>` заполнителя. Это имя является частью имени узла сервера MySQL, `<mysql_server_name>.mysql.database.azure.com`, поэтому ему toobe глобально уникальным. Кроме того, замените `<admin_user>` и `<admin_password>` собственными значениями.

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

При создании сервера MySQL hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a>Настройка брандмауэра сервера

Создать правило брандмауэра для MySQL server tooallow клиентских соединений с помощью hello [az mysql правила брандмауэра для сервера — создание](/cli/azure/mysql/server/firewall-rule#create) команды. 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> База данных Azure для MySQL (предварительная версия) пока не поддерживает автоматическое подключение из служб Azure. Как динамически назначаются IP-адресов в Azure, это лучше tooenable все IP-адреса теперь. По мере его предварительной версии службы hello лучше методы защиты базы данных будет включено.

## <a name="configure-hello-azure-mysql-database"></a>Настройка базы данных MySQL в Azure hello

В окне терминала hello на компьютере подключение toohello MySQL server в Azure. Используйте значение hello, указанную ранее `<admin_user>` и `<mysql_server_name>`.

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>Создание базы данных 

В hello `mysql` запрос, создайте базу данных и таблицу для hello заданий для выполнения.

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>Создание пользователя с разрешениями

Создание пользователя базы данных и присвойте ему все привилегии в hello `tododb` базы данных. Замените заполнители hello `<Javaapp_user>` и `<Javaapp_password>` приложения уникальное имя.

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

Завершите подключение к серверу, введя команду `quit`.

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>Развертывание образца hello tooAzure службы приложений

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

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>Настройка базы данных Azure SQL hello toouse приложения hello

Перед запуском пример приложения hello, настройте параметры приложения на hello веб-приложения toouse hello Azure MySQL база данных, созданные в Azure. Эти свойства предоставляется toohello веб-приложение как переменные среды и переопределить hello значения, заданные в application.properties hello внутри hello упакованных веб-приложения. 

Задайте параметры приложения с помощью [az webapp конфигурации appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) в hello CLI:

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a>Получение учетных данных FTP для развертывания 
Вы можете развернуть appservice tooAzure вашего приложения различными способами, включая FTP, локальный Git, GitHub, Visual Studio Team Services и BitBucket. В этом примере FTP toodeploy hello. WAR-файла, созданного ранее на ваш локальный компьютер tooAzure службы приложений.

toodetermine, что учетные данные toopass вдоль в ftp команда toohello веб-приложения используйте [az appservice web развертывания списка публикации профили-](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) команды: 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a>Отправка приложения hello, с помощью протокола FTP

С помощью вашего любимого hello toodeploy средство FTP. Файл toohello WAR */site/wwwroot/webapps* папку на адрес сервера hello, взяты из hello `URL` в предыдущей команде hello. Удалите hello существующий каталог приложений по умолчанию (ROOT) и замените существующие ROOT.war с hello hello. WAR-файл, встроенной в hello ранее в учебнике hello.

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a>Веб-приложения hello теста

Обзор слишком`http://<app_name>.azurewebsites.net/` и добавьте список toohello несколько задач. 

![Приложение Java, работающее в службе приложений Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**Поздравляем!** Вы запустили управляемое данными приложение Java в службе приложений Azure.

## <a name="update-hello-app-and-redeploy"></a>Приложение hello обновления и повторного развертывания

Обновление приложения hello tooinclude дополнительный столбец в список todo hello для какой день hello элемент был создан. Spring загрузки обрабатывает обновление схемы базы данных hello как hello изменений модели данных без изменения существующей записи базы данных.

1. На локальном компьютере, откройте *src/main/java/com/example/fabrikam/TodoItem.java* и добавьте следующие hello импортирует toohello класса:   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. Добавить `String` свойство `timeCreated` слишком*src/main/java/com/example/fabrikam/TodoItem.java*, инициализирует его с отметкой времени создания объекта. Добавьте методы получения и задания для нового hello `timeCreated` свойство при редактировании этого файла.

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. Обновление *src/main/java/com/example/fabrikam/TodoDemoController.java* со строкой в hello `updateTodo` timestamp hello tooset метод:

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. Добавлена поддержка нового поля hello в шаблоне Thymeleaf hello. Обновление *src/main/resources/templates/index.html* с заголовком таблицы для отметки времени hello и новое значение поля toodisplay hello объекта hello timestamp в каждой строке таблицы данных.

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. Повторное построение приложения hello:

    ```bash
    mvnw clean package 
    ```

6. Обновить hello FTP. WAR как до, удалив существующие hello */wwwroot или веб-приложения или корневого КАТАЛОГА сайта* каталога и *ROOT.war*, то передача hello обновлены. WAR-файл как ROOT.war. 

При обновлении приложения hello **время создания** столбца является видимым. При добавлении новой задачи, приложение hello будет автоматически заполнять hello отметки времени. Существующие задачи остаются без изменений и работать с приложение hello, несмотря на то, что изменилось hello базовой модели данных. 

![Приложение Java, в которое добавлен новый столбец](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>Потоковая передача журналов диагностики 

Во время работы приложения Java в службе приложений Azure, можно получить консоли hello журналы по конвейеру непосредственно tooyour терминала. Таким образом, можно получить hello же диагностические сообщения toohelp отладке ошибок приложения.

Журнал toostart потоковой передачи, используйте hello [заключительного фрагмента журнала webapp az](/cli/azure/appservice/web/log#tail) команды.

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>Управление веб-приложением Azure

Go toohello hello Azure портала toosee веб-приложения, созданный.

toodo, вход слишком[https://portal.azure.com](https://portal.azure.com).

Hello в левом меню, щелкните **службы приложений**, затем щелкните имя hello Azure веб-приложения.

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-java-mysql/access-portal.png)

По умолчанию колонки веб-приложение отображает hello **Обзор** страницы. Здесь вы можете наблюдать за работой приложения. Вы также можете выполнять базовые задачи управления, например завершение, запуск, перезагрузку и удаление. Hello вкладках hello левой части колонки hello отображаются страницы hello другой конфигурации, которые можно открыть.

![Колонка службы приложений на портале Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

Эти закладки в колонке hello показывают hello множеством замечательных функций, можно добавить tooyour веб-приложения. После списка Hello предоставляет несколько возможностей hello:
* сопоставление настраиваемого DNS-имени;
* привязка настраиваемого SSL-сертификата;
* настройка непрерывного развертывания;
* вертикальное и горизонтальное масштабирование;
* добавление аутентификации пользователей.

## <a name="clean-up-resources"></a>Очистка ресурсов

Если эти ресурсы не требуется другой учебник (см. [дальнейшие действия](#next)), их можно удалить, выполнив следующую команду hello: 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="checklist"]
> * Создание базы данных MySQL в Azure.
> * Подключение toohello приложения Java образец MySQL
> * Развертывание tooAzure приложения hello
> * Обновить и повторно развернуть приложение hello
> * Потоковая передача журналов диагностики из Azure.
> * Управление приложение hello в hello портал Azure

Переместить следующий учебник toolearn toohello как toomap пользовательские DNS название toohello приложения.

> [!div class="nextstepaction"] 
> [Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений](app-service-web-tutorial-custom-domain.md)
