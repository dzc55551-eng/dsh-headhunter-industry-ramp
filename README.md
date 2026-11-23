# dsh-headhunter-industry-ramp

> 猎头陌生行业速研技能 · DeepSeek Harness 插件
> 数小时内吃透一个此前从未接触过的赛道，产出会能打电话的名单。

## 它解决什么问题

猎头接到一个此前从未接触过的赛道岗位，最常见的三种卡点：

1. **不懂行**——和候选人聊不到技术路线上，客户追问行业格局答不上来；
2. **没有名单**——知道赛道热闹，但找不出 4 家真正值得投的标杆公司；
3. **交付不了**——做出来的东西不能直接发给客户，也不能直接照着打电话。

这个 skill 把这三件事拆成一条有硬规则的流水线，跑完得到：行业认知、目标公司池、人才地图，以及一份可交付的 HTML/docx 报告和一张人才地图 Excel。

## 安装

DSH 一条命令：

```bash
dsh plugin add dzc55551-eng/dsh-headhunter-industry-ramp
```

不用 DSH，或者想手动装，把 skill 目录复制过去：

```bash
git clone https://github.com/dzc55551-eng/dsh-headhunter-industry-ramp.git
cp -r dsh-headhunter-industry-ramp/skills/headhunter-industry-ramp ~/.agents/skills/
```

也可以只装到某个项目：

```bash
cp -r dsh-headhunter-industry-ramp/skills/headhunter-industry-ramp /你的项目/.agents/skills/
```

放进去就能用，不用重启。

## 什么时候会触发

模型读到下面这类描述时会自动调用：陌生行业、新赛道、行业速研、行业研究、赛道研究、行业格局、技术路线、mapping、人才地图、目标公司清单、longlist。

不适合的场景：熟悉的赛道做常规寻访、纯商业尽调、推荐报告撰写、面试辅导。

## 里面有什么

```
package.json                 声明 dsh.bundle，让 `dsh plugin add` 能装
cordis.patch.yml             插件挂载点
index.js                     把 skills/ 注册成一个 skill 提供方
examples/walkthrough.md      一次完整的真实跑通记录
assets/icon-180.png          市场卡片图标
skills/headhunter-industry-ramp/
├── SKILL.md                 主文件，先读这个
├── references/
│   ├── jd-anatomy.md        JD 拆解：岗位锚定、能力画像、信号词
│   ├── source-playbook.md   来源分级与时间盒，信息可信度怎么判
│   ├── knowledge-map.md     行业知识框架怎么搭
│   ├── company-teardown.md  标杆企业拆解模板
│   ├── talent-mapping.md    人才地图四张表的口径定义
│   ├── candidate-playbook.md 候选人触达话术
│   └── html-style-guide.md  交付物样式与格式规范
├── templates/
│   ├── report-template.html 客户版报告模板（12 段，360 处占位符）
│   ├── report-copy-outline.md 报告文字稿骨架
│   └── talent-map.xlsx      人才地图四表模板（含分项得分公式）
└── assets/
    └── case-humanoid.md      完整案例：人形机器人赛道
```

## 三条硬规则

技能里写死了三条不可协商的规则，模型每次都会先读：

| 规则 | 含义 | 不遵守的后果 |
|---|---|---|
| **来源分级** | 每条事实标注来源等级，L1–L4 一级来源和推测分开写 | 交付物里混进推测，客户一眼看穿 |
| **时间盒** | 每个阶段有硬性时长上限，超时就降级交付而不是无限深挖 | 一个赛道吃三天，做单节奏崩掉 |
| **岗位导向** | 所有信息必须服务于"能不能给这个人打电话"，无关信息直接砍 | 报告很全但没法用 |

## 七阶段主流程

```
阶段 0  岗位锚定      拆 JD，反推能力画像与关键信号词
阶段 1  知识框架      搭行业认知骨架，标注未知项
阶段 2  标杆拆解      4 家标杆公司，定位人才聚集地
阶段 3  人才地图      公司池 / 团队层 / 人才层 / 岗位信号 四张表
阶段 4  话术准备      候选人触达话术与异议处理
阶段 5  交付          HTML 报告 + docx 报告 + 人才地图 Excel
阶段 6  收尾          知识库矩阵挂载与自检清单
```

## 交付物

一次跑完产出四个载体：

- **HTML 报告**——12 段式客户版结构，含来源分级与时间盒说明
- **docx 报告**——同样内容的文字稿版
- **人才地图 Excel**——四张表，分项得分自动算总分与档位（值得推 / 备选 / 不优先）
- **对话交付**——直接在对话里给出结论与名单

知识库链接只允许出现在标题为「延伸资源」的区块，正文和来源分级表里不出现。

## 本地安装说明

这个插件把 `skills/` 注册成一个**独立的** skill 提供方（`includeDefaultRoots: false`），不会接管你本机的 `~/.dsh/skills`。

如果你之前手动把技能复制到了 `~/.dsh/skills/headhunter-industry-ramp/`，装上插件后会看到同名技能出现两次——删掉手动复制的那份即可。

## 英文说明

**What it does.** A headhunter skill for mapping an unfamiliar industry in hours rather than days. It turns one unknown sector into industry context, a shortlist of four benchmark companies, a talent map, and a client-ready HTML/docx report plus a talent-map spreadsheet.

**When it fires.** Unknown industry, new sector, industry mapping, sector research, industry landscape, talent mapping, target company list, longlist.

**Three hard rules.** Every fact is labelled with a source tier (L1–L4); every stage is time-boxed and degrades rather than digs deeper; every piece of information must serve one question — can I call this person.

**Install.**

```bash
dsh plugin add dzc55551-eng/dsh-headhunter-industry-ramp
```

## License

MIT — see [LICENSE](LICENSE).
