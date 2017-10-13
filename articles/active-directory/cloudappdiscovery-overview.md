---
title: "Усовершенствования Cloud App Discovery в Azure Active Directory | Документы Майкрософт"
description: "Содержит сведения о поиске приложений и управлении ими с помощью Cloud App Discovery, а также преимуществах и принципах работы Cloud App Discovery."
services: active-directory
keywords: "cloud app discovery, управление приложениями"
documentationcenter: 
author: curtand
manager: femila
tags: ignite
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2017
ms.author: curtand
ms.reviewer: nigu
ms.openlocfilehash: 59af2a5de5936d15456058aaeacfc334b9b34d4c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="cloud-app-discovery-enhancements-in-azure-active-directory"></a>Усовершенствования Cloud App Discovery в Azure Active Directory 
Более 80 % сотрудников признают, что используют неутвержденные приложения SaaS в рабочих целях. Сейчас мы интегрируем Cloud App Discovery в Azure AD вместе с данными и аналитическими функциями Microsoft Cloud App Security, чтобы вам было проще определить больше неуправляемых облачных приложений. Действия по настройке этой новой интеграции отличаются от требовавшихся ранее.

## <a name="what-can-i-do-now-with-the-improvements-to-cloud-app-discovery-in-azure-ad"></a>Что дают вам эти усовершенствования Cloud App Discovery в Azure AD?

* **Более четкое представление об использовании облачных приложений** — Cloud App Discovery в Azure AD теперь обнаруживает **более 15 000 приложений** во всем сетевом трафике организации и с любого устройства. 
* **Агенты не нужны** — для новой версии Cloud App Discovery не требуется устанавливать агенты на устройства пользователей. Вместо этого обнаружение выполняется на основе файлов журнала, импортируемых из брандмауэров и с прокси-серверов. Вы можете обнаруживать приложения во всем сетевом трафике организации, независимо от операционной системы или устройства.
* **Оперативный анализ и оповещения** — теперь Cloud App Discovery в Azure AD предоставляет подробный оперативный анализ рисков и оповещения об использовании нового приложения. Вы можете более детально изучить использование облачных приложений в вашей организации, например, получить сведения о входящем трафике, исходящем трафике и ключевых пользователях для обнаруженных приложений.

При отсутствии подписки Active Directory Premium см. статью [Цены на Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

Используйте эту ссылку для ознакомления с [новым интерфейсом Cloud App Discovery в Azure AD](https://portal.cloudappsecurity.com).

## <a name="next-steps"></a>Дальнейшие действия
Используйте следующие ссылки для настройки Cloud App Discovery в Azure AD.

* [Приступая к работе с Cloud App Discovery в Azure AD](cloudappdiscovery-get-started.md)
* [Создание отчетов о моментальных снимках](cloudappdiscovery-set-up-snapshots.md)
* [Настройка непрерывного создания отчетов](https://docs.microsoft.com/cloud-app-security/discovery-docker)
* [Использование настраиваемого средства синтаксического анализа журналов](https://docs.microsoft.comcommit/cloud-app-security/custom-log-parser)