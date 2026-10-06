# watch-live-match

通过真实浏览器截图观察体育或电竞直播，核实比分变化，并持续观察到用户指定的停止条件。

A portable agent skill for observing live sports and esports broadcasts through real browser screenshots.

## 能做什么

- 从直播画面的 HUD 读取队名、当前地图/局比分和系列赛大比分
- 核实画面正在推进，区分直播、回放、中场、加时和最终结果
- 按队伍身份跟踪比分，避免换边后把比分对应错队
- 报告已确认的比分变化，并提供用户要求的真实截图
- 持续到用户指定的半场、当前地图结束、整场/系列赛结束或取消
- 浏览器受阻、画面不可读或播放停滞时，如实报告最后确认的比分和时间

## 使用前提与限制

这是供兼容助手读取的工作流程，不是独立运行的软件，也不自带视频访问能力、实时比分后端、OCR 服务或 AgentReach。

使用它的助手需要实际可用且获得授权的浏览器控制、截图、视觉读取、消息发送及等待/持续执行能力。没有这些能力时，安装这个 skill 也不会自动获得它们。登录、地区、版权、付费和其他访问限制仍然适用，不能绕过。

比分来自所观察到的直播画面，可能存在转播延迟。定期截图可能错过中间回合，不能保证每次比分变化都被捕捉。浏览器被阻止或会话停止时，不能声称仍在持续监控。

## 文件结构

```text
watch-live-match/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── assets/
    └── icon.svg
```

`SKILL.md` 是主要工作流程；`agents/openai.yaml` 提供兼容宿主可选使用的界面信息；`assets/icon.svg` 是随 skill 打包的图标。

## 安装与使用

1. 下载本仓库中的 `watch-live-match.zip`，或通过 GitHub 的 Code → Download ZIP 下载源码。
2. 解压后，找到包含 `SKILL.md` 的 `watch-live-match` 文件夹。
3. 使用宿主产品支持的技能导入功能，或按照其文档放入技能目录。不同产品的安装方式可能不同。
4. 给出具体直播链接、需要通知的事件和停止条件。

示例请求：

> 使用 watch-live-match 观察这个直播：[直播链接]。每次确认比分变化就告诉我，区分当前地图比分和系列赛大比分，看到整个系列赛结束。

> 继续看这场比赛，直到半场；现在截一张能看到两队名称和比分的真实画面。

## English summary

The skill requires a capable, authorized host with real browser screenshots, visual understanding, messaging and continued execution. It does not install tools, provide a live-score API, guarantee uninterrupted coverage, or bypass access restrictions. Scores must come from the broadcast HUD, not comments or page metadata. Periodic observations can miss intermediate changes, and stream delay may apply.

## Export notes

This package preserves the existing skill workflow and bundled agent metadata/icon. One host-specific attachment-delivery paragraph was generalized for portability. The package does not contain account data, a default room, credentials, cookies, viewing history or screenshots.

No license has been added to this repository.
