---
title: "Использование SendGrid в Функциях Azure | Документация Майкрософт"
description: "Здесь описывается, как использовать SendGrid в Функциях Azure"
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
ms.openlocfilehash: 05c9f4e4a4351219da68af8b702c25f21d7d4d02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-sendgrid-in-azure-functions"></a><span data-ttu-id="8d9f7-103">Использование SendGrid в Функциях Azure</span><span class="sxs-lookup"><span data-stu-id="8d9f7-103">How to use SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="8d9f7-104">Общие сведения о SendGrid</span><span class="sxs-lookup"><span data-stu-id="8d9f7-104">SendGrid Overview</span></span>

<span data-ttu-id="8d9f7-105">Функции Azure поддерживают выходные привязки SendGrid, позволяя вашим функциям отправлять сообщения электронной почты с помощью нескольких строк кода и учетной записи SendGrid.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-105">Azure Functions supports SendGrid output bindings to enable your functions to send email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="8d9f7-106">Чтобы использовать API SendGrid в функции Azure, необходимо иметь [учетную запись SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="8d9f7-106">To use the SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="8d9f7-107">А также необходимо иметь ключ API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="8d9f7-108">Чтобы создать ключ API, войдите в учетную запись SendGrid и выберите **Параметры**, а затем — **Ключ API**.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-108">Log in to your SendGrid account and click **Settings** then **API Key** to generate an API key.</span></span> <span data-ttu-id="8d9f7-109">Сохраните этот ключ, так как он потребуется на последующем шаге.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="8d9f7-110">Теперь вы готовы создать приложение-функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-110">You are now ready to create an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="8d9f7-111">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="8d9f7-111">Create an Azure Function app</span></span> 

<span data-ttu-id="8d9f7-112">Приложения-функции Azure являются контейнерами для одной или нескольких функций Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="8d9f7-113">Функции Azure являются именно функциями.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="8d9f7-114">Каждая функция Azure связана с одним триггером, который является событием, инициирующим запуск функции.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-114">Each Azure function is tied to one trigger, which is an event that causes the function to run.</span></span>
<span data-ttu-id="8d9f7-115">Каждая функция может содержать любое количество входных или выходных привязок.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="8d9f7-116">Привязки — это службы, которые можно использовать в функции.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="8d9f7-117">SendGrid — это выходная привязка, которую можно использовать для отправки электронной почты.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-117">SendGrid is an output binding you can use to send email.</span></span> 

1. <span data-ttu-id="8d9f7-118">Войдите на портал Azure и [создайте приложение-функцию Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) или откройте существующее приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-118">Log in to the Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="8d9f7-119">Создайте функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-119">Create an Azure function.</span></span> <span data-ttu-id="8d9f7-120">Для простоты выберите ручной триггер и C#.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-120">To keep it simple, choose a manual trigger and C#.</span></span> 

 ![Создание функции Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="8d9f7-122">Настройка SendGrid для использования в приложении-функции Azure</span><span class="sxs-lookup"><span data-stu-id="8d9f7-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="8d9f7-123">Чтобы использовать ключ API SendGrid в функции, необходимо сохранить его как параметр приложения.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-123">You must store your SendGrid API Key as an app setting to use it in a function.</span></span> <span data-ttu-id="8d9f7-124">Поле ApiKey является не фактическим ключом API SendGrid, а определяемым вами параметром приложения, который представляет фактический ключ API.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-124">The ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="8d9f7-125">Такое хранение ключа способствует обеспечению безопасности, так как ключ отделен от кода и файлов, которые могут быть возвращены в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="8d9f7-126">Создайте ключ **AppSettings** в **параметрах** приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Создание функции Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="8d9f7-128">Настройка выходных привязок SendGrid</span><span class="sxs-lookup"><span data-stu-id="8d9f7-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="8d9f7-129">Привязка SendGrid доступна как выходная привязка функции Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="8d9f7-130">Чтобы создать выходную привязку SendGrid, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8d9f7-130">To create a SendGrid output binding:</span></span>

1. <span data-ttu-id="8d9f7-131">Перейдите на вкладку **Интегрировать** функции на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-131">Go to the **Integrate** tab of the function in the Azure portal.</span></span>
2. <span data-ttu-id="8d9f7-132">Чтобы создать выходную привязку SendGrid, щелкните **Новое выходное значение**.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-132">Click **New Output** to create a SendGrid output binding.</span></span>
3. <span data-ttu-id="8d9f7-133">Заполните свойства **Ключ SendGrid API** и **Имя параметра сообщения**.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-133">Fill in the **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="8d9f7-134">При желании вы можете ввести сейчас и другие свойства или закодировать их.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-134">If you want, you can enter the other properties now, or code them instead.</span></span> <span data-ttu-id="8d9f7-135">Приведенные здесь параметры можно использовать как значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-135">These settings can be used as defaults.</span></span>

 ![Настройка выходных привязок SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="8d9f7-137">При добавлении в функцию привязки в папке функции создается файл с именем **function.json**.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-137">Adding a binding to a function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="8d9f7-138">Этот файл содержит все те же сведения, которые можно видеть на вкладке **Интегрировать** функции Azure, но в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-138">This file contains all the same information that you see in the Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="8d9f7-139">Если задать значения полей **Ключ SendGrid API**, **Имя параметра сообщения** и **Адрес отправителя**, то в файле **function.json** будут созданы следующие записи:</span><span class="sxs-lookup"><span data-stu-id="8d9f7-139">Setting the **ApiKey**, **message**, and **from** fields create the following entries in the **function.json** file:</span></span> 

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

<span data-ttu-id="8d9f7-140">При желании вы можете изменить этот файл самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="8d9f7-141">Теперь, когда созданы и настроены приложение-функция и функция, можно написать код для отправки электронной почты.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-141">Now that you have created and configured the Function App and function, you can write the code to send an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="8d9f7-142">Написание кода, который создает и отправляет электронную почту</span><span class="sxs-lookup"><span data-stu-id="8d9f7-142">Write code that creates and sends email</span></span>

<span data-ttu-id="8d9f7-143">API SendGrid содержит все команды, необходимые для создания и отправки электронной почты.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-143">The SendGrid API contains all the commands you need to create and send an email.</span></span>  

- <span data-ttu-id="8d9f7-144">Замените код в функции следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="8d9f7-144">Replace the code in the function with the following code:</span></span>

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
    // change to email of recipient
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

<span data-ttu-id="8d9f7-145">Обратите внимание, что в первой строке содержится директива ```#r```, которая ссылается на сборку SendGrid.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-145">Notice the first line contains the ```#r``` directive that references the SendGrid assembly.</span></span> <span data-ttu-id="8d9f7-146">Затем можно использовать инструкцию ```using```, чтобы упростить доступ к объектам в этом пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-146">After that, you can use a ```using``` statement to more easily access the objects in that namespace.</span></span> <span data-ttu-id="8d9f7-147">Из интерфейса API SendGrid создайте в коде экземпляры объектов ```Mail```, ```Personalization``` и ```Content```, из которых состоит сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-147">In the code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from the SendGrid API that compose the email.</span></span> <span data-ttu-id="8d9f7-148">Когда вы возвращаете сообщение, SendGrid доставляет его.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-148">When you return the message, SendGrid delivers it.</span></span> 

<span data-ttu-id="8d9f7-149">Подпись функции также содержит дополнительный выходной параметр типа ```Mail``` с именем ```message```.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-149">The function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="8d9f7-150">Как входные, так и выходные привязки выражаются в коде как параметры функции.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="8d9f7-151">Протестируйте код, щелкнув **Тест** и введя сообщение в поле **Текст запроса**. Затем нажмите кнопку **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-151">Test your code by clicking **Test** and entering a message into the **Request body** field, then clicking the **Run** button.</span></span>

 ![Тестирование кода](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="8d9f7-153">Проверьте электронную почту, чтобы убедиться в отправке сообщения SendGrid.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-153">Check email to verify that SendGrid sent the email.</span></span> <span data-ttu-id="8d9f7-154">Оно должно быть доставлено на адрес, указанный в коде на шаге 1, и содержать сообщение, введенное в поле **Текст запроса**.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-154">It should go to the address in the code from step 1, and contain the message from the **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d9f7-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d9f7-155">Next steps</span></span>
<span data-ttu-id="8d9f7-156">В этой статье показано, как использовать службу SendGrid для создания и отправки электронной почты.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-156">This article has demonstrated how to use the SendGrid service to create and send email.</span></span> <span data-ttu-id="8d9f7-157">Дополнительные сведения об использовании Функций Azure в приложениях см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="8d9f7-157">To learn more about using Azure Functions in your apps, see the following topics:</span></span> 

- <span data-ttu-id="8d9f7-158">[Рекомендации по Функциям Azure](functions-best-practices.md). Некоторые рекомендации по созданию функций Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="8d9f7-159">[Руководство для разработчиков по Функциям Azure](functions-reference.md). Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="8d9f7-160">[Тестирование функций Azure](functions-test-a-function.md). Описание различных средств и методов тестирования функций.</span><span class="sxs-lookup"><span data-stu-id="8d9f7-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>