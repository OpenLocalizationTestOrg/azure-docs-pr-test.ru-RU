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
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="76600-103">Как tooconfigure уведомления и шаблонов в Azure API Management электронной почты</span><span class="sxs-lookup"><span data-stu-id="76600-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="76600-104">API управления предоставляет возможность hello tooconfigure уведомления для определенных событий и шаблонов сообщений электронной почты hello tooconfigure, используемые toocommunicate с hello администраторами и разработчиками экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="76600-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="76600-105">В этом разделе показано, как tooconfigure уведомления для hello доступных событий и общие сведения о настройке шаблонов hello сообщений электронной почты, используемый для этих событий.</span><span class="sxs-lookup"><span data-stu-id="76600-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="76600-106"><a name="publisher-notifications"> </a>Настройка уведомлений издателя</span><span class="sxs-lookup"><span data-stu-id="76600-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="76600-107">Щелкните уведомления tooconfigure **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="76600-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="76600-108">Откроется портал издателя управления API toohello.</span><span class="sxs-lookup"><span data-stu-id="76600-108">This takes you toohello API Management publisher portal.</span></span>

![Портал издателя][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="76600-110">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="76600-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="76600-111">Нажмите кнопку **уведомления** из hello **управления API** меню hello слева tooview hello доступных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="76600-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![Уведомления издателя][api-management-publisher-notifications]

<span data-ttu-id="76600-113">Hello следующий список событий можно настроить для уведомлений.</span><span class="sxs-lookup"><span data-stu-id="76600-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="76600-114">**Запросы подписок (требуется утверждение)** - hello получателей электронной почты указанного, и пользователи будут получать уведомления по электронной почте о запросах подписки для API продуктов, требующих оповещений.</span><span class="sxs-lookup"><span data-stu-id="76600-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="76600-115">**Новые подписки** - hello получателей электронной почты указанного, и пользователи будут получать уведомления по электронной почте о новых подписках API продукта.</span><span class="sxs-lookup"><span data-stu-id="76600-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="76600-116">**Запросы приложений коллекции** — hello указанного электронной почты получателей, и пользователи будут получать уведомления по электронной почте, когда новые приложения, отправленной toohello коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="76600-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="76600-117">**Скрытая копия** - hello указанного электронной почты получателей, и пользователи будут получать по электронной почте скрытых копий из всех электронных сообщений, отправляемых toodevelopers.</span><span class="sxs-lookup"><span data-stu-id="76600-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="76600-118">**Новый вопрос или комментарий** - hello электронной почты указанным получателям и пользователи будут получать уведомления по электронной почте, когда новый вопрос или комментарий отправляется на портал разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="76600-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="76600-119">**Сообщение закрытия учетной записи** - hello указанного электронной почты получателей, и пользователи будут получать уведомления по электронной почте, при закрытии учетной записи.</span><span class="sxs-lookup"><span data-stu-id="76600-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="76600-120">**Около подписки квоту** - hello следующих получателей электронной почты, и пользователи будут получать уведомления по электронной почте, при использовании подписки возвращает закрыть toousage квоты.</span><span class="sxs-lookup"><span data-stu-id="76600-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="76600-121">Для каждого события можно указать получателей электронной почты, с помощью текстового поля адрес электронной почты hello, или можно выбрать пользователей из списка.</span><span class="sxs-lookup"><span data-stu-id="76600-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="76600-122">toospecify toobe на адреса hello по электронной почте уведомление о том, введите их в поле адреса электронной почты hello.</span><span class="sxs-lookup"><span data-stu-id="76600-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="76600-123">При наличии нескольких адресов электронной почты разделяйте их с помощью запятых.</span><span class="sxs-lookup"><span data-stu-id="76600-123">If you have multiple email addresses, separate them using commas.</span></span>

![Получатели уведомлений][api-management-email-addresses]

<span data-ttu-id="76600-125">Щелкните toospecify hello пользователей toobe уведомления, **добавьте получателя**, установите флажок "hello" рядом с toobe пользователей hello уведомление о том и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="76600-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="76600-126">Только администраторы, отображаются в списке hello.</span><span class="sxs-lookup"><span data-stu-id="76600-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="76600-127">После настройки hello получателей уведомлений, щелкните **Сохранить** tooapply hello обновления получателей уведомления.</span><span class="sxs-lookup"><span data-stu-id="76600-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="76600-128">Если покинуть Здравствуй **издатель уведомлений** портал издателя hello вкладку предупреждения, если имеются несохраненные изменения.</span><span class="sxs-lookup"><span data-stu-id="76600-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="76600-129"><a name="email-templates"> </a>Настройка почтовых шаблонов</span><span class="sxs-lookup"><span data-stu-id="76600-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="76600-130">Управление API предоставляет шаблонов сообщений электронной почты для hello сообщения электронной почты, отправленных в курсе hello администрирования и с помощью службы hello.</span><span class="sxs-lookup"><span data-stu-id="76600-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="76600-131">предоставляются следующие шаблонов сообщений электронной почты Hello.</span><span class="sxs-lookup"><span data-stu-id="76600-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="76600-132">Отправка в коллекцию приложений утверждена</span><span class="sxs-lookup"><span data-stu-id="76600-132">Application gallery submission approved</span></span>
* <span data-ttu-id="76600-133">Прощальное письмо разработчика</span><span class="sxs-lookup"><span data-stu-id="76600-133">Developer farewell letter</span></span>
* <span data-ttu-id="76600-134">Уведомление о приближении предельной квоты разработчика</span><span class="sxs-lookup"><span data-stu-id="76600-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="76600-135">Приглашение пользователя</span><span class="sxs-lookup"><span data-stu-id="76600-135">Invite user</span></span>
* <span data-ttu-id="76600-136">Добавить новый комментарий tooan проблемы</span><span class="sxs-lookup"><span data-stu-id="76600-136">New comment added tooan issue</span></span>
* <span data-ttu-id="76600-137">Получена новая проблема</span><span class="sxs-lookup"><span data-stu-id="76600-137">New issue received</span></span>
* <span data-ttu-id="76600-138">Активирована новая подписка</span><span class="sxs-lookup"><span data-stu-id="76600-138">New subscription activated</span></span>
* <span data-ttu-id="76600-139">Подтверждение обновления подписки</span><span class="sxs-lookup"><span data-stu-id="76600-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="76600-140">Отклонение запроса подписки</span><span class="sxs-lookup"><span data-stu-id="76600-140">Subscription request declines</span></span>
* <span data-ttu-id="76600-141">Получен запрос подписки</span><span class="sxs-lookup"><span data-stu-id="76600-141">Subscription request received</span></span>

<span data-ttu-id="76600-142">При необходимости, эти шаблоны можно изменять.</span><span class="sxs-lookup"><span data-stu-id="76600-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="76600-143">tooview и настроить hello шаблонов сообщений электронной почты для вашего экземпляра API управления, щелкните **уведомления** из hello **API управления** меню слева Здравствуйте и выберите hello **шаблонов сообщений электронной почты**  вкладки.</span><span class="sxs-lookup"><span data-stu-id="76600-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![Почтовые шаблоны][api-management-email-templates]

<span data-ttu-id="76600-145">tooview или изменить указанный шаблон, выберите его из hello **шаблоны** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="76600-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![Список почтовых шаблонов][api-management-email-templates-list]

<span data-ttu-id="76600-147">Каждый почтовый шаблон имеет тему в формате обычного текста и определение тела в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="76600-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="76600-148">При необходимости, можно настраивать каждый элемент.</span><span class="sxs-lookup"><span data-stu-id="76600-148">Each item can be customized as desired.</span></span>

![Редактор почтовых шаблонов][api-management-email-template]

<span data-ttu-id="76600-150">Hello **параметры** список содержит список параметров, которые после вставлена hello теме или тексте, будет значением заменяемого hello назначен, при отправке электронной почты hello.</span><span class="sxs-lookup"><span data-stu-id="76600-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="76600-151">tooinsert параметра, поместите курсор hello, где правильно toogo параметр hello и нажмите кнопку hello стрелка влево toohello параметра с именем hello.</span><span class="sxs-lookup"><span data-stu-id="76600-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="76600-152">Нажмите кнопку **предварительного просмотра** или **отправить тестовое** toosee, как будет выглядеть hello электронной почты или отправить тестовое сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="76600-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="76600-153">Параметры Hello не заменяются фактическими значениями при предварительном просмотре или отправке теста.</span><span class="sxs-lookup"><span data-stu-id="76600-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="76600-154">toosave hello изменения toohello электронного сообщения, нажмите кнопку **Сохранить**, или нажмите кнопку изменения hello toocancel **отменить**.</span><span class="sxs-lookup"><span data-stu-id="76600-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

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
