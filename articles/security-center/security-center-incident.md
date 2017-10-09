---
title: "предупреждения безопасности aaaHandling в центр безопасности Azure | Документы Microsoft"
description: "Этот документ поможет вам toouse центра безопасности Azure возможности toohandle безопасности инцидентов."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>Обработка инцидентов в центре безопасности Azure
Рассмотрения и исследование предупреждений безопасности может занять много времени для hello даже более опытным аналитикам в области безопасности, а также для многих это жестких tooeven знать, где toobegin. С помощью [analytics](security-center-detection-capabilities.md) tooconnect hello информации между различных [оповещений системы безопасности](security-center-managing-and-responding-alerts.md), центр обеспечения безопасности может предоставить одно представление кампании атаки и все hello связанные предупреждения — вы можете быстро понять, какие действия hello злоумышленник заняло, какие ресурсы были затронуты.

В этом документе рассматриваются как toouse безопасности предупреждают в центр обеспечения безопасности tooassist возможность обработки инцидентов безопасности.

## <a name="what-is-a-security-incident"></a>Что такое инцидент?
В центре безопасности инцидентом считается совокупность всех оповещений для ресурса, которые соответствуют схемам [этапов нарушения безопасности](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) . Инциденты отображаются в hello [оповещений системы безопасности](security-center-managing-and-responding-alerts.md) плитки и колонки. Инцидент будет открывать связанные предупреждения список hello, который позволяет вам tooobtain дополнительную информацию о каждое вхождение.

## <a name="managing-security-incidents"></a>Управление инцидентами
Можно просмотреть события безопасности в вашей текущей, просмотрев плитку предупреждения безопасности hello. Доступ к hello портала Azure и выполните действия hello ниже toosee подробной информации о каждом угрозы безопасности.

1. На панели мониторинга hello центра обеспечения безопасности, вы увидите hello **оповещений системы безопасности** плитки.

    ![Плитка "Оповещения системы безопасности" в центре безопасности](./media/security-center-incident/security-center-incident-fig1.png)

2. Щелкните этот tooexpand плитки и если обнаруживается угрозы безопасности, он отобразится в график предупреждения безопасности hello как показано ниже:

    ![Инцидент](./media/security-center-incident/security-center-incident-fig2.png)

3. Обратите внимание, что описание инцидента hello безопасности имеет свой значок, сравнивать tooother предупреждения. Щелкните его tooview более подробные сведения об инциденте.

    ![Инцидент](./media/security-center-incident/security-center-incident-fig3.png)

4. На hello **инцидент** колонку, вы увидите более сведений о безопасности инциденте, включающий полное описание, его важность (который в данном случае является высокого уровня), его текущее состояние (в этом случае она по-прежнему *активный*, что подразумевает hello пользователь еще не выполнено tooit действия — это можно сделать, щелкнув правой кнопкой мыши на инцидент hello в hello **оповещений системы безопасности** колонку), hello атаке ресурсов (в этом случае *VM1*), hello действия по исправлению для hello инцидент, и в нижней части окна hello имеется hello оповещения, которые были включены в этот инцидент. Если требуется tooobtain Дополнительные сведения о каждом оповещении, щелкните его и другая панель откроется, как показано ниже:

    ![Инцидент](./media/security-center-incident/security-center-incident-fig4.png)

Hello сведения в этой колонке изменяется соответствующим toohello предупреждение. Чтение [toosecurity управление и отвечает на запросы предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) Дополнительные сведения о том, как toomanage эти оповещения. Некоторые важные замечания, касающиеся работы этой функции.

* Новый фильтр можно, только ваш tooIncident представление оповещения только toocustomize или оба.
* такого же предупреждения могут существовать как часть инцидент (если применимо), а также отображаются как предупреждение автономный toobe приветствия.

## <a name="see-also"></a>См. также
В этом документе вы узнали, как toouse hello инцидента возможностей безопасности в центре безопасности. toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Управление и отвечать на запросы toosecurity оповещения в центр безопасности Azure](security-center-managing-and-responding-alerts.md)
* [Возможности обнаружения центра безопасности Azure](security-center-detection-capabilities.md)
* [Руководство по планированию использования центра безопасности Azure и работе в нем](security-center-planning-and-operations-guide.md)
* [Управление и отвечать на запросы toosecurity оповещения в центр безопасности Azure](security-center-managing-and-responding-alerts.md)
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md)— часто задаваемые вопросы об использовании hello службы поиска.
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.
