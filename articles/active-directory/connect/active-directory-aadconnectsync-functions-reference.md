---
title: "Синхронизация Azure AD Connect: справочник по функциям | Документация Майкрософт"
description: "Общие сведения о выражениях декларативной подготовки в Azure AD Connect Sync"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="d2f63-103">Синхронизация Azure AD Connect: справочник по функциям</span><span class="sxs-lookup"><span data-stu-id="d2f63-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="d2f63-104">В Azure AD Connect функции, используемые toomanipulate значение атрибута во время синхронизации.</span><span class="sxs-lookup"><span data-stu-id="d2f63-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="d2f63-105">Синтаксис функции hello Hello выражается с помощью hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="d2f63-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="d2f63-106">Если функция перегружена и принимает несколько вариантов синтаксиса, перечисляются все допустимые варианты синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="d2f63-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="d2f63-107">функции Hello строго типизированы и проверяют, тип hello переданный тип hello задокументированы совпадений.</span><span class="sxs-lookup"><span data-stu-id="d2f63-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="d2f63-108">Если тип hello не совпадают, возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="d2f63-109">типы Hello выражаются с hello, используя синтаксис:</span><span class="sxs-lookup"><span data-stu-id="d2f63-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="d2f63-110">**bin** – двоичное значение</span><span class="sxs-lookup"><span data-stu-id="d2f63-110">**bin** – Binary</span></span>
* <span data-ttu-id="d2f63-111">**bool** — логическое значение</span><span class="sxs-lookup"><span data-stu-id="d2f63-111">**bool** – Boolean</span></span>
* <span data-ttu-id="d2f63-112">**dt** — дата и время в формате UTC</span><span class="sxs-lookup"><span data-stu-id="d2f63-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="d2f63-113">**enum** — перечисление известных констант</span><span class="sxs-lookup"><span data-stu-id="d2f63-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="d2f63-114">**EXP** — выражение, являющееся ожидается tooevaluate tooa логическое значение</span><span class="sxs-lookup"><span data-stu-id="d2f63-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="d2f63-115">**mvbin** — двоичное значение с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="d2f63-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="d2f63-116">**mvstr** — строка с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="d2f63-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="d2f63-117">**mvref** — ссылка с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="d2f63-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="d2f63-118">**num** — числовое значение</span><span class="sxs-lookup"><span data-stu-id="d2f63-118">**num** – Numeric</span></span>
* <span data-ttu-id="d2f63-119">**ref** — ссылка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-119">**ref** – Reference</span></span>
* <span data-ttu-id="d2f63-120">**str** — строка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-120">**str** – String</span></span>
* <span data-ttu-id="d2f63-121">**var** — вариант (почти) любого другого типа</span><span class="sxs-lookup"><span data-stu-id="d2f63-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="d2f63-122">**void** — не возвращает значение</span><span class="sxs-lookup"><span data-stu-id="d2f63-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="d2f63-123">Здравствуйте, функции, имеющие типы hello **mvbin**, **mvstr**, и **mvref** может работать только с несколькими значениями атрибутов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="d2f63-124">Функции типов **bin**, **str** и **ref** работают с однозначными и многозначными атрибутами.</span><span class="sxs-lookup"><span data-stu-id="d2f63-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="d2f63-125">Справочник по функциям</span><span class="sxs-lookup"><span data-stu-id="d2f63-125">Functions Reference</span></span>
| <span data-ttu-id="d2f63-126">Список функций</span><span class="sxs-lookup"><span data-stu-id="d2f63-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d2f63-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="d2f63-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="d2f63-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="d2f63-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="d2f63-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="d2f63-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="d2f63-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="d2f63-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="d2f63-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="d2f63-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="d2f63-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="d2f63-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="d2f63-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="d2f63-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="d2f63-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="d2f63-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="d2f63-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="d2f63-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="d2f63-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="d2f63-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="d2f63-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="d2f63-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="d2f63-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="d2f63-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="d2f63-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="d2f63-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="d2f63-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="d2f63-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="d2f63-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="d2f63-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="d2f63-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="d2f63-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="d2f63-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="d2f63-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="d2f63-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="d2f63-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="d2f63-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="d2f63-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="d2f63-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="d2f63-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="d2f63-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="d2f63-150">**Преобразование**</span><span class="sxs-lookup"><span data-stu-id="d2f63-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="d2f63-151">CBool</span><span class="sxs-lookup"><span data-stu-id="d2f63-151">CBool</span></span>](#cbool) |[<span data-ttu-id="d2f63-152">CDate</span><span class="sxs-lookup"><span data-stu-id="d2f63-152">CDate</span></span>](#cdate) |[<span data-ttu-id="d2f63-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="d2f63-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="d2f63-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="d2f63-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="d2f63-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="d2f63-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="d2f63-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="d2f63-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="d2f63-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="d2f63-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="d2f63-158">CNum</span><span class="sxs-lookup"><span data-stu-id="d2f63-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="d2f63-159">CRef</span><span class="sxs-lookup"><span data-stu-id="d2f63-159">CRef</span></span>](#cref) |[<span data-ttu-id="d2f63-160">CStr</span><span class="sxs-lookup"><span data-stu-id="d2f63-160">CStr</span></span>](#cstr) |[<span data-ttu-id="d2f63-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="d2f63-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="d2f63-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="d2f63-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="d2f63-163">**Date / Time**</span><span class="sxs-lookup"><span data-stu-id="d2f63-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="d2f63-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="d2f63-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="d2f63-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="d2f63-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="d2f63-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="d2f63-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="d2f63-167">Now</span><span class="sxs-lookup"><span data-stu-id="d2f63-167">Now</span></span>](#now) | |
| [<span data-ttu-id="d2f63-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="d2f63-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="d2f63-169">**Каталог**</span><span class="sxs-lookup"><span data-stu-id="d2f63-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="d2f63-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="d2f63-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="d2f63-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="d2f63-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="d2f63-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="d2f63-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="d2f63-173">**Оценка**</span><span class="sxs-lookup"><span data-stu-id="d2f63-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="d2f63-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="d2f63-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="d2f63-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="d2f63-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="d2f63-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="d2f63-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="d2f63-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="d2f63-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="d2f63-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="d2f63-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="d2f63-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="d2f63-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="d2f63-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="d2f63-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="d2f63-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="d2f63-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="d2f63-182">IsString</span><span class="sxs-lookup"><span data-stu-id="d2f63-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="d2f63-183">**Math**</span><span class="sxs-lookup"><span data-stu-id="d2f63-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="d2f63-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="d2f63-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="d2f63-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="d2f63-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="d2f63-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="d2f63-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="d2f63-187">**Функции с несколькими значениями:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="d2f63-188">Содержит</span><span class="sxs-lookup"><span data-stu-id="d2f63-188">Contains</span></span>](#contains) |[<span data-ttu-id="d2f63-189">Count</span><span class="sxs-lookup"><span data-stu-id="d2f63-189">Count</span></span>](#count) |[<span data-ttu-id="d2f63-190">Элемент</span><span class="sxs-lookup"><span data-stu-id="d2f63-190">Item</span></span>](#item) |[<span data-ttu-id="d2f63-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="d2f63-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="d2f63-192">Join</span><span class="sxs-lookup"><span data-stu-id="d2f63-192">Join</span></span>](#join) |[<span data-ttu-id="d2f63-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="d2f63-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="d2f63-194">разделение;</span><span class="sxs-lookup"><span data-stu-id="d2f63-194">Split</span></span>](#split) | | |
| <span data-ttu-id="d2f63-195">**Program Flow**</span><span class="sxs-lookup"><span data-stu-id="d2f63-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="d2f63-196">Ошибка</span><span class="sxs-lookup"><span data-stu-id="d2f63-196">Error</span></span>](#error) |[<span data-ttu-id="d2f63-197">IIF</span><span class="sxs-lookup"><span data-stu-id="d2f63-197">IIF</span></span>](#iif) |[<span data-ttu-id="d2f63-198">Выбор</span><span class="sxs-lookup"><span data-stu-id="d2f63-198">Select</span></span>](#select) |[<span data-ttu-id="d2f63-199">Switch</span><span class="sxs-lookup"><span data-stu-id="d2f63-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="d2f63-200">Where</span><span class="sxs-lookup"><span data-stu-id="d2f63-200">Where</span></span>](#where) |[<span data-ttu-id="d2f63-201">With</span><span class="sxs-lookup"><span data-stu-id="d2f63-201">With</span></span>](#with) | | | |
| <span data-ttu-id="d2f63-202">**текст**</span><span class="sxs-lookup"><span data-stu-id="d2f63-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="d2f63-203">GUID</span><span class="sxs-lookup"><span data-stu-id="d2f63-203">GUID</span></span>](#guid) |[<span data-ttu-id="d2f63-204">InStr</span><span class="sxs-lookup"><span data-stu-id="d2f63-204">InStr</span></span>](#instr) |[<span data-ttu-id="d2f63-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="d2f63-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="d2f63-206">LCase</span><span class="sxs-lookup"><span data-stu-id="d2f63-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="d2f63-207">Left</span><span class="sxs-lookup"><span data-stu-id="d2f63-207">Left</span></span>](#left) |[<span data-ttu-id="d2f63-208">Len</span><span class="sxs-lookup"><span data-stu-id="d2f63-208">Len</span></span>](#len) |[<span data-ttu-id="d2f63-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="d2f63-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="d2f63-210">Mid</span><span class="sxs-lookup"><span data-stu-id="d2f63-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="d2f63-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="d2f63-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="d2f63-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="d2f63-212">PadRight</span></span>](#padright) |[<span data-ttu-id="d2f63-213">PCase</span><span class="sxs-lookup"><span data-stu-id="d2f63-213">PCase</span></span>](#pcase) |[<span data-ttu-id="d2f63-214">Замените</span><span class="sxs-lookup"><span data-stu-id="d2f63-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="d2f63-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="d2f63-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="d2f63-216">Right</span><span class="sxs-lookup"><span data-stu-id="d2f63-216">Right</span></span>](#right) |[<span data-ttu-id="d2f63-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="d2f63-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="d2f63-218">Trim</span><span class="sxs-lookup"><span data-stu-id="d2f63-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="d2f63-219">UCase</span><span class="sxs-lookup"><span data-stu-id="d2f63-219">UCase</span></span>](#ucase) |[<span data-ttu-id="d2f63-220">Word</span><span class="sxs-lookup"><span data-stu-id="d2f63-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="d2f63-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="d2f63-221">BitAnd</span></span>
<span data-ttu-id="d2f63-222">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-222">**Description:**</span></span>  
<span data-ttu-id="d2f63-223">Hello функция BitAnd устанавливает указанные биты значения.</span><span class="sxs-lookup"><span data-stu-id="d2f63-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="d2f63-224">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="d2f63-225">value1, value2: числовые значения, которые должны быть соединены оператором AND.</span><span class="sxs-lookup"><span data-stu-id="d2f63-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="d2f63-226">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-226">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-227">Эта функция преобразует оба параметры toohello двоичное представление и устанавливает для бита:</span><span class="sxs-lookup"><span data-stu-id="d2f63-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="d2f63-228">0 — Если один или оба соответствующих бита в Здравствуйте, *маска* и *флаг* : 0</span><span class="sxs-lookup"><span data-stu-id="d2f63-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="d2f63-229">1 — Если оба соответствующих бита hello равны 1.</span><span class="sxs-lookup"><span data-stu-id="d2f63-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="d2f63-230">Другими словами она возвращает 0 во всех случаях, за исключением случаев, когда hello соответствующие биты в обоих параметрах равны 1.</span><span class="sxs-lookup"><span data-stu-id="d2f63-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="d2f63-231">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="d2f63-232">Возвращает 7, так как шестнадцатеричное "F" и «F7» вычислить значение toothis.</span><span class="sxs-lookup"><span data-stu-id="d2f63-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="d2f63-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="d2f63-233">BitOr</span></span>
<span data-ttu-id="d2f63-234">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-234">**Description:**</span></span>  
<span data-ttu-id="d2f63-235">Hello функция BitOr устанавливает указанные биты значения.</span><span class="sxs-lookup"><span data-stu-id="d2f63-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="d2f63-236">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="d2f63-237">value1, value2: числовые значения, которые должны быть соединены оператором OR.</span><span class="sxs-lookup"><span data-stu-id="d2f63-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="d2f63-238">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-238">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-239">Эта функция преобразует оба параметры toohello двоичное представление и задает too1 бит, если один или оба соответствующих бита hello в маске и флаге 1 и too0, если оба соответствующих бита hello равны 0.</span><span class="sxs-lookup"><span data-stu-id="d2f63-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="d2f63-240">Другими словами он возвращает 1 во всех случаях, за исключением того, где hello соответствующие биты в обоих параметрах равны 0.</span><span class="sxs-lookup"><span data-stu-id="d2f63-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="d2f63-241">CBool</span><span class="sxs-lookup"><span data-stu-id="d2f63-241">CBool</span></span>
<span data-ttu-id="d2f63-242">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-242">**Description:**</span></span>  
<span data-ttu-id="d2f63-243">Hello функция CBool возвращает логическое выражение вычисляется hello</span><span class="sxs-lookup"><span data-stu-id="d2f63-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="d2f63-244">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="d2f63-245">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-245">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-246">Если hello выражения вычисляется tooa ненулевое значение, CBool возвращает True, в противном случае он возвращает значение False.</span><span class="sxs-lookup"><span data-stu-id="d2f63-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="d2f63-247">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="d2f63-248">Здравствуйте, возвращает True, если атрибуты имеют одинаковое значение.</span><span class="sxs-lookup"><span data-stu-id="d2f63-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="d2f63-249">CDate</span><span class="sxs-lookup"><span data-stu-id="d2f63-249">CDate</span></span>
<span data-ttu-id="d2f63-250">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-250">**Description:**</span></span>  
<span data-ttu-id="d2f63-251">Hello Функция CDate возвращает UTC DateTime из строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="d2f63-252">DateTime не является собственным типом атрибута синхронизации, но используется некоторыми функциями.</span><span class="sxs-lookup"><span data-stu-id="d2f63-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="d2f63-253">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="d2f63-254">Value: строка с датой, временем и (необязательно) часовым поясом.</span><span class="sxs-lookup"><span data-stu-id="d2f63-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="d2f63-255">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-255">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-256">Hello возвращается строка всегда находится в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="d2f63-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="d2f63-257">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="d2f63-258">Возвращает значение DateTime, на основе времени начала hello сотрудника</span><span class="sxs-lookup"><span data-stu-id="d2f63-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="d2f63-259">Возвращает объект DateTime, представляющий значение 2013-01-11 12:00 AM.</span><span class="sxs-lookup"><span data-stu-id="d2f63-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="d2f63-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="d2f63-260">CertExtensionOids</span></span>
<span data-ttu-id="d2f63-261">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-261">**Description:**</span></span>  
<span data-ttu-id="d2f63-262">Возвращает hello значения Oid все критические расширения hello объекта сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="d2f63-263">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-264">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-265">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="d2f63-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="d2f63-266">CertFormat</span></span>
<span data-ttu-id="d2f63-267">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-267">**Description:**</span></span>  
<span data-ttu-id="d2f63-268">Возвращает hello имя hello формата сертификата X.509v3.</span><span class="sxs-lookup"><span data-stu-id="d2f63-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="d2f63-269">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-270">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-271">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="d2f63-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="d2f63-272">CertFriendlyName</span></span>
<span data-ttu-id="d2f63-273">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-273">**Description:**</span></span>  
<span data-ttu-id="d2f63-274">Возвращает hello связанный псевдоним для сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="d2f63-275">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-276">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-277">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="d2f63-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="d2f63-278">CertHashString</span></span>
<span data-ttu-id="d2f63-279">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-279">**Description:**</span></span>  
<span data-ttu-id="d2f63-280">Возвращает хэш-значение SHA1 для сертификата X.509v3 hello hello виде шестнадцатеричной строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="d2f63-281">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-282">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-283">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="d2f63-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="d2f63-284">CertIssuer</span></span>
<span data-ttu-id="d2f63-285">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-285">**Description:**</span></span>  
<span data-ttu-id="d2f63-286">Возвращает hello имя hello сертификации, выдавшего сертификат X.509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="d2f63-287">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-288">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-289">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="d2f63-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="d2f63-290">CertIssuerDN</span></span>
<span data-ttu-id="d2f63-291">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-291">**Description:**</span></span>  
<span data-ttu-id="d2f63-292">Возвращает hello различающееся имя издателя сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="d2f63-293">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-294">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-295">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="d2f63-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-296">CertIssuerOid</span></span>
<span data-ttu-id="d2f63-297">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-297">**Description:**</span></span>  
<span data-ttu-id="d2f63-298">Возвращает hello Oid hello издателя сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="d2f63-299">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-300">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-301">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="d2f63-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="d2f63-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="d2f63-303">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-303">**Description:**</span></span>  
<span data-ttu-id="d2f63-304">Возвращает hello сведения об алгоритме ключа для сертификата X.509v3 в виде строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="d2f63-305">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-306">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-307">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="d2f63-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="d2f63-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="d2f63-309">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-309">**Description:**</span></span>  
<span data-ttu-id="d2f63-310">Возвращает hello параметры алгоритма ключа для сертификата X.509v3 hello в виде шестнадцатеричной строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="d2f63-311">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-312">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-313">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="d2f63-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="d2f63-314">CertNameInfo</span></span>
<span data-ttu-id="d2f63-315">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-315">**Description:**</span></span>  
<span data-ttu-id="d2f63-316">Возвращает hello субъекта и издателя имена из сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="d2f63-317">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="d2f63-318">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-319">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="d2f63-320">X509NameType: hello X509NameType значение для темы hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="d2f63-321">includesIssuerName: имя издателя hello tooinclude значение true; в противном случае — значение false.</span><span class="sxs-lookup"><span data-stu-id="d2f63-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="d2f63-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="d2f63-322">CertNotAfter</span></span>
<span data-ttu-id="d2f63-323">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-323">**Description:**</span></span>  
<span data-ttu-id="d2f63-324">Возвращает hello дату в формате местного времени, после чего сертификат является допустимым.</span><span class="sxs-lookup"><span data-stu-id="d2f63-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="d2f63-325">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-326">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-327">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="d2f63-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="d2f63-328">CertNotBefore</span></span>
<span data-ttu-id="d2f63-329">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-329">**Description:**</span></span>  
<span data-ttu-id="d2f63-330">Возвращает hello дату в формате местного времени, в которой сертификат становится действительным.</span><span class="sxs-lookup"><span data-stu-id="d2f63-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="d2f63-331">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-332">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-333">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="d2f63-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-334">CertPublicKeyOid</span></span>
<span data-ttu-id="d2f63-335">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-335">**Description:**</span></span>  
<span data-ttu-id="d2f63-336">Возвращает hello Oid hello открытого ключа для сертификата X.509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="d2f63-337">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-338">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-339">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="d2f63-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="d2f63-341">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-341">**Description:**</span></span>  
<span data-ttu-id="d2f63-342">Возвращает hello Oid hello параметров открытого ключа для сертификата X.509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="d2f63-343">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-344">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-345">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="d2f63-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="d2f63-346">CertSerialNumber</span></span>
<span data-ttu-id="d2f63-347">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-347">**Description:**</span></span>  
<span data-ttu-id="d2f63-348">Возвращает серийный номер сертификата X.509v3 hello hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="d2f63-349">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-350">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-351">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="d2f63-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="d2f63-353">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-353">**Description:**</span></span>  
<span data-ttu-id="d2f63-354">Возвращает hello Oid hello алгоритма используется toocreate hello подписи сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="d2f63-355">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-356">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-357">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="d2f63-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="d2f63-358">CertSubject</span></span>
<span data-ttu-id="d2f63-359">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-359">**Description:**</span></span>  
<span data-ttu-id="d2f63-360">Возвращает hello различающееся имя субъекта из сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="d2f63-361">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-362">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-363">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="d2f63-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="d2f63-364">CertSubjectNameDN</span></span>
<span data-ttu-id="d2f63-365">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-365">**Description:**</span></span>  
<span data-ttu-id="d2f63-366">Возвращает hello различающееся имя субъекта из сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="d2f63-367">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-368">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-369">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="d2f63-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="d2f63-370">CertSubjectNameOid</span></span>
<span data-ttu-id="d2f63-371">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-371">**Description:**</span></span>  
<span data-ttu-id="d2f63-372">Возвращает hello Oid hello имени субъекта из сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="d2f63-373">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-374">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-375">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="d2f63-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="d2f63-376">CertThumbprint</span></span>
<span data-ttu-id="d2f63-377">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-377">**Description:**</span></span>  
<span data-ttu-id="d2f63-378">Возвращает hello отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="d2f63-379">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-380">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-381">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="d2f63-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="d2f63-382">CertVersion</span></span>
<span data-ttu-id="d2f63-383">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-383">**Description:**</span></span>  
<span data-ttu-id="d2f63-384">Возвращает hello версию формата сертификата X.509.</span><span class="sxs-lookup"><span data-stu-id="d2f63-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="d2f63-385">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-386">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-387">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="d2f63-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="d2f63-388">CGuid</span></span>
<span data-ttu-id="d2f63-389">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-389">**Description:**</span></span>  
<span data-ttu-id="d2f63-390">Hello функция CGuid Преобразует строковое представление hello tooits двоичное представление идентификатора GUID.</span><span class="sxs-lookup"><span data-stu-id="d2f63-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="d2f63-391">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="d2f63-392">Строка отформатирована по следующему шаблону: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx или {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="d2f63-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="d2f63-393">Содержит</span><span class="sxs-lookup"><span data-stu-id="d2f63-393">Contains</span></span>
<span data-ttu-id="d2f63-394">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-394">**Description:**</span></span>  
<span data-ttu-id="d2f63-395">функции Hello Contains находит строку внутри многозначного атрибута</span><span class="sxs-lookup"><span data-stu-id="d2f63-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="d2f63-396">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-396">**Syntax:**</span></span>  
<span data-ttu-id="d2f63-397">`num Contains (mvstring attribute, str search)` — с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="d2f63-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="d2f63-398">`num Contains (mvref attribute, str search)` — с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="d2f63-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="d2f63-399">атрибут: hello toosearch многозначного атрибута.</span><span class="sxs-lookup"><span data-stu-id="d2f63-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="d2f63-400">Поиск: строка toofind в атрибуте hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="d2f63-401">Casetype: без учета регистра или с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="d2f63-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="d2f63-402">Возвращает индекс в многозначном атрибуте hello, где найдена строка hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="d2f63-403">Если строка hello не найдена, возвращается 0.</span><span class="sxs-lookup"><span data-stu-id="d2f63-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="d2f63-404">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-404">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-405">Для многозначных строковых атрибутов hello искомое подстроки в значениях hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="d2f63-406">Для ссылочных атрибутов hello искомая строка должна точно соответствовать рассматриваются как совпадающие toobe значение hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="d2f63-407">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="d2f63-408">Если атрибут proxyAddresses hello содержит основной адрес электронной почты (обозначается в верхний регистр «SMTP:»), возвращается атрибут proxyAddress hello, в противном случае возвращает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="d2f63-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="d2f63-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="d2f63-409">ConvertFromBase64</span></span>
<span data-ttu-id="d2f63-410">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-410">**Description:**</span></span>  
<span data-ttu-id="d2f63-411">Hello ConvertFromBase64 функция преобразует hello указан строка регулярного tooa значение в кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="d2f63-412">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-412">**Syntax:**</span></span>  
<span data-ttu-id="d2f63-413">`str ConvertFromBase64(str source)` — здесь предполагается кодирование Юникод.</span><span class="sxs-lookup"><span data-stu-id="d2f63-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="d2f63-414">source: строка в кодировке Base64</span><span class="sxs-lookup"><span data-stu-id="d2f63-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="d2f63-415">Кодировка: Юникод, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="d2f63-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="d2f63-416">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="d2f63-417">Оба примера возвращают сообщение "*Hello world!*".</span><span class="sxs-lookup"><span data-stu-id="d2f63-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="d2f63-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="d2f63-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="d2f63-419">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-419">**Description:**</span></span>  
<span data-ttu-id="d2f63-420">Hello ConvertFromUTF8Hex функция преобразует hello указанную строку tooa значение шестнадцатеричной кодировке UTF8.</span><span class="sxs-lookup"><span data-stu-id="d2f63-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="d2f63-421">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="d2f63-422">source: строка в двухбайтовой кодировке UTF8.</span><span class="sxs-lookup"><span data-stu-id="d2f63-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="d2f63-423">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-423">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-424">Hello различие между этой функции и ConvertFromBase64([],UTF8) в результате этого hello понятное для атрибута DN hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="d2f63-425">Azure Active Directory использует этот формат в качестве различающегося имени.</span><span class="sxs-lookup"><span data-stu-id="d2f63-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="d2f63-426">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="d2f63-427">Возвращает сообщение*Hello world!*.</span><span class="sxs-lookup"><span data-stu-id="d2f63-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="d2f63-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="d2f63-428">ConvertToBase64</span></span>
<span data-ttu-id="d2f63-429">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-429">**Description:**</span></span>  
<span data-ttu-id="d2f63-430">Hello функция ConvertToBase64 преобразует строку tooa Юникода в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="d2f63-431">Преобразует значение hello массив целых чисел tooits эквивалентное строковое представление, представлен в кодировке base-64 знаков.</span><span class="sxs-lookup"><span data-stu-id="d2f63-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="d2f63-432">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="d2f63-433">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="d2f63-434">Возвращает SABlAGwAbABvACAAdwBvAHIAbABkACEA.</span><span class="sxs-lookup"><span data-stu-id="d2f63-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="d2f63-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="d2f63-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="d2f63-436">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-436">**Description:**</span></span>  
<span data-ttu-id="d2f63-437">Hello функция ConvertToUTF8Hex преобразует строку tooa значение шестнадцатеричной кодировке UTF8.</span><span class="sxs-lookup"><span data-stu-id="d2f63-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="d2f63-438">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="d2f63-439">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-439">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-440">Hello формат вывода этой функции используется службой Azure Active Directory в качестве формата атрибута DN.</span><span class="sxs-lookup"><span data-stu-id="d2f63-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="d2f63-441">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="d2f63-442">Возвращает 48656C6C6F20776F726C6421.</span><span class="sxs-lookup"><span data-stu-id="d2f63-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="d2f63-443">Count</span><span class="sxs-lookup"><span data-stu-id="d2f63-443">Count</span></span>
<span data-ttu-id="d2f63-444">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-444">**Description:**</span></span>  
<span data-ttu-id="d2f63-445">Hello функция Count возвращает количество элементов в hello в многозначном атрибуте</span><span class="sxs-lookup"><span data-stu-id="d2f63-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="d2f63-446">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="d2f63-447">CNum</span><span class="sxs-lookup"><span data-stu-id="d2f63-447">CNum</span></span>
<span data-ttu-id="d2f63-448">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-448">**Description:**</span></span>  
<span data-ttu-id="d2f63-449">Hello функция CNum принимает строку и возвращает числовой тип данных.</span><span class="sxs-lookup"><span data-stu-id="d2f63-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="d2f63-450">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="d2f63-451">CRef</span><span class="sxs-lookup"><span data-stu-id="d2f63-451">CRef</span></span>
<span data-ttu-id="d2f63-452">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-452">**Description:**</span></span>  
<span data-ttu-id="d2f63-453">Преобразует строку tooa ссылочный атрибут</span><span class="sxs-lookup"><span data-stu-id="d2f63-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="d2f63-454">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="d2f63-455">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="d2f63-456">CStr</span><span class="sxs-lookup"><span data-stu-id="d2f63-456">CStr</span></span>
<span data-ttu-id="d2f63-457">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-457">**Description:**</span></span>  
<span data-ttu-id="d2f63-458">Hello функция CStr преобразует tooa строкового типа данных.</span><span class="sxs-lookup"><span data-stu-id="d2f63-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="d2f63-459">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="d2f63-460">value: может быть числовым значением, ссылочным атрибутом или логическим значением.</span><span class="sxs-lookup"><span data-stu-id="d2f63-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="d2f63-461">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="d2f63-462">Может вернуть cn=Joe,dc=contoso,dc=com.</span><span class="sxs-lookup"><span data-stu-id="d2f63-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="d2f63-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="d2f63-463">DateAdd</span></span>
<span data-ttu-id="d2f63-464">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-464">**Description:**</span></span>  
<span data-ttu-id="d2f63-465">Возвращает дату, содержащий toowhich даты, который был добавлен указанный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="d2f63-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="d2f63-466">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="d2f63-467">интервал: строковое выражение, интервал времени, tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="d2f63-468">Строка Hello должен иметь одно из hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d2f63-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="d2f63-469">yyyy год</span><span class="sxs-lookup"><span data-stu-id="d2f63-469">yyyy Year</span></span>
  * <span data-ttu-id="d2f63-470">q квартал</span><span class="sxs-lookup"><span data-stu-id="d2f63-470">q Quarter</span></span>
  * <span data-ttu-id="d2f63-471">m месяц</span><span class="sxs-lookup"><span data-stu-id="d2f63-471">m Month</span></span>
  * <span data-ttu-id="d2f63-472">y день года</span><span class="sxs-lookup"><span data-stu-id="d2f63-472">y Day of year</span></span>
  * <span data-ttu-id="d2f63-473">d день</span><span class="sxs-lookup"><span data-stu-id="d2f63-473">d Day</span></span>
  * <span data-ttu-id="d2f63-474">w день недели</span><span class="sxs-lookup"><span data-stu-id="d2f63-474">w Weekday</span></span>
  * <span data-ttu-id="d2f63-475">ww неделя</span><span class="sxs-lookup"><span data-stu-id="d2f63-475">ww Week</span></span>
  * <span data-ttu-id="d2f63-476">h час</span><span class="sxs-lookup"><span data-stu-id="d2f63-476">h Hour</span></span>
  * <span data-ttu-id="d2f63-477">n минута</span><span class="sxs-lookup"><span data-stu-id="d2f63-477">n Minute</span></span>
  * <span data-ttu-id="d2f63-478">s секунда</span><span class="sxs-lookup"><span data-stu-id="d2f63-478">s Second</span></span>
* <span data-ttu-id="d2f63-479">значение: hello число единиц, требуется tooadd.</span><span class="sxs-lookup"><span data-stu-id="d2f63-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="d2f63-480">Оно может быть положительным (tooget даты в будущем hello) или отрицательное (tooget даты в прошлом hello).</span><span class="sxs-lookup"><span data-stu-id="d2f63-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="d2f63-481">Дата: DateTime, представляющих дату toowhich hello интервал добавляется.</span><span class="sxs-lookup"><span data-stu-id="d2f63-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="d2f63-482">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="d2f63-483">Добавляет три месяца и возвращает значение DateTime 2001-04-01.</span><span class="sxs-lookup"><span data-stu-id="d2f63-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="d2f63-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="d2f63-484">DateFromNum</span></span>
<span data-ttu-id="d2f63-485">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-485">**Description:**</span></span>  
<span data-ttu-id="d2f63-486">Hello функция DateFromNum преобразует значение в tooa формат даты AD типа DateTime.</span><span class="sxs-lookup"><span data-stu-id="d2f63-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="d2f63-487">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="d2f63-488">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="d2f63-489">Возвращает значение DateTime, равное 2012-01-01 23:00:00.</span><span class="sxs-lookup"><span data-stu-id="d2f63-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="d2f63-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="d2f63-490">DNComponent</span></span>
<span data-ttu-id="d2f63-491">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-491">**Description:**</span></span>  
<span data-ttu-id="d2f63-492">Hello функция DNComponent возвращает значение hello указанного компонента различающегося Имени, отсчитываемого слева.</span><span class="sxs-lookup"><span data-stu-id="d2f63-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="d2f63-493">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="d2f63-494">различающееся имя: hello ссылку атрибут toointerpret</span><span class="sxs-lookup"><span data-stu-id="d2f63-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="d2f63-495">ComponentNumber: компонент hello в tooreturn hello DN</span><span class="sxs-lookup"><span data-stu-id="d2f63-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="d2f63-496">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="d2f63-497">Если значение различающегося имени равно cn=Joe,ou=…, функция возвращает Joe.</span><span class="sxs-lookup"><span data-stu-id="d2f63-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="d2f63-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="d2f63-498">DNComponentRev</span></span>
<span data-ttu-id="d2f63-499">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-499">**Description:**</span></span>  
<span data-ttu-id="d2f63-500">Hello функция DNComponentRev возвращает значение hello указанного компонента различающегося Имени, отсчитываемого справа (hello end).</span><span class="sxs-lookup"><span data-stu-id="d2f63-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="d2f63-501">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="d2f63-502">различающееся имя: hello ссылку атрибут toointerpret</span><span class="sxs-lookup"><span data-stu-id="d2f63-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="d2f63-503">ComponentNumber - компонент hello в tooreturn hello DN</span><span class="sxs-lookup"><span data-stu-id="d2f63-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="d2f63-504">Options: DC — игнорировать все компоненты с "dc=".</span><span class="sxs-lookup"><span data-stu-id="d2f63-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="d2f63-505">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-505">**Example:**</span></span>  
<span data-ttu-id="d2f63-506">Если различающееся имя — cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com, то</span><span class="sxs-lookup"><span data-stu-id="d2f63-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="d2f63-507">оба вернут US.</span><span class="sxs-lookup"><span data-stu-id="d2f63-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="d2f63-508">Ошибка</span><span class="sxs-lookup"><span data-stu-id="d2f63-508">Error</span></span>
<span data-ttu-id="d2f63-509">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-509">**Description:**</span></span>  
<span data-ttu-id="d2f63-510">функции ошибок Hello — используется tooreturn настраиваемой ошибки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="d2f63-511">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="d2f63-512">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="d2f63-513">Если отсутствует атрибут accountName hello, вызывают ошибку для hello объекта.</span><span class="sxs-lookup"><span data-stu-id="d2f63-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="d2f63-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="d2f63-514">EscapeDNComponent</span></span>
<span data-ttu-id="d2f63-515">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-515">**Description:**</span></span>  
<span data-ttu-id="d2f63-516">функция EscapeDNComponent Hello один компонент различающегося имени и переключает его, поэтому он может быть представлен в LDAP.</span><span class="sxs-lookup"><span data-stu-id="d2f63-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="d2f63-517">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="d2f63-518">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="d2f63-519">Гарантирует, что hello объекта может быть создан в каталоге LDAP, даже если hello атрибут displayName содержит символы, которые необходимо экранировать в LDAP.</span><span class="sxs-lookup"><span data-stu-id="d2f63-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="d2f63-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="d2f63-520">FormatDateTime</span></span>
<span data-ttu-id="d2f63-521">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-521">**Description:**</span></span>  
<span data-ttu-id="d2f63-522">функция FormatDateTime Hello — используется tooformat строка tooa DateTime в указанном формате</span><span class="sxs-lookup"><span data-stu-id="d2f63-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="d2f63-523">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="d2f63-524">значение: значение в формате DateTime hello</span><span class="sxs-lookup"><span data-stu-id="d2f63-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="d2f63-525">формат: строка, представляющая hello tooconvert формат для.</span><span class="sxs-lookup"><span data-stu-id="d2f63-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="d2f63-526">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-526">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-527">Здравствуйте возможные значения для hello формата можно найти здесь: [определяемые пользователем форматы даты и времени (функция Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="d2f63-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="d2f63-528">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="d2f63-529">выдает результат 2007-12-25.</span><span class="sxs-lookup"><span data-stu-id="d2f63-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="d2f63-530">может вернуть результат 20140905081453.0Z.</span><span class="sxs-lookup"><span data-stu-id="d2f63-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="d2f63-531">GUID</span><span class="sxs-lookup"><span data-stu-id="d2f63-531">GUID</span></span>
<span data-ttu-id="d2f63-532">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-532">**Description:**</span></span>  
<span data-ttu-id="d2f63-533">Hello функция GUID создает случайный идентификатор GUID</span><span class="sxs-lookup"><span data-stu-id="d2f63-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="d2f63-534">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="d2f63-535">IIF</span><span class="sxs-lookup"><span data-stu-id="d2f63-535">IIF</span></span>
<span data-ttu-id="d2f63-536">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-536">**Description:**</span></span>  
<span data-ttu-id="d2f63-537">Hello функции IIF возвращает один из набора возможных значений на основе заданного условия.</span><span class="sxs-lookup"><span data-stu-id="d2f63-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="d2f63-538">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="d2f63-539">условие: любое значение или выражение, которое может быть вычислено tootrue или false.</span><span class="sxs-lookup"><span data-stu-id="d2f63-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="d2f63-540">valueIfTrue: hello условие tootrue, hello возвращенное значение.</span><span class="sxs-lookup"><span data-stu-id="d2f63-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="d2f63-541">valueIfFalse: hello условие toofalse, hello возвращенное значение.</span><span class="sxs-lookup"><span data-stu-id="d2f63-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="d2f63-542">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="d2f63-543">Если пользователь hello интернирования, возвращает hello псевдоним пользователя, имеющего «t-» добавлены toohello начале, else возвращает псевдоним пользователя hello без изменений.</span><span class="sxs-lookup"><span data-stu-id="d2f63-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="d2f63-544">InStr</span><span class="sxs-lookup"><span data-stu-id="d2f63-544">InStr</span></span>
<span data-ttu-id="d2f63-545">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-545">**Description:**</span></span>  
<span data-ttu-id="d2f63-546">Hello функция InStr находит hello первого вхождения подстроки в строке.</span><span class="sxs-lookup"><span data-stu-id="d2f63-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="d2f63-547">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="d2f63-548">проверяемая_строка: строка toobe поиск</span><span class="sxs-lookup"><span data-stu-id="d2f63-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="d2f63-549">искомая_строка: строка найдена toobe</span><span class="sxs-lookup"><span data-stu-id="d2f63-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="d2f63-550">Начать: начиная с позиции toofind hello подстроки</span><span class="sxs-lookup"><span data-stu-id="d2f63-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="d2f63-551">compare: vbTextCompare или vbBinaryCompare.</span><span class="sxs-lookup"><span data-stu-id="d2f63-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="d2f63-552">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-552">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-553">Позиция возвращает hello, где было найдено подстроки hello или 0, если не найден.</span><span class="sxs-lookup"><span data-stu-id="d2f63-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="d2f63-554">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="d2f63-555">/ / Возвращает too5</span><span class="sxs-lookup"><span data-stu-id="d2f63-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="d2f63-556">Результатом является too7</span><span class="sxs-lookup"><span data-stu-id="d2f63-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="d2f63-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="d2f63-557">InStrRev</span></span>
<span data-ttu-id="d2f63-558">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-558">**Description:**</span></span>  
<span data-ttu-id="d2f63-559">Hello функция InStrRev находит hello последнее вхождение подстроки в строке.</span><span class="sxs-lookup"><span data-stu-id="d2f63-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="d2f63-560">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="d2f63-561">проверяемая_строка: строка toobe поиск</span><span class="sxs-lookup"><span data-stu-id="d2f63-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="d2f63-562">искомая_строка: строка найдена toobe</span><span class="sxs-lookup"><span data-stu-id="d2f63-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="d2f63-563">Начать: начиная с позиции toofind hello подстроки</span><span class="sxs-lookup"><span data-stu-id="d2f63-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="d2f63-564">compare: vbTextCompare или vbBinaryCompare.</span><span class="sxs-lookup"><span data-stu-id="d2f63-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="d2f63-565">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-565">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-566">Позиция возвращает hello, где было найдено подстроки hello или 0, если не найден.</span><span class="sxs-lookup"><span data-stu-id="d2f63-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="d2f63-567">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="d2f63-568">Возвращает значение 7.</span><span class="sxs-lookup"><span data-stu-id="d2f63-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="d2f63-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="d2f63-569">IsBitSet</span></span>
<span data-ttu-id="d2f63-570">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-570">**Description:**</span></span>  
<span data-ttu-id="d2f63-571">Hello функция IsBitSet проверяет, если битовое или нет</span><span class="sxs-lookup"><span data-stu-id="d2f63-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="d2f63-572">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="d2f63-573">значение: числовое значение, представляющее evaluated.flag: числовое значение, которое имеет hello бит toobe оценка</span><span class="sxs-lookup"><span data-stu-id="d2f63-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="d2f63-574">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="d2f63-575">Возвращает значение True, так как «4» бита в шестнадцатеричное значение hello «F»</span><span class="sxs-lookup"><span data-stu-id="d2f63-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="d2f63-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="d2f63-576">IsDate</span></span>
<span data-ttu-id="d2f63-577">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-577">**Description:**</span></span>  
<span data-ttu-id="d2f63-578">Если hello выражение может быть hello Функция IsDate принимает tooTrue вычисляет типа DateTime.</span><span class="sxs-lookup"><span data-stu-id="d2f63-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="d2f63-579">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="d2f63-580">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-580">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-581">Toodetermine используется в том случае, если функция CDate() может быть успешно.</span><span class="sxs-lookup"><span data-stu-id="d2f63-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="d2f63-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="d2f63-582">IsCert</span></span>
<span data-ttu-id="d2f63-583">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-583">**Description:**</span></span>  
<span data-ttu-id="d2f63-584">Возвращает значение true, если hello необработанные данные могут быть сериализованы в объект .NET X509Certificate2 сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="d2f63-585">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="d2f63-586">certificateRawData: представление сертификата X.509 в виде массива байтов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="d2f63-587">Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d2f63-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="d2f63-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="d2f63-588">IsEmpty</span></span>
<span data-ttu-id="d2f63-589">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-589">**Description:**</span></span>  
<span data-ttu-id="d2f63-590">Если атрибут hello в hello CS или MV, но результатом является пустая строка tooan, функция IsEmpty hello оценивает tooTrue.</span><span class="sxs-lookup"><span data-stu-id="d2f63-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="d2f63-591">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="d2f63-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="d2f63-592">IsGuid</span></span>
<span data-ttu-id="d2f63-593">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-593">**Description:**</span></span>  
<span data-ttu-id="d2f63-594">Если строка hello удалось преобразованный tooa GUID, функция isguid возвращает hello вычисляется tootrue.</span><span class="sxs-lookup"><span data-stu-id="d2f63-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="d2f63-595">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="d2f63-596">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-596">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-597">GUID представляет собой строку, созданную по одному из этих шаблонов: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx или {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}.</span><span class="sxs-lookup"><span data-stu-id="d2f63-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="d2f63-598">Toodetermine используется в том случае, если функция CGuid() может быть успешно.</span><span class="sxs-lookup"><span data-stu-id="d2f63-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="d2f63-599">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="d2f63-600">Если hello атрибут StrAttribute имеет формат GUID, возвращает двоичное представление, в противном случае возвращает значение Null.</span><span class="sxs-lookup"><span data-stu-id="d2f63-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="d2f63-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="d2f63-601">IsNull</span></span>
<span data-ttu-id="d2f63-602">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-602">**Description:**</span></span>  
<span data-ttu-id="d2f63-603">Если hello выражение tooNull, hello IsNull, функция возвращает значение true.</span><span class="sxs-lookup"><span data-stu-id="d2f63-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="d2f63-604">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="d2f63-605">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-605">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-606">Значение Null для атрибута, выражается hello отсутствие атрибута hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="d2f63-607">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="d2f63-608">Возвращает значение True, если отсутствует атрибут hello в hello CS и MV.</span><span class="sxs-lookup"><span data-stu-id="d2f63-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="d2f63-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="d2f63-609">IsNullOrEmpty</span></span>
<span data-ttu-id="d2f63-610">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-610">**Description:**</span></span>  
<span data-ttu-id="d2f63-611">Если hello выражение имеет значение null или пустую строку, hello функция IsNullOrEmpty возвращает true.</span><span class="sxs-lookup"><span data-stu-id="d2f63-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="d2f63-612">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="d2f63-613">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-613">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-614">Для атрибута эта функция tooTrue Если атрибут hello отсутствует или присутствует, но является пустой строкой.</span><span class="sxs-lookup"><span data-stu-id="d2f63-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="d2f63-615">Hello обратная функция называется IsPresent.</span><span class="sxs-lookup"><span data-stu-id="d2f63-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="d2f63-616">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="d2f63-617">Возвращает значение True, если атрибут hello не существует или является пустой строкой в hello CS и MV.</span><span class="sxs-lookup"><span data-stu-id="d2f63-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="d2f63-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="d2f63-618">IsNumeric</span></span>
<span data-ttu-id="d2f63-619">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-619">**Description:**</span></span>  
<span data-ttu-id="d2f63-620">Hello функция IsNumeric возвращает логическое значение, указывающее, является ли выражение может быть распознано как числовой тип.</span><span class="sxs-lookup"><span data-stu-id="d2f63-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="d2f63-621">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="d2f63-622">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-622">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-623">Использовать toodetermine ли CNum() успешно tooparse hello выражения.</span><span class="sxs-lookup"><span data-stu-id="d2f63-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="d2f63-624">IsString</span><span class="sxs-lookup"><span data-stu-id="d2f63-624">IsString</span></span>
<span data-ttu-id="d2f63-625">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-625">**Description:**</span></span>  
<span data-ttu-id="d2f63-626">Если выражение hello может быть вычисленное tooa строковый тип, то hello функция IsString возвращает tooTrue.</span><span class="sxs-lookup"><span data-stu-id="d2f63-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="d2f63-627">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="d2f63-628">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-628">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-629">Использовать toodetermine ли CStr() успешно tooparse hello выражения.</span><span class="sxs-lookup"><span data-stu-id="d2f63-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="d2f63-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="d2f63-630">IsPresent</span></span>
<span data-ttu-id="d2f63-631">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-631">**Description:**</span></span>  
<span data-ttu-id="d2f63-632">Если hello выражение tooa строку, которая не имеет значение Null и не является пустым, затем hello IsPresent, функция возвращает значение true.</span><span class="sxs-lookup"><span data-stu-id="d2f63-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="d2f63-633">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="d2f63-634">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-634">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-635">Hello обратная функция называется IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="d2f63-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="d2f63-636">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="d2f63-637">Элемент</span><span class="sxs-lookup"><span data-stu-id="d2f63-637">Item</span></span>
<span data-ttu-id="d2f63-638">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-638">**Description:**</span></span>  
<span data-ttu-id="d2f63-639">Hello функция Item возвращает один элемент из многозначной строки или атрибута.</span><span class="sxs-lookup"><span data-stu-id="d2f63-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="d2f63-640">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="d2f63-641">attribute: атрибут с несколькими значениями</span><span class="sxs-lookup"><span data-stu-id="d2f63-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="d2f63-642">Индекс: элемент tooan индекса в многозначную строку hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="d2f63-643">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-643">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-644">Hello функция Item полезна в сочетании hello функция Contains так как последний функции hello возвращает элемент tooan индекса hello в многозначном атрибуте hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="d2f63-645">Вызывает ошибку, если индекс выходит за допустимые пределы.</span><span class="sxs-lookup"><span data-stu-id="d2f63-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="d2f63-646">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="d2f63-647">Возвращает hello основной адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="d2f63-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="d2f63-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="d2f63-648">ItemOrNull</span></span>
<span data-ttu-id="d2f63-649">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-649">**Description:**</span></span>  
<span data-ttu-id="d2f63-650">Hello функция ItemOrNull возвращает один элемент из многозначной строки или атрибута.</span><span class="sxs-lookup"><span data-stu-id="d2f63-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="d2f63-651">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="d2f63-652">attribute: атрибут с несколькими значениями</span><span class="sxs-lookup"><span data-stu-id="d2f63-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="d2f63-653">Индекс: элемент tooan индекса в многозначную строку hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="d2f63-654">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-654">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-655">Hello функция ItemOrNull полезна в сочетании hello функция Contains так как последний функции hello возвращает элемент tooan индекса hello в многозначном атрибуте hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="d2f63-656">Возвращает значение Null, если индекс выходит за допустимые пределы.</span><span class="sxs-lookup"><span data-stu-id="d2f63-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="d2f63-657">Join</span><span class="sxs-lookup"><span data-stu-id="d2f63-657">Join</span></span>
<span data-ttu-id="d2f63-658">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-658">**Description:**</span></span>  
<span data-ttu-id="d2f63-659">функции Hello Join принимает многозначную строку и возвращает однозначную строку с указанным разделителем между элементами.</span><span class="sxs-lookup"><span data-stu-id="d2f63-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="d2f63-660">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="d2f63-661">атрибут: многозначный атрибут, содержащий строки toobe присоединен.</span><span class="sxs-lookup"><span data-stu-id="d2f63-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="d2f63-662">разделитель: любая строка, используемые tooseparate подстроки hello вернул строку hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="d2f63-663">Если не указано, hello символ пробела (» «) используется.</span><span class="sxs-lookup"><span data-stu-id="d2f63-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="d2f63-664">Если разделитель является строкой нулевой длины ("») или Nothing, все элементы в списке hello сцепляются без разделителей.</span><span class="sxs-lookup"><span data-stu-id="d2f63-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="d2f63-665">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="d2f63-665">**Remarks**</span></span>  
<span data-ttu-id="d2f63-666">Имеется соответствие между hello соединения и функции разбиения.</span><span class="sxs-lookup"><span data-stu-id="d2f63-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="d2f63-667">Hello функция Join принимает массив строк и объединяет их с помощью строки-разделителя, tooreturn одну строку.</span><span class="sxs-lookup"><span data-stu-id="d2f63-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="d2f63-668">Hello функция Split принимает строку и разбивает ее по разделителям hello, tooreturn массив строк.</span><span class="sxs-lookup"><span data-stu-id="d2f63-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="d2f63-669">Эти функции различаются тем, что Join может объединять строки с любой строкой-разделителем, а Split может разделять строки с помощью одного символа-разделителя.</span><span class="sxs-lookup"><span data-stu-id="d2f63-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="d2f63-670">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="d2f63-671">Может вернуть: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="d2f63-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="d2f63-672">LCase</span><span class="sxs-lookup"><span data-stu-id="d2f63-672">LCase</span></span>
<span data-ttu-id="d2f63-673">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-673">**Description:**</span></span>  
<span data-ttu-id="d2f63-674">Hello функция LCase преобразует все символы в случае toolower строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="d2f63-675">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="d2f63-676">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="d2f63-677">Возвращает значение Test.</span><span class="sxs-lookup"><span data-stu-id="d2f63-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="d2f63-678">Left</span><span class="sxs-lookup"><span data-stu-id="d2f63-678">Left</span></span>
<span data-ttu-id="d2f63-679">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-679">**Description:**</span></span>  
<span data-ttu-id="d2f63-680">Hello функция Left возвращает указанное количество символов слева hello строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="d2f63-681">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="d2f63-682">строки: hello tooreturn символов строки из</span><span class="sxs-lookup"><span data-stu-id="d2f63-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="d2f63-683">NumChars: число, задающее количество hello tooreturn символов с начала hello (слева), строки</span><span class="sxs-lookup"><span data-stu-id="d2f63-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="d2f63-684">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-684">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-685">Строка, содержащая первые numChars символов hello в строке:</span><span class="sxs-lookup"><span data-stu-id="d2f63-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="d2f63-686">если numChars = 0, возвращается пустая строка;</span><span class="sxs-lookup"><span data-stu-id="d2f63-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="d2f63-687">если numChars < 0, возвращается введенная строка;</span><span class="sxs-lookup"><span data-stu-id="d2f63-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="d2f63-688">если строка имеет значение Null, возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-688">If string is null, return empty string.</span></span>

<span data-ttu-id="d2f63-689">Если строка содержит меньше символов, чем hello числу, заданному параметром numChars, возвращается строка идентичные toostring, (, содержащего все символы в параметр 1).</span><span class="sxs-lookup"><span data-stu-id="d2f63-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="d2f63-690">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="d2f63-691">Возвращает значение Joh.</span><span class="sxs-lookup"><span data-stu-id="d2f63-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="d2f63-692">Len</span><span class="sxs-lookup"><span data-stu-id="d2f63-692">Len</span></span>
<span data-ttu-id="d2f63-693">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-693">**Description:**</span></span>  
<span data-ttu-id="d2f63-694">Hello функция Len возвращает число символов в строке.</span><span class="sxs-lookup"><span data-stu-id="d2f63-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="d2f63-695">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="d2f63-696">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="d2f63-697">Возвращает значение 8.</span><span class="sxs-lookup"><span data-stu-id="d2f63-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="d2f63-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="d2f63-698">LTrim</span></span>
<span data-ttu-id="d2f63-699">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-699">**Description:**</span></span>  
<span data-ttu-id="d2f63-700">Hello функция LTrim удаляет начальные пробелы из строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="d2f63-701">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="d2f63-702">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="d2f63-703">Возвращает значение Test.</span><span class="sxs-lookup"><span data-stu-id="d2f63-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="d2f63-704">Mid</span><span class="sxs-lookup"><span data-stu-id="d2f63-704">Mid</span></span>
<span data-ttu-id="d2f63-705">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-705">**Description:**</span></span>  
<span data-ttu-id="d2f63-706">Здравствуйте, Mid функция возвращает указанное количество символов, начиная с указанной позиции в строке.</span><span class="sxs-lookup"><span data-stu-id="d2f63-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="d2f63-707">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="d2f63-708">строки: hello tooreturn символов строки из</span><span class="sxs-lookup"><span data-stu-id="d2f63-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="d2f63-709">Начать: число, задающее hello, начальная позиция в строку символов tooreturn из</span><span class="sxs-lookup"><span data-stu-id="d2f63-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="d2f63-710">NumChars: число, задающее количество hello tooreturn символов из положения в строке</span><span class="sxs-lookup"><span data-stu-id="d2f63-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="d2f63-711">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-711">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-712">Возвращает символы numChars, начиная с позиции start в строке.</span><span class="sxs-lookup"><span data-stu-id="d2f63-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="d2f63-713">Строка, содержащая numChars символов начиная с позиции start в строке:</span><span class="sxs-lookup"><span data-stu-id="d2f63-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="d2f63-714">если numChars = 0, возвращается пустая строка;</span><span class="sxs-lookup"><span data-stu-id="d2f63-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="d2f63-715">если numChars < 0, возвращается введенная строка;</span><span class="sxs-lookup"><span data-stu-id="d2f63-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="d2f63-716">Если запустить > Здравствуйте, длина строки, возвращается исходная строка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="d2f63-717">если start < = 0, возвращается введенная строка;</span><span class="sxs-lookup"><span data-stu-id="d2f63-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="d2f63-718">если строка имеет значение Null, возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-718">If string is null, return empty string.</span></span>

<span data-ttu-id="d2f63-719">Если в строке не осталось numChar символов начиная с позиции start, возвращается столько символов, сколько может быть возвращено.</span><span class="sxs-lookup"><span data-stu-id="d2f63-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="d2f63-720">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="d2f63-721">Возвращает значение hn Do.</span><span class="sxs-lookup"><span data-stu-id="d2f63-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="d2f63-722">Возвращает значение Doe.</span><span class="sxs-lookup"><span data-stu-id="d2f63-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="d2f63-723">Now</span><span class="sxs-lookup"><span data-stu-id="d2f63-723">Now</span></span>
<span data-ttu-id="d2f63-724">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-724">**Description:**</span></span>  
<span data-ttu-id="d2f63-725">Hello Теперь функция возвращает значение типа DateTime hello текущую дату и время, в соответствии с tooyour компьютера системной даты и времени.</span><span class="sxs-lookup"><span data-stu-id="d2f63-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="d2f63-726">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="d2f63-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="d2f63-727">NumFromDate</span></span>
<span data-ttu-id="d2f63-728">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-728">**Description:**</span></span>  
<span data-ttu-id="d2f63-729">Hello функция NumFromDate возвращает дату в формате.</span><span class="sxs-lookup"><span data-stu-id="d2f63-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="d2f63-730">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="d2f63-731">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="d2f63-732">Возвращает значение 129699324000000000.</span><span class="sxs-lookup"><span data-stu-id="d2f63-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="d2f63-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="d2f63-733">PadLeft</span></span>
<span data-ttu-id="d2f63-734">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-734">**Description:**</span></span>  
<span data-ttu-id="d2f63-735">Hello PadLeft функции left дополняет tooa строку, в указанный длины, используя заданный заполняющий символ.</span><span class="sxs-lookup"><span data-stu-id="d2f63-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="d2f63-736">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="d2f63-737">строки: hello toopad строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-737">string: hello string toopad.</span></span>
* <span data-ttu-id="d2f63-738">Длина: integer, представляющее hello требуемого длину строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="d2f63-739">символ padCharacter: строка, состоящая из одного символа toouse как знак-заполнитель hello</span><span class="sxs-lookup"><span data-stu-id="d2f63-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="d2f63-740">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-740">**Remarks:**</span></span>

* <span data-ttu-id="d2f63-741">Если hello длина строки меньше length, символ padCharacter — многократно присоединенных toohello начало (слева) строки до его длина равна toolength.</span><span class="sxs-lookup"><span data-stu-id="d2f63-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="d2f63-742">Значение padCharacter может быть символом пробела, но оно не может иметь значение Null.</span><span class="sxs-lookup"><span data-stu-id="d2f63-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="d2f63-743">Если длина hello строки больше, чем длина равна tooor, строка возвращается без изменений.</span><span class="sxs-lookup"><span data-stu-id="d2f63-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="d2f63-744">Если строка имеет длину больше или равно toolength, возвращается toostring одинаковые строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="d2f63-745">Если hello длина строки меньше length, новая строка hello требуемого возвращается длина, содержащий строку, дополненную символом padCharacter.</span><span class="sxs-lookup"><span data-stu-id="d2f63-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="d2f63-746">Если строка имеет значение null, функция hello возвращает пустую строку.</span><span class="sxs-lookup"><span data-stu-id="d2f63-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="d2f63-747">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="d2f63-748">Возвращает значение 000000User.</span><span class="sxs-lookup"><span data-stu-id="d2f63-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="d2f63-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="d2f63-749">PadRight</span></span>
<span data-ttu-id="d2f63-750">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-750">**Description:**</span></span>  
<span data-ttu-id="d2f63-751">Hello PadRight функция дополняет справа tooa строку, в указанный длины, используя заданный заполняющий символ.</span><span class="sxs-lookup"><span data-stu-id="d2f63-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="d2f63-752">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="d2f63-753">строки: hello toopad строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-753">string: hello string toopad.</span></span>
* <span data-ttu-id="d2f63-754">Длина: integer, представляющее hello требуемого длину строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="d2f63-755">символ padCharacter: строка, состоящая из одного символа toouse как знак-заполнитель hello</span><span class="sxs-lookup"><span data-stu-id="d2f63-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="d2f63-756">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-756">**Remarks:**</span></span>

* <span data-ttu-id="d2f63-757">Если hello длина строки меньше length, символ padCharacter — многократно присоединенных toohello конец (справа) строки до его длина равна toolength.</span><span class="sxs-lookup"><span data-stu-id="d2f63-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="d2f63-758">Значение padCharacter может быть символом пробела, но оно не может иметь значение Null.</span><span class="sxs-lookup"><span data-stu-id="d2f63-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="d2f63-759">Если длина hello строки больше, чем длина равна tooor, строка возвращается без изменений.</span><span class="sxs-lookup"><span data-stu-id="d2f63-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="d2f63-760">Если строка имеет длину больше или равно toolength, возвращается toostring одинаковые строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="d2f63-761">Если hello длина строки меньше length, новая строка hello требуемого возвращается длина, содержащий строку, дополненную символом padCharacter.</span><span class="sxs-lookup"><span data-stu-id="d2f63-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="d2f63-762">Если строка имеет значение null, функция hello возвращает пустую строку.</span><span class="sxs-lookup"><span data-stu-id="d2f63-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="d2f63-763">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="d2f63-764">Возвращает значение User000000.</span><span class="sxs-lookup"><span data-stu-id="d2f63-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="d2f63-765">PCase</span><span class="sxs-lookup"><span data-stu-id="d2f63-765">PCase</span></span>
<span data-ttu-id="d2f63-766">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-766">**Description:**</span></span>  
<span data-ttu-id="d2f63-767">Hello функция PCase преобразует первый символ каждого слова с разделителями-пробелами, в случае tooupper строку hello, а все остальные символы преобразуются toolower регистр.</span><span class="sxs-lookup"><span data-stu-id="d2f63-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="d2f63-768">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="d2f63-769">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-769">**Remarks:**</span></span>

* <span data-ttu-id="d2f63-770">Эта функция не обеспечивает в настоящее время tooconvert с учетом регистра слово, которое является полностью верхнем регистре, например акронима.</span><span class="sxs-lookup"><span data-stu-id="d2f63-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="d2f63-771">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="d2f63-772">Возвращает значение Test.</span><span class="sxs-lookup"><span data-stu-id="d2f63-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="d2f63-773">Возвращает значение Test.</span><span class="sxs-lookup"><span data-stu-id="d2f63-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="d2f63-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="d2f63-774">RandomNum</span></span>
<span data-ttu-id="d2f63-775">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-775">**Description:**</span></span>  
<span data-ttu-id="d2f63-776">Hello функция RandomNum возвращает случайное число из указанного интервала.</span><span class="sxs-lookup"><span data-stu-id="d2f63-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="d2f63-777">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="d2f63-778">Начать: номер идентификации hello нижний предел toogenerate случайное значение hello</span><span class="sxs-lookup"><span data-stu-id="d2f63-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="d2f63-779">конец: номер идентификации hello верхний предел toogenerate случайное значение hello</span><span class="sxs-lookup"><span data-stu-id="d2f63-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="d2f63-780">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="d2f63-781">Может вернуть значение 734.</span><span class="sxs-lookup"><span data-stu-id="d2f63-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="d2f63-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="d2f63-782">RemoveDuplicates</span></span>
<span data-ttu-id="d2f63-783">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-783">**Description:**</span></span>  
<span data-ttu-id="d2f63-784">Hello функция RemoveDuplicates принимает многозначную строку и убедитесь, что каждое значение является уникальным.</span><span class="sxs-lookup"><span data-stu-id="d2f63-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="d2f63-785">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="d2f63-786">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="d2f63-787">Возвращает очищенный атрибут proxyAddress, в котором удалены все повторяющиеся значения.</span><span class="sxs-lookup"><span data-stu-id="d2f63-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="d2f63-788">Замените</span><span class="sxs-lookup"><span data-stu-id="d2f63-788">Replace</span></span>
<span data-ttu-id="d2f63-789">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-789">**Description:**</span></span>  
<span data-ttu-id="d2f63-790">Hello функция Replace заменяет все вхождения строки tooanother строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="d2f63-791">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="d2f63-792">Строка: tooreplace строка значений.</span><span class="sxs-lookup"><span data-stu-id="d2f63-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="d2f63-793">OldValue: hello toosearch строку для и tooreplace.</span><span class="sxs-lookup"><span data-stu-id="d2f63-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="d2f63-794">Новое значение: hello tooreplace строка для.</span><span class="sxs-lookup"><span data-stu-id="d2f63-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="d2f63-795">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-795">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-796">функции Hello распознает следующие специальные моникеры hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="d2f63-797">\n — новая строка;</span><span class="sxs-lookup"><span data-stu-id="d2f63-797">\n – New Line</span></span>
* <span data-ttu-id="d2f63-798">\r — возврат каретки;</span><span class="sxs-lookup"><span data-stu-id="d2f63-798">\r – Carriage Return</span></span>
* <span data-ttu-id="d2f63-799">\t – символ табуляции.</span><span class="sxs-lookup"><span data-stu-id="d2f63-799">\t – Tab</span></span>

<span data-ttu-id="d2f63-800">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="d2f63-801">Заменяет CRLF запятую и пробел и может вызвать слишком «Один Microsoft способом, Редмонд, штат Вашингтон, США»</span><span class="sxs-lookup"><span data-stu-id="d2f63-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="d2f63-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="d2f63-802">ReplaceChars</span></span>
<span data-ttu-id="d2f63-803">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-803">**Description:**</span></span>  
<span data-ttu-id="d2f63-804">Hello функция ReplaceChars заменяет все вхождения символов в строке ReplacePattern hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="d2f63-805">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="d2f63-806">Строка: tooreplace строка символов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="d2f63-807">ReplacePattern: строка, содержащая словарь с tooreplace символов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="d2f63-808">Hello формат: {source1}: {target1}, {source2}: {target2}, {sourceN}: {targetN} где hello символ toofind и целевой hello строка tooreplace с исходной.</span><span class="sxs-lookup"><span data-stu-id="d2f63-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="d2f63-809">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-809">**Remarks:**</span></span>

* <span data-ttu-id="d2f63-810">функция Hello принимает каждое вхождение каждого исходного и заменяет их символом hello целевых объектов.</span><span class="sxs-lookup"><span data-stu-id="d2f63-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="d2f63-811">Hello источник должен иметь ровно один символ (Юникод).</span><span class="sxs-lookup"><span data-stu-id="d2f63-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="d2f63-812">Hello источником не может быть пустым или содержать больше одного символа (Ошибка синтаксического анализа).</span><span class="sxs-lookup"><span data-stu-id="d2f63-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="d2f63-813">Hello целевая служба может иметь несколько символов, например ö, β: ss.</span><span class="sxs-lookup"><span data-stu-id="d2f63-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="d2f63-814">Hello цель может быть пустым, указывающее на то, что символ hello должны быть удалены.</span><span class="sxs-lookup"><span data-stu-id="d2f63-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="d2f63-815">Источник Hello с учетом регистра и должны точно совпадать.</span><span class="sxs-lookup"><span data-stu-id="d2f63-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="d2f63-816">Привет, (запятая) и: (двоеточие) зарезервированы и не может быть заменен с использованием этой функции.</span><span class="sxs-lookup"><span data-stu-id="d2f63-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="d2f63-817">Пробелы и другие пробельные символы в hello строки ReplacePattern игнорируются.</span><span class="sxs-lookup"><span data-stu-id="d2f63-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="d2f63-818">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="d2f63-819">Возвращает значение Raksmorgas.</span><span class="sxs-lookup"><span data-stu-id="d2f63-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="d2f63-820">Возвращает «oneil "; hello такт имеет определенный toobe удалены.</span><span class="sxs-lookup"><span data-stu-id="d2f63-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="d2f63-821">Right</span><span class="sxs-lookup"><span data-stu-id="d2f63-821">Right</span></span>
<span data-ttu-id="d2f63-822">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-822">**Description:**</span></span>  
<span data-ttu-id="d2f63-823">Hello функция Right возвращает указанное количество символов из hello вправо (конец) строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="d2f63-824">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="d2f63-825">строки: hello tooreturn символов строки из</span><span class="sxs-lookup"><span data-stu-id="d2f63-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="d2f63-826">NumChars: число, задающее количество hello tooreturn символов из hello конец (справа) строки</span><span class="sxs-lookup"><span data-stu-id="d2f63-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="d2f63-827">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-827">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-828">Возвращает NumChars символов начиная с последней позиции hello строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="d2f63-829">Строка, содержащая последние numChars символов hello в строке:</span><span class="sxs-lookup"><span data-stu-id="d2f63-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="d2f63-830">если numChars = 0, возвращается пустая строка;</span><span class="sxs-lookup"><span data-stu-id="d2f63-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="d2f63-831">если numChars < 0, возвращается введенная строка;</span><span class="sxs-lookup"><span data-stu-id="d2f63-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="d2f63-832">если строка имеет значение Null, возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-832">If string is null, return empty string.</span></span>

<span data-ttu-id="d2f63-833">Если строка содержит меньше символов, чем число NumChars hello, возвращается toostring одинаковые строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="d2f63-834">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="d2f63-835">Возвращает значение Doe.</span><span class="sxs-lookup"><span data-stu-id="d2f63-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="d2f63-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="d2f63-836">RTrim</span></span>
<span data-ttu-id="d2f63-837">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-837">**Description:**</span></span>  
<span data-ttu-id="d2f63-838">Hello функция RTrim удаляет конечные пробелы из строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="d2f63-839">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="d2f63-840">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="d2f63-841">Возвращает значение Test.</span><span class="sxs-lookup"><span data-stu-id="d2f63-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="d2f63-842">Выберите пункт</span><span class="sxs-lookup"><span data-stu-id="d2f63-842">Select</span></span>
<span data-ttu-id="d2f63-843">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-843">**Description:**</span></span>  
<span data-ttu-id="d2f63-844">Обработка всех значений атрибута с несколькими значениями (или выходного значения выражения) в соответствии с указанной функцией.</span><span class="sxs-lookup"><span data-stu-id="d2f63-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="d2f63-845">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="d2f63-846">элемент: представляет элемент в многозначном атрибуте hello</span><span class="sxs-lookup"><span data-stu-id="d2f63-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="d2f63-847">атрибут: hello многозначный атрибут</span><span class="sxs-lookup"><span data-stu-id="d2f63-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="d2f63-848">expression: выражение, возвращающее коллекцию значений</span><span class="sxs-lookup"><span data-stu-id="d2f63-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="d2f63-849">условие: любая функция, которая может обрабатывать элемента в атрибуте hello</span><span class="sxs-lookup"><span data-stu-id="d2f63-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="d2f63-850">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="d2f63-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="d2f63-851">Возврат всех значений hello в многозначном атрибуте телефон hello, после удаления дефисы (-).</span><span class="sxs-lookup"><span data-stu-id="d2f63-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="d2f63-852">разделение;</span><span class="sxs-lookup"><span data-stu-id="d2f63-852">Split</span></span>
<span data-ttu-id="d2f63-853">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-853">**Description:**</span></span>  
<span data-ttu-id="d2f63-854">Hello функция Split принимает строку с разделителями и делает его многозначную строку.</span><span class="sxs-lookup"><span data-stu-id="d2f63-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="d2f63-855">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="d2f63-856">значение: hello строку с tooseparate символ разделителя.</span><span class="sxs-lookup"><span data-stu-id="d2f63-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="d2f63-857">разделитель: один символ toobe используется как разделитель hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="d2f63-858">limit: максимальное количество значений, которые могут быть возвращены.</span><span class="sxs-lookup"><span data-stu-id="d2f63-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="d2f63-859">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="d2f63-860">Возвращает многозначную строку с двумя элементами, полезные для атрибута proxyAddress hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="d2f63-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="d2f63-861">StringFromGuid</span></span>
<span data-ttu-id="d2f63-862">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-862">**Description:**</span></span>  
<span data-ttu-id="d2f63-863">Hello функция StringFromGuid принимает двоичный идентификатор GUID и преобразует его в строку tooa</span><span class="sxs-lookup"><span data-stu-id="d2f63-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="d2f63-864">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="d2f63-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="d2f63-865">StringFromSid</span></span>
<span data-ttu-id="d2f63-866">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-866">**Description:**</span></span>  
<span data-ttu-id="d2f63-867">Hello функция StringFromSid преобразует массив байтов, содержащий строку tooa идентификатора безопасности.</span><span class="sxs-lookup"><span data-stu-id="d2f63-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="d2f63-868">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="d2f63-869">Switch</span><span class="sxs-lookup"><span data-stu-id="d2f63-869">Switch</span></span>
<span data-ttu-id="d2f63-870">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-870">**Description:**</span></span>  
<span data-ttu-id="d2f63-871">функция Switch Hello — tooreturn используется одно значение в соответствии с результатом проверки условий.</span><span class="sxs-lookup"><span data-stu-id="d2f63-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="d2f63-872">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="d2f63-873">expr: выражение типа Variant, которое должно tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="d2f63-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="d2f63-874">значение: toobe значение возвращаемое, если hello соответствующее выражение имеет значение True.</span><span class="sxs-lookup"><span data-stu-id="d2f63-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="d2f63-875">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-875">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-876">Здравствуйте, аргумент функции Switch состоит из пар выражений и значений.</span><span class="sxs-lookup"><span data-stu-id="d2f63-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="d2f63-877">Hello выражения вычисляются из левой tooright и возвращается значение hello, связанное с hello первого выражения tooevaluate tooTrue.</span><span class="sxs-lookup"><span data-stu-id="d2f63-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="d2f63-878">Если hello составлены неправильно, возникает ошибка времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="d2f63-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="d2f63-879">Например, если expr1 имеет значение True, функция Switch возвращает value1.</span><span class="sxs-lookup"><span data-stu-id="d2f63-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="d2f63-880">Если expr-1 имеет значение False, а expr-2 — True функция Switch возвращает значение value-2 и т. д.</span><span class="sxs-lookup"><span data-stu-id="d2f63-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="d2f63-881">Функция Switch возвращает Nothing при таких условиях:</span><span class="sxs-lookup"><span data-stu-id="d2f63-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="d2f63-882">Ни одно из выражений hello имеют значение True.</span><span class="sxs-lookup"><span data-stu-id="d2f63-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="d2f63-883">Hello первое значение True, выражение имеет соответствующее значение, равное Null.</span><span class="sxs-lookup"><span data-stu-id="d2f63-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="d2f63-884">Функция Switch вычисляет все выражения, хотя возвращает только одно из них.</span><span class="sxs-lookup"><span data-stu-id="d2f63-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="d2f63-885">Поэтому необходимо следить за нежелательными побочными эффектами.</span><span class="sxs-lookup"><span data-stu-id="d2f63-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="d2f63-886">Например если вычисление hello любого выражения происходит деление на ноль, возвращается ошибка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="d2f63-887">Значение может быть также hello ошибки функции, которая возвращает настраиваемую строку.</span><span class="sxs-lookup"><span data-stu-id="d2f63-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="d2f63-888">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="d2f63-889">Возвращает язык hello в некоторых основных городов, в противном случае возвращает ошибку.</span><span class="sxs-lookup"><span data-stu-id="d2f63-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="d2f63-890">Trim</span><span class="sxs-lookup"><span data-stu-id="d2f63-890">Trim</span></span>
<span data-ttu-id="d2f63-891">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-891">**Description:**</span></span>  
<span data-ttu-id="d2f63-892">функция Trim Hello удаляет начальные и конечные пробелы из строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="d2f63-893">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="d2f63-894">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="d2f63-895">Возвращает значение Test.</span><span class="sxs-lookup"><span data-stu-id="d2f63-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="d2f63-896">Удаляет начальные и конечные пробелы для каждого значения атрибута proxyAddress hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="d2f63-897">UCase</span><span class="sxs-lookup"><span data-stu-id="d2f63-897">UCase</span></span>
<span data-ttu-id="d2f63-898">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-898">**Description:**</span></span>  
<span data-ttu-id="d2f63-899">Hello функция UCase преобразует все символы в случае tooupper строки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="d2f63-900">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="d2f63-901">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="d2f63-902">Возвращает значение Test.</span><span class="sxs-lookup"><span data-stu-id="d2f63-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="d2f63-903">Where</span><span class="sxs-lookup"><span data-stu-id="d2f63-903">Where</span></span>

<span data-ttu-id="d2f63-904">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-904">**Description:**</span></span>  
<span data-ttu-id="d2f63-905">Возвращает подмножество значений атрибута с несколькими значениями (или выходного значения выражения) в соответствии с указанным условием.</span><span class="sxs-lookup"><span data-stu-id="d2f63-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="d2f63-906">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="d2f63-907">элемент: представляет элемент в многозначном атрибуте hello</span><span class="sxs-lookup"><span data-stu-id="d2f63-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="d2f63-908">атрибут: hello многозначный атрибут</span><span class="sxs-lookup"><span data-stu-id="d2f63-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="d2f63-909">условие: любое выражение, которое может быть вычислено tootrue или false</span><span class="sxs-lookup"><span data-stu-id="d2f63-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="d2f63-910">expression: выражение, возвращающее коллекцию значений</span><span class="sxs-lookup"><span data-stu-id="d2f63-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="d2f63-911">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="d2f63-912">Возвращаемые значения сертификата hello в многозначном атрибуте userCertificate hello, которой не истек срок действия.</span><span class="sxs-lookup"><span data-stu-id="d2f63-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="d2f63-913">With</span><span class="sxs-lookup"><span data-stu-id="d2f63-913">With</span></span>
<span data-ttu-id="d2f63-914">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-914">**Description:**</span></span>  
<span data-ttu-id="d2f63-915">Hello с функцией предоставляет toosimplify способом сложное выражение с помощью переменной toorepresent часть выражения, которая отображается один или более раз в hello сложного выражения.</span><span class="sxs-lookup"><span data-stu-id="d2f63-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="d2f63-916">**Синтаксис:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="d2f63-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="d2f63-917">переменная: представляет hello части выражения.</span><span class="sxs-lookup"><span data-stu-id="d2f63-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="d2f63-918">subExpression: часть выражения, представленная переменной.</span><span class="sxs-lookup"><span data-stu-id="d2f63-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="d2f63-919">complexExpression: сложное выражение.</span><span class="sxs-lookup"><span data-stu-id="d2f63-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="d2f63-920">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="d2f63-921">Функционально эквивалентно следующему:</span><span class="sxs-lookup"><span data-stu-id="d2f63-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="d2f63-922">В атрибуте userCertificate hello, которая возвращает только значения с неистекшим сроком действия сертификата.</span><span class="sxs-lookup"><span data-stu-id="d2f63-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="d2f63-923">Word</span><span class="sxs-lookup"><span data-stu-id="d2f63-923">Word</span></span>
<span data-ttu-id="d2f63-924">**Описание.**</span><span class="sxs-lookup"><span data-stu-id="d2f63-924">**Description:**</span></span>  
<span data-ttu-id="d2f63-925">Hello функция Word возвращает слово, содержащееся в строки, с учетом параметров, описывающих toouse разделители hello и номеров tooreturn слово hello.</span><span class="sxs-lookup"><span data-stu-id="d2f63-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="d2f63-926">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d2f63-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="d2f63-927">строки: hello слова из строки tooreturn.</span><span class="sxs-lookup"><span data-stu-id="d2f63-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="d2f63-928">WordNumber: число, определяющее количество слов, которые должны быть возвращены.</span><span class="sxs-lookup"><span data-stu-id="d2f63-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="d2f63-929">разделители: строка, представляющая delimiter(s) hello, следует использовать tooidentify слова</span><span class="sxs-lookup"><span data-stu-id="d2f63-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="d2f63-930">**Примечания:**</span><span class="sxs-lookup"><span data-stu-id="d2f63-930">**Remarks:**</span></span>  
<span data-ttu-id="d2f63-931">Каждая строка символов строки, разделенные одним из символов hello в разделители hello идентифицируются как слов:</span><span class="sxs-lookup"><span data-stu-id="d2f63-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="d2f63-932">если number < 1, возвращается пустая строка;</span><span class="sxs-lookup"><span data-stu-id="d2f63-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="d2f63-933">если string имеет значение Null, возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="d2f63-934">Если строка содержит меньше слов, чем number, или строка не содержит слов, идентифицируемых с помощью разделителей, возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="d2f63-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="d2f63-935">**Пример**</span><span class="sxs-lookup"><span data-stu-id="d2f63-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="d2f63-936">Возвращает значение "brown".</span><span class="sxs-lookup"><span data-stu-id="d2f63-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="d2f63-937">Вернет значение "has".</span><span class="sxs-lookup"><span data-stu-id="d2f63-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2f63-938">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d2f63-938">Additional Resources</span></span>
* [<span data-ttu-id="d2f63-939">Знакомство с выражениями декларативной подготовки.</span><span class="sxs-lookup"><span data-stu-id="d2f63-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="d2f63-940">Azure AD Connect Sync: настройка параметров синхронизации</span><span class="sxs-lookup"><span data-stu-id="d2f63-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="d2f63-941">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2f63-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
