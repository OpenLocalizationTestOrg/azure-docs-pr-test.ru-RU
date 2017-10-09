---
title: "aaaConfigure SSL разгрузки - шлюз Azure приложения - портал Azure | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate разгрузки шлюза приложения с помощью протокола SSL с помощью портала hello"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a>Настройка шлюза приложения для разгрузки SSL с помощью портала hello

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-ssl-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-ssl-arm.md)
> * [Классическая модель — Azure PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Шлюз приложения Azure может быть настроенный tooterminate hello Secure Sockets Layer (SSL) сеанс при hello шлюза tooavoid дорогостоящих SSL расшифровки задачи toohappen на hello веб-фермы. Разгрузка SSL также упрощает hello интерфейсном сервере настройку и управление ими hello веб-приложения.

## <a name="scenario"></a>Сценарий

следующие сценарии Hello проходит через Настройка разгрузки SSL для существующего шлюза приложения. Hello сценарии предполагается, что уже выполнены действия hello слишком[создания шлюза приложения](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Перед началом работы

tooconfigure разгрузки SSL со шлюзом приложений, требуется сертификат. Этот сертификат загружается на шлюзе приложения hello и использовать tooencrypt и расшифровки hello трафика, передаваемого через SSL. Hello сертификат должен toobe в формате обмена личной информацией (pfx). Этот формат позволяет для hello закрытого ключа toobe экспортированы, необходимые для hello приложения шлюза tooperform hello шифрованием/дешифрованием трафика.

## <a name="add-an-https-listener"></a>Добавление прослушивателя HTTPS

HTTPS-прослушиватель Hello ищет трафика в зависимости от конфигурации и помогает маршрута hello трафика toohello внутренние пулы.

### <a name="step-1"></a>Шаг 1

Найдите toohello портал Azure и выберите существующего шлюза приложения

### <a name="step-2"></a>Шаг 2

Нажмите кнопку прослушивателей затем tooadd кнопку hello добавить прослушиватель.

![Колонка обзора шлюза приложений][1]

### <a name="step-3"></a>Шаг 3.

Заполните необходимые сведения для прослушивателя hello hello и передачи hello PFX-файл сертификата, по завершении нажмите кнопку ОК.

**Имя** -это значение — это понятное имя прослушивателя hello.

**Конфигурация интерфейсных IP-адресов** -это значение равно hello IP-конфигурацию, используемый для прослушивателя hello.

**Интерфейсный порт (имя и порт)** -понятное имя для hello порт, используемый для внешнего интерфейса hello шлюза приложения hello и hello фактическое порт, используемый.

**Протокол** -toodetermine коммутатор, если для hello переднего плана используется протокол https или http.

**Сертификат (имя и пароль)** — если используется разгрузка SSL, то для этого параметра требуется указать PFX-файл сертификата, понятное имя и пароль.

![Колонка добавления прослушивателя][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a>Создание правила и связать его toohello прослушивателя

создан прослушиватель Hello. Это время toocreate трафика hello toohandle правило из hello прослушивателя. Правила определяют, как трафика перенаправленное toohello внутренние пулы на основе нескольких параметры конфигурации, включая использование сходство сеансов на основе файлов cookie, протокол, порт и проверках работоспособности.

### <a name="step-1"></a>Шаг 1

Нажмите кнопку hello **правила** шлюза приложения hello и нажмите кнопку Добавить.

![Колонка правил шлюза приложений][3]

### <a name="step-2"></a>Шаг 2

На hello **добавить базовое правило** колонки, введите в hello понятное имя для правила hello и нажмите на предыдущем шаге hello прослушивателя hello. Выберите соответствующий внутренний пул hello и настройка http и нажмите кнопку **ОК**

![Окно параметров HTTPS][4]

Hello параметры будут сохранены toohello шлюз приложений. Hello сохранения этих параметров может занять некоторое время, прежде чем они станут доступны tooview через портал hello или PowerShell. Шлюз приложений после сохранения hello обрабатывает hello шифрования и расшифровки трафика. Весь трафик между шлюзом приложения hello и hello серверной части веб-серверов будет осуществляться по протоколу http. Любой клиент задней toohello связи, если инициировано по протоколу https будет возвращаться клиента toohello зашифрован.

## <a name="next-steps"></a>Дальнейшие действия

toolearn tooconfigure пользовательские работоспособности проверки с помощью шлюза приложения Azure, в статье [создать пробу пользовательских работоспособности](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
