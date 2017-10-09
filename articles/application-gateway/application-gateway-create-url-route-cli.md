---
title: "правила с помощью маршрутизации URL-адрес шлюза приложения - aaaCreate Azure CLI 2.0 | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate, настройте шлюз приложения Azure с помощью правила маршрутизации URL-адрес"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>Создание шлюза приложений с помощью маршрутизации на основе пути с использованием Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

Маршрутизация URL-адрес на основе пути позволяет вам tooassociate маршрутов на основе hello пути URL-адреса HTTP-запроса. Он проверяет при внутреннем пул tooa маршрута, настроенный для hello URL-адрес, представленных в hello шлюза приложений и отправляет hello сетевой трафик toohello определенного пула серверной части. Обычно используются для маршрутизации на основе URL-адрес — tooload балансировать нагрузку по запросам для различных типов содержимого toodifferent серверных пулов.

Маршрутизация на основе URL-адрес появился новый шлюз tooapplication тип правила. Шлюз приложений имеет два типа правил: базовые правила и правила на основе пути. Основное правило тип предоставляет циклического службы для внутреннего интерфейса hello пулов при PathBasedRouting Кроме распространения tooround циклический перебор, также учитывает шаблон пути URL-адреса запроса hello при выборе пула hello серверной части.

## <a name="scenario"></a>Сценарий

В следующем примере hello, шлюз приложений обслуживает трафика для contoso.com с помощью двух серверных пулов: пул сервера по умолчанию и пул образ сервера.

Запросы для http://contoso.com/image * направлено пул серверов tooimage (imagesBackendPool), если hello не соответствует шаблон пути, выбранного пула сервера по умолчанию (appGatewayBackendPool).

![Маршрут URL-адреса](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Откройте hello **командной строки пакета Microsoft Azure**и войдите в систему. 

```azurecli
az login -u "username"
```

> [!NOTE]
> Можно также использовать `az login` без ключа hello для входа устройство, которое требуется ввод кода на aka.ms/devicelogin.

После ввода предшествующий пример hello предоставляется код. Перейдите toohttps://aka.ms/devicelogin в процессе входа hello toocontinue браузера.

![Команда, выводящая имя пользователя устройства][1]

В браузере hello введите полученный код hello. Все перенаправленные tooa-на страницу входа.

![Код tooenter браузера][2]

После ввода кода hello вы войдете в toocontinue hello закрыть браузер на со сценарием hello.

![Вход выполнен][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a>Добавление правила на основе пути tooan существующие приложения шлюза

Создание шлюза приложений с определенным правилом на основе пути

### <a name="create-a-new-back-end-pool"></a>Создание внутреннего пула

Настройка параметров шлюза приложения **imagesBackendPool** hello балансировки нагрузки сетевого трафика в пуле hello серверной части. В этом примере вы настройки другой пул серверной части для нового пула внутренней hello. Для каждого пула тыловых серверов параметры можно настроить отдельно.  Параметры HTTP серверной используются членами правила tooroute трафика toohello правильный внутренний пул. Определяет hello протокол и порт, используемый при отправке трафика члены пула toohello серверной части. Сеансы на основе файлов cookie, также определяются hello параметров серверного HTTP.  Если параметр включен, сходство сеансов на основе файлов cookie отправляет трафик toohello один внутренний как предыдущие запросы для каждого пакета.

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>Создание внешнего порта

Настройте hello интерфейсный порт для шлюза приложения. Объект конфигурации Hello интерфейсный порт используется toodefine прослушивателя что порт прослушивает трафик через прослушиватель hello шлюза приложения hello.

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>Создание прослушивателя

Настройте прослушиватель hello. Этот шаг позволяет настроить прослушиватель hello hello общедоступный IP-адрес и порт, используемый tooreceive входящего сетевого трафика. Следующий пример Hello принимает hello ранее настроен интерфейсный IP-конфигурации, конфигурацию интерфейсный порт и протокол (http или https) и настраивает hello прослушивателя. В этом примере hello прослушиватель прослушивает трафик tooHTTP порт 82 hello общедоступный IP-адрес, который был создан ранее.

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a>Создать сопоставление пути hello URL-адресов

Настройте правило пути URL-адресов для пулов hello серверной части. Этот шаг позволяет настроить hello относительный путь, используемый службой приложения шлюза toodefine hello сопоставления URL-адрес и какой пул внутренней назначается toohandle hello входящего трафика.

> [!IMPORTANT]
> Каждый путь должен начинаться с / и hello единственное место «\*» допускается, находится в конце hello. Примеры допустимых значений: /xyz, /xyz* или /xyz/*. Hello строка переданы сопоставителе toohello путь не содержит текст после hello сначала «?» или «#» и эти знаки не допускаются. 

Hello следующий пример создает одно правило для «/ images / *» путь маршрутизации трафика tooback-end «imagesBackendPool». Это правило обеспечивает трафика для каждого набора URL-адресов серверной части перенаправленного toohello. Например, http://adatum.com/images/figure1.jpg становится слишком «imagesBackendPool». Если путь hello не соответствует ни одному из правил предопределенный путь hello, hello правило пути карты конфигурация также настраивает пул адресов серверной части по умолчанию. Например http://adatum.com/shoppingcart/test.html переходит toopool1 как она определена в качестве пула по умолчанию hello для несопоставленных трафика.

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a>Дальнейшие действия

Если toolearn о разгрузки Secure Sockets Layer (SSL), см. [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl-cli.md).


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
