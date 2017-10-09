---
title: "iOS v2 aaaAzure AD Приступая к работе - установки | Документы Microsoft"
description: "В этой статье описано, как приложения iOS (Swift) могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="95d08-103">Настройка приложения iOS</span><span class="sxs-lookup"><span data-stu-id="95d08-103">Setting up your iOS application</span></span>

<span data-ttu-id="95d08-104">Этот раздел содержит пошаговые инструкции для toocreate нового toodemonstrate проекта как toointegrate приложения iOS (Swift) с *вход с помощью Microsoft* , может обращаться к веб-API, требующие маркера.</span><span class="sxs-lookup"><span data-stu-id="95d08-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="95d08-105">Предпочтение toodownload проекту XCode в этом примере вместо этого?</span><span class="sxs-lookup"><span data-stu-id="95d08-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="95d08-106">[Загрузка проекта](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) и пропустить toohello [шаг настройки](#create-an-application-express) образец кода hello tooconfigure перед выполнением.</span><span class="sxs-lookup"><span data-stu-id="95d08-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="95d08-107">Установка Carthage toodownload и построение MSAL</span><span class="sxs-lookup"><span data-stu-id="95d08-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="95d08-108">Диспетчер пакетов Carthage используется период предварительного просмотра hello MSAL — она интегрируется с XCode, при этом сохраняя возможность hello библиотеки toohello изменения toomake Microsoft.</span><span class="sxs-lookup"><span data-stu-id="95d08-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="95d08-109">Загрузить и установить последний выпуск hello Carthage [здесь](https://github.com/Carthage/Carthage/releases "Carthage загрузки URL-адрес")</span><span class="sxs-lookup"><span data-stu-id="95d08-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="95d08-110">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="95d08-110">Creating your application</span></span>

1.  <span data-ttu-id="95d08-111">Откройте в Xcode и выберите `Create a new Xcode project`.</span><span class="sxs-lookup"><span data-stu-id="95d08-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="95d08-112">Выберите `iOS` > `Single view Application` и нажмите кнопку *Далее*.</span><span class="sxs-lookup"><span data-stu-id="95d08-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="95d08-113">Введите название продукта и нажмите кнопку *Далее*.</span><span class="sxs-lookup"><span data-stu-id="95d08-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="95d08-114">Выберите toocreate папку приложения и нажмите кнопку *создать*</span><span class="sxs-lookup"><span data-stu-id="95d08-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="95d08-115">Построение hello MSAL Framework</span><span class="sxs-lookup"><span data-stu-id="95d08-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="95d08-116">Следуйте инструкциям по hello toopull, а затем построить hello последнюю версию библиотек MSAL, с помощью Carthage:</span><span class="sxs-lookup"><span data-stu-id="95d08-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="95d08-117">Откройте терминалов bash hello и перейдите в корневую папку приложения toohello</span><span class="sxs-lookup"><span data-stu-id="95d08-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="95d08-118">Скопируйте hello ниже и вставьте в toocreate терминалов bash hello в файл «Cartfile»:</span><span class="sxs-lookup"><span data-stu-id="95d08-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="95d08-119">Скопируйте и вставьте hello ниже.</span><span class="sxs-lookup"><span data-stu-id="95d08-119">Copy and paste hello below.</span></span> <span data-ttu-id="95d08-120">Эта команда извлекает зависимостей в папку Carthage и извлечения, а затем создает hello MSAL библиотеки:</span><span class="sxs-lookup"><span data-stu-id="95d08-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="95d08-121">описанный выше процесс Hello — используется toodownload и hello сборки библиотеки проверки подлинности Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="95d08-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="95d08-122">MSAL обрабатывает получение, кэширование и обновление tooaccess пользователя маркеры, используемые интерфейсы API, защищенные hello v2 Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95d08-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="95d08-123">Добавить приложение tooyour framework MSAL hello</span><span class="sxs-lookup"><span data-stu-id="95d08-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="95d08-124">В Xcode, откройте hello `General` вкладка</span><span class="sxs-lookup"><span data-stu-id="95d08-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="95d08-125">Go toohello `Linked Frameworks and Libraries` и нажмите кнопку`+`</span><span class="sxs-lookup"><span data-stu-id="95d08-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="95d08-126">Выберите `Add other…`</span><span class="sxs-lookup"><span data-stu-id="95d08-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="95d08-127">Выберите `Carthage` > `Build` > `iOS` > `MSAL.framework` и нажмите кнопку *Открыть*.</span><span class="sxs-lookup"><span data-stu-id="95d08-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="95d08-128">Вы увидите `MSAL.framework` добавлены toohello списка.</span><span class="sxs-lookup"><span data-stu-id="95d08-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="95d08-129">Go слишком`Build Phases` и нажмите кнопку `+` значок, выберите`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="95d08-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="95d08-130">Добавьте следующие toohello содержимое hello *скрипт области*:</span><span class="sxs-lookup"><span data-stu-id="95d08-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="95d08-131">Добавьте hello следующие слишком<code>Input Files</code> , щелкнув <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="95d08-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="95d08-132">Создание пользовательского интерфейса приложения</span><span class="sxs-lookup"><span data-stu-id="95d08-132">Creating your application’s UI</span></span>
<span data-ttu-id="95d08-133">Файл Main.storyboard должен быть создан автоматически, как часть шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="95d08-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="95d08-134">Следуйте инструкциям hello ниже приложение hello toocreate пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="95d08-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="95d08-135">Щелкните, удерживая нажатой `Main.storyboard` toobring вверх hello контекстного меню и выберите:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="95d08-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="95d08-136">Замените hello `<scenes>` узел hello код, приведенный ниже:</span><span class="sxs-lookup"><span data-stu-id="95d08-136">Replace hello `<scenes>` node with hello code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
