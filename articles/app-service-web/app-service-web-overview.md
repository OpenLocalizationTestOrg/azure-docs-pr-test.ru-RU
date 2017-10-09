---
title: "Обзор приложений aaaWeb | Документы Microsoft"
description: "Узнайте, как служба приложений Azure помогает разрабатывать и размещать веб-приложения."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>Обзор веб-приложений
*Веб-приложения службы приложений* — это полностью управляемая вычислительная платформа, оптимизированная для размещения веб-сайтов и веб-приложений. Это [платформа как служба](https://en.wikipedia.org/wiki/Platform_as_a_service) предложение Microsoft Azure (PaaS) позволяет вам сосредоточиться на бизнес-логики, пока Azure заботится об инфраструктуре toorun hello и масштабирования приложения.

следующие видео 5-минутного Hello вводит веб-приложениях службы приложений Azure.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>Что такое веб-приложение в службе приложений?
В службе приложений *веб-приложения* — hello вычислительных ресурсов, предоставляемых Azure для размещения веб-сайта или веб-приложения.  

Hello вычислительные ресурсы могут находиться на общий или выделенный виртуальных машин (ВМ), в зависимости от ценовой категории, выбранная hello. Код приложения выполняется на управляемой виртуальной машине, которая изолирована от других клиентов.

Этот код может быть создан на любом языке или платформе, поддерживаемой [службой приложений Azure](../app-service/app-service-value-prop-what-is.md), включая ASP.NET, Node.js, Java, PHP или Python. В веб-приложениях также можно запускать скрипты, которые используют [PowerShell и другие языки сценариев](web-sites-create-web-jobs.md#acceptablefiles) .

Примеры сценариев приложений обычно можно использовать веб-приложений для см. в разделе [веб-сценариев приложения](https://azure.microsoft.com/documentation/scenarios/web-app/) и hello **сценарии и рекомендации** раздел [службе приложений Azure, Virtual Сравнение машин, Service Fabric и облачные службы](choose-web-site-cloud-service-vm.md#scenarios).

## <a name="why-use-web-apps"></a>Зачем использовать веб-приложения?
Ниже приведены некоторые ключевые возможности службы приложений, применяемые tooWeb приложений.

* **Поддержка нескольких языков и платформ.** Служба приложений превосходно поддерживает ASP.NET, Node.js, Java, PHP и Python. Кроме того, вы можете запустить [PowerShell и другие скрипты или исполняемые файлы](web-sites-create-web-jobs.md) в виртуальных машинах службы приложений.
* **Оптимизация DevOps.** Настраивайте [непрерывную интеграцию и развертывание](app-service-continuous-deployment.md) в Visual Studio Team Services, GitHub или BitBucket. Повышайте уровень обновлений с помощью [тестовых и промежуточных сред](web-sites-staged-publishing.md). Выполняйте [тестирование A/B](app-service-web-test-in-production-get-start.md). Управлять приложениями в службе приложений с помощью [Azure PowerShell](/powershell/azureps-cmdlets-docs) или hello [межплатформенного интерфейса командной строки (CLI)](../cli-install-nodejs.md).
* **Высокодоступное глобальное масштабирование.** [Увеличивайте](web-sites-scale.md) либо [уменьшайте](../monitoring-and-diagnostics/insights-how-to-scale.md) размер вручную или автоматически. Размещение приложений в любом месте инфраструктуры глобальных центров обработки данных корпорации Майкрософт и hello службы приложений [соглашения об уровне ОБСЛУЖИВАНИЯ](https://azure.microsoft.com/support/legal/sla/app-service/) обещания высокого уровня доступности.
* **Платформы и локальных данных tooSaaS подключений** -выбрать из более чем 50 [соединители](../connectors/apis-list.md) систем предприятия (например, SAP, Siebel и Oracle), служб SaaS (например, Salesforce и Office 365) и Интернет службы (например, Facebook и Twitter). Получайте доступ к локальным данным с помощью [гибридных подключений](../biztalk-services/integration-hybrid-connection-overview.md) и [виртуальных сетей Azure](web-sites-integrate-with-vnet.md).
* **Безопасность и соответствие требованиям.** Служба приложений совместима со стандартами [ISO, SOC и PCI](https://www.microsoft.com/TrustCenter/).
* **Шаблоны приложений** -выберите с помощью различных шаблонов приложений в hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) , которые позволяют использовать мастер tooinstall популярных открытая программного обеспечения как WordPress, Drupal и Joomla.
* **Интеграция с Visual Studio** -выделенного средства в Visual Studio оптимизировать работу hello создания, развертывания и отладки.

Кроме того, веб-приложение может использовать преимущества функций, предлагаемых [приложениями API](../app-service-api/app-service-api-apps-why-best-platform.md) (например, поддержку CORS) и [мобильными приложениями](../app-service-mobile/app-service-mobile-value-prop.md) (например, push-уведомления). Дополнительные сведения о типах приложений в службе приложений см. в статье [Что такое служба приложений Azure?](../app-service/app-service-value-prop-what-is.md)

Помимо веб-приложений в службе приложений, Azure предлагает и другие службы, которые можно использовать для размещения веб-сайтов и веб-приложений. В большинстве сценариев веб-приложения является наилучшим вариантом hello.  Архитектура микрослужбу рассмотрим [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric)и если требуется больший контроль над hello, код выполняется на ВМ, рассмотрите возможность [виртуальных машинах Azure](https://azure.microsoft.com/documentation/services/virtual-machines/). Дополнительные сведения о том, как toochoose между этих служб Azure в разделе [службе приложений Azure, виртуальные машины, Service Fabric и облачные службы сравнения](choose-web-site-cloud-service-vm.md).

## <a name="getting-started"></a>Приступая к работе
tooget работы путем развертывания образца кода tooa новое веб-приложение в службе приложений, выполните одну из hello учебников по hello, следуя раскрывающемся списке. Вам понадобится бесплатная учетная запись Azure

> [!div class="op_single_selector"]
> * [Развертывание вашей первый tooAzure ASP.NET web app в 5 минут](app-service-web-get-started-dotnet.md)
> * [Развертывание вашего первого приложения tooAzure web PHP 5 минут](app-service-web-get-started-php.md)
> * [Развертывание вашего первого приложения tooAzure web Node.js в 5 минут](app-service-web-get-started-nodejs.md)
> * [Развертывание вашего первого приложения tooAzure web Java в 5 минут](app-service-web-get-started-java.md)
> * [Развертывание вашего первого приложения tooAzure web Python в течение 5 минут](app-service-web-get-started-python.md)
> * [Развертывание вашего первого узла tooAzure HTML 5 минут](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure. Создание начального приложения и воспроизведение к ней до часа tooan--без кредитной карты требуется, не обязательства.
> 
> 
