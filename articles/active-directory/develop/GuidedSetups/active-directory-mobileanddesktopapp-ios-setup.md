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
## <a name="setting-up-your-ios-application"></a>Настройка приложения iOS

Этот раздел содержит пошаговые инструкции для toocreate нового toodemonstrate проекта как toointegrate приложения iOS (Swift) с *вход с помощью Microsoft* , может обращаться к веб-API, требующие маркера.

> Предпочтение toodownload проекту XCode в этом примере вместо этого? [Загрузка проекта](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) и пропустить toohello [шаг настройки](#create-an-application-express) образец кода hello tooconfigure перед выполнением.


## <a name="install-carthage-toodownload-and-build-msal"></a>Установка Carthage toodownload и построение MSAL
Диспетчер пакетов Carthage используется период предварительного просмотра hello MSAL — она интегрируется с XCode, при этом сохраняя возможность hello библиотеки toohello изменения toomake Microsoft.

- Загрузить и установить последний выпуск hello Carthage [здесь](https://github.com/Carthage/Carthage/releases "Carthage загрузки URL-адрес")

## <a name="creating-your-application"></a>Создание приложения

1.  Откройте в Xcode и выберите `Create a new Xcode project`.
2.  Выберите `iOS` > `Single view Application` и нажмите кнопку *Далее*.
3.  Введите название продукта и нажмите кнопку *Далее*.
4.  Выберите toocreate папку приложения и нажмите кнопку *создать*

## <a name="build-hello-msal-framework"></a>Построение hello MSAL Framework

Следуйте инструкциям по hello toopull, а затем построить hello последнюю версию библиотек MSAL, с помощью Carthage:

1.  Откройте терминалов bash hello и перейдите в корневую папку приложения toohello
2.  Скопируйте hello ниже и вставьте в toocreate терминалов bash hello в файл «Cartfile»:

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Скопируйте и вставьте hello ниже. Эта команда извлекает зависимостей в папку Carthage и извлечения, а затем создает hello MSAL библиотеки:
</li>
</ol>

```bash
carthage update
```

> описанный выше процесс Hello — используется toodownload и hello сборки библиотеки проверки подлинности Microsoft (MSAL). MSAL обрабатывает получение, кэширование и обновление tooaccess пользователя маркеры, используемые интерфейсы API, защищенные hello v2 Azure Active Directory.

## <a name="add-hello-msal-framework-tooyour-application"></a>Добавить приложение tooyour framework MSAL hello
1.  В Xcode, откройте hello `General` вкладка
2.  Go toohello `Linked Frameworks and Libraries` и нажмите кнопку`+`
3.  Выберите `Add other…`
4.  Выберите `Carthage` > `Build` > `iOS` > `MSAL.framework` и нажмите кнопку *Открыть*. Вы увидите `MSAL.framework` добавлены toohello списка.
5.  Go слишком`Build Phases` и нажмите кнопку `+` значок, выберите`New Run Script Phase`
6.  Добавьте следующие toohello содержимое hello *скрипт области*:

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Добавьте hello следующие слишком<code>Input Files</code> , щелкнув <code>+</code>:
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a>Создание пользовательского интерфейса приложения
Файл Main.storyboard должен быть создан автоматически, как часть шаблона проекта. Следуйте инструкциям hello ниже приложение hello toocreate пользовательского интерфейса.

1.  Щелкните, удерживая нажатой `Main.storyboard` toobring вверх hello контекстного меню и выберите:`Open As` > `Source Code`
2.  Замените hello `<scenes>` узел hello код, приведенный ниже:

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
