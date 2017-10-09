---
title: "aaaAdd новую учетную запись клиента Azure стека в Azure Active Directory | Документы Microsoft"
description: "После развертывания пакета средств разработки Microsoft Azure стека, необходимо по крайней мере один toocreate клиента учетной записи пользователя, поэтому можно изучить hello клиентского портала."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a75d5c88-5b9e-4e9a-a6e3-48bbfa7069a7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: f0cd380d4fc0b52f4e5f6f0c9ef80d3dd0d64443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a><span data-ttu-id="c2aae-103">Добавление новой учетной записи клиента Azure Stack в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2aae-103">Add a new Azure Stack tenant account in Azure Active Directory</span></span>
<span data-ttu-id="c2aae-104">После [развертывание hello Azure стека Development Kit](azure-stack-run-powershell-script.md), потребуется учетной записью клиента, поэтому вы можете анализировать hello портала клиента и протестируйте свои предложения и планы.</span><span class="sxs-lookup"><span data-stu-id="c2aae-104">After [deploying hello Azure Stack Development Kit](azure-stack-run-powershell-script.md), you'll need a tenant user account so you can explore hello tenant portal and test your offers and plans.</span></span> <span data-ttu-id="c2aae-105">Можно создать учетную запись с [с помощью портала Azure "hello"](#create-an-azure-stack-tenant-account-using-the-azure-portal) или [с помощью PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span><span class="sxs-lookup"><span data-stu-id="c2aae-105">You can create a tenant account by [using hello Azure portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) or by [using PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span></span>

## <a name="create-an-azure-stack-tenant-account-using-hello-azure-portal"></a><span data-ttu-id="c2aae-106">Создать учетную запись клиента Azure стека с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="c2aae-106">Create an Azure Stack tenant account using hello Azure portal</span></span>
<span data-ttu-id="c2aae-107">Необходимо иметь подписку Azure toouse hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c2aae-107">You must have an Azure subscription toouse hello Azure portal.</span></span>

1. <span data-ttu-id="c2aae-108">Войдите в слишком[Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c2aae-108">Log in too[Azure](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c2aae-109">На левой навигационной панели Microsoft Azure щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2aae-109">In Microsoft Azure left navigation bar, click **Active Directory**.</span></span>
3. <span data-ttu-id="c2aae-110">В список каталогов hello щелкните каталог hello должны toouse для стека Azure или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="c2aae-110">In hello directory list, click hello directory that you want toouse for Azure Stack, or create a new one.</span></span>
4. <span data-ttu-id="c2aae-111">На странице каталога щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c2aae-111">On this directory page, click **Users**.</span></span>
5. <span data-ttu-id="c2aae-112">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="c2aae-112">Click **Add user**.</span></span>
6. <span data-ttu-id="c2aae-113">В hello **добавить пользователя** мастера в hello **тип пользователя** выберите **новый пользователь в вашей организации**.</span><span class="sxs-lookup"><span data-stu-id="c2aae-113">In hello **Add user** wizard, in hello **Type of user** list, choose **New user in your organization**.</span></span>
7. <span data-ttu-id="c2aae-114">В hello **имя пользователя** введите имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="c2aae-114">In hello **User name** box, type a name for hello user.</span></span>
8. <span data-ttu-id="c2aae-115">В hello  **@**  выберите соответствующую запись hello.</span><span class="sxs-lookup"><span data-stu-id="c2aae-115">In hello **@** box, choose hello appropriate entry.</span></span>
9. <span data-ttu-id="c2aae-116">Щелкните стрелку hello.</span><span class="sxs-lookup"><span data-stu-id="c2aae-116">Click hello next arrow.</span></span>
10. <span data-ttu-id="c2aae-117">В hello **профиля пользователя** на странице приветствия мастера введите команду **имя**, **Фамилия**, и **отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="c2aae-117">In hello **User profile** page of hello wizard, type a **First name**, **Last name**, and **Display name**.</span></span>
11. <span data-ttu-id="c2aae-118">В hello **роли** выберите **пользователя**.</span><span class="sxs-lookup"><span data-stu-id="c2aae-118">In hello **Role** list, choose **User**.</span></span>
12. <span data-ttu-id="c2aae-119">Щелкните стрелку hello.</span><span class="sxs-lookup"><span data-stu-id="c2aae-119">Click hello next arrow.</span></span>
13. <span data-ttu-id="c2aae-120">На hello **получение временного пароля** щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="c2aae-120">On hello **Get temporary password** page, click **Create**.</span></span>
14. <span data-ttu-id="c2aae-121">Копировать hello **новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="c2aae-121">Copy hello **New password**.</span></span>
15. <span data-ttu-id="c2aae-122">Войдите в tooMicrosoft Azure с новой учетной записью hello.</span><span class="sxs-lookup"><span data-stu-id="c2aae-122">Log in tooMicrosoft Azure with hello new account.</span></span> <span data-ttu-id="c2aae-123">Изменение пароля hello при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="c2aae-123">Change hello password when prompted.</span></span>
16. <span data-ttu-id="c2aae-124">Войдите в слишком`https://portal.local.azurestack.external` с hello новой учетной записи toosee hello портала клиента.</span><span class="sxs-lookup"><span data-stu-id="c2aae-124">Log in too`https://portal.local.azurestack.external` with hello new account toosee hello tenant portal.</span></span>

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a><span data-ttu-id="c2aae-125">Создание учетной записи клиента Azure Stack с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2aae-125">Create an Azure Stack tenant account using PowerShell</span></span>
<span data-ttu-id="c2aae-126">Если у вас нет подписки Azure, нельзя использовать hello Azure портала tooadd учетной записью клиента.</span><span class="sxs-lookup"><span data-stu-id="c2aae-126">If you don't have an Azure subscription, you can't use hello Azure portal tooadd a tenant user account.</span></span> <span data-ttu-id="c2aae-127">В этом случае можно вместо этого использовать hello Azure Active Directory модуля для Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2aae-127">In this case, you can use hello Azure Active Directory Module for Windows PowerShell instead.</span></span>

> [!NOTE]
> <span data-ttu-id="c2aae-128">При использовании учетной записи Майкрософт (Live ID) toodeploy пакет средств разработки стек Azure нельзя использовать учетную запись клиента toocreate AAD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2aae-128">If you are using Microsoft Account (Live ID) toodeploy Azure Stack Development Kit, you can't use AAD PowerShell toocreate tenant account.</span></span> 
> 
> 

1. <span data-ttu-id="c2aae-129">Установка hello [Microsoft Online Services помощник по входу для ИТ-специалистов RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span><span class="sxs-lookup"><span data-stu-id="c2aae-129">Install hello [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span></span>
2. <span data-ttu-id="c2aae-130">Установка hello [Azure Active Directory модуля для Windows PowerShell (64-разрядная версия)](http://go.microsoft.com/fwlink/p/?linkid=236297) и откройте его.</span><span class="sxs-lookup"><span data-stu-id="c2aae-130">Install hello [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297) and open it.</span></span>
3. <span data-ttu-id="c2aae-131">Выполните следующие командлеты hello.</span><span class="sxs-lookup"><span data-stu-id="c2aae-131">Run hello following cmdlets:</span></span>

    ```powershell
    # Provide hello AAD credential you use toodeploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with hello initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. <span data-ttu-id="c2aae-132">Войдите в tooMicrosoft Azure с новой учетной записью hello.</span><span class="sxs-lookup"><span data-stu-id="c2aae-132">Sign in tooMicrosoft Azure with hello new account.</span></span> <span data-ttu-id="c2aae-133">Изменение пароля hello при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="c2aae-133">Change hello password when prompted.</span></span>
2. <span data-ttu-id="c2aae-134">Войдите в слишком`https://portal.local.azurestack.external` с hello новой учетной записи toosee hello портала клиента.</span><span class="sxs-lookup"><span data-stu-id="c2aae-134">Sign in too`https://portal.local.azurestack.external` with hello new account toosee hello tenant portal.</span></span>

