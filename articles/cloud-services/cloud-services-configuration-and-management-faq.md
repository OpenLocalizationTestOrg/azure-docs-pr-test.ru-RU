---
title: "проблемы aaaConfiguration и управления для облачных служб Microsoft Azure часто задаваемые вопросы о | Документы Microsoft"
description: "В этой статье перечислены hello часто задаваемые вопросы о конфигурации и управления для облачных служб Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Проблемы конфигурации и управления для облачных служб Azure. Вопросы и ответы (FAQ)

В этой статье приведены часто задаваемые вопросы по конфигурации и управлению для [облачных служб Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Кроме того, можно обратиться к hello [страницы размер виртуальной Машины облачных служб](cloud-services-sizes-specs.md) для сведений о размере.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>Как добавить веб-сайт toomy «nosniff»?
Клиенты tooprevent из сканирование hello типов MIME, добавьте параметр в вашей *web.config* файла.

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

Его можно также добавить как параметр в службах IIS. Используйте следующие hello команды с hello [общие задачи запуска](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) статьи.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

## <a name="how-do-i-customize-iis-for-a-web-role"></a>Как настроить IIS для веб-роли?
Используйте сценарий запуска IIS hello из hello [общие задачи запуска](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) статьи.

## <a name="i-cannot-scale-beyond-x-instances"></a>Не удается выполнить масштабирование на более чем X экземпляров
Подписки Azure имеет ограничение на количество ядер, которые можно использовать в hello. Масштабирование не будет работать при использовании всех доступных ядер hello. Например, если установлено ограничение в 100 ядер, это означает, что в облачной службе можно создать 100 экземпляров виртуальной машины размера A1 или 50 экземпляров виртуальной машины размера A2.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>Как реализовать доступ на основе ролей для облачных служб?
Облачные службы не поддерживает модель управления доступом на основе ролей (RBAC) hello, как он не является службой на основе диспетчера ресурсов Azure.

См. [Управление доступом на основе ролей в Azure и классические администраторы подписки](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>Как задать время ожидания простоя hello для балансировки нагрузки Azure?
Можно указать время ожидания hello в файле определения (csdef) службы следующим образом:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
Дополнительные сведения см. в статье [Новое: настраиваемое время ожидания простоя для Azure Load Balancer](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/).

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>Можно внутренней разработчиками Майкрософт экземпляров службы протокола удаленного рабочего СТОЛА toocloud без разрешения?
Следующим Microsoft, которые strict процесс, который не допускает внутренней инженеров tooRDP в облачной службе без письменного разрешения (адрес электронной почты или других переписки) из hello владельца или она их.

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>Почему неполон hello цепочки сертификатов my SSL-сертификата облачной службы
Корпорация Майкрософт рекомендует пользователям установить hello Полная цепочка сертификатов (cert конечного, промежуточных сертификатов и корневого сертификата) вместо просто hello конечного сертификата. При установке только hello конечного сертификата полагаться на цепочку сертификатов Windows toobuild hello путем прохода hello списка доверия Сертификатов. В случае периодически возникающие сетевые проблемы или DNS в Azure или Центра обновления Windows при toovalidate hello сертификата Windows hello сертификат может считаться недействительными. Установив hello Полная цепочка сертификатов, можно избежать этой проблемы. Здравствуйте, блог по [как tooinstall цепочек SSL-сертификат](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) показано, как toodo это.

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>Как связать статический облачной службы toomy IP адрес?
tooset статический IP-адрес необходимо toocreate зарезервированный IP-адрес. Этот зарезервированный IP-адрес может быть связан tooa развертывании новой облачной службы или tooan существующий. См. следующие документы подробности hello.
* [Как toocreate зарезервированного IP-адреса](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [Зарезервировать IP-адрес hello существующей облачной службы](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [Связать зарезервированный IP tooa новой облачной службы](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [Связать зарезервированный tooa IP выполнение развертывания](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [Связать зарезервированный IP tooa облачной службы с помощью файла конфигурации службы](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>Что такое hello квоту для моей облачной службы
См. раздел [Ограничения определенных служб](../azure-subscription-service-limits.md#subscription-limits).

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>Почему hello диска на виртуальную Машину my облачной службы определяет очень мало свободного места на диске
Это ожидаемое поведение, и его не следует вызывать любое приложение tooyour проблему. Ведение журнала включается для дисков % на виртуальных машинах Azure PaaS, который фактически использует double hello объем пространства, файлы обычно занимают uproot hello %. Однако существует несколько моментов toobe, которое фактически превратить в не проблемой.

Hello размер диска % approot % вычисляется как < размер .cspkg + размер журнала max > + поле свободного пространства, или 1,5 ГБ, какая величина больше. размер ВМ Hello никак не влияет на это вычисление. (hello размер виртуальной Машины влияет только на размер hello временный диск C: hello.) 

Это не поддерживается toowrite toohello % approot % диска. При создании toohello виртуальной Машине Azure, это необходимо сделать в ресурсе временные LocalStorage (или другой параметр больших двоичных объектов, например хранилище файлов Azure и т. д.). Поэтому hello объем свободного места в папке % approot % hello не имеет смысла. Если вы не уверены, есть ли приложение записывает approot % toohello % диска, всегда можно позволить службе работают в течение нескольких дней, а затем сравнить hello, «до» и «после» размеры. 

Azure ничего не записывают approot % toohello % диска. Hello виртуальный жесткий ДИСК создается из вашего cspkg-файл и hello виртуальной Машины Azure для подключения, hello единственное, что могли бы написать toothis диска после вашего приложения. 

параметры журнала Hello ненастраиваемые, поэтому его нельзя отключить.

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Каковы функции hello и возможности, предоставляемые Azure basic IP-адресов и Идентификаторы и DDOS?
Azure имеет IP-адресов и Идентификаторы в toodefend физических серверов центра обработки данных от угроз. Кроме того, клиенты могут разворачивать сторонние решения по обеспечению безопасности, такие как брандмауэры приложений, сетевые брандмауэры, антивредоносное ПО, системы обнаружения вторжений, системы предотвращения (IDS/IPS) и многое другое. Дополнительные сведения см. в разделе [Защита данных и ресурсов и соответствие глобальным стандартам безопасности](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).

Корпорация Майкрософт постоянно отслеживает угрозы toodetect серверов, сетей и приложений. Подход multipronged управления угрозами Azure использует обнаружения вторжений, распределенных отказ в обслуживании (DDoS) атаки предотвращения проникновения, аналитику поведения, обнаружение аномалий и машинное обучение tooconstantly усилить его защиты и снижения степени риска. Антивредоносное ПО Майкрософт для Azure защищает облачные службы и виртуальные машины Azure. У вас есть hello параметр toodeploy безопасности стороннего решения Кроме того, таких как брандмауэры приложения web, Сетевые брандмауэры, защиты от вредоносных программ, вторжений выявления и предотвращения систем (Идентификаторы или IP-адреса) и многое другое.

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>Почему IIS остановить запись toohello каталог журнала?
Исчерпаны hello квоты локальное хранилище для написания toohello каталог журнала. Чтобы исправить это, выполните одно из следующих трех действий.
* Включение диагностики для служб IIS и диагностики hello периодически перемещаются tooblob хранилища.
* Вручную удалите файлы журнала из каталога ведения журнала hello.
* Увеличьте квоту для локальных ресурсов.

Дополнительные сведения см. в разделе hello следующие документы:
* [Хранение и просмотр диагностических данных в службе хранилища Azure](cloud-services-dotnet-diagnostics-storage.md)
* [Журналы IIS прекращают запись в облачной службе](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>Что такое назначение hello hello «Windows Azure Tools шифрования сертификата для расширения»
Эти сертификаты автоматически создаются каждый раз, когда расширение добавляется toohello облачной службы. Чаще всего это hello WAD расширения или hello расширения протокола удаленного рабочего СТОЛА, но это может быть другим пользователям, например hello модуль защиты от вредоносных программ или сборщик журналов. Эти сертификаты используются только для шифрования и расшифровки hello закрытой конфигурации расширения hello. Дата окончания срока действия Hello никогда не проверяется, не имеет значения, если истек срок действия сертификата hello. 

Эти сертификаты можно игнорировать. Если вы хотите очистить hello сертификаты, нужно удалить их все. Azure возникнет ошибка при попытке toodelete сертификат, который уже используется.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>Как создать подписи сертификата запроса (CSR) без «RDP-ing» в экземпляре toohello?
См. следующие рекомендации документа hello.

>[Получение сертификата для использования с веб-сайтами Microsoft Azure (WAWS)](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

Обратите внимание, что CSR является просто текстовым файлом. Он не имеет toobe, созданного на основе компьютера hello где hello будет в конечном счете использоваться сертификат. Несмотря на то, что этот документ предназначен для приложения службы, создания CSR hello является универсальной и применяется также для облачных служб.
