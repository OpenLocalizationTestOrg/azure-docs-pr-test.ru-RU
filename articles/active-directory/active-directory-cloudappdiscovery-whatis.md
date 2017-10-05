---
title: "Поиск неуправляемых облачных приложений с помощью Cloud App Discovery | Документация Майкрософт"
description: "Содержит сведения о поиске приложений и управлении ими с помощью Cloud App Discovery, а также преимуществах и принципах работы Cloud App Discovery."
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
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Поиск неуправляемых облачных приложений с помощью Cloud App Discovery
## <a name="overview"></a>Обзор
На современных предприятиях ИТ-специалисты часто не знают обо всех облачных приложениях, при помощи которых пользователи выполняют свои задачи. Легко понять, почему администраторов беспокоят несанкционированный доступ к корпоративным данным, возможная утечка данных и другие угрозы безопасности. Эта недостаточная осведомленность может сильно усложнить разработку плана по борьбе с этими угрозами безопасности.

Cloud App Discovery — это функция службы Azure Active Directory (AD) уровня Премиум, которая позволяет обнаруживать облачные приложения, используемые сотрудниками организации.

**С помощью Cloud App Discovery вы сможете:**

* Обнаруживать используемые облачные приложения и оценивать их использование по числу пользователей, объему трафика или числу веб-запросов к приложению.
* Идентифицировать пользователей, использующих приложение.
* Экспортировать данные для автономного анализа.
* Получить контроль над этими приложениями с помощью средств ИТ и включить доступ с единым входом для управления пользователями.

## <a name="how-it-works"></a>Принцип работы
1. На компьютерах пользователей устанавливаются агенты использования приложения.
2. Информация об использовании приложения, записанная агентами, отправляется по безопасному зашифрованному каналу в службу Cloud App Discovery.
3. Служба Cloud App Discovery оценивает данные и создает отчеты.

![Схема Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

Дополнительную информацию о работе Cloud App Discovery см. в статье [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx) (Начало работы с Cloud App Discovery).

## <a name="related-articles"></a>Связанные статьи
* [Вопросы безопасности и конфиденциальности Cloud App Discovery](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Руководство по развертыванию групповой политики Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Руководство по развертыванию центра Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Параметры реестра для настройки Cloud App Discovery для прокси-серверов с пользовательскими портами](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Журнал изменений агента Cloud App Discovery ](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Часто задаваемые вопросы по Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)

