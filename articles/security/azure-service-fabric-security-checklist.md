---
title: "Контрольный список безопасности структуры службы aaaAzure | Документы Microsoft"
description: "В этой статье представлен контрольный список для обеспечения безопасности Azure Service Fabric."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Контрольный список для обеспечения безопасности Azure Service Fabric
Эта статья содержит удобный контрольный список, который поможет обеспечить защиту среды Azure Service Fabric.

## <a name="introduction"></a>Введение
Azure Service Fabric — это платформа распределенных систем, который позволяет легко toopackage, развертывания и управления масштабируемыми и надежными микрослужбами. Service Fabric также устраняет hello значительным препятствием для разработки и управления ими облачных приложений. Получая гарантированную масштабируемость, надежность и управляемость, разработчики и администраторы могут сосредоточиться на реализации критически важных и ресурсоемких рабочих нагрузок вместо того, чтобы тратить силы на решение сложных проблем с инфраструктурой.

## <a name="checklist"></a>Контрольный список
Используйте следующий контрольный список toohelp, убедитесь, что еще не пропущены все важные вопросы, касающиеся настройки и управления ей безопасное решение Azure Service Fabric hello.


|Категория контрольного списка| Описание |
| ------------ | -------- |
|[Управление доступом на основе ролей (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>Контроль доступа позволяет hello кластера администратора toolimit доступа toocertain кластера операции для разных групп пользователей, повышение безопасности кластера hello.</li><li>Администраторы имеют полный доступ toomanagement возможности (включая возможности чтения и записи). </li><li>   Пользователи, по умолчанию имеют только доступ на чтение toomanagement возможности (например, возможности работы с запросами), hello возможность tooresolve, приложений и служб.</li></ul>|
|[Сертификаты X.509 и Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>[Сертификаты](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates), которые используются в кластерах, выполняющих рабочие нагрузки в рабочей среде, следует создать с помощью правильно настроенной службы сертификации Windows Server или получить из утвержденного [центра сертификации](https://en.wikipedia.org/wiki/Certificate_authority).</li><li>Никогда не используйте в рабочей среде какие-либо [временные или тестовые сертификаты](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development), созданные с помощью таких инструментов, как [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx). </li><li>Можно использовать [самозаверяющий сертификат](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security), но это следует делать только для тестовых кластеров, а не в рабочей среде.</li></ul>|
|[Безопасность кластера](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>сценарии безопасности кластера Hello включают безопасность узла на узел, узел клиента [управление доступом на основе ролей (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles).</li></ul>|
|[Аутентификация в кластере](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Позволяет аутентифицировать [обмен данными между узлами](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md) для федерации кластера. </li></ul>|
|[Аутентификация сервера](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Проверяет подлинность hello [кластера конечные точки управления](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal) tooa управления клиента.</li></ul>|
|[Безопасность приложения](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>шифрование и расшифровка значений конфигурации приложений;</li><li> шифрование данных между узлами во время репликации.</li></ul>|
|[Сертификат кластера](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>Этот сертификат является обязательным toosecure hello взаимодействия между hello узлы в кластере.</li><li>  Задать hello отпечаток сертификата основной hello в разделе отпечаток hello и который hello получателей в переменных ThumbprintSecondary hello.</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>Этот сертификат представлены toohello клиента, она попытается tooconnect toothis кластера. Для обновления можно использовать два разных сертификата сервера — основной и дополнительный.</li></ul>|
|ClientCertificateThumbprints| <ul><li>Это набор сертификатов, которые должны tooinstall на клиентах hello с проверкой подлинности. </li></ul>|
|ClientCertificateCommonNames| <ul><li>Задать hello общее имя hello первый сертификат клиента для hello CertificateCommonName. Hello CertificateIssuerThumbprint является отпечатком hello для hello поставщиком этого сертификата. </li></ul>|
|ReverseProxyCertificate| <ul><li>Это необязательный сертификат, который может быть указан, если необходимо, чтобы toosecure вашей [обратного прокси-сервера](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy). </li></ul>|
|Хранилище ключей| <ul><li>Использовать сертификаты toomanage для кластеров Service Fabric в Azure.  </li></ul>|


## <a name="next-steps"></a>Дальнейшие действия
- [Обновление кластера Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [Управление приложениями Service Fabric в Visual Studio](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio)
- [Общие сведения о наблюдении за работоспособностью системы в Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction)
