---
title: "Обзор шаблона лицензий PlayReady служб aaaMedia"
description: "В этом разделе приводится обзор шаблона лицензий PlayReady, который используется tooconfigure лицензии PlayReady."
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
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="e9ecd-103">Обзор шаблонов лицензий PlayReady служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="e9ecd-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="e9ecd-104">Службы мультимедиа Azure теперь обеспечивают доставку лицензий Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="e9ecd-105">Когда hello проигрывателя конечного пользователя (например, Silverlight) пытается tooplay контент, защищенный PlayReady, запрос был отправлен toohello лицензии доставки службы tooobtain лицензию.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="e9ecd-106">Если hello служба лицензий утверждает запрос hello, она выдает лицензии hello отправленных toohello клиента и может быть используется toodecrypt- and -play hello указанным содержимым.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="e9ecd-107">Также службы мультимедиа предоставляют интерфейсы API, которые позволяют настраивать лицензии PlayReady.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="e9ecd-108">Лицензии содержат права hello и ограничения, что требуется для hello tooenforce среда выполнения PlayReady DRM, когда пользователь пытается tooplayback защищенного содержимого.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="e9ecd-109">Ниже приведены некоторые примеры лицензионных ограничений PlayReady, которые вы можете указать.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="e9ecd-110">Hello DateTime, из которого hello лицензия считается действительной.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="e9ecd-111">Здравствуйте, значение даты и времени, после истечения срока действия лицензии hello.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="e9ecd-112">Для toobe лицензии hello сохранены в постоянное хранилище на приветствия клиента.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="e9ecd-113">Постоянные лицензии являются типовыми tooallow автономного воспроизведения содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="e9ecd-114">Hello минимальный уровень безопасности, должен иметь проигрыватель tooplay контента.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="e9ecd-115">Hello выходной уровень защиты для hello выходных элементов управления для видеоконтента.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="e9ecd-116">Дополнительные сведения см элементы вывода hello статьи (3.5) в hello [правила соответствия PlayReady](https://www.microsoft.com/playready/licensing/compliance/) документа.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="e9ecd-117">В настоящее время можно настроить только PlayRight лицензии PlayReady hello (это право является обязательным) hello.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="e9ecd-118">Hello PlayRight предоставляет клиента hello hello возможность tooplayback hello содержимого.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="e9ecd-119">Hello PlayRight также позволяет настраивать tooplayback определенные ограничения.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="e9ecd-120">Дополнительные сведения см. в разделе [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="e9ecd-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="e9ecd-121">лицензии PlayReady tooconfigure с помощью служб мультимедиа, необходимо настроить шаблон лицензии PlayReady служб мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="e9ecd-122">Hello шаблон определен в XML.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-122">hello template is defined in XML.</span></span>

<span data-ttu-id="e9ecd-123">Hello пример hello простой (и самый распространенный) шаблон, который настраивает базовую лицензию потокового воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="e9ecd-124">С этой лицензией клиентов будет доступ tooplayback контент, защищенный PlayReady.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

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

<span data-ttu-id="e9ecd-125">Hello XML соответствует toohello PlayReady схема XML шаблонов лицензий определенные в шаблоне лицензии PlayReady hello раздела схемы XML.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="e9ecd-126">Службы мультимедиа также определяют набор классов .NET, которые могут использоваться tooserialized и десериализованный tooand из hello XML.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="e9ecd-127">Описание основных классов .NET служб мультимедиа см. [здесь](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="e9ecd-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="e9ecd-128">которые используется tooconfigure шаблонов лицензий.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="e9ecd-129">Пример начала до конца, в котором используется платформа .NET классов шаблон лицензии PlayReady hello tooconfigure см. в разделе [с помощью динамического шифрования PlayReady и службы доставки лицензий](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="e9ecd-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="e9ecd-130"><a id="classes"></a>Классы .NET служб мультимедиа, которые являются tooconfigure используемых шаблонов лицензий</span><span class="sxs-lookup"><span data-stu-id="e9ecd-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="e9ecd-131">Hello ниже приведены основные классы .NET hello используется tooconfigure шаблонов лицензий PlayReady служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="e9ecd-132">Эти классы сопоставлены toohello типы, определенные в [схема XML шаблонов лицензий PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="e9ecd-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="e9ecd-133">Hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) класс используется tooserialize и десериализации tooand из XML шаблонов лицензий служб мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="e9ecd-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="e9ecd-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="e9ecd-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -этот класс представляет шаблон hello для hello ответ отправлен назад toohello конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="e9ecd-136">Он содержит поле для строки пользовательских данных между сервером лицензирования hello и приложения hello (может быть полезным для пользовательской логики приложения), а также список из одного или нескольких шаблонов лицензий.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="e9ecd-137">Это класс «верхнего уровня» hello в иерархии шаблонов hello.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="e9ecd-138">Это означает, что hello шаблон ответа включает список шаблонов лицензий и шаблонов hello лицензий включают (прямо или косвенно) все hello другие классы, которые составляют hello шаблона данных toobe сериализации.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="e9ecd-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="e9ecd-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="e9ecd-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -hello класс представляет шаблон лицензии для создания toobe лицензии PlayReady, возвращается toohello конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="e9ecd-141">Он содержит данные hello на hello ключа контента в лицензии hello и любые права или ограничения toobe обеспечивается средой hello среда выполнения PlayReady DRM при использовании ключа контента hello.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="e9ecd-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="e9ecd-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="e9ecd-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -этот класс представляет PlayRight лицензии PlayReady hello.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="e9ecd-144">Он предоставляет hello пользователя hello возможность tooplayback hello toohello содержимого субъекта ноль или настроить дополнительные ограничения в лицензии hello и hello PlayRight (для воспроизведения определенной политики).</span><span class="sxs-lookup"><span data-stu-id="e9ecd-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="e9ecd-145">Большая часть политики hello на hello PlayRight имеет toodo с выходным ограничениям, которые hello типы выходных данных, которые может воспроизводиться hello содержимого элементов управления и каких-либо ограничений, которые необходимо применить на месте при использовании заданного выходного потока.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="e9ecd-146">Например если параметр DigitalVideoOnlyContentRestriction включен, приветствия затем hello среда выполнения DRM допускает только видео toobe hello отображается через цифровой выход (аналоговые видеосигналы не будут разрешены toopass hello содержимого).</span><span class="sxs-lookup"><span data-stu-id="e9ecd-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9ecd-147">Эти типы ограничений могут быть очень полезны, но могут также влиять на возможности использования hello.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="e9ecd-148">Если hello выходные средства защиты настроены слишком строго, hello контент будет невозможно воспроизвести на некоторых клиентах.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="e9ecd-149">Дополнительные сведения см. в разделе hello [правила соответствия PlayReady](https://www.microsoft.com/playready/licensing/compliance/) документа.</span><span class="sxs-lookup"><span data-stu-id="e9ecd-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="e9ecd-150">Пример уровней защиты, которые поддерживает Silverlight, см. [здесь](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="e9ecd-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="e9ecd-151"><a id="schema"></a>XML-схема шаблона лицензий PlayReady</span><span class="sxs-lookup"><span data-stu-id="e9ecd-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="e9ecd-152">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="e9ecd-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e9ecd-153">Отзывы</span><span class="sxs-lookup"><span data-stu-id="e9ecd-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

