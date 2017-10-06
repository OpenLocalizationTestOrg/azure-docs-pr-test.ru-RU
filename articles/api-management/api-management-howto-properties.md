---
title: "свойства toouse aaaHow в политики управления API Azure"
description: "Узнайте, как toouse свойств политики управления API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>Как toouse свойств политики управления API Azure
Политики управления API — это мощная возможность системы hello, разрешить издателю hello поведение hello toochange hello API через конфигурацию. Политики представляют собой набор инструкций, которые выполняются последовательно, по запросу hello или ответу API-интерфейса. Для создания правил политики можно использовать литеральные текстовые значения, выражения политики и свойства. 

Каждый экземпляр службы управления API имеет свойства коллекцию пар "ключ значение", содержащихся toohello глобальный экземпляр службы. Эти свойства можно использовать toomanage постоянные строковые значения для всех API конфигурации и политики. Каждое свойство имеет следующие атрибуты hello.

| Атрибут | Тип | Описание |
| --- | --- | --- |
| Name (Имя) |string |Имя свойства hello Hello. Может содержать только буквы, цифры, точки, тире и знаки подчеркивания. |
| Значение |string |значение свойства hello Hello. Не может быть пустым или состоять только из пробелов. |
| Секрет |Логическое |Определяет, является ли значение hello секрета и должны быть зашифрованы или нет. |
| Теги |Массив строк |Необязательный теги, если может быть список свойств используется toofilter hello. |

Свойства настраиваются на портале издателю hello hello **свойства** вкладки. В следующем примере hello настраиваются три свойства.

![Свойства][api-management-properties]

Значения свойств могут содержать строковые литералы и [выражения политики](https://msdn.microsoft.com/library/azure/dn910913.aspx). Hello следующей таблице показаны hello предыдущие три свойства и их атрибуты. Здравствуйте, значение `ExpressionProperty` является hello политики выражение, которое возвращает строку, содержащую текущую дату и время. Здравствуйте, свойство `ContosoHeaderValue` помечен как секретного кода, поэтому его значение не отображается.

| Имя | Значение | Секрет | Теги |
| --- | --- | --- | --- |
| ContosoHeader |TrackingId |Ложь |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |Истина |Contoso |
| ExpressionProperty |@(DateTime.Now.ToString()) |Ложь | |

## <a name="toouse-a-property"></a>Свойство toouse
Имя свойства hello месте внутри пары двойных фигурных скобок toouse свойства в политике, например `{{ContosoHeader}}`, как показано в следующий пример hello.

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

В этом примере `ContosoHeader` используется как hello имя заголовка в `set-header` политики, и `ContosoHeaderValue` используется в качестве hello значение этого заголовка. Если эта политика вычисляется во время запроса или ответа toohello API управления шлюзом, `{{ContosoHeader}}` и `{{ContosoHeaderValue}}` будут заменены соответствующими значениями свойств.

Свойства можно использовать как полный атрибут или элемент значения, как показано в предыдущем примере hello, но они также быть вставлена или вместе с частью выражения литеральный текст, как показано в следующий пример hello:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

Свойства могут также содержать выражения политики. В следующем примере hello, hello `ExpressionProperty` используется.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

При оценке этой политики `{{ExpressionProperty}}` заменяется своим значением: `@(DateTime.Now.ToString())`. Поскольку значение hello выражения политики, вычисляется выражение hello и hello политики продолжается с его выполнением.

Эту возможность можно проверить на портале разработчиков hello, вызвав операцию, которая имеет политику со свойствами в области. В следующем примере hello, эта операция называется hello два предыдущих примера `set-header` политики со свойствами. Обратите внимание, что ответ hello содержит два пользовательские заголовки, которые были настроены с помощью политик со свойствами.

![Портал разработчика][api-management-send-results]

Если взглянуть на hello [трассировки API инспектора](api-management-howto-api-inspector.md) для вызова, включающую hello два предыдущих примера политики со свойствами, можно увидеть два hello `set-header` политики со значениями свойств hello, вставки, а также выражение политики hello оценки для hello свойства, которое содержит выражение политики hello.

![Трассировка с помощью инспектора API][api-management-api-inspector-trace]

Обратите внимание, что хотя значения свойств могут содержать выражения политики, они не могут содержать другие свойства. Если текст, содержащий ссылку на свойство используется для значения свойства, такие как `Property value text {{MyProperty}}`, что ссылку на свойство не будет заменена и будут включены в значение свойства hello.

## <a name="toocreate-a-property"></a>Свойство toocreate
toocreate свойство, нажмите кнопку **добавить свойство** на hello **свойства** вкладки.

![Добавление свойства][api-management-properties-add-property-menu]

Поля **Имя** и **Значение** обязательны для заполнения. Если это свойство имеет значение секрета, проверьте hello **это секрет** флажок. Введите один или несколько необязательных тегов toohelp с упорядочение свои свойства и нажмите кнопку **Сохранить**.

![Добавление свойства][api-management-properties-add-property]

При сохранении нового свойства hello **свойства поиска** текстовое поле заполняется hello имя нового свойства hello и отображается новое свойство hello. Очистить все свойства toodisplay hello **свойства поиска** текстовое поле и нажмите клавишу ВВОД.

![Свойства][api-management-properties-property-saved]

Сведения о создании свойства с помощью hello REST API см. в разделе [создавать свойства с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).

## <a name="tooedit-a-property"></a>Свойство tooedit
tooedit свойство, нажмите кнопку **изменить** рядом с tooedit свойство hello.

![Изменение свойства][api-management-properties-edit]

Внесите необходимые изменения и нажмите кнопку **Сохранить**. Если изменить имя свойства hello, все политики, которые ссылаются на это свойство, автоматически обновляются toouse hello новое имя.

![Изменение свойства][api-management-properties-edit-property]

Сведения об изменении свойства с помощью API-интерфейса REST hello. в разделе [изменить свойства с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).

## <a name="toodelete-a-property"></a>Свойство toodelete
toodelete свойство, нажмите кнопку **удалить** рядом с toodelete свойство hello.

![Изменение свойства][api-management-properties-delete]

Нажмите кнопку **Да, удалите его** tooconfirm.

![Подтверждение удаления][api-management-delete-confirm]

> [!IMPORTANT]
> Если свойство hello ссылается на какие-либо политики, будут недоступны toosuccessfully удалить его, пока вы не удалите hello свойств всех политик, которые его используют.
> 
> 

Сведения об удалении свойства с помощью API-интерфейса REST hello. в разделе [удалить свойство, с помощью API-интерфейса REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).

## <a name="toosearch-and-filter-properties"></a>свойства toosearch и фильтр
Hello **свойства** вкладку включает в себя поиск и фильтрация toohelp возможности управлять свои свойства. Список свойств hello toofilter по имени свойства, введите условие поиска в hello **свойства поиска** текстового поля. Очистить все свойства toodisplay hello **свойства поиска** текстовое поле и нажмите клавишу ВВОД.

![Поиск][api-management-properties-search]

Список свойств hello toofilter значениями tag, введите один или несколько тегов в hello **фильтрации по тегам** текстового поля. Очистить все свойства toodisplay hello **фильтрации по тегам** текстовое поле и нажмите клавишу ВВОД.

![Фильтр][api-management-properties-filter]

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше о работе с политиками
  * [Политики в управлении API](api-management-howto-policies.md)
  * [Справочник по политикам](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [Выражения политики](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>Просмотр видеообзора
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

