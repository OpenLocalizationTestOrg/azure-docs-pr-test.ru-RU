---
ms.assetid: 
title: "Системы безопасности Azure Key Vault | Документация Майкрософт"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 921bbd109c9ea98d8b5c286a7512bed026412d26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="3925b-102">Системы безопасности и географические ограничения Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3925b-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="3925b-103">Azure Key Vault —это мультитенантная служба, которая использует пул аппаратных модулей безопасности в каждом расположении Azure.</span><span class="sxs-lookup"><span data-stu-id="3925b-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="3925b-104">Все аппаратные модули безопасности в расположениях Azure в одном регионе совместно используют одни и те же криптографические ограничения (системы безопасности Thales).</span><span class="sxs-lookup"><span data-stu-id="3925b-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="3925b-105">Например, Восток США и Запад США совместно используют одну и ту же систему безопасности, так как они принадлежат к географическому местоположению "США".</span><span class="sxs-lookup"><span data-stu-id="3925b-105">For example, East US and West US share the same security world because they belong to the US geo location.</span></span> <span data-ttu-id="3925b-106">Аналогичным образом, все местоположения Azure в Японии совместно используют одну и ту же систему безопасности и все локации Azure в Австралии, Индии и т. д.</span><span class="sxs-lookup"><span data-stu-id="3925b-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="3925b-107">Поведение резервного копирования и восстановления</span><span class="sxs-lookup"><span data-stu-id="3925b-107">Backup and restore behavior</span></span>

<span data-ttu-id="3925b-108">Резервную копия ключа из хранилища ключей в одном расположении Azure можно восстановить ​​в хранилище ключей в другом расположении Azure при соблюдении обоих условий:</span><span class="sxs-lookup"><span data-stu-id="3925b-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="3925b-109">Оба расположения Azure принадлежат одному географическому расположению.</span><span class="sxs-lookup"><span data-stu-id="3925b-109">Both of the Azure locations belong to the same geographical location</span></span>
- <span data-ttu-id="3925b-110">Оба хранилища ключей принадлежат одной подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="3925b-110">Both of the key vaults belong to the same Azure subscription</span></span>

<span data-ttu-id="3925b-111">Например, резервную копию ключа, полученную с помощью данной подписки в хранилище ключей в западной Индии, можно восстановить ​​только в другом хранилище ключей в той же подписке и том же географическом расположении: западной Индии, центральной Индии или южной Индии.</span><span class="sxs-lookup"><span data-stu-id="3925b-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="3925b-112">Регионы и продукты</span><span class="sxs-lookup"><span data-stu-id="3925b-112">Regions and products</span></span>

- [<span data-ttu-id="3925b-113">Регионы Azure</span><span class="sxs-lookup"><span data-stu-id="3925b-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="3925b-114">Доступность продуктов по регионам</span><span class="sxs-lookup"><span data-stu-id="3925b-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="3925b-115">Регионы, которые сопоставлены с системами безопасности, выделены как заголовки в таблицах.</span><span class="sxs-lookup"><span data-stu-id="3925b-115">Regions are mapped to security worlds, shown as major headings in the tables:</span></span>

<span data-ttu-id="3925b-116">В статье "Доступность продуктов по регионам", например, вкладка **Америка** содержит регионы "Восток США", "Центральная часть США" и "Запад США", которые сопоставлены с регионом "Америка".</span><span class="sxs-lookup"><span data-stu-id="3925b-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="3925b-117">Исключением являются восточная часть США (US DOD) и центральная часть США (US DOD), которые имеют собственные системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="3925b-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="3925b-118">Аналогично Северная и Западная Европа на вкладке **Европа** сопоставляются с регионом "Европа".</span><span class="sxs-lookup"><span data-stu-id="3925b-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span></span> <span data-ttu-id="3925b-119">Это также касается вкладки **Азиатско-Тихоокеанский регион**.</span><span class="sxs-lookup"><span data-stu-id="3925b-119">The same is also true on the **Asia Pacific** tab.</span></span>



