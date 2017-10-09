---
title: "aaaMap существующие пользовательские DNS имя tooAzure веб-приложений | Документы Microsoft"
description: "Узнайте, как tooadd существующий личный домен DNS имя веб-приложения tooa (именного домена), внутреннего сервера мобильного приложения или приложения API в службе приложений Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений

[Веб-приложения Azure](app-service-web-overview.md) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости. Этот учебник показывает, как toomap существующие пользовательские DNS имя tooAzure веб-приложений.

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Сопоставление поддомена (например, `www.contoso.com`) с помощью записи CNAME.
> * Сопоставление корневого домена (например, `contoso.com`) с помощью записи A.
> * Сопоставление домена с подстановочным знаком (например, `*.contoso.com`) с помощью записи CNAME.
> * Автоматизация сопоставления доменов с помощью скриптов.

Можно использовать любой **запись CNAME** или **запись** toomap пользовательские DNS имя tooApp службы. 

> [!NOTE]
> Мы рекомендуем использовать записи CNAME для всех настраиваемых DNS-имен, кроме корневого домена (например, `contoso.com`).

toomigrate действующем сайте и его tooApp имя домена DNS службы, см. раздел [миграции active tooAzure имя DNS службы приложений](app-service-custom-domain-name-migrate.md).

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

* [Создайте приложение службы приложений](/azure/app-service/) или используйте приложение, созданное для работы с другим руководством.
* Приобретите имени домена и убедитесь, что у вас есть доступ toohello DNS реестра поставщику домена (например, GoDaddy).

  Например, tooadd DNS-записей для `contoso.com` и `www.contoso.com`, должно быть параметров DNS может tooconfigure hello для hello `contoso.com` корневого домена.

  > [!NOTE]
  > Если у вас нет существующего домена имя, рассмотрите возможность [приобретение домена с помощью портала Azure "hello"](custom-dns-web-site-buydomains-web-app.md). 

## <a name="prepare-hello-app"></a>Подготовка приложения hello

toomap пользовательские DNS имя tooa веб-приложения, веб-приложения hello [план служб приложений](https://azure.microsoft.com/pricing/details/app-service/) должен быть платной уровня (**Shared**, **основные**, **Стандартная**, или  **"Премиум"**). На этом шаге вы убедитесь, что этого приложения службы, используемой в hello hello поддерживается ценовой категории.

### <a name="sign-in-tooazure"></a>Войдите в tooAzure

Откройте hello [портал Azure](https://portal.azure.com) и выполните вход с учетной записью Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Перейдите в приложение toohello в hello портал Azure

Hello в левом меню, выберите **службы приложений**, а затем выберите имя hello приложение hello.

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/select-app.png)

Вы увидите страницу управления hello объекта hello приложение служб приложений.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>Проверьте hello ценовой категории

Hello навигации страницы приложения hello слева, прокрутите toohello **параметры** , выберите **масштаб (план службы приложений)**.

![Меню увеличения масштаба](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

приложение Hello текущего уровня, выделяется синей рамкой. Убедитесь том, что приложение hello не hello toomake **Free** уровня. Пользовательские DNS не поддерживается в hello **Free** уровня. 

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Если hello план служб приложений не **Free**, закройте hello **выберите ценовую категорию** страницы и пропуска слишком[сопоставить запись CNAME](#cname).

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>Вертикальное масштабирование hello план служб приложений

Выберите любой из уровней занятых hello (**Shared**, **основные**, **Стандартная**, или **Premium**). 

Нажмите кнопку **Выбрать**.

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

При появлении hello после уведомления hello шкалы операция завершена.

![Подтверждение операции масштабирования](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>Сопоставление записи CNAME

В примере учебника hello, добавьте запись CNAME для hello `www` поддомен (например, `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Создайте запись CNAME hello

Добавление узла по умолчанию приложения toohello поддомен toomap записей CNAME (`<app_name>.azurewebsites.net`).

Для hello `www.contoso.com` пример домена добавьте запись CNAME, которая сопоставляет имя hello `www` слишком`<app_name>.azurewebsites.net`.

После добавления hello CNAME страницы записей DNS hello выглядит следующим образом hello в следующем примере.

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Разрешить сопоставление запись CNAME hello в Azure

В hello оставшийся навигации страницы приложения hello hello портал Azure, выберите **пользовательские домены**. 

![Меню личных доменов](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

В hello **пользовательские домены** страницы приложения hello, добавьте hello полное доменное имя настраиваемого DNS (`www.contoso.com`) toohello списка.

Выберите hello  **+**  значок Далее слишком**добавить имя узла**.

![Добавление имени узла](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Полное доменное имя типа hello, добавлена запись CNAME для, таких как `www.contoso.com`. 

Выберите **Проверка**.

Hello **добавить имя узла** кнопка активна. 

Убедитесь, что **тип записи имени узла** задано слишком**CNAME (www.example.com или любого поддомена)**.

Выберите **Добавить имя узла**.

![Добавить приложение toohello имя DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Он может занять некоторое время для нового узла toobe hello отражаются в приложение hello **пользовательские домены** страницы. Попробуйте обновить tooupdate hello hello обозревателя данных.

![Запись CNAME добавлена](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Если пропущена операция или сделали опечатку. вы Где-либо ранее, отображается ошибка проверки hello нижней части страницы приветствия.

![Ошибка проверки](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>Сопоставление записи A

В примере учебника hello, добавьте запись A для hello корневого домена (например, `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Скопируйте приложение hello IP-адрес

запись A toomap необходимо приложение hello внешний IP-адрес. Этот IP-адрес можно найти в приложение hello **пользовательские домены** страницу приветствия портал Azure.

В hello оставшийся навигации страницы приложения hello hello портал Azure, выберите **пользовательские домены**. 

![Меню личных доменов](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

В hello **пользовательские домены** скопируйте приложение hello IP-адрес.

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Создание записи hello

toomap A записей tooan приложения, службы приложений требуется **два** DNS-записей:

- **A** записи приложения toohello toomap IP-адрес.
- Объект **TXT** записи узла по умолчанию приложения toohello toomap `<app_name>.azurewebsites.net`. Службы приложений данная запись используется только во время настройки, tooverify, что вы являетесь владельцем hello пользовательского домена. После проверки и настройки личного домена в службе приложений эту TXT-запись можно удалить. 

Для hello `contoso.com` пример домена создайте hello A- и TXT записи, в соответствии с toohello в следующей таблице (`@` обычно представляет hello корневой домен). 

| Тип записи | Узел | Значение |
| - | - | - |
| A | `@` | IP-адрес из [приложение hello копирования IP-адрес](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

При добавлении записей hello, hello страницы записей DNS выглядит как следующий пример hello:

![Страница записей DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Включить запись сопоставления в приложение hello hello

Обратно в приложение hello **пользовательские домены** страницы приветствия портал Azure, добавьте hello полное доменное имя настраиваемого DNS (например, `contoso.com`) toohello списка.

Выберите hello  **+**  значок Далее слишком**добавить имя узла**.

![Добавление имени узла](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

Тип hello полное доменное имя настройки записи hello A, такие как `contoso.com`.

Выберите **Проверка**.

Hello **добавить имя узла** кнопка активна. 

Убедитесь, что **тип записи имени узла** задано слишком**записи (example.com)**.

Выберите **Добавить имя узла**.

![Добавить приложение toohello имя DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Он может занять некоторое время для нового узла toobe hello отражаются в приложение hello **пользовательские домены** страницы. Попробуйте обновить tooupdate hello hello обозревателя данных.

![Запись добавлена](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

Если пропущена операция или сделали опечатку. вы Где-либо ранее, отображается ошибка проверки hello нижней части страницы приветствия.

![Ошибка проверки](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>Сопоставление домена с подстановочными знаками

В обучающий пример hello, можно сопоставить [подстановочное DNS-имя](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (например, `*.contoso.com`) toohello приложением служб приложений, добавив запись CNAME. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Создайте запись CNAME hello

Добавление узла по умолчанию приложения имя подстановочные toohello toomap записей CNAME (`<app_name>.azurewebsites.net`).

Для hello `*.contoso.com` пример домена hello запись CNAME будет сопоставить имя hello `*` слишком`<app_name>.azurewebsites.net`.

При добавлении hello CNAME hello страницы записей DNS выглядит как следующий пример hello:

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Разрешить сопоставление запись CNAME hello в приложение hello

Теперь можно добавить любой дочерний домен, который соответствует приложение toohello имя hello подстановочный знак (например, `sub1.contoso.com` и `sub2.contoso.com` соответствует `*.contoso.com`). 

В hello оставшийся навигации страницы приложения hello hello портал Azure, выберите **пользовательские домены**. 

![Меню личных доменов](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Выберите hello  **+**  значок Далее слишком**добавить имя узла**.

![Добавление имени узла](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Введите полное доменное имя, которое совпадает с именем домена hello подстановочный знак (например, `sub1.contoso.com`), а затем выберите **проверки**.

Hello **добавить имя узла** кнопка активна. 

Убедитесь, что **тип записи имени узла** задано слишком**запись CNAME (www.example.com или любого поддомена)**.

Выберите **Добавить имя узла**.

![Добавить приложение toohello имя DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Он может занять некоторое время для нового узла toobe hello отражаются в приложение hello **пользовательские домены** страницы. Попробуйте обновить tooupdate hello hello обозревателя данных.

Выберите hello  **+**  значок снова tooadd другого имени узла, которое совпадает с именем домена hello подстановочный знак. Например, добавьте `sub2.contoso.com`.

![Запись CNAME добавлена](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>Тестирование в браузере

Обзор DNS-имен toohello ранее (например, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, и `sub2.contoso.com`).

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>Автоматизация с помощью сценариев

Можно автоматизировать управление пользовательскими доменами с помощью скриптов, с помощью hello [Azure CLI](/cli/azure/install-azure-cli) или [Azure PowerShell](/powershell/azure/overview). 

### <a name="azure-cli"></a>Инфраструктура CLI Azure 

Hello, следующая команда добавляет настроенное пользовательские DNS имя tooan приложением служб приложений. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

Дополнительные сведения см. в разделе [карты веб-приложения tooa пользовательского домена](scripts/app-service-cli-configure-custom-domain.md). 

### <a name="azure-powershell"></a>Azure PowerShell 

Hello, следующая команда добавляет настроенное пользовательские DNS имя tooan приложением служб приложений. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

Дополнительные сведения см. в разделе [назначить веб-приложения пользовательского домена tooa](scripts/app-service-powershell-configure-custom-domain.md).

## <a name="next-steps"></a>Дальнейшие действия

Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Сопоставление поддомена с помощью записи CNAME.
> * Сопоставление корневого домена с помощью записи A.
> * Сопоставление домена с подстановочным знаком с помощью записи CNAME.
> * Автоматизация сопоставления доменов с помощью скриптов.

Переместить следующий учебник toolearn toohello как toobind пользовательские SSL-сертификат tooa веб-приложения.

> [!div class="nextstepaction"]
> [Привязать существующий пользовательский SSL сертификат tooAzure веб-приложений](app-service-web-tutorial-custom-ssl.md)
