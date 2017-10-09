---
title: "aaaGetting работает с Foundry облака в Microsoft Azure | Документы Microsoft"
description: "Запуск OSS или Pivotal Cloud Foundry в Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Cloud Foundry в Azure

Cloud Foundry — это платформа как услуга (PaaS) с открытым кодом, предназначенная для сборки, развертывания и эксплуатации 12-факторных приложений, разработанных с использованием разных языков и платформ. В этом документе описываются параметры hello, которые имеют по запуску Foundry облака в Azure и как можно начать работу.

## <a name="cloud-foundry-offerings"></a>Предложения Cloud Foundry

Существует две формы доступных toorun Foundry облака в Azure: Foundry облака (OSS CF) открытым исходным кодом и жизненно важную Foundry облака (PCF). OSS CF является полностью [открытая](https://github.com/cloudfoundry) версии Foundry облака под управлением hello Foundation Foundry облака. Жизненно важную Foundry облака состоит в распределении enterprise Foundry облака из жизненно важную Inc. программного обеспечения Мы рассмотрим некоторые hello различия между двумя предложениями hello.

### <a name="open-source-cloud-foundry"></a>Cloud Foundry с открытым кодом

Можно развернуть OSS Foundry облака в Azure, сначала развертывание директора BOSH, а затем развернуть Foundry облака, используя hello [инструкциям на сайте GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md). toolearn Подробнее об использовании OSS CF см hello [документации](https://docs.cloudfoundry.org/) предоставляемые hello Foundation Foundry облака.

Корпорация Майкрософт обеспечивает поддержку усилия для OSS CF через hello, следуя каналах сообщества:

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>канал bosh-azure-cpi на сайте [Cloud Foundry Slack](https://slack.cloudfoundry.org/);
- [список рассылки cf-bosh](https://lists.cloudfoundry.org/pipermail/cf-bosh);
- Проблемы, связанные с GitHub hello [знаков на ДЮЙМ](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) и [компонента service broker](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> уровень поддержки для ресурсов Azure, таких как виртуальные машины hello, где выполняется Foundry облака Hello основан на соглашении поддержки Azure. Поддержка сообщества усилия применяется только компоненты toohello Foundry специфичную для облака.

### <a name="pivotal-cloud-foundry"></a>Pivotal Cloud Foundry

Жизненно важную Foundry облака включает hello одной базовой платформой как hello OSS распространения, вместе с набором средств управления собственности и Корпоративная поддержка. toorun PCF в Azure, необходимо приобрести лицензию из Pivotal. 90-дневная пробная лицензия включает в себя предложение PCF Hello hello Azure marketplace.

Hello средства включают в себя [жизненно важную Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), веб-приложения, который упрощает развертывание и управление основу Foundry облака, и [жизненно важную Диспетчер приложений](https://docs.pivotal.io/pivotalcf/console/), веб-приложение для управления пользователи и приложения.

Кроме перечисленных выше CF OSS каналы поддержки toohello, PCF лицензия вы toocontact Pivotal для поддержки. Microsoft и Pivotal также включена поддержка рабочих процессов, которые позволяют вам toocontact любой из сторон обратитесь за помощью и ваш запрос правильной маршрутизации в зависимости от того, чем состоит проблема hello.

## <a name="azure-service-broker"></a>Azure Service Broker

Облако Foundry стимулирует hello [«коэффициент 12 app»](https://12factor.net/) методологии, который обеспечивает четкое разделение процессов без сохранения состояния приложения и резервном служб с отслеживанием состояния. [Службы брокеров](https://docs.cloudfoundry.org/services/api.html) обеспечивают tooprovision согласованный способ и выполнить привязку службы tooapplications резервного. Hello [Azure сервис-брокера](https://github.com/Azure/meta-azure-service-broker) предоставляет некоторые hello основных служб Azure через этот канал, включая хранилища Azure и Azure SQL.

При использовании жизненно важную Foundry облака, компонент service broker hello также является [доступен в качестве плитки](https://docs.pivotal.io/azure-sb/installing.html) из hello жизненно важную сети.

## <a name="related-resources"></a>Связанные ресурсы

### <a name="visual-studio-team-services-plugin"></a>Подключаемый модуль Visual Studio Team Services

Облако Foundry — хорошо подходит tooagile разработки программного обеспечения, включая использование hello непрерывной интеграции (CI) и непрерывной поставки (CD). Если использовать Visual Studio Team Services (VSTS) toomanage проектами и хотите tooset копирование элемента конфигурации/CD конвейера, предназначенных для облака Foundry, можно использовать hello [расширение сборки VSTS облака Foundry](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension). Hello подключаемый модуль делает простой tooconfigure и автоматизации развертывания tooCloud Foundry, ли работает в Azure или другой среды.

## <a name="next-steps"></a>Дальнейшие действия

- [Развертывание жизненно важную Foundry облака из hello Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [Развертывание приложения tooCloud Foundry в Azure](./cloudfoundry-deploy-your-first-app.md)
