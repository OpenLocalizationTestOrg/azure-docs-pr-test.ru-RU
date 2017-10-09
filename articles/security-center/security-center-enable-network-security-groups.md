---
title: "aaaEnable группами безопасности сети в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить сетевой безопасности групп **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Включение групп безопасности сети в центре безопасности Azure
Центр безопасности Azure порекомендует вам включить группы безопасности сети (NSG), если они еще не включены. Nsg содержит список правил список управления доступом (ACL), которые разрешают или запрещают трафик tooyour экземпляров виртуальных Машин в виртуальной сети. Группы безопасности сети можно связать с подсетями или отдельными экземплярами виртуальных машин в одной из подсетей. Когда NSG связана с подсетью, правила ACL hello применяются tooall экземпляров виртуальных Машин hello в этой подсети. Кроме того, tooan трафик отдельных виртуальных Машин может быть ограничен продолжается связывание NSG непосредственно toothat виртуальной Машины. более разделе toolearn [что такое группа безопасности сети (NSG)?](../virtual-network/virtual-networks-nsg.md)

Если у вас Nsg включен, центр обеспечения безопасности представляется двумя tooyou рекомендации: включить Сетевые группы безопасности в подсети и включить группы безопасности сети на виртуальных машинах. Можно выбрать, какой уровень, подсети или виртуальной Машины, tooapply Nsg.

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания.  Он не является пошаговым руководством.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **рекомендации** колонке выберите **включить группы безопасности сети** подсетей или виртуальных машинах.
   ![Включение групп безопасности сети][1]
2. Это открывает колонку hello **настройки отсутствуют сетевые группы безопасности** для подсетей или виртуальных машин, в зависимости от рекомендаций hello выбранного. Установите в подсети или виртуальной машины tooconfigure NSG.

   ![Настройка группы безопасности сети для подсети][2]

   ![Настройка группы безопасности сети для виртуальной машины][3]
3. На hello **выберите сетевую группу безопасности** колонке выберите существующей NSG или **создать новый** toocreate NSG.

   ![Выбрать группу безопасности сети][4]

При создании NSG, следуйте указаниям hello [как с помощью Nsg toomanage hello портал Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate NSG и набор правил безопасности.

## <a name="see-also"></a>См. также
В этой статье показано, как tooimplement hello центра обеспечения безопасности, рекомендации «включить Сетевые группы безопасности» для подсетей или виртуальных машин. toolearn Дополнительные сведения о включении Nsg, см. ниже hello:

* [Группа безопасности сети](../virtual-network/virtual-networks-nsg.md)
* [Как с помощью Nsg toomanage hello портал Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
* [Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) --получить последние новости безопасности Azure hello и информацию.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
