---
title: "aaaCreate, сборка и развертывание приложений логики в Visual Studio — приложения логики Azure | Документы Microsoft"
description: "Узнайте, как создавать проекты Visual Studio для проектирования, создания и развертывания приложений логики с помощью Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>Проектирование, создание и развертывание приложений логики Azure в Visual Studio

Несмотря на то что hello [портал Azure](https://portal.azure.com/) предлагает отличный способ для вас toocreate и управлять приложения логики Azure, можно использовать Visual Studio для проектирования, создания и развертывания приложений логики. Visual Studio предоставляет широкие возможности средств, таких как hello конструктор логику приложения для вас toocreate логику приложения и настроить шаблоны развертывания и автоматизации развертывания tooany среды. 

tooget работы с приложениями логики Azure, узнайте [как toocreate своего первого приложения логики в hello портал Azure](logic-apps-create-a-logic-app.md).

## <a name="installation-steps"></a>Шаги установки

tooinstall и настройка средств Visual Studio для приложения логики Azure, выполните следующие действия.

### <a name="prerequisites"></a>Предварительные требования

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) или Visual Studio 2015.
* [пакет Azure SDK последней версии](https://azure.microsoft.com/downloads/) (версия 2.9.1 или выше);
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* Web toohello доступ при использовании конструктора внедренные hello

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>Установка средств Visual Studio для Azure Logic Apps

После установки необходимых компонентов hello:

1. Откройте Visual Studio. На hello **средства** последовательно выберите пункты **расширения и обновления**.
2. Разверните hello **Online** категории, можно найти в Интернете.
3. Найдите **средства Azure Logic Apps Tools для Visual Studio**. Если потребуется, выполните поиск по названию **Logic Apps**.
4. toodownload и расширение hello установки, нажмите кнопку **загрузить**.
5. После установки перезапустите Visual Studio.

> [!NOTE]
> Можно также загрузить [инструментов приложения логики Azure для Visual Studio 2017 г](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) и hello [инструментов приложения логики Azure для Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) непосредственно из Visual Studio Marketplace hello.

После завершения установки можно использовать hello проекта группы ресурсов Azure с помощью конструктора логики приложения.

## <a name="create-your-project"></a>Создание проекта

1. На hello **файл** меню перейдите слишком**New**и выберите **проекта**. Или tooadd tooan вашего проекта, существующие решения go слишком**добавить**и выберите **новый проект**.

    ![Меню «Файл»](./media/logic-apps-deploy-from-vs/filemenu.png)

2. В hello **новый проект** окна, найдите **облака**и выберите **группы ресурсов Azure**. Присвойте проекту имя и нажмите кнопку **ОК**.

    ![Добавление нового проекта](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. Выберите hello **приложения логики** шаблона, который создает шаблон развертывания приложения пустое логику для вас toouse. Выбрав нужный шаблон, нажмите **ОК**.

    ![Выбор шаблона Logic App](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    Теперь вы добавили решения tooyour логику приложения проекта. 
    В hello обозреватель решений файл развертывания должен отображаться.

    ![Файл развертывания](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>Создание приложения логики с помощью конструктора приложений логики

При наличии проекта группы ресурсов Azure, содержащий приложение логики, можно открыть конструктор логику приложения hello в Visual Studio toocreate рабочего процесса. 

> [!NOTE]
> Конструктор Hello требуется подключение к Интернету запроса слишком соединители для доступных свойств и данных. Например при использовании соединитель Dynamics CRM Online hello hello конструктор запрашивает настраиваемый доступных tooshow экземпляра CRM и свойства по умолчанию.

1. Щелкните правой кнопкой мыши файл `<template>.json` и выберите пункт **Открыть в конструкторе Logic App**. (`Ctrl+L`)

2. Выберите подписку Azure, группу ресурсов и расположение шаблона развертывания.

    > [!NOTE]
    > При проектировании приложения логики будут создаваться ресурсы для подключения к API, которые используются для получения свойств. Visual Studio использует эти подключения вашей toocreate группы выбранного ресурса во время разработки. tooview или изменить любые соединения API, перейти toohello портал Azure и поиск **подключений API**.

    ![Средство выбора подписки](./media/logic-apps-deploy-from-vs/designer_picker.png)

    Конструктор Hello использует определения hello в hello `<template>.json` файл для подготовки к просмотру.

4. Создайте и подготовьте приложение логики. Шаблон развертывания обновляется в соответствии со всеми вносимыми изменениями.

    ![Конструктор Logic App в Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

Visual Studio добавляет `Microsoft.Web/connections` слишком ресурс файла ресурсов для любых соединений логику приложению toofunction. Эти свойства соединения можно задавать при развертывании и управлять после развертывания в **подключений API** в hello портал Azure.

### <a name="switch-toojson-code-view"></a>Переключение tooJSON в представлении кода

hello tooshow JSON-представление для логики приложения, выберите hello **в представлении кода** вкладку внизу hello hello конструктора.

tooswitch обратно toohello ресурсов JSON, щелкните правой кнопкой мыши hello `<template>.json` правой кнопкой мыши и выберите **откройте**.

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>Добавьте ссылки на зависимые ресурсы tooVisual Studio развертывания шаблонов

При необходимости вашего приложения логики tooreference зависимые ресурсы, можно использовать [функции шаблона Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) в шаблон развертывания логику приложения. Например может потребоваться вашей tooreference приложения логики Azure функции или интеграции учетной записью, которую toodeploy вместе с логикой приложения. Необходимо помнить о подготовке правильно toouse параметры в шаблон развертывания, который hello конструктор логику приложения. 

Параметры приложений логики можно использовать в следующих типах триггеров и действий.

*   Дочерний рабочий процесс
*   Приложение-функция
*   Вызов APIM
*   URL-адрес API среды выполнения
*   Путь для подключения к API.

Вы также можете использовать функции шаблонов: parameters, variables, resourceId, concat и т. п. Например Вот как можно заменить идентификатор ресурса Azure функции hello.

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

А так вы можете использовать параметры:

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
В качестве другого примера можно параметризовать hello сообщение операции отправки служебной шины:

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> Параметр host.runtimeUrl является необязательным, его можно удалить из шаблона.
> 


> [!NOTE] 
> Для toowork конструктор логику приложения hello при использовании параметров, необходимо предоставить значения по умолчанию, например:
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>Сохранение приложения логики

go логику приложения в любое время, toosave слишком**файл** > **Сохранить**. (`Ctrl+S`) 

Если логика приложения все ошибки при сохранении свое приложение, они отображаются в Visual Studio hello **выходов** окна.

## <a name="deploy-your-logic-app-from-visual-studio"></a>Развертывание приложения логики из Visual Studio

Когда настройка приложения логики будет завершена, вы можете развернуть его, выполнив несколько простых действий напрямую из Visual Studio. 

1. В обозревателе решений щелкните правой кнопкой мыши проект и перейдите в слишком**развернуть** > **новое развертывание...**

    ![Новое развертывание](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. Если появится запрос, может входить в tooyour подписки Azure. 

3. Теперь необходимо выбрать hello сведений для группы ресурсов hello место toodeploy логику приложения. Закончив, щелкните **Развернуть**.

    > [!NOTE]
    > Убедитесь, что выбран правильный шаблон hello и файл параметров для группы ресурсов hello. Например toodeploy tooa рабочей среде следует выберите файл параметров рабочей hello.

    ![Развертывание группы tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    отображается состояние развертывания Hello hello **вывода** окна. 
    Возможно, tooselect **подготовки Azure** в hello **Показать выходные данные от** списка.

    ![Вывод информации о состоянии развертывания](./media/logic-apps-deploy-from-vs/output.png)

В будущем hello можно изменить логику приложения в системе управления версиями и использовать Visual Studio toodeploy новых версий.

> [!NOTE]
> Если непосредственно изменить определение hello в hello портал Azure, эти изменения будут перезаписаны при развертывании из Visual Studio следующий раз. 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>Добавьте существующий проект группы ресурсов логику приложения tooan

При наличии существующего проекта группы ресурсов, можно добавить в окне структуры JSON hello проекта toothat логику приложения. Можно также добавить другое приложение логики, наряду с приложение hello, созданного ранее.

1. Откройте hello `<template>.json` файла.

2. hello tooopen окно структуры JSON go слишком**представление** > **другие окна** > **структуры JSON**.

3. Щелкните файл шаблона ресурсов toohello tooadd **добавить ресурс** hello верхней части окна hello структуры JSON. Или щелкните правой кнопкой мыши в окне структуры JSON hello **ресурсов**и выберите **добавить новый ресурс**.

    ![Окно "Структура JSON"](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. В hello **добавить ресурс** диалоговое окно, найдите и выберите **приложения логики**. Присвойте имя приложению логики и выберите **Добавить**.

    ![Добавление ресурса](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>Дальнейшие действия

* [Управление Logic Apps с помощью Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Примеры приложений логики и распространенные сценарии](logic-apps-examples-and-scenarios.md)
* [Узнайте, как tooautomate business обрабатывает с приложениями логики Azure](http://channel9.msdn.com/Events/Build/2016/T694)
* [Узнайте, как toointegrate системах с логикой приложения Azure](http://channel9.msdn.com/Events/Build/2016/P462)
