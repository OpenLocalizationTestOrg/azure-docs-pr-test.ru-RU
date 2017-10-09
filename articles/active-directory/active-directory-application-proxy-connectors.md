---
title: "aaaClassic портала соединителей прокси приложения Azure AD | Документы Microsoft"
description: "Рассматриваются как toocreate группы соединителей прокси приложения Azure AD и управлять ими."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Публикация приложений в отдельных сетях и расположениях с помощью групп соединителей
> [!div class="op_single_selector"]
> * [Портал Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [Классический портал Azure](active-directory-application-proxy-connectors.md)
>
>

Группы соединителей удобно использовать в нескольких сценариях, включая следующие:

* Сайты с несколькими взаимосвязанными центрами обработки данных. В этом случае требуется tookeep объем трафика в центре обработки данных hello максимально из-за ссылок между центрами дорогостоящий и медленно. Вы можете развернуть соединителей в каждый центр обработки данных tooserve только hello приложения, находящиеся в центре обработки данных hello. Такой подход сводит к минимуму ссылки между центрами и предоставляет возможность полностью прозрачны tooyour пользователей.
* Управление приложений, установленных в изолированных сетях, которые не являются частью hello главной корпоративной сети. Можно использовать соединители tooinstall выделенной группы соединителя в изолированных сетях tooalso изоляции приложений toohello сети.
* Для приложений, установленных на IaaS для доступа к облаку соединитель группы предоставляют общие службы toosecure hello доступа tooall hello приложений. Группы соединителей не создать дополнительную зависимость в корпоративной сети или фрагмент интерфейса приложения hello. Соединители можно установить в каждом облачном центре обработки данных для обслуживания только тех приложений, которые размещены в этой сети. Можно установить несколько соединителей tooachieve высокого уровня доступности.
* Поддержка сред с несколькими лесами в которых можно развернуть на один лес и задать конкретные приложения tooserve определенные соединители.
* Группы соединителей может использоваться на сайтах аварийного восстановления tooeither обнаружение отработки отказа, или как резервное копирование для hello основного сайта.
* Группы соединителей может также быть tooserve используется несколько компаний от одного клиента.

## <a name="prerequisite-create-your-connectors"></a>Необходимое условие: создание соединителей
toogroup соединителях, [установить несколько соединителей](active-directory-application-proxy-enable.md), введите название и сгруппировать их. Наконец, что у вас есть tooassign их toospecific приложений.

## <a name="step-1-create-connector-groups"></a>Шаг 1. Создание групп соединителей
Можно создать любое число групп соединителей. Создание группы для соединителя выполняется в hello классический портал Azure.

1. Выберите свой каталог и щелкните **Настройка**.  
    ![Снимок экрана: настройка прокси приложения: выбор "Управление группами соединителей"](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. В разделе прокси приложения, нажмите кнопку **Управление группами соединитель** и создайте группу соединитель путем предоставления имени группы hello.  
    ![Снимок экрана групп соединителей прокси приложения: присвоение имени для новой группы](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>Шаг 2: Назначение соединители группы tooyour
После создания группы соединителей hello переместите hello соединители toohello соответствующую группу.

1. В разделе **Прокси приложения** нажмите кнопку **Управление соединителями**.
2. В разделе **группы**, выберите группу hello, необходимо для каждого соединителя. Соединители hello вверх toobecome too10 минут может занять активен в новую группу hello.  
    ![Снимок экрана соединителей прокси приложения: выбор группы из раскрывающегося меню](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>Шаг 3: Назначение приложений tooyour группы соединителей
Последний шаг Hello является tooset каждой toohello соединителя из групп приложений, выполняющий его.

1. В hello классический портал Azure, в вашем каталоге, выберите hello приложения tooassign toohello группы и нажмите кнопку **Настройка**.
2. В разделе **группы соединителей**выберите hello группу hello toouse приложения. Это изменение применяется немедленно.  
    ![Снимок экрана группы соединителей прокси приложения: выбор группы из раскрывающегося меню](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>Дополнительные материалы
* [Включение прокси приложения](active-directory-application-proxy-enable.md)
* [Включение единого входа](active-directory-application-proxy-sso-using-kcd.md)
* [Включение условного доступа](active-directory-application-proxy-conditional-access.md)
* [Устранение неполадок с прокси приложения](active-directory-application-proxy-troubleshoot.md)

Для получения hello последние новости и обновления, посетите hello [блога прокси приложения](http://blogs.technet.com/b/applicationproxyblog/)
