---
title: "Azure AD Connect Health с синхронизацией aaaUsing | Документы Microsoft"
description: "Это страница hello Azure AD Connect Health, обсудим, как синхронизировать toomonitor Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Мониторинг синхронизации Azure AD Connect с помощью Azure AD Connect Health
Следующая документация Hello — конкретных toomonitoring Azure AD Connect (Синхронизация) с Azure AD Connect Health.  Сведения о мониторинге AD FS с помощью Azure AD Connect Health см. в [этой статье](active-directory-aadconnect-health-adfs.md). Кроме того, сведения о мониторинге доменных служб Active Directory с помощью Azure AD Connect Health можно найти [здесь](active-directory-aadconnect-health-adds.md).

![Azure AD Connect Health для синхронизации](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Оповещения Azure AD Connect Health для синхронизации
Hello Azure AD оповещения Connect Health для синхронизации раздела предоставляет hello список активных оповещений. Каждое оповещение включает важные сведения, шаги разрешения и документации toorelated ссылки. После выбора оповещения активных или разрешенных появится новая колонка с дополнительной информацией, а также действия, которые можно выполнить tooresolve hello оповещений и документации tooadditional ссылки. Также можно просмотреть исторические данные об оповещениях, которые были разрешены в прошлом hello.

После выбора оповещения, вам будут предоставлены дополнительные сведения, а также шаги вы сможете предупреждение tooresolve hello и ссылки tooadditional документации.

![Ошибка синхронизации Azure AD Connect](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Ограниченное ознакомление с оповещениями
Если Azure AD Connect не использует конфигурацию по умолчанию hello (например, если фильтрация атрибутов меняется с настраиваемыми tooa конфигурации по умолчанию hello), затем hello Azure AD Connect Health agent, не передают tooAzure связанные события ошибки hello AD Connect.

Это ограничивает hello оценки оповещений службой hello. Может появится заголовка, который определяет это условие в hello портал Azure под вашей службы.

![Azure AD Connect Health для синхронизации](./media/active-directory-aadconnect-health-sync/banner.png)

Это можно изменить, нажав кнопку «Параметры» и позволяя tooupload агента Azure AD Connect Health все журналы ошибок.

![Azure AD Connect Health для синхронизации](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Sync Insight
Администраторы часто требуется tooknow о hello время изменения toosync tooAzure AD и hello объем изменений производится. Эта функция предоставляет простой способ toovisualize это с помощью hello под графиками:   

* задержка операций синхронизации;
* тренд, отображающий изменения объектов.

### <a name="sync-latency"></a>Задержка синхронизации
Эта функция обеспечивает графический тенденций задержки hello операций синхронизации (импорт, экспорт, т. д.) для соединителей.  Это позволяет быстро и легко toounderstand не только hello задержки операций (большего размера, при наличии большого набора изменений, происходящих), но и способ toodetect аномалий в hello задержки, требующих дополнительного изучения.

![Задержка синхронизации](./media/active-directory-aadconnect-health-sync/synclatency02.png)

По умолчанию отображаются только hello задержка для операции «Export» hello hello соединителя Azure AD.  toosee больше операций в соединителе hello или tooview операций из других соединителей, щелкните правой кнопкой мыши на диаграмме hello выберите изменить диаграмму или нажмите кнопку «Изменить диаграмму задержка» hello и выберите определенную операцию hello и соединителей.

### <a name="sync-object-changes"></a>Изменения объектов синхронизации
Эта функция обеспечивает графический тренда hello число изменений, которые вычисляются и экспортировать tooAzure AD.  Сегодня, идет toogather эти сведения из журналов синхронизации hello сложно.  Диаграмма Hello дает, не только более простой способ мониторинга hello число изменений, которые происходят в вашей среде, но визуального представления hello сбоев, которые выполняются.

![Задержка синхронизации](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Отчет об ошибках синхронизации на уровне объектов (предварительная версия)
Этот компонент предоставляет отчет об ошибках синхронизации, которые могут возникать при синхронизации данных удостоверений между Windows Server AD и Azure AD с помощью Azure AD Connect.

* Hello отчет охватывает ошибки с клиентом синхронизации hello (Azure AD Connect версии 1.1.281.0 или более поздней версии)
* Он включает hello ошибки, возникшие в hello последняя операция синхронизации на модуль синхронизации hello. («Экспорт» на hello соединителя Azure AD.)
* Агенту Azure AD Connect Health для синхронизации должен иметь исходящие подключения требуется toohello конечных точек для hello отчетов tooinclude hello последние данные.
* отчет Hello **обновленные через каждые 30 минут** с использованием данных hello загрузить агент Azure AD Connect Health для синхронизации. Он предоставляет следующие основные возможности hello

  * классификация ошибок;
  * Вывод списка объектов с ошибками по категориям
  * Здравствуйте, все данные об ошибках hello в одном месте
  * Рядом с ошибкой из-за конфликта tooa приведено сравнение объектов
  * Загрузить отчет об ошибке hello как CVS, (ожидается в ближайшее время)

### <a name="categorization-of-errors"></a>Классификация ошибок
Hello отчетов категорию hello существующих ошибок синхронизации в hello следующие категории:

| Категория | Description (Описание) |
| --- | --- |
| Повторяющийся атрибут |Ошибки при попытках Azure AD Connect создать или обновить объекты с повторяющимися значениями одного или нескольких атрибутов в Azure AD, которые должны быть уникальными в клиенте, такие как proxyAddresses, UserPrincipalName. |
| Несоответствие данных |Ошибки, когда hello soft-match не toomatch объекты, которые приводят к ошибкам синхронизации. |
| Сбой проверки данных |Ошибки из-за tooinvalid данные, такие как неподдерживаемые символы в важных атрибутов, таких как UserPrincipalName, форматирования ошибок, которые не прошли проверку перед записью в Azure AD. |
| Большой атрибут |Ошибки, когда один или несколько атрибутов крупнее, чем hello допускается длина, размеру или по количеству. |
| Другие |Все остальные ошибки, которые не помещаются в hello выше категорий. На основе отзывов эти категории будут разделены на подкатегории. |

![Сводка по отчету об ошибках синхронизации](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Категории отчета об ошибках синхронизации](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Вывод списка объектов с ошибками по категориям
Углубления в каждой категории предоставит hello список объектов, содержащих ошибки hello в этой категории.
![Список объектов в отчете об ошибках синхронизации](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Сведения об ошибке
Следующие данные доступны в hello подробного представления для каждой ошибки

* Идентификаторы для hello *объекта AD* участвующих
* Идентификаторы для hello *объекта AD Azure* участвующих (если применимо)
* Описание ошибки и как toofix
* Связанные статьи

![Сведения об ошибках в отчете об ошибках синхронизации](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Загрузить отчет об ошибке hello как CSV
Выбрав hello «Export» кнопку, можно загрузить CSV-файл со всеми hello сведениями обо всех ошибках hello.

## <a name="related-links"></a>Связанные ссылки
* [Устранение ошибок синхронизации](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [Синхронизация удостоверений и устойчивость повторяющихся атрибутов](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Установка агента Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Операции Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Использование Azure AD Connect Health с AD FS](active-directory-aadconnect-health-adfs.md)
* [Using Azure AD Connect Health with AD DS (Использование Azure AD Connect Health с AD DS)](active-directory-aadconnect-health-adds.md)
* [Часто задаваемые вопросы об Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health: история версий](active-directory-aadconnect-health-version-history.md)