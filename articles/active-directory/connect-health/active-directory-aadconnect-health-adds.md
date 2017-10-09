---
title: "Azure AD Connect Health в AD DS aaaUsing | Документы Microsoft"
description: "Это страница hello Azure AD Connect Health, будут рассматриваться как toomonitor AD DS."
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Использование Azure AD Connect Health с AD DS
Следующая документация Hello — конкретных toomonitoring доменных служб Active Directory с Azure AD Connect Health. Hello поддерживается версии службы AD DS: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 и Windows Server 2016.

Дополнительные сведения о мониторинге AD FS с помощью Azure AD Connect Health см. в статье [Использование Azure AD Connect Health с AD FS](active-directory-aadconnect-health-adfs.md). Сведения о мониторинге синхронизации Azure AD Connect с помощью Azure AD Connect Health см. в статье [Использование Azure AD Connect Health для синхронизации](active-directory-aadconnect-health-sync.md).

![Azure AD Connect Health для AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>Предупреждения Azure AD Connect Health для AD DS
Hello раздел предупреждений в Azure AD Connect Health для AD DS, предоставляет вам список активных и разрешенных оповещения, контроллеры домена связанные tooyour. После выбора оповещения активных или разрешенных открывается новая колонка с дополнительной информацией, а также действия, а связывает toosupporting документации. Каждый тип сообщения может иметь один или несколько экземпляров, которые соответствуют tooeach hello контроллеров доменов, подвержены каждого из оповещений. Hello нижней части колонки предупреждения hello можно дважды щелкнуть tooopen контроллера домена дополнительных колонка с более подробными сведениями о экземпляр этого предупреждения.

В этой колонке можно включить уведомления по электронной почте для оповещений и изменить диапазон времени hello в представлении. Расширение диапазона времени hello позволяет toosee предыдущего разрешенные предупреждения.

![Ошибка синхронизации Azure AD Connect](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Панель мониторинга контроллеров домена
На этой панели мониторинга отображается топология среды, ключевые рабочие метрики и состояние работоспособности всех отслеживаемых контроллеров домена. Hello представлены метрики для идентификации tooquickly, контроллеры домена, которые могут потребовать дальнейшего изучения. По умолчанию отображается только подмножество столбцов hello. Тем не менее можно найти hello весь набор доступных столбцов, дважды щелкнув команду столбцы hello. Выбор столбцов hello, наиболее важные для вас, включает эту панель мониторинга в единую и легко разместить tooview hello работоспособности среды AD DS.

![Контроллеры домена](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

Контроллеры домена могут быть сгруппированы по каталогу соответствующего домена или сайта, который полезен для понимания топология среды hello. Наконец дважды щелкнув заголовок колонки hello, hello мониторинга повышает tooutilize hello доступных-площадь экрана. Это удобно при отображении большого числа столбцов.

## <a name="replication-status-dashboard"></a>Панель мониторинга состояния репликации
Эта информационная панель предоставляет представление hello репликации состояния и топологию репликации контроллеров домена, отслеживаемых. Hello состояние последней попытки репликации hello указано, вместе с документацией, полезные для любой ошибки, найден. Вы можете дважды контроллера домена с ошибкой tooopen Новая колонка с информацией, такие как: получить сведения об ошибке hello, рекомендуемые шаги разрешения и связывает tootroubleshooting документации.

![Состояние репликации](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>Мониторинг
Эта функция обеспечивает графический тенденции разных счетчиков производительности, которые постоянно собираются из каждого hello отслеживаемых контроллеров домена. Производительность контроллера домена можно легко сравнить с производительностью всех остальных отслеживаемых контроллеров домена в лесу. Кроме того, вы можете просматривать различные счетчики производительности параллельно. Эти данные могут пригодиться при устранении неполадок в среде.

![Мониторинг](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

По умолчанию обновляемые четыре счетчики производительности; Тем не менее можно включить другие, команды фильтр hello и Выбор или Отмена выбора любого требуемых счетчиков производительности. Кроме того можно дважды щелкнуть tooopen диаграммы счетчика производительности Новая колонка, который включает точки данных для каждого hello отслеживаемых контроллеров домена.

## <a name="related-links"></a>Связанные ссылки
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Установка агента Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Операции Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Использование Azure AD Connect Health с AD FS](active-directory-aadconnect-health-adfs.md)
* [Использование Azure AD Connect Health для синхронизации](active-directory-aadconnect-health-sync.md)
* [Часто задаваемые вопросы об Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health: история версий](active-directory-aadconnect-health-version-history.md)

