---
title: "aaaFinding неуправляемого облачных приложений с Cloud App Discovery | Документы Microsoft"
description: "Сведения о поиске и управление приложениями с помощью Cloud App Discovery, Каковы преимущества hello и как он работает."
services: active-directory
keywords: "cloud app discovery, управление приложениями"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Поиск неуправляемых облачных приложений с помощью Cloud App Discovery
## <a name="overview"></a>Обзор
На современных предприятиях ИТ-отделы, часто не знают все hello облачных приложений, что члены организации используют toodo свою работу. Это легко toosee, почему Администраторы бы обеспокоены toocorporate несанкционированного доступа к данным, возможными утечками данных и других угроз безопасности. Эта недостаточная осведомленность может сильно усложнить разработку плана по борьбе с этими угрозами безопасности.

Cloud App Discovery — это функция Azure Active Directory (AD) Premium, благодаря которой вы toodiscover облачных приложений, используемых hello сотрудниками вашей организации.

**С помощью Cloud App Discovery вы сможете:**

* Найдите hello облачные приложения используются и мера такого использования, по количеству пользователей, объему трафика или количество toohello запросов веб-приложения.
* Определите hello пользователей, использующих приложения.
* Экспортировать данные для автономного анализа.
* Получить контроль над этими приложениями с помощью средств ИТ и включить доступ с единым входом для управления пользователями.

## <a name="how-it-works"></a>Принцип работы
1. На компьютерах пользователей устанавливаются агенты использования приложения.
2. сведения об использовании приложения Hello, записанные агентами hello передаются через служба безопасный, зашифрованный канал toohello cloud app discovery.
3. Hello службы Cloud App Discovery оценивает данные hello и создает отчеты.

![Схема Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

tooget работы с Cloud App Discovery см [Приступая к работе с Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>Связанные статьи
* [Вопросы безопасности и конфиденциальности Cloud App Discovery](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Руководство по развертыванию групповой политики Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Руководство по развертыванию центра Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Параметры реестра для настройки Cloud App Discovery для прокси-серверов с пользовательскими портами](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Журнал изменений агента Cloud App Discovery ](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Часто задаваемые вопросы по Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)

