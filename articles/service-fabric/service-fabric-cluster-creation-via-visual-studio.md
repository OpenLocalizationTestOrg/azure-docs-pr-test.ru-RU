---
title: "aaaSetting кластера Service Fabric, с помощью Visual Studio | Документы Microsoft"
description: "Описывает, каким образом tooset копирование Service Fabric кластера с помощью шаблона Azure Resource Manager, созданные проекта группы ресурсов Azure в Visual Studio"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Настройка кластера Service Fabric с помощью Visual Studio
В этой статье описывается, как tooset копирование Azure Service Fabric кластера с помощью шаблона диспетчера ресурсов Azure и Visual Studio. Мы будем использовать шаблона Visual Studio Azure проекта группы ресурсов toocreate hello. После создания шаблона hello, его можно развернуть tooAzure прямо из Visual Studio. Его также можно использовать из сценария или в ходе процесса непрерывной интеграции (CI).

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Создание шаблона кластера Service Fabric с помощью проекта группы ресурсов Azure
tooget к работе, откройте Visual Studio создайте проект группы ресурсов Azure (она доступна в hello **облака** папки):

![Диалоговое окно "Новый проект" с выбранным проектом группы ресурсов Azure][1]

Можно создать новое решение Visual Studio для этого проекта или добавить его в существующее решение tooan.

> [!NOTE]
> Если отсутствует hello проекта группы ресурсов Azure в узле hello облака, у вас hello установленный пакет SDK Azure. Запустите установщик веб-платформы ([установить сейчас](http://www.microsoft.com/web/downloads/platform.aspx) Если это еще не сделано) и выполните поиск «Azure SDK для .NET» и установите версию hello, которая совместима с версией Visual Studio.
> 
> 

После нажатия кнопки "ОК" hello, Visual Studio запросит tooselect hello диспетчера ресурсов шаблон toocreate:

![Диалоговое окно "Выбор шаблона Azure" с выбранным шаблоном кластера Service Fabric][2]

Выберите шаблон кластера Service Fabric hello и попаданий hello ОК кнопку еще раз. Теперь создан проект Hello и hello шаблона диспетчера ресурсов.

## <a name="prepare-hello-template-for-deployment"></a>Подготовка к развертыванию hello шаблона
До шаблона hello развернутой toocreate hello кластера, необходимо указать значения для параметров шаблона требуется hello. Эти значения параметров считываются из hello `ServiceFabricCluster.parameters.json` файл, который находится в hello `Templates` папки проекта группы ресурсов hello. Откройте файл hello и предоставить hello следующие значения:

| Имя параметра | Описание |
| --- | --- |
| adminUserName |Hello имя учетной записи администратора hello Service Fabric компьютеров (узлов). |
| certificateThumbprint |Здравствуйте, отпечаток сертификата hello, обеспечивающую безопасность кластера hello. |
| sourceVaultResourceId |Hello *идентификатор ресурса* из хранилища ключей hello, где hello, обеспечивающую безопасность кластера hello сертификат. |
| certificateUrlValue |URL-адрес Hello hello сертификат безопасности кластера. |

шаблон диспетчера ресурсов структуры в Visual Studio службы Hello создает безопасный кластера, защищенного с помощью сертификата. Этот сертификат идентифицируется hello последние три параметра шаблона (`certificateThumbprint`, `sourceVaultValue`, и `certificateUrlValue`), и он должен присутствовать в **хранилище ключей Azure**. Дополнительные сведения о как toocreate hello сертификат безопасности кластера см. в разделе [сценарии безопасности кластера Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) статьи.

## <a name="optional-change-hello-cluster-name"></a>(Необязательно) измените имя кластера hello
У каждого кластера Service Fabric есть имя. При создании кластера Fabric в Azure определяет, имя кластера (а также hello регион Azure) hello имя системы доменных имен (DNS) для кластера hello. Например, если имя кластера `myBigCluster`и hello местоположение (регион Azure) группы ресурсов hello, где будет размещаться новый кластер hello Восток США, hello DNS-имя кластера hello будет `myBigCluster.eastus.cloudapp.azure.com`.

По умолчанию имя кластера hello автоматически создается и становится уникальной путем присоединения префикс «кластер» tooa случайных суффикс. Это делает шаблон hello очень легко toouse как часть **непрерывной интеграции** системы (CI). Toouse определенное имя для кластера, это может применяться tooyou задайте значение hello hello `clusterName` переменных в файле шаблона диспетчера ресурсов hello (`ServiceFabricCluster.json`) имя выбранного tooyour. Это первая переменная hello, определенный в этом файле.

## <a name="optional-add-public-application-ports"></a>Добавление общедоступных портов приложения (необязательно)
Вы также можете toochange hello приложения открытые порты для hello кластера перед ее развертыванием. По умолчанию шаблон hello открывает только два открытых TCP-порты (80 и 8081). Если требуется несколько приложений, измените определение подсистемы балансировки нагрузки Azure hello в шаблоне hello. Определение Hello хранится в файле основного шаблона hello (`ServiceFabricCluster.json`). Откройте этот файл и выполните поиск `loadBalancedAppPort`. Каждый порт связан с тремя артефактами.

1. Шаблон переменной, определяющей hello номер порта TCP для hello порта:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. Объект *проверки* , определяющий, как часто и как долго hello балансировки нагрузки Azure пытается toouse конкретный узел Service Fabric перед переходом на другой через tooanother один. Hello зонды являются частью hello ресурсов подсистемы балансировки нагрузки. Вот определение hello пробы для hello первый порт приложения по умолчанию.
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. Объект *правило балансировки нагрузки* , объединяет порт hello и hello проверки, который позволит Балансировка нагрузки по набору узлов кластера Service Fabric:
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   При планировании кластера toohello toodeploy приложения hello требуются дополнительные порты, их можно добавить путем создания дополнительной проверки и определения правил балансировки нагрузки. Дополнительные сведения о том, как toowork с подсистемой балансировки нагрузки Azure посредством шаблонов диспетчера ресурсов. в разделе [приступить к созданию внутренней подсистемы балансировки нагрузки с помощью шаблона](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-hello-template-by-using-visual-studio"></a>Развертывание hello шаблона с помощью Visual Studio
После сохранения всех hello значения обязательного параметра в`ServiceFabricCluster.param.dev.json` файла будут готовы toodeploy hello шаблона и создание кластера Service Fabric. Щелкните правой кнопкой мыши проект группы ресурсов hello в обозревателе решений Visual Studio и выберите **развертывание | Новое развертывание...** . Если необходимо, Visual Studio будет отображать hello **развертывание tooResource группы** диалоговое окно, запрашивающее tooauthenticate tooAzure:

![Диалоговое окно tooResource Группа развертывания][3]

диалоговое окно «Hello» позволяет выбрать существующую группу ресурсов диспетчера ресурсов для кластера hello и предоставляет параметр toocreate hello новый. Обычно становится toouse смысл отдельной группе ресурсов кластера Service Fabric.

После нажатия кнопки hello развертывание Visual Studio предложит вам значения параметров шаблона tooconfirm hello. Попаданий hello **Сохранить** кнопки. Один параметр не имеет постоянного значения: hello пароль учетной записи администратора для кластера hello. Visual Studio по запросу для одного необходимо tooprovide значение пароля.

> [!NOTE]
> Начиная с версии Azure SDK 2.9, Visual Studio поддерживает чтение паролей из **хранилища ключей Azure** во время развертывания. В диалоговом окне Параметры шаблона hello Обратите внимание, что hello `adminPassword` текстовом поле параметра имеет маленький значок «ключ» на hello вправо. Этот значок позволяет tooselect существующие секрета хранилища ключей как hello пароля администратора для кластера hello. Просто убедитесь, что toofirst разрешить доступ к диспетчеру ресурсов Azure для шаблона-развертывания в hello Дополнительные политики доступа к хранилищу ключей. 
> 
> 

Вы можете отслеживать ход выполнения процесса развертывания hello в окне вывода Visual Studio hello hello. После завершения развертывания шаблона hello на новый кластер: toouse Готово!

> [!NOTE]
> Если PowerShell никогда не используется tooadminister Azure на основе машины hello, используется в данный момент, toodo необходимо немного обслуживания.
> 
> 1. Включить скрипты, запустив hello PowerShell [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) команды. Для компьютеров разработчиков обычно устанавливается политика "Без ограничений".
> 2. Решите, будет ли tooallow сбор диагностических данных из команд Azure PowerShell и запустите [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) или [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) при необходимости. Это позволит избежать вывода ненужных запросов во время развертывания шаблона.
> 
> 

Если имеются ошибки, воспользуйтесь toohello [портал Azure](https://portal.azure.com/) и группе ресурсов Привет открыть, было выполнено развертывание. Нажмите кнопку **все параметры**, нажмите кнопку **развертываний** в колонке параметров hello. Здесь будут находиться подробные диагностические сведения о неудачном развертывании группы ресурсов.

> [!NOTE]
> Кластеров Service Fabric требуется определенное количество узлов toobe toomaintain доступности и сохранить состояние - ссылка tooas «поддержания кворума». Таким образом, она будет безопасно tooshut строя все машины hello в кластере hello пока сначала выполнить [полного резервного копирования состояния](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о настройке кластера Service Fabric, с помощью портала Azure hello](service-fabric-cluster-creation-via-portal.md)
* [Узнайте, как toomanage и развертывать приложения Service Fabric, с помощью Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
