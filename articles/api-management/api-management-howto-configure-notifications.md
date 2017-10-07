---
title: "aaaConfigure уведомления и шаблонов в Azure API Management электронной почты | Документы Microsoft"
description: "Узнайте, как tooconfigure уведомления и шаблонов в Azure API Management электронной почты."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a>Как tooconfigure уведомления и шаблонов в Azure API Management электронной почты
API управления предоставляет возможность hello tooconfigure уведомления для определенных событий и шаблонов сообщений электронной почты hello tooconfigure, используемые toocommunicate с hello администраторами и разработчиками экземпляра службы управления API. В этом разделе показано, как tooconfigure уведомления для hello доступных событий и общие сведения о настройке шаблонов hello сообщений электронной почты, используемый для этих событий.

## <a name="publisher-notifications"> </a>Настройка уведомлений издателя
Щелкните уведомления tooconfigure **портал издателя** в hello портала Azure для службы управления API. Откроется портал издателя управления API toohello.

![Портал издателя][api-management-management-console]

> [!NOTE] 
> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.

Нажмите кнопку **уведомления** из hello **управления API** меню hello слева tooview hello доступных уведомлений.

![Уведомления издателя][api-management-publisher-notifications]

Hello следующий список событий можно настроить для уведомлений.

* **Запросы подписок (требуется утверждение)** - hello получателей электронной почты указанного, и пользователи будут получать уведомления по электронной почте о запросах подписки для API продуктов, требующих оповещений.
* **Новые подписки** - hello получателей электронной почты указанного, и пользователи будут получать уведомления по электронной почте о новых подписках API продукта.
* **Запросы приложений коллекции** — hello указанного электронной почты получателей, и пользователи будут получать уведомления по электронной почте, когда новые приложения, отправленной toohello коллекции приложений.
* **Скрытая копия** - hello указанного электронной почты получателей, и пользователи будут получать по электронной почте скрытых копий из всех электронных сообщений, отправляемых toodevelopers.
* **Новый вопрос или комментарий** - hello электронной почты указанным получателям и пользователи будут получать уведомления по электронной почте, когда новый вопрос или комментарий отправляется на портал разработчиков hello.
* **Сообщение закрытия учетной записи** - hello указанного электронной почты получателей, и пользователи будут получать уведомления по электронной почте, при закрытии учетной записи.
* **Около подписки квоту** - hello следующих получателей электронной почты, и пользователи будут получать уведомления по электронной почте, при использовании подписки возвращает закрыть toousage квоты.

Для каждого события можно указать получателей электронной почты, с помощью текстового поля адрес электронной почты hello, или можно выбрать пользователей из списка.

toospecify toobe на адреса hello по электронной почте уведомление о том, введите их в поле адреса электронной почты hello. При наличии нескольких адресов электронной почты разделяйте их с помощью запятых.

![Получатели уведомлений][api-management-email-addresses]

Щелкните toospecify hello пользователей toobe уведомления, **добавьте получателя**, установите флажок "hello" рядом с toobe пользователей hello уведомление о том и нажмите кнопку **ОК**.

> [!NOTE] 
> Только администраторы, отображаются в списке hello.


После настройки hello получателей уведомлений, щелкните **Сохранить** tooapply hello обновления получателей уведомления.

> [!NOTE] 
> Если покинуть Здравствуй **издатель уведомлений** портал издателя hello вкладку предупреждения, если имеются несохраненные изменения.


## <a name="email-templates"> </a>Настройка почтовых шаблонов
Управление API предоставляет шаблонов сообщений электронной почты для hello сообщения электронной почты, отправленных в курсе hello администрирования и с помощью службы hello. предоставляются следующие шаблонов сообщений электронной почты Hello.

* Отправка в коллекцию приложений утверждена
* Прощальное письмо разработчика
* Уведомление о приближении предельной квоты разработчика
* Приглашение пользователя
* Добавить новый комментарий tooan проблемы
* Получена новая проблема
* Активирована новая подписка
* Подтверждение обновления подписки
* Отклонение запроса подписки
* Получен запрос подписки

При необходимости, эти шаблоны можно изменять.

tooview и настроить hello шаблонов сообщений электронной почты для вашего экземпляра API управления, щелкните **уведомления** из hello **API управления** меню слева Здравствуйте и выберите hello **шаблонов сообщений электронной почты**  вкладки.

![Почтовые шаблоны][api-management-email-templates]

tooview или изменить указанный шаблон, выберите его из hello **шаблоны** раскрывающегося списка.

![Список почтовых шаблонов][api-management-email-templates-list]

Каждый почтовый шаблон имеет тему в формате обычного текста и определение тела в формате HTML. При необходимости, можно настраивать каждый элемент.

![Редактор почтовых шаблонов][api-management-email-template]

Hello **параметры** список содержит список параметров, которые после вставлена hello теме или тексте, будет значением заменяемого hello назначен, при отправке электронной почты hello. tooinsert параметра, поместите курсор hello, где правильно toogo параметр hello и нажмите кнопку hello стрелка влево toohello параметра с именем hello.

Нажмите кнопку **предварительного просмотра** или **отправить тестовое** toosee, как будет выглядеть hello электронной почты или отправить тестовое сообщение электронной почты.

> [!NOTE] 
> Параметры Hello не заменяются фактическими значениями при предварительном просмотре или отправке теста.

toosave hello изменения toohello электронного сообщения, нажмите кнопку **Сохранить**, или нажмите кнопку изменения hello toocancel **отменить**.
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
