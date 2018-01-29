---
title: "Обзор веб-приложений | Документация Майкрософт"
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
ms.openlocfilehash: f8510bb6b412e9af8aad30ba32bc74206c22042f
ms.sourcegitcommit: 804db51744e24dca10f06a89fe950ddad8b6a22d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2017
---
# <a name="web-apps-overview"></a>Обзор веб-приложений

*Веб-приложения службы приложений Azure* (или просто "Веб-приложения") — это служба для размещения веб-приложений, интерфейсов REST API и серверной части мобильных решений. Вы можете выполнять разработку на привычном языке: .NET, .NET Core, Java, Ruby, Node.js, PHP или Python. Эта служба также позволяет легко запускать и масштабировать приложения на виртуальных машинах Windows или Linux (см. статью [Вводные сведения о службе приложений Azure на платформе Linux](containers/app-service-linux-intro.md)). 

В службе "Веб-приложения" реализованы не только возможности Microsoft Azure для приложения, включая функции обеспечения безопасности, балансировки нагрузки, автоматического масштабирования и автоматизированного управления. Вы также можете воспользоваться такими преимуществами DevOps, как непрерывное развертывание из VSTS, GitHub, Docker Hub и других источников, управление пакетами, а также возможность использования промежуточных сред, личного домена и SSL-сертификатов. 

В службе приложений плата начисляется за используемые вычислительные ресурсы Azure. Используемые вычислительные ресурсы определяются _планом службы приложений_, в котором выполняется служба "Веб-приложения". Дополнительные сведения см. в статье [Подробный обзор планов службы приложений Azure](azure-web-sites-web-hosting-plans-in-depth-overview.md).

Это 5-минутное видео знакомит вас с веб-приложениями службы приложений Azure.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

## <a name="why-use-web-apps"></a>Зачем использовать веб-приложения?
Ниже представлены некоторые ключевые функции службы "Веб-приложения службы приложений".

* **Поддержка нескольких языков и платформ**. Служба "Веб-приложения" полностью поддерживает ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP и Python. Кроме того, вы можете запускать [PowerShell и другие скрипты или исполняемые файлы](web-sites-create-web-jobs.md) в качестве фоновых служб.
* **Оптимизация DevOps.** Настраивайте [непрерывную интеграцию и развертывание](app-service-continuous-deployment.md) в Visual Studio Team Services, GitHub, BitBucket, Docker Hub или службе контейнеров Azure. Повышайте уровень обновлений с помощью [тестовых и промежуточных сред](web-sites-staged-publishing.md). Управляйте приложениями в службе "Веб-приложения" с помощью оболочки [Azure PowerShell](/powershell/azureps-cmdlets-docs) или [кроссплатформенного интерфейса командной строки (CLI)](/cli/azure/install-azure-cli).
* **Высокодоступное глобальное масштабирование.** [Увеличивайте](web-sites-scale.md) либо [уменьшайте](../monitoring-and-diagnostics/insights-how-to-scale.md) размер вручную или автоматически. Храните приложения в любом месте глобальной инфраструктуры центра обработки данных. При этом [соглашение об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/app-service/) гарантирует высокую доступность.
* **Подключение к платформам SaaS и локальным данным.** Доступно более 50 [соединителей](../connectors/apis-list.md) для корпоративных систем (например, SAP), служб SaaS (например, Salesforce) и популярных интернет-служб (например, Facebook). Получайте доступ к локальным данным с помощью [гибридных подключений](../biztalk-services/integration-hybrid-connection-overview.md) и [виртуальных сетей Azure](web-sites-integrate-with-vnet.md).
* **Безопасность и соответствие требованиям.** Служба приложений совместима со стандартами [ISO, SOC и PCI](https://www.microsoft.com/TrustCenter/). Выполняйте аутентификацию пользователей с помощью [Azure Active Directory](app-service-mobile-how-to-configure-active-directory-authentication.md) или входа в учетные записи социальных сетей ([Google](app-service-mobile-how-to-configure-google-authentication.md), [Facebook](app-service-mobile-how-to-configure-facebook-authentication.md), [Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) и [Microsoft](app-service-mobile-how-to-configure-microsoft-authentication.md)). Создавайте [ограничения IP-адресов](app-service-ip-restrictions.md) и [управляйте удостоверениями службы](app-service-managed-service-identity.md).
* **Шаблоны приложений.** Вы можете выбрать любой шаблон приложения из обширного списка в [Azure Marketplace](https://azure.microsoft.com/marketplace/), например WordPress, Joomla и Drupal.
* **Интеграция с Visual Studio.** Выделенные инструменты в Visual Studio упрощают создание, развертывание и отладку приложений.
* **Функции API и мобильных приложений.** Служба "Веб-приложения" обеспечивает полную поддержку CORS для работы с RESTful API. Также она упрощает использование мобильных приложений, обеспечивая аутентификацию, автономную синхронизацию данных, отправку push-уведомлений и многое другое.
* **Независимый от сервера код.** Выполняйте фрагменты кода или скрипта по требованию без необходимости явно подготавливать и администрировать инфраструктуру. Платите только за время выполнения кода (см. статью [Документация по функциям Azure](/azure/azure-functions/)).

Помимо веб-приложений в службе приложений, Azure предлагает и другие службы, которые можно использовать для размещения веб-сайтов и веб-приложений. В большинстве случаев оптимальным вариантом являются веб-приложения.  Сведения об архитектуре микрослужб см. в статье о [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric). См. дополнительные сведения о дополнительном контроле над [виртуальными машинами Azure, на которых выполняется код](https://azure.microsoft.com/documentation/services/virtual-machines/). Дополнительные сведения о выборе между этими службами Azure см. в статье [Сравнение службы приложений Azure, виртуальных машин, Service Fabric и облачных служб](choose-web-site-cloud-service-vm.md).

## <a name="next-steps"></a>Дальнейшие действия

Создайте первое веб-приложение.

> [!div class="nextstepaction"]
> [ASP.NET](app-service-web-get-started-dotnet.md)

> [!div class="nextstepaction"]
> [PHP](app-service-web-get-started-php.md)

> [!div class="nextstepaction"]
> [Node.js](app-service-web-get-started-nodejs.md)

> [!div class="nextstepaction"]
> [Java](app-service-web-get-started-java.md)

> [!div class="nextstepaction"]
> [Python](app-service-web-get-started-python.md)

> [!div class="nextstepaction"]
> [HTML](app-service-web-get-started-html.md)

