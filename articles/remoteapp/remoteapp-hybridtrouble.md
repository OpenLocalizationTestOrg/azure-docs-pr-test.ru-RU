---
title: "Создание гибридной коллекции RemoteApp aaaTroubleshoot | Документы Microsoft"
description: "Узнайте, как сбои при создании коллекции гибридного tootroubleshoot удаленных приложений RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Устранение неполадок создания гибридных коллекций Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Размещается в гибридной коллекции и сохраняет данные в облако Azure hello, но также позволяет пользователям обращаться к данным и ресурсам, хранимым в локальной сети. Пользователи могут получать доступ к приложениям, выполняя вход с помощью своих корпоративных учетных данных, синхронизированных с Azure Active Directory с федерацией. Вы можете развернуть гибридную коллекцию, которая использует существующую виртуальную сеть Azure, или создать новую виртуальную сеть. Рекомендуем создать или использовать подсеть виртуальной сети с достаточно большим диапазоном CIDR, рассчитанным на ожидаемый в будущем рост для Azure RemoteApp.

Еще не создали свою коллекцию? В разделе [Создание гибридной коллекции](remoteapp-create-hybrid-deployment.md) hello шагов.

Если возникают проблемы при создании коллекции или если коллекция hello не работает способом hello, вы считаете, что он должен, извлечь hello следующую информацию.

## <a name="your-image-is-invalid"></a>Недопустимый образ
При появлении сообщения, как «GoldImageInvalid», когда ожидается для Azure tooprovision вашей коллекции, это означает, что образ шаблона не соответствует hello [определенные требования изображения](remoteapp-imagereqs.md). Начинаем, читать их [требования](remoteapp-imagereqs.md), исправьте образ и повторите попытку коллекции toocreate.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>Определены ли группы безопасности сети для вашей виртуальной сети?
При наличии сетевых групп безопасности, определенные в подсети hello, вы используете для коллекции, убедитесь, что они [URL-адреса и порты](remoteapp-ports.md) осуществляется из подсети.

Можно добавить дополнительный сетевой безопасности группы toohello развернуты виртуальные машины вами в подсети hello более жесткий контроль.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Используете ли вы собственные DNS-серверы? Доступны ли они из вашей подсети виртуальной сети?
> [!NOTE]
> У вас есть toomake приветствия убедиться, что DNS-серверы в сети, всегда являются вверх и всегда будет tooresolve hello виртуальных машин, размещенных в hello виртуальной сети. Не используйте Google DNS для этого.
> 
> 

Для гибридных коллекций используйте собственные DNS-серверы. Можно указать их в схеме конфигурации сети или через портал управления hello при создании виртуальной сети. DNS-серверы используются в порядке hello, они указаны в виде перехода на другой ресурс (в противоположность tooround циклический перебор).  
См. слишком[разрешение имен для виртуальных машин и экземпляров ролей](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake убедиться, что DNS-серверы, настроенные correcly.

Убедитесь, что hello DNS-серверов для вашей коллекции доступны через hello подсети виртуальной сети, указанное для этой коллекции.

Например:

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Определение DNS-сервера](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>Используется ли в вашей коллекции контроллер домена Active Directory?
В настоящее время с Azure RemoteApp можно связать только один домен Active Directory. Hello гибридного коллекция поддерживает только Azure Active Directory учетные записи, которые были синхронизированы с помощью средства DirSync из развертывания Windows Server Active Directory; в частности либо синхронизирован с параметром синхронизации паролей hello синхронизированы с федерацией служб федерации Active Directory (AD FS) настроен. Требуется toocreate настраиваемый домен, который соответствует hello суффикс домена имени участника-пользователя для локального домена и настройка интеграции каталогов.

Дополнительные сведения см. в статье [Требования Azure AD + Active Directory для Azure RemoteApp](remoteapp-ad.md).

Убедитесь, что указаны допустимые сведения домена hello и hello контроллер домена доступен из hello создания виртуальной Машины в подсети hello, используемой для удаленного приложения Azure. Также убедитесь, что hello учетной записи службы, предоставленные учетные данные предоставлены разрешения tooadd компьютеров toohello домена и что hello имя AD, предоставляемые разрешается из hello DNS в hello виртуальной сети.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Какое имя домена было указано при создании коллекции?
имя домена Hello, создании или добавлено должно быть внутреннее имя домена (не имя домена Azure AD) и должно быть в разрешимом формате DNS (contoso.local). Например имеется внутреннее имя Active Directory (contoso.local) и Active Directory имя участника-пользователя (contoso.com) - имеется toouse hello внутреннее имя при создании коллекции.

