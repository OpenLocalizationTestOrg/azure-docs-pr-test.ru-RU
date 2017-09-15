
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, the following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through the new Azure portal
-->


1. <span data-ttu-id="d737c-101">Войдите на [портал Azure](https://portal.azure.com/) по адресу http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="d737c-101">Log in to the [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="d737c-102">В заголовке слева щелкните **ПРОСМОТРЕТЬ ВСЕ**.</span><span class="sxs-lookup"><span data-stu-id="d737c-102">In the left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="d737c-103">Отобразится колонка **Обзор** .</span><span class="sxs-lookup"><span data-stu-id="d737c-103">The **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="d737c-104">Найдите и выберите **Серверы SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="d737c-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="d737c-105">Отобразится колонка **Серверы SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="d737c-105">The **SQL servers** blade is displayed.</span></span>
   
    ![Поиск своего сервера Базы данных SQL Azure на портале][b21-FindServerInPortal]
4. <span data-ttu-id="d737c-107">Для удобства щелкните элемент управления "Свернуть" в предыдущей колонке **Обзор** .</span><span class="sxs-lookup"><span data-stu-id="d737c-107">For convenience, click the minimize control on the earlier **Browse** blade.</span></span>
5. <span data-ttu-id="d737c-108">В текстовом поле фильтра начните вводить имя своего сервера.</span><span class="sxs-lookup"><span data-stu-id="d737c-108">In the filter text box, start typing the name of your server.</span></span> <span data-ttu-id="d737c-109">Отобразится строка.</span><span class="sxs-lookup"><span data-stu-id="d737c-109">Your row is displayed.</span></span>
6. <span data-ttu-id="d737c-110">Щелкните строку с вашим сервером.</span><span class="sxs-lookup"><span data-stu-id="d737c-110">Click the row for your server.</span></span> <span data-ttu-id="d737c-111">Отобразится колонка для вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="d737c-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="d737c-112">На колонке вашего сервера нажмите кнопку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="d737c-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="d737c-113">Отобразится колонка **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="d737c-113">The **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="d737c-114">Щелкните пункт **Брандмауэр**.</span><span class="sxs-lookup"><span data-stu-id="d737c-114">Click **Firewall**.</span></span> <span data-ttu-id="d737c-115">Отобразится колонка **Параметры брандмауэра** .</span><span class="sxs-lookup"><span data-stu-id="d737c-115">The **Firewall Settings** blade is displayed.</span></span>
   
    ![Последовательно выберите пункты "Параметры" > "Брандмауэр"][b31-SettingsFirewallNavig]
9. <span data-ttu-id="d737c-117">Щелкните **Добавить IP-адрес клиента**.</span><span class="sxs-lookup"><span data-stu-id="d737c-117">Click **Add Client IP**.</span></span> <span data-ttu-id="d737c-118">В первом текстовом поле введите имя для нового правила.</span><span class="sxs-lookup"><span data-stu-id="d737c-118">Type in a name for your new rule into the first text box.</span></span>
10. <span data-ttu-id="d737c-119">Введите нижнее и верхнее значения IP-адресов для требуемого диапазона.</span><span class="sxs-lookup"><span data-stu-id="d737c-119">Type in the low and high IP address values for the range you want to enable.</span></span>
    
    * <span data-ttu-id="d737c-120">Удобными могут оказаться нижнее значение, оканчивающееся на **.0**, и верхнее — на **.255**.</span><span class="sxs-lookup"><span data-stu-id="d737c-120">It can be handy to have the low value end with **.0** and the high with **.255**.</span></span>
    
    ![Добавьте допустимый диапазон IP-адресов][b41-AddRange]
11. <span data-ttu-id="d737c-122">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d737c-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
