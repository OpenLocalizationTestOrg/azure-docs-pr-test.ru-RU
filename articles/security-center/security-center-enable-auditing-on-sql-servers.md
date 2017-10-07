---
title: "aaaEnable аудита и угрозы обнаружения на SQL Server в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить аудит & угроз обнаружения на серверах SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a>Включение аудита и обнаружения угроз для серверов SQL в центре безопасности Azure
Центр безопасности Azure порекомендует включить аудит и обнаружение угроз для всех баз данных на всех серверах SQL Azure, если аудит еще не включен. Аудит и обнаружение угроз могут помочь вам соблюсти стандарты, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на бизнес-проблемы или предполагаемые нарушения безопасности.

После включения аудита можно настроить для обнаружения угроз параметры и сообщения электронной почты tooreceive оповещений системы безопасности. Обнаружение угроз обнаруживает аномальные действия базы данных, указывающее базу данных toohello потенциальные угрозы безопасности. Это позволяет toodetect и отвечать toopotential угроз, как только они происходят.

Данная рекомендация применяется toohello службой Azure SQL. она не включает SQL Server, работающий на виртуальных машинах в службах инфраструктуры Azure (Azure IaaS).

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания.  Он не является пошаговым руководством.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **рекомендации** колонке выберите **включить аудит & угроз обнаружения на серверах SQL Server**.  При этом откроется hello **включить аудит & угроз обнаружения на серверах SQL Server** колонку.

   ![Включение аудита для серверов SQL][1]
2. Установите SQL server tooenable аудита и угрозы обнаружения. При этом откроется hello **аудита и обнаружения угроз** колонку.

3. На hello **аудита и обнаружения угроз** колонке выберите **ON** под **аудита**.

   ![Включение параметров аудита][2]
4. Следуйте указаниям hello [аудита базы данных SQL в hello портал Azure](../sql-database/sql-database-auditing-portal.md) tooconfigure хранилище, где будет храниться журналов аудита. Hello подписки в учетной записи хранилища для сбора данных — учетная запись хранения по умолчанию hello.
5. Следуйте указаниям hello [Приступая к работе с обнаружением угроз для базы данных SQL](../sql-database/sql-database-threat-detection.md) tooturn на и настроить обнаружение угроз и tooconfigure hello список адресов электронной почты, которые будут получать предупреждения системы безопасности при обнаружении аномальных действий.

## <a name="see-also"></a>См. также
В этой статье показано, как tooimplement hello рекомендации центра обеспечения безопасности «Включение аудита и угрозы обнаружения на серверах SQL Server». toolearn Дополнительные сведения о защите базы данных SQL, см. ниже hello:

* [Защита Базы данных SQL](../sql-database/sql-database-security-overview.md)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
* [Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) --получить последние новости безопасности Azure hello и информацию.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
