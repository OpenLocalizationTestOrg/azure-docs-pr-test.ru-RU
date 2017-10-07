---
title: "aaaAzure журнала интеграция с центром обеспечения безопасности | Документы Microsoft"
description: "Узнайте, как tooget безопасности Azure center оповещения, работа с интеграцией журнала"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>Как tooget ваш центр безопасности оповещения в Azure log интеграции
Эта статья содержит hello действия требуется tooenable hello службы интеграции Azure журнала toopull предупреждение безопасности информации, создаваемой центра безопасности Azure. Необходимо успешно выполнить шаги hello hello [начать](security-azure-log-integration-get-started.md) статьи, прежде чем выполнять действия hello в этой статье.

## <a name="detailed-steps"></a>Подробные инструкции
Hello следующее создаст hello необходимые субъекта-службы Azure Active Directory и назначьте hello участника службы подписки toohello разрешения на чтение:
1. Откройте командную строку hello и перехода слишком**c:\Program Files\Microsoft Azure журнала интеграции**
2. Выполните команду hello``azlog createazureid``

    Эта команда запрашивает имя для входа Azure. Затем создается команда Hello [субъекта-службы Azure Active Directory](../active-directory/develop/active-directory-application-objects.md) в hello клиенты Azure AD, содержащие hello подписок Azure, в какие hello, пользователь является администратором, администратором или владельцем. Команда Hello завершится ошибкой, если пользователь hello равно только существование пользователя Guest в hello клиента Azure AD. Проверка подлинности tooAzure выполняется через Azure Active Directory (AD). При создании субъекта-службы для интеграции Azlog создается hello удостоверений Azure AD, предоставляемую tooread доступ из подписки Azure.

2. Теперь вы выполните команду, которая назначает доступ для чтения на hello участника-службы подписки toohello созданный на шаге 2. Если не указать идентификатор подписки, команда hello попытается tooassign hello службы чтения основной роли tooall подписки toowhich имеют доступ. </br></br>
``azlog authorize <SubscriptionID>`` </br> Например: </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Может появиться предупреждения при запуске hello авторизовать команда сразу же после команды createazureid hello. Возникает некоторая задержка между при создании учетной записи hello Azure AD и когда hello учетной записи доступна для использования. Если Подождите около 60 секунд после выполнения команды toorun hello createazureid hello авторизовать команды, то вы не увидите эти предупреждения.

4. Проверьте, что существуют следующие tooconfirm папки, файлы JSON журнала аудита hello hello:
 * **c:\Users\azlog\AzureResourceManagerJson;**
 * **c:\Users\azlog\AzureResourceManagerJsonLD.** </br></br>
5. Проверьте следующие папки tooconfirm, оповещения центра обеспечения безопасности существуют в их hello.</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD.** </br></br>

Если возникли проблемы во время установки hello и конфигурации, откройте [запрос на получение поддержки](/azure-supportability/how-to-create-azure-support-request.md)выберите **интеграции журнала** как служба hello, для которого запрашивается поддержка.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о журнале интеграции Azure, см. следующие документы hello.

* [Служба интеграции журналов Microsoft Azure для журналов Azure](https://www.microsoft.com/download/details.aspx?id=53324) — посетите Центр загрузки, чтобы получить дополнительные сведения, изучить требования к системе и получить инструкции по установке службы интеграции журналов Azure.
* [Введение tooAzure журнала интеграции](security-azure-log-integration-overview.md) — в этом документе представлены интеграцию tooAzure журнала, его основные возможности и как он работает.
* [Действия по настройке партнера](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) — в этой записи блога показано, как tooconfigure Azure журнала toowork интеграция с решениями партнеров Splunk и разработанное HP, IBM QRadar.
* [Azure log integration frequently asked questions (FAQ)](security-azure-log-integration-faq.md) (Служба интеграции журналов Azure: часто задаваемые вопросы) — эта статья содержит ответы на часто задаваемые вопросы об интеграции журналов Azure.
* [Интеграция центра обеспечения безопасности интеграции журнала предупреждений с помощью Azure](../security-center/security-center-integrating-alerts-with-log-integration.md) — в этом документе показано, как оповещения центра обеспечения безопасности toosync, вместе с событиями безопасности виртуальной машины, собранные диагностики Azure и журналы аудита Azure, с помощью аналитики журналов или Решения SIEM.
* [Новые возможности диагностики Azure и журналы аудита Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) — в этой записи блога вводит tooAzure журналы аудита и другие средства, помогающие анализировать hello операций с ресурсами Azure.
