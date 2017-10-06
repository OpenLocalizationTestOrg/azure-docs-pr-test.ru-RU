---
title: "aaaResolve оповещений о работоспособности endpoint protection в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** разрешить Endpoint Protection работоспособности оповещения **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Разрешение оповещений о работоспособности Endpoint Protection в центре безопасности Azure
Центр безопасности Azure будет рекомендовать разрешить выявленные оповещения о работоспособности Endpoint Protection.  Центр обеспечения безопасности позволяет toosee виртуальных машин (ВМ) имеют сбоям защиты конечной точки и сколько.

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания. Он не является пошаговым руководством.
> 
> 

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **колонке рекомендации**выберите **оповещения о работоспособности Endpoint Protection Разрешить**.
   ![Разрешение оповещений о работоспособности Endpoint Protection][1]
2. Это открывает колонку hello **сбоя Endpoint Protection** в котором перечислены виртуальные машины с ошибками и hello количество отказов для каждой виртуальной Машины. Выберите виртуальную Машину из списка hello.
   ![Endpoint protection failure][2]
3. Объект **список сбоев** открывает колонку для hello выбранных виртуальных Машин, отображается список ошибок. Выберите дополнительные toolearn список hello сбоя. Откроется панель с информацией о сбое hello выбран.
   ![Список сбоев][3]
   ![Событие сбоя][4]

## <a name="see-also"></a>См. также
toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md)— Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md)— узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md)— Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md)--Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md)— часто задаваемые вопросы об использовании hello службы поиска.
* [Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/)--получить последние новости безопасности Azure hello и информацию.

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
