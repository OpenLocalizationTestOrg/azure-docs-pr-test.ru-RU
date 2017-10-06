---
title: "aaaDeploy управления API Azure служб toomultiple Azure областей | Документы Microsoft"
description: "Узнайте, как toodeploy управления API Azure службы toomultiple экземпляра Azure областей."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>Как toodeploy управления API Azure службы toomultiple экземпляра Azure областей
API-Интерфейс управления поддерживает развертывание в нескольких регионах позволяющий toodistribute издателей API одну службу управления API между любым числом требуемой регионов Azure. Это сокращает задержки, связанные с географической удаленностью потребителей API, а также повышает доступность службы, когда какой-либо из регионов переходит в автономный режим. 

Если изначально создается служба управления API, он содержит только один [единицы] [ unit] и находится в одном регионе Azure, обозначенного как hello основной регион. Других регионах могут быть легко добавлена через hello портала Azure. Сервер шлюза управления API является tooeach развернутой области и вызова трафик будет поступать перенаправленное toohello ближайший шлюза. Если область переходит в автономный режим, трафик hello — toohello автоматически перенаправляется далее ближайший шлюза. 

> [!IMPORTANT]
> Развертывание в нескольких регионах доступен только в hello  **[Premium] [ Premium]**  уровня.
> 
> 

## <a name="add-region"></a>API управления службы экземпляра tooa новую область развертывания
> [!NOTE]
> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.
> 
> 

В портале Azure hello перейдите toohello **масштабирования и ценах** страницы для вашего экземпляра службы управления API. 

![Вкладка "Масштаб"][api-management-scale-service]

Новая область tooa toodeploy, если щелкнуть **+ добавить область** из инструментов hello.

![Добавление региона][api-management-add-region]

Выберите расположение hello hello раскрывающегося списка и задайте hello число единиц для с hello ползунка.

![Указание единиц][api-management-select-location-units]

Нажмите кнопку **добавить** tooplace выбора, сделанного в таблице hello. 

Повторите эту процедуру, чтобы отобразить все расположения, настроенные и нажмите кнопку **Сохранить** из процесса развертывания hello toostart инструментов hello.

## <a name="remove-region"> </a>Удаление экземпляра службы управления API из расположения
В портале Azure hello перейдите toohello **масштабирования и ценах** страницы для вашего экземпляра службы управления API. 

![Вкладка "Масштаб"][api-management-scale-service]

Для расположения hello хотелось бы tooremove откройте контекстное меню hello, с помощью hello **...**  кнопку в правом конце hello hello таблицы. Выберите hello **удалить** параметр.

![Удаление региона][api-management-remove-region]

Запрашивать подтверждение при удалении hello и нажмите кнопку **Сохранить** tooapply hello изменения.

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

