---
title: "aaaUsing Ruby в Azure приложение службы веб-приложения на платформе Linux | Документы Microsoft"
description: "Использование Ruby в веб-приложении службы приложений Azure на платформе Linux."
keywords: "Служба приложений Azure, веб-приложение, вопросы и ответы, Linux, OSS, Ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>Использование Ruby в веб-приложении на платформе Linux #

С hello последние обновления tooour серверной части мы появилась поддержка Ruby v.2.3. Параметр конфигурации hello веб-приложения Linux можно изменить стека приложения hello.

## <a name="using-hello-azure-portal"></a>С помощью портала Azure hello ##

Новое меню hello в hello [портал Azure](https://portal.azure.com), вы можете toocreate веб-приложения на платформе Linux с hello Web + мобильный телефон как показано в hello после изображения:

![Приступить к созданию веб-приложения на hello портал Azure][1]

Здравствуйте, затем **создать колонки** открывается, как показано в hello после изображения:

![Создать колонки Hello][2]

1. Присвойте веб-приложению имя.
2. Выберите имеющуюся группу ресурсов или создайте новую. (См. доступных регионов в hello [разделе "ограничения"](app-service-linux-intro.md).)
3. Выберите имеющийся план службы приложений Azure или создайте новый. (См. примечания плана служб приложений в hello [разделе "ограничения"](app-service-linux-intro.md).)
4. Выберите hello Ruby стеки hello встроенных среды выполнения.

После создания Ruby веб-приложение получает можно развернуть tooit с использованием Git или FTP.

toolearn Дополнительные сведения о создании приложений Ruby, проверьте hello [get руководство для начинающих](app-service-linux-ruby-get-started.md)

## <a name="next-steps"></a>Дальнейшие действия
* [Что такое веб-приложение на платформе Linux?](app-service-linux-intro.md)
* [Локальные развертывания Git tooAzure службы приложений](app-service-deploy-local-git.md)
* [Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](app-service-linux-faq.md)
* [Создание приложения Ruby с помощью веб-приложения на платформе Linux (предварительная версия)](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png