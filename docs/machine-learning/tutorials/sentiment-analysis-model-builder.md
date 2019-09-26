---
title: 教程：分析情绪 - 二元分类
description: 本教程演示如何创建 Razor Pages 应用程序，该应用程序对网站评论情绪进行分类并采取适当的措施。 二元情绪分类器使用 Visual Studio 中的模型生成器。
ms.date: 09/13/2019
author: luisquintanilla
ms.author: luquinta
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: c6184e097daf4604173db9e2a34606e68eb0fdc8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054272"
---
# <a name="tutorial-analyze-sentiment-of-website-comments-in-a-web-application-using-mlnet-model-builder"></a><span data-ttu-id="a692d-104">教程：使用 ML.NET 模型生成器在 Web 应用程序中分析网站评论的情绪</span><span class="sxs-lookup"><span data-stu-id="a692d-104">Tutorial: Analyze sentiment of website comments in a web application using ML.NET Model Builder</span></span>

<span data-ttu-id="a692d-105">了解如何在 Web 应用程序中实时分析评论中的情绪。</span><span class="sxs-lookup"><span data-stu-id="a692d-105">Learn how to analyze sentiment from comments in real-time inside a web application.</span></span>

<span data-ttu-id="a692d-106">本教程演示如何创建 ASP.NET Core Razor Pages 应用程序，该应用程序实时对网站评论情绪进行分类并采取适当的措施。</span><span class="sxs-lookup"><span data-stu-id="a692d-106">This tutorial shows you how to create an ASP.NET Core Razor Pages application that classifies sentiment from website comments in real-time.</span></span>

<span data-ttu-id="a692d-107">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="a692d-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a692d-108">创建 ASP.NET Core Razor Pages 应用程序</span><span class="sxs-lookup"><span data-stu-id="a692d-108">Create an ASP.NET Core Razor Pages application</span></span>
> * <span data-ttu-id="a692d-109">准备和了解数据</span><span class="sxs-lookup"><span data-stu-id="a692d-109">Prepare and understand the data</span></span>
> * <span data-ttu-id="a692d-110">选择方案</span><span class="sxs-lookup"><span data-stu-id="a692d-110">Choose a scenario</span></span>
> * <span data-ttu-id="a692d-111">加载数据</span><span class="sxs-lookup"><span data-stu-id="a692d-111">Load the data</span></span>
> * <span data-ttu-id="a692d-112">定型模型</span><span class="sxs-lookup"><span data-stu-id="a692d-112">Train the model</span></span>
> * <span data-ttu-id="a692d-113">评估模型</span><span class="sxs-lookup"><span data-stu-id="a692d-113">Evaluate the model</span></span>
> * <span data-ttu-id="a692d-114">使用预测模型</span><span class="sxs-lookup"><span data-stu-id="a692d-114">Use the model for predictions</span></span>

> [!NOTE]
> <span data-ttu-id="a692d-115">模型生成器当前为预览版。</span><span class="sxs-lookup"><span data-stu-id="a692d-115">Model Builder is currently in Preview.</span></span>

<span data-ttu-id="a692d-116">可以在 [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples) 存储库中找到本教程的源代码。</span><span class="sxs-lookup"><span data-stu-id="a692d-116">You can find the source code for this tutorial at the [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples) repository.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="a692d-117">先决条件</span><span class="sxs-lookup"><span data-stu-id="a692d-117">Pre-requisites</span></span>

<span data-ttu-id="a692d-118">请访问[模型生成器安装指南](../how-to-guides/install-model-builder.md)，查看先决条件和安装说明的列表。</span><span class="sxs-lookup"><span data-stu-id="a692d-118">For a list of pre-requisites and installation instructions, visit the [Model Builder installation guide](../how-to-guides/install-model-builder.md).</span></span>

## <a name="create-a-razor-pages-application"></a><span data-ttu-id="a692d-119">创建 Razor Pages 应用程序</span><span class="sxs-lookup"><span data-stu-id="a692d-119">Create a Razor Pages application</span></span>

1. <span data-ttu-id="a692d-120">创建 ASP.NET Core Razor Pages 应用程序  。</span><span class="sxs-lookup"><span data-stu-id="a692d-120">Create a **ASP.NET Core Razor Pages Application**.</span></span>

    1. <span data-ttu-id="a692d-121">打开 Visual Studio 并从菜单栏中选择“文件”>“新建”>“项目”  。</span><span class="sxs-lookup"><span data-stu-id="a692d-121">Open Visual Studio and select **File > New > Project** from the menu bar.</span></span> 
    1. <span data-ttu-id="a692d-122">在“新项目”对话框中，依次选择“Visual C#”  节点和“Web”  节点。</span><span class="sxs-lookup"><span data-stu-id="a692d-122">In the New Project dialog, select the **Visual C#** node followed by the **Web** node.</span></span> 
    1. <span data-ttu-id="a692d-123">然后，选择“ASP.NET Core Web 应用程序”  项目模板。</span><span class="sxs-lookup"><span data-stu-id="a692d-123">Then select the **ASP.NET Core Web Application** project template.</span></span> 
    1. <span data-ttu-id="a692d-124">在“名称”  文本框中，键入“SentimentRazor”。</span><span class="sxs-lookup"><span data-stu-id="a692d-124">In the **Name** text box, type "SentimentRazor".</span></span>
    1. <span data-ttu-id="a692d-125">默认情况下，应选中“创建解决方案的目录”  复选框。</span><span class="sxs-lookup"><span data-stu-id="a692d-125">The **Create a directory for solution** checkbox should be checked by default.</span></span> <span data-ttu-id="a692d-126">如果未选中，请将其选中。</span><span class="sxs-lookup"><span data-stu-id="a692d-126">If that's not the case, check it.</span></span> 
    1. <span data-ttu-id="a692d-127">选择“确定”  按钮。</span><span class="sxs-lookup"><span data-stu-id="a692d-127">Select the **OK** button.</span></span>
    1. <span data-ttu-id="a692d-128">在显示不同类型 ASP.NET Core 项目的窗口中，选择“Web 应用程序”  ，然后选择“确定”  按钮。</span><span class="sxs-lookup"><span data-stu-id="a692d-128">Choose **Web Application** in the window that displays the different types of ASP.NET Core Projects, and then select the **OK** button.</span></span>

## <a name="prepare-and-understand-the-data"></a><span data-ttu-id="a692d-129">准备和了解数据</span><span class="sxs-lookup"><span data-stu-id="a692d-129">Prepare and understand the data</span></span>

<span data-ttu-id="a692d-130">下载[维基百科 detox 数据集](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv)。</span><span class="sxs-lookup"><span data-stu-id="a692d-130">Download [Wikipedia detox dataset](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv).</span></span> <span data-ttu-id="a692d-131">打开网页时，右键单击页面，选择“另存为”  ，将文件保存到计算机上的任何位置。</span><span class="sxs-lookup"><span data-stu-id="a692d-131">When the webpage opens, right-click on the page, select **Save As** and save the file anywhere on your computer.</span></span> 

<span data-ttu-id="a692d-132">wikipedia-detox-250-line-data.tsv  数据集中的每一行都代表一个用户在维基百科上留下的不同评价。</span><span class="sxs-lookup"><span data-stu-id="a692d-132">Each row in the *wikipedia-detox-250-line-data.tsv* dataset represents a different review left by a user on Wikipedia.</span></span> <span data-ttu-id="a692d-133">第一列表示文本的情绪（0 表示 non-toxic (无害)，1 表示 toxic (不良)），第二列表示用户留下的评论。</span><span class="sxs-lookup"><span data-stu-id="a692d-133">The first column represents the sentiment of the text (0 is non-toxic, 1 is toxic), and the second column represents the comment left by the user.</span></span> <span data-ttu-id="a692d-134">列由制表符分隔。</span><span class="sxs-lookup"><span data-stu-id="a692d-134">The columns are separated by tabs.</span></span> <span data-ttu-id="a692d-135">数据类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="a692d-135">The data looks like the following:</span></span>

| <span data-ttu-id="a692d-136">情绪</span><span class="sxs-lookup"><span data-stu-id="a692d-136">Sentiment</span></span> | <span data-ttu-id="a692d-137">情绪文本</span><span class="sxs-lookup"><span data-stu-id="a692d-137">SentimentText</span></span> |
| :---: | :---: |
<span data-ttu-id="a692d-138">1</span><span class="sxs-lookup"><span data-stu-id="a692d-138">1</span></span> | <span data-ttu-id="a692d-139">==RUDE== Dude, you are rude upload that carl picture back, or else.</span><span class="sxs-lookup"><span data-stu-id="a692d-139">==RUDE== Dude, you are rude upload that carl picture back, or else.</span></span>
<span data-ttu-id="a692d-140">1</span><span class="sxs-lookup"><span data-stu-id="a692d-140">1</span></span> | <span data-ttu-id="a692d-141">== OK!</span><span class="sxs-lookup"><span data-stu-id="a692d-141">== OK!</span></span> <span data-ttu-id="a692d-142">==  IM GOING TO VANDALIZE WILD ONES WIKI THEN!!!</span><span class="sxs-lookup"><span data-stu-id="a692d-142">==  IM GOING TO VANDALIZE WILD ONES WIKI THEN!!!</span></span>
<span data-ttu-id="a692d-143">0</span><span class="sxs-lookup"><span data-stu-id="a692d-143">0</span></span> | <span data-ttu-id="a692d-144">我希望这会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="a692d-144">I hope this helps.</span></span>

## <a name="choose-a-scenario"></a><span data-ttu-id="a692d-145">选择方案</span><span class="sxs-lookup"><span data-stu-id="a692d-145">Choose a scenario</span></span>

![](./media/sentiment-analysis-model-builder/model-builder-screen.png)

<span data-ttu-id="a692d-146">为了训练模型，需要从模型生成器提供的可用机器学习方案列表中进行选择。</span><span class="sxs-lookup"><span data-stu-id="a692d-146">To train your model, you need to select from the list of available machine learning scenarios provided by Model Builder.</span></span> 

1. <span data-ttu-id="a692d-147">在“解决方案资源管理器”中，右键单击“SentimentRazor”项目，然后选择“添加” > “机器学习”     。</span><span class="sxs-lookup"><span data-stu-id="a692d-147">In **Solution Explorer**, right-click the *SentimentRazor* project, and select **Add** > **Machine Learning**.</span></span>
1. <span data-ttu-id="a692d-148">对于本示例，方案为情绪分析。</span><span class="sxs-lookup"><span data-stu-id="a692d-148">For this sample, the scenario is sentiment analysis.</span></span> <span data-ttu-id="a692d-149">在模型生成器工具的“方案”步骤中，选择“情绪分析”方案   。</span><span class="sxs-lookup"><span data-stu-id="a692d-149">In the *scenario* step of the Model Builder tool, select the **Sentiment Analysis** scenario.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="a692d-150">加载数据</span><span class="sxs-lookup"><span data-stu-id="a692d-150">Load the data</span></span>

<span data-ttu-id="a692d-151">模型生成器接受来自两个源的数据：SQL Server 数据库或者 `csv` 或 `tsv` 格式的本地文件。</span><span class="sxs-lookup"><span data-stu-id="a692d-151">Model Builder accepts data from two sources, a SQL Server database or a local file in `csv` or `tsv` format.</span></span>

1. <span data-ttu-id="a692d-152">在模型生成器工具的数据步骤中，选择数据源下拉列表中的“文件”  。</span><span class="sxs-lookup"><span data-stu-id="a692d-152">In the data step of the Model Builder tool, select **File** from the data source dropdown.</span></span>
1. <span data-ttu-id="a692d-153">选择“选择文件”文本框旁边的按钮，并使用文件资源管理器浏览到 wikipedia-detox-250-line-data.tsv 文件，然后选择该文件   。</span><span class="sxs-lookup"><span data-stu-id="a692d-153">Select the button next to the **Select a file** text box and use File Explorer to browse and select the *wikipedia-detox-250-line-data.tsv* file.</span></span>
1. <span data-ttu-id="a692d-154">在“要预测的标签或列”下拉列表中选择“情绪”  </span><span class="sxs-lookup"><span data-stu-id="a692d-154">Choose **Sentiment** in the **Label or Column to Predict** dropdown</span></span>
1. <span data-ttu-id="a692d-155">选择“训练”  链接以转到模型生成器工具中的下一步。</span><span class="sxs-lookup"><span data-stu-id="a692d-155">Select the **Train** link to move to the next step in the Model Builder tool.</span></span>

## <a name="train-the-model"></a><span data-ttu-id="a692d-156">定型模型</span><span class="sxs-lookup"><span data-stu-id="a692d-156">Train the model</span></span>

<span data-ttu-id="a692d-157">在本教程中，用于训练价格预测模型的机器学习任务是二元分类。</span><span class="sxs-lookup"><span data-stu-id="a692d-157">The machine learning task used to train the price prediction model in this tutorial is binary classification.</span></span> <span data-ttu-id="a692d-158">在模型训练过程中，模型生成器使用不同的二元分类算法和设置训练各个模型，以便为数据集找到性能最佳的模型。</span><span class="sxs-lookup"><span data-stu-id="a692d-158">During the model training process, Model Builder trains separate models using different binary classification algorithms and settings to find the best performing model for your dataset.</span></span>

<span data-ttu-id="a692d-159">模型训练所需的时间与数据量成正比。</span><span class="sxs-lookup"><span data-stu-id="a692d-159">The time required for the model to train is proportionate to the amount of data.</span></span> <span data-ttu-id="a692d-160">模型生成器会根据数据源的大小自动选择“训练时间(秒)”的默认值  。</span><span class="sxs-lookup"><span data-stu-id="a692d-160">Model Builder automatically selects a default value for **Time to train (seconds)** based on the size of your data source.</span></span> 

1. <span data-ttu-id="a692d-161">尽管模型生成器将“训练时间(秒)”  的值设置为 10 秒，但可以将其增加到 30 秒。</span><span class="sxs-lookup"><span data-stu-id="a692d-161">Although Model Builder sets the value of **Time to train (seconds)** to 10 seconds, increase it to 30 seconds.</span></span> <span data-ttu-id="a692d-162">通过较长时间段的训练，模型生成器可以在最佳模型的搜索中浏览更多的算法和参数组合。</span><span class="sxs-lookup"><span data-stu-id="a692d-162">Training for a longer period of time allows Model Builder to explore a larger number of algorithms and combination of parameters in search of the best model.</span></span>
1. <span data-ttu-id="a692d-163">选择“开始训练”  。</span><span class="sxs-lookup"><span data-stu-id="a692d-163">Select **Start Training**.</span></span>

    <span data-ttu-id="a692d-164">在训练过程中，进度数据显示在训练步骤中的 `Progress` 部分。</span><span class="sxs-lookup"><span data-stu-id="a692d-164">Throughout the training process, progress data is displayed in the `Progress` section of the train step.</span></span>

    - <span data-ttu-id="a692d-165">“状态”显示训练进程的完成状态。</span><span class="sxs-lookup"><span data-stu-id="a692d-165">Status displays the completion status of the training process.</span></span>
    - <span data-ttu-id="a692d-166">“最高准确性”显示截至目前由模型生成器找到的性能最佳的模型的准确性。</span><span class="sxs-lookup"><span data-stu-id="a692d-166">Best accuracy displays the accuracy of the best performing model found by Model Builder so far.</span></span> <span data-ttu-id="a692d-167">准确性越高，意味着模型对测试数据的预测越准确。</span><span class="sxs-lookup"><span data-stu-id="a692d-167">Higher accuracy means the model predicted more correctly on test data.</span></span>
    - <span data-ttu-id="a692d-168">“最佳算法”显示截至目前由模型生成器找到的性能最佳的算法的名称。</span><span class="sxs-lookup"><span data-stu-id="a692d-168">Best algorithm displays the name of the best performing algorithm performed found by Model Builder so far.</span></span>
    - <span data-ttu-id="a692d-169">“最新算法”显示模型生成器为了训练模型采用的最新算法名称。</span><span class="sxs-lookup"><span data-stu-id="a692d-169">Last algorithm displays the name of the algorithm most recently used by Model Builder to train the model.</span></span>

1. <span data-ttu-id="a692d-170">训练完成后，选择“评估”  链接以转到下一步。</span><span class="sxs-lookup"><span data-stu-id="a692d-170">Once training is complete, select the **evaluate** link to move to the next step.</span></span>

## <a name="evaluate-the-model"></a><span data-ttu-id="a692d-171">评估模型</span><span class="sxs-lookup"><span data-stu-id="a692d-171">Evaluate the model</span></span>

<span data-ttu-id="a692d-172">训练步骤的成果将是一个模型，该模型具备最佳的性能。</span><span class="sxs-lookup"><span data-stu-id="a692d-172">The result of the training step will be one model which had the best performance.</span></span> <span data-ttu-id="a692d-173">在模型生成器工具的评估步骤中，输出部分将包含“最佳模型”项中性能最佳的模型使用的算法，并包含“最佳模型质量 (RSquared)”中的指标   。</span><span class="sxs-lookup"><span data-stu-id="a692d-173">In the evaluate step of the Model Builder tool, the output section, will contain the algorithm used by the best performing model in the **Best Model** entry along with metrics in **Best Model Quality (RSquared)**.</span></span> <span data-ttu-id="a692d-174">此外还有一个摘要表格，包含性能最佳的前五种模型以及它们的指标信息。</span><span class="sxs-lookup"><span data-stu-id="a692d-174">Additionally, a summary table containing top five models and their metrics.</span></span>

<span data-ttu-id="a692d-175">如果对自己的准确性指标不满意，尝试提高模型准确性的简单方法是增加模型的训练时间或使用更多数据。</span><span class="sxs-lookup"><span data-stu-id="a692d-175">If you're not satisfied with your accuracy metrics, some easy ways to try and improve model accuracy are to increase the amount of time to train the model or use more data.</span></span> <span data-ttu-id="a692d-176">否则，选择“代码”  链接以转到模型生成器工具中的最后一步。</span><span class="sxs-lookup"><span data-stu-id="a692d-176">Otherwise, select the **code** link to move to the final step in the Model Builder tool.</span></span>

## <a name="add-the-code-to-make-predictions"></a><span data-ttu-id="a692d-177">添加代码进行预测</span><span class="sxs-lookup"><span data-stu-id="a692d-177">Add the code to make predictions</span></span>

<span data-ttu-id="a692d-178">训练期间会创建两个项目。</span><span class="sxs-lookup"><span data-stu-id="a692d-178">Two projects will be created as a result of the training process.</span></span>

### <a name="reference-the-trained-model"></a><span data-ttu-id="a692d-179">引用已训练的模型</span><span class="sxs-lookup"><span data-stu-id="a692d-179">Reference the trained model</span></span>

1. <span data-ttu-id="a692d-180">在模型生成器工具的“代码”  步骤中，选择“添加项目”  将自动生成的项目添加到解决方案。</span><span class="sxs-lookup"><span data-stu-id="a692d-180">In the *code* step of the Model Builder tool, select **Add Projects** to add the autogenerated projects to the solution.</span></span>

    <span data-ttu-id="a692d-181">以下项目应出现在解决方案资源管理器  中：</span><span class="sxs-lookup"><span data-stu-id="a692d-181">The following projects should appear in the **Solution Explorer**:</span></span>

    - <span data-ttu-id="a692d-182">*SentimentRazorML.ConsoleApp*：包含模型训练和预测代码的 .NET Core 控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="a692d-182">*SentimentRazorML.ConsoleApp*: A .NET Core Console application that contains the model training and prediction code.</span></span>
    - <span data-ttu-id="a692d-183">*SentimentRazorML.Model*：一个 .NET Standard 类库，包含定义输入和输出模型数据架构的数据模型，以及在训练期间性能最佳的模型的持久版本。</span><span class="sxs-lookup"><span data-stu-id="a692d-183">*SentimentRazorML.Model*: A .NET Standard class library containing the data models that define the schema of input and output model data as well as the persisted version of the best performing model during training.</span></span>

    <span data-ttu-id="a692d-184">对于本教程，只使用 SentimentRazorML.Model  项目，因为预测将在 SentimentRazor  Web 应用程序中（而不是控制台中）进行。</span><span class="sxs-lookup"><span data-stu-id="a692d-184">For this tutorial, only the *SentimentRazorML.Model* project is used because predictions will be made in the *SentimentRazor* web application rather than in the console.</span></span> <span data-ttu-id="a692d-185">尽管 SentimentRazorML.ConsoleApp  不用于评分，但它可用于在以后使用新数据重新训练模型。</span><span class="sxs-lookup"><span data-stu-id="a692d-185">Although the *SentimentRazorML.ConsoleApp* won't be used for scoring, it can be used to retrain the model using new data at a later time.</span></span> <span data-ttu-id="a692d-186">重新训练不属于本教程的讨论范围。</span><span class="sxs-lookup"><span data-stu-id="a692d-186">Retraining is outside the scope of this tutorial though.</span></span>

1. <span data-ttu-id="a692d-187">要在 Razor Pages 应用程序中使用已训练的模型，请添加对 SentimentRazorML.Model  项目的引用。</span><span class="sxs-lookup"><span data-stu-id="a692d-187">To use the trained model inside your Razor Pages application, add a reference to the *SentimentRazorML.Model* project.</span></span>

    1. <span data-ttu-id="a692d-188">右键单击 SentimentRazor  项目。</span><span class="sxs-lookup"><span data-stu-id="a692d-188">Right-click **SentimentRazor** project.</span></span> 
    1. <span data-ttu-id="a692d-189">选择“添加”>“引用”  。</span><span class="sxs-lookup"><span data-stu-id="a692d-189">Select **Add > Reference**.</span></span> 
    1. <span data-ttu-id="a692d-190">选择“项目”>“解决方案”  节点，从列表中选中“SentimentRazorML.Model”  项目。</span><span class="sxs-lookup"><span data-stu-id="a692d-190">Choose the **Projects > Solution** node and from the list, check the **SentimentRazorML.Model** project.</span></span>
    1. <span data-ttu-id="a692d-191">选择“确定”  。</span><span class="sxs-lookup"><span data-stu-id="a692d-191">Select **OK**.</span></span>

### <a name="configure-the-predictionengine-pool"></a><span data-ttu-id="a692d-192">配置 PredictionEngine 池</span><span class="sxs-lookup"><span data-stu-id="a692d-192">Configure the PredictionEngine pool</span></span>

<span data-ttu-id="a692d-193">若要进行单个预测，请使用 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)。</span><span class="sxs-lookup"><span data-stu-id="a692d-193">To make a single prediction, use [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602).</span></span> <span data-ttu-id="a692d-194">要在应用程序中使用 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)，则必须在需要时创建它。</span><span class="sxs-lookup"><span data-stu-id="a692d-194">In order to use [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) in your application, you must create it when it's needed.</span></span> <span data-ttu-id="a692d-195">在这种情况下，可考虑的最佳做法是依赖项注入。</span><span class="sxs-lookup"><span data-stu-id="a692d-195">In that case, a best practice to consider is dependency injection.</span></span>

> [!WARNING]
> <span data-ttu-id="a692d-196">[`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 不是线程安全型。</span><span class="sxs-lookup"><span data-stu-id="a692d-196">[`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) is not thread-safe.</span></span> <span data-ttu-id="a692d-197">为了提高性能和线程安全性，请使用 `PredictionEnginePool` 服务，该服务可创建 `PredictionEngine` 对象的 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) 供应用程序使用。</span><span class="sxs-lookup"><span data-stu-id="a692d-197">For improved performance and thread safety, use the `PredictionEnginePool` service, which creates an [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) of `PredictionEngine` objects for application use.</span></span> <span data-ttu-id="a692d-198">阅读以下博客文章，了解有关[在 ASP.NET Core 中创建和使用 `PredictionEngine` 对象池](https://devblogs.microsoft.com/cesardelatorre/how-to-optimize-and-run-ml-net-models-on-scalable-asp-net-core-webapis-or-web-apps/)的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a692d-198">Read the following blog post to learn more about [creating and using `PredictionEngine` object pools in ASP.NET Core](https://devblogs.microsoft.com/cesardelatorre/how-to-optimize-and-run-ml-net-models-on-scalable-asp-net-core-webapis-or-web-apps/).</span></span> 

1. <span data-ttu-id="a692d-199">安装 Microsoft.Extensions.ML NuGet 包  ：</span><span class="sxs-lookup"><span data-stu-id="a692d-199">Install the *Microsoft.Extensions.ML* NuGet package:</span></span>

    1. <span data-ttu-id="a692d-200">在“解决方案资源管理器”中，右键单击项目，然后选择“管理 NuGet 包”   。</span><span class="sxs-lookup"><span data-stu-id="a692d-200">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span> 
    1. <span data-ttu-id="a692d-201">选择“nuget.org”作为“包源”。</span><span class="sxs-lookup"><span data-stu-id="a692d-201">Choose "nuget.org" as the Package source.</span></span> 
    1. <span data-ttu-id="a692d-202">选择“浏览”  选项卡，搜索“Microsoft.Extensions.ML”  。</span><span class="sxs-lookup"><span data-stu-id="a692d-202">Select the **Browse** tab and search for **Microsoft.Extensions.ML**.</span></span> 
    1. <span data-ttu-id="a692d-203">在列表中选择包，然后选择“安装”  按钮。</span><span class="sxs-lookup"><span data-stu-id="a692d-203">Select the package in the list, and select the **Install** button.</span></span> 
    1. <span data-ttu-id="a692d-204">选择“预览更改”  对话框中的“确定”  按钮</span><span class="sxs-lookup"><span data-stu-id="a692d-204">Select the **OK** button on the **Preview Changes** dialog</span></span>
    1. <span data-ttu-id="a692d-205">如果同意所列包的许可条款，请选择“接受许可”  对话框中的“我接受”  按钮。</span><span class="sxs-lookup"><span data-stu-id="a692d-205">Select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span> 

1. <span data-ttu-id="a692d-206">打开“SentimentRazor”  项目中的“Startup.cs”  文件。</span><span class="sxs-lookup"><span data-stu-id="a692d-206">Open the *Startup.cs* file in the *SentimentRazor* project.</span></span>
1. <span data-ttu-id="a692d-207">添加以下 using 语句以引用 Microsoft.Extensions.ML  NuGet 包和 SentimentRazorML.Model  项目：</span><span class="sxs-lookup"><span data-stu-id="a692d-207">Add the following using statements to reference the *Microsoft.Extensions.ML* NuGet package and *SentimentRazorML.Model* project:</span></span>

    [!code-csharp [StartupUsings](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L12-L14)]        

1. <span data-ttu-id="a692d-208">创建全局变量以存储已训练模型文件的位置。</span><span class="sxs-lookup"><span data-stu-id="a692d-208">Create a global variable to store the location of the trained model file.</span></span>

    [!code-csharp [ModelPath](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L20)]

1. <span data-ttu-id="a692d-209">模型文件与应用程序的程序集文件一起存储在生成目录中。</span><span class="sxs-lookup"><span data-stu-id="a692d-209">The model file is stored in the build directory alongside the assembly files of your application.</span></span> <span data-ttu-id="a692d-210">为了便于访问，在 `Configure` 方法后创建一个称为 `GetAbsolutePath` 的帮助程序方法</span><span class="sxs-lookup"><span data-stu-id="a692d-210">To make it easier to access, create a helper method called `GetAbsolutePath` after the `Configure` method</span></span>

    [!code-csharp [GetAbsolutePathMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L66-L73)]

1. <span data-ttu-id="a692d-211">使用 `Startup` 类构造函数中的 `GetAbsolutePath` 方法来设置 `_modelPath`。</span><span class="sxs-lookup"><span data-stu-id="a692d-211">Use the `GetAbsolutePath` method in the `Startup` class constructor to set the `_modelPath`.</span></span>

    [!code-csharp [InitModelPath](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L25)]

1. <span data-ttu-id="a692d-212">在 `ConfigureServices` 方法中为应用程序配置 `PredictionEnginePool`：</span><span class="sxs-lookup"><span data-stu-id="a692d-212">Configure the `PredictionEnginePool` for your application in the `ConfigureServices` method:</span></span>

    [!code-csharp [InitPredEnginePool](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L42)]

### <a name="create-sentiment-analysis-handler"></a><span data-ttu-id="a692d-213">创建情绪分析处理程序</span><span class="sxs-lookup"><span data-stu-id="a692d-213">Create sentiment analysis handler</span></span>

<span data-ttu-id="a692d-214">预测将在应用程序的主页内进行。</span><span class="sxs-lookup"><span data-stu-id="a692d-214">Predictions will be made inside the main page of the application.</span></span> <span data-ttu-id="a692d-215">因此，需要添加一个采用用户输入并使用 `PredictionEnginePool` 来返回预测的方法。</span><span class="sxs-lookup"><span data-stu-id="a692d-215">Therefore, a method that takes the user input and uses the `PredictionEnginePool` to return a prediction needs to be added.</span></span>

1. <span data-ttu-id="a692d-216">打开位于 *Pages* 目录中的 Index.cshtml.cs  文件，并添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="a692d-216">Open the *Index.cshtml.cs* file located in the *Pages* directory and add the following using statements:</span></span>

    [!code-csharp [IndexUsings](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L7-L8)]

    <span data-ttu-id="a692d-217">要使用 `Startup` 类中已配置的 `PredictionEnginePool`，必须将它插入到要在其中使用它的模型的构造函数中。</span><span class="sxs-lookup"><span data-stu-id="a692d-217">In order to use the `PredictionEnginePool` configured in the `Startup` class, you have to inject it into the constructor of the model where you want to use it.</span></span> 

1. <span data-ttu-id="a692d-218">添加变量以引用 `IndexModel` 类中的 `PredictionEnginePool`。</span><span class="sxs-lookup"><span data-stu-id="a692d-218">Add a variable to reference the `PredictionEnginePool` inside the `IndexModel` class.</span></span>

    [!code-csharp [PredEnginePool](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L14)]

1. <span data-ttu-id="a692d-219">在 `IndexModel` 类中创建一个构造函数，并将 `PredictionEnginePool` 服务注入到其中。</span><span class="sxs-lookup"><span data-stu-id="a692d-219">Create a constructor in the `IndexModel` class and inject the `PredictionEnginePool` service into it.</span></span>

    [!code-csharp [IndexConstructor](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L16-L19)]

1. <span data-ttu-id="a692d-220">创建一个方法处理程序，该处理程序使用 `PredictionEnginePool` 来对从网页接收的用户输入进行预测。</span><span class="sxs-lookup"><span data-stu-id="a692d-220">Create a method handler that uses the `PredictionEnginePool` to make predictions from user input received from the web page.</span></span>

    1. <span data-ttu-id="a692d-221">在 `OnGet` 方法下面，创建一个名为 `OnGetAnalyzeSentiment` 的新方法</span><span class="sxs-lookup"><span data-stu-id="a692d-221">Below the `OnGet` method, create a new method called `OnGetAnalyzeSentiment`</span></span>

        ```csharp
        public IActionResult OnGetAnalyzeSentiment([FromQuery] string text)
        {

        }
        ```

    1. <span data-ttu-id="a692d-222">在 `OnGetAnalyzeSentiment` 方法中，如果用户输入为空或为 null，则返回“中性”情绪  。</span><span class="sxs-lookup"><span data-stu-id="a692d-222">Inside the `OnGetAnalyzeSentiment` method, return *Neutral* sentiment if the input from the user is blank or null.</span></span>

        [!code-csharp [InitInput](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L28)] 
    
    1. <span data-ttu-id="a692d-223">给定有效的输入，创建新的 `ModelInput` 实例。</span><span class="sxs-lookup"><span data-stu-id="a692d-223">Given a valid input, create a new instance of `ModelInput`.</span></span> 

        [!code-csharp [InitInput](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L29)] 

    1. <span data-ttu-id="a692d-224">使用 `PredictionEnginePool` 预测情绪。</span><span class="sxs-lookup"><span data-stu-id="a692d-224">Use the `PredictionEnginePool` to predict sentiment.</span></span>

        [!code-csharp [MakePrediction](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L30)] 

    1. <span data-ttu-id="a692d-225">使用以下代码将预测的 `bool` 值转换为“toxic”或“not toxic”。</span><span class="sxs-lookup"><span data-stu-id="a692d-225">Convert the predicted `bool` value into toxic or not toxic with the following code.</span></span>

        [!code-csharp [ConvertPrediction](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L31)]

    1. <span data-ttu-id="a692d-226">最后，将情绪返回到网页上。</span><span class="sxs-lookup"><span data-stu-id="a692d-226">Finally, return the sentiment back to the web page.</span></span>

        [!code-csharp [ReturnSentiment](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L32)]

### <a name="configure-the-web-page"></a><span data-ttu-id="a692d-227">配置网页</span><span class="sxs-lookup"><span data-stu-id="a692d-227">Configure the web page</span></span>

<span data-ttu-id="a692d-228">`OnGetAnalyzeSentiment` 返回的结果将在 `Index` 网页上动态显示。</span><span class="sxs-lookup"><span data-stu-id="a692d-228">The results returned by the `OnGetAnalyzeSentiment` will be dynamically displayed on the `Index` web page.</span></span>

1. <span data-ttu-id="a692d-229">在“Pages”  目录中打开 Index.cshtml  文件，并将其内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="a692d-229">Open the *Index.cshtml* file in the *Pages* directory and replace its contents with the following code:</span></span> 

    [!code-cshtml [IndexPage](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml)]

1. <span data-ttu-id="a692d-230">接下来，将 css 样式代码添加到 wwwroot\css  目录中的 site.css  页面的末尾：</span><span class="sxs-lookup"><span data-stu-id="a692d-230">Next, add css styling code to the end of the *site.css* page in the *wwwroot\css* directory:</span></span>

    [!code-css [CssStyling](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/css/site.css#L61-L105)]

1. <span data-ttu-id="a692d-231">然后，添加代码，将源自网页的输入发送到 `OnGetAnalyzeSentiment` 处理程序。</span><span class="sxs-lookup"><span data-stu-id="a692d-231">After that, add code to send inputs from the web page to the `OnGetAnalyzeSentiment` handler.</span></span>

    1. <span data-ttu-id="a692d-232">在 wwwroot\js  目录中的 site.js  文件中，创建名为 `getSentiment` 的函数，以便向 `OnGetAnalyzeSentiment` 处理程序的用户输入发出 GET HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="a692d-232">In the *site.js* file located in the *wwwroot\js* directory, create a function called `getSentiment` to make a GET HTTP request with the user input to the `OnGetAnalyzeSentiment` handler.</span></span>

        [!code-javascript [GetSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L5-L10)]

    1. <span data-ttu-id="a692d-233">在它的下面，添加另一个名为 `updateMarker` 的函数，以便在预测情绪时，动态更新网页上标记的位置。</span><span class="sxs-lookup"><span data-stu-id="a692d-233">Below that, add another function called `updateMarker` to dynamically update the position of the marker on the web page as sentiment is predicted.</span></span>

        [!code-javascript [UpdateMarkerMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L12-L15)]

    1. <span data-ttu-id="a692d-234">创建一个名为 `updateSentiment` 的事件处理程序函数以获取用户的输入，使用 `getSentiment` 函数将其发送到 `OnGetAnalyzeSentiment` 函数，并使用 `updateMarker` 函数更新标记。</span><span class="sxs-lookup"><span data-stu-id="a692d-234">Create an event handler function called `updateSentiment` to get the input from the user, send it to the `OnGetAnalyzeSentiment` function using the `getSentiment` function and update the marker with the `updateMarker` function.</span></span>

        [!code-javascript [UpdateSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L17-L34)]

    1. <span data-ttu-id="a692d-235">最后，注册事件处理程序并将其绑定到具有 `id=Message` 特性的 `textarea` 元素。</span><span class="sxs-lookup"><span data-stu-id="a692d-235">Finally, register the event handler and bind it to the `textarea` element with the `id=Message` attribute.</span></span>

        [!code-javascript [UpdateSentimentEvtHandler](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L36)]

## <a name="run-the-application"></a><span data-ttu-id="a692d-236">运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="a692d-236">Run the application</span></span>

<span data-ttu-id="a692d-237">既然应用程序已设置，请运行应在浏览器中启动的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a692d-237">Now that your application is set up, run the application which should launch in your browser.</span></span>

<span data-ttu-id="a692d-238">当应用程序启动时，在文本区域中输入“Model Builder is cool!” </span><span class="sxs-lookup"><span data-stu-id="a692d-238">When the application launches, enter *Model Builder is cool!*</span></span> <span data-ttu-id="a692d-239">。</span><span class="sxs-lookup"><span data-stu-id="a692d-239">into the text area.</span></span> <span data-ttu-id="a692d-240">显示的预测情绪应为“Not Toxic”  。</span><span class="sxs-lookup"><span data-stu-id="a692d-240">The predicted sentiment displayed should be *Not Toxic*.</span></span>

![](./media/sentiment-analysis-model-builder/web-app.png)

<span data-ttu-id="a692d-241">如果稍后需要在另一个解决方案中引用模型生成器生成的项目，可以在 `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` 目录中找到它们。</span><span class="sxs-lookup"><span data-stu-id="a692d-241">If you need to reference the Model Builder generated projects at a later time inside of another solution, you can find them inside the `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a692d-242">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a692d-242">Next steps</span></span>

<span data-ttu-id="a692d-243">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="a692d-243">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a692d-244">创建 ASP.NET Core Razor Pages 应用程序</span><span class="sxs-lookup"><span data-stu-id="a692d-244">Create an ASP.NET Core Razor Pages application</span></span>
> * <span data-ttu-id="a692d-245">准备和了解数据</span><span class="sxs-lookup"><span data-stu-id="a692d-245">Prepare and understand the data</span></span>
> * <span data-ttu-id="a692d-246">选择方案</span><span class="sxs-lookup"><span data-stu-id="a692d-246">Choose a scenario</span></span>
> * <span data-ttu-id="a692d-247">加载数据</span><span class="sxs-lookup"><span data-stu-id="a692d-247">Load the data</span></span>
> * <span data-ttu-id="a692d-248">定型模型</span><span class="sxs-lookup"><span data-stu-id="a692d-248">Train the model</span></span>
> * <span data-ttu-id="a692d-249">评估模型</span><span class="sxs-lookup"><span data-stu-id="a692d-249">Evaluate the model</span></span>
> * <span data-ttu-id="a692d-250">使用预测模型</span><span class="sxs-lookup"><span data-stu-id="a692d-250">Use the model for predictions</span></span>

### <a name="additional-resources"></a><span data-ttu-id="a692d-251">其他资源</span><span class="sxs-lookup"><span data-stu-id="a692d-251">Additional Resources</span></span>

<span data-ttu-id="a692d-252">若要详细了解本教程中所述的主题，请访问以下资源:</span><span class="sxs-lookup"><span data-stu-id="a692d-252">To learn more about topics mentioned in this tutorial, visit the following resources:</span></span>

- [<span data-ttu-id="a692d-253">模型生成器应用场景</span><span class="sxs-lookup"><span data-stu-id="a692d-253">Model Builder Scenarios</span></span>](../automate-training-with-model-builder.md#scenarios)
- [<span data-ttu-id="a692d-254">二元分类</span><span class="sxs-lookup"><span data-stu-id="a692d-254">Binary Classification</span></span>](../resources/glossary.md#binary-classification)
- [<span data-ttu-id="a692d-255">二元分类模型指标</span><span class="sxs-lookup"><span data-stu-id="a692d-255">Binary Classification Model Metrics</span></span>](../resources/metrics.md#metrics-for-binary-classification)