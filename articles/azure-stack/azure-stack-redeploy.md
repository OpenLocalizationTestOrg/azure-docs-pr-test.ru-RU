---
title: "aaaRedeploy стек Azure | Документы Microsoft"
description: "Повторное развертывание стек Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 795af5ea-892d-40b1-a080-42e4472e4bba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: ec26745bcb54edd7c26960eec55d41504aff1911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-azure-stack"></a>Повторное развертывание стек Azure
tooredeploy стек Azure вы должны начать с нуля как описано ниже.

## <a name="steps-tooredeploy-azure-stack"></a>Действия tooredeploy стек Azure
1. На узел комплект средств для разработки hello, откройте консоль PowerShell с повышенными привилегиями > перейдите сценарий asdk installer.ps1 toohello > запустите его > щелкните **перезагрузки**.
2. Здравствуйте, выберите базовую операционную систему (не **стека Azure**) и нажмите кнопку **Далее**.
3. После перезагрузки узла комплект средств для разработки hello, удалите файл CloudBuilder.vhdx hello, который использовался в рамках предыдущего развертывания hello.
4. [Развертывание пакета средств разработки hello](azure-stack-run-powershell-script.md).

## <a name="next-steps"></a>Дальнейшие действия
[Подключение tooAzure стека](azure-stack-connect-azure-stack.md)

