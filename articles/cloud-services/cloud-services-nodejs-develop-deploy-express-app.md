---
title: "aaaWeb приложение с экспресс-выпуск (Node.js) | Документы Microsoft"
description: "Учебник, в котором основана на hello облачной службы учебника и показано, как toouse hello модуль экспресс-выпуск."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>Создание веб-приложения Node.js с использованием модуля Express в облачной службе Azure
Node.js включает минимальный набор функциональных возможностей в среде выполнения ядра hello.
Разработчики часто используют сторонних производителей модулей tooprovide дополнительные функциональные возможности при разработке приложений Node.js. В этом учебнике создается новое приложение с помощью hello [Express] [ Express] модуль, который предоставляет платформу MVC для создания веб-приложений Node.js.

Снимок экрана приложения hello завершения используется следующим образом:

![Веб-браузер, отображение tooExpress Добро пожаловать в Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>Создание проекта облачной службы
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

Hello следующих шагов toocreate Создание проекта облачной службы с именем «expressapp»:

1. Из hello **меню "Пуск"** или **рабочий стол**, поиск **Windows PowerShell**. Щелкните правой кнопкой мыши **Windows PowerShell** и выберите **Запуск от имени администратора**.
   
    ![Значок Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. Измените каталоги toohello **c:\\узел** каталога, а затем введите следующие команды toocreate новое решение с именем hello **expressapp** и веб-роль с именем **WebRole1** :
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > По умолчанию **Add-AzureNodeWebRole** использует предыдущую версию Node.js. Hello **AzureServiceProjectRole набор** выше инструкция предписывает v0.10.21 Azure toouse узла.  Обратите внимание, что параметры hello зависят от регистра.  Можно проверить, проверив hello был выбран hello правильную версию Node.js **ядер** свойство в **WebRole1\package.json**.
    > 
    > 

## <a name="install-express"></a>Установка модуля Express
1. Установите генератор Express hello, выполнив следующую команду hello:
   
        PS C:\node\expressapp> npm install express-generator -g
   
    Hello выходные данные команды npm hello должен выглядеть примерно ниже toohello результата. 
   
    ![Express команда установки Windows PowerShell отображение hello выходные данные hello npm.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. Измените каталоги toohello **WebRole1** каталог и использовать hello toogenerate express команда нового приложения:
   
        PS C:\node\expressapp\WebRole1> express
   
    Вам будет запрашиваемые toooverwrite предыдущих приложения. Введите **y** или **Да** toocontinue. Express приведет к созданию файла в файле app.js hello и структуру папок для построения приложения.
   
    ![Hello выходные данные команды express hello](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. tooinstall Дополнительные зависимости, определенные в файле package.json hello, введите следующую команду hello:
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Команда установки hello npm выходные данные Hello](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. Используйте hello следующая команда toocopy hello **bin/www** файла слишком**server.js**. Это так, чтобы hello облачной службы можно найти hello точку входа для этого приложения.
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   После выполнения этой команды должно быть **server.js** файл в каталоге hello WebRole1.
5. Изменение hello **server.js** tooremove один hello "." символов из следующей строкой hello.
   
       var app = require('../app');
   
   После внесения этого изменения, строка hello должен выглядеть следующим образом.
   
       var app = require('./app');
   
   Это изменение не требуется, так как мы перешли файл hello (прежнее название — **bin/www**,) toohello же каталоге, что файл приложения hello является обязательным. После этого изменения сохранить hello **server.js** файла.
6. Используйте hello следующая команда toorun приложения hello в hello эмулятор Azure:
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Веб-страница, содержащая tooexpress приветствия.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>Изменение представления hello
Теперь измените hello представление toodisplay приветственное сообщение «Вас приветствует tooExpress в Azure».

1. Введите следующие команды tooopen hello index.jade файл hello:
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Hello содержимое файла index.jade hello.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade — обработчик представлений по умолчанию hello, используемых приложениями, экспресс-выпуск. Дополнительные сведения о обработчик Jade представлений hello. в разделе [http://jade-lang.com][http://jade-lang.com].
2. Измените hello последней строки текста, добавив **в Azure**.
   
   ![считывает файл index.jade Hello, последняя строка hello: p Добро пожаловать слишком\#{title} в Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. Сохраните файл hello и закройте Блокнот.
4. Обновите браузер и увидите изменения.
   
   ![Окно браузера, страница приветствия содержит tooExpress Добро пожаловать в Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

После тестирования приложения hello, используйте hello **Stop AzureEmulator** командлет toostop hello эмулятора.

## <a name="publishing-hello-application-tooazure"></a>Публикация tooAzure приложения hello
В окне Azure PowerShell hello использовать hello **AzureServiceProject публикации** командлет toodeploy приложения hello tooa облачной службы

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

После завершения операции развертывания hello браузера открыть и отобразить веб-страницу приветствия.

![Веб-браузер, отображения страницы приветствия, экспресс-выпуск. URL-адрес Hello указывает, что теперь она размещается в Azure.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [Центр разработчика Node.js](/develop/nodejs/).

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


