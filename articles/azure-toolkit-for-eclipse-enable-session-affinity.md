---
title: "Здравствуйте, aaaEnable сходство сеансов с помощью средств Azure для Eclipse"
description: "Узнайте, как hello tooenable сходство сеанса с помощью средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>Включение сходства сеансов
В hello средств Azure для Eclipse можно включить соответствие сеанса HTTP или «закрепленные сеансы» для ваших ролей. Hello на рисунке показаны hello **балансировки нагрузки** функции соответствия сеанса hello tooenable использование диалогового окна свойств:

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>сходство сеансов tooenable для роли
1. Щелкните правой кнопкой мыши роль hello в обозревателе проектов Eclipse, щелкните **Azure**, а затем нажмите кнопку **балансировки нагрузки**.

2. В hello **свойства для балансировки нагрузки WorkerRole1** диалогового окна:

   а. Установите флажок **Enable HTTP session affinity (sticky sessions) for this role**

   b. Для **входной конечной точки toouse**, выберите toouse входную конечную точку, например, **http (общедоступный: 80, частный: 8080)**. Ваше приложение должно использовать эту конечную точку в качестве своей конечной точки HTTP. Можно включить несколько конечных точек для роли, но можно выбрать только один из них toosupport закрепленных сеансов.

   c. Перестройте приложение.

После включения, если имеется более одного экземпляра роли, HTTP-запросы, поступающие от конкретного клиента продолжит обрабатываются hello же экземпляра роли.

Hello средств Eclipse позволяет сделать это путем установки специального модуля IIS маршрутизации запросов приложений (ARR) в каждый из экземпляров ролей. ARR перенаправляет HTTP запросы toohello соответствующий экземпляр роли. набор средств Hello автоматически настроит hello выбранной конечной точки, таким образом, чтобы входящий трафик HTTP hello первый ARR перенаправленное toohello программного обеспечения. набор средств Hello также создает новую внутреннюю конечную точку, toolisten, настроенных на сервере Java. Это hello конечная точка, используемая с ARR tooreroute hello HTTP трафика toohello соответствующий экземпляр роли. Таким образом, каждый экземпляр роли в развертывании с несколькими экземплярами служит в качестве обратного прокси-сервера для всех hello других экземпляров, включая закрепленные сеансы.

## <a name="notes-about-session-affinity"></a>Заметки о сходстве сеансов
* Соответствие сеанса не работает в эмуляторе вычислений hello. Параметры Hello может применяться в эмуляторе вычислений hello, не нарушая процесса построения или выполнения эмулятора вычислений, но сама функция hello не работает в эмуляторе вычислений hello.

* Включение соответствия сеанса приведет к увеличению hello объем дискового пространства, занимаемого развертыванием в Azure, как дополнительное программное обеспечение будет загружен и установлен в экземпляры роли, при запуске службы в облаке Azure hello.

* время tooinitialize Hello каждой роли займет больше времени.

* Внутренняя конечная точка, toofunction перенаправления трафика, как было сказано выше, будут добавлены.


## <a name="see-also"></a>См. также
[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]

[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
