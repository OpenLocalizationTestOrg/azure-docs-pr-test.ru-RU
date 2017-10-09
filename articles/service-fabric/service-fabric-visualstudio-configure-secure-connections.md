---
title: "aaaConfigure безопасные Azure Service Fabric подключения кластера | Документы Microsoft"
description: "Узнайте, как Visual Studio tooconfigure toouse обеспечивать безопасность соединений, которые поддерживаются в кластере Azure Service Fabric hello."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a>Настройка кластера Service Fabric tooa безопасных соединений из Visual Studio
Узнайте, как Visual Studio toosecurely toouse доступ к кластеру Azure Service Fabric с настройки политики управления доступом.

## <a name="cluster-connection-types"></a>Типы подключения кластера
Поддерживаются два типа подключений кластером hello Azure Service Fabric: **небезопасные** соединений и **x509 на основе сертификатов** безопасные подключения. (Кластеры Service Fabric, размещенные локально, также поддерживают проверку подлинности **Windows** и **dSTS**.) У вас тип подключения кластера hello tooconfigure при создании кластера hello. После его создания не изменить тип подключения hello.

средства Visual Studio Service Fabric Hello поддерживает все типы проверки подлинности для подключения кластера tooa для публикации. В разделе [установка кластера Service Fabric с портала Azure hello](service-fabric-cluster-creation-via-portal.md) инструкции о том, как tooset безопасности кластера Service Fabric.

## <a name="configure-cluster-connections-in-publish-profiles"></a>Настройка подключения кластера в профилях публикации
Если вы публикуете проект Service Fabric из Visual Studio, используйте hello **опубликовать приложение Service Fabric** диалогового окна поле toochoose кластера с Azure Service Fabric. В разделе **Конечная точка подключения** выберите кластер в своей подписке.

![Hello ** публикации службы структуры приложения ** используется диалоговое окно используется tooconfigure подключения Service Fabric.][publishdialog]

Hello **опубликовать приложение Service Fabric** диалоговое окно автоматически проверяет подключение кластера hello. Если будет предложено, войдите в tooyour учетная запись Azure. Проверка считается пройденной, означает, что в системе установлены правильные сертификаты безопасно установлены tooconnect toohello кластера или кластера, не защищенного hello. Сбои при выполнении проверки может быть вызвана, неполадками в сети или при отсутствии безопасного кластеру tooa tooconnect системы правильно настроены.

![Hello ** публикации службы структуры приложения ** диалоговое окно проверяет существующий, правильность настройки подключения кластера Service Fabric.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a>tooconnect tooa безопасности кластера
1. Убедитесь, что доступен один hello сертификатов клиентов, которые hello доверие кластера назначения. сертификат Hello обычно совместно как файл обмена личной информацией (PFX-файл). В разделе [установка кластера Service Fabric с портала Azure hello](service-fabric-cluster-creation-via-portal.md) для как tooconfigure hello server toogrant доступ к tooa клиента.
2. Установите сертификат доверенного hello. toodo, дважды щелкните hello PFX-файл, или используйте hello PowerShell скрипт Import-PfxCertificate tooimport hello сертификаты. Установите сертификат hello слишком**Cert: \LocalMachine\My**. Он является ОК tooaccept все параметры по умолчанию при импорте сертификата hello.
3. Выберите hello **публикации...**  контекстном меню hello объекта hello tooopen проекта hello **публикации приложения Azure** диалоговое окно, выберите hello целевого кластера. Средство Hello автоматически разрешает подключение hello и сохраняет профиль публикации параметров в hello безопасное соединение hello.
4. Необязательно: Изменение hello публикации toospecify профиля подключения безопасности кластера.
   
   Поскольку требуется вручную изменить сведения о сертификате hello toospecify в файл XML профиля публикации hello, убедиться, что имя хранилища сертификатов toonote hello, хранения, расположение и отпечаток сертификата. Вам потребуется tooprovide эти значения для хранилища сертификатов hello имя и местоположение хранилища. В разделе [как: hello получения отпечатка сертификата](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) для получения дополнительной информации.
   
   Можно использовать hello *ClusterConnectionParameters* параметры toospecify hello PowerShell параметры toouse при подключении toohello кластера Service Fabric. Допустимые параметры — это все, принимаются командлетом Connect-ServiceFabricCluster hello. Список доступных параметров см. в статье [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).
   
   Если вы публикуете tooa удаленного кластера, необходимо toospecify hello соответствующие параметры для этого конкретного кластера. Hello ниже приведен пример кластера незащищенные подключения tooa:
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   Ниже приведен пример для подключения tooan x509 на основании сертификата безопасности кластера:
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. Другие необходимые параметры, такие как параметры обновления и расположение файла параметров приложения и снова опубликовать приложение из hello **опубликовать приложение Service Fabric** диалоговое окно в Visual Studio.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о доступе к кластерам Service Fabric см. в статье [Визуализация кластера с помощью Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
