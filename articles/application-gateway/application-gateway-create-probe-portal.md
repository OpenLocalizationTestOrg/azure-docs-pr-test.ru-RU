---
title: "aaaCreate пользовательской проверки - шлюз Azure приложения - портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate пользовательской проверки для шлюза приложения с помощью портала hello"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>Создать пользовательский зонд для шлюза приложения с помощью портала hello

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-probe-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-probe-ps.md)
> * [Классическая модель — Azure PowerShell](application-gateway-create-probe-classic-ps.md)

В этой статье добавьте пользовательский зонд tooan существующий шлюз приложений через портал Azure hello. Пользовательские зонды полезны для приложений, имеющих страницы проверки работоспособности конкретного или для приложений, которые не предоставляют успешный ответ на веб-приложения по умолчанию hello.

## <a name="before-you-begin"></a>Перед началом работы

Если вы не сделали этого шлюза приложения, посетите [создания шлюза приложения](application-gateway-create-gateway-portal.md) toocreate toowork шлюза приложения с.

## <a name="createprobe"></a>Создать пробу hello

Зонды настраиваются в два этапа через портал hello. Hello первым шагом является проверка toocreate hello. Hello втором шаге добавьте параметров hello пробы toohello серверного http шлюза приложения hello.

1. Войдите в toohello [портал Azure](https://portal.azure.com). Если у вас нет учетной записи, вы можете зарегистрироваться для получения [бесплатной пробной версии на один месяц](https://azure.microsoft.com/free).

1. В hello портал Azure область "Избранное" выберите все ресурсы. Выберите шлюз приложения hello в hello колонке все ресурсы. Если подписка hello уже содержит несколько ресурсов, можно ввести partners.contoso.net в hello фильтр по имени... шлюз приложения hello доступа tooeasily поле.

1. Нажмите кнопку **проверяет** и нажмите кнопку hello **добавить** tooadd кнопку зонда.

  ![Колонка добавления пробы с заполненной информацией][1]

1. На hello **проверки работоспособности добавить** колонки, заполните hello необходимые сведения для проверки hello и по завершении нажмите кнопку **ОК**.

  |**Параметр** | **Значение** | **Дополнительные сведения**|
  |---|---|---|
  |**Имя**|customProbe|Это значение является зонда toohello понятное имя, доступной на портале hello.|
  |**Протокол**|HTTP или HTTPS | использует протокол Hello, hello проверки работоспособности.|
  |**Host**|Например, contoso.com|Это значение является hello имя узла, который используется для проверки hello. Применяется только в случае, когда в шлюзе приложений настроено многосайтовое подключение. В противном случае используется значение 127.0.0.1. Это значение отличается от hello имя узла виртуальной Машины.|
  |**Путь**|/ или другой путь|Hello оставшуюся часть hello полный URL-адрес для проверки пользовательских hello. Путь должен начинаться с /. Путь по умолчанию hello http://contoso.com просто используйте «/» |
  |**Интервал (с)**|30|Как часто hello проверки выполняется toocheck для работоспособности. Не рекомендуется tooset hello меньше 30 секунд.|
  |**Время ожидания (с)**|30|объем Hello hello проверки времени ожидания до истечения времени ожидания. доступен Hello время ожидания интервал потребностей toobe достаточно велико, что вызов http можно сделать tooensure hello внутреннего состояния страницы.|
  |**Пороговое значение сбоя**|3|Число неудачных попыток toobe считаться неработоспособным. Пороговое значение 0 означает, что при сбое проверки работоспособности hello серверной части определяется неработоспособное немедленно.|

  > [!IMPORTANT]
  > Имя узла Hello hello не совпадает с именем сервера. Это значение является именем hello hello виртуального узла на сервере приложения hello. зонд Hello отправляется toohttp: / /(host name):(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>Добавление проверки toohello шлюза

Hello проверки будет создана, представляет время tooadd его toohello шлюза. Параметры выборки, задаются на параметров серверного http hello шлюза приложения hello.

1. Нажмите кнопку **параметры HTTP** шлюзе приложения hello, toobring вверх колонке конфигурации hello щелкните hello текущие серверной части http параметры перечислены в окне приветствия.

  ![Окно параметров HTTPS][2]

1. На hello **appGatewayBackEndHttpSettings** колонку параметров, проверка hello **используйте пользовательский зонд** флажок и выбрать hello пробы, созданные в hello [пробы hello создать](#createprobe) раздела на hello **пользовательский зонд** раскрывающийся список...
По завершении нажмите кнопку **Сохранить** и применяются параметры hello.

проба по умолчанию Hello проверяет hello по умолчанию доступ toohello веб-приложения. После создания пользовательский зонд шлюз приложения hello использует работоспособности toomonitor пользовательский путь, определенный hello для внутренних серверов hello. На основе hello критериев, был определен, шлюз приложения hello проверяет hello пути, указанному в пробы hello. Если hello вызовите toohost:Port / path не возвращает HTTP 200 399 состояние ответа, hello server берется из ротации после hello неработоспособности порога. Проверка продолжается на toodetermine hello неработоспособное экземпляр после его восстановления работоспособности. После добавления пула серверов задней toohealthy экземпляр hello трафик начинает попытку передачи tooit и проверки toohello экземпляр продолжает указанным интервалом пользователя обычным образом.

## <a name="next-steps"></a>Дальнейшие действия

toolearn tooconfigure разгрузки SSL со шлюзом приложения Azure, в статье [Настройка разгрузки SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

