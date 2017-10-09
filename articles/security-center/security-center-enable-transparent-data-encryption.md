---
title: "Прозрачное шифрование данных в центр безопасности Azure aaaEnable | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить прозрачное данных шифрования **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Включение прозрачного шифрования данных в центре безопасности Azure
Центр безопасности Azure порекомендует включить прозрачное шифрование данных (TDE) для баз данных SQL, если оно еще не включено. Прозрачное шифрование данных защищает данные и помогает соответствие требованиям путем шифрования вашей базы данных, связанных резервных копий и файлов журнала транзакций в rest, не требуя внесения изменений tooyour приложения. более разделе toolearn [прозрачное шифрование данных с базой данных SQL Azure](https://msdn.microsoft.com/library/dn948096).

Данная рекомендация применяется toohello службой Azure SQL. не содержит SQL, работающих на виртуальных машинах.

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания.  Он не является пошаговым руководством.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **рекомендации** колонке выберите **Включение прозрачного шифрования данных**.
   ![Включение прозрачного шифрования данных][1]
2. При этом откроется hello **Включение прозрачного шифрования данных в базах данных SQL** колонку. Выберите tooenable базы данных SQL прозрачного шифрования данных.
   ![Выбор баз данных SQL Server tooenable прозрачное шифрование данных на][2]
3. На hello **прозрачное шифрование данных** колонке выберите **ON** под шифрование данных и выберите **Сохранить** в верхней ленте hello колонка hello.
   ![Включение прозрачного шифрования данных][3]

   После включения прозрачного шифрования данных в hello выбранной базы данных SQL, hello **состояние шифрования** изменится слишком**шифрование**.    

   ![Состояние шифрования][4]

## <a name="see-also"></a>См. также
В этой статье показано, как tooimplement hello рекомендации центра обеспечения безопасности «Включить прозрачное шифрование данных.» toolearn Дополнительные сведения о прозрачном шифровании данных SQL см. ниже hello:

* [Прозрачное шифрование данных в Базе данных SQL Azure](https://msdn.microsoft.com/library/dn948096)
* [Начало работы с прозрачным шифрованием данных (TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
* [Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) --получить последние новости безопасности Azure hello и информацию.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
