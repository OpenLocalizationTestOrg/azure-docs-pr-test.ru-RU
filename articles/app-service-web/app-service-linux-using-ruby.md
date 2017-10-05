---
title: "Использование Ruby в веб-приложении службы приложений Azure на платформе Linux | Документация Майкрософт"
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
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>Использование Ruby в веб-приложении на платформе Linux #

В последнем обновлении нашей серверной части мы добавили поддержку Ruby версии 2.3. Настроив конфигурацию веб-приложения Linux, вы можете изменить стек приложений.

## <a name="using-the-azure-portal"></a>Использование портала Azure ##

Из меню "Создать" на [портале Azure](https://portal.azure.com) вы можете создать веб-приложение на платформе Linux, выбрав "Интернет+мобильные устройства", как показано на следующем рисунке.

![Начало создания веб-приложения на портале Azure][1]

После этого откроется колонка **Создание**, как показано на следующем изображении.

![Колонка "Создание"][2]

1. Присвойте веб-приложению имя.
2. Выберите имеющуюся группу ресурсов или создайте новую. (Доступные регионы см. в [разделе с ограничениями](app-service-linux-intro.md).)
3. Выберите имеющийся план службы приложений Azure или создайте новый. (Заметки о плане службы приложений см. в [разделе с ограничениями](app-service-linux-intro.md).)
4. Выберите Ruby из списка встроенных стеков времени выполнения.

После создания веб-приложения Ruby его можно развернуть с помощью Git или FTP.

Дополнительные сведения о создании приложения Ruby см. в [этом руководстве по началу работы](app-service-linux-ruby-get-started.md).

## <a name="next-steps"></a>Дальнейшие действия
* [Что такое веб-приложение на платформе Linux?](app-service-linux-intro.md)
* [Развертывание локального репозитория Git в службе приложений Azure](app-service-deploy-local-git.md)
* [Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](app-service-linux-faq.md)
* [Создание приложения Ruby с помощью веб-приложения на платформе Linux (предварительная версия)](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png