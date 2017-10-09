<span data-ttu-id="43a26-101">Azure будет определить версию hello toouse Python для его виртуальной среды с hello, следуя приоритет:</span><span class="sxs-lookup"><span data-stu-id="43a26-101">Azure will determine hello version of Python toouse for its virtual environment with hello following priority:</span></span>

1. <span data-ttu-id="43a26-102">версия, указанная в runtime.txt в корневой папке hello</span><span class="sxs-lookup"><span data-stu-id="43a26-102">version specified in runtime.txt in hello root folder</span></span>
2. <span data-ttu-id="43a26-103">версия, указанная параметром Python в конфигурации приложения hello web (hello **параметры** > **параметры приложения** колонку для веб-приложения hello портал Azure)</span><span class="sxs-lookup"><span data-stu-id="43a26-103">version specified by Python setting in hello web app configuration (hello **Settings** > **Application Settings** blade for your web app in hello Azure Portal)</span></span>
3. <span data-ttu-id="43a26-104">Python 2.7 — по умолчанию hello, если заданы выше hello</span><span class="sxs-lookup"><span data-stu-id="43a26-104">python-2.7 is hello default if none of hello above are specified</span></span>

<span data-ttu-id="43a26-105">Допустимые значения для hello содержимое</span><span class="sxs-lookup"><span data-stu-id="43a26-105">Valid values for hello contents of</span></span> 

    \runtime.txt

<span data-ttu-id="43a26-106">:</span><span class="sxs-lookup"><span data-stu-id="43a26-106">are:</span></span>

* <span data-ttu-id="43a26-107">python-2.7</span><span class="sxs-lookup"><span data-stu-id="43a26-107">python-2.7</span></span>
* <span data-ttu-id="43a26-108">python-3.4</span><span class="sxs-lookup"><span data-stu-id="43a26-108">python-3.4</span></span>

<span data-ttu-id="43a26-109">Если версия micro hello (третьего знака) указан, то он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="43a26-109">If hello micro version (third digit) is specified, it is ignored.</span></span>

