---
title: "Конфигурация aaaUsing PM2 для Node.js в веб-приложения Azure для Linux | Документы Microsoft"
description: "Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux."
keywords: "служба приложений azure, веб-приложение, nodejs, pm2, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="5dfdf-104">Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="5dfdf-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="5dfdf-105">При tooNode.js стек приложения hello, задаваемое для веб-приложения Azure в Linux, появляется параметр tooset hello файла запуска Node.js как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="5dfdf-105">If you set hello application stack tooNode.js for Azure Web App on Linux, you get hello option tooset a Node.js startup file as shown in hello following image:</span></span>

![Указание загрузочного файла Node.js][1]

<span data-ttu-id="5dfdf-107">Можно использовать параметр toodo один из hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5dfdf-107">You can use this option toodo one of hello following tasks:</span></span>

* <span data-ttu-id="5dfdf-108">Укажите сценарий запуска приветствия для Node.js приложения (например: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="5dfdf-108">Specify hello startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="5dfdf-109">Укажите hello PM2 toouse файла конфигурации приложения Node.js (например: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="5dfdf-109">Specify hello PM2 configuration file toouse for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5dfdf-110">Ваш toorestart Node.js процессы автоматически при изменении определенных файлов, используйте hello PM2 конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5dfdf-110">If you want your Node.js processes toorestart automatically when certain files are modified, use hello PM2 configuration.</span></span> <span data-ttu-id="5dfdf-111">В противном случае приложение не будет перезапускаться после получения уведомлений об изменениях (например, после изменения кода приложения).</span><span class="sxs-lookup"><span data-stu-id="5dfdf-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="5dfdf-112">Вы можете проверить hello Node.js [обработать файл документации](http://pm2.keymetrics.io/docs/usage/application-declaration/) для всех hello параметры, но ниже приведен пример того, можно использовать как файл process.json:</span><span class="sxs-lookup"><span data-stu-id="5dfdf-112">You can check hello Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all hello options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="5dfdf-113">Перечислены важные моменты, о toonote в этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5dfdf-113">Important things toonote in this configuration are:</span></span>

* <span data-ttu-id="5dfdf-114">Свойство «сценарий» Hello указывает сценария запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="5dfdf-114">hello "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="5dfdf-115">Свойство «экземпляры» Hello указывает, сколько экземпляров процесса toolaunch hello узла.</span><span class="sxs-lookup"><span data-stu-id="5dfdf-115">hello "instances" property specifies how many instances of hello node process toolaunch.</span></span> <span data-ttu-id="5dfdf-116">При запуске приложения на виртуальных машинах большего размера, которые имеют несколько ядер это toomaximize хорошее представление ресурсов, задав более высокое значение здесь.</span><span class="sxs-lookup"><span data-stu-id="5dfdf-116">If you are running your application on larger VMs that have multiple cores, it's a good idea toomaximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="5dfdf-117">Здравствуйте, «просмотреть» массива указывает все требуемые файлы toorestart hello узел процесс при изменении ее.</span><span class="sxs-lookup"><span data-stu-id="5dfdf-117">hello "watch" array specifies all files that you want toorestart hello node process for when they change.</span></span>
* <span data-ttu-id="5dfdf-118">Для hello «watch_options» необходимо в данный момент toospecify «usePolling» значение true из-за hello, как подключить содержимое вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="5dfdf-118">For hello "watch_options", you currently need toospecify "usePolling" as true because of hello way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dfdf-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5dfdf-119">Next steps</span></span>
* [<span data-ttu-id="5dfdf-120">Что такое веб-приложение Azure на платформе Linux?</span><span class="sxs-lookup"><span data-stu-id="5dfdf-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="5dfdf-121">Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="5dfdf-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
