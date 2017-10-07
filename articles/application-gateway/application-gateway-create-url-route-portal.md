---
title: "Портал Azure — шлюз приложений Azure — правило aaaCreate, основанную на пути | Документы Microsoft"
description: "Узнайте, как правило на основе пути для шлюза приложения с помощью toocreate hello портала"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>Создание правила на основе пути для шлюза приложения с помощью портала hello

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

Маршрутизация URL-адрес на основе пути позволяет вам tooassociate маршрутов на основе hello пути URL-адреса HTTP-запроса. Он проверяет при внутреннем пул tooa маршрута, настроенный для hello URL, перечисленных в hello шлюза приложений и отправляет hello сетевой трафик toohello определенного пула серверной части. Обычно используются для маршрутизации на основе URL-адрес — tooload балансировать нагрузку по запросам для различных типов содержимого toodifferent серверных пулов.

Маршрутизация на основе URL-адрес появился новый шлюз tooapplication тип правила. Шлюз приложений имеет два типа правил: базовые правила и правила на основе пути. Здравствуйте, тип основные правила, предоставляет циклического службы для внутреннего интерфейса hello пулов при правила на основе пути Кроме распространения tooround циклический перебор, также учитывает шаблон пути URL-адреса запроса hello при выборе hello соответствующий внутренний пул.

## <a name="scenario"></a>Сценарий

Hello следующий сценарий рассмотрено создание правила на основе пути в существующего шлюза приложения.
Hello сценарии предполагается, что уже выполнены действия hello слишком[создания шлюза приложения](application-gateway-create-gateway-portal.md).

![Маршрут URL-адреса][scenario]

## <a name="createrule"></a>Создание правила на основе пути hello

Правила на основе пути требуется собственный прослушиватель перед созданием hello правило будет убедиться, что tooverify, у вас есть toouse доступных прослушивателя.

### <a name="step-1"></a>Шаг 1

Перейдите toohello [портал Azure](http://portal.azure.com) и выберите существующий шлюз приложений. Щелкните **Правила**

![Обзор шлюза приложений][1]

### <a name="step-2"></a>Шаг 2

Нажмите кнопку **основанную на пути** tooadd кнопку новое правило пути.

### <a name="step-3"></a>Шаг 3.

Hello **добавить правило на основе пути** колонке состоит из двух разделов. Первый раздел Hello —, где определен прослушиватель hello, имя hello hello правила и параметры пути по умолчанию hello. параметры пути по умолчанию Hello предназначены для маршрутов, не вошедшие в hello пользовательский путь маршрутов на основе. Здравствуйте, во второй части hello **добавить правило на основе пути** колонка является определение правила на основе пути hello сами.

**Основные параметры**

* **Имя** -это значение является понятное имя toohello правило, доступной на портале hello.
* **Прослушиватель** -это значение равно hello прослушиватель, который используется для правила hello.
* **По умолчанию серверный пул** -это является параметром hello, который определяет toobe hello серверной части, используемые для правила по умолчанию hello
* **Параметры HTTP по умолчанию** -это является параметром hello, который определяет параметры toobe hello HTTP, используемый для правила по умолчанию hello.

**Правила на основе пути**

* **Имя** -это значение — это понятное имя на основе toopath правило.
* **Пути** -этот параметр определяет hello путь hello правило ищет перенаправления трафика
* **Внутренний пул** -это является параметром hello, который определяет toobe серверной части hello, используемый для правила hello
* **Параметр HTTP** -это является параметром hello, который определяет параметры toobe hello HTTP, используется для правила hello.

> [!IMPORTANT]
> Путей: список hello toomatch шаблонов пути. Каждый должно начинаться с / и hello единственное место «\*» может быть на стороне hello. Примеры допустимых значений: /xyz, /xyz* или /xyz/*.  

![Колонка добавления правила на основе пути с заполненной информацией][2]

Добавление tooan правила на основе пути существующего шлюза приложения — это простой процесс, через портал hello. После создания правила на основе путь может быть измененного tooadd Дополнительные правила. 

![добавление правил на основе пути][3]

Так настраивается маршрут на основе пути. Важные toounderstand запросы не перезаписываются, при поступлении запросов шлюз приложений проверяет запрос hello и basic на hello URL-адрес шаблона отправляет hello запроса toohello соответствующие серверной части.

## <a name="next-steps"></a>Дальнейшие действия

toolearn tooconfigure разгрузки SSL со шлюзом приложения Azure, в статье [Настройка разгрузки SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
