---
title: "Основные различия между Azure и Azure Stack при использовании служб и создании приложений | Документация Майкрософт"
description: "Что необходимо знать при использовании служб или создании приложений для Azure Stack."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: c81f551d-c13e-47d9-a5c2-eb1ea4806228
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 09/25/2017
ms.author: mabrigg
ms.openlocfilehash: 695824ef2537a97ea0530f2c33ad24d5cd9e20f8
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="key-considerations-using-services-or-building-apps-for-azure-stack"></a>Важные аспекты использования служб и создания приложений в Azure Stack

*Область применения: интегрированные системы Azure Stack и пакет SDK для Azure Stack*

Если вы используете службы или создаете приложения в Azure Stack, важно иметь представление о различиях между Azure Stack и Azure. В этой статье представлен обзор важнейших аспектов, которые нужно учесть при выборе Azure Stack в качестве гибридной облачной среды разработки.

## <a name="overview"></a>Обзор

Azure Stack ― это гибридная облачная платформа, позволяющая использовать службы Azure из центра обработки данных вашей компании или поставщика услуг. Разработчик может создавать приложения для работы в Azure Stack. Эти приложения можно развернуть в Azure Stack или в Azure. Также вы можете создать настоящие гибридные приложения, которые используют взаимодействие между облаком Azure Stack и Azure.

У оператора Azure Stack можно узнать, какие службы доступны для использования и как получить поддержку. Эти службы предоставляются в составе настраиваемых планов и предложений.

В технической документации по Azure предполагается, что приложения разрабатываются именно для службы Azure, а не для Azure Stack. При разработке и развертывании приложений в Azure Stack важно учитывать несколько важных различий.

* Azure Stack предоставляет подмножество служб и функций, доступных в Azure.
* Компания или поставщик услуг могут самостоятельно выбрать, какие службы они будут предоставлять. Это могут быть настраиваемые службы или приложения. Также они могут предоставлять собственные версии документации.
* Необходимо использовать правильные конечные точки, предназначенные для работы с Azure Stack (например, URL-адрес портала и конечную точку Azure Resource Manager).
* Необходимо использовать версии PowerShell и API, которые поддерживаются в Azure Stack. Только в этом случае можно гарантировать, что приложения будут работать в Azure Stack и Azure.

## <a name="cheat-sheet-high-level-differences"></a>Памятка: основные различия

В следующей таблице перечислены основные различия между Azure Stack и Azure. Не забывайте о них, когда создаете приложения для Azure Stack или используете службы Azure Stack.

| Область | Azure (глобальная) | Azure Stack |
| -------- | ------------- | ----------|
| Кто оператор? | Microsoft | Ваша организация или поставщик услуг.|
| Куда обращаться для получения поддержки? | Microsoft | В интегрированной системе за поддержкой следует обращаться к оператору Azure Stack (это может быть ваша организация или поставщик услуг).<br><br>Если вы используете пакет SDK для Azure Stack, посетите [форумы Майкрософт](https://social.msdn.microsoft.com/Forums/home?forum=azurestack). Так как пакет разработки предлагается как среда для оценки, служба поддержки корпорации Майкрософт не предоставляет для него официальную поддержку.
| Доступные службы | См. список [продуктов Azure](https://azure.microsoft.com/services/?b=17.04b). Выбор доступных служб зависит от региона Azure. | Azure Stack поддерживает некоторое подмножество служб Azure. Конкретный набор зависит от политики вашей организации или поставщика услуг.
| Конечная точка Azure Resource Manager* | https://management.azure.com | При работе с интегрированной системой Azure Stack используйте конечную точку, предоставленную оператором Azure Stack.<br><br>В пакете SDK используйте адрес https://management.local.azurestack.external.
| URL-адрес портала* | [https://portal.azure.com](https://portal.azure.com) | При работе с интегрированной системой Azure Stack используйте URL-адрес, предоставленный оператором Azure Stack.<br><br>В пакете SDK используйте адрес https://portal.local.azurestack.external.
| Регион | Вы можете самостоятельно выбрать регион для развертывания. | В интегрированной системе Azure Stack используется регион, доступный в этой системе.<br><br>В пакете SDK всегда используется только **локальный** регион.
| Группы ресурсов | Группа ресурсов может размещаться в нескольких регионах. | Как в интегрированной системе, так и в пакете SDK доступен только один регион.
|Поддержка пространств имен, типов ресурсов и версий API | Новейшие версии (или более ранние, пока для них сохраняется поддержка). | Azure Stack поддерживает только определенные версии. См. также раздел "Требования к версиям" в этой статье.
| | |

* Если вы являетесь оператором Azure Stack, дополнительные сведения вы можете получить в статьях [об использовании портала администрирования](../azure-stack-manage-portals.md) и [основных понятиях администрирования](../azure-stack-manage-basics.md).

## <a name="helpful-tools-and-best-practices"></a>Полезные средства и рекомендации
 
 Корпорация Майкрософт предоставляет несколько средств и рекомендаций, которые помогут вам в разработке приложений для Azure Stack.

| Рекомендации | Ссылки | 
| -------- | ------------- | 
| Установите подходящие инструментальные средства на рабочей станции разработчика. | - [Установка PowerShell](azure-stack-powershell-install.md)<br>- [Скачивание средств](azure-stack-powershell-download.md)<br>- [Настройка PowerShell](azure-stack-powershell-configure-user.md)<br>- [Установка Visual Studio](azure-stack-install-visual-studio.md) 
| Изучите информацию по следующим темам:<br>рекомендации по использованию шаблона Azure Resource Manager;<br>где найти шаблоны для быстрого начала работы;<br>использование модуля политики, который позволяет применять Azure для разработки решений в Azure Stack. | [Разработка для Azure Stack](azure-stack-developer.md) | 
| Изучите и соблюдайте рекомендации для шаблонов. | [Шаблоны Resource Manager для быстрого начала работы](https://github.com/Azure/azure-quickstart-templates/blob/master/1-CONTRIBUTION-GUIDE/best-practices.md#best-practices)
| | |

## <a name="version-requirements"></a>Требования к версиям

Azure Stack поддерживает конкретные версии Azure PowerShell и API служб Azure. Следует использовать именно эти поддерживаемые версии, чтобы приложение можно было развернуть как в Azure Stack, так и в Azure.

Чтобы гарантировать правильность версии Azure PowerShell, используйте [профили версий API](azure-stack-version-profiles.md). Чтобы определить самый свежий профиль версии API, который можно использовать, узнайте номер используемой сборки Azure Stack. Эти сведения можно получить у администратора Azure Stack.

>[!NOTE]
 Если вы используете пакет SDK для Azure Stack и имеете учетные данные администратора, воспользуйтесь разделом об определении текущей версии из статьи по [управлению обновлениями](https://docs.microsoft.com/azure/azure-stack/azure-stack-updates#determine-the-current-version).

Для получения информации о других API выполните приведенную ниже команду PowerShell, которая выводит все пространства имен, типы ресурсов и версии API, поддерживаемые для подписки Azure Stack. Обратите внимание, что на уровне свойств могут сохраниться некоторые различия. (Для выполнения этой команды необходимо [установить](azure-stack-powershell-install.md) и [настроить](azure-stack-powershell-configure-user.md) среду PowerShell для Azure Stack. Также вам потребуется подписка на действующее предложение Azure Stack.)

 ```powershell
Get-AzureRmResourceProvider | Select ProviderNamespace -Expand ResourceTypes | Select * -Expand ApiVersions | `
Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} 
```

С примером (фрагментом) выходных данных команды Get-AzureRmResourceProvider ![можно ознакомиться здесь](media/azure-stack-considerations/image1.png).
 
## <a name="next-steps"></a>Дальнейшие действия

Более подробные сведения о различиях на уровне служб см. в следующих документах.

* [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md) (Рекомендации по работе с виртуальными машинами в Azure Stack).
* [Рекомендации по работе с хранилищем Azure Stack](azure-stack-acs-differences.md).
* [Considerations for Azure Stack networking](azure-stack-network-differences.md) (Рекомендации по работе с сетями в Azure Stack).
