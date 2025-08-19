# Mermaid 图表生成提示词指南

本仓库包含一个专门设计的提示词，旨在指导AI模型生成高质量的Mermaid图表。**我们的初衷是为了解决目前大多数AI模型在生成Mermaid代码时，尤其是在处理中文内容时，容易出现细小语法错误的问题。** 此提示词通过提供清晰、严格的规则，确保生成的Mermaid代码具有一致性、语法正确性，并遵循最佳实践。

## 简介

Mermaid是一个强大的、受Markdown启发的工具，用于从文本生成图表和流程图。尽管其功能强大且应用广泛，但在实践中，我们发现**目前主流的AI模型在生成Mermaid代码时，特别是在图表中包含中文文本时，常常会产生一些难以察觉的细微错误**，例如使用了错误的引号类型、在不应出现换行的地方使用了换行符，或者节点ID与中文文本的结合方式不符合Mermaid规范。这些错误通常需要手动修正，耗费时间和精力。

本提示词正是为了解决这些痛点而设计。通过为AI模型提供明确、简洁的规则，我们旨在**规避掉因中文内容引发的常见Mermaid语法错误**，确保AI生成的Mermaid代码始终是有效、可渲染且符合预期的。

## 提示词

以下是用于指导AI模型生成Mermaid图表的精确提示词：

```
"All content in the Mermaid code, especially Chinese content, MUST be enclosed exclusively in English double quotes "". Never use Chinese double quotes “” to enclose any content. "
"Inside English double quotes, no punctuation or special characters are allowed, except for the English comma ,. "
"Do not use \n for line breaks. "
"Node IDs MUST be in English. If Chinese text is required for display, it should be placed within double quotes. For example, use A["中文显示文本"] instead of 中文节点["文本"]. "
"When defining nodes with explanatory information using [], all information inside [] MUST be enclosed in double quotes, like A["Interface MethodSet"]. "
"For quadrant charts, do not use [label] for points, as this syntax format is incompatible. Points should be defined as A: [x, y]. "
"When generating requirement diagrams, replace fulfills with SATISFIES (满足) and calls with TRACES (追踪) to meet the required syntax. "
```

## 关键指南解释

此提示词强调了几条关键规则，以确保Mermaid代码的正确生成，尤其针对中文内容：

1.  **独家使用英文双引号（`""`）**：这对于所有内容，尤其是中文文本至关重要。**AI模型常犯的错误之一是混用中英文双引号**，而Mermaid解析器只识别英文双引号。
2.  **双引号内有限的标点符号**：双引号内只允许使用英文逗号（`,`）。**过多的特殊字符或不规范的标点符号常常导致Mermaid解析失败**。
3.  **不使用换行符（`\n`）**：Mermaid会隐式处理换行或通过特定语法处理。**AI模型有时会错误地插入`\n`字符**，导致渲染问题。
4.  **英文节点ID**：所有节点标识符（例如，`A`、`B`、`Task1`）必须是英文。如果显示文本是中文，则应将其包含在与节点定义关联的双引号内（例如，`A["中文显示文本"]`）。**AI模型有时会直接使用中文作为节点ID，这是Mermaid不允许的**。
5.  **节点解释使用双引号**：节点方括号`[]`内的任何解释性文本也必须包含在英文双引号内（例如，`A["Interface MethodSet"]`）。
6.  **象限图点定义**：对于`quadrantChart`，点应直接用坐标定义（例如，`PointA: [0.3, 0.6]`），而不是使用`[label]`语法，因为这种语法不兼容。
7.  **需求图语法**：强制使用需求图的特定关键字：`SATISFIES` (满足) 代替 `fulfills`，以及 `TRACES` (追踪) 代替 `calls`。这确保了此类图表的正确生成。

## 如何使用

在请求Mermaid图表生成之前，只需将此提示词提供给您的AI模型。然后，您可以跟进您的具体图表请求（例如，“生成一个用户登录流程的流程图，使用中文显示文本”）。AI随后应严格遵守这些规则，从而生成高质量、无错误的Mermaid代码。

## 示例用法（概念性）

**用户输入：**

```
"All content in the Mermaid code, especially Chinese content, MUST be enclosed exclusively in English double quotes "". Never use Chinese double quotes “” to enclose any content. "
"Inside English double quotes, no punctuation or special characters are allowed, except for the English comma ,. "
"Do not use \n for line breaks. "
"Node IDs MUST be in English. If Chinese text is required for display, it should be placed within double quotes. For example, use A["中文显示文本"] instead of 中文节点["文本"]. "
"When defining nodes with explanatory information using [], all information inside [] MUST be enclosed in double quotes, like A["Interface MethodSet"]. "
"For quadrant charts, do not use [label] for points, as this syntax format is incompatible. Points should be defined as A: [x, y]. "
"When generating requirement diagrams, replace fulfills with SATISFIES (满足) and calls with TRACES (追踪) to meet the required syntax. "

生成一个简单的流程图，显示用户登录、检查凭据，以及成功或失败的情况。显示文本使用中文。
```
