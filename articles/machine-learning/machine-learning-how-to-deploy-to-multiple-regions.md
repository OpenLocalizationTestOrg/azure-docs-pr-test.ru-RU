---
title: "aaaHow toodeploy веб-службы областей toomultiple | Документы Microsoft"
description: "Действия toodeploy (копия) регионов tooother веб-службу."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>Как toodeploy веб-службы toomultiple областей
Hello новый веб-службы Azure позволяют tooeasily развертывание web service toomultiple области без необходимости использовать несколько подписок или рабочие области. 

Цены — область конкретного, поэтому необходимо определить план выставления счетов для каждого региона, в которых выполняется развертывание hello веб-службы.

## <a name="toocreate-a-plan-in-another-region"></a>toocreate плана в другой регион
1. Выполните вход в [веб-службы Машинного обучения Microsoft Azure](https://services.azureml.net/).
2. Нажмите кнопку hello **планы** пункт меню.
3. В планах hello через представление страницы, нажмите кнопку **New**.
4. Из hello **подписки** раскрывающийся список, в какие hello новый план будет находиться подписки выберите hello.
5. Из hello **область** раскрывающийся список, выберите регион для hello новый план. Hello параметры плана для hello выбранной области будут отображаться в hello **параметры плана** раздел страницы приветствия.
6. Из hello **группы ресурсов** раскрывающийся список, выберите группу ресурсов для hello плана. Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. В **имя плана** имя типа hello hello плана.
8. В разделе **параметры плана**, выберите уровень выставления счетов hello для hello новый план.
9. Щелкните **Создать**.

## <a name="deploying-hello-web-service-tooanother-region"></a>Развертывание hello web service tooanother области
1. Нажмите кнопку hello **веб-службы** пункт меню.
2. Выберите веб-служба развертывается новая область tooa hello.
3. Нажмите **Копировать**.
4. В **имя веб-службы**, введите новое имя для hello веб-службы.
5. В **веб-службы описание**, введите описание для hello веб-службы.
6. Из hello **подписки** раскрывающийся список, выберите hello подписки, в которой hello будет находиться веб-службу.
7. Из hello **группы ресурсов** раскрывающийся список, выберите группу ресурсов для hello веб-службы. Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Из hello **область** раскрывающийся список, выберите hello региона, в какие toodeploy hello веб-службы.
9. Из hello **учетной записи хранилища** раскрывающийся список, выберите учетную запись хранения в которых hello toostore веб-службы.
10. Из hello **цена плана** раскрывающийся список, выберите план в регионе hello, выбранная на шаге 8.
11. Нажмите **Копировать**.

