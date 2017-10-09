---
title: "aaaAzure журнала интеграция с журналы аудита Azure Active Directory | Документы Microsoft"
description: "Узнайте, как tooinstall hello службы интеграции журналов Azure и интегрировать журналы из журналов аудита Azure"
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
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Интеграция журналов аудита Azure Active Directory

События аудита Azure Active Directory (Azure AD) помогают определить привилегированные действия, выполняемые в Azure Active Directory. Можно просматривать hello типы событий, которые можно отследить, просмотрев [события отчетов аудита Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Прежде чем hello действия, описанные в этой статье, необходимо просмотреть hello [начать](security-azure-log-integration-get-started.md) статью и завершить там шаги hello.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>Журналы аудита Azure Active directory toointegrate действия

1. Откройте командную строку hello и выполните следующую команду:

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Выполните следующую команду: 
 
   ``azlog createazureid``

   Эта команда запрашивает имя для входа Azure. Hello команда создает Azure Active Directory участника-службы в клиентов hello Azure AD, на которых размещены hello в какой hello вошедшего в систему пользователя — администратора, соадминистратора или владелец подписок Azure. Hello команда завершится ошибкой, если hello вошедшего в систему пользователя только пользователя guest в клиенте Azure AD hello. TooAzure проверка подлинности выполняется с помощью Azure AD. При создании субъекта-службы для интеграции Azure журнала создается hello удостоверений Azure AD, которому дано tooread доступ из подписки Azure.

3. Запустите следующие команды tooprovide hello свой идентификатор клиента. Требуется член toobe hello клиента администратора роли toorun hello команды.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Пример:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Убедитесь, что в них создаются следующие папки tooconfirm, hello файлы JSON журналов аудита Azure Active Directory hello:

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Hello следующем видеоролике показано hello шаги, описанные в данной статье:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> За инструкциями по приведению hello сведения в файлах JSON hello в сведения о безопасности и системных событий управления (SIEM) обратитесь к поставщику SIEM.

Помощь сообщества доступна через hello [форум MSDN интеграции Azure журнала](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Этот форум позволяет пользователям в toosupport сообщества интеграции Azure журнала hello, друг с другом в вопросы, ответы, советы и рекомендации. Кроме того команды hello интеграции журналов Azure отслеживает этот форум и помогает всякий раз, когда это возможно.

Можно также отправить [запрос в службу поддержки](../azure-supportability/how-to-create-azure-support-request.md). Выберите **интеграции журнала** как служба hello, для которого запрашивается поддержка.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о журнале интеграции Azure, см.:

* [Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) (Служба интеграции журналов Microsoft Azure). На этой странице Центра загрузки можно получить дополнительные сведения, изучить требования к системе и получить инструкции по установке службы интеграции журналов Azure.
* [Введение tooAzure интеграции журнала](security-azure-log-integration-overview.md): в этой статье описаны tooAzure интеграции журнала, его основные возможности и как он работает.
* [Действия по настройке партнера](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): в этой записи блога показано, как решения Splunk, разработанное HP и IBM QRadar партнеров tooconfigure toowork интеграции Azure журнала с.
* [Интеграция журналов Azure: часто задаваемые вопросы](security-azure-log-integration-faq.md). В этой статье содержатся ответы на часто задаваемые вопросы об интеграции журналов Azure.
* [Интеграция с интеграцией журнала Azure оповещения центра обеспечения безопасности](../security-center/security-center-integrating-alerts-with-log-integration.md): в этой статье показано, как оповещения центра обеспечения безопасности toosync, вместе с собранными диагностики Azure и журналы аудита Azure, с помощью вашей аналитики журналов событий безопасности виртуальной машины или Решения SIEM.
* [Новые возможности диагностики Azure и Azure журналы аудита](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): в этой записи блога представлены tooAzure журналы аудита, а также другие средства, помогающие анализировать hello операций с ресурсами Azure.
