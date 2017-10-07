---
title: "aaaIntroduction tooAzure веб-приложения на платформе Linux | Документы Microsoft"
description: "Сведения о веб-приложении Azure на платформе Linux."
keywords: "служба приложений azure, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a>Введение tooAzure веб-приложения в Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Обзор
Клиенты могут использовать веб-приложения в Linux toohost веб-приложениях в Linux для приложений поддерживаются стеки. Hello в подразделе ниже приведены стеки приложения hello, которые в настоящее время поддерживаются. 

## <a name="features"></a>Функции
Веб-приложения на платформе Linux в настоящее время поддерживает следующие стеки приложения hello:

* Node.js
    * 4.4.
    * 4.5.
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* .NET Core.
    * 1.0
    * 1,1
* Ruby
    * 2.3

Чтобы развертывать собственные приложения, клиенты могут использовать следующее:

* FTP
* локальный репозиторий Git;
* GitHub
* Bitbucket;

Масштабирование приложения осуществляется следующими способами:

* Клиенты вверх и вниз масштабирование веб-приложений можно изменить уровень hello их план служб приложений
* Клиентов можно масштабировать приложения и запустить несколько экземпляров приложения в рамках ограничивающее hello их номера SKU

Для Kudu некоторые основные функциональные возможности hello:

* средами;
* Развернутые приложения
* базовая консоль;
* SSH

Функции для DevOps:

* Промежуточные среды
* запись контроля доступа и непрерывная интеграция и развертывание Docker Hub.

## <a name="limitations"></a>Ограничения
Hello портал Azure показывает только функции, которые в настоящее время работают для веб-приложения на платформе Linux и скрывает hello rest. Как мы включить дополнительные функции, они будут видны на портале hello.

Некоторые функции, такие как интеграция виртуальной сети, аутентификация Azure Active Directory, сторонняя аутентификация или расширения сайтов Kudu, в настоящее время недоступны. Когда эти возможности доступны, мы обновим наши документацию и блог об изменениях hello.

Это общедоступной предварительной версии в данный момент доступна только в hello следующие области:

* Запад США
* Восток США
* Западная Европа
* Северная Европа
* Южно-центральный регион США
* Северо-центральный регион США
* Юго-Восточная Азия
* Восточная Азия
* Восточная часть Австралии
* Восточная часть Японии
* Южная часть Бразилии
* Южная Индия

Веб-приложения на платформе Linux поддерживаются только в планах службы выделенного приложения hello и не имеет бесплатном или общем уровне. Кроме того, планы службы приложений для обычных веб-приложений и веб-приложений Linux взаимоисключающие. Это значит, что веб-приложение Linux нельзя создать в рамках плана службы приложений не для платформы Linux.

Веб-приложения на платформе Linux необходимо создать в группе ресурсов, который не содержит веб-приложений не Linux в hello одного региона.

## <a name="troubleshooting"></a>Устранение неполадок ##

При сбое приложения toostart или требуется ведение журнала hello toocheck из приложения, проверьте журналы Docker в каталог LogFiles hello hello. Доступ к этому каталогу можно получить либо на сайте SCM, либо через FTP.
toolog hello `stdout` и `stderr` из контейнера, необходимо tooenable **ведения журнала контейнера Docker** под **журналы диагностики**.

![Включение ведения журнала][2]

![С помощью журналов Docker tooview Kudu][1]

Получить доступ к сайту SCM hello **дополнительные средства** в hello **средства разработки** меню.

## <a name="next-steps"></a>Дальнейшие действия
См. следующие ссылки tooget к работе со службой приложения на платформе Linux hello. Если у вас возникли вопросы, опубликуйте их на [нашем форуме](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Как toouse пользовательские Docker изображения для веб-приложения Azure в Linux](app-service-linux-using-custom-docker-image.md)
* [Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux](app-service-linux-using-nodejs-pm2.md)
* [Использование .NET Core в веб-приложении службы приложений Azure на платформе Linux](app-service-linux-using-dotnetcore.md)
* [Использование Ruby в веб-приложении службы приложений Azure на платформе Linux](app-service-linux-ruby-get-started.md)
* [Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](app-service-linux-faq.md)
* [Поддержка SSH для веб-приложения Azure на платформе Linux](./app-service-linux-ssh-support.md)
* [Настройка промежуточных сред в службе приложений Azure](./web-sites-staged-publishing.md)
* [Непрерывное развертывание Docker Hub для веб-приложения Azure на платформе Linux](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png