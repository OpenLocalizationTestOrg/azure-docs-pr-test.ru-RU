---
title: "aaaPolicies в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toocreate, изменить и настроить политики в службе управления API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a>Политики в Azure API Management
В Azure API Management политик — это мощная возможность системы hello, разрешить издателю hello поведение hello toochange hello API через конфигурацию. Политики представляют собой набор инструкций, которые выполняются последовательно, по запросу hello или ответу API-интерфейса. Среди наиболее популярных инструкций вспомнить преобразование формата XML tooJSON и toorestrict hello объема входящих вызовов от разработчика ограничение частоты вызовов. Стандартной hello доступны многие дополнительные политики.

В разделе hello [ссылка на политику] [ Policy Reference] полный список инструкций политики и их параметры.

Политики применяются внутри hello шлюза, который располагается между потребителя API hello и hello управляемых API. Hello шлюз получает все запросы и пересылает их без изменений обычно toohello базовый API. Однако политика может применяться изменения tooboth hello входящего запроса и исходящего ответа.

Выражения политики может использоваться как значения атрибутов или текстовыми значениями в любой hello политиках управления интерфейсами API, если политика hello не указывает иное. Некоторые политики, такие как hello [поток управления] [ Control flow] и [переменным] [ Set variable] политики основаны на выражениях политики. Чтобы узнать больше, ознакомьтесь с [расширенными политиками][Advanced policies] и [выражениями политики][Policy expressions].

## <a name="scopes"></a>Как tooconfigure политики
Политики можно настроить глобально или в области hello [продукта][Product], [API] [ API] или [операции] [Operation]. tooconfigure политики, перейдите в редактор политики toohello hello портала издателя.

![Меню «Политики»][policies-menu]

Редактор политики Hello состоит из трех основных частей: hello области (верхнего) hello политики определения политики где инструкций hello список (справа) и (слева) для изменения политики:

![Редактор политик][policies-editor]

Настройка политики, необходимо сначала выбрать область hello, на какие hello должна применяться политика toobegin. На снимке экрана приветствия ниже hello **начальный** выбранного продукта. Обратите внимание, что hello объект Далее toohello имя политики указывает на этом уровне уже применяется политика.

![Область][policies-scope]

Так как уже применена политика, hello конфигурация показана на просмотр определения hello.

![Настройка][policies-configure]

политика Hello отображается только для чтения на первом. В порядке tooedit определение hello щелкните hello **Настройка политики** действие.

![Редактирование][policies-edit]

Определение политики Hello — простой XML-документ, описывающий последовательность инструкций, входящих и исходящих подключений. Hello XML можно изменять непосредственно в окне определения hello. Список инструкций предоставляется право toohello и инструкций применимо toohello текущей области включены и выделяются; как видно hello **ограничение скорости вызова** инструкции снимке экрана приветствия выше.

Щелкнув оператор включен добавит hello соответствующий XML в расположении hello hello курсора в представлении определения hello. 

> [!NOTE]
> Hello политики, которые должны tooadd не включена, убедитесь, что находятся в неправильной области hello для этой политики. Каждая инструкция политики предназначена для использования в определенных областях и разделах политики. разделы политики tooreview hello и области для политики, проверьте hello **использование** раздел для этой политики в hello [ссылка на политику][Policy Reference].
> 
> 

Полный список инструкций политики и их параметры доступны в hello [ссылка на политику][Policy Reference].

Например, tooadd новый оператор toorestrict входящих запросов toospecified IP-адресов, поместите курсор hello внутри содержимого hello hello `inbound` hello XML элемент и нажмите кнопку **вызывающий объект ограничение IP-адресов** инструкции.

![Политики ограничения][policies-restrict]

При этом будет добавлено toohello фрагмент XML `inbound` элемент, описано, как tooconfigure hello инструкции.

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit входящие запросы и принимать только те из IP-адрес 1.2.3.4 изменить hello XML следующим образом:

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Сохранить][policies-save]

По завершении настройки hello инструкций для hello политики щелкните **Сохранить** hello изменения немедленно будут распространенный toohello API Management gateway.

## <a name="sections"> </a>Общая информация о конфигурации политики
Политика — это набор операторов, которые выполняются для создания запроса и получения ответа. Hello конфигурации состоит из соответствующим образом `inbound`, `backend`, `outbound`, и `on-error` разделов, как показано в hello следующая конфигурация.

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

Если возникает ошибка во время обработки запроса hello, все остальные шаги в hello `inbound`, `backend`, или `outbound` разделы пропускаются, и выполнение переходит toohello инструкций в hello `on-error` раздела. Путем размещения операторов политики в hello `on-error` раздел hello ошибки можно просмотреть с помощью hello `context.LastError` свойства, проверка и настройка с помощью hello hello отклик `set-body` политики и настроить, что происходит при возникновении ошибки. Предусмотрено кодов ошибок для встроенных действий и ошибки, возникающие во время обработки hello инструкций политики. Дополнительные сведения см. в статье [Обработка ошибок в политиках управления API](https://msdn.microsoft.com/library/azure/mt629506.aspx).

Так как на различных уровнях (глобальные, продукт, api и операции) можно указать политики конфигурации hello предоставляет способ для вас toospecify hello порядок, в котором определения политики hello инструкции выполняются с учетом toohello родительской политики. 

Области политики оцениваются в hello последовательностью.

1. Глобальная область
2. Область продукта
3. Область API
4. Область операций

Hello инструкций в них вычисляются toohello размещение hello в соответствии с `base` элемента, если он имеется. Глобальные политики имеет нет родительской политики и с помощью hello `<base>` элемент в нем не делает ничего.

Например при наличии политики на глобальном уровне hello и политика, заданная для API-Интерфейс, затем всякий раз, когда используется этот конкретный API обе политики применяются. Управление API позволяет детерминированным упорядочение инструкций объединенный политики через hello базового элемента. 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

В определении политики пример hello выше, hello `cross-domain` инструкция выполняется перед любой более поздней версии политики, которые в свою очередь, будет следовать hello `find-and-replace` политики. 

политики hello toosee в текущей области hello в редакторе hello политики, щелкните **пересчитать эффективную политику для выбранной области**.

## <a name="next-steps"></a>Дальнейшие действия
Посмотрите следующие видео о выражениях политики.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
