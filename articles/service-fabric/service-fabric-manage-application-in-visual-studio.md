---
title: "aaaManage приложений в Visual Studio | Документы Microsoft"
description: "Используйте Visual Studio toocreate, разработать пакет, развертывания и отладки Service Fabric приложений и служб."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>Используйте Visual Studio toosimplify записи и управления приложениями Service Fabric
Вы можете управлять приложениями и службами Azure Service Fabric с помощью Visual Studio. После [Настройка среды разработки](service-fabric-get-started.md), использовать приложения Service Fabric toocreate Visual Studio, добавить службы или пакета, регистр и развертывания приложений в к локальному кластеру разработки.

## <a name="deploy-your-service-fabric-application"></a>Развертывание приложения Service Fabric
По умолчанию развертывание приложения объединяет hello, выполните действия в одной простой операции:

1. Создание пакета приложения hello
2. Отправка хранилища образов toohello пакета приложения hello
3. Регистрация типа приложения hello
4. Удаление любых запущенных экземпляров приложения.
5. Создание экземпляра приложения

В Visual Studio нажав клавишу **F5** развертывает приложения и присоединения экземпляров приложения tooall hello отладчика. Можно использовать **Ctrl + F5** toodeploy приложение без отладки, или вы можете опубликовать tooa локального или удаленного кластера с помощью hello профиль публикации. Дополнительные сведения см. в разделе [публикации удаленного кластера tooa приложений с помощью Visual Studio](service-fabric-publish-app-remote-cluster.md).

### <a name="application-debug-mode"></a>Режим отладки приложения
Visual Studio предоставляет свойство с именем **режим отладки приложения**, который управляет способ развертывания приложения toohandle Visual входящим в процессе отладки.

#### <a name="tooset-hello-application-debug-mode-property"></a>hello tooset свойство режима отладки приложения
1. На hello Service Fabric проекта приложения (*.sfproj) контекстное меню, выберите **свойства** (или нажмите клавишу hello **F4** ключа).
2. В hello **свойства** окна, набор hello **режим отладки приложения** свойство.

![Настройка свойства "Режим отладки приложения"][debugmodeproperty]

#### <a name="application-debug-modes"></a>Режимы отладки приложения

1. **Обновление приложения** этот режим позволяет изменить tooquickly и отладка кода и поддерживает редактирование статического веб-файлов во время отладки. Этот режим работает, только если локальный кластер разработки находится в [режиме с 1 узлом](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Удалить приложение** причины hello toobe приложения удаляются при завершении сеанса отладки hello.
3. **Автоматическое обновление** hello приложения по-прежнему toorun при завершении сеанса отладки hello. Hello следующего сеанса отладки будет считать hello развертывания обновления. Hello процесс обновления сохраняет все данные, введенные в предыдущем сеансе отладки.
4. **Оставьте приложение** сохраняет приложения hello, работающих в кластере hello, когда hello отладки окончания сеанса. Hello начала hello следующего сеанса отладки, приложение hello будет удалено.

Для **автоматическое обновление** данные сохраняются, применяя возможности обновления приложения hello структуры службы. Дополнительные сведения об обновлении приложений и выполнении обновления в реальной среде см. в статье [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).

## <a name="add-a-service-tooyour-service-fabric-application"></a>Добавление службы tooyour приложения Service Fabric
Его функциональность можно добавить новый tooextend приложения tooyour служб.  tooensure, что служба hello включена в пакет приложения, добавить службу hello через hello **новый Service Fabric...**  элемента меню.

![Добавление новой службы Service Fabric][newservice]

Выберите приложение Service Fabric проекта типа tooadd tooyour и укажите имя для службы hello.  В разделе [выборе платформы для службы](service-fabric-choose-framework.md) toohelp, решите, какие службы введите toouse.

![Выберите приложение Service Fabric тип проекта службы tooadd tooyour][addserviceproject]

Новая служба Hello добавляется решение tooyour и существующий пакет приложения. ссылки на службу Hello и экземпляра службы по умолчанию будут добавлены toohello манифест приложения, вызывающие toobe hello службы создается и запускается hello в следующий раз при развертывании приложения hello.

![Новая служба Hello добавляется tooyour манифест приложения][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Создание пакета приложения Service Fabric
toodeploy приложения hello и ее служб tooa кластер, необходимо toocreate пакета приложения.  пакет Hello организует манифест приложения hello, манифесты службы и другие необходимые файлы в определенном формате.  Visual Studio настраивает и управляет hello пакета в папку проекта приложения hello, в каталоге «pkg» hello.  Щелкнув **пакета** из hello **приложения** создает контекстного меню или обновления hello пакета приложения.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Удаление приложений и типов приложений с использованием Cloud Explorer
Можно выполнять операции управления базовый кластер из среды Visual Studio с помощью Cloud Explorer, который можно открыть из hello **представление** меню. Например, вы можете удалить приложения и отменить подготовку типов приложений на локальном или удаленном кластерах.

![Удаление приложения][removeapplication]

> [!TIP]
> Сведения о расширенных функциях управления кластером см. в статье [Визуализация кластера с помощью Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
* [Модель приложений Service Fabric](service-fabric-application-model.md)
* [Развертывание приложений Service Fabric](service-fabric-deploy-remove-applications.md)
* [Управление параметрами приложения для нескольких сред](service-fabric-manage-multiple-environment-app-configuration.md)
* [Отладка приложений Service Fabric](service-fabric-debugging-your-application.md)
* [Визуализация кластера с помощью обозревателя Service Fabric](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png