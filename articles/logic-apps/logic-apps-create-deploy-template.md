---
title: "aaaCreate шаблоны развертывания для приложения логики Azure | Документы Microsoft"
description: "Узнайте, как создавать шаблоны Azure Resource Manager для развертывания приложений логики и управлять выпусками."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>Создание шаблонов для развертывания приложений логики и управления выпусками

После создания приложения логики, может потребоваться toocreate ее в качестве шаблона диспетчера ресурсов Azure.
Таким образом, можно легко развернуть среды tooany hello логику приложения или группы ресурсов, где он может понадобиться.
Дополнительные сведения о шаблонах Resource Manager см. в статьях [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md) и [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="logic-app-deployment-template"></a>Шаблон развертывания приложения логики

Приложение логики состоит из трех основных компонентов:

* **Ресурсов приложения логики**: содержит сведения о таких вещей, как ценовой план, расположение и hello определения рабочего процесса.
* **Определение рабочего процесса**: описание действия рабочего процесса приложения логики и как механизм логики приложения hello должна выполняться hello рабочего процесса.
Это определение можно просмотреть в окне **Представление кода** приложения логики.
В ресурсе приложения hello логики, можно найти это определение в hello `definition` свойство.
* **Подключения**: ссылается tooseparate ресурсы, которые безопасно хранить метаданные любого подключения соединитель, такие как строка подключения и маркер доступа.
В ресурсе приложения hello логику, логику приложения ссылается на эти ресурсы в hello `parameters` раздела.

Вы можете просмотреть все эти компоненты имеющихся приложений логики с помощью таких инструментов, как [обозреватель ресурсов Azure](http://resources.azure.com).

toomake шаблон для логики приложения toouse с развертывания группы ресурсов, необходимо определить ресурсы hello и параметризовать при необходимости.
Например при развертывании tooa разработку, тестирование и рабочей среде, скорее всего нужно toouse строки другое подключение tooa базы данных SQL в каждой среде.
Или можно разместить toodeploy в разных подписок или групп ресурсов.  

## <a name="create-a-logic-app-deployment-template"></a>Создание шаблона развертывания приложения логики

toohave простым способом Hello шаблон развертывания допустимым логику приложения является toouse [средств Visual Studio для приложения логики](logic-apps-deploy-from-vs.md).
средства Visual Studio Hello создавать шаблон допустимым развертывания, который может использоваться в любой подписки или расположение.

При создании шаблона для развертывания приложения логики могут быть полезными и некоторые другие инструменты.
Можно создавать вручную, то есть с помощью hello ресурсы уже описанные здесь параметры toocreate при необходимости.
Другой вариант — toouse [создатель шаблон приложения логики](https://github.com/jeffhollan/LogicAppTemplateCreator) модуля PowerShell. Этот модуль с открытым исходным кодом сначала вычисляет hello логики приложения, а также любые соединения, он использует и создает ресурсов шаблона с hello необходимые параметры для развертывания.
Например если у вас есть приложение логики, которая получает сообщение из очереди Azure Service Bus и добавляет базы данных Azure SQL tooan данных, средство hello сохраняет всю логику orchestration hello и параметризует hello SQL и строки подключения служебной шины, чтобы их можно задать во время развертывания.

> [!NOTE]
> Подключения должны быть в пределах hello же группе ресурсов приложения логики hello.
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>Установка модуля PowerShell шаблон приложения логики hello
Hello простым способом tooinstall hello модуль — это via hello [коллекции PowerShell](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), с помощью команды hello `Install-Module -Name LogicAppTemplate`.  

Также можно установить модуль PowerShell hello вручную:

1. Загрузить последний выпуск hello hello [создатель шаблон приложения логики](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).  
2. Извлеките hello папки в папку модуля PowerShell (обычно `%UserProfile%\Documents\WindowsPowerShell\Modules`).

Для toowork модуля hello любого клиента и подписки доступ токена, мы рекомендуем использовать с hello [ARMClient](https://github.com/projectkudu/ARMClient) средство командной строки.  В этой [записи блога](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) программа ARMClient рассматривается подробней.

### <a name="generate-a-logic-app-template-by-using-powershell"></a>Создание шаблона приложения логики с помощью PowerShell
После установки PowerShell, можно создать шаблон с помощью hello следующую команду:

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`— идентификатор подписки Azure hello. Эту строку сначала получает доступ маркера через ARMClient, а затем передает его через toohello сценарий PowerShell и создает hello шаблона в JSON-файла.

## <a name="add-parameters-tooa-logic-app-template"></a>Добавить шаблон приложения логики tooa параметров
После создания шаблона логики приложения, можно продолжить tooadd или изменить параметры, которые могут потребоваться. Например если определение включает tooan идентификатор ресурса Azure функцию или вложенный рабочий процесс планирования toodeploy в одно развертывание, можно добавить дополнительные ресурсы tooyour шаблон и параметризовать идентификаторов, при необходимости. Hello применимо и к tooany ссылки toocustom API-интерфейсы Swagger конечных точек или предполагается, что toodeploy с каждой группой ресурсов.

## <a name="deploy-a-logic-app-template"></a>Развертывание шаблона приложения логики

С помощью любого средства, как PowerShell, API-Интерфейс REST, можно развернуть шаблон [Visual Studio Team Services Release Management](#team-services)и шаблона-развертывания через портал Azure hello.
Кроме того, toostore hello значения для параметров, рекомендуется создать [файл параметров](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).
Узнайте, каким образом слишком[развертывания ресурсов с помощью PowerShell и шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) или [развертывания ресурсов с помощью шаблонов диспетчера ресурсов Azure и hello портал Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).

### <a name="authorize-oauth-connections"></a>Авторизация подключений OAuth

После развертывания приложения hello логики работает конца в конец с допустимыми параметрами.
Вы по-прежнему необходимо разрешить toogenerate подключений OAuth действительный маркер доступа.
tooauthorize OAuth подключения, откройте приложение hello логику в конструкторе логики приложения hello и разрешить эти подключения. Или для автоматического развертывания можно использовать сценарий tooconsent tooeach OAuth подключения.
На GitHub есть пример сценария в проекте [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) .

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Visual Studio Team Services Release Management

Общие сценарии развертывания и управления ими среды — toouse средства, подобного управления выпусками в Visual Studio Team Services с помощью шаблона развертывания логику приложения. Visual Studio Team Services включает в себя [развертывания группы ресурсов Azure](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) задач можно добавить tooany сборки или выпуска конвейера. Требуется toohave [участника-службы](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) для авторизации toodeploy, а затем можно создать определение выпуска hello.

1. Для создания пустого определения в Release Management выберите пункт **Пусто**.

    ![Создание пустого определения][1]

2. Выберите все ресурсы, необходимые для этого, скорее всего, включая hello логику приложения шаблона, созданного вручную или как часть hello процесса построения.
3. Добавьте задачу **развертывания группы ресурсов Azure** .
4. Настройка с помощью [участника-службы](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)и ссылаться на файлы шаблонов и параметров шаблона hello.
5. По-прежнему toobuild действия в процессе выпуска hello для среды, автоматических тестов или утверждающих при необходимости.

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
