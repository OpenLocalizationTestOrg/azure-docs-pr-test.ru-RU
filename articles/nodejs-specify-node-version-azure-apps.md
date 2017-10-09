---
title: "aaaSpecifying Node.js версии"
description: "Узнайте, как toospecify hello версию Node.js, используемые веб-сайтов Azure и облачные службы"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Указание версии Node.js в приложении Azure
При размещении приложения Node.js, может потребоваться tooensure, что приложение использует конкретную версию Node.js. Существует несколько способов tooaccomplish это для приложений, размещенных в Azure.

## <a name="default-versions"></a>Версии по умолчанию
версии Node.js Hello, предоставляемые Azure постоянно обновляются. Если не указано иначе, hello версия по умолчанию, которая указана в hello `WEBSITE_NODE_DEFAULT_VERSION` переменная среды будет использоваться. toooverride это значение по умолчанию, повторите шаги hello в следующих разделах этой статьи

> [!NOTE]
> Если имеются приложения в облачной службе Azure (рабочих и веб-роль) и впервые hello развернуто приложение hello, Azure попытается toouse hello ту же версию Node.js, как вы установили в среде разработки, если он совпадает с одним из версии по умолчанию hello доступный в Azure.
>
>

## <a name="versioning-with-packagejson"></a>Управление версиями с использованием package.json
Можно задать версию hello используется, добавив следующие tooyour hello toobe Node.js **package.json** файла:

    "engines":{"node":version}

Где *версии* — число toouse hello определенной версии. Вы можете задать более сложные условия для версии, например:

    "engines":{"node": "0.6.22 || 0.8.x"}

Так как 0.6.22 не является одним из доступных в среде размещения hello версий hello, hello самую новую версию hello 0,8 ряда, который доступен используются вместо - 0.8.4.

## <a name="versioning-websites-with-app-settings"></a>Управление версиями веб-сайтов с помощью параметров приложения
При размещении приложения hello на веб-сайте, можно задать переменную среды hello **WEBSITE_NODE_DEFAULT_VERSION** toohello нужную версию.

## <a name="versioning-cloud-services-with-powershell"></a>Управление версиями облачных служб с использованием PowerShell
При размещении приложения hello в облачной службе и развертывании приложения hello, с помощью Azure PowerShell, версия Node.js hello по умолчанию можно переопределить с помощью hello **AzureServiceProjectRole набор** командлета PowerShell. Например:

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

Параметры hello Примечание в hello выше инструкции, зависят от регистра.  Можно проверить, проверив hello был выбран hello правильную версию Node.js **ядер** свойство в данной роли **package.json**.

Можно также использовать hello **Get AzureServiceProjectRoleRuntime** tooretrieve список Node.js версии для приложения, размещенные в облачной службе.  Всегда убедитесь, что версия hello Node.js зависит от проекта — в этом списке.

## <a name="using-a-custom-version-with-azure-websites"></a>Использование настраиваемой версии с веб-сайтами Azure
Хотя Azure предоставляет несколько версий по умолчанию Node.js, может возникнуть toouse версию, которая по умолчанию не предоставляется. Если приложение размещается в виде веб-сайт Azure, это можно сделать, используя hello **iisnode.yml** файла. Hello следующие шаги пошагового hello процесс использования пользовательской версии Node.Js с веб-сайта Azure:

1. Создать новый каталог, а затем создайте **server.js** файл в каталоге hello. Hello **server.js** файл должен содержать hello следующее:

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    Это позволит отобразить hello Node.js версии используются при просмотре веб-сайта hello.
2. Создание нового веб-сайта и имя hello Примечание hello сайта. Например, следующие hello использует hello [средств командной строки Azure] toocreate новый веб-сайт Azure с именем **мой_веб**и затем включите репозитория для веб-сайта hello.

        azure site create mywebsite --git
3. Создайте новый каталог с именем **bin** как дочерний hello каталог, содержащий hello **server.js** файла.
4. Загрузите hello конкретной версии **node.exe** (версия Windows hello) нужно toouse вместе с приложением. Здравствуйте, например, следующие использует **curl** toodownload версии 0.8.1:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Сохранить hello **node.exe** файла в hello **bin** папки, созданной ранее.
5. Создание **iisnode.yml** файл hello же каталоге, что hello **server.js** файла, а затем добавьте следующие содержимого toohello hello **iisnode.yml** файла:

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    Этот путь является там, где hello **node.exe** файла в проект будет располагаться после публикации toohello вашего приложения веб-сайта Azure.
6. Опубликуйте приложение. Например так как ранее созданного нового веб-сайта с параметром--git hello, hello следующие команды Добавление hello приложения файлы toomy локального репозитория Git и отправить их toohello репозитория веб-сайта.

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    После публикации приложения hello откройте веб-сайт hello в браузере. Должно появиться сообщение "Hello from Azure running node version: v0.8.1".

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы знаете, как версия hello toospecify Node.js, используемого приложением, узнайте, каким образом слишком[работают с модулями], [построение и развертывание веб-сайта Node.js](app-service-web/app-service-web-get-started-nodejs.md), и [как toouse hello Azure Средства командной строки для Mac и Linux].

Дополнительные сведения см. в разделе hello [Центр разработчика Node.js](https://azure.microsoft.com/develop/nodejs/).

[как toouse hello Azure Средства командной строки для Mac и Linux]:cli-install-nodejs.md
[средств командной строки Azure]:cli-install-nodejs.md
[работают с модулями]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
