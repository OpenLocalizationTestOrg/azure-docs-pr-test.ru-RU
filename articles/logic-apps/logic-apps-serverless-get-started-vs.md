---
title: "aaaBuild без сервера приложений в Visual Studio | Документы Microsoft"
description: "Начало работы с первым приложением без сервера с помощью этого руководства по созданию, развертыванию и управлению приложение hello в Visual Studio."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Создание бессерверного приложения в Visual Studio с использованием приложений логики и функций

Средства и возможности по созданию бессерверных приложений в Azure позволяют быстро создавать и развертывать облачные приложения.  В этом документе основное внимание уделено tooget работы в Visual Studio, построение без сервера приложения.  Обзор бессерверных приложений в Azure можно найти в [этой статье](logic-apps-serverless-overview.md).

## <a name="getting-everything-ready"></a>Подготовка

Ниже приведены предварительные требования toobuild hello без сервера приложения из Visual Studio.

* [Visual Studio 2017](https://www.visualstudio.com/vs/) или Visual Studio 2015 — выпуски Community, Professional или Enterprise
* [Средства приложений логики для Visual Studio](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [пакет Azure SDK последней версии](https://azure.microsoft.com/downloads/) (версия 2.9.1 или выше);
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Основные инструменты Azure функции](https://www.npmjs.com/package/azure-functions-core-tools) toodebug работает локально
* Веб-toohello доступ при использовании hello внедренного конструктор логику приложения

## <a name="getting-started-with-a-deployment-template"></a>Приступая к работе с шаблоном развертывания

Управление ресурсами в Azure осуществляется в группе ресурсов.  Группа ресурсов — это логическое объединение ресурсов.  Группы ресурсов позволяют развертывать наборы ресурсов и управлять ими.  Наша группа ресурсов для бессерверного приложения в Azure содержит как приложения логики Azure, так и функции Azure.  С помощью hello проекта группы ресурсов в среде Visual Studio, мы получаем доступ toodevelop, управление и развертывание всего приложения hello как одного ресурса.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Создание проекта группы ресурсов в Visual Studio

1. В Visual Studio щелкните tooadd **нового проекта**
1. В hello **облака** категории, выберите toocreate Azure **группы ресурсов** проекта  
 * Если вы не видите hello категории или проект служб, убедитесь, что у вас есть hello пакет Azure SDK для Visual Studio
1. Задайте hello проекта имя и расположение, а затем выберите **ОК** toocreate Visual Studio предлагает tooselect шаблона.  Можно выбрать toostart пустое, начинаются с логикой приложения или других ресурсов.  Однако в этом случае мы используем примеры использования шаблона Azure tooget нам работу с приложением без сервера.
1. Выберите шаблоны tooshow из **быстрый запуск Azure** ![шаблонов при выборе быстрый запуск Azure][1]
1. Шаблон SELECT hello без сервера краткое руководство: **101-logic-app-and-function-app** и нажмите кнопку **ОК**

Шаблон краткого руководства Hello создает шаблон развертывания проекта группы ресурсов.  шаблон Hello содержит простое приложение логики, вызывает функции Azure и возвращает результат hello.  При открытии hello `azuredeploy.json` Здравствуйте, файл в обозревателе решений, можно будет увидеть hello ресурсы для приложения без сервера hello.

## <a name="deploying-hello-serverless-application"></a>Развертывание приложения без сервера hello

Перед открытием визуальный конструктор hello логику приложения в Visual Studio должен toobe предварительном развертывании группы ресурсов Azure.  Это позволяет toocreate конструктора hello и tooresources использование соединений и службы в приложение логику hello.  tooget к работе, мы просто toodeploy hello решении создан.

1. Щелкните правой кнопкой мыши проект hello в Visual Studio, выберите пункт **развернуть**и создать **New** развертывания ![выбрав новое развертывание ресурсов][2]
1. Выберите действительную подписку Azure и группу ресурсов.
1. Выберите также**развернуть** hello решения
1. Введите имя hello hello логику приложения и приложения Azure функции hello.  имя функции Azure Hello требуется toobe глобально уникальным

решение без сервера Hello развертывает в hello определенной группе ресурсов.  Если взглянуть на hello **выходной** в Visual Studio можно просмотреть состояние hello hello развертывания.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Редактирование hello логику приложения в Visual Studio

После развертывания решения hello в любую группу ресурсов hello визуальный конструктор можно использовать tooedit и внести изменения toohello логику приложения.

1. Щелкните правой кнопкой мыши hello `azuredeploy.json` в hello в обозревателе решений и выберите **открыть с логикой приложения конструктор**
1. Выберите hello **группы ресурсов** и **расположение** hello решение являлось развертывания выберите tooand **ОК**

визуальный конструктор логику приложения Hello, теперь должны быть видимыми вместе с Visual Studio.  Выполните шаги tooadd, измените рабочий hello и сохранить изменения.  Вы также можете создавать приложения логики в Visual Studio.  Если щелкнуть правой кнопкой мыши hello **ресурсов** в навигаторе hello шаблона, можно выбрать tooadd **приложения логики** toohello проекта.  Загрузить пустой логику приложения в визуальном конструкторе hello без предварительно развернуть в группе ресурсов.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>Просмотр журнала выполнения и управление им для развернутого приложения логики

Можно также управлять и просмотреть журнал выполнения hello для логики приложений, развернутых в Azure.  При открытии hello **Cloud Explorer** средства в Visual Studio щелкните правой кнопкой мыши любой логики приложения и выберите tooedit, отключить, просмотр свойств или журнал выполнения представления.  Нажав кнопку Изменить также позволяет toodownload приложения опубликованных логики в проект группы ресурсов Visual Studio.  Это означает, что даже если запущен построение логики приложения в hello портал Azure, его можно по-прежнему импортировать и управлять из Visual Studio.

## <a name="developing-an-azure-function-in-visual-studio"></a>Разработка функции Azure в Visual Studio

Hello шаблон развертывания развертывает какие-либо функции Azure, которые содержатся в решении hello для репозитория git hello, указанный в hello `azuredeploy.json` переменных.  При создании проекта в решение hello функция вернуть его в систему управления версиями (GitHub, Visual Studio Team Services, т. д.) и обновить hello `repo` переменной шаблона hello развернет hello Azure функции.

### <a name="creating-an-azure-function-project"></a>Создание проекта функции Azure

Если с помощью JavaScript, Python, F #, Bash, пакет или PowerShell, выполните hello [шагов в hello CLI функции](../azure-functions/functions-run-local.md) toocreate проекта.  Если разработка функции в C#, можно использовать [библиотеки классов C#](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) в текущем решении hello для hello Azure функции.

## <a name="next-steps"></a>Дальнейшие действия

* [Узнайте, как toobuild без сервера социальных панели мониторинга](logic-apps-scenario-social-serverless.md)
* [Управление приложениями логики из Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Язык определения рабочего процесса приложений логики](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
