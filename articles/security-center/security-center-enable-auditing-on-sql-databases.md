---
title: "aaaEnable аудита и угрозы обнаружения на SQL базы данных в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить обнаружение аудита и угроз для базы данных SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a>Включение аудита и обнаружения угроз для баз данных SQL в центре безопасности Azure
Центр безопасности Azure порекомендует включить аудит и обнаружение угроз для всех баз данных SQL, если эти функции еще не включены. Аудит и обнаружение угроз могут помочь вам соблюсти стандарты, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на бизнес-проблемы или предполагаемые нарушения безопасности.

После включения аудита можно настроить для обнаружения угроз параметры и сообщения электронной почты tooreceive оповещений системы безопасности. Обнаружение угроз обнаруживает аномальные действия базы данных, указывающее базу данных toohello потенциальные угрозы безопасности. Это позволяет toodetect и отвечать toopotential угроз, как только они происходят.

Данная рекомендация применяется toohello службой Azure SQL. они не включают SQL, работающих на виртуальных машинах.

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания.  Он не является пошаговым руководством.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **рекомендации** колонке выберите **включить аудит & угроз обнаружения на базах данных SQL**.  При этом откроется hello **включить аудит & угроз обнаружения на базах данных SQL** колонку.

   ![Включение аудита для баз данных SQL][1]
2. Выберите аудита базы данных SQL tooenable на. При этом откроется hello **аудита и обнаружения угроз** колонку.

3. На hello **аудита и обнаружения угроз** колонке выберите **ON** под **аудита**.

   ![Включение аудита и обнаружения угроз][2]
4. Следуйте указаниям hello [обнаружением угроз для базы данных SQL в hello портал Azure](../sql-database/sql-database-threat-detection-portal.md) tooturn на и настроить обнаружение угроз и tooconfigure hello список адресов электронной почты, которые будут получать предупреждения системы безопасности при обнаружении аномальных действий.

## <a name="see-also"></a>См. также
В этой статье показано, как tooimplement hello центра обеспечения безопасности, рекомендации «Включение аудита и угрозы обнаружения на базах данных SQL.» toolearn Дополнительные сведения о защите базы данных SQL, см. ниже hello:

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
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
