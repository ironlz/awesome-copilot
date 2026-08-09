# 🤖 Awesome GitHub Copilot（中文版）
[![Powered by Awesome Copilot](https://img.shields.io/badge/Powered_by-Awesome_Copilot-blue?logo=githubcopilot)](https://aka.ms/awesome-github-copilot) [![GitHub contributors from allcontributors.org](https://img.shields.io/github/all-contributors/github/awesome-copilot?color=ee8449)](#contributors-)

这是一个由社区创建的集合，包含自定义 agent、指令、技能、钩子、工作流和插件，旨在进一步增强你的 GitHub Copilot 使用体验。

> [!TIP]
> **可在网站上查看完整资源集合 →** [awesome-copilot.github.com](https://awesome-copilot.github.com)
>
> 网站提供对数百种资源的全文搜索与筛选，以及 [Learning Hub](https://awesome-copilot.github.com/learning-hub) 供你查找指南和教程。
>
> **想把这个集合用于 AI agent 吗？** 网站提供了机器可读的 [`llms.txt`](https://awesome-copilot.github.com/llms.txt)，其中包含所有 agent、指令和技能的结构化列表。

## 📖 Learning Hub

刚接触 GitHub Copilot 定制化？网站上的 **[Learning Hub](https://awesome-copilot.github.com/learning-hub)** 提供精心整理的文章、逐步指南和参考资料，覆盖从 agent、技能和指令等核心概念，到钩子、agentic workflow、MCP 服务器以及 Copilot 编码 agent 的实践指南。

## 这个仓库里有什么

| 资源 | 描述 | 浏览 |
|----------|-------------|--------|
| 🤖 [Agents](docs/README.agents.md) | 专门的 Copilot agent，可与 MCP 服务器集成 | [查看全部 agent →](https://awesome-copilot.github.com/agents) |
| 📋 [Instructions](docs/README.instructions.md) | 通过文件匹配规则自动应用的编码规范 | [查看全部 instruction →](https://awesome-copilot.github.com/instructions) |
| 🎯 [Skills](docs/README.skills.md) | 自包含的文件夹，包含说明和打包资源 | [查看全部 skill →](https://awesome-copilot.github.com/skills) |
| 🔌 [Plugins](docs/README.plugins.md) | 面向特定工作流的 agent 和 skill 的精选打包集合 | [查看全部 plugin →](https://awesome-copilot.github.com/plugins) |
| 🍳 [Cookbook](cookbook/README.md) | 可直接复制使用的 Copilot API 实战配方 | — |

## 安装插件

对于大多数用户来说，**Awesome Copilot** 市场已经注册到 Copilot CLI/VS Code，因此你可以直接安装插件：

```bash
copilot plugin install <plugin-name>@awesome-copilot
```

如果你使用的是较旧的 Copilot CLI 版本，或者自定义环境中提示市场未知，可以先注册一次，然后再安装：

```bash
copilot plugin marketplace add github/awesome-copilot
copilot plugin install <plugin-name>@awesome-copilot
```

## 参与贡献

请查看 [CONTRIBUTING.md](CONTRIBUTING.md) · [AGENTS.md](AGENTS.md) 以获取 AI agent 指导 · [Security](SECURITY.md) · [Code of Conduct](CODE_OF_CONDUCT.md)

> 这里的自定义内容来自第三方开发者。请在安装任何 agent 前先查看其文档与说明。

## 贡献者 ✨

感谢这些优秀的人（[emoji key](./CONTRIBUTING.md#contributors-recognition)）：

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://www.aaron-powell.com/"><img src="https://avatars.githubusercontent.com/u/434140?v=4" width="100px;" alt=""/><br /><sub><b>Aaron Powell</b></sub></a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://codemilltech.com/"><img src="https://avatars.githubusercontent.com/u/2053639?v=4" width="100px;" alt=""/><br /><sub><b>Matt Soucoup</b></sub></a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://www.buymeacoffee.com/troystaylor"><img src="https://avatars.githubusercontent.com/u/44444967?v=4" width="100px;" alt=""/><br /><sub><b>Troy Simeon Taylor</b></sub></a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/abbas133"><img src="https://avatars.githubusercontent.com/u/7757139?v=4" width="100px;" alt=""/><br /><sub><b>Abbas</b></sub></a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://calva.io/"><img src="https://avatars.githubusercontent.com/u/30010?v=4" width="100px;" alt=""/><br /><sub><b>Peter Strömberg</b></sub></a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://danielscottraynsford.com/"><img src="https://avatars.githubusercontent.com/u/7589164?v=4" width="100px;" alt=""/><br /><sub><b>Daniel Scott-Raynsford</b></sub></a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/jhauga"><img src="https://avatars.githubusercontent.com/u/10998676?v=4" width="100px;" alt=""/><br /><sub><b>John Haugabook</b></sub></a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

这个项目遵循 [all-contributors](https://github.com/all-contributors/all-contributors) 规范，欢迎任何形式的贡献！

## 📚 其他资源

- [VS Code Copilot 定制化文档](https://code.visualstudio.com/docs/copilot/copilot-customization) - Microsoft 官方文档
- [GitHub Copilot Chat 文档](https://code.visualstudio.com/docs/copilot/chat/copilot-chat) - 完整的聊天功能指南
- [VS Code 设置](https://code.visualstudio.com/docs/getstarted/settings) - VS Code 常规配置指南

## ™️ 商标

本项目可能包含某些项目、产品或服务的商标或标志。Microsoft 商标或标志的授权使用必须遵守 [Microsoft 的商标与品牌使用准则](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)。对本项目进行修改后使用 Microsoft 商标或标志时，不得造成混淆，或暗示 Microsoft 的赞助。任何第三方商标或标志的使用都须遵守相应第三方的政策。
