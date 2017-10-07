---
title: "aaaPublish приложения tooa удаленного кластера с помощью Visual Studio | Документы Microsoft"
description: "Узнайте, как toopublish структуру приложения tooa удаленной службы кластера с помощью Visual Studio."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Развертывание и удаление приложений с помощью Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [API-интерфейсы FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Hello Azure Service Fabric расширение Visual Studio предоставляет простой, сценариев и repeatable способ toopublish кластера Service Fabric tooa приложений.

## <a name="hello-artifacts-required-for-publishing"></a>Hello артефакты, необходимые для публикации
### <a name="deploy-fabricapplicationps1"></a>Deploy-FabricApplication.ps1
Это скрипт PowerShell, который использует путь к профилю публикации в качестве параметра для публикации приложений Service Fabric. Поскольку этот скрипт является частью приложения, вы являетесь приветствия toomodify его как необходимы для работы приложения.

### <a name="publish-profiles"></a>Профили публикации
Вызывается в папку проекта приложения Service Fabric hello **PublishProfiles** содержит XML-файлов, хранящих сведения, необходимые для публикации приложений, таких как:

* параметры подключения к кластеру Service Fabric;
* Файл параметров приложения tooan путь
* параметры обновления.

По умолчанию приложение содержит три профиля публикации: Local.1Node.xml, Local.5Node.xml и Cloud.xml. Можно добавить дополнительные профили, скопировав и вставив один из файлов по умолчанию hello.

### <a name="application-parameter-files"></a>Файлы параметров приложений
Вызывается в папку проекта приложения Service Fabric hello **ApplicationParameters** содержит XML-файлы для значения параметра манифеста приложения, определяемый пользователем. Файлы манифеста приложения могут быть параметризованы, так что можно использовать различные значения для параметров развертывания. toolearn Дополнительные сведения о параметризации приложения, в разделе [управление несколькими средами в Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md).

> [!NOTE]
> Для служб субъекта нужно построить проект hello сначала перед выполнением tooedit hello файл в редакторе или с помощью hello диалоговое окно публикации. Это так, как часть файлов манифеста hello создается во время построения hello.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish приложение, используя диалоговое окно приветствия опубликовать приложение Service Fabric
Hello следующие шаги показывают, как приложения с помощью toopublish hello **опубликовать приложение Service Fabric** диалоговое окно «», предоставляемые hello структуры набора средств Visual Studio службы.

1. В контекстном меню проекта приложения Fabric Application hello hello, выберите **публикации...** tooview hello **опубликовать приложение Service Fabric** диалоговое окно.
   
    ![Hello ** диалоговое окно публикации службы структуры приложения **][0]
   
    Hello файла, выбранного в hello **использовать профиль** раскрывающегося списка — где все параметры hello, за исключением **манифеста версии**, сохраняются. Можно повторно использовать существующий профиль или создать новый, выбрав **< Управление профилями... >** в hello **использовать профиль** раскрывающегося списка. При выборе профиля публикации ее содержимое отображается в соответствующих полях hello диалоговое окно «hello». toosave изменения в любое время, выберите hello **сохранить профиль** ссылку.    
2. В hello **конечной точки подключения** укажите конечную точку публикации локального или удаленного кластера Service Fabric элемента. tooadd или измените hello конечной точки подключения, щелкните hello **конечной точки подключения** раскрывающегося списка. Список hello доступных Service Fabric кластера подключения конечные точки toowhich, можно опубликовать на основании подписками Azure Hello. Обратите внимание, что если вы еще не вошли в tooVisual Studio, можно запрашиваемые toodo таким образом.
   
    Используйте toochoose hello кластера выбора диалогового окна поле из набора доступных подписках и кластеры hello.
   
    ![Hello ** диалоговое окно Выбор службы структуры кластера **][1]
   
   > [!NOTE]
   > При желании toopublish tooan произвольный конечной точки (например, кластер стороны). в разделе hello **публикации конечной точки произвольный кластера tooan** разделе ниже.
   > 
   > 
   
    После выбора конечной точки, Visual Studio проверяет кластера Service Fabric toohello выбранного соединения hello. Если кластер hello не защищены, Visual Studio можно подключить tooit немедленно. Однако если hello кластера является защищенным, вам потребуется tooinstall сертификат локального компьютера, прежде чем продолжить. В разделе [как tooconfigure безопасные подключения](service-fabric-visualstudio-configure-secure-connections.md) для получения дополнительной информации. После завершения, выберите hello **ОК** кнопки. отображается выбранный кластер Hello в hello **опубликовать приложение Service Fabric** диалоговое окно.
3. В hello **файл параметров приложения** раскрывающегося списка перейдите tooan файл параметров приложения. Файл параметров приложения содержит указанные пользователем значения для параметров в файле манифеста приложения hello. tooadd или изменение параметра, выберите hello **изменить** кнопки. Введите или измените значение параметра hello в hello **параметры** сетки. После завершения, выберите hello **Сохранить** кнопки.
   
    ![Hello ** диалоговое окно изменения параметров **][2]
4. Используйте hello **обновления hello приложения** toospecify флажок этого публикации действия ли обновление. Действия обновления отличаются от обыкновенных действий публикации. Список различий см. в статье [Обновление приложения Service Fabric](service-fabric-application-upgrade.md). tooconfigure обновления свойств, выберите hello **настроить параметры обновления** ссылку. Откроется окно редактора обновления параметра Hello. В разделе [настроить обновление hello приложения Service Fabric](service-fabric-visualstudio-configure-upgrade.md) toolearn Дополнительные сведения о параметрах обновления.
5. Выберите hello **версии манифеста...** Кнопка tooview hello **изменение версии** диалоговое окно. Версий tooupdate приложения и службы, необходимые для обновления tootake месте. В разделе [учебника обновления приложения Service Fabric](service-fabric-application-upgrade-tutorial.md) toolearn приложения и версии манифеста службы влиять на время обновления.
   
    ![Hello ** диалоговое окно Изменение версии **][3]
   
    Если приложение hello и версии службы используются семантического управления версиями, такие как 1.0.0 или числовые значения в формате hello 1.0.0.0, установите hello **автоматическое обновление версий приложения и службы** параметр. Когда выберите этот параметр, служба hello и номеров версий приложения автоматически обновляются каждый раз, когда код, конфигурации или обновляется версия пакета данных. При желании tooedit hello версий вручную, снимите флажок toodisable hello этот компонент.
   
   > [!NOTE]
   > Для всех tooappear записи пакета для проекта субъекта вначале постройте проект toogenerate hello hello записей в файлах манифеста службы hello.
   > 
   > 
6. После этого все необходимые параметры hello, указав выберите hello **публикации** кнопку toopublish toohello вашего приложения, в выбранных кластера Service Fabric. применяются заданные вами параметры Hello toohello процесса публикации.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>Публикует конечную произвольный кластера tooan (включая стороны)
Hello возможности публикации Visual Studio оптимизирована для публикации tooremote кластеры, связанные с одной из ваших подписок Azure. Однако это конечные точки tooarbitrary возможных toopublish (такие как кластеры субъекта Service Fabric) путем непосредственного редактирования hello публикации XML-профиль. Как описано выше трех профилей публикации предоставлено по умолчанию —**Local.1Node.xml**, **Local.5Node.xml**, и **Cloud.xml**--, но являются toocreate приветствия Дополнительные профили для различных сред. Например, может потребоваться toocreate профиль для публикации tooparty кластеры, такими **Party.xml**.

При подключении tooan незащищенным кластера все, что требуется является hello конечной точки подключения кластера, например `partycluster1.eastus.cloudapp.azure.com:19000`. В этом случае конечная точка подключения hello в hello публикации профиль будет выглядеть примерно следующим образом:

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  При подключении tooa защищенного кластера, необходимо также tooprovide подробности hello hello клиентский сертификат из локального хранилища toobe hello, используемый для проверки подлинности. Дополнительные сведения см. в разделе [кластера Service Fabric Настройка безопасных подключений tooa](service-fabric-visualstudio-configure-secure-connections.md).

  После настройки профиль публикации, на него можно ссылаться в hello опубликовать диалоговое окно, как показано ниже.

  ![Новый профиль публикации в диалоговом окне публикации][4]

  Обратите внимание, что в этом случае hello новый профиль публикации точек tooone файлов параметров приложения по умолчанию hello. Это подходит, если требуется toopublish hello того же приложения конфигурации tooa число сред. В отличие от этого в случаях, где требуется toohave различные конфигурации для каждой среды, требуется toopublish для принесет toocreate смысле соответствующий файл параметров приложения.

## <a name="next-steps"></a>Дальнейшие действия
tooautomate hello процесса публикации в среде непрерывной интеграции. в статье toolearn [Настройка непрерывной интеграции Service Fabric](service-fabric-set-up-continuous-integration.md).

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
