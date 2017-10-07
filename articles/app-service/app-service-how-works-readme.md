---
title: "aaaHow работает служба приложений Azure"
description: "Принцип работы службы приложений"
keywords: "служба приложений, служба приложений azure, масштабировать, масштабируемый, план службы приложений, стоимость службы приложений"
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a>Принцип работы службы приложений
Служба приложений Azure — облачной службы, спроектированный toosolve hello практические неполадкам повседневных инженеров.
Службы приложений основное внимание уделяется предоставление высокому уровню продуктивности разработки без влияния на hello должны toodeliver приложений в масштабе облака. 

Службы приложений также предоставляет функции hello и платформ, которые необходимы для создания корпоративных бизнес-приложений. Приложение службы можно разрабатывать приложения в наиболее популярных языках программирования, включая Java, PHP, Node.js, Python и языках Microsoft .NET hello. С помощью службы приложений вы можете делать следующее.

* создавать веб-приложения с высоким уровнем масштабируемости;
* быстро создавать серверную часть мобильных приложений с такими удобными возможностями, как серверная часть данных, проверка подлинности пользователей и push-уведомления;
* создавать, развертывать и публиковать API с помощью служб API;
* объединять бизнес-приложения в рабочие процессы и преобразовывать данные, используя приложения логики.

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

Все типы приложений используют hello масштабируемая и гибкая веб-приложений платформе, которая позволяет разработчикам toohave возникнуть оптимизированного весь жизненный цикл из обслуживания tooapp разработки приложения. функции Hello жизненным циклом обеспечивают hello следующее:

* **Быстро создавать приложения.** С самого начала или выбора пакета оперативной поддержки системы (ОС) из hello Azure Marketplace.
* **Осуществлять непрерывное развертывание.** Автоматически развертывать новый код из таких популярных решений управления версиями, как TFS, GitHub и BitBucket, и синхронизировать содержимое с такими службами онлайн-хранилищ, как OneDrive и DropBox.
* **Тестировать приложение в рабочей среде.** Плавно создания предварительной рабочей среде и управления ими hello объем трафика, который будет toothem. Отладка в облаке hello при необходимости и накат при обнаружении ошибок.
* **Выполнять асинхронные задачи и пакетные задания.** Выполнять код в фоновом режиме или активировать его на основе событий (например, при поступлении сообщений в очередь хранилища Azure) или в определенное время (CRON).
* **Масштабирование приложения hello**. Используйте одну из многих вариантов tooautomatically масштабировать службу по горизонтали и вертикали в зависимости от трафика и использовании ресурсов. Настройка частного сред, выделенный tooyour приложений.   
* **Обслуживание приложения hello**. Использовать многие отладки hello и toostay функции диагностики опережает проблем и tooefficiently устранить их, либо в режиме реального времени (с такими функциями как автоматическое восстановление и динамической отладки) или после проведения hello путем анализа памяти и журналы дампов.

В целом возможности службы приложения включите toofocus разработчиков для своего кода и быстро достичь состояния стабильными и высокой степенью масштабирования рабочей. Hello API приложения и компоненты приложения логики разработчики могут создавать реальных корпоративных приложений, мост барьеров между бизнес-решений и локальная интеграция toocloud. 

## <a name="videos"></a>Видеоролики
* [Why Azure Web Sites? Web Sites Architecture — with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/) (Зачем использовать именно веб-сайты Azure? Архитектура веб-сайтов со Стефаном Шашковым)

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о службе приложений в одном hello следующие вопросы:

* [Что такое служба приложений Azure?](app-service-value-prop-what-is.md)
  * [Веб-приложение](../app-service-web/app-service-web-overview.md)
  * [Мобильное приложение](../app-service-mobile/app-service-mobile-value-prop.md)
  * [Приложение API](../app-service-api/app-service-api-apps-why-best-platform.md)
* [Windows Azure Web Sites - Things they don’t teach kids in school](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [Сравнение службы приложений, облачных служб и виртуальных машин Azure](../app-service-web/choose-web-site-cloud-service-vm.md)
* [Подробный обзор планов службы приложений Azure](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [Введение tooApp среды службы](../app-service-web/app-service-app-service-environment-intro.md)
  * [Создание среды службы приложений](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [Windows Azure Websites Development Stacks Support (Поддержка стеков разработки веб-сайтов Windows Azure)](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



