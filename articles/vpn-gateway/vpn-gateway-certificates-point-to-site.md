---
title: "Создание и экспорт сертификатов для подключений типа \"точка-сеть\" в Azure с помощью PowerShell | Документы Майкрософт"
description: "В этой статье содержатся действия toocreate самозаверяющий корневой сертификат, экспортируйте открытый ключ hello и создания сертификатов клиента с помощью PowerShell на Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="ba0a9-103">Создание и экспорт сертификатов для подключений типа "точка-сеть" с помощью PowerShell в Windows 10</span><span class="sxs-lookup"><span data-stu-id="ba0a9-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="ba0a9-104">Точка-сеть соединения используют tooauthenticate сертификаты.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="ba0a9-105">В этой статье показано, как toocreate a самозаверяющий корневой сертификат и создания сертификатов клиента с помощью PowerShell на Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="ba0a9-106">Если вам нужны дополнительные действия по настройке точки сайтами, таких как как список tooupload корневые сертификаты, выберите один из статей hello "Настройка точка-сеть" из hello следующие:</span><span class="sxs-lookup"><span data-stu-id="ba0a9-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba0a9-107">Создание самозаверяющих сертификатов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba0a9-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="ba0a9-108">Создание и экспорт сертификатов для подключений типа "точка — сеть" с помощью MakeCert</span><span class="sxs-lookup"><span data-stu-id="ba0a9-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="ba0a9-109">Настройка подключения "точка — сеть" модели Resource Manager на портале Azure</span><span class="sxs-lookup"><span data-stu-id="ba0a9-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="ba0a9-110">Настройка подключения "точка-сеть" — Resource Manager — PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba0a9-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="ba0a9-111">Настройка подключения "точка —сеть" классической модели на портале Azure</span><span class="sxs-lookup"><span data-stu-id="ba0a9-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="ba0a9-112">В этой статье на компьютере под управлением Windows 10, необходимо выполнить действия hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="ba0a9-113">командлеты PowerShell Hello использовать toogenerate сертификаты являются частью операционной системы Windows 10 hello и не работают в других версиях Windows.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="ba0a9-114">компьютер Hello Windows 10 — только сертификаты, необходимые toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="ba0a9-115">После hello сертификаты создаются, можно загрузить их или установить их на любых поддерживаемых клиентских операционных систем.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="ba0a9-116">Если у вас компьютер Windows 10 tooa доступа, можно использовать [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate сертификаты.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="ba0a9-117">Hello сертификаты, создаваемые с помощью любого метода можно установить на любом [поддерживается](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) клиентской операционной системы.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="ba0a9-118"><a name="rootcert"></a>Создание самозаверяющего корневого сертификата</span><span class="sxs-lookup"><span data-stu-id="ba0a9-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="ba0a9-119">Используйте toocreate командлет New-SelfSignedCertificate hello самозаверяющего корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="ba0a9-120">Дополнительные сведения о параметре см. в разделе [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="ba0a9-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="ba0a9-121">На компьютере под управлением Windows 10 откройте консоль Windows PowerShell с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="ba0a9-122">Используйте следующий пример toocreate hello самозаверяющий корневой сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="ba0a9-123">Hello пример создает самозаверяющий корневой сертификат, с именем «P2SRootCert», который автоматически устанавливается в «Сертификаты — текущий пользователь\личные\сертификаты».</span><span class="sxs-lookup"><span data-stu-id="ba0a9-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="ba0a9-124">Hello сертификата можно просмотреть, открыв *certmgr.msc*, или *Управление сертификатами пользователей*.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="ba0a9-125"><a name="cer"></a>Экспорт hello открытого ключа (CER)</span><span class="sxs-lookup"><span data-stu-id="ba0a9-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="ba0a9-126">Hello exported.cer файл должен быть загруженного tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="ba0a9-127">Дополнительные сведения см. в разделе [Подготовка CER-файла корневого сертификата к передаче](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="ba0a9-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="ba0a9-128">tooadd дополнительных доверенный корневой сертификат [в этом разделе](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) hello статьи.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="ba0a9-129">Экспорт самозаверяющего корневого сертификата hello и открытого ключа toostore его (необязательно)</span><span class="sxs-lookup"><span data-stu-id="ba0a9-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="ba0a9-130">Вы можете tooexport hello самозаверяющий корневой сертификат и безопасно хранить.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="ba0a9-131">При необходимости позднее можно будет установить его на другом компьютере и создать дополнительные сертификаты клиента или экспортировать другой CER-файл.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="ba0a9-132">tooexport hello самозаверяющий корневой сертификат как PFX-файл, выберите hello корневой сертификат или использовать hello же действия, как описано в [Экспорт сертификата клиента](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="ba0a9-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="ba0a9-133"><a name="clientcert"></a>Создание сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="ba0a9-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="ba0a9-134">Каждый клиентский компьютер, который подключается tooa виртуальной сети с помощью точка-сайт должен иметь установленный сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="ba0a9-135">Создайте сертификат клиента из hello самозаверяющий корневой сертификат и затем экспортировать и установите сертификат клиента hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="ba0a9-136">Если сертификат клиента hello не установлен, не пройдет проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="ba0a9-137">Hello следующие шаги описывают создание клиентский сертификат из самозаверяющего корневого сертификата.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="ba0a9-138">Можно создать несколько сертификатов из hello выдачи корневых сертификатов.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="ba0a9-139">При создании клиентских сертификатов, используя приведенные ниже действия hello hello сертификат клиента автоматически устанавливается на компьютере hello использования сертификата toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="ba0a9-140">Если требуется tooinstall сертификата клиента на другой компьютер, можно экспортировать сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="ba0a9-141">Hello примерах используется toogenerate командлет New-SelfSignedCertificate hello сертификат клиента, срок действия истекает через один год.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="ba0a9-142">Дополнительные сведения о параметре, например установку другой срок для сертификата клиента hello, в разделе [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="ba0a9-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="ba0a9-143">Пример 1</span><span class="sxs-lookup"><span data-stu-id="ba0a9-143">Example 1</span></span>

<span data-ttu-id="ba0a9-144">В этом примере используется переменная «$cert» hello в предыдущем разделе объявлена hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="ba0a9-145">Если консоль PowerShell hello закрыто, после создания hello самозаверяющий корневой сертификат или создаете дополнительные клиентские сертификаты в новом сеансе консоли PowerShell, выполните шаги hello в [пример 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="ba0a9-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="ba0a9-146">Изменения и выполнения toogenerate пример hello сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="ba0a9-147">При запуске hello следующий пример без изменения его результат hello — сертификат клиента с именем «P2SChildCert».</span><span class="sxs-lookup"><span data-stu-id="ba0a9-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="ba0a9-148">Tooname hello дочерний сертификат либо другие, измените значение CN hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="ba0a9-149">Не изменяйте hello TextExtension при запуске данного примера.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="ba0a9-150">Hello сертификат клиента, который создается автоматически устанавливается в «Сертификаты — текущий пользователь\личные\сертификаты» на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="ba0a9-151"><a name="ex2"></a>Пример 2</span><span class="sxs-lookup"><span data-stu-id="ba0a9-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="ba0a9-152">При создании дополнительных клиентских сертификатов, или не используя hello же сеанс PowerShell, используемые toocreate самозаверяющий корневой сертификат, используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ba0a9-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="ba0a9-153">Определите hello самозаверяющего корневого сертификата, установленного на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="ba0a9-154">Этот командлет возвращает список сертификатов, установленных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="ba0a9-155">Найдите имя субъекта hello hello возвращается список, а затем копировать hello отпечаток, найти следующее вхождение текста tooa tooit файл.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="ba0a9-156">В следующем примере hello существует два сертификата.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="ba0a9-157">Hello CN-имя — имя hello hello самозаверяющего корневого сертификата, из которого нужно toogenerate дочерний сертификат.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="ba0a9-158">В данном случае это P2SRootCert.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="ba0a9-159">Объявите переменную для hello корневого сертификата, с помощью отпечатка hello из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="ba0a9-160">Замените ОТПЕЧАТОК отпечаток hello hello корневого сертификата, из которого нужно toogenerate дочерний сертификат.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="ba0a9-161">Например переменная hello с помощью отпечатка hello для P2SRootCert в предыдущем шаге hello, выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ba0a9-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="ba0a9-162">Изменения и выполнения toogenerate пример hello сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="ba0a9-163">При запуске hello следующий пример без изменения его результат hello — сертификат клиента с именем «P2SChildCert».</span><span class="sxs-lookup"><span data-stu-id="ba0a9-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="ba0a9-164">Tooname hello дочерний сертификат либо другие, измените значение CN hello.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="ba0a9-165">Не изменяйте hello TextExtension при запуске данного примера.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="ba0a9-166">Hello сертификат клиента, который создается автоматически устанавливается в «Сертификаты — текущий пользователь\личные\сертификаты» на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ba0a9-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="ba0a9-167"><a name="clientexport"></a>Экспорт сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="ba0a9-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="ba0a9-168"><a name="install"></a>Установка экспортированного сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="ba0a9-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ba0a9-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba0a9-169">Next steps</span></span>

<span data-ttu-id="ba0a9-170">Продолжайте настраивать параметры конфигурации типа "точка-сеть".</span><span class="sxs-lookup"><span data-stu-id="ba0a9-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="ba0a9-171">Для **диспетчера ресурсов** модели шагов развертывания см. в разделе [Настройка tooa подключение точка-сайт виртуальной сети](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba0a9-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="ba0a9-172">Для **классический** модели шагов развертывания см. в разделе [Настройка tooa подключение точка-сеть VPN виртуальной сети (классические)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba0a9-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
