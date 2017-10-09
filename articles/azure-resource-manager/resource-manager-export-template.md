---
title: "шаблон диспетчера ресурсов Azure aaaExport | Документы Microsoft"
description: "Используйте Управление ресурсов Azure tooexport шаблон в существующую группу ресурсов."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>Экспорт шаблона Azure Resource Manager из существующих ресурсов
В этой статье вы узнаете, как tooexport шаблона диспетчера ресурсов от существующих ресурсов в вашей подписке. Можно использовать, созданного шаблона toogain лучше понять синтаксис шаблона.

Существует два способа tooexport шаблона:

* Вы можете экспортировать hello **фактическое шаблон, используемый для развертывания**. экспортированный шаблон Hello включает все параметры hello и переменные, точно так, как они выглядели в исходном шаблоне hello. Этот подход полезен при развертывании ресурсы с помощью портала hello и требуется toosee hello шаблона toocreate эти ресурсы. Этот шаблон удобно использовать. 
* Вы можете экспортировать **созданный шаблон, который представляет текущее состояние группы ресурсов hello hello**. экспортированный шаблон Hello не основывается на любой шаблон, который использовался для развертывания. Вместо этого он создает шаблон, который является моментальным снимком, группа ресурсов «hello». экспортированный шаблон Hello имеет много жестко запрограммированных значений и, возможно, не все параметры, как обычно при определении. Этот подход полезен, если вы изменили после развертывания группы ресурсов hello. Перед использованием в этот шаблон обычно требуется внести изменения.

В этом разделе показаны оба подхода через портал hello.

## <a name="deploy-resources"></a>Развертывание ресурсов
Давайте начнем, развернув tooAzure ресурсов, который можно использовать для экспорта в качестве шаблона. Если уже есть группа ресурсов в подписке, что требуется шаблон tooa tooexport, этот раздел можно пропустить. Hello оставшейся части этой статьи предполагается, что вы развернули hello веб-приложения и решения базы данных SQL, приведенные в этом разделе. При использовании другого решения работы может немного отличаться, но являются tooexport шаблон действия hello hello таким же. 

1. В hello [портал Azure](https://portal.azure.com)выберите **New**.
   
      ![Выбор нового](./media/resource-manager-export-template/new.png)
2. Поиск **веб-приложение + SQL** и выберите его из доступных параметров hello.
   
      ![Поиск элемента "Веб-приложение и SQL"](./media/resource-manager-export-template/webapp-sql.png)

3. Нажмите кнопку **Создать**.

      ![Выбор создания](./media/resource-manager-export-template/create.png)

4. Укажите hello необходимые значения для hello веб-приложения и базы данных SQL. Нажмите кнопку **Создать**.

      ![Указание значений SQL и веб-приложения](./media/resource-manager-export-template/provide-web-values.png)

Hello развертывания может занять около минуты. После завершения развертывания hello подписки содержит решение hello.

## <a name="view-template-from-deployment-history"></a>Просмотр шаблона из журнала развертываний
1. Go toohello колонки группы ресурсов для новой группы ресурсов. Обратите внимание, что этой колонке hello отображается результат последнего развертывания hello hello. Щелкните эту ссылку.
   
      ![колонка группы ресурсов](./media/resource-manager-export-template/select-deployment.png)
2. Можно просмотреть журнал развертывания для группы hello. В вашем случае hello колонки, скорее всего, перечислены только одно развертывание. Выберите его.
   
     ![последнее развертывание](./media/resource-manager-export-template/select-history.png)
3. Hello колонке Сводка hello развертывания. Сводка Hello включает hello состояние развертывания hello, операций и значения hello, предоставленный для параметров. toosee hello шаблона, который использовался для развертывания hello, выберите **Просмотр шаблона**.
   
     ![просмотр сводки по развертыванию](./media/resource-manager-export-template/view-template.png)
4. Диспетчер ресурсов получает hello следующие семь файлы автоматически:
   
   1. **Шаблон** -hello шаблон, определяющий hello инфраструктуры для вашего решения. При создании учетной записи хранилища hello через портал hello, диспетчер ресурсов использовать toodeploy шаблона его и сохранить для дальнейшего использования этого шаблона.
   2. **Параметры** -файл параметров, можно использовать toopass значений, во время развертывания. Он содержит hello значения, указанные во время первого развертывания hello. Эти значения можно изменить при повторном развертывании шаблона hello.
   3. **CLI** -можно использовать шаблон hello toodeploy сценария файл Azure интерфейс командной строки (CLI).
   3. **CLI 2.0** -можно использовать шаблон hello toodeploy сценария файл Azure интерфейс командной строки (CLI).
   4. **PowerShell** -файл сценария Azure PowerShell можно использовать шаблон toodeploy hello.
   5. **.NET** -класс .NET, можно использовать шаблон toodeploy hello.
   6. **Ruby** -класс Ruby, можно использовать шаблон toodeploy hello.
      
      Hello файлы могут быть доступны по ссылкам по колонке hello. По умолчанию hello колонке отображает шаблон hello.
      
       ![Просмотреть шаблон](./media/resource-manager-export-template/see-template.png)
      
Этот шаблон представляет собой фактическое шаблона hello используемых toocreate, веб-приложения и базы данных SQL. Обратите внимание, что он содержит параметры, позволяющие tooprovide различные значения во время развертывания. toolearn Дополнительные сведения о структуре hello шаблона, в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).

## <a name="export-hello-template-from-resource-group"></a>Экспорт шаблона hello из группы ресурсов
Если вы вручную изменить ресурсы или добавить ресурсы в несколько развертываний, получение шаблона из журнала развертывания hello не отражает текущее состояние группы ресурсов hello hello. В этом разделе показано, как шаблон, который отражает tooexport hello текущее состояние группы ресурсов hello. 

> [!NOTE]
> Нельзя экспортировать шаблон для группы ресурсов, которая содержит более 200 ресурсов.
> 
> 

1. шаблон hello tooview для группы ресурсов, выберите **сценарий автоматизации**.
   
      ![экспорт группы ресурсов](./media/resource-manager-export-template/select-automation.png)
   
     Диспетчер ресурсов для оценки hello ресурсов в группе ресурсов hello и создает шаблон для этих ресурсов. Не все типы ресурсов поддерживают hello экспорта шаблона функции. Может появиться сообщение о том, имеется проблема с экспортом hello. Вы узнаете, как toohandle те проблемы в hello [исправление проблемы при экспорте](#fix-export-issues) раздела.
2. Снова появиться hello шесть файлов, которые можно использовать решение tooredeploy hello. Тем не менее этот шаблон hello времени будет немного отличаться. Обратите внимание, что hello созданного шаблона содержит меньшее число параметров, чем шаблон hello в предыдущем разделе. Кроме того многие hello значения (например, расположение и значения номера SKU) жестко запрограммированы в этот шаблон, а не принимает значение параметра. Перед повторным использованием этого шаблона, может потребоваться tooedit шаблона hello toomake лучше использовать параметры. 
   
3. У вас есть два способа для продолжения toowork с помощью этого шаблона. Можно загрузить шаблон hello и работать с ним локально с помощью редактора JSON. Также можно сохранить библиотека tooyour шаблонов hello и работать с ним через портал hello.
   
     Если вы знакомы с помощью редактора JSON, например [VS Code](https://code.visualstudio.com/) или [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), может потребоваться, загрузив шаблон hello локально и с помощью этого редактора. toowork локально, выберите **загрузить**.
   
      ![скачивание шаблона](./media/resource-manager-export-template/download-template.png)
   
     Если вы не настроены с помощью редактора JSON, может потребоваться редактирования шаблона hello через портал hello. Hello оставшейся части этой статьи предполагается, что вы сохранили библиотека tooyour шаблонов hello hello портала. Однако сделать hello же изменения синтаксиса шаблона toohello ли локально работа с редактором JSON или через портал hello. Выберите toowork через портал hello **добавить toolibrary**.
   
      ![добавить toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     При добавлении библиотеки шаблонов toohello, дайте шаблону hello, имя и описание. Затем нажмите кнопку **Сохранить**.
   
     ![задание значений шаблона](./media/resource-manager-export-template/save-library-template.png)
4. Выберите шаблон, сохраненный в библиотеке, tooview **дополнительные службы**, тип **шаблоны** toofilter результатов установите **шаблоны**.
   
      ![поиск шаблонов](./media/resource-manager-export-template/find-templates.png)
5. Выберите шаблон hello с именем hello сохранения.
   
      ![выбор шаблона](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Настройка шаблона hello
работает Hello экспортированный шаблон нормально, если требуется toocreate hello же и веб-приложения базы данных SQL для всех развертываний. Но Resource Manager обеспечивает более гибкое развертывание. В этой статье показано, как параметры tooadd для hello базы данных, имя и пароль администратора. Можно использовать этот же подход tooadd большую гибкость для других значений в шаблоне hello.

1. toocustomize hello шаблона, выберите **изменить**.
   
     ![отображение шаблона](./media/resource-manager-export-template/select-edit.png)
2. Выберите шаблон hello.
   
     ![изменение шаблона](./media/resource-manager-export-template/select-added-template.png)
3. значения hello может toopass toobe, toospecify может возникнуть во время развертывания, добавьте следующие два параметра toohello hello **параметры** раздела hello шаблона:

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. новые параметры toouse hello, замените определение сервера SQL hello hello **ресурсов** раздела. Обратите внимание, что **administratorLogin** и **administratorLoginPassword** теперь используют значения параметров.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. Выберите **ОК** после редактирования шаблона hello.
7. Выберите **Сохранить** toosave hello изменения toohello шаблона.
   
     ![сохранение шаблона](./media/resource-manager-export-template/save-template.png)
8. tooredeploy hello обновить шаблон, выберите **развернуть**.
   
     ![развертывание шаблона](./media/resource-manager-export-template/redeploy-template.png)
9. Укажите значения параметров и выберите ресурсов группы toodeploy hello ресурсов.


## <a name="fix-export-issues"></a>Устранение проблем при экспорте
Не все типы ресурсов поддерживают hello экспорта шаблона функции. tooresolve эту проблему, вручную добавить отсутствующие ресурсы hello обратно в шаблон. сообщение об ошибке Hello включает hello типы ресурсов, которые невозможно экспортировать. Найдите этот тип ресурса в [справочнике по шаблонам](/azure/templates/). Например, toomanually Добавление шлюза виртуальной сети см. в разделе [ссылка на шаблон Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).

> [!NOTE]
> Проблемы при экспорте могут возникать, только если шаблон экспортируется из группы ресурсов, а не из журнала развертываний. При развертывании последнего точно представляет текущее состояние группы ресурсов hello hello, следует экспортировать шаблон hello из журнала развертывания hello, а не из группы ресурсов hello. Экспортируйте только из группы ресурсов после внесения изменений toohello ресурсов группы, не определенные в одном шаблоне.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Вы узнали, каким образом tooexport шаблон на основе ресурсов, которые вы создали на портале hello.

* Вы можете развернуть шаблон с помощью [PowerShell](resource-group-template-deploy.md), [интерфейса командной строки Azure](resource-group-template-deploy-cli.md) или [REST API](resource-group-template-deploy-rest.md).
* tooexport шаблона с помощью PowerShell. в статье toosee [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](powershell-azure-resource-manager.md).
* tooexport шаблона с помощью Azure CLI см. в статье toosee [используйте hello Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure](xplat-cli-azure-resource-manager.md).

