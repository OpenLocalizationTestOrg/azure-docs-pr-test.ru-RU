---
title: "Предварительная версия управления aaaAdministrative единицы в Azure Active Directory"
description: "Использование административных единиц для делегирования разрешений в Azure Active Directory на фрагментарном уровне"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Управление административными единицами в Azure AD (общедоступная предварительная версия)
В этой статье описываются административные единицы — новый контейнер ресурсов, которые могут использоваться для передачи административных разрешений по подсетям пользователей и применения политик tooa подмножества пользователей Azure Active Directory. В Azure Active Directory административные единицы позволяют Центральные администраторы toodelegate разрешения tooregional Администраторы или tooset политики на более детальном уровне.

Это полезно для организаций с независимыми подразделениями, например большого университета, состоящего из многочисленных автономных факультетов (бизнес-школы, инженерных и технических факультетов и пр.). В таких структурах есть собственные ИТ-администраторы, которые управляют доступом, пользователями и политиками на уровне своего подразделения. Центральные администраторы должны toobe может предоставить эти разрешения администраторы подразделений переноса пользователей hello в их конкретного подразделения. В частности для этого примера центральный администратор может, для экземпляра, создать административную единицу для конкретной школы (бизнес-школы) и заполнить ее только пользователями бизнес-школы hello. Затем центральный администратор может добавить hello бизнес-школы tooa области ИТ сотрудник, другими словами, hello предоставление ИТ-персоналу административные разрешения бизнес школы только через hello административной единицы.

> [!IMPORTANT]
> Для назначения ролей для административных единиц вам необходима активная подписка Azure Active Directory Premium. Дополнительные сведения см. в разделе [Приступая к работе с Azure AD Premium](active-directory-get-started-premium.md).
>


С точки зрения центрального администратора hello административная единица — объект каталога, можно создать и заполнить с помощью ресурсов. **В этом выпуске предварительной версии ресурсами могут быть только пользователи.** После создания и заполнения административную единицу hello может служить hello toorestrict область, разрешение только ресурсами, которые содержатся в административной единице hello.

## <a name="managing-administrative-units"></a>Управление административными единицами
В этом предварительном выпуске можно создать и управлять административными единицами с помощью hello Azure Active Directory для командлеты модуля Windows PowerShell. Дополнительные сведения о том, как toolearn toodo, в разделе [работа с административными единицами](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Дополнительные сведения о требованиях к программному обеспечению и установке модуля hello Azure AD, а также сведения о hello командлеты модуля Azure AD для управления административными единицами, включая синтаксис, описания параметров и примеры см. в разделе [Azure Active Каталог PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

## <a name="next-steps"></a>Дальнейшие действия
[Выпуски Azure Active Directory](active-directory-editions.md)
