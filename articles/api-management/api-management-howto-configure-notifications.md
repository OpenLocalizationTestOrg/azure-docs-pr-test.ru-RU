---
title: "Настройка уведомлений и шаблонов писем в службе управления API Azure | Документация Майкрософт"
description: "Сведения о настройке уведомлений и шаблонов писем в службе управления API Azure"
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
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="2bcd2-103">Как настраивать уведомления и почтовые шаблоны в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="2bcd2-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="2bcd2-104">Служба управления API позволяет настраивать уведомления для определенных событий, а также почтовые шаблоны, которые используются для связи с администраторами и разработчиками экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="2bcd2-105">В этом разделе показано, как настраивать уведомления для доступных событий, и приводится обзор процесса настройки почтовых шаблонов, используемых для этих событий.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="2bcd2-106"><a name="publisher-notifications"> </a>Настройка уведомлений издателя</span><span class="sxs-lookup"><span data-stu-id="2bcd2-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="2bcd2-107">Для настройки уведомлений щелкните **Publisher portal** (Портал издателя) на портале Azure службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="2bcd2-108">Будет открыт портал издателя службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-108">This takes you to the API Management publisher portal.</span></span>

![Портал издателя][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="2bcd2-110">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2bcd2-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="2bcd2-111">Щелкните **Уведомления** в расположенном слева меню **Управление API** для просмотра доступных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Уведомления издателя][api-management-publisher-notifications]

<span data-ttu-id="2bcd2-113">Следующий список событий можно настроить для уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="2bcd2-114">**Запросы на подписку (требуется утверждение)** - Указанные получатели электронной почты и пользователи будут получать почтовые уведомления о запросах подписки на продукты API, для которых требуются утверждение.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="2bcd2-115">**Новые подписки** - Указанные получатели электронной почты и пользователи будут получать почтовые уведомления о новых подписках на продукты API.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="2bcd2-116">**Запросы коллекции приложений** - Указанные получатели электронной почты и пользователи будут получать почтовые уведомления при поступлении новых заявлений в коллекцию приложений.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="2bcd2-117">**BCC** - Указанные получатели электронной почты и пользователи будут получать слепые копии всех сообщений электронной почты, отправленных разработчикам.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="2bcd2-118">**Новая проблема или комментарий** - Указанные получатели электронной почты и пользователи будут получать почтовые уведомления при поступлении сведений о новой проблеме или комментария на портал разработчика.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="2bcd2-119">**Сообщение о закрытии учетной записи** - Указанные получатели электронной почты и пользователи будут получать почтовые уведомления при закрытии учетной записи.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="2bcd2-120">**Приближается предельная квота подписок** - Указанные получатели электронной почты и пользователи будут получать почтовые уведомления, когда использование подписок приблизится к квоте использования.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="2bcd2-121">Для каждого события можно указать получателей электронной почты с помощью текстового поля адреса электронной почты или можно выбрать пользователей в списке.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="2bcd2-122">Для указания адресов электронной почты, которые должны будут получать уведомления, введите их в текстовом поле адресов электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="2bcd2-123">При наличии нескольких адресов электронной почты разделяйте их с помощью запятых.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-123">If you have multiple email addresses, separate them using commas.</span></span>

![Получатели уведомлений][api-management-email-addresses]

<span data-ttu-id="2bcd2-125">Для указания пользователей, которые должны будут получать уведомления, щелкните **Добавить получателя**, установите флажок рядом с пользователями, которым будет необходимо отправлять уведомления, и щелкните**OK**.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="2bcd2-126">В списке отображаются только администраторы.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="2bcd2-127">После настройки получателей уведомлений щелкните **Сохранить** для применения обновленных получателей уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="2bcd2-128">В случае перехода с вкладки **Уведомления издателя** портал издателя предупредит вас, если остались несохраненные изменения.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="2bcd2-129"><a name="email-templates"> </a>Настройка почтовых шаблонов</span><span class="sxs-lookup"><span data-stu-id="2bcd2-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="2bcd2-130">API Management предоставляет почтовые шаблоны для сообщений электронной почты, которые отправляются во время администрирования и использования службы.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="2bcd2-131">Существуют следующие почтовые шаблоны.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-131">The following email templates are provided.</span></span>

* <span data-ttu-id="2bcd2-132">Отправка в коллекцию приложений утверждена</span><span class="sxs-lookup"><span data-stu-id="2bcd2-132">Application gallery submission approved</span></span>
* <span data-ttu-id="2bcd2-133">Прощальное письмо разработчика</span><span class="sxs-lookup"><span data-stu-id="2bcd2-133">Developer farewell letter</span></span>
* <span data-ttu-id="2bcd2-134">Уведомление о приближении предельной квоты разработчика</span><span class="sxs-lookup"><span data-stu-id="2bcd2-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="2bcd2-135">Приглашение пользователя</span><span class="sxs-lookup"><span data-stu-id="2bcd2-135">Invite user</span></span>
* <span data-ttu-id="2bcd2-136">Добавлен новый комментарий по проблеме</span><span class="sxs-lookup"><span data-stu-id="2bcd2-136">New comment added to an issue</span></span>
* <span data-ttu-id="2bcd2-137">Получена новая проблема</span><span class="sxs-lookup"><span data-stu-id="2bcd2-137">New issue received</span></span>
* <span data-ttu-id="2bcd2-138">Активирована новая подписка</span><span class="sxs-lookup"><span data-stu-id="2bcd2-138">New subscription activated</span></span>
* <span data-ttu-id="2bcd2-139">Подтверждение обновления подписки</span><span class="sxs-lookup"><span data-stu-id="2bcd2-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="2bcd2-140">Отклонение запроса подписки</span><span class="sxs-lookup"><span data-stu-id="2bcd2-140">Subscription request declines</span></span>
* <span data-ttu-id="2bcd2-141">Получен запрос подписки</span><span class="sxs-lookup"><span data-stu-id="2bcd2-141">Subscription request received</span></span>

<span data-ttu-id="2bcd2-142">При необходимости, эти шаблоны можно изменять.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="2bcd2-143">Для просмотра и настройки почтовых шаблонов для экземпляра API Management щелкните **Уведомления** в расположенном слева меню **Управление API** и перейдите на вкладку **Почтовые шаблоны**.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![Почтовые шаблоны][api-management-email-templates]

<span data-ttu-id="2bcd2-145">Для просмотра или изменения конкретного шаблона выберите его в раскрывающемся списке **Шаблоны** .</span><span class="sxs-lookup"><span data-stu-id="2bcd2-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![Список почтовых шаблонов][api-management-email-templates-list]

<span data-ttu-id="2bcd2-147">Каждый почтовый шаблон имеет тему в формате обычного текста и определение тела в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="2bcd2-148">При необходимости, можно настраивать каждый элемент.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-148">Each item can be customized as desired.</span></span>

![Редактор почтовых шаблонов][api-management-email-template]

<span data-ttu-id="2bcd2-150">Список **Параметры** содержит список параметров, который в случае вставки в тему или тело будет заменен на заданное значение при отправке сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="2bcd2-151">Для вставки параметра поместите курсор в то место, куда необходимо вставить параметр, и щелкните стрелку слева от имени параметра.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="2bcd2-152">Щелкните **Предварительный просмотр** или **Отправить тестовое сообщение**, чтобы увидеть, как будет выглядеть сообщение электронной почты, или отправить тестовое сообщение.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="2bcd2-153">При предварительном просмотре или отправке тестового сообщения параметры не заменяются фактическими значениями.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="2bcd2-154">Для сохранения изменений в почтовом шаблоне щелкните**Сохранить**. Для отмены изменений щелкните **Отменить**.</span><span class="sxs-lookup"><span data-stu-id="2bcd2-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
