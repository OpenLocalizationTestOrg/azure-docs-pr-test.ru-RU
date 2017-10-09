---
title: "Интеграция журнала aaaIntegrating оповещения центра безопасности Azure с помощью Azure | Документы Microsoft"
description: "Эта статья поможет вам приступить к интеграции оповещений центра безопасности Azure с помощью интеграции журналов Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>Интеграция оповещений центра безопасности Azure с помощью интеграции журналов Azure
Многие операции безопасности и группами реагирования на события полагаться на это решение сведения о безопасности и управления событий (SIEM) как hello, начальная точка для рассмотрения и исследование предупреждений системы безопасности. Благодаря интеграции журнала Azure оповещения центра безопасности Azure можно интегрировать в решение SIEM.

Служба интеграции журналов Azure в настоящее время поддерживает HP ArcSight, Splunk и IBM QRadar.

## <a name="what-logs-can-i-integrate"></a>Какие журналы можно интегрировать?
Azure создает подробные журналы для каждой службы. Они подразделяются на следующие категории:

* **Управление/журналы** , предоставляющее видимость hello операций СОЗДАНИЯ диспетчера ресурсов Azure, UPDATE и DELETE. Эти события плоскости управления отображаются в hello журналы действий Azure
* **Журналы плоскости данных** , предоставляющее видимость hello событий, возникающих при использовании ресурс Azure. Например, журнал событий Windows hello, где можно получить сведения о событиях безопасности из канала безопасности в средстве просмотра событий hello. События данных (генерируемые виртуальной машиной или службой Azure) регистрируются в журналах диагностики Azure.

Интеграция журналов Azure в настоящее время поддерживает интеграцию hello:

* журналы виртуальных машин Azure;
* журналы аудита Azure;
* оповещения центра безопасности Azure.

## <a name="install-azure-log-integration"></a>Установка интеграции журналов Azure
Скачайте компонент [интеграции журналов Azure](https://www.microsoft.com/download/details.aspx?id=53324).

Hello служба интеграции журналов Azure собирает данные телеметрии с hello компьютер, на котором он установлен.  Собираются следующие данные телеметрии:

* исключения, возникающие при выполнении интеграции журналов Azure;
* Метрики о количестве hello запросов и обработки событий
* статистические данные использования параметров командной строки Azlog.exe.

> [!NOTE]
> Сбор данных телеметрии можно отключить, сняв этот флажок.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Интеграция оповещений центра безопасности и журналов аудита Azure
1. Привет открыть командную строку и **cd** в **c:\Program Files\Microsoft Azure журнала интеграции**.
2. Запустите hello **azlog createazureid** toocreate команда [субъекта-службы Azure Active Directory](../active-directory/active-directory-application-objects.md) в hello Azure Active Directory (AD) для клиентов, на которых размещены hello подписок Azure.

    Вам будет предложено ввести учетные данные Azure.

   > [!NOTE]
   > Должна быть hello владельца или Соадминистратором подписки hello.
   >
   >

    TooAzure проверка подлинности выполняется с помощью Azure AD.  При создании субъекта-службы для интеграции Azure log создается hello Azure AD identity, заданные tooread доступ из подписки Azure.
3. Запустите hello **авторизовать azlog <SubscriptionID>**  команды tooassign доступ для чтения на hello участника-службы подписки toohello созданный на шаге 2. Если не указать **SubscriptionID**, то hello участника-службы — назначенный hello чтения роли tooall подписки toowhich у вас есть доступ.

   > [!NOTE]
   > Может появиться предупреждения при запуске hello **авторизовать** команду сразу же после hello **createazureid** команды. Возникает некоторая задержка между при создании учетной записи hello Azure AD и когда hello учетной записи доступна для использования. Если подождать около 10 секунд после запуска hello **createazureid** команда hello toorun **авторизовать** команды, то вы не увидите эти предупреждения.
   >
   >
4. Проверьте, что существуют следующие tooconfirm папки, файлы JSON журнала аудита hello hello:

   * **c:\Users\azlog\AzureResourceManagerJson;**
   * **c:\Users\azlog\AzureResourceManagerJsonLD.**
5. Проверьте следующие папки tooconfirm, оповещения центра обеспечения безопасности существуют в их hello.

   * **c:\Users\azlog\AzureSecurityCenterJson;**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD.**
6. Настройте hello SIEM файла сервера пересылки соединитель toohello соответствующую папку. Hello процедуры зависят от hello SIEM, вы используете.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о журналах активности Azure и определения свойств, см.:

* [Операции аудита с помощью диспетчера ресурсов](../azure-resource-manager/resource-group-audit.md)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) — Дополнительные сведения как предупреждения toosecurity toomanage и отправки ответа.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
* [Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) — получить последние новости безопасности Azure hello и информацию.
