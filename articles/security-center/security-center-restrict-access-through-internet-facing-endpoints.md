---
title: "aaaRestrict доступ с помощью конечных точек с выходом в Интернет в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** ограничение доступа через конечную точку **, подключенных к Интернету."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>Ограничение доступа через подключенную к Интернету конечную точку в центре безопасности Azure
Центр безопасности Azure будет рекомендовать ограничить доступ через подключенную к Интернету конечную точку, если в какой-либо группе безопасности сети есть одно или несколько правил входящего трафика, разрешающих доступ с "любого" исходного IP-адреса. Открытие доступа слишком «any» могут включить злоумышленники tooaccess ресурсов. Центр безопасности Майкрософт рекомендует изменять эти правила для входящих подключений toorestrict доступа toosource IP-адресов, фактически требуется доступ.

Эта рекомендация создается для любого порта, не являющегося веб-портом, для которого в качестве источника указано значение "Любой".

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания. Он не является пошаговым руководством.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **колонке рекомендации**выберите **ограничить доступ через конечную точку сети Интернет**.

   ![Ограничение доступа через подключенную к Интернету конечную точку][1]
2. Это открывает колонку hello **ограничить доступ через конечную точку сети Интернет**. Эта колонка список hello виртуальных машин (ВМ) с правила для входящих подключений, создать угрозу для безопасности. Выберите виртуальную машину.

   ![Выбор виртуальной машины][2]
3. Hello **NSG** колонке отображаются данные сетевой группы безопасности, связанные правила для входящих подключений, и hello связанных виртуальных Машин. Выберите **изменить правила для входящих подключений** tooproceed с изменением правила входящего подключения.

   ![Колонка "Группа безопасности сети"][3]
4. На hello **безопасности правила для входящих подключений** колонке выберите hello tooedit правило для входящего трафика. В этом примере выберем **AllowWeb**.

   ![Правила безопасности для входящего трафика][4]

   Обратите внимание, что вы также можете выбрать **по умолчанию правила** toosee hello набор правил по умолчанию, содержащиеся в все Nsg. правила по умолчанию Hello нельзя удалить, но, так как они будут назначены более низкий уровень приоритета, они могут быть переопределены созданных вами правил hello. Узнайте больше о [правилах по умолчанию](../virtual-network/virtual-networks-nsg.md#default-rules).

   ![Правила по умолчанию][5]
5. На hello **AllowWeb** колонки, изменение свойств hello hello правило для входящего трафика, который hello **источника** — это IP-адрес или блок IP-адресов. toolearn больше о свойствах hello hello правило для входящего трафика, в разделе [правила NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).

   ![Изменение правила входящего трафика][6]

## <a name="see-also"></a>См. также
В этой статье показано, как tooimplement hello центра обеспечения безопасности, рекомендации «ограничить доступ через конечную точку в Интернете». toolearn Дополнительные сведения о включении Nsg и правилах, см. ниже hello:

* [Группа безопасности сети](../virtual-network/virtual-networks-nsg.md)
* [Как с помощью Nsg toomanage hello портал Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md)— Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md)— узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md)— Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md)--Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md)— часто задаваемые вопросы об использовании hello службы поиска.
* [Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/)--получить последние новости безопасности Azure hello и информацию.

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
