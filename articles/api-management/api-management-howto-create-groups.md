---
title: "с помощью групп в Azure API управления учетными записями разработчиков aaaManage | Документы Microsoft"
description: "Узнайте, как разработчик toomanage учетных записей с помощью групп в службе управления API Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>Как разработчик toomanage группы toocreate и использование учетных записей в Azure API Management
В службе управления API группы — видимость hello используется toomanage toodevelopers продуктов. Продукты, первый toogroups сделан видимым и затем разработчики в эти группы могут просматривать и подписываться toohello продуктов, которые связаны с группами hello. 

Управление API имеет следующие группы неизменяемые hello.

* **Администраторы** — члены этой группы являются администраторами подписок Azure. Администраторы управления экземплярами службы управления API, создание hello API, операции и продукты, которые используются разработчиками.
* **Разработчики** — в эту группу входят пользователи портала разработчиков, прошедшие проверку подлинности. Разработчики, hello пользователи, создающие приложения, использующие собственные интерфейсы API. Разработчики предоставляются портал разработчиков toohello доступа и создавать приложения, которые вызывают hello операции API-интерфейса.
* **Гостевые системы** -непроверенных пользователей портала разработчиков, например потенциальных клиентов, посетив портал разработчиков hello падения экземпляр управления API в эту группу. Они могут быть предоставлены определенные доступа только для чтения, например tooview hello возможности API-интерфейсов, но не их вызова.

В дополнение toothese системные группы, администраторы могут создавать настраиваемые группы или [использование внешних групп в связанных клиентов Azure Active Directory][leverage external groups in associated Azure Active Directory tenants]. Пользовательские и внешних групп могут использоваться вместе со системные группы в предоставляя разработчикам видимость и доступ к tooAPI продуктов. Например, можно создать одну пользовательскую группу для разработчиков, связано с определенным организации партнера и разрешить им доступ toohello API-интерфейсы для продукта, содержащий соответствующие интерфейсы API. Пользователь может входить в несколько групп.

В этом руководстве показано, как администраторы экземпляра службы управления API могут добавлять новые группы и связывать их с продуктами и разработчиками.

> [!NOTE]
> В дополнение к этому toocreating групп и управление ими в портал издателя hello, можно создать и управлять группами с помощью API REST управления hello [группы](https://msdn.microsoft.com/library/azure/dn776329.aspx) сущности.
> 
> 

## <a name="create-group"> </a>Создание группы
toocreate новую группу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API. Откроется портал издателя управления API toohello.

![Портал издателя][api-management-management-console]

> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.
> 
> 

Нажмите кнопку **группы** из hello **API управления** меню hello слева, а затем нажмите **добавить группу**.

![Добавление новой группы][api-management-add-group]

Введите уникальное имя для группы hello и описание (необязательно) и нажмите кнопку **Сохранить**.

![Добавление новой группы][api-management-add-group-window]

Hello новая группа появится в hello tooedit вкладку групп hello **имя** или **описание** hello группы, щелкните имя hello hello группы в списке hello. toodelete hello группы, нажмите кнопку **удалить**.

![Группа добавлена][api-management-new-group]

Теперь, когда hello группа будет создана, его можно связать с продуктами и разработчиков.

## <a name="associate-group-product"> </a>Связывание группы с продуктом
Щелкните tooassociate группы с продуктом, **продуктов** из hello **API управления** меню hello и выберите команду hello имя нужного продукта hello.

![Настройка видимости][api-management-add-group-to-product]

Выберите hello **видимость** вкладке tooadd и удаление групп и tooview hello текущих групп hello продукта. tooadd или удалите группы, установите или снимите флажки hello в случае, для hello требуемого группы и нажмите кнопку **Сохранить**.

![Настройка видимости][api-management-add-group-to-product-visibility]

> [!NOTE]
> tooadd группы Azure Active Directory, см. [как разработчик tooauthorize учетных записей с помощью Azure Active Directory в Azure API Management](api-management-howto-aad.md).
> 
> tooconfigure группы из hello **видимость** для продукта, щелкните **Управление группами**.
> 
> 

Если продукт связан с группой, разработчики в этой группе можно просматривать и подписываться toohello продукта.

## <a name="associate-group-developer"> </a>Связывание групп с разработчиками
tooassociate групп с разработчиками, нажмите кнопку **пользователей** из hello **управления API** меню hello слева, а затем hello флажок рядом с hello разработчикам нужно tooassociate с группой.

![Добавить toogroup разработчика][api-management-add-group-to-developer]

После hello требуемого разработчикам проверяются, щелкните hello нужной группы в hello **добавить tooGroup** раскрывающегося списка. Разработчики могут быть удалены из групп с помощью hello **удалить из группы** раскрывающегося списка. 

![Разработчики][api-management-add-group-to-developer-saved]

После добавления hello связь между разработчиком hello и группой hello его можно просмотреть в hello **пользователей** вкладки.

## <a name="next-steps"> </a>Дальнейшие действия
* После добавления группы tooa разработчик можно просматривать и подписываться toohello продукты, связанные с данной группой. Дополнительные сведения см. в статье [Создание и публикация продукта в службе управления API Azure][How create and publish a product in Azure API Management].
* В дополнение к этому toocreating групп и управление ими в портал издателя hello, можно создать и управлять группами с помощью API REST управления hello [группы](https://msdn.microsoft.com/library/azure/dn776329.aspx) сущности.

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
