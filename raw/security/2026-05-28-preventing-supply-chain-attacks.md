# 最新的不一定好——预防供应链攻击

> Source: https://geeknote.net/Rei/posts/3286
> Collected: 2026-05-28
> Published: 2026-05-24

最近看到新闻，GitHub 疑似因员工 VS code 更新了被植入恶意代码的插件导致被入侵([Hacker News](https://news.ycombinator.com/item?id=48201316)) 。然后搜了一下，今年以来通过包管理器进行供应链攻击的案例已经有三起：

- 2026年3月 axios npm 包攻击 （ [Hacker News](https://news.ycombinator.com/item?id=47582220) ）
- 2026年5月 TanStack npm 包攻击 （ [Hacker News](https://news.ycombinator.com/item?id=48100706) ）
- 2026年5月 VS Code 扩展供应链攻击 （ [Hacker News](https://news.ycombinator.com/item?id=48189368) ）

理论上，包的托管平台应该对新发布的包进行安全扫描，从源头杜绝恶意代码散布，但这个机制还没普及。当下在开发者一侧，可以给软件包更新加上冷却时间来降低风险。

我搜集了我用到的包管理器的冷却设置记录如下，欢迎评论区补充。

## GitHub Dependabot

Dependabot 支持设置 cooldown 时间，配置：

```
- package-ecosystem: <name>
  cooldown:
    default-days: 7
```

Cooldown 选项仅适用于版本更新，不适用于安全更新。

文档： https://docs.github.com/en/code-security/reference/supply-chain-security/dependabot-options-reference#cooldown- 。

## NPM

NPM v11.10.0 以上可以设置 `min-release-age` ，命令：

```
npm config set min-release-age 7
```

文档： https://docs.npmjs.com/cli/v11/using-npm/config#min-release-age 。

其他 js 包管理器也有类似机制。

## Bundler

Bundler 还没支持 cooldown，但有一个讨论： https://github.com/ruby/rubygems/discussions/9113 。

## 编辑器

### VS Code

VS Code 可以关闭插件自动更新：

文档： https://code.visualstudio.com/docs/configure/extensions/extension-marketplace#_extension-autoupdate 。

### Zed

Zed 还不支持关闭插件自动更新，但有一个讨论： https://github.com/zed-industries/zed/discussions/38661 。
