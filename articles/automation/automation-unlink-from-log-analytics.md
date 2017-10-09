---
title: "Учетная запись службы автоматизации Azure из службы анализа журналов aaaUnlink | Документы Microsoft"
description: "В этой статье предоставляет общие сведения о том, как toounlink автоматизации Azure учетной записи из рабочей области OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>Toounlink автоматической учетной записи из рабочей области аналитики журналов

Служба автоматизации Azure интегрируется с анализа журналов toonot только поддержка упреждающего мониторинга заданий runbook для всех учетных записей автоматизации, но требуется также при импорте hello следующие решения, которые зависят от службы анализа журналов:

* [Управление обновлениями](../operations-management-suite/oms-solution-update-management.md)
* [Отслеживание изменений](../log-analytics/log-analytics-change-tracking.md)
* [Запуск и остановка виртуальных машин в нерабочее время](automation-solution-vm-management.md)
 
Если вы решили, что необходимо прекратить toointegrate ваша учетная запись автоматизации с помощью аналитики журналов, можно разорвать связь учетной записи непосредственно из hello портал Azure.  Прежде чем продолжить, необходимо сначала tooremove hello решения, приведенные выше, в противном случае этот процесс сможет продолжить.  Просмотрите раздел hello для конкретного решения hello импорта toounderstand hello шаги tooremove его.  

После удаления этих решений можно выполнить следующие шаги toounlink hello ваша учетная запись автоматизации.

## <a name="unlink-workspace"></a>Удаление связи с рабочей областью

1. Hello портал Azure, откройте учетную запись автоматизации и в колонке учетной записи автоматизации hello в колонке hello учетной записи, выберите **разорвать связь рабочей**.<br><br> ![Параметр удаления связи с рабочей областью](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. В колонке рабочей hello отменить связь, нажмите кнопку **разорвать связь worksapce**.<br><br> ![Колонка удаления связи с рабочей областью](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  Вы получите приглашение проверка того, что вы хотите tooproceed.<br><br>
3. Хотя Azure Automation пытается учетной записи hello toounlink рабочей области аналитики журналов, отслеживания хода hello в **уведомления** меню "hello".

При использовании решения управления обновлениями hello, при необходимости вы можете hello tooremove следующих элементов, которые больше не нужны после удаления решения hello.

* Обновление расписаний.  Каждый будет иметь имена, которые соответствуют hello развертываний обновлений, созданный)

* Гибридной рабочей группы, создаваемые для решения hello.  Каждая будет называться аналогично слишком machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).

При использовании виртуальных машин для запуска и остановки hello во время решения нерабочие часы, при необходимости вы можете hello tooremove следующих элементов, которые больше не нужны после удаления решения hello.

* Расписание запуска и остановки виртуальной машины. 
* Рабочие роли Runbook запуска и остановки виртуальной машины.
* Переменные   

## <a name="next-steps"></a>Дальнейшие действия

tooreconfigure вашей toointegrate учетной записи автоматизации с помощью аналитики журналов OMS, в разделе [вперед от tooLog автоматизации Analytics (OMS) состояние задания и задания потоки](automation-manage-send-joblogs-log-analytics.md). 
