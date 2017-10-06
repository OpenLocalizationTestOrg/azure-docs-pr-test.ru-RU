---
title: "aaaHow toouse SendGrid в функциях Azure | Документы Microsoft"
description: "Показано, как toouse SendGrid в функциях Azure"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a><span data-ttu-id="7241d-103">Как toouse SendGrid в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="7241d-103">How toouse SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="7241d-104">Общие сведения о SendGrid</span><span class="sxs-lookup"><span data-stu-id="7241d-104">SendGrid Overview</span></span>

<span data-ttu-id="7241d-105">Azure поддерживает функции SendGrid вывода tooenable привязки функции toosend сообщений электронной почты с помощью нескольких строк кода и учетной записи SendGrid.</span><span class="sxs-lookup"><span data-stu-id="7241d-105">Azure Functions supports SendGrid output bindings tooenable your functions toosend email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="7241d-106">hello toouse SendGrid API-Интерфейс в функции Azure, должен иметь [учетной записи SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="7241d-106">toouse hello SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="7241d-107">А также необходимо иметь ключ API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="7241d-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="7241d-108">Войдите в учетной записи SendGrid tooyour и нажмите **параметры** затем **ключ API** toogenerate API-ключ.</span><span class="sxs-lookup"><span data-stu-id="7241d-108">Log in tooyour SendGrid account and click **Settings** then **API Key** toogenerate an API key.</span></span> <span data-ttu-id="7241d-109">Сохраните этот ключ, так как он потребуется на последующем шаге.</span><span class="sxs-lookup"><span data-stu-id="7241d-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="7241d-110">Теперь вы находитесь готов toocreate Azure функции приложения.</span><span class="sxs-lookup"><span data-stu-id="7241d-110">You are now ready toocreate an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="7241d-111">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="7241d-111">Create an Azure Function app</span></span> 

<span data-ttu-id="7241d-112">Приложения-функции Azure являются контейнерами для одной или нескольких функций Azure.</span><span class="sxs-lookup"><span data-stu-id="7241d-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="7241d-113">Функции Azure являются именно функциями.</span><span class="sxs-lookup"><span data-stu-id="7241d-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="7241d-114">Каждая функция Azure — связанные tooone срабатывание триггера, который представляет событие, вызывающее toorun функции hello.</span><span class="sxs-lookup"><span data-stu-id="7241d-114">Each Azure function is tied tooone trigger, which is an event that causes hello function toorun.</span></span>
<span data-ttu-id="7241d-115">Каждая функция может содержать любое количество входных или выходных привязок.</span><span class="sxs-lookup"><span data-stu-id="7241d-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="7241d-116">Привязки — это службы, которые можно использовать в функции.</span><span class="sxs-lookup"><span data-stu-id="7241d-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="7241d-117">Выходные данные, то можно использовать toosend электронной почты — SendGrid.</span><span class="sxs-lookup"><span data-stu-id="7241d-117">SendGrid is an output binding you can use toosend email.</span></span> 

1. <span data-ttu-id="7241d-118">Войдите в портал Azure toohello и [создать приложение Azure функция](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) или открывать существующие приложения для функции.</span><span class="sxs-lookup"><span data-stu-id="7241d-118">Log in toohello Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="7241d-119">Создайте функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="7241d-119">Create an Azure function.</span></span> <span data-ttu-id="7241d-120">tookeep простым, выберите ручной триггера и C#.</span><span class="sxs-lookup"><span data-stu-id="7241d-120">tookeep it simple, choose a manual trigger and C#.</span></span> 

 ![Создание функции Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="7241d-122">Настройка SendGrid для использования в приложении-функции Azure</span><span class="sxs-lookup"><span data-stu-id="7241d-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="7241d-123">Необходимо хранить свой ключ API SendGrid как параметр приложения toouse его в функции.</span><span class="sxs-lookup"><span data-stu-id="7241d-123">You must store your SendGrid API Key as an app setting toouse it in a function.</span></span> <span data-ttu-id="7241d-124">поле ApiKey Hello не фактические SendGrid API-ключ, но параметр приложения определить, представляет фактический ключ API.</span><span class="sxs-lookup"><span data-stu-id="7241d-124">hello ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="7241d-125">Такое хранение ключа способствует обеспечению безопасности, так как ключ отделен от кода и файлов, которые могут быть возвращены в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="7241d-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="7241d-126">Создайте ключ **AppSettings** в **параметрах** приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="7241d-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Создание функции Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="7241d-128">Настройка выходных привязок SendGrid</span><span class="sxs-lookup"><span data-stu-id="7241d-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="7241d-129">Привязка SendGrid доступна как выходная привязка функции Azure.</span><span class="sxs-lookup"><span data-stu-id="7241d-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="7241d-130">Привязка для вывода toocreate SendGrid:</span><span class="sxs-lookup"><span data-stu-id="7241d-130">toocreate a SendGrid output binding:</span></span>

1. <span data-ttu-id="7241d-131">Go toohello **Интеграция** вкладку функции hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7241d-131">Go toohello **Integrate** tab of hello function in hello Azure portal.</span></span>
2. <span data-ttu-id="7241d-132">Нажмите кнопку **новый Выход** toocreate SendGrid привязка для вывода.</span><span class="sxs-lookup"><span data-stu-id="7241d-132">Click **New Output** toocreate a SendGrid output binding.</span></span>
3. <span data-ttu-id="7241d-133">Заполните hello **ключ API** и **имя параметра сообщение** свойства.</span><span class="sxs-lookup"><span data-stu-id="7241d-133">Fill in hello **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="7241d-134">Если требуется, можно ввести теперь hello других свойств или их вместо этого кода.</span><span class="sxs-lookup"><span data-stu-id="7241d-134">If you want, you can enter hello other properties now, or code them instead.</span></span> <span data-ttu-id="7241d-135">Приведенные здесь параметры можно использовать как значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7241d-135">These settings can be used as defaults.</span></span>

 ![Настройка выходных привязок SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="7241d-137">Добавление функции tooa привязки создает файл с именем **function.json** в папке ваша функция.</span><span class="sxs-lookup"><span data-stu-id="7241d-137">Adding a binding tooa function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="7241d-138">Этот файл содержит все же информация, отображаемая в hello Azure функции hello **Интеграция** вкладки, но в формате Json форматирования.</span><span class="sxs-lookup"><span data-stu-id="7241d-138">This file contains all hello same information that you see in hello Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="7241d-139">Параметр hello **ApiKey**, **сообщение**, и **из** поля создать следующие записи в hello hello **function.json** файла:</span><span class="sxs-lookup"><span data-stu-id="7241d-139">Setting hello **ApiKey**, **message**, and **from** fields create hello following entries in hello **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="7241d-140">При желании вы можете изменить этот файл самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="7241d-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="7241d-141">Теперь, создания и настройки функции приложения hello и функции можно написать toosend кода hello сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7241d-141">Now that you have created and configured hello Function App and function, you can write hello code toosend an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="7241d-142">Написание кода, который создает и отправляет электронную почту</span><span class="sxs-lookup"><span data-stu-id="7241d-142">Write code that creates and sends email</span></span>

<span data-ttu-id="7241d-143">Hello SendGrid API содержит все команды hello требуется toocreate и отправить сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7241d-143">hello SendGrid API contains all hello commands you need toocreate and send an email.</span></span>  

- <span data-ttu-id="7241d-144">Замените код hello в функции hello hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="7241d-144">Replace hello code in hello function with hello following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="7241d-145">Первая строка hello уведомления содержит hello ```#r``` директиву, которая ссылается на сборку SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="7241d-145">Notice hello first line contains hello ```#r``` directive that references hello SendGrid assembly.</span></span> <span data-ttu-id="7241d-146">После этого можно использовать ```using``` toomore инструкции легко получить доступ к объектам hello в этом пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="7241d-146">After that, you can use a ```using``` statement toomore easily access hello objects in that namespace.</span></span> <span data-ttu-id="7241d-147">Создайте в коде hello экземпляров ```Mail```, ```Personalization```, и ```Content``` объектов из hello SendGrid API, Создание электронного сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="7241d-147">In hello code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from hello SendGrid API that compose hello email.</span></span> <span data-ttu-id="7241d-148">При возврате приветственное сообщение SendGrid доставляет его.</span><span class="sxs-lookup"><span data-stu-id="7241d-148">When you return hello message, SendGrid delivers it.</span></span> 

<span data-ttu-id="7241d-149">Hello сигнатуру функции также содержит дополнительный параметр типа out ```Mail``` с именем ```message```.</span><span class="sxs-lookup"><span data-stu-id="7241d-149">hello function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="7241d-150">Как входные, так и выходные привязки выражаются в коде как параметры функции.</span><span class="sxs-lookup"><span data-stu-id="7241d-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="7241d-151">Тестирование кода, щелкнув **теста** и ввода сообщения в hello **текст запроса** поля, а затем щелкнуть hello **запуска** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7241d-151">Test your code by clicking **Test** and entering a message into hello **Request body** field, then clicking hello **Run** button.</span></span>

 ![Тестирование кода](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="7241d-153">Проверьте, SendGrid отправлены по электронной почте hello tooverify электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7241d-153">Check email tooverify that SendGrid sent hello email.</span></span> <span data-ttu-id="7241d-154">Он должен перейти toohello адрес в коде hello из шага 1 и содержать приветственное сообщение из hello **текст запроса**.</span><span class="sxs-lookup"><span data-stu-id="7241d-154">It should go toohello address in hello code from step 1, and contain hello message from hello **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7241d-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7241d-155">Next steps</span></span>
<span data-ttu-id="7241d-156">В этой статье показана как toouse hello toocreate SendGrid службы и отправить по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="7241d-156">This article has demonstrated how toouse hello SendGrid service toocreate and send email.</span></span> <span data-ttu-id="7241d-157">toolearn Подробнее об использовании функций Azure в приложениях см. в разделе hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="7241d-157">toolearn more about using Azure Functions in your apps, see hello following topics:</span></span> 

- <span data-ttu-id="7241d-158">[Советы и рекомендации для функций Azure](functions-best-practices.md) приведены некоторые советы и рекомендации toouse при создании функций Azure.</span><span class="sxs-lookup"><span data-stu-id="7241d-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="7241d-159">[Руководство для разработчиков по Функциям Azure](functions-reference.md). Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="7241d-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="7241d-160">[Тестирование функций Azure](functions-test-a-function.md). Описание различных средств и методов тестирования функций.</span><span class="sxs-lookup"><span data-stu-id="7241d-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>