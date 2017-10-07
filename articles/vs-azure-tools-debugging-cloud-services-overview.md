---
title: "aaaOptions для отладки Azure облачные службы | Документы Microsoft"
description: "Отладка облачных служб Azure"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>Узнайте hello различные способы toodebug облачной службы Azure
В этой статье содержатся ссылки toohello различных способов toodebug облачной службы Azure. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Отладка облачной службы Azure в Visual Studio
Можно сохранить время и деньги с помощью toodebug эмулятор вычислений Azure hello облачной службы на локальном компьютере. Посредством локальной отладки службы перед ее развертыванием можно повысить надежность и производительность службы, не платя за время использования вычислительных ресурсов. Однако некоторые ошибки могут возникнуть только при запуске облачной службы в среде Azure. Включив удаленную отладку при публикации службы, а затем присоединив экземпляра роли tooa hello отладчика можно производить отладку ошибок, возникающих только при выполнении облачной службы в Azure. Дополнительные сведения см. в разделе [Отладка облачной службы на локальном компьютере](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).

## <a name="using-azure-diagnostics"></a>Использование службы диагностики Azure 
Вы можете использовать диагностику Azure toolog подробные сведения из кода, выполняемых внутри ролей, ли hello ролей, выполняются в среде разработки hello, или в Azure. Дополнительные сведения см. в статье [Включение системы диагностики Azure в облачных службах Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).

## <a name="using-intellitrace"></a>Использование IntelliTrace 
Если вы используете Visual Studio Enterprise toowrite ролей целевое .NET Framework 4.5, можно включить IntelliTrace в момент hello развертывания облачной службы Azure из Visual Studio. IntelliTrace предоставляет журнал можно использовать с Visual Studio toodebug приложения как если бы оно было запущено в Azure. Дополнительные сведения см. в статье [Отладка опубликованной облачной службы с помощью IntelliTrace и Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Удаленная отладка 
Можно включить удаленную отладку облачных служб во время hello при развертывании hello облачной службы из Visual Studio. При выборе tooenable удаленной отладки для развертывания службы удаленной отладки устанавливаются на hello виртуальных машин, работающих каждого экземпляра роли. Такие службы (например, `msvsmon.exe`) не влияют на производительность и не требуют дополнительных расходов. Дополнительные сведения см. в разделе [Отладка облачной службы в Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).

## <a name="next-steps"></a>Дальнейшие действия
- [Отладка облачной службы Azure или виртуальной Машины в Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -Узнайте подробности hello как toodebug Azure облачных служб.
