---
layout: post
title:  "大模型-FineTuning模型微调"
tags: 大模型
---

 [OpenAI-FineTuning](https://platform.openai.com/docs/guides/fine-tuning "https://platform.openai.com/docs/guides/fine-tuning")

 [OpenAI-版本更新日志(changelog)](https://platform.openai.com/docs/changelog "https://platform.openai.com/docs/changelog")

 [提示词工程指南](https://platform.openai.com/docs/guides/prompt-engineering "https://platform.openai.com/docs/guides/prompt-engineering")  

 [提示词示例](https://platform.openai.com/docs/examples "https://platform.openai.com/docs/examples")


### 释义：Fine-tuning 模型微调

微调模型能做的，是获得更好的结果和效率（减少费用，减少响应，优化存储）

- 比提示更高质量的结果
- 能够训练比提示所能容纳的更多示例
- 由于提示时间更短而节省的代币 
- 更低的延迟请求

前提知识：你需要知道，每个会话刚开始提供的示例(System prompt)，即是“少量学习”。

微调通过训练比提示中更多的示例来改进小样本学习，让您在大量任务上取得更好的结果。

一旦模型经过微调，您就不需要在提示中提供那么多示例。

这可以节省成本并实现更低延迟的请求。

注：您还可以对微调模型进行微调。


- 这里解释下：Fine-tuning微调会获得更好的效率指什么？

因为其他的微调方式会增加问答字数或增加执行环节，

而Fine-tuning微调后，这些增加字数和环节就可以相应减少了。

- 这里再解释下：其他的微调方式是什么？

1. 提示工程 prompt engineering

   :) 就是国内的知识库功能。

   工作原理：每次提问前将用户数据库内查到的提示文本同时传给大模型.

2. 提示链 prompt chaining

   :) 就是国内的流程编排功能。

   工作原理：将复杂任务分解为多个提示，拆分执行过程。

3. 函数调用 function calling

   :) 就是国内的工具插件。

   工作原理：编写函数，写上函数提示词，AI会根据你的函数提示词，判断是否需要调用你写的函数。

4. 模型精简 distillation

   :) 使用提炼压缩功能，精简后生成一个新的小模型。

   工作原理：以提供需要保留的对话案例为基准，建立基线，根据基线的范围生成一个新的模型。


### 哪些模型可以进行微调？
    

    目前以下模型可以进行微调：
    
    gpt-4o-2024-08-06
    gpt-4o-mini-2024-07-18
    gpt-4-0613
    gpt-3.5-turbo-0125
    gpt-3.5-turbo-1106
    gpt-3.5-turbo-0613


### 何时使用微调

对 OpenAI 文本生成模型进行微调可以使其更好地适用于特定应用，但这需要谨慎投入时间和精力。

我们建议首先尝试使用提示工程、提示链（将复杂任务分解为多个提示）和函数调用来获得良好的结果，

- 主要原因是：

1. 在许多任务中，我们的模型最初可能表现不佳，但只要有正确的用户提示，结果就可以得到改善。 因此可能不需要进行微调。
2. 因为微调需要创建完整的数据集并运行训练作业（因为模型必须使用完整的演示来学习），对提示和其他策略进行迭代的反馈循环比微调迭代要快得多。
3. 在仍然需要微调的情况下，你也可以先尝试下使用初始化的提示词与提示链/工具使用微调。这样也能得你的结果，且影响范围较小。

你可以先看看我们的 [提示工程指南](https://platform.openai.com/docs/guides/prompt-engineering "https://platform.openai.com/docs/guides/prompt-engineering")  提供了一些最有效的策略和战术的背景知识，这些策略和战术无需微调即可获得更好的性能。你可以多试试。


再先看看我们的 [提示示例](https://platform.openai.com/docs/examples "https://platform.openai.com/docs/examples")  


    
    注：一种高级用法是 “展示，而不是讲述” 可以更容易的达到你的目的。
    例：找工作的智能体里，每次回复都将岗位列表与岗位建议展示出来。


常见用例
一些常见的用例可以通过微调来改善结果：

1. 设定风格、基调、格式或其他定性方面
2. 提高产生所需输出的可靠性
3. 纠正无法遵循复杂提示的问题
4. 以特定方式处理许多极端情况
5. 执行一项难以用语言表达的新技能或任务


### 开始微调（Fine-tuning）

一旦您确定微调是正确的解决方案（即您已经尽可能优化了提示并确定了模型仍然存在的问题），

您就需要准备用于训练模型的数据。

您应该创建一组多样化的演示对话，这些对话类似于您在生产中的推理时要求模型响应的对话。


### 准备数据集

聊天格式中的示例可以包含多条具有 AI 角色的消息。

微调期间的默认行为是针对单个示例中的所有 AI 消息进行训练。

要跳过对特定助理消息的微调，可以添加weight字段（权重字段）禁用对该消息的微调，从而允许您控制学习哪些助理消息。

允许的 weight 值当前为 0 或 1。

下面是一些使用weight进行聊天格式的示例。

在这个例子中，我们的目标是创建一个偶尔给出讽刺性回应的聊天机器人，这些是我们可以为数据集创建的三个训练示例（对话）：


    {"messages": [{"role": "system", "content": "Marv is a factual chatbot that is also sarcastic."}, {"role": "user", "content": "What's the capital of France?"}, {"role": "assistant", "content": "Paris", "weight": 0}, {"role": "user", "content": "Can you be more sarcastic?"}, {"role": "assistant", "content": "Paris, as if everyone doesn't know that already.", "weight": 1}]}
    {"messages": [{"role": "system", "content": "Marv is a factual chatbot that is also sarcastic."}, {"role": "user", "content": "Who wrote 'Romeo and Juliet'?"}, {"role": "assistant", "content": "William Shakespeare", "weight": 0}, {"role": "user", "content": "Can you be more sarcastic?"}, {"role": "assistant", "content": "Oh, just some guy named William Shakespeare. Ever heard of him?", "weight": 1}]}
    {"messages": [{"role": "system", "content": "Marv is a factual chatbot that is also sarcastic."}, {"role": "user", "content": "How far is the Moon from Earth?"}, {"role": "assistant", "content": "384,400 kilometers", "weight": 0}, {"role": "user", "content": "Can you be more sarcastic?"}, {"role": "assistant", "content": "Around 384,400 kilometers. Give or take a few, like that really matters.", "weight": 1}]}


我们通常建议在微调之前采用您认为最适合模型的一组说明和提示，并将它们包含在每个训练示例中。

这应该可以让您获得最佳和最通用的结果，

尤其是在您的训练示例相对较少（例如少于 100 个）的情况下。


- 您不能缩短每个示例中重复的指令或提示以节省成本，

否则模型的行为可能会像包含这些指令一样，而不是执行这些指令。

因为模型必须使用完整的演示来学习，而不是指令。


### 检查数据格式

编译数据集后，在创建微调作业之前，检查数据格式非常重要。

为此，我们创建了一个简单的 [Python 脚本](https://cookbook.openai.com/examples/chat_finetuning_data_prep "https://cookbook.openai.com/examples/chat_finetuning_data_prep")    

您可以使用它来查找潜在错误、查看令牌计数并估算微调作业的成本。


### 上传训练文件

验证数据后，需要使用 [Files API](https://platform.openai.com/docs/api-reference/files/create "https://platform.openai.com/docs/api-reference/files/create")   上传文件，以便与微调作业一起使用：

上传文件后，可能需要一些时间来处理。

在处理文件时，您仍然可以创建微调作业，但在文件处理完成之前，它不会启动。

最大文件上传大小为 1 GB，但我们不建议使用该数据量进行微调，

因为您不太可能需要那么大的数据量才能看到改进。




### 创建微调模型

在确保数据集具有正确的数量和结构并上传文件后，下一步是创建微调作业。

我们支持通过微调 UI 或以编程方式创建微调作业。

要使用 OpenAI SDK 启动微调作业，请执行以下操作：
    

    const fineTune = await openai.fineTuning.jobs.create({
        training_file: 'file-abc123',
        model: 'gpt-4o-mini-2024-07-18'
    });



### 使用微调模型


作业完成后，新的模型可以立即使用。推理时使用新的模型名称即可。

在某些情况下，您的模型可能需要几分钟才能准备好处理请求。

如果对模型的请求超时或找不到模型名称，则可能是因为您的模型仍在加载中。

如果发生这种情况，请在几分钟内重试。



### 分析微调后的模型


我们提供在训练过程中计算的以下训练指标：

- training loss 训练损失
- training token accuracy 训练标记准确性
- valid loss 有效损失
- valid token accuracy 有效的令牌准确性


        
        {
            "object": "fine_tuning.job.event",
            "id": "ftevent-abc-123",
            "created_at": 1693582679,
            "level": "info",
            "message": "Step 300/300: training loss=0.15, validation loss=0.27, full validation loss=0.40",
            "data": {
                "step": 300,
                "train_loss": 0.14991648495197296,
                "valid_loss": 0.26569826706596045,
                "total_steps": 300,
                "full_valid_loss": 0.4032616495084362,
                "train_mean_token_accuracy": 0.9444444179534912,
                "valid_mean_token_accuracy": 0.9565217391304348,
                "full_valid_mean_token_accuracy": 0.9089635854341737
            },
            "type": "metrics"
        }