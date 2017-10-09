---
title: "aaaGuide toocreating шаблон решения для hello Marketplace | Документы Microsoft"
description: "Подробные инструкции, как toocreate, сертификации и развернуть решение шаблон изображения нескольких виртуальных Машин для покупки в Azure Marketplace hello."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a>Руководство по toocreate шаблон решения для Azure Marketplace
После завершения шага 1, [создания и регистрации учетной записи][link-acct-creation], вы интерактивной при создании hello шаблона решения Azure совместимой во [технические предварительные условия для создания шаблон решения](marketplace-publishing-solution-template-creation-prerequisites.md). Теперь мы поможет hello действия по созданию шаблона решения для нескольких виртуальных машин на hello [портал публикации] [ link-pubportal] для hello Azure Marketplace.

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a>Создание шаблона ваше решение предложение в hello портал публикации
Go слишком [https://publish.windowsazure.com](http://publish.windowsazure.com). При входе для hello первый раз toohello [портал публикации](https://publish.windowsazure.com/), используйте hello же учетной записи, под которым было зарегистрировано профиль продавца вашей компании. Позже в качестве соадминистратора в hello портал публикации можно добавить любой сотрудник вашей компании.

### <a name="1-select-solution-templates"></a>1. Выберите "Шаблоны решений"
  ![рисунок][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a>2. Создайте новый шаблон решения
  ![рисунок][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a>3. Начните с топологий
Шаблон решения — «родительский» tooall его топологий. В одном шаблоне предложений или решения можно определить сразу несколько топологий. При передаче toostaging предложение, то при переносе со всеми его топологии. Выполните действия hello ниже toodefine ваше предложение.     

* Создание топологии: «Идентификатор топологии» обычно — имя hello hello топологии для шаблона решения hello. Идентификатор Hello топологии используется в URL-адрес hello, как показано ниже:

  Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{пространство_имен_издателя}/{идентификатор_заказа}{идентификатор_топологии};

  портал Azure: https://portal.azure.com/#gallery/{пространство_имен_издателя}.{идентификатор_заказа}{идентификатор_топологии}.
* Добавьте новую версию.

### <a name="4-get-your-topology-versions-certified"></a>4. Сертифицируйте версии топологии
Отправка ZIP-файл, содержащий все требуемые файлы tooprovision конкретную версию hello топологии. Этот ZIP-файл должен содержать hello следующее:

* файлы *mainTemplate.json* и *createUiDefinition.json* в корневом каталоге;
* связанные шаблоны и все необходимые сценарии.

  > [!TIP]
  > Во время работы разработчиков по созданию решения hello топологии шаблона и их Сертифицирован бизнеса hello, маркетинга и/или юридических отделов компании могут работать hello маркетинговые и юридические материалы.
  >
  >

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда создан шаблон решения и отправлены hello ZIP-файл, следуйте инструкциям hello hello [руководство по содержимому маркетинга Marketplace](marketplace-publishing-push-to-staging.md) до отправки toostaging предложение hello. Посетите toosee hello полный набор marketplace публикация статей, [Приступая к работе: как toopublish toohello предложение Azure Marketplace](marketplace-publishing-getting-started.md).

Вас также могут заинтересовать следующие связанные статьи:

* Образы виртуальных машин: [Об образах виртуальных машин в Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)
* Расширения виртуальных машин: [общие сведения об агенте, расширениях](https://msdn.microsoft.com/library/azure/dn832621.aspx) и [компонентах виртуальных машин Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)
* Azure Resource Manager: [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) и [простые примеры шаблонов](https://github.com/rjmax/ArmExamples)
* Регулирует учетной записи хранилища: [как tooMonitor для регулирования учетной записи хранилища](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) и [хранилища Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
