---
title: "Добавление сертификата в хранилище центра сертификации Java | Документация Майкрософт"
description: "Узнайте, как добавить сертификат центра сертификации (ЦС) в хранилище сертификатов (cacerts) центра сертификации Java для службы Twilio или Azure Service Bus."
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
ms.openlocfilehash: 4f3ec837588c6e959e82108ca25ab4289e40d3f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="adding-a-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="5fa47-103">Добавление сертификата в хранилище сертификатов ЦС Java</span><span class="sxs-lookup"><span data-stu-id="5fa47-103">Adding a Certificate to the Java CA Certificates Store</span></span>
<span data-ttu-id="5fa47-104">Ниже показано, как добавить сертификат центра сертификации (ЦС) в хранилище сертификатов (cacerts) центра сертификации Java.</span><span class="sxs-lookup"><span data-stu-id="5fa47-104">The following steps show you how to add a certificate authority (CA) certificate to the Java CA certificate (cacerts) store.</span></span> <span data-ttu-id="5fa47-105">Приведен пример использования сертификата ЦС, требуемого службой Twilio.</span><span class="sxs-lookup"><span data-stu-id="5fa47-105">The example used is for the CA certificate required by the Twilio service.</span></span> <span data-ttu-id="5fa47-106">Ниже в этой статье описана установка сертификата ЦС для шины обслуживания Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa47-106">Information provided later in the topic describes how to install the CA certificate for the Azure Service Bus.</span></span> 

<span data-ttu-id="5fa47-107">Чтобы добавить сертификат ЦС перед сжатием JDK и добавлением его в папку **approot** проекта Azure, можно использовать keytool или выполнить задачу запуска Azure, которая использует keytool для добавления сертификата.</span><span class="sxs-lookup"><span data-stu-id="5fa47-107">You can use keytool to add the CA certificate prior to zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span> <span data-ttu-id="5fa47-108">В этом примере предполагается, что сертификат ЦС будет добавлен перед сжатием JDK.</span><span class="sxs-lookup"><span data-stu-id="5fa47-108">This example assumes you will add a CA certificate prior to the JDK being zipped.</span></span> <span data-ttu-id="5fa47-109">Также в примере будет использоваться конкретный сертификат ЦС, но действия, необходимые для получения различных сертификатов центра сертификации и их импорта в хранилище cacerts, будут такими же.</span><span class="sxs-lookup"><span data-stu-id="5fa47-109">Also, a specific CA certificate will be used in the example, but the steps of obtaining a different CA certificate and importing it into the cacerts store would be similar.</span></span>

## <a name="to-add-a-certificate-to-the-cacerts-store"></a><span data-ttu-id="5fa47-110">Добавление сертификата в хранилище cacerts</span><span class="sxs-lookup"><span data-stu-id="5fa47-110">To add a certificate to the cacerts store</span></span>
1. <span data-ttu-id="5fa47-111">В командной строке для папки JDK **jdk\jre\lib\security** выполните следующий код, чтобы узнать, какие сертификаты установлены:</span><span class="sxs-lookup"><span data-stu-id="5fa47-111">At a command prompt that is set to your JDK's **jdk\jre\lib\security** folder, run the following to see what certificates are installed:</span></span>
   
    `keytool -list -keystore cacerts`
   
    <span data-ttu-id="5fa47-112">Вам будет предложено ввести пароль хранилища.</span><span class="sxs-lookup"><span data-stu-id="5fa47-112">You'll be prompted for the store password.</span></span> <span data-ttu-id="5fa47-113">Пароль по умолчанию — **changeit**.</span><span class="sxs-lookup"><span data-stu-id="5fa47-113">The default password is **changeit**.</span></span> <span data-ttu-id="5fa47-114">(Сведения о том, как изменить пароль, см. в документации по keytool на странице <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) В этом примере предполагается, что сертификат с MD5 устройства отпечатков пальцев 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 отсутствует в списке и вы хотите его импортировать (этот конкретный сертификат необходим для службы API Twilio).</span><span class="sxs-lookup"><span data-stu-id="5fa47-114">(If you want to change the password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) This example assumes that the certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 is not listed, and that you want to import it (this particular certificate is needed by the Twilio API service).</span></span>
2. <span data-ttu-id="5fa47-115">Получение сертификата из списка сертификатов, перечисленных в [корневых сертификатах GeoTrust](http://www.geotrust.com/resources/root-certificates/).</span><span class="sxs-lookup"><span data-stu-id="5fa47-115">Obtain the certificate from the list of certificates listed at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span> <span data-ttu-id="5fa47-116">Щелкните правой кнопкой мыши ссылку сертификата с серийным номером 35:DE:F4:CF и сохраните его в папке **jdk\jre\lib\security**.</span><span class="sxs-lookup"><span data-stu-id="5fa47-116">Right-click the link for the certificate with serial number 35:DE:F4:CF and save it to the **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="5fa47-117">Для целей этого примера он сохранен в файле с именем **Equifax\_Secure\_Certificate\_Authority.cer**.</span><span class="sxs-lookup"><span data-stu-id="5fa47-117">For purposes of this example, it was saved to a file named **Equifax\_Secure\_Certificate\_Authority.cer**.</span></span>
3. <span data-ttu-id="5fa47-118">Импортируйте сертификат с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="5fa47-118">Import the certificate via the following command:</span></span>
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    <span data-ttu-id="5fa47-119">Если выводится приглашение подтвердить доверие этому сертификату, если сертификат имеет отпечаток пальцев MD5 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, введите **y**.</span><span class="sxs-lookup"><span data-stu-id="5fa47-119">When prompted to trust this certificate, if the certificate has MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, respond by typing **y**.</span></span>
4. <span data-ttu-id="5fa47-120">Выполните следующую команду, чтобы убедиться, что сертификат СЦ был успешно импортирован:</span><span class="sxs-lookup"><span data-stu-id="5fa47-120">Run the following command to ensure the CA certificate has been successfully imported:</span></span>
   
    `keytool -list -keystore cacerts`
5. <span data-ttu-id="5fa47-121">Сожмите JDK и добавьте его в папку **approot** проекта Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa47-121">Zip the JDK and add it to your Azure project's **approot** folder.</span></span>

<span data-ttu-id="5fa47-122">Дополнительные сведения о keytool см. по адресу <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="5fa47-122">For information about keytool, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

## <a name="azure-root-certificates"></a><span data-ttu-id="5fa47-123">Корневые сертификаты Azure</span><span class="sxs-lookup"><span data-stu-id="5fa47-123">Azure Root Certificates</span></span>
<span data-ttu-id="5fa47-124">Приложения, использующие службы Azure (например, Azure Service Bus), должны доверять сертификату Baltimore CyberTrust Root.</span><span class="sxs-lookup"><span data-stu-id="5fa47-124">Your applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust Root certificate.</span></span> <span data-ttu-id="5fa47-125">(С 15 апреля 2013 года Azure начала миграцию с глобальной основы GTE CyberTrust в Baltimore CyberTrust Root.</span><span class="sxs-lookup"><span data-stu-id="5fa47-125">(Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global Root to the Baltimore CyberTrust Root.</span></span> <span data-ttu-id="5fa47-126">Такая миграция продолжается несколько месяцев.)</span><span class="sxs-lookup"><span data-stu-id="5fa47-126">This migration took several months to complete.)</span></span>

<span data-ttu-id="5fa47-127">Сертификат Baltimore может быть установлен в вашем хранилище cacerts, поэтому не забудьте выполнить команду **keytool -list** , чтобы проверить, существует ли он уже.</span><span class="sxs-lookup"><span data-stu-id="5fa47-127">The Baltimore certificate might already be installed in your cacerts store, so remember to run the **keytool -list** command first to see if it already exists.</span></span>

<span data-ttu-id="5fa47-128">Если требуется добавить Baltimore CyberTrust Root, он имеет серийный номер 02:00:00:b9 и отпечаток пальца SHA1 d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span><span class="sxs-lookup"><span data-stu-id="5fa47-128">If you need to add the Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="5fa47-129">Его можно скачать по адресу <https://cacert.omniroot.com/bc2025.crt>, сохранить в локальном файле с расширением **CER**, а затем импортировать с помощью **keytool**, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="5fa47-129">It can be downloaded from <https://cacert.omniroot.com/bc2025.crt>, saved to a local file with extension **.cer**, and then imported using **keytool** as shown above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fa47-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5fa47-130">Next steps</span></span>
<span data-ttu-id="5fa47-131">Дополнительные сведения об используемых в Azure корневых сертификатах см. в записи блога [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx) (Перенос корневых сертификатов Azure).</span><span class="sxs-lookup"><span data-stu-id="5fa47-131">For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="5fa47-132">Дополнительные сведения о Java см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).</span><span class="sxs-lookup"><span data-stu-id="5fa47-132">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

