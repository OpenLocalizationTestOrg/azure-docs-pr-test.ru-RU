---
title: "aaaProvision и развернуть микрослужбами предсказуемо в Azure"
description: "Узнайте, как toodeploy приложения, состоящие из микрослужбами в службе приложений Azure как единое целое и предсказуемым образом с помощью JSON ресурсов группы шаблонов и сценариев PowerShell."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>Предсказуемые подготовка и развертывание микрослужб в Azure
В этом учебнике показано как tooprovision и развертывать приложения, состоящие из [микрослужбами](https://en.wikipedia.org/wiki/Microservices) в [службе приложений Azure](/services/app-service/) как единое целое и предсказуемым образом с помощью шаблонов группы ресурсов JSON и Создание скриптов PowerShell. 

При подготовке и развертывании приложения крупномасштабных, которые состоят из высокой изоляцией микрослужбами, повторяемости и предсказуемость являются ключевым toosuccess. [Служба приложений Azure](/services/app-service/) позволяет микрослужбами toocreate, в том числе веб-приложений, мобильных приложений, приложений API и логику приложения. [Диспетчер ресурсов Azure](../azure-resource-manager/resource-group-overview.md) позволяет вам toomanage все микрослужбами hello как единое целое, вместе с зависимости ресурсов, таких как базы данных и источник параметров управления. Теперь можно также развернуть такое приложение с помощью шаблонов JSON и простых скриптов PowerShell. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Выполняемая задача
В учебнике hello развертыванием приложения, которое содержит:

* два веб-приложения (т. е. две микрослужбы);
* базу данных SQL внутреннего сервера;
* параметры приложения, строки подключения и система управления версиями;
* анализы приложений, предупреждения, параметры автоматического масштабирования.

## <a name="tools-you-will-use"></a>Используемые инструменты
В этом учебнике будет использоваться hello следующие средства. Так как он не подробного обсуждения о средствах, я буду toostick toohello начала до конца сценария и просто назначьте tooeach Краткое введение и где можно найти дополнительные сведения о его. 

### <a name="azure-resource-manager-templates-json"></a>Шаблоны диспетчера ресурсов Azure (JSON)
Каждый раз при создании веб-приложения в службе приложений Azure, например, диспетчера ресурсов Azure использует группу JSON hello toocreate шаблона весь ресурс с hello ресурсов компонента. Сложные шаблоны из hello [Azure Marketplace](/marketplace) как hello [масштабируемой WordPress](/marketplace/partners/wordpress/scalablewordpress/) приложения могут включать hello базы данных MySQL, учетные записи хранения, hello план служб приложений, веб-приложения hello сам, правила оповещений, приложение параметры, параметры автоматического масштабирования и дополнительные и все эти шаблоны являются tooyou доступны через PowerShell. Сведения о toodownload и использовать эти шаблоны в статье [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](../powershell-azure-resource-manager.md).

Дополнительные сведения о шаблонах hello диспетчера ресурсов Azure см. в разделе [разработки шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>Пакет SDK для Azure 2.6 для Visual Studio
Hello новейшие SDK содержит улучшения toohello поддержка шаблонов диспетчера ресурсов в редакторе JSON hello. Можно использовать этот tooquickly создать шаблон группы ресурсов с нуля или открыть существующий шаблон JSON (например, шаблон загруженного галереи) для изменения заполнения файла параметров hello и даже развертывания группы ресурсов hello непосредственно из Azure Решения для группы ресурсов.

Дополнительные сведения см. в разделе [Пакет SDK для Azure версии 2.6 для Visual Studio](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/).

### <a name="azure-powershell-080-or-later"></a>Azure PowerShell 0.8.0 или более поздней версии
Начиная с версии 0.8.0 hello Установка Azure PowerShell включает модуль диспетчера ресурсов Azure hello сложения toohello модуль Azure. Этот новый модуль включает развертывания hello tooscript групп ресурсов.

Дополнительные сведения см. в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).

### <a name="azure-resource-explorer"></a>Обозреватель ресурсов Azure
Это [средство предварительного просмотра](https://resources.azure.com) позволяет tooexplore hello JSON определения всех групп ресурсов hello в подписке и hello отдельных ресурсов. В средстве hello можно изменять определения JSON hello ресурса, удаление всей иерархии ресурсов и создания новых ресурсов.  Hello сведения доступны в это средство служит для создания шаблона, поскольку она показывает, что свойства, необходимые tooset для определенного типа ресурса, hello исправьте значения и т. д. Можно даже создать группы ресурсов в hello [портала Azure](https://portal.azure.com/), затем проверьте его определения JSON в toohelp средство обозревателя hello templatize hello группы ресурсов.

### <a name="deploy-tooazure-button"></a>TooAzure кнопка "Развертывание"
Если вы используете GitHub для системы управления версиями, можно поместить [кнопку Развернуть tooAzure](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) в ваш файл README. MD обеспечивает tooAzure под ключ развертывания пользовательского интерфейса. Хотя это можно сделать для любой простой веб-приложения, можно расширить этот tooenable развертывание группы весь ресурс путем помещения файла azuredeploy.json в корень репозитория hello. Этот файл JSON, который содержит шаблон группы ресурсов hello, будет использоваться развертывание hello tooAzure toocreate кнопку hello группы ресурсов. Пример см. в разделе hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) пример, который будет использоваться в этом руководстве.

## <a name="get-hello-sample-resource-group-template"></a>Получить шаблон группы ресурсов образец hello
Теперь давайте tooit вправо.

1. Перейдите toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) образец приложения службы.
2. В файле readme.md, нажмите кнопку **развертывание tooAzure**.
3. Вы будете перенаправлены toohello [развертывание для azure](https://deploy.azure.com) сайта и задаваемые tooinput параметры развертывания. Обратите внимание, что большинство полей hello заполнены имя репозитория hello и некоторых случайных строк для вас. Все поля hello можно изменить, если требуется, но у вас есть tooenter единственное, что hello — это имя входа администратора SQL Server hello и hello пароль, а затем щелкните **Далее**.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. Далее щелкните **развернуть** процесс развертывания toostart hello. После выполнения процесса hello toocompletion щелкните hello http://todoapp*XXXX*. azurewebsites.net ссылку toobrowse hello развернутого приложения. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   Hello пользовательского интерфейса может быть несколько медленнее, если вы сначала просмотреть tooit, поскольку приложения hello просто запускается, но убедиться, что это полностью функциональное приложение.
5. Обратно hello развертывания на странице нажмите кнопку hello **управление** связать новое приложение hello toosee в hello портала Azure.
6. В hello **Essentials** раскрывающийся список, щелкните ссылку группы ресурсов hello. Примечание также веб-приложения hello уже подключен репозитории GitHub toohello под **внешнем проекте**. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. В колонке группы ресурсов hello Обратите внимание, что уже два веб-приложений и одной базы данных SQL в группе ресурсов hello.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

Все, что вы видели только через несколько минут на короткий приложении полностью развернутый двух микрослужбу со всеми компонентами hello, зависимости, параметры, базы данных и непрерывной публикации по задано автоматическое согласование диспетчера ресурсов Azure. Все это было проделано с помощью двух вещей:

* Кнопка tooAzure развернуть Hello
* azuredeploy.JSON в корне репозитория hello

Можно развернуть этот же приложение десятков, сотен или тысяч раз и точное же конфигурацию hello каждый раз. Hello повторяемости и hello предсказуемость такой подход позволяет toodeploy крупномасштабных приложений и без труда достоверности.

## <a name="examine-or-edit-azuredeployjson"></a>Изучение (или изменение) файла AZUREDEPLOY.JSON
Теперь давайте рассмотрим настроек репозитории GitHub hello. Вы будете использовать редактор JSON hello в hello Azure .NET SDK, поэтому если вы еще не установили [Azure .NET SDK 2.6](/downloads/), сделайте это сейчас.

1. Клон hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) репозитория с помощью средства избранные git. В приведенном далее снимке экрана приветствия я делаю это в Team Explorer в Visual Studio 2013 hello.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. Из корневой папки репозитория Привет откройте azuredeploy.json в Visual Studio. Если вы не видите панель hello структуры JSON, вы должны tooinstall Azure .NET SDK.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

Я меня не будет toodescribe все детали hello формат JSON, но hello [дополнительные ресурсы](#resources) разделе имеются ссылки для изучения языка шаблона группы ресурсов hello. Здесь я создаю tooshow hello интересных функций, которые помогут вам приступить к работе в принятии свой собственный пользовательский шаблон для развертывания приложения.

### <a name="parameters"></a>Параметры
Взгляните на toosee раздел параметров hello, большинство из этих параметров являются какие hello **развертывание tooAzure** кнопку предлагает tooinput. Hello сайта за hello **развертывание tooAzure** кнопку заполняет hello ввода пользовательского интерфейса с помощью hello параметры, определенные в azuredeploy.json. Эти параметры используются по всему hello определения ресурсов, таких как имена ресурсов, значения свойств и т. д.

### <a name="resources"></a>Ресурсы
Узел ресурсов «hello» вы увидите, что определены 4 ресурсы верхнего уровня, включая экземпляр SQL Server, план служб приложений и два веб-приложений. 

#### <a name="app-service-plan"></a>План службы приложений
Давайте начнем с простой на корневом уровне ресурс в hello JSON. В hello структуры JSON, нажмите кнопку с именем плана служб приложений hello **[hostingPlanName]** toohighlight hello соответствующий код JSON. 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

Обратите внимание, что hello `type` элемент указывает строку hello для плана службы приложений (он был вызван фермы серверов long, long давно), и другие элементы и свойства заполняются с использованием параметров hello, определенные в файле JSON hello не имеет этого ресурса любой вложенных ресурсов.

> [!NOTE]
> Обратите внимание, что значение hello `apiVersion` сообщает Azure версии hello API-интерфейса REST toouse hello JSON определения ресурса с и он может повлиять на способ форматирования hello ресурсов внутри hello `{}`. 
> 
> 

#### <a name="sql-server"></a>SQL Server
Нажмите кнопку с именем ресурса SQL Server hello **SQLServer** в hello структуры JSON.

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

Примечание hello, следуя о hello выделенный код JSON:

* Использование Hello параметров обеспечивает с именем и настроены так, чтобы их согласованность друг с другом hello создания ресурсов.
* Hello SQLServer ресурсов имеет два вложенных ресурсов, каждый из них имеет другое значение для `type`.
* Hello вложенных ресурсов в `“resources”: […]`, где определяются hello базы данных и правилами брандмауэра hello у `dependsOn` элемент, который задает идентификатор ресурса hello ресурсов SQLServer hello корневого уровня. Это значение определяет Azure Resource Manager «прежде чем создавать этот ресурс, на другой ресурс должен уже существует; и других ресурсов, определен в шаблоне hello, создайте такой сначала».
  
  > [!NOTE]
  > Подробные сведения о том, как toouse hello `resourceId()` см. в разделе [функции шаблона диспетчера ресурсов Azure](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid).
  > 
  > 
* Здравствуйте, эффект hello `dependsOn` элемент является, диспетчера ресурсов Azure можно узнать, какие ресурсы могут быть созданы в параллельном режиме и какие ресурсы должны быть созданы последовательно. 

#### <a name="web-app"></a>Веб-приложение
Теперь перейдем toohello фактическое веб-приложения самостоятельно, которые являются более сложным. Щелкните веб-приложения hello [variables('apiSiteName')] в toohighlight структуры JSON hello его код JSON. Теперь вы увидите гораздо более интересные вещи. Для этой цели мы поговорим о возможностях hello по одному:

##### <a name="root-resource"></a>Корневой ресурс
веб-приложения Hello зависит от двух разных ресурсов. Это означает, что диспетчера ресурсов Azure создаст hello веб-приложения только после обоих hello создания плана служб приложений и hello экземпляр SQL Server.

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>Параметры приложения
Параметры приложения Hello также определены как вложенных ресурсов.

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

В hello `properties` элемент для `config/appsettings`, у вас есть два параметра приложения в формате hello `“<name>” : “<value>”`.

* `PROJECT`— [KUDU параметр](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) сообщающее развертывания Azure какие toouse проекта в решении несколько проектов Visual Studio. Я расскажу позже, как настроить систему управления версиями, но поскольку hello ToDoApp кода в решении несколько проектов Visual Studio, необходимо, чтобы этот параметр.
* `clientUrl`— просто задание, код приложения hello приложение использует.

##### <a name="connection-strings"></a>Строки подключения
строки подключения Hello также определены как вложенных ресурсов.

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

В hello `properties` элемент для `config/connectionstrings`, каждая строка подключения также определяется как пара имя-значение с hello специальный формат `“<name>” : {“value”: “…”, “type”: “…”}`. Для hello `type` элемент, возможные значения: `MySql`, `SQLServer`, `SQLAzure`, и `Custom`.

> [!TIP]
> Определенный список типов подключения строку hello, запустите следующую команду в Azure PowerShell hello: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>Система управления версиями
параметры системы управления версиями Hello также определены как вложенных ресурсов. Диспетчер ресурсов Azure использует этот ресурс tooconfigure непрерывной публикации (см. Примечание `IsManualIntegration` более поздней версии) и также tookick off hello развертывание кода приложения автоматически во время обработки hello hello JSON-файла.

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`и `branch` должно быть интуитивно и должен указывать toohello Git репозитория и hello имя toopublish hello ветвь из. Опять же, они определяются входными параметрами. 

Примечание в hello `dependsOn` элемент, который в toohello Добавление веб-приложения ресурс, `sourcecontrols/web` также зависит от `config/appsettings` и `config/connectionstrings`. Это, поскольку после `sourcecontrols/web` является настройки hello процесса развертывания Azure автоматически предпримет toodeploy, сборка и запуск кода приложения hello. Таким образом Вставка Эта зависимость поможет убедиться, что вы это приложение hello имеет доступ toohello необходимые приложения и строки подключения перед выполнением кода приложения hello. 

> [!NOTE]
> Обратите внимание, что `IsManualIntegration` задано слишком`true`. Это свойство является необходимым в этом учебнике, поскольку фактически не владеет репозитории GitHub hello и таким образом не может предоставить фактически разрешение tooAzure tooconfigure непрерывной публикации из [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (т. е. Принудительная автоматическая репозиторий tooAzure обновления). Можно использовать значение по умолчанию hello `false` для hello в указанном репозитории только в том случае, если вы настроили учетные данные GitHub hello владельца hello [портал Azure](https://portal.azure.com/) до. Другими словами Если вы настроили tooGitHub управления источника или BitBucket для любого приложения в hello [портала Azure](https://portal.azure.com/) ранее, с помощью пользователя учетные данные, то Azure будет запоминать учетные данные hello и использовать их при развертывании из любого приложения GitHub или BitBucket в будущем hello. Тем не менее если вы еще не сделали это, произойдет сбой развертывания шаблона JSON hello, когда диспетчера ресурсов Azure пытается параметры системы управления версиями tooconfigure hello веб-приложения, так как он не может входить в GitHub или BitBucket с учетными данными владельца репозитория hello.
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>Сравнение hello шаблона JSON с группой ресурсов, развернутых
Здесь вы можете пройти все hello веб-приложения колонок в hello [портала Azure](https://portal.azure.com/), но есть другое средство, не только как полезны, если несколько. Go toohello [обозревателя ресурсов Azure](https://resources.azure.com) средства предварительного просмотра, которое предоставляет JSON-представление всех групп ресурсов hello в ваших подписок, поскольку они фактически существуют в hello Azure серверной части. Можно узнать, как группа ресурсов hello иерархии JSON в Azure соответствует иерархии hello в файле шаблона hello, которое использовалось toocreate его.

Например, если перейти toohello [обозревателя ресурсов Azure](https://resources.azure.com) инструмент и разверните узлы hello в обозревателе hello, отображаются группы ресурсов hello и ресурсы hello корневого уровня, которые собираются в типам соответствующих ресурсов.

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

Если детализация углублением tooa веб-приложение, должен быть может toosee web app конфигурации сведения аналогичные toohello приведенном ниже снимке экрана:

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

Еще раз hello вложенных ресурсов должно toothose схожий иерархии в файле шаблона JSON, и вы увидите параметры приложения hello, строки подключения, т. д., правильно отражаются в области hello JSON. отсутствие Hello здесь параметров может указывать на проблему с JSON-файла и могут помочь устранить файла шаблона JSON.

## <a name="deploy-hello-resource-group-template-yourself"></a>Развернуть шаблон группы ресурсов hello вручную
Hello **развертывание tooAzure** кнопку отлично, но с ее помощью можно шаблон группы ресурсов toodeploy hello в azuredeploy.json только в том случае, если вы уже принудительно отправлены azuredeploy.json tooGitHub. Hello Azure .NET SDK также предоставляет средства hello вы toodeploy любой файл шаблона JSON непосредственно с локального компьютера. toodo это, выполните hello шаги:

1. В Visual Studio выберите **Файл** > **Создать** > **Проект**.
2. Выберите **Visual C#** > **Облако** > **Группа ресурсов Azure**, а затем нажмите кнопку **ОК**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. В разделе **Выберите шаблон Azure** выберите **Пустой шаблон** и нажмите кнопку **ОК**.
4. Перетащите в hello azuredeploy.json **шаблона** папку нового проекта.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. В обозревателе решений откройте azuredeploy.json hello копируются.
6. Только ради hello демонстрации hello, добавим некоторые стандартные Application Insight ресурсы tooour JSON-файл, нажав **добавить ресурс**. Если вас интересует только развертывание hello JSON-файл, пропустите шаги развертывания toohello.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. Выберите **Application Insights для веб-приложений**, убедитесь, что выбран существующий план службы приложений и выбрано веб-приложение, а затем нажмите кнопку **Добавить**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   Вам потребуется выполнить теперь быть может toosee несколько новых ресурсов, в зависимости от ресурсов hello и действие, имеют зависимости от либо hello службы приложений плана или hello веб-приложения. Эти ресурсы по их существующее определение не включены, и вы собираетесь toochange.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. В hello структуры JSON, щелкните **appInsights автомасштабирования** toohighlight его код JSON. Это hello масштабирование параметр для плана служб приложений.
9. В hello выделенный код JSON, найдите hello `location` и `enabled` свойства и укажите их, как показано ниже.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. В hello структуры JSON, щелкните **CPUHigh appInsights** toohighlight его код JSON. Это предупреждение.
11. Найдите hello `location` и `isEnabled` свойства и укажите их, как показано ниже. Hello одинаково для hello других трех оповещений (фиолетовый лампочки).
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. Теперь вы готовы toodeploy. Щелкните правой кнопкой мыши проект hello и выберите **развернуть** > **новое развертывание**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. Войдите в свою учетную запись Azure, если вы еще этого не сделали.
14. Выберите существующую группу ресурсов в подписке или создайте новую. Выберите файл **azuredeploy.json**, а затем нажмите кнопку **Изменить параметры**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    Теперь вы сможете может tooedit все параметры hello определены в файле шаблона hello в таблицу с низким приоритетом. Параметры, определяющие значения по умолчанию, уже будут иметь значения по умолчанию, а параметры, определяющие список допустимых значений, будут отображаться в виде раскрывающихся списков.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. Заполните все параметры пустой hello и использовать hello [адрес репозитория GitHub ToDoApp](https://github.com/azure-appservice-samples/ToDoApp.git) в **repoUrl**. Нажмите кнопку **Сохранить**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > Автоматическое масштабирование — функция, предлагаемая в **Стандартная** уровня или более поздней версии и уровне плана оповещения, возможности, предлагаемые **основные** категорию или более поздней версии, вам потребуется tooset hello **sku** параметр слишком**Стандартная** или **Premium** чтобы toosee все новые подробные сведения о приложении ресурсы подсветка.
    > 
    > 
16. Щелкните **Развернуть**. Если вы выбрали **сохранить пароли**, hello пароль будет сохранен в файл параметров hello **в виде обычного текста**. В противном случае запрашивается пароль базы данных hello tooinput во время развертывания hello.

Это все! Теперь необходимо просто toogo toohello [портала Azure](https://portal.azure.com/) и hello [обозревателя ресурсов Azure](https://resources.azure.com) toosee средство hello новые предупреждения и добавлены параметры автоматического масштабирования tooyour JSON развернутого приложения.

Действия, описанные в этом основном выполняются hello следующее:

1. Файл шаблона подготовленного hello
2. Создан файл параметров toogo с использованием файла шаблона hello
3. Файл шаблона развернутое приложение hello, а параметр hello

Последний этап Hello легко выполняется с помощью командлета PowerShell. toosee что сделал Visual Studio при его развертывании вашего приложения, откройте Scripts\Deploy-AzureResourceGroup.ps1. Имеется большой объем кода существует, но я создаю toohighlight все нужные кода hello требуется файл шаблона hello toodeploy с файлом параметр hello.

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

Здравствуйте, последний командлет `New-AzureResourceGroup`, — hello, который фактически выполняет действие hello. После этого следует демонстрации tooyou, что, с помощью средства hello, это относительно простой toodeploy вашей предсказуемо облачных приложений. При каждом запуске командлета hello на hello того же шаблона с hello же файл параметров, которые планируется tooget hello того же результата.

## <a name="summary"></a>Сводка
В DevOps повторяемости и предсказуемость являются ключи tooany успешного развертывания крупномасштабных приложений, состоящие из микрослужбами. В этом учебнике вы развернули tooAzure микрослужбу два приложения в качестве единой группы ресурсов с помощью шаблона Azure Resource Manager hello. Надеюсь, он предоставил вам hello базы знаний, необходимых в порядке toostart преобразования приложения в Azure в шаблон и можно подготовить и развернуть его предсказуемо. 

## <a name="next-steps"></a>Дальнейшие действия
Узнайте, как слишком[применить гибкие методологии и постоянно опубликовать приложение микрослужбами с легкостью](app-service-agile-software-development.md) и дополнительные методы развертывания как [проекте, которая должна развертывания](app-service-web-test-in-production-controlled-test-flight.md) легко.

<a name="resources"></a>

## <a name="more-resources"></a>Дополнительные ресурсы
* [Язык шаблонов в диспетчере ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Функции шаблонов в диспетчере ресурсов Azure](../azure-resource-manager/resource-group-template-functions.md)
* [Развертывание приложения с использованием шаблона диспетчера ресурсов Azure](../azure-resource-manager/resource-group-template-deploy.md)
* [Использование Azure PowerShell с диспетчером ресурсов Azure](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Устранение неполадок при развертывании групп ресурсов в Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md)

