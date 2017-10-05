---
title: "Azure AD Connect: выражения декларативной подготовки | Документация Майкрософт"
description: "Описание выражений декларативной подготовки."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e3a03a97b10e04fb85261620879b2102e1db8465
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a><span data-ttu-id="00557-103">Служба синхронизации Azure AD Connect: общие сведения о выражениях декларативной подготовки</span><span class="sxs-lookup"><span data-stu-id="00557-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span></span>
<span data-ttu-id="00557-104">Служба синхронизации Azure AD Connect основана на принципах декларативной подготовки, впервые представленной в Forefront Identity Manager 2010.</span><span class="sxs-lookup"><span data-stu-id="00557-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span></span> <span data-ttu-id="00557-105">Эта функция позволяет реализовать бизнес-логику интеграции идентификации без необходимости написания компилируемого кода.</span><span class="sxs-lookup"><span data-stu-id="00557-105">It allows you to implement your complete identity integration business logic without the need to write compiled code.</span></span>

<span data-ttu-id="00557-106">Важной частью декларативной подготовки является язык выражений, используемый в потоке атрибутов.</span><span class="sxs-lookup"><span data-stu-id="00557-106">An essential part of declarative provisioning is the expression language used in attribute flows.</span></span> <span data-ttu-id="00557-107">Это подмножество Microsoft® Visual Basic® для приложений (VBA).</span><span class="sxs-lookup"><span data-stu-id="00557-107">The language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span></span> <span data-ttu-id="00557-108">Этот язык используется в Microsoft Office и знаком пользователи, имеющим опыт работы с VBScript.</span><span class="sxs-lookup"><span data-stu-id="00557-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span></span> <span data-ttu-id="00557-109">Язык выражений декларативной подготовки не структурированный и использует только функции,</span><span class="sxs-lookup"><span data-stu-id="00557-109">The Declarative Provisioning Expression Language is only using functions and is not a structured language.</span></span> <span data-ttu-id="00557-110">но не методы или инструкции.</span><span class="sxs-lookup"><span data-stu-id="00557-110">There are no methods or statements.</span></span> <span data-ttu-id="00557-111">Вместо этого функции вложены в поток программы.</span><span class="sxs-lookup"><span data-stu-id="00557-111">Functions are instead nested to express program flow.</span></span>

<span data-ttu-id="00557-112">Подробнее об этом см. в статье [Справочник по языку Office VBA](https://msdn.microsoft.com/library/gg264383.aspx).</span><span class="sxs-lookup"><span data-stu-id="00557-112">For more details, see [Welcome to the Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span></span>

<span data-ttu-id="00557-113">Атрибуты являются строго типизированными.</span><span class="sxs-lookup"><span data-stu-id="00557-113">The attributes are strongly typed.</span></span> <span data-ttu-id="00557-114">Функция принимает только атрибуты правильного типа.</span><span class="sxs-lookup"><span data-stu-id="00557-114">A function only accepts attributes of the correct type.</span></span> <span data-ttu-id="00557-115">Регистр символов также учитывается.</span><span class="sxs-lookup"><span data-stu-id="00557-115">It is also case-sensitive.</span></span> <span data-ttu-id="00557-116">Имена функций и атрибутов должны указываться с учетом регистра, иначе произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="00557-116">Both function names and attribute names must have proper casing or an error is thrown.</span></span>

## <a name="language-definitions-and-identifiers"></a><span data-ttu-id="00557-117">Определения и идентификаторы языка</span><span class="sxs-lookup"><span data-stu-id="00557-117">Language definitions and Identifiers</span></span>
* <span data-ttu-id="00557-118">У функции есть имя, за которым следует список аргументов в скобках: имя_функции(аргумент 1, аргумент N).</span><span class="sxs-lookup"><span data-stu-id="00557-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span></span>
* <span data-ttu-id="00557-119">Атрибуты заключаются в квадратные скобки: [имя_атрибута].</span><span class="sxs-lookup"><span data-stu-id="00557-119">Attributes are identified by square brackets: [attributeName]</span></span>
* <span data-ttu-id="00557-120">Параметры задаются знаком процента: %имя_параметра%.</span><span class="sxs-lookup"><span data-stu-id="00557-120">Parameters are identified by percent signs: %ParameterName%</span></span>
* <span data-ttu-id="00557-121">Строковые константы заключаются в кавычки, например "Contoso" (обратите внимание, что необходимо использовать прямые (""), а не парные (“”) кавычки).</span><span class="sxs-lookup"><span data-stu-id="00557-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span></span>
* <span data-ttu-id="00557-122">Числовые значения приводятся без кавычек; они считаются десятичными.</span><span class="sxs-lookup"><span data-stu-id="00557-122">Numeric values are expressed without quotes and expected to be decimal.</span></span> <span data-ttu-id="00557-123">Шестнадцатеричные значения должны иметь префикс &H.</span><span class="sxs-lookup"><span data-stu-id="00557-123">Hexadecimal values are prefixed with &H.</span></span> <span data-ttu-id="00557-124">Например, 98052, &HFF.</span><span class="sxs-lookup"><span data-stu-id="00557-124">For example, 98052, &HFF</span></span>
* <span data-ttu-id="00557-125">Логические значения выражаются константами True и False.</span><span class="sxs-lookup"><span data-stu-id="00557-125">Boolean values are expressed with constants: True, False.</span></span>
* <span data-ttu-id="00557-126">Встроенные константы и литералы выражаются только своим именем: NULL, CRLF, IgnoreThisFlow.</span><span class="sxs-lookup"><span data-stu-id="00557-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span></span>

### <a name="functions"></a><span data-ttu-id="00557-127">Functions</span><span class="sxs-lookup"><span data-stu-id="00557-127">Functions</span></span>
<span data-ttu-id="00557-128">Декларативная подготовка использует множество функций для преобразования значений атрибутов.</span><span class="sxs-lookup"><span data-stu-id="00557-128">Declarative provisioning uses many functions to enable the possibility to transform attribute values.</span></span> <span data-ttu-id="00557-129">Эти функции могут быть вложенными, так что результат из одной функции передается в другую функцию.</span><span class="sxs-lookup"><span data-stu-id="00557-129">These functions can be nested so the result from one function is passed in to another function.</span></span>

`Function1(Function2(Function3()))`

<span data-ttu-id="00557-130">Полный список функций можно найти в [справочнике по функциям](active-directory-aadconnectsync-functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="00557-130">The complete list of functions can be found in the [function reference](active-directory-aadconnectsync-functions-reference.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="00557-131">Параметры</span><span class="sxs-lookup"><span data-stu-id="00557-131">Parameters</span></span>
<span data-ttu-id="00557-132">Параметр задается соединителем или администратором с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00557-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span></span> <span data-ttu-id="00557-133">Обычно параметры содержат значения, которые отличаются в разных системах, например имя домена, в котором находится пользователь.</span><span class="sxs-lookup"><span data-stu-id="00557-133">Parameters usually contain values that are different from system to system, for example the name of the domain the user is located in.</span></span> <span data-ttu-id="00557-134">Эти параметры могут использоваться в потоках атрибутов.</span><span class="sxs-lookup"><span data-stu-id="00557-134">These parameters can be used in attribute flows.</span></span>

<span data-ttu-id="00557-135">Соединитель Active Directory предоставляет следующие параметры для входящих правил синхронизации.</span><span class="sxs-lookup"><span data-stu-id="00557-135">The Active Directory Connector provided the following parameters for inbound Synchronization Rules:</span></span>

| <span data-ttu-id="00557-136">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="00557-136">Parameter Name</span></span> | <span data-ttu-id="00557-137">Комментарий</span><span class="sxs-lookup"><span data-stu-id="00557-137">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="00557-138">Domain.Netbios</span><span class="sxs-lookup"><span data-stu-id="00557-138">Domain.Netbios</span></span> |<span data-ttu-id="00557-139">Формат NetBIOS импортируемого домена, например FABRIKAMSALES</span><span class="sxs-lookup"><span data-stu-id="00557-139">Netbios format of the domain currently being imported, for example FABRIKAMSALES</span></span> |
| <span data-ttu-id="00557-140">Domain.FQDN</span><span class="sxs-lookup"><span data-stu-id="00557-140">Domain.FQDN</span></span> |<span data-ttu-id="00557-141">Формат FQDN импортируемого домена, например sales.fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="00557-141">FQDN format of the domain currently being imported, for example sales.fabrikam.com</span></span> |
| <span data-ttu-id="00557-142">Domain.LDAP</span><span class="sxs-lookup"><span data-stu-id="00557-142">Domain.LDAP</span></span> |<span data-ttu-id="00557-143">Формат LDAP импортируемого домена, например DC=sales,DC=fabrikam,DC=com</span><span class="sxs-lookup"><span data-stu-id="00557-143">LDAP format of the domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span></span> |
| <span data-ttu-id="00557-144">Forest.Netbios</span><span class="sxs-lookup"><span data-stu-id="00557-144">Forest.Netbios</span></span> |<span data-ttu-id="00557-145">Формат NetBIOS импортируемого имени леса, например FABRIKAMCORP</span><span class="sxs-lookup"><span data-stu-id="00557-145">Netbios format of the forest name currently being imported, for example FABRIKAMCORP</span></span> |
| <span data-ttu-id="00557-146">Forest.FQDN</span><span class="sxs-lookup"><span data-stu-id="00557-146">Forest.FQDN</span></span> |<span data-ttu-id="00557-147">Формат FQDN импортируемого имени леса, например fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="00557-147">FQDN format of the forest name currently being imported, for example fabrikam.com</span></span> |
| <span data-ttu-id="00557-148">Forest.LDAP</span><span class="sxs-lookup"><span data-stu-id="00557-148">Forest.LDAP</span></span> |<span data-ttu-id="00557-149">Формат LDAP импортируемого имени леса, например DC=fabrikam,DC=com</span><span class="sxs-lookup"><span data-stu-id="00557-149">LDAP format of the forest name currently being imported, for example DC=fabrikam,DC=com</span></span> |

<span data-ttu-id="00557-150">Система предоставляет следующий параметр, который используется для получения идентификатора запущенного соединителя:</span><span class="sxs-lookup"><span data-stu-id="00557-150">The system provides the following parameter, which is used to get the identifier of the Connector currently running:</span></span>  
`Connector.ID`

<span data-ttu-id="00557-151">Ниже приведен пример, где атрибут метавселенной domain заполнен NetBIOS-именем домена, в котором расположен пользователь.</span><span class="sxs-lookup"><span data-stu-id="00557-151">Here is an example that populates the metaverse attribute domain with the netbios name of the domain where the user is located:</span></span>  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a><span data-ttu-id="00557-152">Операторы</span><span class="sxs-lookup"><span data-stu-id="00557-152">Operators</span></span>
<span data-ttu-id="00557-153">Могут использоваться следующие операторы.</span><span class="sxs-lookup"><span data-stu-id="00557-153">The following operators can be used:</span></span>

* <span data-ttu-id="00557-154">**Сравнение**: <, <=, <>, =, >, >=</span><span class="sxs-lookup"><span data-stu-id="00557-154">**Comparison**: <, <=, <>, =, >, >=</span></span>
* <span data-ttu-id="00557-155">**Математические**: +, -, \*, -</span><span class="sxs-lookup"><span data-stu-id="00557-155">**Mathematics**: +, -, \*, -</span></span>
* <span data-ttu-id="00557-156">**Строковые**: & (сцепление)</span><span class="sxs-lookup"><span data-stu-id="00557-156">**String**: & (concatenate)</span></span>
* <span data-ttu-id="00557-157">**Логические**: && (и), || (или)</span><span class="sxs-lookup"><span data-stu-id="00557-157">**Logical**: && (and), || (or)</span></span>
* <span data-ttu-id="00557-158">**Порядок вычисления**: ( )</span><span class="sxs-lookup"><span data-stu-id="00557-158">**Evaluation order**: ( )</span></span>

<span data-ttu-id="00557-159">Операторы выполняются в порядке слева направо и имеют одинаковый приоритет вычисления.</span><span class="sxs-lookup"><span data-stu-id="00557-159">Operators are evaluated left to right and have the same evaluation priority.</span></span> <span data-ttu-id="00557-160">Это значит, что умножение (\*) не вычисляется до вычитания (–).</span><span class="sxs-lookup"><span data-stu-id="00557-160">That is, the \* (multiplier) is not evaluated before - (subtraction).</span></span> <span data-ttu-id="00557-161">2\*(5+3) не равно 2\*5+3.</span><span class="sxs-lookup"><span data-stu-id="00557-161">2\*(5+3) is not the same as 2\*5+3.</span></span> <span data-ttu-id="00557-162">Скобки () используются, чтобы изменить порядок вычислений, когда порядок вычислений слева направо не подходит.</span><span class="sxs-lookup"><span data-stu-id="00557-162">The brackets ( ) are used to change the evaluation order when left to right evaluation order isn't appropriate.</span></span>

## <a name="multi-valued-attributes"></a><span data-ttu-id="00557-163">Многозначные атрибуты</span><span class="sxs-lookup"><span data-stu-id="00557-163">Multi-valued attributes</span></span>
<span data-ttu-id="00557-164">Функции могут работать с однозначными и многозначными атрибутами.</span><span class="sxs-lookup"><span data-stu-id="00557-164">The functions can operate on both single-valued and multi-valued attributes.</span></span> <span data-ttu-id="00557-165">Для многозначных атрибутов функция работает с каждым отдельным значением и применяет одну и ту же функцию к каждому отдельному значению.</span><span class="sxs-lookup"><span data-stu-id="00557-165">For multi-valued attributes, the function operates over every value and applies the same function to every value.</span></span>

<span data-ttu-id="00557-166">Например, </span><span class="sxs-lookup"><span data-stu-id="00557-166">For example:</span></span>  
<span data-ttu-id="00557-167">`Trim([proxyAddresses])` выполняет обрезку (Trim) для каждого значения атрибута proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="00557-167">`Trim([proxyAddresses])` Do a Trim of every value in the proxyAddress attribute.</span></span>  
<span data-ttu-id="00557-168">`Word([proxyAddresses],1,"@") & "@contoso.com"`Для каждого значения с @-sign, замените домен с @contoso.com.</span><span class="sxs-lookup"><span data-stu-id="00557-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace the domain with @contoso.com.</span></span>  
<span data-ttu-id="00557-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Найдите SIP-адрес и удалите его из значений.</span><span class="sxs-lookup"><span data-stu-id="00557-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for the SIP-address and remove it from the values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00557-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="00557-170">Next steps</span></span>
* <span data-ttu-id="00557-171">Дополнительные сведения о модели конфигурации, см. в статье о [принципах декларативной подготовки](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="00557-171">Read more about the configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="00557-172">Примеры стандартного использования декларативной подготовки см. в статье [Службы синхронизации Azure AD Connect: рекомендации по изменению конфигурации по умолчанию](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="00557-172">See how declarative provisioning is used out-of-box in [Understanding the default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
* <span data-ttu-id="00557-173">Инструкции по практическим изменениям с помощью декларативной подготовки см. в статье [Службы синхронизации Azure AD Connect: изменение конфигурации по умолчанию](active-directory-aadconnectsync-change-the-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="00557-173">See how to make a practical change using declarative provisioning in [How to make a change to the default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="00557-174">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="00557-174">**Overview topics**</span></span>

* [<span data-ttu-id="00557-175">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="00557-175">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="00557-176">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00557-176">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<span data-ttu-id="00557-177">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="00557-177">**Reference topics**</span></span>

* [<span data-ttu-id="00557-178">Синхронизация Azure AD Connect: справочник по функциям</span><span class="sxs-lookup"><span data-stu-id="00557-178">Azure AD Connect sync: Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md)

