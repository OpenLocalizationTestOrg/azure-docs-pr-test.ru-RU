---
title: "aaaInstall Endpoint Protection в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** установить Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Установка Endpoint Protection в центре безопасности Azure
Центр безопасности Azure рекомендует установить решение для защиты конечных точек на виртуальных машинах Azure, если оно еще не включено. Данная рекомендация применяется tooWindows только для виртуальных машин.

> [!NOTE]
> В этом примере развертывания используется антивредоносное ПО Майкрософт. Список партнеров, решения которых интегрированы с центром безопасности, см. в статье [Интеграция партнеров в центре безопасности Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center).  
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания.  Этот документ не является пошаговым руководством.
>
>

1. В hello **рекомендации** колонке выберите **установить Endpoint Protection**.
   ![Выберите "Установить Endpoint Protection"][1]
2. Hello **установить Endpoint Protection** открывается колонка, отображающая список виртуальных машин без защиты конечной точки. Выберите из списка hello hello виртуальных машин, которые требуются tooinstall endpoint protection и нажмите кнопку **установить на виртуальных машинах**.
   ![Выберите виртуальные машины tooinstall Endpoint Protection на][2]
3. Hello **выберите Endpoint Protection** tooallow открывает колонку вы tooselect hello endpoint protection решения, нужно toouse. В этом примере мы выберем **Антивредоносное ПО Майкрософт**.
   ![Select Endpoint Protection][3]
4. Дополнительные сведения о hello решение для защиты конечной точки отображаются. Нажмите кнопку **Создать**.
   ![Создание решения для защиты от вредоносных программ][4]
5. Введите hello необходимые параметры конфигурации на hello **расширения Add** колонки, а затем выберите **ОК**. в разделе toolearn Дополнительные сведения о параметрах конфигурации hello, [по умолчанию и защиты от вредоносных программ Настраиваемая конфигурация](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[Microsoft Antimalware](../security/azure-security-antimalware.md) теперь активно hello выбранные виртуальные машины.

## <a name="see-also"></a>См. также
В этой статье показано, как tooimplement hello рекомендации центра обеспечения безопасности «Установить Endpoint Protection». toolearn Дополнительные сведения о включении защиты от вредоносных программ Майкрософт в Azure, см. следующий документ hello.

* [Microsoft Antimalware для облачных служб и виртуальных машин](../security/azure-security-antimalware.md) — Узнайте, как toodeploy Майкрософт защиты от вредоносных программ.

toolearn Дополнительные сведения о центра обеспечения безопасности, см. следующие документы hello.

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
