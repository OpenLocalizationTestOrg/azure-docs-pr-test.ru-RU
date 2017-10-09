---
title: "aaaSecure в кластер, запущенный в Windows с помощью средств безопасности Windows | Документы Microsoft"
description: "Узнайте, как tooconfigure на автономный узел узел и узел клиента безопасности кластера под управлением Windows с помощью средств безопасности Windows."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Защита изолированного кластера под управлением Windows с помощью системы безопасности Windows
tooprevent несанкционированный доступ кластера Service Fabric tooa, необходимо обеспечить безопасность кластера hello. Безопасность особенно важна, запускаемый рабочих нагрузок кластера hello. В этой статье описывается как tooconfigure безопасности узла на узел и узел клиента с помощью системы безопасности Windows в hello *ClusterConfig.JSON* файла.  процесс Hello соответствует toohello настройки безопасности шага [создать автономный кластер, запущенный в Windows](service-fabric-cluster-creation-for-windows-server.md). Дополнительные сведения об использовании системы безопасности Windows в Service Fabric см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).

> [!NOTE]
> Выбор hello безопасности узла на узел следует внимательно рассмотреть так существует не поддерживается обновление кластера из одного tooanother Выбор безопасности. Выбор безопасности toochange hello, у вас есть полный кластера toorebuild hello.
>
>

## <a name="configure-windows-security-using-gmsa"></a>Настройка безопасности Windows с помощью групповой управляемой учетной записи службы  
Образец Hello *ClusterConfig.gMSA.Windows.MultiMachine.JSON* загрузить файл конфигурации с hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. Почтовый](http://go.microsoft.com/fwlink/?LinkId=730690) изолированный пакет кластера содержит шаблон для настройки безопасности Windows с помощью [групповой управляемой учетной записи службы (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **Параметр конфигурации** | **Описание** |  
| --- | --- |  
| WindowsIdentities |Содержит идентификаторы hello кластера и клиента. |  
| ClustergMSAIdentity |Настраивает безопасность обмена данными между узлами. Групповая управляемая учетная запись службы. |  
| ClusterSPN |Полное доменное имя субъекта-службы для групповой управляемой учетной записи службы|  
| ClientIdentities |Настраивает безопасность обмена данными между клиентами и узлами. Массив учетных записей клиентов. |  
| Удостоверение |удостоверение клиента Hello, пользователя домена. |  
| IsAdmin |Значение true указывает, что пользователь домена hello не клиентского доступа администратора, false для клиентского доступа пользователя. |  
  
[Узел безопасности toonode](service-fabric-cluster-security.md#node-to-node-security) настроить, задав **ClustergMSAIdentity** структуры службы, когда потребуется toorun под групповой управляемой учетной записи. В порядке toobuild отношений доверия между узлами они должны быть в курсе друг с другом. Это можно сделать двумя способами: указать hello группы управляемых учетных записей служб, включающий все узлы в кластере hello или группу домена машины hello, которая включает все узлы в кластере hello. Настоятельно рекомендуется использовать hello [групповой управляемой учетной записи службы (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) подход, особенно для больших кластеров (более 10 узлов) или для кластеров, которые, скорее всего, toogrow или сжатия.  
Этот подход не требует создания hello группы домена, для которого администратор кластера были предоставлены tooadd права доступа и удалять элементы. Эти учетные записи также можно использовать для автоматического управления паролями. Дополнительные сведения см. в статье [Начало работы с групповыми управляемыми учетными записями служб](http://technet.microsoft.com/library/jj128431.aspx).  
 
[Клиент toonode безопасности](service-fabric-cluster-security.md#client-to-node-security) настраивается с помощью **ClientIdentities**. В порядке tooestablish отношения доверия между клиентом и hello кластера необходимо настроить tooknow кластера hello идентификаторы, которые клиент, он может доверять. Это можно сделать двумя способами: указать hello пользователи группы домена, можно подключиться, или указать hello узел пользователей домена, которые могут подключаться. Service Fabric поддерживает два типа элемента управления различный уровень доступа для клиентов, подключенных tooa кластера Service Fabric: администратора и пользователя. Управление доступом предоставляет возможность hello hello кластера администратора toolimit доступа toocertain типы операций кластера для разных групп пользователей, повышение безопасности кластера hello.  Администраторы имеют полный доступ toomanagement возможности (включая возможности чтения и записи). Пользователи, по умолчанию имеют только доступ на чтение toomanagement возможности (например, возможности работы с запросами), hello возможность tooresolve, приложений и служб. Дополнительные сведения о ролях доступа см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric](service-fabric-cluster-security-roles.md).  
 
Hello в следующем примере **безопасности** раздел настраивает безопасность Windows, с помощью управляемой и указывает, что hello компьютеров в *ServiceFabric.clusterA.contoso.com* gMSA являются частью кластера hello и что *CONTOSO\usera* имеет доступ администратора клиента:  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>Настройка безопасности Windows с использованием группы компьютеров  
Образец Hello *ClusterConfig.Windows.MultiMachine.JSON* загрузить файл конфигурации с hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. Почтовый](http://go.microsoft.com/fwlink/?LinkId=730690) изолированный пакет кластера содержит шаблон для настройки безопасности Windows.  Безопасность Windows настраивается в hello **свойства** раздела: 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **Параметр конфигурации** | **Описание** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** задано слишком*Windows* Если ClusterIdentity указывает имя группы компьютеров Active Directory. |  
| ServerCredentialType |Значение слишком*Windows* tooenable безопасности Windows для клиентов.<br /><br />Это означает, что выполнение клиентов hello hello кластера и самого кластера hello в домене Active Directory. |  
| WindowsIdentities |Содержит идентификаторы hello кластера и клиента. |  
| ClusterIdentity |Используйте имя группы компьютеров, domain\machinegroup, tooconfigure безопасности узла на узел. |  
| ClientIdentities |Настраивает безопасность обмена данными между клиентами и узлами. Массив учетных записей клиентов. |  
| Удостоверение |Добавьте пользователя домена hello домен\имя пользователя для удостоверения клиента hello. |  
| IsAdmin |Набор tootrue toospecify, hello пользователя домена имеет доступ администратора клиента или false для клиентского доступа пользователя. |  

[Узел безопасности toonode](service-fabric-cluster-security.md#node-to-node-security) настраивается с помощью параметра **ClusterIdentity** Если toouse группу компьютеров в домене Active Directory. Дополнительные сведения см. в статье [How to Create a Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx) (Как создать группу компьютеров в Active Directory).

[Защиту обмена данными между клиентом и узлом](service-fabric-cluster-security.md#client-to-node-security) можно настроить с помощью параметра **ClientIdentities**. tooestablish доверие между клиентом и hello кластера, необходимо настроить клиент hello tooknow кластера hello, можно доверять удостоверений, которые hello кластера. Установить отношения доверия можно двумя разными способами:

- Укажите пользователи группы домена hello, которые могут подключаться.
- Укажите узел пользователи hello домена, которые могут подключаться.

Service Fabric поддерживает два типа элемента управления различный уровень доступа для клиентов, подключенных tooa кластера Service Fabric: администратора и пользователя. Контроль доступа позволяет hello кластера администратора toolimit доступа toocertain типы операций кластера для разных групп пользователей, что делает более безопасные hello кластера.  Администраторы имеют полный доступ toomanagement возможности (включая возможности чтения и записи). Пользователи, по умолчанию имеют только доступ на чтение toomanagement возможности (например, возможности работы с запросами), hello возможность tooresolve, приложений и служб.  

Hello в следующем примере **безопасности** раздел, предназначенный для настройки безопасности Windows, указывает, что hello компьютеров в *ServiceFabric/clusterA.contoso.com* являются частью кластера hello и указывает, что  *CONTOSO\usera* имеет доступ администратора клиента:

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> Службу Service Fabric не нужно развертывать на контроллере домена. Убедитесь в том, что ClusterConfig.json не включать hello IP-адрес контроллера домена hello, при использовании группу компьютеров или группы управляемой учетной записи службы (gMSA).
>
>

## <a name="next-steps"></a>Дальнейшие действия
После настройки безопасности Windows в hello *ClusterConfig.JSON* файла, возобновить процесс создания кластера hello в [создать автономный кластер, запущенный в Windows](service-fabric-cluster-creation-for-windows-server.md).

Дополнительные сведения о защите обмена данными между узлами, между клиентом и узлом и об управлении доступом на основе ролей см. в статье [Сценарии защиты кластера Service Fabric](service-fabric-cluster-security.md).

В разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md) примеры соединения с помощью PowerShell или FabricClient.
