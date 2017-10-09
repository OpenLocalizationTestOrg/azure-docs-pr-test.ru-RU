---
title: "проекты группы ресурсов Studio Azure aaaVisual | Документы Microsoft"
description: "Использование Visual Studio toocreate проекта группы ресурсов Azure и развертывания ресурсов tooAzure hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Создание и развертывание групп ресурсов Azure с помощью Visual Studio
С помощью Visual Studio и hello [пакета Azure SDK](https://azure.microsoft.com/downloads/), можно создать проект, который развертывает tooAzure вашей инфраструктуры и кода. Например можно определить hello веб-узел, веб-сайта и базы данных для приложения, а также развернуть этой инфраструктуры, а также кода hello. Или можно определить виртуальную машину, виртуальную сеть и учетную запись хранилища, а затем развернуть эту инфраструктуру со сценарием, который выполняется на виртуальной машине. Hello **группы ресурсов Azure** проект развертывания позволяет вам toodeploy все hello необходимые ресурсы в один repeatable операцией. Подробнее о развертывании ресурсов и управлении ими см. в разделе [Общие сведения о диспетчере ресурсов Azure](resource-group-overview.md).

Проекты группы ресурсов Azure содержат шаблоны JSON диспетчера ресурсов Azure, которые определяют ресурсы hello развертывания tooAzure. toolearn об элементах hello hello шаблона диспетчера ресурсов, в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md). Visual Studio позволяет вам tooedit эти шаблоны, а также предоставляет средства, которые упрощают работу с шаблонами.

В этой статье показано, как развернуть веб-приложение и базу данных SQL. Однако hello действия являются почти hello же для каждого типа ресурса. С такой же легкостью можно развернуть виртуальную машину и связанные с ней ресурсы. Visual Studio предоставляет разные начальные шаблоны для распространенных сценариев развертывания.

В этой статье используется Visual Studio 2017. Если используется Visual Studio 2015 с обновлением 2 и Microsoft Azure SDK .NET 2.9 или Visual Studio 2013 с Azure SDK 2.9 работу, в значительной степени hello таким же. Можно использовать версии hello Azure SDK 2.6 или более поздняя версия; Однако продуктивной работе hello пользовательского интерфейса может отличаться от hello пользовательский интерфейс, приведенными в этой статье. Настоятельно рекомендуется установить последнюю версию hello hello [пакета Azure SDK](https://azure.microsoft.com/downloads/) перед началом действия hello. 

## <a name="create-azure-resource-group-project"></a>Создание проекта группы ресурсов Azure
В этой процедуре мы создадим проект группы ресурсов Azure с помощью шаблона **Веб-приложение + SQL** .

1. В Visual Studio последовательно выберите **Файл**, **Создать проект**, а затем — **C#** или **Visual Basic**. Щелкните **Облако** и выберите проект **Группа ресурсов Azure**.
   
    ![Проект облачного развертывания](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Выбор шаблона hello, которые должны toodeploy tooAzure диспетчера ресурсов. Обратите внимание, существует много различных вариантов в зависимости от hello типа проекта следует toodeploy. Для данной статьи выберите hello **веб-приложение + SQL** шаблона.
   
    ![Выберите шаблон](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    шаблон Hello выбираемое является просто отправной точкой; Вы можно добавлять и удалять ресурсы toofulfill вашего сценария.
   
   > [!NOTE]
   > Visual Studio получает список доступных шаблонов в Интернете. Hello список может измениться.
   > 
   > 
   
    Visual Studio создает проект развертывания группы ресурсов для hello веб-приложения и базы данных SQL.
3. toosee то, что вы создали, поиск на узле hello в проекте развертывания hello.
   
    ![Показать узлы](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    Поскольку мы выбрали hello веб-приложение + шаблон SQL для этого примера, вы видите hello следующие файлы: 
   
   | Имя файла | Описание |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |Сценарий PowerShell, который вызывает tooAzure toodeploy команды PowerShell диспетчера ресурсов.<br />**Примечание** Visual Studio использует этот toodeploy сценария PowerShell шаблон. Можно производить любые изменения сценария toothis влияет на развертывание в Visual Studio, поэтому будьте внимательны. |
   | WebSiteSQLDatabase.json |Hello шаблон диспетчера ресурсов, который определяет hello инфраструктуры, который требуется развернуть tooAzure и hello параметры, которые можно указать во время развертывания. Он также определяет hello зависимости между ресурсами hello, диспетчер ресурсов развертывает ресурсы hello в правильном порядке hello. |
   | WebSiteSQLDatabase.parameters.json |Файл параметров, содержащий значения, необходимые hello шаблона. Передать параметр toocustomize значения каждого развертывания. |
   
    Все проекты развертывания группы ресурсов содержат эти основные файлы. Другие проекты могут содержать дополнительные файлы toosupport другие функциональные возможности.

## <a name="customize-hello-resource-manager-template"></a>Настройка шаблона диспетчера ресурсов hello
Проект развертывания можно настроить путем изменения шаблонов hello JSON, описывающих hello ресурсов, toodeploy. JSON расшифровывается как JavaScript Object Notation и является форматом сериализованных данных, просто toowork с. Hello JSON-файлы используют схему, на которую ссылается hello верхней части каждого файла. Если нужно toounderstand hello схему, можно загрузить и проанализировать его. Hello схема определяет какие элементы являются допустимыми, hello типы и форматы полей, hello возможные значения перечисляемых значений и т. д. toolearn об элементах hello hello шаблона диспетчера ресурсов, в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).

Откройте toowork в шаблоне, **WebSiteSQLDatabase.json**.

Hello Visual Studio, редактор предоставляет средства tooassist можно с помощью редактирования hello шаблона диспетчера ресурсов. Hello **структуры JSON** окно позволяет легко toosee hello элементов, определенных в шаблоне.

![Показать структуру JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

При выборе любого из элементов hello в структуре hello осуществляется toothat частью шаблона hello и выделяет hello соответствующий JSON.

![Перейти к JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

Для добавления ресурса необходимо либо выбрав hello **добавить ресурс** кнопку вверху hello окно структуры JSON hello, или щелкните правой кнопкой мыши **ресурсов** и выбрав **добавить новый ресурс**.

![Добавить ресурсы](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

Для этого примера выберите пункт **Учетная запись хранения** и присвойте этой учетной записи имя. Имя учетной записи хранения должно содержать только цифры и строчные буквы, а длина не должна превышать 11 символов.

![Добавить хранилище](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

Обратите внимание, не только был добавлен hello ресурсов, но также является параметром для hello введите учетную запись хранения и переменную для названия hello hello учетной записи хранения.

![Показать структуру](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

Hello **storageType** параметр предварительно определенных разрешенных типов и тип по умолчанию. Вы можете использовать эти значения или изменить их для своего сценария. Если другие пользователи не могли toodeploy **Premium_LRS** учетной записи хранения при помощи этого шаблона, удалите его из hello допустимые типы. 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

Visual Studio также позволяет понять, какие свойства toohelp intellisense доступны при редактировании шаблона hello. Например, свойства hello tooedit для плана служб приложений перейдите toohello **HostingPlan** ресурсов и добавить значение для hello **свойства**. Обратите внимание, что intellisense показывает доступные значения hello, а также приводится описание этого значения.

![Показать Intellisense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

Можно задать **numberOfWorkers** too1.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>Развертывание проекта tooAzure hello группы ресурсов
Вы являются теперь готовы toodeploy проекта. При развертывании проекта группы ресурсов Azure развертывается tooan группы ресурсов Azure. Группа ресурсов Hello находится логической группировки ресурсов, которые совместно используют общий жизненный цикл.

1. В контекстном меню узла проекта развертывания hello hello, выберите **развернуть** > **New**.
   
    ![Пункт меню "Развертывание", "Новое развертывание"](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    Hello **развертывание tooResource группы** откроется диалоговое окно.
   
    ![Развертывание tooResource диалоговое окно «группа»](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. В hello **группы ресурсов** раскрывающемся списке выберите существующую группу ресурсов или создайте новую. toocreate группу ресурсов, откройте hello **группы ресурсов** раскрывающийся список и выберите **создать новый**.
   
    ![Развертывание tooResource диалоговое окно «группа»](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    Hello **Создание группы ресурсов** откроется диалоговое окно. Присвойте группе имя и расположение, а затем выберите hello **создать** кнопки.
   
    ![Диалоговое окно "Создание группы ресурсов"](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. Изменить параметры hello hello развертывания, выбрав hello **изменение параметров** кнопки.
   
    ![Кнопка "Изменить параметры"](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Укажите значения для параметров пустой hello и выберите hello **Сохранить** кнопки. пустые параметры Hello **hostingPlanName**, **Имя_входа_администратора**, **administratorLoginPassword**, и **databaseName**.
   
    **hostingPlanName** указывает имя для hello [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate. 
   
    **Имя_входа_администратора** указывает имя пользователя hello Здравствуйте, администратор SQL Server. Не используйте общие имена администраторов, такие как **sa** или **admin**. 
   
    Hello **administratorLoginPassword** указывает пароль для администратора SQL Server. Hello **хранить пароли в виде обычного текста в файле параметров hello** параметр не является безопасный; таким образом, этот параметр не выбран. Так как hello пароль не сохраняется как обычный текст, необходимы tooprovide этот пароль еще раз во время развертывания. 
   
    **Имя базы данных** указывает имя базы данных toocreate hello. 
   
    ![Диалоговое окно "Изменение параметров"](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Выберите hello **развернуть** tooAzure проекта hello toodeploy кнопки. За пределами экземпляра Visual Studio hello открывает консоль Windows PowerShell. Введите пароль администратора SQL Server hello в консоли PowerShell hello при появлении запроса. **Консоль PowerShell может скрыта от других элементов, или свернуто в панели задач hello.** Найдите эту консоль и выберите его tooprovide hello пароль.
   
   > [!NOTE]
   > Visual Studio может попросить вас tooinstall hello командлетов Azure PowerShell. Требуется hello Azure PowerShell командлеты toosuccessfully развертывания группы ресурсов. При появлении запроса установите их.
   > 
   > 
6. Hello развертывания может занять несколько минут. В hello **вывода** windows, отображается статус hello hello развертывания. По завершении развертывания hello последнее сообщение hello указывает успешное развертывание с примерно:
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. Откройте в браузере, hello [портал Azure](https://portal.azure.com/) и tooyour учетная запись для входа. toosee hello группы ресурсов, выберите **групп ресурсов** и развертывании группы ресурсов hello.
   
    ![Выбрать группу](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. Можно просмотреть все ресурсы развернуты hello. Обратите внимание, что hello имя hello учетной записи хранилища не только теми, которые указаны при добавлении этого ресурса. Hello учетной записи хранения должно быть уникальным. Hello шаблон автоматически добавляет строку символов имени toohello введенным tooprovide уникальное имя. 
   
    ![Показать ресурсы](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. Если внести изменения и требуется tooredeploy проекта, выберите существующую группу ресурсов hello hello контекстном меню проекта группы ресурсов Azure. Hello контекстном меню, выберите **развернуть**, а затем выберите группу ресурсов hello был развернут.
   
    ![Развернутая группа ресурсов Azure](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>Развертывание кода с определенной инфраструктурой
На этом этапе вы развернули hello инфраструктуры для вашего приложения, но нет фактических кода, развернутых с помощью проекта hello. В этой статье показано, как toodeploy веб-приложения и базы данных SQL таблицы во время развертывания. При развертывании виртуальной машины, а не веб-приложения toorun требуется некоторый код на компьютере hello в ходе развертывания. Здравствуйте, процесс развертывания кода для веб-приложения или для настройки виртуальной машины является практически hello таким же.

1. Добавьте проект tooyour решения Visual Studio. Щелкните правой кнопкой мыши решение hello и выберите **добавить** > **новый проект**.
   
    ![Добавить проект](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. Добавьте **веб-приложение ASP.NET**. 
   
    ![Добавить веб-приложение](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. Выберите **MVC**.
   
    ![Выбрать MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. После Visual Studio создает веб-приложение, вы увидите обоих проектов в решении hello.
   
    ![Показать проекты](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. Теперь требуется toomake том, что проект группы ресурсов учитывает hello новый проект. Вы можете вернуться проекта группы ресурсов tooyour (AzureResourceGroup1). Щелкните правой кнопкой мыши **Ссылки** и выберите **Добавить ссылку**.
   
    ![Добавить ссылку](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. Выберите проект веб-приложения hello, созданный вами.
   
    ![Добавить ссылку](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    Добавив ссылку, связать hello проекта приложения web toohello проекта группы ресурсов и автоматически устанавливается три ключевых свойств. Можно просмотреть эти свойства в hello **свойства** окна для hello ссылки.
   
      ![Просмотреть ссылку](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    Существуют следующие свойства Hello
   
   * Hello **дополнительные свойства** содержит пакет веб-развертывания hello промежуточное расположение, отправляемое toohello хранилища Azure. Обратите внимание, hello папку (ExampleApp) и файл (package.zip). Необходимо tooknow эти значения так, как указать, как приложение hello параметров при развертывании. 
   * Hello **включать путь к файлу** содержит hello путь, где создается пакет hello. Hello **целевые объекты включают** содержит hello команду, которая выполняет развертывание. 
   * значение по умолчанию Hello **сборки; Пакет** включает hello toobuild развертывания и создайте пакет веб-развертывания (package.zip).  
     
     Профиль публикации не обязательно как hello развертывания получает hello необходимые сведения из toocreate hello hello свойств пакета.
7. TooWebSiteSQLDatabase.json вернуться назад и добавить шаблон toohello ресурсов.
   
    ![Добавить ресурсы](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. На этот раз выберите **Веб-развертывание для веб-приложений**. 
   
    ![Добавить веб-развертывание](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. Повторное развертывание группы ресурсов toohello проекта группы ресурсов. В этом случае будут использоваться некоторые новые параметры. Нет необходимости tooprovide значения для **_artifactsLocation** или **_artifactsLocationSasToken** так, как Visual Studio автоматически создает эти значения. Тем не менее, у вас есть tooset hello папки и путь toohello имя файла, содержащего пакет развертывания hello (показано как **ExampleAppPackageFolder** и **ExampleAppPackageFileName** в hello после изображения ). Укажите значения hello было показано ранее в hello свойства ссылки (**ExampleApp** и **package.zip**).
   
    ![Добавить веб-развертывание](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Для hello **учетной записи хранилища артефактов**, выберите hello, одна развернута в этой группе ресурсов.
10. После завершения развертывания hello, выберите веб-приложения на портале hello. Выберите toobrowse toohello hello URL-адрес сайта.
    
     ![Перейти на сайт](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. Обратите внимание, что приложение ASP.NET по умолчанию hello успешно развернут.
    
     ![Показать развернутое приложение](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>Дальнейшие действия
* toolearn об управлении ресурсам через портал hello. в разделе [использование hello Azure портала toomanage ресурсам Azure](resource-group-portal.md).
* toolearn Дополнительные сведения о шаблонах, в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).

