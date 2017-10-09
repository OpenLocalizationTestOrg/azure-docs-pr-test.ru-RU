---
title: "aaaDevelop функции Azure с помощью Visual Studio | Документы Microsoft"
description: "Узнайте, как функции Azure toodevelop и тестирования с помощью функции средств Azure для Visual Studio 2017 г."
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a>Инструменты Функций Azure для Visual Studio  

Средства Azure функции для Visual Studio 2017 г. — это расширение Visual Studio, которое позволяет разрабатывать, тестировать и развертывать tooAzure функции C#. Если это ваш первый опыт работы с Azure функции, Дополнительные сведения в [tooAzure введение функции](functions-overview.md).

Hello функции средства Azure предоставляет hello следующие преимущества: 

* Создание, редактирование и выполнение функций на локальном компьютере для разработки. 
* Публикация функций Azure непосредственно проект tooAzure. 
* Используйте веб-задания атрибутов toodeclare функции привязки непосредственно в hello кода C# вместо обслуживание отдельных function.json для определений привязки.
* Разработка и развертывание предварительно скомпилированных функций C#. Предварительно скомпилированные функции обеспечивают более высокую производительность при холодном запуске, чем функции C# на основе сценариев. 
* Код функций в C#, имея все преимущества hello разработки Visual Studio. 

В этом разделе показано, как toouse hello функции средства Azure для Visual Studio 2017 г toodevelop функций в C#. Вы также узнаете, как toopublish tooAzure ваш проект как сборку .NET.

## <a name="prerequisites"></a>Предварительные требования

Инструменты Azure функции входит в рабочую нагрузку разработки Azure hello [Visual Studio 2017 г. версия 15,3](https://www.visualstudio.com/vs/), или более поздней версии. Не забудьте поставить hello **разработки Azure** рабочей нагрузки в вашей установке версии 15,3 2017 г. Visual Studio:

![Установка Visual Studio 2017 г. с помощью рабочей нагрузки для разработки Azure hello](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

toocreate и развернуть функции, необходимо также:

* Активная подписка Azure. Если у вас нет подписки Azure, воспользуйтесь [бесплатными учетными записями](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

* Учетная запись хранения Azure. toocreate учетной записи хранения в разделе [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
## <a name="create-an-azure-functions-project"></a>Создание проекта Функций Azure 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a>Настройка проекта hello для локальной разработки

При создании нового проекта с помощью шаблона Azure функции hello, вы получаете пустой проект C#, содержащий hello следующие файлы:

* **Host.JSON**: позволяет настроить hello узла функции. Эти параметры применяются как в локальном режиме, так и в Azure. Дополнительные сведения см. в справочной статье о [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).
    
* **local.settings.json**: содержит параметры, используемые при выполнении функций локально. Эти параметры не используются в Azure, они используются hello [основные инструменты Azure функции](functions-run-local.md). Используйте этот файл toospecify параметры, такие как строки соединения tooother Azure службы. Добавление нового ключа toohello **значения** массива для каждого соединения, необходимые для функции в проекте. Дополнительные сведения см. в разделе [параметры локального файла](functions-run-local.md#local-settings-file) в разделе Основные инструменты Azure функции hello.

Учетная запись хранилища Azure использует время выполнения функции Hello для внутренних целей. Для всех инициировать типам, отличным от HTTP и веб-привязок, необходимо задать hello **Values.AzureWebJobsStorage** ключа tooa допустимую хранилища Azure строку подключения для учетной записи.

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 Строка подключения учетной записи хранилища hello tooset:

1. В Visual Studio откройте **Cloud Explorer**, разверните **учетной записи хранилища** > **учетной записи хранения**, а затем выберите **свойства**и копирования hello **основной строка подключения** значение.   

2. В проекте откройте файл проекта local.settings.json hello и задайте значение hello hello **AzureWebJobsStorage** toohello строку подключения, вы скопировали ключ.

3. Повторите hello предыдущего шага tooadd уникальные ключи toohello **значения** массива для других соединений, необходимые для функций.  

## <a name="create-a-function"></a>Создание функции

В предварительно скомпилированного функции hello привязки, используемые функцией hello определяются путем применения атрибутов в коде hello. При использовании функций на основе шаблонов, предоставляемых hello toocreate средства Azure функции hello эти атрибуты применяются автоматически. 

1. Щелкните правой кнопкой мыши узел проекта в **обозревателе решений** и выберите **Добавить** > **Новый элемент**. Выберите **функция Azure**, введите команду **имя** hello класса, а затем щелкните **добавить**.

2. Выберите код триггера, задать свойства привязки hello и нажмите кнопку **создать**. Hello пример hello параметры при создании хранилища очередей активации функции. 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    Ключ строки подключения с именем **QueueStorage** предоставляется, которая определена в файле local.settings.json hello. 
 
3. Изучите hello добавления класса. Вы видите статический **запуска** методы, к которым имеет атрибут hello **FunctionName** атрибута. Этот атрибут указывает на то, что метод hello hello точки входа для функции hello. 

    Например hello следующий класс C# представляет основной функции хранения активации очереди:

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    Привязки особый атрибут имеет метод точки входа toohello указан параметр примененных tooeach привязки. атрибут Hello принимает сведения о привязке hello в качестве параметров. В предыдущем примере hello hello первый параметр имеет **QueueTrigger** применен атрибут, указывающий функцию активации очереди. Имя очереди Hello и имя параметра строки соединения, передаются как параметры.  

## <a name="testing-functions"></a>Функции тестирования

Основные инструменты службы Функции Azure позволяют запускать проекты функций Azure на локальном компьютере разработчика. Все запрашиваемые tooinstall, эти средства hello первом запуске функции из Visual Studio.  

tootest работу, нажмите клавишу F5. При необходимости принятия запроса hello из Visual Studio toodownload и установить средства основных функций Azure (CLI).  Может также потребоваться tooenable исключение брандмауэра, чтобы средства hello можно обрабатывать HTTP-запросы.

С проектом hello под управлением можно проверить код как тестируется развернутой функции. Дополнительные сведения см. в статье [Методика тестирования кода с помощью Функций Azure](functions-test-a-function.md). При работе в режиме отладки точки останова срабатывают в Visual Studio должным образом. 

Пример запуска функции tootest очереди, разделе hello [очередь запускается функция краткого руководства](functions-create-storage-queue-triggered-function.md#test-the-function).  

toolearn Подробнее об использовании hello Azure функции основные инструменты в разделе [кода и тестирования функций Azure локально](functions-run-local.md).

## <a name="publish-tooazure"></a>Публикация tooAzure

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
>Все параметры, которые вы добавили в hello local.settings.json необходимо также добавить toohello функции приложения в Azure. Эти параметры не добавляются автоматически. Необходимые параметры tooyour функции приложения можно добавить одним из следующих способов:
>
>* [Здравствуйте, с помощью портала Azure](functions-how-to-use-azure-function-app-settings.md#settings).
>* [С помощью hello `--publish-local-settings` публикации параметр в hello основные инструменты Azure функции](functions-run-local.md#publish).
>* [С помощью hello Azure CLI](/cli/azure/functionapp/config/appsettings#set). 

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о функции инструменты Azure, см. в разделе hello разделе вопросы hello "Общие" [2017 г средств Visual Studio для функций Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) записи блога.

toolearn Дополнительные сведения о средствах основные функции hello Azure, в разделе [кода и тестирования функций Azure локально](functions-run-local.md).  
toolearn Дополнительные сведения о разработке функции как библиотеки классов .NET, в разделе [библиотеки классов с помощью .NET с помощью функций Azure](functions-dotnet-class-library.md). В этом разделе также приведены примеры как атрибуты toodeclare toouse hello различные типы привязок, поддерживаемых функций Azure.    
