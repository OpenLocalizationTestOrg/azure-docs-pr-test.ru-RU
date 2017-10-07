---
title: "aaaAdd следующего поколения брандмауэра в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** добавьте следующего поколения брандмауэра ** и ** маршрута анализировать трафик через NGFW только **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a>Добавление брандмауэра следующего поколения в центре безопасности Azure
Центр безопасности Azure может рекомендуем добавить брандмауэром следующего поколения (NGFW) от партнера Майкрософт tooincrease мер по обеспечению безопасности. В этом документе описан процесс пример toodo это.

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания.  Он не является пошаговым руководством.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **рекомендации** колонке выберите **Добавление следующего поколения брандмауэр**.
   ![Добавить брандмауэр следующего поколения][1]
2. В hello **Добавление следующего поколения брандмауэр** колонке выберите конечную точку.
   ![Выбор конечной точки][2]
3. Откроется вторая колонка **Добавить брандмауэр следующего поколения** . Вы можете toouse существующее решение при наличии или можно создать новую. В этом примере нет доступных решений, поэтому мы создадим NGFW.
   ![Создание брандмауэра следующего поколения][3]
4. toocreate NGFW выберите решение из списка hello интеграции партнеров. В нашем примере мы выберем **Check Point**.
   ![Выбор решения брандмауэра следующего поколения][4]
5. Hello **Check Point** открывает колонку обеспечивает сведения о решении hello партнера. Выберите **создать** в колонке сведения hello.
   ![Колонка со сведениями о брандмауэре][5]
6. Hello **создать виртуальную машину** открывает колонку. Здесь можно ввести сведения, необходимые toospin виртуальную машину (VM) под управлением hello NGFW. Выполните действия hello и укажите необходимые сведения NGFW hello. Выберите ОК tooapply.
   ![Создание виртуальной машины toorun NGFW][6]

## <a name="route-traffic-through-ngfw-only"></a>Маршрутизация трафика только через NGFW
Вернуть toohello **рекомендации** колонку. Когда вы добавите добавления NGFW с помощью центра безопасности, будет создана запись **Маршрутизировать трафик только через NGFW**. Эта рекомендация создается только в том случае, если вы установили NGFW с помощью центра безопасности. При наличии конечных точек с выходом в Интернет, центр обеспечения безопасности рекомендует настраивать правил сетевой группы безопасности, принудительно tooyour входящий трафик ВМ с помощью вашей NGFW.

1. В hello **колонке рекомендации**выберите **направить трафик только через NGFW**.
   ![Route traffic through NGFW only (Маршрутизировать трафик только через NGFW)][7]
2. Это открывает колонку hello **направить трафик только через NGFW**, в котором перечислены виртуальные машины, которые может направлять трафик. Выберите виртуальную Машину из списка hello.
   ![Выбор виртуальной машины][8]
3. Стоечный модуль для hello выбрать ВМ откроется связанные правила для входящих подключений. Отображенное описание будет содержать дополнительные сведения о возможных дальнейших действиях. Выберите **изменить правила для входящих подключений** tooproceed с изменением правила входящего подключения. Hello ожидается, что **источника** не задано слишком**любой** для конечных точек с выходом в Интернет hello связанных с hello NGFW. toolearn больше о свойствах hello hello правило для входящего трафика, в разделе [правила NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).
   ![Настройка правил доступа toolimit][9]
   ![изменить правила для входящего трафика][10]

## <a name="see-also"></a>См. также
В этом документе вы узнали, как tooimplement hello рекомендации центра обеспечения безопасности «Добавить следующего поколения брандмауэр». toolearn Дополнительные сведения о NGFWs и hello решение партнера Check Point, см. ниже hello:

* [Next-Generation Firewall](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [Check Point vSEC](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
