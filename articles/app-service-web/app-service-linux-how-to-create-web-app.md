---
title: "aaaCreate Azure веб-приложение, работающее на платформе Linux | Документы Microsoft"
description: "Рабочий процесс создания веб-приложения для веб-приложения Azure на платформе Linux."
keywords: "служба приложений azure, веб-приложение, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Создание веб-приложения Azure на платформе Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>Использовать hello Azure портала toocreate веб-приложения
Вы можете начать создание веб-приложения на платформе Linux из hello [портал Azure](https://portal.azure.com) как показано в hello после изображения:

![Приступить к созданию веб-приложения на hello портал Azure][1]

Здравствуйте, затем **создать колонки** открывается, как показано в hello после изображения:

![Создать колонки Hello][2]

1. Присвойте веб-приложению имя.
2. Выберите имеющуюся группу ресурсов или создайте новую. (См. доступных регионов в hello [разделе "ограничения"](app-service-linux-intro.md).)
3. Выберите имеющийся план службы приложений Azure или создайте новый. (См. примечания плана служб приложений в hello [разделе "ограничения"](app-service-linux-intro.md).)
4. Выберите приложение hello, следует присвоить toouse стека. На выбор предоставляется несколько версий Node.js, PHP, .NET Core и Ruby.

После создания приложения hello, можно изменить стека приложения hello из параметров приложения hello, как показано в hello после изображения:

![Параметры приложения][3]

## <a name="deploy-your-web-app"></a>Развертывание веб-приложения
Выбор **варианты развертывания** из портала дает hello управления вы hello параметр toouse локальный Git и GitHub репозитория toodeploy приложения. rest Hello hello инструкций, аналогичные toothose для веб-приложения не Linux. Инструкции hello в [локальное развертывание Git](app-service-deploy-local-git.md) или [непрерывного развертывания](app-service-continuous-deployment.md) toodeploy приложения.

Также можно использовать FTP tooupload tooyour узла приложения. Можно получить конечную точку FTP hello веб-приложения из системы диагностики hello разделе журналы как показано в hello после изображения:

![Раздел "Журналы диагностики"][4]

## <a name="next-steps"></a>Дальнейшие действия
* [Что такое веб-приложение Azure на платформе Linux?](app-service-linux-intro.md)
* [Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux](app-service-linux-using-nodejs-pm2.md)
* [Использование Ruby в веб-приложении службы приложений Azure на платформе Linux](app-service-linux-ruby-get-started.md)
* [Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
