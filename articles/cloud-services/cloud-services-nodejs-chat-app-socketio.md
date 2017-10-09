---
title: "с помощью Socket.io приложения aaaNode.js | Документы Microsoft"
description: "Узнайте, как socket.io toouse в node.js приложении, размещенном в Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>Создание приложения для разговора Node.js с Socket.IO в облачной службе Azure
Socket.IO обеспечивает связь в режиме реального времени между сервером и клиентами node.js. В этом учебнике рассматривается размещение приложения для разговора на основе Socket.IO в Azure. Дополнительные сведения о Socket.IO см. на веб-сайте <http://socket.io/>.

Снимок экрана приложения hello завершения используется следующим образом:

![Окно браузера, отображение hello службе, размещенной в Azure][completed-app]  

## <a name="prerequisites"></a>Предварительные требования
Убедитесь, что hello следующих продуктов и версий, установленных toosuccessfully hello полный пример в этой статье:

* установить [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx);
* Установите [Node.js](https://nodejs.org/download/)
* Установите [Python версии 2.7.10](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>Создание проекта облачной службы
Hello следующие действия создадут hello проекта облачной службы, где будет размещаться приложение Socket.IO hello.

1. Из hello **меню "Пуск"** или **рабочий стол**, поиск **Windows PowerShell**. Щелкните правой кнопкой мыши **Windows PowerShell** и выберите **Запуск от имени администратора**.
   
    ![Значок Azure PowerShell][powershell-menu]
2. Сначала создайте каталог **c:\\node**. 
   
        PS C:\> md node
3. Измените каталоги toohello **c:\\узел** каталог
   
        PS C:\> cd node
4. Введите следующие команды toocreate новое решение с именем hello **chatapp** и рабочей роли с названием **WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    Вы увидите hello следующий ответ:
   
    ![Вывод Hello hello новый azureservice и добавить azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>Загрузите hello пример чата
Для этого проекта, мы будем использовать пример hello разговора с hello [репозитории Socket.IO GitHub]. Выполните следующий пример hello toodownload действия hello и добавьте его toohello проекта, созданного ранее.

1. Создать локальную копию репозитория hello с помощью hello **клон** кнопки. Можно также использовать hello **ZIP** кнопку toodownload hello проекта.
   
   ![Просмотр https://github.com/LearnBoost/socket.io/tree/master/examples/chat, значком загрузки ZIP "hello" выделяются окно браузера][chat-example-view]
2. Перейдите структуры каталогов hello hello локальный репозиторий, пока не будет выполнен переход на hello **примеры\\чата** каталога. Скопируйте содержимое hello этот каталог toothe **C:\\узел\\chatapp\\WorkerRole1** каталогом, созданным ранее.
   
   ![Обозреватель, отображающая содержимое hello hello примеры\\каталог чата, извлеченных из архива hello][chat-contents]
   
   Hello выделенные элементы в снимке экрана приветствия выше, hello файлов, скопированных из hello **примеры\\чата** каталога
3. В hello **C:\\узел\\chatapp\\WorkerRole1** каталог, удаление hello **server.js** файла, а затем переименуйте hello **в файле app.js**файл слишком**server.js**. При этом удаляются по умолчанию hello **server.js** файл, созданный ранее hello **Add-AzureNodeWorkerRole** командлета и заменяет его с помощью приложения hello файл из hello пример разговора.

### <a name="modify-serverjs-and-install-modules"></a>Изменение Server.js и установка модулей
Прежде чем приложение hello тестирования в hello эмулятор Azure необходимо некоторые незначительные изменения. Выполните следующие шаги toothe server.js файл hello.

1. Откройте hello **server.js** файл в Visual Studio или в любом текстовом редакторе.
2. Найти hello **зависимости модулей** в начале hello server.js и измените hello строке, содержащей **sio = require('.. //.. LIB//Socket.IO ")** слишком**sio = require('socket.io')** как показано ниже:
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. приложение hello tooensure прослушивает hello правильный порт, откройте server.js в блокноте или любом редакторе и измените следующую строку, заменяя **3000** с **process.env.port** как показано ниже:
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

После сохранения изменений hello слишком**server.js**, используйте hello следующие шаги для установки требуемых модулей и проверить приложение hello в эмуляторе Azure:

1. С помощью **Azure PowerShell**, измените каталоги toohello **C:\\узел\\chatapp\\WorkerRole1** каталог и использовать hello, следующая команда tooinstall hello модули, необходимых для этого приложения:
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   Будет выполнена установка hello модулей, перечисленных в файле package.json hello. После завершения команды hello, вы увидите примерно toothe следующие выходные данные:
   
   ![Команда установки hello npm выходные данные Hello][The-output-of-the-npm-install-command]
2. Поскольку в этом примере был изначально частью hello репозитории Socket.IO GitHub и прямая ссылка на библиотеку Socket.IO hello относительного пути, Socket.IO нет ссылок в файл package.json hello, поэтому его необходимо установить, выполнив следующую команду hello:
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>Тестирование и развертывание
1. Запустите эмулятор hello, выполнив следующую команду hello:
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > С запуском эмулятора может возникнуть проблема, например во время выполнения команды Start-AzureEmulator произошла непредвиденная ошибка.  Подробные сведения: Произошла непредвиденная ошибка hello объект связи System.ServiceModel.Channels.ServiceChannel, не может использоваться для связи, так как он находится в состоянии Faulted hello.
   
      Переустановите AzureAuthoringTools версии 2.7.1 и AzureComputeEmulator версии 2.7 (убедитесь, что версии совпадают).
   >
   >


2. Откройте браузер и перейдите в слишком**http://127.0.0.1**.
3. В открывшемся окне браузера hello введите понятное имя и затем нажмите клавишу ВВОД.
   Это позволит вам toopost сообщений от определенного понятное имя. функциональные возможности tootest несколькими пользователями, открывать окна браузера, используя же URL-адрес и введите разные псевдонимы.
   
   ![Два окна браузера с сообщениями разговора от пользователей User1 и User2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. После тестирования приложения hello остановите hello эмулятора, введя следующую команду:
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. tooAzure приложения hello toodeploy, используйте **AzureServiceProject публикации** командлета. Например:
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > Можно убедиться, что toouse уникальное имя, в противном случае hello публикации процесс завершится ошибкой. После завершения развертывания hello обозреватель hello и перехода toohello развертывания службы.
   > 
   > Если появляется следующее сообщение об ошибке, hello, если имя подписки не существует в hello импортировать профиль публикации, необходимо загрузить и импортировать профиль публикации hello для вашей подписки, перед развертыванием tooAzure. . В разделе hello **развертывание tooAzure приложения hello** раздел [построения и развертывания tooan приложений Node.js облачной службы Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![Окно браузера, отображение hello службе, размещенной в Azure][completed-app]
   
   > [!NOTE]
   > Если появляется следующее сообщение об ошибке, hello, если имя подписки не существует в hello импортировать профиль публикации, необходимо загрузить и импортировать профиль публикации hello для вашей подписки, перед развертыванием tooAzure. . В разделе hello **развертывание tooAzure приложения hello** раздел [построения и развертывания tooan приложений Node.js облачной службы Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

Теперь ваше приложение выполняется на платформе Azure и может передавать сообщения чата между различными клиентами с использованием Socket.IO.

> [!NOTE]
> Для простоты в этом примере используется ограниченный toochatting между toohello подключенных пользователей того же экземпляра. Это означает, что если hello облачная служба создает двух экземпляров рабочей роли, пользователи только смогут toochat с другими разделами подключен toohello того же экземпляра роли рабочего процесса. toowork приложения hello tooscale с несколькими экземплярами роли, можно использовать технологию как Service Bus tooshare hello Socket.IO сохранение состояния между экземплярами. Примеры см. в разделе hello очереди Service Bus и разделы примеры использования в hello [Azure SDK для репозитория Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, как toocreate это основные чата приложение, размещенное в облачной службе Azure. toolearn toohost этого приложения в веб-сайта Azure. в статье [построения приложения чат Node.js с Socket.IO на веб-сайте Azure][chatwebsite].

Дополнительные сведения см. также: hello [Центр разработчика Node.js](/develop/nodejs/).

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[репозитории Socket.IO GitHub]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


