---
title: "aaaHow toogenerate и передача ключей, защищенных HSM для хранилища ключей Azure | Документы Microsoft"
description: "Используйте этот toohelp статьи для планирования, создания и затем перенести собственные ключей, защищенных HSM toouse с хранилищем ключей Azure. Также известные как собственные ключи или BYOK."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="562e3-104">Как toogenerate и передача ключей, защищенных HSM для хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="562e3-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="562e3-105">Введение</span><span class="sxs-lookup"><span data-stu-id="562e3-105">Introduction</span></span>
<span data-ttu-id="562e3-106">При использовании хранилища ключей Azure, для повышения надежности можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM), никогда не покидают границ HSM hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="562e3-107">Этот сценарий часто является ссылка tooas *Используй свой ключ*, или BYOK.</span><span class="sxs-lookup"><span data-stu-id="562e3-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="562e3-108">Hello аппаратные модули безопасности являются FIPS 140-2 уровня 2 проверки.</span><span class="sxs-lookup"><span data-stu-id="562e3-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="562e3-109">Хранилище ключей Azure использует семейство Thales nShield HSM tooprotect ключей.</span><span class="sxs-lookup"><span data-stu-id="562e3-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="562e3-110">Используйте hello сведения в этой статье toohelp планирования, создания и затем перенести собственные ключей, защищенных HSM toouse с хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="562e3-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="562e3-111">Эта функция недоступна для Китая.</span><span class="sxs-lookup"><span data-stu-id="562e3-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="562e3-112">Дополнительные сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="562e3-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="562e3-113">Указания по началу работы, включая создание хранилища для ключей, защищенных аппаратным модулем безопасности, см. в статье [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="562e3-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="562e3-114">Дополнительные сведения о создании и передаче Перенос аппаратно защищенного ключа по Интернету hello:</span><span class="sxs-lookup"><span data-stu-id="562e3-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="562e3-115">Вы создаете ключ hello рабочую станцию вне сети, что снижает уязвимость hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="562e3-116">Hello ключ шифруется с помощью ключа обмена ключ Ключами, который остается зашифрованным, пока он не переносятся toohello HSM хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="562e3-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="562e3-117">Hello только зашифрованная версия ключа покидает исходную рабочую станцию hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="562e3-118">Hello набор средств задает свойства ключа клиента, который привязывает вашего ключа toohello системы безопасности хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="562e3-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="562e3-119">Поэтому после HSM хранилища ключей Azure hello получат и расшифруют ключ, только эти аппаратные модули безопасности смогут использовать его.</span><span class="sxs-lookup"><span data-stu-id="562e3-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="562e3-120">Экспортировать ключ нельзя.</span><span class="sxs-lookup"><span data-stu-id="562e3-120">Your key cannot be exported.</span></span> <span data-ttu-id="562e3-121">Эта привязка применяется hello аппаратные модули безопасности Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="562e3-122">Hello обмена ключ (Ключами), используемые tooencrypt ваш ключ создается в HSM хранилища ключей Azure hello и не может быть экспортирован.</span><span class="sxs-lookup"><span data-stu-id="562e3-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="562e3-123">Hello аппаратные модули безопасности принудительно, что может быть не точной версии hello ключа обмена Ключами вне hello аппаратные модули безопасности.</span><span class="sxs-lookup"><span data-stu-id="562e3-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="562e3-124">Кроме того hello набор средств включает аттестацию Thales, hello ключа обмена Ключами не может быть экспортирован и был создан в подлинном аппаратном модуле безопасности, изготовленным Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="562e3-125">Hello набор средств включает аттестацию Thales, hello world безопасности также была создана в подлинном аппаратном модуле безопасности, изготовленном Thales хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="562e3-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="562e3-126">Это аттестации доказывает tooyou, что корпорация Майкрософт использует подлинное оборудование.</span><span class="sxs-lookup"><span data-stu-id="562e3-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="562e3-127">Корпорация Майкрософт применяет отдельные ключи шифрования ключей, а также отдельные системы безопасности в каждом географическом регионе.</span><span class="sxs-lookup"><span data-stu-id="562e3-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="562e3-128">Такое разделение гарантирует, что ключ можно использовать только в центрах обработки данных в регионе hello, в котором он зашифрован.</span><span class="sxs-lookup"><span data-stu-id="562e3-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="562e3-129">Например, ключ европейского клиента нельзя использовать в центрах обработки данных в Северной Америке или Азии.</span><span class="sxs-lookup"><span data-stu-id="562e3-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="562e3-130">Дополнительные сведения об аппаратных модулях безопасности Thales и службах Майкрософт</span><span class="sxs-lookup"><span data-stu-id="562e3-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="562e3-131">Thales e-Security является ведущий глобальный поставщик шифрование данных и кибер безопасности решений toohello финансовых услуг, высоких технологий, производства, государственных организаций и секторов технологии.</span><span class="sxs-lookup"><span data-stu-id="562e3-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="562e3-132">40-летнем опыте защиты корпоративной и государственной информации 4 hello пяти крупнейших энергетических и аэрокосмическое оборудование компаний при использовании решения Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="562e3-133">Эти решения также используются в 22 странах НАТО и защищают более 80 процентов платежных транзакций по всему миру.</span><span class="sxs-lookup"><span data-stu-id="562e3-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="562e3-134">Майкрософт сотрудничает с Thales tooenhance hello технического развития аппаратных модулей безопасности.</span><span class="sxs-lookup"><span data-stu-id="562e3-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="562e3-135">Эти улучшения позволяют tooget hello стандартные преимущества размещаемых служб, не уменьшая контроль над ключами.</span><span class="sxs-lookup"><span data-stu-id="562e3-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="562e3-136">В частности эти усовершенствования позволят корпорации Майкрософт управлять hello аппаратные модули безопасности, чтобы не нужно.</span><span class="sxs-lookup"><span data-stu-id="562e3-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="562e3-137">Как облако, хранилище ключей service, Azure легко масштабируется в краткое уведомление toomeet резко возрастает использования вашей организации.</span><span class="sxs-lookup"><span data-stu-id="562e3-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="562e3-138">AT hello же время ваш ключ защищен аппаратными модулями безопасности корпорации Майкрософт: вы получаете контроль над жизненным циклом ключа hello, так как создание ключа hello и передать его в tooMicrosoft аппаратные модули безопасности.</span><span class="sxs-lookup"><span data-stu-id="562e3-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="562e3-139">Реализация сценария BYOK для хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="562e3-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="562e3-140">Hello используйте следующие сведения и процедуры, если будет создавать Перенос аппаратно защищенного ключа, а затем перенести tooAzure хранилище ключей — hello перевести сценарию ключа (BYOK).</span><span class="sxs-lookup"><span data-stu-id="562e3-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="562e3-141">Предварительные требования для BYOK</span><span class="sxs-lookup"><span data-stu-id="562e3-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="562e3-142">См. в следующей таблице список предварительных требований для hello личной передачи собственного ключа (BYOK) для хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="562e3-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="562e3-143">Требование</span><span class="sxs-lookup"><span data-stu-id="562e3-143">Requirement</span></span> | <span data-ttu-id="562e3-144">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="562e3-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="562e3-145">TooAzure подписки</span><span class="sxs-lookup"><span data-stu-id="562e3-145">A subscription tooAzure</span></span> |<span data-ttu-id="562e3-146">toocreate хранилище ключей Azure, необходимо получить подписку Azure: [Подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="562e3-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="562e3-147">Здравствуйте, хранилище ключей Azure Premium службы уровня toosupport ключей, защищенных HSM</span><span class="sxs-lookup"><span data-stu-id="562e3-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="562e3-148">Дополнительные сведения об уровнях обслуживания hello и возможностях для хранилища ключей Azure см. в разделе hello [цены на хранилище ключей Azure](https://azure.microsoft.com/pricing/details/key-vault/) веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="562e3-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="562e3-149">Аппаратный модуль безопасности Thales, смарт-карты и программное обеспечение поддержки</span><span class="sxs-lookup"><span data-stu-id="562e3-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="562e3-150">Необходимо иметь доступ к tooa аппаратный модуль безопасности Thales и базовые знания о аппаратные модули безопасности Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="562e3-151">В разделе [аппаратный модуль безопасности Thales](https://www.thales-esecurity.com/msrms/buy) hello список совместимых моделей или toopurchase модуль HSM, если не имеется.</span><span class="sxs-lookup"><span data-stu-id="562e3-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="562e3-152">Здравствуйте, следующие оборудования и программного обеспечения:</span><span class="sxs-lookup"><span data-stu-id="562e3-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="562e3-153">Автономная рабочая станция x64 с операционной системой Windows версии не ниже Windows 7 и программным обеспечением Thales nShield версии не ниже 11.50.</span><span class="sxs-lookup"><span data-stu-id="562e3-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="562e3-154">Если рабочая станция выполняется на ОС Windows 7, [установите Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="562e3-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="562e3-155">На рабочей станции, подключенной toohello Интернета с минимальной операционной системы Windows, Windows 7 и [Azure PowerShell](/powershell/azure/overview) **минимальной версии 1.1.0** установлен.</span><span class="sxs-lookup"><span data-stu-id="562e3-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="562e3-156">USB-накопитель или другое переносное устройство хранения, на котором имеется не менее 16 МБ свободного места.</span><span class="sxs-lookup"><span data-stu-id="562e3-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="562e3-157">По соображениям безопасности рекомендуется первую рабочую станцию, hello не является tooa подключенной сети.</span><span class="sxs-lookup"><span data-stu-id="562e3-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="562e3-158">Однако это не применяется принудительно программным путем.</span><span class="sxs-lookup"><span data-stu-id="562e3-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="562e3-159">Обратите внимание, что в дальнейших инструкциях hello этой рабочей станции рабочей станции ссылка tooas hello отключен.</span><span class="sxs-lookup"><span data-stu-id="562e3-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="562e3-160">Кроме того Если ваш ключ клиента предназначен для производственной сети, рекомендуется использовать вторую, отдельную рабочую станцию toodownload hello набор средств и отправки hello ключ клиента.</span><span class="sxs-lookup"><span data-stu-id="562e3-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="562e3-161">Однако в целях тестирования можно использовать hello рабочую станцию, как первое hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="562e3-162">Обратите внимание, что в hello, следуйте инструкциям, вторая рабочая станция hello ссылка tooas подключенного к Интернету рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="562e3-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="562e3-163">Создание и передача вашего ключа tooAzure HSM хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="562e3-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="562e3-164">Будет использовать следующие пять шагов toogenerate hello и передача вашего ключа tooan HSM хранилища ключей Azure:</span><span class="sxs-lookup"><span data-stu-id="562e3-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="562e3-165">Шаг 1. Подготовка рабочей станции, подключенной к Интернету</span><span class="sxs-lookup"><span data-stu-id="562e3-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="562e3-166">Шаг 2. Подготовка отключенной рабочей станции</span><span class="sxs-lookup"><span data-stu-id="562e3-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="562e3-167">Шаг 3. Создание ключа</span><span class="sxs-lookup"><span data-stu-id="562e3-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="562e3-168">Шаг 4. Подготовка ключа к передаче</span><span class="sxs-lookup"><span data-stu-id="562e3-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="562e3-169">Шаг 5: Передача вашего ключа tooAzure хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="562e3-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="562e3-170">Шаг 1. Подготовка рабочей станции, подключенной к Интернету</span><span class="sxs-lookup"><span data-stu-id="562e3-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="562e3-171">Для первого шага hello следующих процедур на рабочей станции, подключенной toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="562e3-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="562e3-172">Шаг 1.1. Установка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="562e3-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="562e3-173">С компьютера, подключенного к Интернету hello Загрузите и установите модуль Azure PowerShell hello, содержащий toomanage hello командлеты хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="562e3-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="562e3-174">Требуется версия не ниже 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="562e3-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="562e3-175">Инструкции по установке см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="562e3-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="562e3-176">Шаг 1.2. Получение идентификатора подписки Azure</span><span class="sxs-lookup"><span data-stu-id="562e3-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="562e3-177">Запустите сеанс Azure PowerShell и войдите в tooyour учетная запись Azure с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="562e3-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="562e3-178">В hello всплывающем окне браузера введите имя пользователя учетной записи Azure и пароль.</span><span class="sxs-lookup"><span data-stu-id="562e3-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="562e3-179">Затем с помощью hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) команды:</span><span class="sxs-lookup"><span data-stu-id="562e3-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="562e3-180">Hello в выходных данных найдите идентификатор hello для hello подписки, которая будет использоваться для хранилища ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="562e3-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="562e3-181">Этот идентификатор подписки понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="562e3-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="562e3-182">Не закрывайте окно Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="562e3-183">Шаг 1.3: Загрузите набор средств BYOK hello для хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="562e3-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="562e3-184">Go toohello центра загрузки Майкрософт и [скачайте набор средств BYOK для хранилища ключей Azure hello](http://www.microsoft.com/download/details.aspx?id=45345) для географической области или экземпляр Azure.</span><span class="sxs-lookup"><span data-stu-id="562e3-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="562e3-185">Используйте следующие hello сведения tooidentify hello пакета имя toodownload и его соответствующие SHA-256 пакета хэширования:</span><span class="sxs-lookup"><span data-stu-id="562e3-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="562e3-186">**США:**</span><span class="sxs-lookup"><span data-stu-id="562e3-186">**United States:**</span></span>

<span data-ttu-id="562e3-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="562e3-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="562e3-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="562e3-189">**Европа**</span><span class="sxs-lookup"><span data-stu-id="562e3-189">**Europe:**</span></span>

<span data-ttu-id="562e3-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="562e3-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="562e3-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="562e3-192">**Азия**</span><span class="sxs-lookup"><span data-stu-id="562e3-192">**Asia:**</span></span>

<span data-ttu-id="562e3-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="562e3-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="562e3-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="562e3-195">**Латинская Америка**</span><span class="sxs-lookup"><span data-stu-id="562e3-195">**Latin America:**</span></span>

<span data-ttu-id="562e3-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="562e3-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="562e3-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="562e3-198">**Япония**</span><span class="sxs-lookup"><span data-stu-id="562e3-198">**Japan:**</span></span>

<span data-ttu-id="562e3-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="562e3-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="562e3-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="562e3-201">**Корея**</span><span class="sxs-lookup"><span data-stu-id="562e3-201">**Korea:**</span></span>

<span data-ttu-id="562e3-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="562e3-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="562e3-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="562e3-204">**Австралия**</span><span class="sxs-lookup"><span data-stu-id="562e3-204">**Australia:**</span></span>

<span data-ttu-id="562e3-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="562e3-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="562e3-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="562e3-207">**Azure для государственных организаций:**</span><span class="sxs-lookup"><span data-stu-id="562e3-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="562e3-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="562e3-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="562e3-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="562e3-210">**Министерство обороны США**</span><span class="sxs-lookup"><span data-stu-id="562e3-210">**US Government DOD:**</span></span>

<span data-ttu-id="562e3-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="562e3-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="562e3-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="562e3-213">**Канада**</span><span class="sxs-lookup"><span data-stu-id="562e3-213">**Canada:**</span></span>

<span data-ttu-id="562e3-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="562e3-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="562e3-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="562e3-216">**Германия**</span><span class="sxs-lookup"><span data-stu-id="562e3-216">**Germany:**</span></span>

<span data-ttu-id="562e3-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="562e3-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="562e3-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="562e3-219">**Индия**</span><span class="sxs-lookup"><span data-stu-id="562e3-219">**India:**</span></span>

<span data-ttu-id="562e3-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="562e3-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="562e3-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="562e3-222">**Великобритания:**</span><span class="sxs-lookup"><span data-stu-id="562e3-222">**United Kingdom:**</span></span>

<span data-ttu-id="562e3-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="562e3-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="562e3-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="562e3-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="562e3-225">целостность загруженных инструментов BYOK, из сеанса Azure PowerShell, используйте hello hello toovalidate [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="562e3-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="562e3-226">Hello набор включено следующее hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="562e3-227">Пакет ключей обмена ключами с именем, начинающимся с **BYOK-KEK-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="562e3-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="562e3-228">Пакет Security World с именем, начинающимся с **BYOK-SecurityWorld-pkg-**</span><span class="sxs-lookup"><span data-stu-id="562e3-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="562e3-229">Сценарий на Python с именем **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="562e3-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="562e3-230">Исполняемый файл командной строки с именем **KeyTransferRemote.exe** и связанными библиотеками DLL.</span><span class="sxs-lookup"><span data-stu-id="562e3-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="562e3-231">Распространяемый пакет Visual C++ с именем **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="562e3-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="562e3-232">Скопируйте hello пакета tooa USB-накопитель или другое переносное устройство.</span><span class="sxs-lookup"><span data-stu-id="562e3-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="562e3-233">Шаг 2. Подготовка отключенной рабочей станции</span><span class="sxs-lookup"><span data-stu-id="562e3-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="562e3-234">Для выполнения этого шага второй hello следующих процедур на рабочей станции hello, не подключенной tooa сеть (hello Интернета или внутренней сети).</span><span class="sxs-lookup"><span data-stu-id="562e3-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="562e3-235">Шаг 2.1: Подготовка рабочей станции hello отключен с аппаратным модулем безопасности Thales</span><span class="sxs-lookup"><span data-stu-id="562e3-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="562e3-236">Установка hello программное обеспечение поддержки nCipher (Thales) на компьютере Windows, а затем подключите компьютер toothat аппаратный модуль безопасности Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="562e3-237">Убедитесь, что hello средства Thales находятся в вашем пути (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="562e3-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="562e3-238">Например введите ниже hello:</span><span class="sxs-lookup"><span data-stu-id="562e3-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="562e3-239">Дополнительные сведения см. в руководстве пользователя hello, входящий в состав hello аппаратный модуль безопасности Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="562e3-240">Шаг 2.2: Набор средств BYOK установки hello на рабочей станции hello отключен</span><span class="sxs-lookup"><span data-stu-id="562e3-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="562e3-241">Скопируйте пакет набора средств BYOK hello с hello USB-накопитель или другое переносное устройство, а затем hello следующие:</span><span class="sxs-lookup"><span data-stu-id="562e3-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="562e3-242">Извлеките файлы hello из hello загрузки пакета в любую папку.</span><span class="sxs-lookup"><span data-stu-id="562e3-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="562e3-243">Запустите файл vcredist_x64.exe из этой папки.</span><span class="sxs-lookup"><span data-stu-id="562e3-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="562e3-244">Следуйте инструкциям hello toohello установить hello компонентов среды выполнения Visual C++ для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="562e3-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="562e3-245">Шаг 3. Создание ключа</span><span class="sxs-lookup"><span data-stu-id="562e3-245">Step 3: Generate your key</span></span>
<span data-ttu-id="562e3-246">Для выполнения этого шага третий hello следующих процедур на рабочей станции hello отключен.</span><span class="sxs-lookup"><span data-stu-id="562e3-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="562e3-247">toocomplete этот шаг должен быть вашего аппаратного модуля безопасности в режим инициализации.</span><span class="sxs-lookup"><span data-stu-id="562e3-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="562e3-248">Шаг 3.1: Изменение режима too'I hello аппаратный модуль безопасности "</span><span class="sxs-lookup"><span data-stu-id="562e3-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="562e3-249">Если вы используете Thales nShield границы, режим hello toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="562e3-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="562e3-250">Используйте hello режиме кнопка toohighlight hello нужный режим работы.</span><span class="sxs-lookup"><span data-stu-id="562e3-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="562e3-251">2.</span><span class="sxs-lookup"><span data-stu-id="562e3-251">2.</span></span> <span data-ttu-id="562e3-252">Через несколько секунд нажмите и удерживайте кнопку "Сброс" hello несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="562e3-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="562e3-253">При изменении режима hello hello новый режим Индикатор перестанет мигать и остается подсветкой.</span><span class="sxs-lookup"><span data-stu-id="562e3-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="562e3-254">Hello Индикатор состояния может нерегулярно flash на несколько секунд и затем мигает регулярно при готовности устройства hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="562e3-255">В противном случае горит hello устройство остается в текущем режиме hello режимом hello соответствующий Индикатор.</span><span class="sxs-lookup"><span data-stu-id="562e3-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="562e3-256">Шаг 3.2. Создание системы безопасности</span><span class="sxs-lookup"><span data-stu-id="562e3-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="562e3-257">Откройте командную строку и запустите hello программы Thales новой системы.</span><span class="sxs-lookup"><span data-stu-id="562e3-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="562e3-258">Эта программа создает **системы безопасности** файл в каталоге % NFAST_KMDATA%\local\world, который соответствует папке C:\ProgramData\nCipher\Key Management Data\local toohello.</span><span class="sxs-lookup"><span data-stu-id="562e3-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="562e3-259">Можно использовать разные значения для кворума hello, но в нашем примере выполняется запрос tooenter три пустых карты и закрепления для каждой из них.</span><span class="sxs-lookup"><span data-stu-id="562e3-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="562e3-260">После этого любые две карты присвойте системы безопасности toohello полный доступ.</span><span class="sxs-lookup"><span data-stu-id="562e3-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="562e3-261">Эти карты станут hello **набором карт администратора** для hello новой системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="562e3-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="562e3-262">Затем hello следующие:</span><span class="sxs-lookup"><span data-stu-id="562e3-262">Then do hello following:</span></span>

* <span data-ttu-id="562e3-263">Создайте резервную копию файла hello world.</span><span class="sxs-lookup"><span data-stu-id="562e3-263">Back up hello world file.</span></span> <span data-ttu-id="562e3-264">Защитите файл hello world hello карты администратора и их закрепления и убедитесь, что никто имеет toomore доступ, чем к одной карте.</span><span class="sxs-lookup"><span data-stu-id="562e3-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="562e3-265">Шаг 3.3: Изменение режима too'O hello аппаратный модуль безопасности "</span><span class="sxs-lookup"><span data-stu-id="562e3-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="562e3-266">Если вы используете Thales nShield границы, режим hello toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="562e3-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="562e3-267">Используйте hello режиме кнопка toohighlight hello нужный режим работы.</span><span class="sxs-lookup"><span data-stu-id="562e3-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="562e3-268">2.</span><span class="sxs-lookup"><span data-stu-id="562e3-268">2.</span></span> <span data-ttu-id="562e3-269">Через несколько секунд нажмите и удерживайте кнопку "Сброс" hello несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="562e3-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="562e3-270">При изменении режима hello hello новый режим Индикатор перестанет мигать и остается подсветкой.</span><span class="sxs-lookup"><span data-stu-id="562e3-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="562e3-271">Hello Индикатор состояния может нерегулярно flash на несколько секунд и затем мигает регулярно при готовности устройства hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="562e3-272">В противном случае горит hello устройство остается в текущем режиме hello режимом hello соответствующий Индикатор.</span><span class="sxs-lookup"><span data-stu-id="562e3-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="562e3-273">Шаг 3.4: Проверка пакета загружаются hello</span><span class="sxs-lookup"><span data-stu-id="562e3-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="562e3-274">Этот шаг необязателен, но рекомендуется, чтобы вы могли проверить следующее hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="562e3-275">Hello ключа обмена ключами, которое включено в набор инструментов hello был создан в подлинном аппаратном модуле безопасности Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="562e3-276">хэш Hello hello World безопасности, включенный в набор инструментов hello был создан в подлинном аппаратном модуле безопасности Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="562e3-277">Hello ключа обмена ключами не экспортируется.</span><span class="sxs-lookup"><span data-stu-id="562e3-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="562e3-278">toovalidate hello загружен пакет, hello аппаратный модуль безопасности должен быть подключен, включен и должен иметь систему безопасности его (например, «hello, который вы только что создали).</span><span class="sxs-lookup"><span data-stu-id="562e3-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="562e3-279">пакет загружен hello toovalidate:</span><span class="sxs-lookup"><span data-stu-id="562e3-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="562e3-280">Запустите скрипт verifykeypackage.py hello, введите одно из следующих hello, в зависимости от географической области или экземпляр Azure:</span><span class="sxs-lookup"><span data-stu-id="562e3-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="562e3-281">Для Северной Америки:</span><span class="sxs-lookup"><span data-stu-id="562e3-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="562e3-282">Для Европы:</span><span class="sxs-lookup"><span data-stu-id="562e3-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="562e3-283">Для Азии:</span><span class="sxs-lookup"><span data-stu-id="562e3-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="562e3-284">Для Латинской Америки:</span><span class="sxs-lookup"><span data-stu-id="562e3-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="562e3-285">Для Японии:</span><span class="sxs-lookup"><span data-stu-id="562e3-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="562e3-286">Для Кореи:</span><span class="sxs-lookup"><span data-stu-id="562e3-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="562e3-287">Для Австралии:</span><span class="sxs-lookup"><span data-stu-id="562e3-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="562e3-288">Для [Azure для государственных](https://azure.microsoft.com/features/gov/), которая использует экземпляр правительства США hello Azure:</span><span class="sxs-lookup"><span data-stu-id="562e3-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="562e3-289">Для министерства обороны США:</span><span class="sxs-lookup"><span data-stu-id="562e3-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="562e3-290">Для Канады:</span><span class="sxs-lookup"><span data-stu-id="562e3-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="562e3-291">Для Германии:</span><span class="sxs-lookup"><span data-stu-id="562e3-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="562e3-292">Для Индии:</span><span class="sxs-lookup"><span data-stu-id="562e3-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="562e3-293">Hello программное обеспечение Thales включает файл python в %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="562e3-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="562e3-294">Подтвердите, что вы видите следующее hello, что указывает на успешную проверку: **результат: успех**</span><span class="sxs-lookup"><span data-stu-id="562e3-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="562e3-295">Этот скрипт проверяет цепочку подписавшего hello вверх toohello корневого ключа Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="562e3-296">Hello хэш этого корневого ключа встроен в скрипт hello и его значение должно быть **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="562e3-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="562e3-297">Вы можете также подтвердить это значение отдельно, посетив hello [веб-сайт Thales](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="562e3-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="562e3-298">Теперь вы готовы toocreate новый ключ.</span><span class="sxs-lookup"><span data-stu-id="562e3-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="562e3-299">Шаг 3.5. Создание ключа</span><span class="sxs-lookup"><span data-stu-id="562e3-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="562e3-300">Создать ключ с помощью hello Thales **generatekey** программы.</span><span class="sxs-lookup"><span data-stu-id="562e3-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="562e3-301">Выполните следующие команды toogenerate hello ключ hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="562e3-302">При выполнении команды следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="562e3-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="562e3-303">Здравствуйте, параметр *защиты* необходимо присвоить значение toohello **модуль**, как показано.</span><span class="sxs-lookup"><span data-stu-id="562e3-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="562e3-304">В результате будет создан ключ, защищенный модулем.</span><span class="sxs-lookup"><span data-stu-id="562e3-304">This creates a module-protected key.</span></span> <span data-ttu-id="562e3-305">набор средств BYOK Hello не поддерживает ключи, защищенные периодически подключаемыми системами.</span><span class="sxs-lookup"><span data-stu-id="562e3-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="562e3-306">Замените значение hello *contosokey* для hello **ident** и **plainname** с любым строковым значением.</span><span class="sxs-lookup"><span data-stu-id="562e3-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="562e3-307">toominimize административные затраты и уменьшить риск hello ошибок, рекомендуется использовать одинаковое значение для обоих hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="562e3-308">Hello **ident** значение должно содержать только цифры, тире и буквы нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="562e3-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="562e3-309">в этом примере Hello значение pubexp остается пустым (по умолчанию), но можно указать конкретные значения.</span><span class="sxs-lookup"><span data-stu-id="562e3-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="562e3-310">Дополнительные сведения см. в разделе hello документации Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="562e3-311">Эта команда создает файл ключа с токеном в папке %NFAST_KMDATA%\local с именем, начинающимся с **key_simple_**, а затем hello **ident** , указанный в команде hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="562e3-312">Пример: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="562e3-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="562e3-313">Этот файл содержит зашифрованный ключ.</span><span class="sxs-lookup"><span data-stu-id="562e3-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="562e3-314">Создайте резервную копию файла ключа с токеном в безопасном расположении.</span><span class="sxs-lookup"><span data-stu-id="562e3-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="562e3-315">Позже при передаче вашего ключа tooAzure хранилище ключей, корпорация Майкрософт не может экспортировать этого ключа tooyou назад, поэтому крайне важно сделать резервную копию ключа и безопасности системы безопасно.</span><span class="sxs-lookup"><span data-stu-id="562e3-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="562e3-316">За инструкциями и рекомендациями по резервному копированию ключа обращайтесь в компанию Thales.</span><span class="sxs-lookup"><span data-stu-id="562e3-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="562e3-317">Вы являются теперь готовы tootransfer вашего ключа tooAzure хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="562e3-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="562e3-318">Шаг 4. Подготовка ключа к передаче</span><span class="sxs-lookup"><span data-stu-id="562e3-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="562e3-319">Для выполнения этого шага четвертый hello следующих процедур на рабочей станции hello отключен.</span><span class="sxs-lookup"><span data-stu-id="562e3-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="562e3-320">Шаг 4.1. Создание копии ключа с ограниченными разрешениями</span><span class="sxs-lookup"><span data-stu-id="562e3-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="562e3-321">Откройте новую командную строку и измените hello расположение текущего каталога toohello где распаковал hello BYOK ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="562e3-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="562e3-322">tooreduce hello разрешения в ключе, из командной строки, выполните одну из следующих hello, в зависимости от географической области или экземпляр Azure.</span><span class="sxs-lookup"><span data-stu-id="562e3-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="562e3-323">Для Северной Америки:</span><span class="sxs-lookup"><span data-stu-id="562e3-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="562e3-324">Для Европы:</span><span class="sxs-lookup"><span data-stu-id="562e3-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="562e3-325">Для Азии:</span><span class="sxs-lookup"><span data-stu-id="562e3-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="562e3-326">Для Латинской Америки:</span><span class="sxs-lookup"><span data-stu-id="562e3-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="562e3-327">Для Японии:</span><span class="sxs-lookup"><span data-stu-id="562e3-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="562e3-328">Для Кореи:</span><span class="sxs-lookup"><span data-stu-id="562e3-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="562e3-329">Для Австралии:</span><span class="sxs-lookup"><span data-stu-id="562e3-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="562e3-330">Для [Azure для государственных](https://azure.microsoft.com/features/gov/), которая использует экземпляр правительства США hello Azure:</span><span class="sxs-lookup"><span data-stu-id="562e3-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="562e3-331">Для министерства обороны США:</span><span class="sxs-lookup"><span data-stu-id="562e3-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="562e3-332">Для Канады:</span><span class="sxs-lookup"><span data-stu-id="562e3-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="562e3-333">Для Германии:</span><span class="sxs-lookup"><span data-stu-id="562e3-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="562e3-334">Для Индии:</span><span class="sxs-lookup"><span data-stu-id="562e3-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="562e3-335">При выполнении этой команды замените *contosokey* hello таким же значением, которое указано в **3.5 шаг: Создание нового ключа** из hello [Создание ключа](#step-3-generate-your-key) шаг.</span><span class="sxs-lookup"><span data-stu-id="562e3-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="562e3-336">Будет предложено tooplug карты администратора системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="562e3-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="562e3-337">После завершения команды hello, вы видите **результат: успех** и hello копии ключа с ограниченными разрешениями, находятся в файле hello, с именем key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="562e3-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="562e3-338">Возможно проверяет hello списки управления ДОСТУПОМ с помощью следующих команд с помощью служебных программ Thales "hello":</span><span class="sxs-lookup"><span data-stu-id="562e3-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="562e3-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="562e3-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="562e3-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="562e3-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="562e3-341">При выполнении этих команд замените contosokey hello таким же значением, которое указано в **3.5 шаг: Создание нового ключа** из hello [Создание ключа](#step-3-generate-your-key) шаг.</span><span class="sxs-lookup"><span data-stu-id="562e3-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="562e3-342">Шаг 4.2. Шифрование ключа с помощью ключа обмена ключами Майкрософт</span><span class="sxs-lookup"><span data-stu-id="562e3-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="562e3-343">Выполните одну из следующих команд в зависимости от географического региона или экземпляр Azure hello.</span><span class="sxs-lookup"><span data-stu-id="562e3-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="562e3-344">Для Северной Америки:</span><span class="sxs-lookup"><span data-stu-id="562e3-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-345">Для Европы:</span><span class="sxs-lookup"><span data-stu-id="562e3-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-346">Для Азии:</span><span class="sxs-lookup"><span data-stu-id="562e3-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-347">Для Латинской Америки:</span><span class="sxs-lookup"><span data-stu-id="562e3-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-348">Для Японии:</span><span class="sxs-lookup"><span data-stu-id="562e3-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-349">Для Кореи:</span><span class="sxs-lookup"><span data-stu-id="562e3-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-350">Для Австралии:</span><span class="sxs-lookup"><span data-stu-id="562e3-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-351">Для [Azure для государственных](https://azure.microsoft.com/features/gov/), которая использует экземпляр правительства США hello Azure:</span><span class="sxs-lookup"><span data-stu-id="562e3-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-352">Для министерства обороны США:</span><span class="sxs-lookup"><span data-stu-id="562e3-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-353">Для Канады:</span><span class="sxs-lookup"><span data-stu-id="562e3-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-354">Для Германии:</span><span class="sxs-lookup"><span data-stu-id="562e3-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="562e3-355">Для Индии:</span><span class="sxs-lookup"><span data-stu-id="562e3-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="562e3-356">При выполнении команды следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="562e3-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="562e3-357">Замените *contosokey* с идентификатором hello, который вы использовали toogenerate hello в **3.5 шаг: Создание нового ключа** из hello [Создание ключа](#step-3-generate-your-key) шаг.</span><span class="sxs-lookup"><span data-stu-id="562e3-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="562e3-358">Замените *SubscriptionID* с Идентификатором hello hello подписку Azure, содержащий ваше хранилище ключа.</span><span class="sxs-lookup"><span data-stu-id="562e3-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="562e3-359">Вы получили это значение раньше, в **пункте 1.2: получить идентификатор подписки Azure** из hello [Подготовка рабочей станции, подключенного к Интернету](#step-1-prepare-your-internet-connected-workstation) шаг.</span><span class="sxs-lookup"><span data-stu-id="562e3-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="562e3-360">Замените *ContosoFirstHSMKey* меткой, которая используется для имени выходного файла.</span><span class="sxs-lookup"><span data-stu-id="562e3-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="562e3-361">При этом завершается успешно, отображается **результат: успех** , и новый файл в папке hello с именем hello: KeyTransferPackage -*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="562e3-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="562e3-362">Шаг 4.3: Копирование к передаче ключа пакета toohello подключенного к Интернету рабочей станции</span><span class="sxs-lookup"><span data-stu-id="562e3-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="562e3-363">Используйте USB-накопитель или другие переносное устройство toocopy hello выходной файл hello предыдущего шага (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour подключенного к Интернету рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="562e3-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="562e3-364">Шаг 5: Передача вашего ключа tooAzure хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="562e3-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="562e3-365">На этом этапе hello подключенного к Интернету, на рабочей станции использовать hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) пакет передачи ключа hello tooupload командлета, скопированный из hello отключен toohello рабочей станции HSM хранилища ключей Azure:</span><span class="sxs-lookup"><span data-stu-id="562e3-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="562e3-366">Если hello Отправка завершена успешно, можно увидеть свойства отображаемого hello hello ключа, который был только что добавлен.</span><span class="sxs-lookup"><span data-stu-id="562e3-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="562e3-367">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="562e3-367">Next steps</span></span>
<span data-ttu-id="562e3-368">Теперь ключ, защищенный с помощью аппаратного модуля безопасности, можно использовать в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="562e3-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="562e3-369">Дополнительные сведения см. в разделе hello **следует toouse аппаратный модуль безопасности (HSM)** раздела hello [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="562e3-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
