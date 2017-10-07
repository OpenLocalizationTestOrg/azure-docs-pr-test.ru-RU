---
title: "aaaApply системных обновлений в центре безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** применения обновлений системы ** и ** перезагрузки после обновления системы **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Применение обновлений системы в центре безопасности Azure
Центр безопасности Azure ежедневно проверяет наличие обновлений операционной системы виртуальных машин Windows и Linux. Центр безопасности получает список доступных критических обновлений и обновлений для системы безопасности из Центра обновления Windows или служб Windows Server Update Services в зависимости от того, какая служба настроена для виртуальной машины Windows.  Центр обеспечения безопасности также проверяет наличие последних обновлений hello в системах Linux. Если на виртуальной машине отсутствует обновление системы, центр безопасности порекомендует его применить.

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания.  Он не является пошаговым руководством.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **рекомендации** колонке выберите **применения обновлений системы**.

   ![Применение обновлений системы][1]
2. Hello **применения обновлений системы** открывается колонка, отображающая список виртуальных машин отсутствуют обновления для системы. Выберите виртуальную машину.

   ![Выбор виртуальной машины][2]
3. Откроется колонка со списком отсутствующих обновлений для этой виртуальной машины. Выберите обновление системы. В этом примере выберем обновление KB3156016.

   ![Отсутствующие обновления безопасности][3]

4. Следуйте указаниям hello hello **обновление системы безопасности** tooapply колонке hello отсутствующие обновления.

   ![Обновление для системы безопасности][4]

## <a name="reboot-after-system-updates"></a>Перезагрузка после завершения обновлений системы
1. Вернуть toohello **рекомендации** колонку. После применения обновлений системы будет создана запись с названием **Перезагрузить после завершения обновлений системы**. Эта запись позволяет узнать необходимые tooreboot hello ВМ toocomplete hello процесс применения обновлений системы.

   ![Перезагрузка после завершения обновлений системы][5]
2. Выберите **Перезагрузить после завершения обновлений системы**. При этом откроется **это ожидание toocomplete системных обновлений** колонки, отображается список виртуальных машин, необходимо toorestart toocomplete hello применить процесс обновления системы.

   ![Ожидание перезагрузки][6]

Перезапустите hello ВМ из Azure toocomplete hello процесса.

## <a name="see-also"></a>См. также
toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
