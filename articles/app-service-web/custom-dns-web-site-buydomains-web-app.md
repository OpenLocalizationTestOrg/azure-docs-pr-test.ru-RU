---
title: "aaaBuy пользовательское доменное имя для веб-приложений Azure"
description: "Узнайте, как имя toobuy пользовательский домен с веб-приложения в службе приложений Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Приобретение имени личного домена для веб-приложений Azure

Домены службы приложений (предварительная версия) — это домены верхнего уровня, которые управляются непосредственно в Azure. Они позволяют легко toomanage пользовательских доменов [веб-приложениях Azure](app-service-web-overview.md). Этот учебник показывает, как toobuy домен приложения службы и назначьте DNS имена tooAzure веб-приложений.

Эта статья предназначена для службы приложений Azure ("Веб-приложения", "Приложения API", "Мобильные приложения", Logic Apps). Для хранилища Azure или виртуальной Машине Azure в разделе [tooAzure домена назначение приложения службы виртуальных Машин или хранилище Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/). Сведения об облачных службах см. в статье [Настройка пользовательского доменного имени для облачной службы Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

* [Создайте приложение службы приложений](/azure/app-service/) или используйте приложение, созданное для работы с другим руководством.

## <a name="prepare-hello-app"></a>Подготовка приложения hello

toouse пользовательских доменов в Azure веб-приложений, веб-приложения [план служб приложений](https://azure.microsoft.com/pricing/details/app-service/) должен быть платной уровня (**Shared**, **основные**, **Стандартная**, или **Premium**). На этом шаге вы убедитесь, что веб-приложения hello в hello поддерживается ценовой категории.

### <a name="sign-in-tooazure"></a>Войдите в tooAzure

Откройте hello [портал Azure](https://portal.azure.com) и выполните вход с учетной записью Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Перейдите в приложение toohello в hello портал Azure

Hello в левом меню, выберите **службы приложений**, а затем выберите имя hello приложение hello.

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/select-app.png)

Вы увидите страницу управления hello объекта hello приложение служб приложений.  

### <a name="check-hello-pricing-tier"></a>Проверьте hello ценовой категории

Hello навигации страницы приложения hello слева, прокрутите toohello **параметры** , выберите **масштаб (план службы приложений)**.

![Меню увеличения масштаба](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

приложение Hello текущего уровня, выделяется синей рамкой. Убедитесь том, что приложение hello не hello toomake **Free** уровня. Пользовательские DNS не поддерживается в hello **Free** уровня. 

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Если hello план служб приложений не **Free**, закройте hello **выберите ценовую категорию** страницы и пропуска слишком[домена hello Покупка](#buy-the-domain).

### <a name="scale-up-hello-app-service-plan"></a>Вертикальное масштабирование hello план служб приложений

Выберите любой из уровней занятых hello (**Shared**, **основные**, **Стандартная**, или **Premium**). 

Нажмите кнопку **Выбрать**.

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

При появлении hello после уведомления hello шкалы операция завершена.

![Подтверждение операции масштабирования](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>Приобретение hello домена

### <a name="sign-in-tooazure"></a>Войдите в tooAzure
Откройте hello [портал Azure](https://portal.azure.com/) и выполните вход с учетной записью Azure.

### <a name="launch-buy-domains"></a>Запуск приобретения доменов
В hello **веб-приложений** щелкните имя веб-приложения, выберите hello **параметры**, а затем выберите **пользовательские домены**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

В hello **пользовательские домены** щелкните **купить домены**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>Настройка домена покупки hello

В hello **домен приложения службы** страницы в hello **поиск домена** введите имя домена на hello toobuy и тип `Enter`. Hello предлагаемые доступных доменов отображаются под hello текстовое поле. Выберите один или несколько доменов, которые вы хотите toobuy. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Нажмите кнопку hello **контактные данные** и заполните форму hello домена контактные данные. По завершении нажмите кнопку **ОК** tooreturn toohello домен приложения службы страницы.
   
Очень важно ввести правильные данные в обязательные поля. Неверные данные для получения контактной информации может привести к toopurchase домены сбоя. 

Затем выберите параметры hello требуемого для своего домена. См. в следующей таблице для объяснения hello.

| Настройка | Рекомендуемое значение | Описание |
|-|-|-|
|Автоматическое возобновление | **Включение** | Домен службы приложений автоматически возобновляется каждый год. Плата вашей кредитной карты hello одной цене покупки во время обновления hello. |
|Защита конфиденциальности | Включение | Соглашаться слишком «Защита личных», который включается в цены покупки hello _бесплатно_ (за исключением доменов верхнего уровня, реестр которого не поддерживают защиты конфиденциальности, таких как _. co.in_, _. CO.uk_и так далее). |
| Назначение имен узлов по умолчанию | **www** и **@** | Выберите hello требуемого привязки имени узла, при необходимости. По завершении операции покупки hello домена веб-приложения может осуществляться в hello выбранные имена узлов. Если веб-приложение hello находится за [диспетчера трафика Azure](https://azure.microsoft.com/services/traffic-manager/), вы не видите hello параметр tooassign hello корневого домена (@), так как поддержка записи A не диспетчера трафика. Можно изменять имя узла назначения toohello после завершения покупки домена hello. |

### <a name="accept-terms-and-purchase"></a>Принятие условий и приобретение

Нажмите кнопку **условия** tooreview hello термины и hello накладные расходы, нажмите кнопку **купить**.

> [!NOTE]
> Домены приложений службы используйте домены hello toohost Azure DNS. Кроме плата регистрации домена toohello, взимается плата за использование для Azure DNS. Дополнительные сведения см. на странице [цен на Azure DNS](https://azure.microsoft.com/pricing/details/dns/).
>
>

Вернитесь в hello **домен приложения службы** щелкните **ОК**. Во время операции hello появляется hello следующие уведомления:

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>Имена узлов hello теста

Если вы назначили по умолчанию имена узлов tooyour веб-приложения, также будет показано уведомление об успехе для каждого выбранного имени узла. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

Появится hello выбранные имена узлов в hello **пользовательские домены** страницы в hello **имена узлов** раздела. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

tootest приветствия имен узлов, перейдите в списке toohello имена узлов в браузере hello. В примере hello в hello предшествующий экрана, повторите перемещение too_kontoso.net_ и _www.kontoso.net_.

## <a name="assign-hostnames-tooweb-app"></a>Назначение приложения tooweb имена узлов

Если выбирается не tooassign одно или несколько веб-приложения tooyour по умолчанию имена узлов во время hello приобрести процесса, или если не требуется tooassign имени узла в списке, можно назначить имя узла в любое время.

Можно также назначить имена узлов в домен приложения службы tooany hello другие веб-приложения. Hello действия зависят от ли hello домен приложения службы и веб-приложения hello принадлежат toohello одной подписке.

- Другой подписке: сопоставить пользовательские записи DNS из веб-приложения toohello hello домен приложения службы как извне приобретенных домен. Сведения о добавлении пользовательских DNS-имена tooan домен приложения службы, см. в разделе [управление пользовательские записи DNS](#custom). toomap внешнего домена приобретенных tooa веб-приложение, в разделе [сопоставления существующих пользовательских DNS имя tooAzure веб-приложений](app-service-web-tutorial-custom-domain.md). 
- Одной подписке: hello используйте следующие шаги.

### <a name="launch-add-hostname"></a>Запуск добавления имени узла
В hello **службы приложений** страницу, выберите hello имя веб-приложения, должны tooassign имен узлов, выберите **параметры**, а затем выберите **пользовательские домены**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Убедитесь, что указано приобретенных домена в hello **доменов приложения службы** статьи, но не его выбрать. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Все домены приложения службы в одной подписке отображаются в веб-приложения hello hello **пользовательские домены** страницы. Если домен находится в подписке hello веб-приложения, но он не отображается в веб-приложения hello **пользовательские домены** страницы, повторите попытку открытия hello **пользовательские домены** страницы или обновить веб-страницу приветствия. Кроме того проверьте колокольчика уведомления hello вверху hello hello портал Azure для создания или выполнения сбоев.
>
>

Выберите **Добавить имя узла**.

### <a name="configure-hostname"></a>Настройка имени узла
В hello **добавить имя узла** диалогового окна, hello полное доменное имя типа службы домена приложения или любой дочерний домен. Например:

- kontoso.net
- www.kontoso.net
- abc.kontoso.net

По завершении выберите **Проверить**. Тип записи имени узла Hello выбирается автоматически.

Выберите **Добавить имя узла**.

По завершении операции hello появится уведомление об успехе для hello, назначенный имени узла.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>Закрытие страницы добавления имени узла
В hello **добавить имя узла** назначьте любое имя узла tooyour веб-приложения, в случае необходимости. После завершения закройте hello **добавить имя узла** страницы.

Вы увидите hostname(s) hello новые назначенные в вашем приложении **пользовательские домены** страницы.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>Имена узлов hello теста

Перейдите в списке toohello имена узлов в браузере hello. В примере перед экрана приветствия hello попробуйте too_abc.kontoso.net_ навигации.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>Управление пользовательскими записями DNS

В Azure управление записями DNS для домена службы приложений осуществляется с помощью [Azure DNS](https://azure.microsoft.com/services/dns/). Вы можете добавлять, удалять и обновлять записи DNS так же, как для приобретенного внешнего домена.

### <a name="open-app-service-domain"></a>Открытие домена службы приложений

В hello hello левого меню портала Azure выберите **более служб** > **доменов приложения службы**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Выберите домен toomanage hello. 

### <a name="access-dns-zone"></a>Доступ к зоне DNS

В левом меню hello домена, выберите **зоны DNS**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Это действие открывает hello [зоны DNS](../dns/dns-zones-records.md) страницы службы домена приложения в Azure DNS. Сведения о том, как tooedit DNS-записи, в разделе [как toomanage зоны DNS в hello портал Azure](../dns/dns-operations-dnszones-portal.md).

## <a name="cancel-purchase-delete-domain"></a>Отмена покупки (удаление домена)

После приобретения hello домен приложения службы, у вас есть пять дней toocancel покупки для возмещение. Через пять дней можно удалить hello домен приложения службы, но не может получить возмещение.

### <a name="open-app-service-domain"></a>Открытие домена службы приложений

В hello hello левого меню портала Azure выберите **более служб** > **доменов приложения службы**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Выберите hello tooyou домена требуется toocancel или удалить. 

### <a name="delete-hostname-bindings"></a>Удаление привязок имен узлов

В левом меню hello домена, выберите **привязки имени узла**. Здесь перечислены привязки имени узла Hello из всех служб Azure.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

Не удается удалить hello домен приложения службы, пока не будут удалены все привязки имени узла.

Удалите каждую привязку имени узла, выбрав **...** > **Удалить**. После удаления всех привязок hello выберите **Сохранить**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>Отмена или удаление

В левом меню hello домена, выберите **Обзор**. 

Если hello отмены в домене приобретенных hello не истекло, выберите **отменить покупку**. В противном случае вы увидите кнопку **Удалить**. домен hello toodelete без возврата, выберите **удалить**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

Выберите **ОК** tooconfirm hello операции. Если вы не хотите tooproceed, щелкните за пределами hello диалоговое окно подтверждения.

По завершении операции hello домена hello выпущено из подписки и доступна для тех, кто toopurchase еще раз. 
