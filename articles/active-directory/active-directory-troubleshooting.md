---
title: "Устранение неполадок: Элемент «Active Directory» отсутствует или недоступен | Документы Microsoft"
description: "Какие toodo при Active Directory пункт меню не отображается в hello портала управления Azure."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="a4917-103">Устранение неполадок: элемент Active Directory отсутствует или недоступен</span><span class="sxs-lookup"><span data-stu-id="a4917-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="a4917-104">Многие hello инструкции по использованию функции Azure Active Directory и службы начинаются с «toohello портал управления Azure перейдите и выберите **Active Directory**.»</span><span class="sxs-lookup"><span data-stu-id="a4917-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="a4917-105">Но что делать, если hello Active Directory расширения или пункта меню не появляется или если он помечен как **недоступно**?</span><span class="sxs-lookup"><span data-stu-id="a4917-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="a4917-106">Этот раздел является спроектированный toohelp.</span><span class="sxs-lookup"><span data-stu-id="a4917-106">This topic is designed toohelp.</span></span> <span data-ttu-id="a4917-107">Здесь описываются условия, при которых hello **Active Directory** отсутствует или недоступен и объясняется, как tooproceed.</span><span class="sxs-lookup"><span data-stu-id="a4917-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="a4917-108">Active Directory отсутствует</span><span class="sxs-lookup"><span data-stu-id="a4917-108">Active Directory is missing</span></span>
<span data-ttu-id="a4917-109">Как правило **Active Directory** элемент появляется в меню навигации слева hello.</span><span class="sxs-lookup"><span data-stu-id="a4917-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="a4917-110">инструкции Hello в Azure Active Directory процедуры предполагают, что этот элемент находится в представлении.</span><span class="sxs-lookup"><span data-stu-id="a4917-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Снимок экрана: Active Directory в Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="a4917-112">элемент Hello Active Directory появляется в hello левом меню навигации, когда любое из следующих условий hello.</span><span class="sxs-lookup"><span data-stu-id="a4917-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="a4917-113">В противном случае — элемент hello не отображается.</span><span class="sxs-lookup"><span data-stu-id="a4917-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="a4917-114">Hello текущий пользователь вошел с учетной записью Майкрософт (которая ранее называлась Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="a4917-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="a4917-115">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="a4917-115">OR</span></span>
* <span data-ttu-id="a4917-116">Hello клиент Windows Azure имеет каталог и hello текущая учетная запись является администратором каталога.</span><span class="sxs-lookup"><span data-stu-id="a4917-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="a4917-117">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="a4917-117">OR</span></span>
* <span data-ttu-id="a4917-118">Hello клиент Windows Azure имеет по крайней мере одно пространство имен Azure AD Access Control (ACS).</span><span class="sxs-lookup"><span data-stu-id="a4917-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="a4917-119">Дополнительные сведения см. в статье о [пространстве имен контроля доступа](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4917-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="a4917-120">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="a4917-120">OR</span></span>
* <span data-ttu-id="a4917-121">Hello клиент Windows Azure имеет хотя бы один поставщик многофакторной проверки подлинности Azure.</span><span class="sxs-lookup"><span data-stu-id="a4917-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="a4917-122">Дополнительные сведения см. в статье [Администрирование поставщиков Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="a4917-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="a4917-123">пространство имен Access Control или поставщика многофакторной проверки подлинности, щелкните toocreate **+ создать** > **службы приложений** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4917-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="a4917-124">каталог tooa tooget права администратора, имеют администратора назначить администратора роли tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="a4917-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="a4917-125">Дополнительные сведения см. в статье [Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a4917-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="a4917-126">Active Directory недоступен</span><span class="sxs-lookup"><span data-stu-id="a4917-126">Active Directory is not available</span></span>
<span data-ttu-id="a4917-127">Элемент **Active Directory** отобразится, если щелкнуть **+Создать** > **Службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="a4917-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="a4917-128">В частности элемент hello Active Directory появляется при все возможности Active Directory hello, например каталог, управление доступом или поставщик многофакторной проверки подлинности, доступные toohello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="a4917-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="a4917-129">Однако во время загрузки страницы приветствия hello элемент будет недоступен и помечен **недоступно**.</span><span class="sxs-lookup"><span data-stu-id="a4917-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="a4917-130">Это временное состояние.</span><span class="sxs-lookup"><span data-stu-id="a4917-130">This is a temporary state.</span></span> <span data-ttu-id="a4917-131">Если подождать несколько секунд, пункт hello станет доступным.</span><span class="sxs-lookup"><span data-stu-id="a4917-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="a4917-132">Если hello задержка продлевается, обновление hello веб-страницы часто устраняет проблему hello.</span><span class="sxs-lookup"><span data-stu-id="a4917-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![Снимок экрана: Active Directory недоступен](./media/active-directory-troubleshooting/not-available.png)

