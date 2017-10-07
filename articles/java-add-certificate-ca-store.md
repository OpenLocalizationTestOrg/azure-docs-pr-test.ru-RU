---
title: "хранилище сертификатов ЦС Java toohello aaaAdd | Документы Microsoft"
description: "Узнайте, как tooadd сертификат центра сертификации (ЦС) сертификат toohello Java сертификат ЦС (cacerts) хранения для Twilio службы или шины обслуживания Azure."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a><span data-ttu-id="ab359-103">Добавление сертификата toohello хранилище сертификатов ЦС Java</span><span class="sxs-lookup"><span data-stu-id="ab359-103">Adding a Certificate toohello Java CA Certificates Store</span></span>
<span data-ttu-id="ab359-104">Здравствуй, следующие шаги показывают, как tooadd сертификат центра сертификации (ЦС) сертификат toohello Java сертификат ЦС (cacerts) хранения.</span><span class="sxs-lookup"><span data-stu-id="ab359-104">hello following steps show you how tooadd a certificate authority (CA) certificate toohello Java CA certificate (cacerts) store.</span></span> <span data-ttu-id="ab359-105">пример Hello используется для сертификата ЦС hello требуется hello Twilio службы.</span><span class="sxs-lookup"><span data-stu-id="ab359-105">hello example used is for hello CA certificate required by hello Twilio service.</span></span> <span data-ttu-id="ab359-106">Далее в разделе hello описываются как hello tooinstall ЦС сертификат для hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ab359-106">Information provided later in hello topic describes how tooinstall hello CA certificate for hello Azure Service Bus.</span></span> 

<span data-ttu-id="ab359-107">JDK и добавив его tooyour проекта Azure можно использовать toozipping предыдущего сертификата ЦС hello tooadd keytool **approot** папки, или может запустить задачу Azure при запуске, которая использует keytool tooadd hello сертификат.</span><span class="sxs-lookup"><span data-stu-id="ab359-107">You can use keytool tooadd hello CA certificate prior toozipping your JDK and adding it tooyour Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool tooadd hello certificate.</span></span> <span data-ttu-id="ab359-108">В этом примере предполагается, что вы добавите предыдущих toohello каталога сертификат ЦС JDK ZIP-архиве.</span><span class="sxs-lookup"><span data-stu-id="ab359-108">This example assumes you will add a CA certificate prior toohello JDK being zipped.</span></span> <span data-ttu-id="ab359-109">Кроме того конкретного сертификата ЦС будет использоваться в примере hello, но hello действия получения другой сертификат ЦС и импортировав их в hello cacerts хранилища будет выглядеть.</span><span class="sxs-lookup"><span data-stu-id="ab359-109">Also, a specific CA certificate will be used in hello example, but hello steps of obtaining a different CA certificate and importing it into hello cacerts store would be similar.</span></span>

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a><span data-ttu-id="ab359-110">сохранить сертификат toohello cacerts tooadd</span><span class="sxs-lookup"><span data-stu-id="ab359-110">tooadd a certificate toohello cacerts store</span></span>
1. <span data-ttu-id="ab359-111">В командной строке, имеет значение tooyour JDK **jdk\jre\lib\security** запуска hello toosee, какие сертификаты установлены следующие папки:</span><span class="sxs-lookup"><span data-stu-id="ab359-111">At a command prompt that is set tooyour JDK's **jdk\jre\lib\security** folder, run hello following toosee what certificates are installed:</span></span>
   
    `keytool -list -keystore cacerts`
   
    <span data-ttu-id="ab359-112">Вам будет выведен для hello хранить пароль.</span><span class="sxs-lookup"><span data-stu-id="ab359-112">You'll be prompted for hello store password.</span></span> <span data-ttu-id="ab359-113">пароль по умолчанию Hello — **changeit**.</span><span class="sxs-lookup"><span data-stu-id="ab359-113">hello default password is **changeit**.</span></span> <span data-ttu-id="ab359-114">(Если требуется пароль toochange hello, см. в документации по keytool hello в <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) В этом примере предполагается hello сертификата с MD5 отпечатков пальцев 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 отсутствует в списке, и что требуется tooimport ИТ (это определенный сертификат требуется hello Twilio API-службы).</span><span class="sxs-lookup"><span data-stu-id="ab359-114">(If you want toochange hello password, see hello keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) This example assumes that hello certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 is not listed, and that you want tooimport it (this particular certificate is needed by hello Twilio API service).</span></span>
2. <span data-ttu-id="ab359-115">Получить сертификат hello hello список сертификатов, перечисленных в [GeoTrust корневые сертификаты](http://www.geotrust.com/resources/root-certificates/).</span><span class="sxs-lookup"><span data-stu-id="ab359-115">Obtain hello certificate from hello list of certificates listed at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span> <span data-ttu-id="ab359-116">Щелкните правой кнопкой мыши ссылку hello для hello сертификат с серийным номером 35:DE:F4:CF и сохраните его toohello **jdk\jre\lib\security** папки.</span><span class="sxs-lookup"><span data-stu-id="ab359-116">Right-click hello link for hello certificate with serial number 35:DE:F4:CF and save it toohello **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="ab359-117">Для этого примера, он был сохранен файл tooa с именем **Equifax\_Secure\_сертификат\_Authority.cer**.</span><span class="sxs-lookup"><span data-stu-id="ab359-117">For purposes of this example, it was saved tooa file named **Equifax\_Secure\_Certificate\_Authority.cer**.</span></span>
3. <span data-ttu-id="ab359-118">Импортируйте сертификат hello через hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ab359-118">Import hello certificate via hello following command:</span></span>
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    <span data-ttu-id="ab359-119">При появлении запроса о tootrust этот сертификат hello сертификат имеет Отпечаток MD5 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 ответ, введя **y**.</span><span class="sxs-lookup"><span data-stu-id="ab359-119">When prompted tootrust this certificate, if hello certificate has MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, respond by typing **y**.</span></span>
4. <span data-ttu-id="ab359-120">Выполнения hello, следующая команда tooensure hello ЦС сертификата успешно импортировано:</span><span class="sxs-lookup"><span data-stu-id="ab359-120">Run hello following command tooensure hello CA certificate has been successfully imported:</span></span>
   
    `keytool -list -keystore cacerts`
5. <span data-ttu-id="ab359-121">ZIP-архив hello JDK и добавить его tooyour проекта Azure в **approot** папки.</span><span class="sxs-lookup"><span data-stu-id="ab359-121">Zip hello JDK and add it tooyour Azure project's **approot** folder.</span></span>

<span data-ttu-id="ab359-122">Дополнительные сведения о keytool см. по адресу <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="ab359-122">For information about keytool, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

## <a name="azure-root-certificates"></a><span data-ttu-id="ab359-123">Корневые сертификаты Azure</span><span class="sxs-lookup"><span data-stu-id="ab359-123">Azure Root Certificates</span></span>
<span data-ttu-id="ab359-124">Приложения, использующие службы Azure (например, Azure Service Bus) требуется сертификат Baltimore CyberTrust Root tootrust hello.</span><span class="sxs-lookup"><span data-stu-id="ab359-124">Your applications that use Azure services (such as Azure Service Bus) need tootrust hello Baltimore CyberTrust Root certificate.</span></span> <span data-ttu-id="ab359-125">(Начиная 15 апреля 2013 г., Azure начала миграции с hello глобальной основы CyberTrust GTE toohello Baltimore CyberTrust Root.</span><span class="sxs-lookup"><span data-stu-id="ab359-125">(Beginning April 15, 2013, Azure began migrating from hello GTE CyberTrust Global Root toohello Baltimore CyberTrust Root.</span></span> <span data-ttu-id="ab359-126">Эта миграция заняла toocomplete несколько месяцев).</span><span class="sxs-lookup"><span data-stu-id="ab359-126">This migration took several months toocomplete.)</span></span>

<span data-ttu-id="ab359-127">Hello Baltimore сертификатов могут быть уже установлены в хранилище cacerts, поэтому необходимо учитывать toorun hello **keytool-список** команды первого toosee, если он уже существует.</span><span class="sxs-lookup"><span data-stu-id="ab359-127">hello Baltimore certificate might already be installed in your cacerts store, so remember toorun hello **keytool -list** command first toosee if it already exists.</span></span>

<span data-ttu-id="ab359-128">Если вам требуется tooadd hello Baltimore CyberTrust Root, она имеет 02:00:00:b9 серийный номер и c d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 отпечаток SHA1: 78:db:28:52:ca:e4:74.</span><span class="sxs-lookup"><span data-stu-id="ab359-128">If you need tooadd hello Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="ab359-129">Ее можно загрузить из <https://cacert.omniroot.com/bc2025.crt>, сохраняемый tooa локальный файл с расширением **CER-файл**, а затем импортировать с помощью **keytool** как показано выше.</span><span class="sxs-lookup"><span data-stu-id="ab359-129">It can be downloaded from <https://cacert.omniroot.com/bc2025.crt>, saved tooa local file with extension **.cer**, and then imported using **keytool** as shown above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab359-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab359-130">Next steps</span></span>
<span data-ttu-id="ab359-131">Дополнительные сведения о hello корневые сертификаты, используемые в Azure см. в разделе [Azure корневой сертификат миграции](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab359-131">For more information about hello root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="ab359-132">Дополнительные сведения о Java см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).</span><span class="sxs-lookup"><span data-stu-id="ab359-132">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

