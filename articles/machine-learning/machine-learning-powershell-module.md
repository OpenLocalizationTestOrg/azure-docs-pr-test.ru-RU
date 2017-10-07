---
title: "модуль aaaPowerShell для машинного обучения | Документы Microsoft"
description: "модуль PowerShell Hello для машинного обучения Azure доступна в режиме общедоступной предварительной версии. Использование PowerShell toocreate и управления рабочими областями, экспериментов, веб-службы и многое другое."
keywords: "эксперимент,линейная регрессия,алгоритмы машинного обучения,руководство по машинному обучению,приемы прогнозного моделирования,эксперимент по обработке и анализу данных"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>Модуль PowerShell для машинного обучения Microsoft Azure
модуль PowerShell Hello для машинного обучения Azure — мощное средство, позволяющее workspaces toomanage toouse Windows PowerShell, экспериментов, наборы данных, классического веб-службы и многое другое.

Можно просматривать документацию hello и загрузить модуль hello, а также hello полный исходный код, на [https://aka.ms/amlps](https://aka.ms/amlps). 

> [!NOTE]
> Hello Azure Machine Learning PowerShell в настоящее время доступен в режиме предварительного просмотра. Hello модуль по-прежнему toobe улучшены и развернуты в течение этого периода предварительной версии. Обратите внимание на hello [Cortana аналитики и блог обучения машины](https://blogs.technet.microsoft.com/machinelearning/) новости и информация.

## <a name="what-is-hello-machine-learning-powershell-module"></a>Что такое модуль PowerShell обучения машины hello
модуль PowerShell обучения машины Hello. На основе NET модуль DLL, позволяющий toofully управление рабочие области машинного обучения Azure, экспериментов, наборы данных, классического веб-служб и конечных точек службы web классический из Windows PowerShell. 

Вместе с модулем hello можно загрузить hello полный исходный код, который включает в себя полностью разделенными [уровень API C#](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs). На эту библиотеку DLL можно ссылаться из собственного проекта .NET, а также управлять машинным обучением Azure с помощью кода .NET. Кроме того hello DLL зависит от базовые интерфейсы API REST, который можно использовать напрямую из клиента.

## <a name="what-can-i-do-with-hello-powershell-module"></a>Что можно делать с модулем PowerShell hello
Ниже приведены некоторые задачи hello, которые можно выполнять с помощью этот модуль PowerShell. Извлечение hello [Полная документация](https://aka.ms/amlps) эти и многие другие функции.

* Подготовка новой рабочей области с помощью сертификата управления ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace)).
* Экспорт и импорт файла JSON, представляющего граф эксперимента ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) и [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph)).
* Запуск эксперимента ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment)).
* Создание веб-службы из прогнозного эксперимента ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice)).
* Создание конечной точки в опубликованной веб-службе ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint)).
* Вызов конечной точки веб-службы BES и (или) RRS ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) и [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint)).

Ниже приведен краткий пример использования PowerShell toorun эксперимента существующих:

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

Для более подробного варианта использования, см. статью на использование tooautomate модуль PowerShell hello задачи часто запрашиваемые: [создать много машинного обучения моделей и веб-конечные точки службы из одной эксперимента с помощью PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).

## <a name="how-do-i-get-started"></a>Как начать работу?
tooget к работе с PowerShell машины обучения, загрузите hello [пакета выпуска](https://github.com/hning86/azuremlps/releases) из GitHub и следовать hello [инструкции по установке](https://github.com/hning86/azuremlps/blob/master/README.md). инструкции Hello объясняется, как toounblock hello загружен/распаковал DLL и затем импортировать его в среде PowerShell. Большая часть приветствия командлетов необходимо указать идентификатор рабочей области hello, маркер авторизации hello рабочей области и hello регионе Azure, которая hello рабочей области находится в. Hello простейший способ tooprovide hello значения выполняется с помощью файла config.json по умолчанию. Hello инструкции также объясняется, как tooconfigure этот файл. 

Если требуется, можно клонировать дерево git hello, изменения кода hello и скомпилировать его локально с помощью Visual Studio.

## <a name="next-steps"></a>Дальнейшие действия
Можно найти hello Полная документация для модуля PowerShell hello в [https://aka.ms/amlps](https://aka.ms/amlps). 

Расширенный пример как toouse hello модуля в реальном сценарии, извлечение hello подробные использовать регистр, [создать много машинного обучения моделей и веб-конечные точки службы из одной эксперимента с помощью PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).
