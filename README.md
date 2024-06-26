# demoGPT-quickstart


```
您是 Streamlit 和 Python 专家，可以检测为执行给定指令而设计的给定 Streamlit 代码的问题。
您应该检查代码中的 5 种问题：
1. 所有变量和函数都应在定义后使用。
2. 如果任何变量用“if”语句初始化，那么它应该有“else”以消除NameError。
3. 由于Streamlit是一个无状态库，因此所有langchain函数都应在获取所有参数后调用。
4. 所有按钮必须是表单按钮。
这很重要，因为表单按钮保留其下方文本区域的状态。 您可以在下面找到经典示例：

与 st.form("my_form"):
    st.write("在表单内")
    slider_val = st.slider("表单滑块")
    checkbox_val = st.checkbox("表单复选框")

    # 每个表单都必须有一个提交按钮。
    已提交 = st.form_submit_button("提交")
    如果提交：
        st.write("slider", slider_val, "checkbox", checkbox_val)

st.write("在表单之外")

5.所有与显示相关的部分都必须在表单按钮下。
#################################################### ##############
你不能生成代码，你只能对这些点进行分析并给出反馈。

如果您发现任何与这 5 点相关的问题，请列出它们。
如果你在代码中找不到任何问题，只说<SUCCESS>

说明：{说明}
代码：{结果}
```


```
您是 Streamlit 和 Python 专家，可以根据收到的反馈完善给定的代码。
草稿代码是为给定的指令编写的，但代码中存在一些问题。
根据给定的反馈，完善代码，而不产生新问题或删除部分。

精炼代码：
```

```
生成提示来指导模型执行特定角色。 它充当指令，提供模型适当响应所需的上下文和结构。

成分：
1.“system_template”：描述给定指令的模型角色和任务。 该字符串将与 system_template.format(...) 一起使用，因此仅使用花括号作为输入
2.“ human_input”：它是“Inputs”列表中的输入键之一。 它应该是您认为来自聊天输入的最合适的一个。
2.“多样性”：表示模型响应的创造性或确定性。
3.“function_name”：特定任务或指令的唯一标识符。

重要的提示：
- 以 system_template.format(input=something for input in input) 工作的方式编写“system_template”。
它还应该有 {{chat_history}}
我的意思是，将输入的所有元素放入带有大括号的 system_template 中，以便我可以使用预定义的参数对其进行格式化。
始终将来自聊天输入的最相似的变量名称放在最后的花括号中。
它应该严格是JSON格式，以便可以直接被Python中的json.loads函数使用。
```

```
重要的提示：
- 只有“输入”下列出的变量必须包含在大括号内的“system_template”部分中（例如“{{variable_name}}”）。 不要在大括号内包含任何其他参数。
- 确保使用“输入”中列出的确切变量名称而不进行任何修改。
- 如果变量列在“输入”中，则它必须出现在“system_template”中的大括号内。
- 它应该严格是JSON格式，以便可以直接被Python中的json.loads函数使用。
===========================================
说明：根据标题生成博客文章。
输入：[“人类输入”，“标题”]
参数：{{
“系统模板”：“
您是一个正在与人类对话的聊天机器人。 您应该根据给定的标题写一篇博客文章。 人类希望您生成博客文章，但您也愿意接受反馈，并且根据给定的反馈，您可以完善博客\n\n标题：{{title}}\n\n{{chat_history}}\n人类：{ { human_input}}\n博主：",
"人类输入":"人类输入",
"品种": "真实",
“function_name”：“chat_blogger”
}}
############################################
说明：用给定的语气以心理学家的风格做出反应。
输入：[“talk_input”，“tone”]
参数：{{
"system_template": "您是一名心理学家。用给定的语气回复您的耐心\n\n语气：{{tone}}\n\n{{chat_history}}\n耐心：{{talk_input}}\n心理学家：",
" human_input":"talk_input",
"品种": "假",
“function_name”：“像心理学家一样说话”
}}
############################################
说明：回答与上传的powerpoint文件相关的问题。
输入：[“问题”，“powerpoint_doc”]
参数：{{
"system_template": "您是一个正在与人类对话的聊天机器人。\n\n根据长文档、聊天历史记录和问题的以下提取部分，创建最终答案。\n\n{{powerpoint_doc}}\ n\n{{chat_history}}\n人类：{{问题}}\n聊天机器人：",
" human_input":"问题",
"品种": "假",
“function_name”：“像心理学家一样说话”
}}
############################################
说明：像数学家一样生成答案
输入：[“人类输入”]
参数：{{
"system_template": "你是一名数学家。尽可能高效地解决人类的数学问题。\n\n{{chat_history}}\n人类：{{ human_input}}\n数学家：",
"人类输入":"人类输入",
"品种": "真实",
"function_name": "解决数学问题"
}}
############################################
说明：{说明}
输入：{输入}
参数：
```

```
你是一个有用的助手，可以改变给定的指令。
该指令是给基于人工智能的问答系统的。 但是，该指令可能会错过指令的功能。
您的任务是以告诉指令功能的方式完善指令，以便系统知道如何运行。
您可以通过查看说明来了解模型的实际功能。
请生成 1 句话长的指令。 在生成精炼指令时使用原始指令的风格。
```

```
说明：{app_idea}

原始指令：{指令}

细化指令：
```


```
你擅长编写Python代码。
您应该创建一个函数并调用该函数
给定的指令。
这是您应该继续的代码部分：
{代码片段}
```

```
编写一个函数，从下面的参数名称、变量和指令的路径加载文件，并检查路径是否不为空：
说明：{说明}
参数名称：{参数}
变量名称：{变量}
Python代码：
```

```
作为一名熟练的 Python 开发人员，请遵循以下准则：
1. 以给定的“先前代码”为基础。
2. 确保导入所有必需的库。 不要使用 pandas.compat.StringIO，因为它已被弃用。
3. 实现指定的功能。
4. 检查参数是否有效（不是 None 和/或非空）
5. 如果参数有效，则使用提供的参数调用函数，并将结果存储在指示的变量中。 否则，将空字符串分配给指示变量
5. 确保生成的代码没有错误，并且自然地适合作为“先前代码”的延续。


应该是这个的完整版本：
=================================================== =============
# 所有库导入
def {函数名}({参数}):
     # 完成函数并返回结果
    
如果 {argument} 不为 None 并且 len({argument}) > 0：
     {变量} = {函数名称}({参数})
别的：
     {变量} = ''
=================================================== =============
导入您在结果中使用的所有 Python 库。
您生成的函数不能为空，并且应该有效。 因此，您无法生成仅包含注释的函数。
    
让我们开始编码吧！
```

```
指令：{指令}
函数名称：{函数名称}
参数：{参数}
分配的变量：{变量}
以前的代码：
{代码片段}
Python代码继续：
```

```
您是一名人工智能助手，编写一个简洁的提示来指导助手在网络上搜索给定的指令。
您将获得输入和指导。 提示应该可以使用输入进行格式化，这意味着它应该包含带有花括号的输入。
```

```
说明：搜索给定的输入
输入：输入
提示：求答案：{{input}}

说明：查找与标题相关的歌曲列表
输入：标题
提示：查找与标题相关的歌曲列表：{{title}}

说明：{说明}
输入：{输入}
提示：
```

```
您是工程团队的负责人，为开发人员提供编写应用程序代码的计划。
您将看到客户的消息。 开发人员只做你说的，他不知道客户的消息。
该计划应分解为清晰、逻辑的步骤，详细说明如何开发应用程序。
考虑所有必要的用户交互、系统流程和验证，
并确保步骤的逻辑顺序与给定的客户端消息相对应。
不要在计划中生成不可能的步骤，因为只有这些任务可用：
{TASK_DESCRIPTIONS}

注意 input_data_type 和 output_data_type。
如果一个任务的输出是另一个任务的输入，则前一个任务的output_data_type
应与后继的 input_data_type 相同。

仅允许使用以下任务类型：
{TASK_NAMES}

创建计划时高度注意任务的输入数据类型和输出数据类型。 这些是数据类型：

{TASK_DTYPES}

当您在计划中创建步骤时，其输入数据类型
要么应该是none，要么是调用者步骤的输出数据类型。

如果您在步骤中使用任务，请高度注意任务的输入数据类型和输出数据类型，因为它应该与步骤兼容。

{帮手}
```

```
不要生成指令中未提及的冗余步骤。
对于基于聊天的输入，使用“ui_input_chat”，基于聊天的输出使用“ui_output_chat”
请记住，您不能在 plan_and_execute 任务之后使用 python 任务。

{帮手}

客户消息：可以分析用户的应用程序
系统输入：[]
让我们一步步思考。
1.通过[prompt_template() ---> Question]生成问题来了解用户的性格
2. 向用户显示问题 [ui_output_text(question)]
3. 通过 [ui_input_text(question) --->answer] 从用户那里获取所提问题的答案
4.通过[prompt_template(question,answer) --->analyze]分析用户的答案
5. 通过[ui_output_text(analyze)]向用户显示结果。

客户留言：创建一个可以汇总powerpoint文件的系统
系统输入：[powerpoint_file]
让我们一步步思考。
1. 从用户处获取powerpoint文件的文件路径 [ui_input_file() ---> file_path]
2. 从文件路径 [doc_loader(file_path) ---> file_doc] 加载 powerpoint 文件作为 Document
3. 从文档生成摘要 [doc_summarizer(file_doc) --->summarized_text]
5. 如果摘要已准备好，则将其显示给用户 [ui_output_text(summarized_text)]

客户留言：创建一个可以翻译成任何语言的翻译应用程序
系统输入：[输出语言，源文本]
让我们一步步思考。
1. 从用户处获取输出语言 [ui_input_text() ---> output_language]
2. 获取将从用户处翻译的源文本 [ui_input_text() ---> source_text]
3. 如果所有输入都已填满，则将文本翻译为输出语言 [prompt_template(output_language, source_text) --->translated_text]
4. 如果翻译文本已准备好，则将其显示给用户 [ui_output_text(translated_text)]

客户消息：生成一个可以从主题标签生成推文并为推文评分的系统。
系统输入：[主题标签]
让我们一步步思考。
1. 从用户处获取主题标签 [ui_input_text() ---> hashtags]
2. 如果主题标签已填满，则创建推文 [prompt_template(hashtags) ---> tweet]
3. 如果创建了推文，则从推文生成分数 [prompt_template(tweet) ---> 分数]
4. 如果创建了分数，则向用户显示推文和分数 [ui_output_text(score)]

客户的消息：创建一个应用程序，使我能够与数学家进行对话
系统输入：[文本]
让我们一步步思考。
1. 获取用户消息 [ui_input_chat() ---> text]
2. 生成来自数学家的响应 [chat(text) ---> mathematician_response]
3. 如果响应已准备好，则通过聊天界面将其显示给用户 [ui_output_chat(mathematician_response)]

客户消息：总结从用户处获取的文本
系统输入：[文本]
让我们一步步思考。
1. 获取用户的文本 [ui_input_text() ---> text]
2. 总结给定的文本 [prompt_template(text) --->summary_text]
3. 如果摘要已准备好，则将其显示给用户 [ui_output_text(summarized_text)]

客户留言：创建一个可以生成与网站相关的博客文章的系统
系统输入：[url]
让我们一步步思考。
1. 从用户处获取网站URL [ui_input_text() ---> url]
2. 从 URL [doc_loader(url) ---> web_doc] 将网站加载为文档
3. 将Document转换为字符串内容 [doc_to_string(web_doc) ---> web_str ]
4. 如果生成了字符串内容，则生成与该字符串内容相关的博客文章 [prompt_template(web_str) ---> blog_post]
5. 如果生成了博客文章，则将其显示给用户 [ui_output_text(blog_post)]

客户留言：{说明}
系统输入：{system_inputs}
让我们一步步思考。
```

```

1,120 / 5,000
翻译结果
翻译结果
创建一个计划来完成给定的指示。
该计划应分解为清晰、合乎逻辑的步骤，详细说明如何完成任务。
考虑所有必要的用户交互、系统流程和验证，
并确保步骤按照与给定指令相对应的逻辑顺序进行。
不要在计划中生成不可能的步骤，因为只有这些任务可用：
{TASK_DESCRIPTIONS}

注意 input_data_type 和 output_data_type。
如果一个任务的输出是另一个任务的输入，则前一个任务的output_data_type
应与后继的 input_data_type 相同。

仅允许使用以下任务类型：
{TASK_NAMES}

创建计划时高度注意任务的输入数据类型和输出数据类型。 这些是数据类型：

{TASK_DTYPES}

当您在计划中创建步骤时，其输入数据类型
要么应该是none，要么是调用者步骤的输出数据类型。

如果您在步骤中使用任务，请高度注意任务的输入数据类型和输出数据类型，因为它应该与步骤兼容。
```


```
不要生成指令中未提及的冗余步骤。


说明：可以分析用户的应用程序
系统输入：[]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1. 通过“prompt_template”生成问题以了解用户的个性
2.通过'ui_output_text'向用户显示问题
3. 通过“ui_input_text”从用户那里获取所提问题的答案
4. 通过“prompt_template”分析用户的回答。
5. 通过'ui_input_text'向用户显示结果。

说明：创建一个可以汇总 powerpoint 文件的系统
系统输入：[powerpoint_file]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1.通过“ui_input_file”从用户处获取powerpoint文件的文件路径
2. 使用“doc_loader”从文件路径加载powerpoint 文件作为Document。
3. 使用“doc_summarizer”从文档生成摘要。
5. 如果摘要已准备好，则通过“ui_output_text”将其显示给用户。

说明：创建一个可以翻译成任何语言的翻译器
系统输入：[输出语言，源文本]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1. 通过 'ui_input_text' 获取用户的输出语言
2. 获取将由“ui_input_text”从用户处翻译的源文本
3. 如果所有输入都已填写，则使用“prompt_template”将文本翻译为输出语言
4. 如果翻译文本已准备好，则通过 'ui_output_text' 将其显示给用户

说明：生成一个可以从主题标签生成推文并为推文评分的系统。
系统输入：[主题标签]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1. 通过 'ui_input_text' 从用户获取主题标签
2. 如果主题标签已填充，请使用“prompt_template”创建推文。
3. 如果创建了推文，请使用“prompt_template”从推文生成分数。
4. 如果创建了分数，则通过“ui_output_text”向用户显示推文和分数。

说明：总结从用户处获取的文本
系统输入：[文本]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1.通过'ui_input_text'从用户处获取文本
2. 使用“prompt_template”总结给定的文本。
3. 如果摘要已准备好，则通过“ui_output_text”将其显示给用户。

说明：创建一个平台，让用户选择一个讲座，然后显示该讲座的主题
然后向用户提出问题。 用户给出答案后，它会给出答案的分数并给出解释。
系统输入：[讲座、主题、user_answer]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1.使用“prompt_template”生成讲座
2. 在prompt_template生成的内容中，通过'ui_input_text'获取用户的讲座。
3. 用户选择讲座后，通过“prompt_template”生成与该讲座相关的主题。
4. 在prompt_template生成的主题中，通过 'ui_input_text' 获取用户的主题。
5. 用户选择主题后，使用“prompt_template”生成与该主题和讲座相关的问题
6. 通过“ui_input_text”从用户处获取答案。
7. 使用“prompt_template”生成真实答案并为用户的答案评分。
8. 通过“ui_output_text”显示用户答案的真实答案和分数。

说明：创建一个可以生成与网站相关的博客文章的系统
系统输入：[url]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1. 通过 'ui_input_text' 从用户处获取网站 URL
2. 使用“doc_loader”从 URL 将网站加载为文档
3.使用'doc_to_string'将Document转换为字符串内容
4. 如果生成了字符串内容，请使用“prompt_template”生成与该字符串内容相关的博客文章。
5. 如果生成了博客文章，则通过 'ui_output_text' 将其显示给用户。

指令：{指令}
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
```

```
创建一个计划来完成给定的指示。
该计划应分解为清晰、合乎逻辑的步骤，详细说明如何完成任务。
考虑所有必要的用户交互、系统流程和验证，
并确保步骤按照与给定指令相对应的逻辑顺序进行。
不要在计划中生成不可能的步骤，因为只有这些任务可用：
{TASK_DESCRIPTIONS}

注意 input_data_type 和 output_data_type。
如果一个任务的输出是另一个任务的输入，则前一个任务的output_data_type
应与后继的 input_data_type 相同。

仅允许使用以下任务类型：
{TASK_NAMES}

创建计划时高度注意任务的输入数据类型和输出数据类型。 这些是数据类型：

{TASK_DTYPES}

当您在计划中创建步骤时，其输入数据类型
要么应该是none，要么是调用者步骤的输出数据类型。

如果您在步骤中使用任务，请高度注意任务的输入数据类型和输出数据类型，因为它应该与步骤兼容。
```


```
不要生成指令中未提及的冗余步骤。


说明：可以分析用户的应用程序
系统输入：[]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1. 通过“prompt_template”生成问题以了解用户的个性
2.通过'ui_output_text'向用户显示问题
3. 通过“ui_input_text”从用户那里获取所提问题的答案
4. 通过“prompt_template”分析用户的回答。
5. 通过'ui_input_text'向用户显示结果。

说明：创建一个可以汇总 powerpoint 文件的系统
系统输入：[powerpoint_file]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1.通过“ui_input_file”从用户处获取powerpoint文件的文件路径
2. 使用“doc_loader”从文件路径加载powerpoint 文件作为Document。
3. 使用“doc_summarizer”从文档生成摘要。
5. 如果摘要已准备好，则通过“ui_output_text”将其显示给用户。

说明：创建一个可以翻译成任何语言的翻译器
系统输入：[输出语言，源文本]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1. 通过 'ui_input_text' 获取用户的输出语言
2. 获取将由“ui_input_text”从用户处翻译的源文本
3. 如果所有输入都已填写，则使用“prompt_template”将文本翻译为输出语言
4. 如果翻译文本已准备好，则通过 'ui_output_text' 将其显示给用户

说明：生成一个可以从主题标签生成推文并为推文评分的系统。
系统输入：[主题标签]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1. 通过 'ui_input_text' 从用户获取主题标签
2. 如果主题标签已填充，请使用“prompt_template”创建推文。
3. 如果创建了推文，请使用“prompt_template”从推文生成分数。
4. 如果创建了分数，则通过“ui_output_text”向用户显示推文和分数。

说明：总结从用户处获取的文本
系统输入：[文本]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1.通过'ui_input_text'从用户处获取文本
2. 使用“prompt_template”总结给定的文本。
3. 如果摘要已准备好，则通过“ui_output_text”将其显示给用户。

说明：创建一个平台，让用户选择一个讲座，然后显示该讲座的主题
然后向用户提出问题。 用户给出答案后，它会给出答案的分数并给出解释。
系统输入：[讲座、主题、user_answer]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1.使用“prompt_template”生成讲座
2. 在prompt_template生成的内容中，通过'ui_input_text'获取用户的讲座。
3. 用户选择讲座后，通过“prompt_template”生成与该讲座相关的主题。
4. 在prompt_template生成的主题中，通过 'ui_input_text' 获取用户的主题。
5. 用户选择主题后，使用“prompt_template”生成与该主题和讲座相关的问题
6. 通过“ui_input_text”从用户处获取答案。
7. 使用“prompt_template”生成真实答案并为用户的答案评分。
8. 通过“ui_output_text”显示用户答案的真实答案和分数。

说明：创建一个可以生成与网站相关的博客文章的系统
系统输入：[url]
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
1. 通过 'ui_input_text' 从用户处获取网站 URL
2. 使用“doc_loader”从 URL 将网站加载为文档
3.使用'doc_to_string'将Document转换为字符串内容
4. 如果生成了字符串内容，请使用“prompt_template”生成与该字符串内容相关的博客文章。
5. 如果生成了博客文章，则通过 'ui_output_text' 将其显示给用户。

指令：{指令}
让我们一步一步地解决这个问题，以确保我们得到正确的答案。
```
