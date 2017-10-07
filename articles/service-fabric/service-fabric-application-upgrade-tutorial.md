---
title: "Учебник обновления приложения Fabric aaaService | Документы Microsoft"
description: "В этой статье рассматриваются возможности hello развертывания приложения Service Fabric, изменения кода hello и развертывание обновления с помощью Visual Studio."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a>Учебник по обновлению приложений Service Fabric с помощью Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Azure Service Fabric упрощает процесс обновления облачных приложений за счет того, что обновляются только измененные службы и о мониторинге работоспособности приложения на протяжении всего процесса обновления hello hello. Он также автоматически выполняет откат hello приложения toohello предыдущей версии при возникновении проблем. Обновление приложения Service Fabric *время простоя ноль*, поскольку можно обновить приложение hello без простоев. В этом учебнике описано как toocomplete последовательного обновления из Visual Studio.

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a>Шаг 1: Создавать и публиковать образец hello визуальных объектов
Сначала загрузите hello [визуальных объектов](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) приложений с сайта GitHub. Затем, сборка и публикация приложения hello, щелкнув правой кнопкой мыши проект приложения hello, **VisualObjects**и выбрав hello **публикации** команды в пункте меню Service Fabric hello.

![Контекстное меню для приложения Service Fabric][image1]

При выборе **публикации** появится всплывающее окно, и можно задать hello **использовать профиль** слишком**PublishProfiles\Local.xml**. Hello должно выглядеть окно hello следующие, прежде чем нажимать кнопку **публикации**.

![Публикация приложения Service Fabric][image2]

Теперь можно выбрать **публикации** в диалоговое окно «hello». Можно использовать [Service Fabric Explorer tooview hello кластера и hello приложения](service-fabric-visualizing-your-cluster.md). Hello визуальных объектов приложения имеет веб-службы, вы можете перейти ввода tooby [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) в адресной строке браузера hello.  Вы увидите 10 перемещаемые объекты visual, перемещение на экране приветствия.

**Примечание:** Если развертывание слишком`Cloud.xml` профиля (Azure Service Fabric), приложение hello затем должны быть доступны в **http://{ServiceFabricName}. {} Region}.cloudapp.Azure.com:8081/visualobjects/**. Убедитесь, что вы имеете `8081/TCP` настроен в hello балансировки нагрузки (найти hello балансировки нагрузки в hello же группе ресурсов экземпляра Service Fabric hello).

## <a name="step-2-update-hello-visual-objects-sample"></a>Шаг 2: Обновление визуальных объектов образец hello
Можно заметить, что с версией hello, которое было развернуто на шаге 1, hello визуальных объектов не поворачиваются. Давайте обновление tooone этого приложения, где также вращать hello визуальных объектов.

Выберите проект VisualObjects.ActorService hello в hello VisualObjects решение и открыть hello **VisualObjectActor.cs** файла. В этом файле go метод toohello `MoveObject`, закомментируйте `visualObject.Move(false)`и раскомментируйте `visualObject.Move(true)`. Это изменение кода поворачивает hello объекты после обновления службы hello.  **Теперь можно построить (не перестроение) hello решения**, какие сборки hello изменения проектов. При выборе *перестроить все*, у вас есть tooupdate hello версий для всех hello проектов.

Мы также должны tooversion нашего приложения. версия hello toomake меняется после правой кнопкой мыши на hello **VisualObjects** проекта, hello Visual Studio можно использовать **изменение версии манифеста** параметр. При выборе этого параметра отображается hello диалоговое окно для выпуска версий следующим образом:

![Диалоговое окно "Управление версиями"][image3]

Hello версий обновления для hello изменить проекты и их пакеты кода вместе с tooversion приложения hello 2.0.0. После внесения изменений hello, hello манифест должен выглядеть hello следующим образом (выделенным полужирным шрифтом частям Показать изменения hello):

![Обновление версий][image4]

Hello набора средств Visual Studio можно выполнить автоматическое накопительные пакеты обновления версий после выбора **автоматическое обновление версий приложения и службы**. Если вы используете [SemVer](http://www.semver.org), требуется код tooupdate hello и/или конфигурации пакета версии только в том случае, если данный параметр выбран.

Сохранить изменения hello и проверьте hello **обновления hello приложения** поле.

## <a name="step-3--upgrade-your-application"></a>Шаг 3. Обновление приложения
Ознакомьтесь с hello [параметров обновления приложения](service-fabric-application-upgrade-parameters.md) и hello [процесс обновления](service-fabric-application-upgrade.md) tooget хорошо понимать hello различных обновить параметры, значения времени ожидания и работоспособности критерий, который можно применить. В этом пошаговом руководстве критерий оценки работоспособности службы hello имеет значение по умолчанию toohello (не отслеживается mode). Эти параметры можно настроить, выбрав **настроить параметры обновления** , а затем изменить параметры hello в случае необходимости.

Теперь мы все приложения hello toostart набор обновления, выбрав **публикации**. Эта функция обновляет вашего приложения tooversion 2.0.0, в котором поворот объектов hello. Структура службы обновляет в одном домене обновления за раз (некоторые объекты обновляются во-первых, следуют другие) и службы hello остается доступным во время обновления hello. Служба доступа к toohello может проверяться через клиент (браузер).  

Теперь, как hello продолжается обновления приложения, вы можете отслеживать ее с помощью Service Fabric Explorer с помощью hello **обновления выполняется** вкладка приложения hello.

Через несколько минут все домены обновления должны быть обновлены (завершено), а hello окне вывода Visual Studio также должны указать завершение обновления hello. И вы должны найти, *все* теперь заменяемого hello визуальных объектов в окне обозревателя!

Может требуется tootry изменение версий hello и переход с версии 2.0.0 tooversion 3.0.0 в качестве упражнения или даже от версии 2.0.0 резервное tooversion 1.0.0. Работать с тайм-аутов и toomake политики работоспособности самостоятельно ознакомиться с ними. При развертывании Azure кластера в качестве tooan отличие от локального кластера tooa, hello параметров, используемых может иметь toodiffer. Рекомендуется достаточно экономно значение тайм-ауты hello.

## <a name="next-steps"></a>Дальнейшие действия
[Обновление приложения с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) поможет вам выполнить обновление приложения с помощью PowerShell.

Управление обновлениями приложения осуществляется с помощью [параметров обновления](service-fabric-application-upgrade-parameters.md).

Обеспечить совместимость на обновление приложения путем изучения как toouse [сериализации данных](service-fabric-application-upgrade-data-serialization.md).

Узнайте, как toouse расширенные функции при обновлении приложения с помощью ссылки слишком[дополнительные разделы](service-fabric-application-upgrade-advanced.md).

Исправьте распространенных проблем в обновлений приложений с помощью ссылки действия toohello в [Устранение неполадок обновлений приложений](service-fabric-application-upgrade-troubleshooting.md).

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
