---
title: "aaaManage логику приложений в Visual Studio — приложения логики Azure | Документы Microsoft"
description: "Узнайте, как управлять приложениями логики и другими ресурсами Azure с помощью Visual Studio с помощью Visual Studio Cloud Explorer."
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>Управление приложениями логики с помощью Visual Studio Cloud Explorer

Несмотря на то что hello [портал Azure](https://portal.azure.com/) предлагает отличный способ для вас toodesign и управлять Azure логику приложения, Visual Studio Cloud Explorer можно использовать для управления много ресурсов Azure, включая логику приложения. Visual Studio Cloud Explorer позволяет просматривать, изменять и скачивать опубликованные приложения логики, а также управлять ими. К задачам управления относятся включение, отключение и просмотр журнала выполнения. 

Чтобы иметь доступ к приложениям логики в Visual Studio и управлять ими, установите и настройте перечисленные ниже инструменты Visual Studio для Azure Logic Apps. 

## <a name="prerequisites"></a>Предварительные требования

* [Visual Studio 2015 или Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* [пакет Azure SDK последней версии](https://azure.microsoft.com/downloads/) (версия 2.9.1 или выше);
* [Visual Studio Cloud Explorer](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* Web toohello доступ при использовании конструктора внедренные hello

## <a name="install-visual-studio-tools-for-logic-apps"></a>Установка инструментов Visual Studio для приложений логики

После установки необходимых компонентов hello, загрузите и установите логику приложения hello Azure Tools для Visual Studio.

1. Откройте Visual Studio. На hello **средства** последовательно выберите пункты **расширения и обновления**.
2. Разверните hello **Online** категории, можно найти в Интернете в hello коллекции Visual Studio.
3. Найдите **средства Azure Logic Apps Tools для Visual Studio**. Если потребуется, выполните поиск по названию **Logic Apps**.
4. toodownload и расширение hello установки, нажмите кнопку **загрузить**.
5. После установки перезапустите Visual Studio.

> [!NOTE]
> hello toodownload инструментов приложения логики Azure для Visual Studio перейдите непосредственно, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>Поиск приложений логики в Cloud Explorer

1.  tooopen Cloud Explorer на hello **представление** меню, выберите **Cloud Explorer**.
2.  Найдите приложение логики, используя поиск по группе ресурсов или типу ресурса. 

    * Если перейти от типа ресурса, выберите подписку Azure, разверните hello **Logic Apps** и выберите логику приложения. 
    * Если перейти по группе ресурсов, разверните группу ресурсов hello, имеет логику приложения и выберите логику приложения.

    команды tooview логику приложения, либо щелкните правой кнопкой мыши логику приложения или внизу hello Cloud Explorer, выберите пункт hello **действия** меню.

    ![Поиск приложения логики](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>Изменение приложения логики с помощью конструктора приложений логики

Из Cloud Explorer можно открыть приложение развернутой логики в hello одного конструктора, используемого в hello портал Azure. 

* tooedit логику приложения, в Cloud Explorer, щелкните правой кнопкой мыши логику приложения и выберите **открыть с помощью редактора логику приложения**. 

* toopublish облако вашей toohello обновления, выберите **публикации**. 

* Выберите новое выполнение toostart **запуска триггера**.

![Конструктор Logic Apps](./media/logic-apps-manage-from-vs/designer.png)

В конструкторе hello, вы можете также **загрузки** приложения логики. Это действие автоматически параметризует определение приложения логики hello и сохраняет определение hello в качестве шаблона развертывания диспетчера ресурсов Azure. Можно добавить этот проект группы ресурсов Azure tooyour шаблона развертывания.

## <a name="browse-your-logic-app-run-history"></a>Просмотр журнала выполнения приложения логики

журнал приложения логики выполнения hello tooview логику приложения и выберите **открыть журнал выполнения**. tooreorder историю выполнения на основе любого из заголовка столбца hello свойства отображается, выберите hello.

![Журнал выполнения](media/logic-apps-manage-from-vs/runs.png)

журнал для экземпляра выполнения, что можно просмотреть результаты, включая hello входы и выходы на каждом этапе выполнения hello hello tooshow дважды щелкните одну из hello запуска экземпляров.

![Результаты в журнале выполнения, входные и выходные данные по шагам](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>Дальнейшие действия

* [Создание приложения логики](logic-apps-create-a-logic-app.md)
* [Создание и развертывание приложений логики Azure в Visual Studio](logic-apps-deploy-from-vs.md).
* [Примеры приложений логики и распространенные сценарии](logic-apps-examples-and-scenarios.md)
* [Видео. Автоматизация бизнес-процессов с помощью Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)
* [Видео. Интеграция систем с Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
