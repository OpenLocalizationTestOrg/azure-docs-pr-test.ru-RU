---
title: "Обзор шаблонов лицензий PlayReady служб мультимедиа"
description: "В этом разделе содержится обзор шаблонов лицензий PlayReady, которые используются для настройки лицензий PlayReady."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: be19f616e36916655390cd05e738e93c08dcdf68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="363db-103">Обзор шаблонов лицензий PlayReady служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="363db-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="363db-104">Службы мультимедиа Azure теперь обеспечивают доставку лицензий Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="363db-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="363db-105">Когда проигрыватель конечного пользователя (например, Silverlight) пытается воспроизвести содержимое, защищенное с помощью PlayReady, в службу доставки лицензий отправляется запрос на получение лицензии.</span><span class="sxs-lookup"><span data-stu-id="363db-105">When the end user player (for example, Silverlight) tries to play your PlayReady protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="363db-106">Если служба лицензий утверждает запрос, она выдает лицензию, которая отправляется клиенту и может использоваться для расшифровки и воспроизведения указанного содержимого.</span><span class="sxs-lookup"><span data-stu-id="363db-106">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="363db-107">Также службы мультимедиа предоставляют интерфейсы API, которые позволяют настраивать лицензии PlayReady.</span><span class="sxs-lookup"><span data-stu-id="363db-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="363db-108">Лицензии определяют права и ограничения, которые должны применяться в среде выполнения PlayReady DRM при попытке пользователя воспроизвести защищенное содержимое.</span><span class="sxs-lookup"><span data-stu-id="363db-108">Licenses contain the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to playback protected content.</span></span>
<span data-ttu-id="363db-109">Ниже приведены некоторые примеры лицензионных ограничений PlayReady, которые вы можете указать.</span><span class="sxs-lookup"><span data-stu-id="363db-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="363db-110">Значение даты и времени (DateTime) начала действия лицензии.</span><span class="sxs-lookup"><span data-stu-id="363db-110">The DateTime from which the license is valid.</span></span>
* <span data-ttu-id="363db-111">Значение даты и времени (DateTime) окончания действия лицензии.</span><span class="sxs-lookup"><span data-stu-id="363db-111">The DateTime value when the license expires.</span></span> 
* <span data-ttu-id="363db-112">Для лицензии, которая будет храниться в постоянном хранилище на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="363db-112">For the license to be saved in persistent storage on the client.</span></span> <span data-ttu-id="363db-113">Постоянные лицензии обычно используются для разрешения автономного воспроизведения содержимого.</span><span class="sxs-lookup"><span data-stu-id="363db-113">Persistent licenses are typically used to allow offline playback of the content.</span></span>
* <span data-ttu-id="363db-114">Минимальный уровень безопасности, необходимый для воспроизведения содержимого проигрывателем.</span><span class="sxs-lookup"><span data-stu-id="363db-114">The minimum security level that a player must have to play your content.</span></span> 
* <span data-ttu-id="363db-115">Уровень защиты выходных данных для элементов управления выводом аудио- или видеосодержимого.</span><span class="sxs-lookup"><span data-stu-id="363db-115">The output protection level for the output controls for audio\video content.</span></span> 
* <span data-ttu-id="363db-116">Дополнительные сведения см. в разделе "Элементы управления выходными данными" (3.5) в [правилах соответствия PlayReady](https://www.microsoft.com/playready/licensing/compliance/).</span><span class="sxs-lookup"><span data-stu-id="363db-116">For more information, see the Output Controls section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="363db-117">В настоящее время можно настроить только право PlayRight лицензии PlayReady (это право является обязательным).</span><span class="sxs-lookup"><span data-stu-id="363db-117">Currently, you can only configure the PlayRight of the PlayReady license (this right is required).</span></span> <span data-ttu-id="363db-118">Право PlayRight дает клиенту возможность воспроизводить содержимое.</span><span class="sxs-lookup"><span data-stu-id="363db-118">The PlayRight gives the client the ability to playback the content.</span></span> <span data-ttu-id="363db-119">Также PlayRight позволяет настраивать ограничения, касающиеся воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="363db-119">The PlayRight also allows configuring restrictions specific to playback.</span></span> <span data-ttu-id="363db-120">Дополнительные сведения см. в разделе [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="363db-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="363db-121">Чтобы настроить лицензии PlayReady с помощью служб мультимедиа, необходимо настроить шаблон лицензии PlayReady служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="363db-121">To configure PlayReady licenses using Media Services, you must configure the Media Services PlayReady license template.</span></span> <span data-ttu-id="363db-122">Шаблон определяется в XML-коде.</span><span class="sxs-lookup"><span data-stu-id="363db-122">The template is defined in XML.</span></span>

<span data-ttu-id="363db-123">В следующем примере показан самый простой (и наиболее распространенный) шаблон, который позволяет настроить базовую лицензию на потоковую передачу.</span><span class="sxs-lookup"><span data-stu-id="363db-123">The following example shows the simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="363db-124">С этой лицензией клиенты могут воспроизводить защищенное содержимое PlayReady.</span><span class="sxs-lookup"><span data-stu-id="363db-124">With this license, your clients would be able to playback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="363db-125">XML-код соответствует XML-схеме шаблона лицензий PlayReady, определенной в разделе XML-схемы шаблона лицензий PlayReady.</span><span class="sxs-lookup"><span data-stu-id="363db-125">The XML conforms to the PlayReady license template XML schema defined in the PlayReady license template XML schema section.</span></span>

<span data-ttu-id="363db-126">Службы мультимедиа также определяют набор классов .NET, которые могут использоваться для сериализации в XML и десериализации из XML.</span><span class="sxs-lookup"><span data-stu-id="363db-126">Media Services also defines a set of .NET classes that could be used to serialized and deserialized to and from the XML.</span></span> <span data-ttu-id="363db-127">Описание основных классов .NET служб мультимедиа см. [здесь](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="363db-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="363db-128">Эти классы используются для настройки шаблонов лицензий.</span><span class="sxs-lookup"><span data-stu-id="363db-128">that are used to configure license templates.</span></span>

<span data-ttu-id="363db-129">Комплексный пример использования классов .NET для настройки шаблона лицензии PlayReady см. в статье [Использование общего динамического шифрования PlayReady и (или) Widevine DRM](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="363db-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="363db-130"><a id="classes"></a>Классы .NET служб мультимедиа, используемые для настройки шаблонов лицензий</span><span class="sxs-lookup"><span data-stu-id="363db-130"><a id="classes"></a>Media Services .NET classes that are used to configure license templates</span></span>
<span data-ttu-id="363db-131">Ниже перечислены основные классы .NET, которые используются для настройки шаблонов лицензий PlayReady служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="363db-131">The following are the main .NET classes are used to configure Media Services PlayReady license templates.</span></span> <span data-ttu-id="363db-132">Эти классы сопоставляются с типами, определенными в [XML-схеме шаблона лицензий PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="363db-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="363db-133">Класс [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) используется для сериализации шаблона лицензии служб мультимедиа в XML-код и десериализации из XML-кода.</span><span class="sxs-lookup"><span data-stu-id="363db-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="363db-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="363db-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="363db-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) — этот класс представляет шаблон для ответа, отправляемого конечному пользователю.</span><span class="sxs-lookup"><span data-stu-id="363db-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents the template for the response sent back to the end user.</span></span> <span data-ttu-id="363db-136">Он содержит поле для строки пользовательских данных, используемых сервером лицензий и приложением (может быть полезно для настраиваемой логики приложения), а также список из одного или нескольких шаблонов лицензий.</span><span class="sxs-lookup"><span data-stu-id="363db-136">It contains a field for a custom data string between the license server and the application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="363db-137">Это класс верхнего уровня в иерархии шаблонов.</span><span class="sxs-lookup"><span data-stu-id="363db-137">This is the “top level” class in the template hierarchy.</span></span> <span data-ttu-id="363db-138">Это означает, что шаблон ответа включает список шаблонов лицензий, а шаблоны лицензий содержат (напрямую или косвенно) все прочие классы, составляющие сериализуемый шаблон данных.</span><span class="sxs-lookup"><span data-stu-id="363db-138">Meaning that the response template includes a list of license templates and the license templates include (directly or indirectly) all of the other classes that make up the template data to be serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="363db-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="363db-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="363db-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) — этот класс представляет шаблон лицензии для создания лицензий PlayReady, которые будут возвращены конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="363db-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - The class represents a license template for creating PlayReady licenses to be returned to the end users.</span></span> <span data-ttu-id="363db-141">Он содержит данные о ключе содержимого в лицензии и возможные права или ограничения, которые должны применяться средой выполнения DRM PlayReady при использовании данного ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="363db-141">It contains the data on the content key in the license and any rights or restrictions to be enforced by the PlayReady DRM runtime when using the content key.</span></span>

### <span data-ttu-id="363db-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="363db-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="363db-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) — этот класс представляет право PlayRight лицензии PlayReady.</span><span class="sxs-lookup"><span data-stu-id="363db-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents the PlayRight of a PlayReady license.</span></span> <span data-ttu-id="363db-144">Он предоставляет пользователю возможность воспроизводить содержимое с ограничениями и без, что указано в лицензии и самом праве PlayRight (для политики, касающейся воспроизведения).</span><span class="sxs-lookup"><span data-stu-id="363db-144">It grants the user the ability to playback the content subject to the zero or more restrictions configured in the license and on the PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="363db-145">Большая часть политики в PlayRight связана с ограничениями выходных данных. Эти ограничения определяют типы выходных данных, в формате которых возможно воспроизведение содержимого. А также возможные ограничения, которые должны быть установлены при использовании заданных выходных данных.</span><span class="sxs-lookup"><span data-stu-id="363db-145">Much of the policy on the PlayRight has to do with output restrictions which control the types of outputs that the content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="363db-146">Например, если включено ограничение DigitalVideoOnlyContentRestriction, среда выполнения DRM будет разрешать отображение видео только через цифровые выходы (на аналоговые видеовыходы содержимое нельзя будет передавать).</span><span class="sxs-lookup"><span data-stu-id="363db-146">For example, if the DigitalVideoOnlyContentRestriction is enabled, then the DRM runtime will only allow the video to be displayed over digital outputs (analog video outputs won’t be allowed to pass the content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="363db-147">Эти типы ограничений могут быть очень мощными, но также могут негативно влиять на возможности, доступные для пользователя.</span><span class="sxs-lookup"><span data-stu-id="363db-147">These types of restrictions can be very powerful but can also affect the consumer experience.</span></span> <span data-ttu-id="363db-148">Если указаны слишком строгие правила защиты выходных данных, содержимое может не воспроизводиться на некоторых клиентах.</span><span class="sxs-lookup"><span data-stu-id="363db-148">If the output protections are configured too restrictive, the content might be unplayable on some clients.</span></span> <span data-ttu-id="363db-149">Дополнительные сведения см. [в правилах соответствия PlayReady](https://www.microsoft.com/playready/licensing/compliance/).</span><span class="sxs-lookup"><span data-stu-id="363db-149">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="363db-150">Пример уровней защиты, которые поддерживает Silverlight, см. [здесь](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="363db-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="363db-151"><a id="schema"></a>XML-схема шаблона лицензий PlayReady</span><span class="sxs-lookup"><span data-stu-id="363db-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="363db-152">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="363db-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="363db-153">Отзывы</span><span class="sxs-lookup"><span data-stu-id="363db-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

