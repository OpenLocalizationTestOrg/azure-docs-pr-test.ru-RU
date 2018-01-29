---
title: "Управление приложениями в Visual Studio | Документация Майкрософт"
description: "Используйте Visual Studio для создания, разработки, упаковки, развертывания и отладки приложений и служб Service Fabric."
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
ms.openlocfilehash: 81814ef07cfab06855b3bfbf0eb6ef51b8dfce4f
ms.sourcegitcommit: 732e5df390dea94c363fc99b9d781e64cb75e220
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/14/2017
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a>Использование Visual Studio для упрощения создания приложениями Service Fabric и управления ими
Вы можете управлять приложениями и службами Azure Service Fabric с помощью Visual Studio. Настроив [свою среду разработки](service-fabric-get-started.md), вы сможете использовать Visual Studio для создания приложений Service Fabric, добавления служб, создания пакетов, регистрации и развертывания приложений в кластере локальной разработки.

## <a name="deploy-your-service-fabric-application"></a>Развертывание приложения Service Fabric
По умолчанию развертывание приложения объединяет в одной простой операции такие действия:

1. Создание пакета приложения.
2. Загрузка пакета приложения в хранилище образов.
3. регистрация типа приложения;
4. Удаление любых запущенных экземпляров приложения.
5. Создание экземпляра приложения

В Visual Studio вы можете развернуть приложение с помощью клавиши **F5**. При этом к каждому его экземпляру будет подключен отладчик. Вы можете воспользоваться сочетанием **CTRL+F5**, чтобы развернуть приложение без отладки, или опубликовать его в локальном или удаленном кластере с помощью профиля публикации. 

### <a name="application-debug-mode"></a>Режим отладки приложения
Visual Studio предоставляет свойство, называемое **Режим отладки приложения**, которое контролирует, как в Visual Studios должно обрабатываться развертывание приложения в ходе отладки.

#### <a name="to-set-the-application-debug-mode-property"></a>Настройка свойства "Режим отладки приложения"
1. В контекстном меню проекта приложения Service Fabric (SFPROJ-файл) выберите **Свойства** или нажмите клавишу **F4**.
2. В окне **Свойства** укажите значение для свойства **Режим отладки приложения**.

![Настройка свойства "Режим отладки приложения"][debugmodeproperty]

#### <a name="application-debug-modes"></a>Режимы отладки приложения

1. **Обновить приложение.** В этом режиме можно быстро изменять и отлаживать код, а также изменять статические веб-файлы во время отладки. Этот режим работает, только если локальный кластер разработки находится в [режиме с 1 узлом](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Удалить приложение.** По завершении сеанса отладки приложение будет удалено.
3. **Автообновление.** Приложение продолжает выполняться после завершения сеанса отладки. В следующем сеансе отладки развертывание будет рассматриваться как обновление. Процесс обновления сохраняет все данные, введенные в предыдущем сеансе отладки.
4. **Сохранить приложение.** После завершения сеанса отладки приложение продолжает выполняться в кластере. В начале следующего сеанса отладки это приложение будет удалено.

Для **автоматического обновления** данные сохраняются путем применения возможностей обновления приложений Service Fabric. Дополнительные сведения об обновлении приложений и выполнении обновления в реальной среде см. в статье [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).

## <a name="add-a-service-to-your-service-fabric-application"></a>Добавление службы в приложение Service Fabric
Чтобы расширить функциональность приложения, вы можете добавить в него новые службы.  Чтобы включить службу в пакет приложения, используйте для ее добавления команду меню **Создать службу Fabric Service** .

![Добавление новой службы Service Fabric][newservice]

Выберите тип проекта Service Fabric, который нужно добавить в ваше приложение, и укажите имя службы.  Рекомендации по выбору типа службы см. в статье [Общие сведения о модели программирования Service Fabric](service-fabric-choose-framework.md).

![Выбор типа проекта службы Service Fabric для добавления в приложение][addserviceproject]

В решение и имеющийся пакет приложения добавляется новая служба. Ссылки на службы и экземпляр службы по умолчанию будут добавлены в манифест приложения, в результате чего при следующем развертывании приложения служба будет создана и запущена.

![Добавление новой службы в манифест приложения][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Создание пакета приложения Service Fabric
Чтобы развернуть приложение и входящие в него службы в кластере, необходимо создать пакет приложения.  Пакет упорядочивает манифест приложения, манифесты служб и другие необходимые файлы определенным образом.  Visual Studio размещает пакет в подкаталоге \pkg, который находится в каталоге проекта приложения.  Чтобы создать или обновить пакет приложения, в контекстном меню **Приложение** выберите пункт **Пакет**.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Удаление приложений и типов приложений с использованием Cloud Explorer
Вы можете выполнить основные операции управления кластером из среды Visual Studio, используя Cloud Explorer, который можно запустить в меню **Просмотр** . Например, вы можете удалить приложения и отменить подготовку типов приложений на локальном или удаленном кластерах.

![Удаление приложения][removeapplication]

> [!TIP]
> Сведения о расширенных функциях управления кластером см. в статье [Визуализация кластера с помощью Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
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