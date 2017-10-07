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
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


При tooNode.js стек приложения hello, задаваемое для веб-приложения Azure в Linux, появляется параметр tooset hello файла запуска Node.js как показано в hello после изображения:

![Указание загрузочного файла Node.js][1]

Можно использовать параметр toodo один из hello следующие задачи:

* Укажите сценарий запуска приветствия для Node.js приложения (например: /bin/server.js).
* Укажите hello PM2 toouse файла конфигурации приложения Node.js (например: /foo/process.json).
  
  > [!NOTE]
  > Ваш toorestart Node.js процессы автоматически при изменении определенных файлов, используйте hello PM2 конфигурации. В противном случае приложение не будет перезапускаться после получения уведомлений об изменениях (например, после изменения кода приложения).
  > 
  > 

Вы можете проверить hello Node.js [обработать файл документации](http://pm2.keymetrics.io/docs/usage/application-declaration/) для всех hello параметры, но ниже приведен пример того, можно использовать как файл process.json:

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

Перечислены важные моменты, о toonote в этой конфигурации.

* Свойство «сценарий» Hello указывает сценария запуска приложения.
* Свойство «экземпляры» Hello указывает, сколько экземпляров процесса toolaunch hello узла. При запуске приложения на виртуальных машинах большего размера, которые имеют несколько ядер это toomaximize хорошее представление ресурсов, задав более высокое значение здесь.
* Здравствуйте, «просмотреть» массива указывает все требуемые файлы toorestart hello узел процесс при изменении ее.
* Для hello «watch_options» необходимо в данный момент toospecify «usePolling» значение true из-за hello, как подключить содержимое вашего приложения.

## <a name="next-steps"></a>Дальнейшие действия
* [Что такое веб-приложение Azure на платформе Linux?](app-service-linux-intro.md)
* [Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
