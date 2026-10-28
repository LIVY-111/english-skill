# english-skill

一个开源的 **专四（TEM-4）口语思辨陪练** Skill。它一轮一轮给出英文思辨话题与一正一反参考句型，你口头作答后，它输出「原句转写 + 一版口语化优化 + 中式英语点评」，并通过【继续】/【重新回答】把同一个话题往深处追问。

## 1. 项目解决什么问题

备考专四口语时，学生普遍卡在三件事上：

- **没人对练**：想练"就一个话题口头说清立场"，但找不到随时能陪练的考官；
- **不知道错在哪**：自己的中式英语（中文直译语序、中式搭配、逻辑断层、母语负迁移）自己听不出来；
- **改词没用**：普通润色只会把 good 换成 excellent，不治语序和连接词的病根。

本 Skill 把这三件事做成一个固定循环：给话题 → 你开口 → 原样保留你的句子 → 只改病根并加粗改了哪 → 用中文点明这次的中式英语问题。纯对话完成，不录音、不联网、不出文件。

## 2. 主要功能

- **出题**：每轮给一个专四难度的平衡型思辨话题（Topic），附一句肯定立场、一句否定立场的纯英文参考句型，然后等你作答。
- **原样转写【我的原句】**：把你的英文作答一字不改地回显，保留所有语序错误、搭配错误和犹豫，不偷偷修正。
- **口语优化【优化句】**：只给一版适配专四口头表达的改写，优先修中式英语病根（语序、搭配、逻辑断层、母语负迁移），拒绝浅层同义词替换；改动的核心部分加粗；句子短、连接自然，不过度书面化。
- **简短点评【简短点评】**：用中文先点名这次的中式英语问题，再评一句逻辑、句式、用词地道度。
- **追问与重答循环**：反馈后给出两个选项——
  - **【继续】**：不换话题，就当前立场追问一个更尖锐的问题，进入新一轮作答；
  - **【重新回答】**：同一话题让你再说一次，再次转写/优化/点评，可反复多轮，直到你选【继续】。
- **换话题**：只有你主动说「换话题 / 下一题 / new topic」时才开启新话题，不会自动跳题。

## 3. 安装方法

本 Skill **无任何依赖、无可执行脚本**，整个文件夹就是全部内容。

1. 把 `english-skill/` 文件夹复制到你的 Agent 的 skills 目录下（支持 OpenAI Skills 规范的客户端会自动识别其中的 `SKILL.md`）。
2. 确认目录结构如下即可：

   ```
   english-skill/
   ├── SKILL.md            # 核心：对话流程规则
   ├── agents/
   │   └── openai.yaml     # 平台 UI 元数据
   └── README.md
   ```

3. 本地快速验证（可选）：用官方校验脚本检查 frontmatter 是否合法：

   ```bash
   python scripts/quick_validate.py path/to/english-skill
   ```

   没有该脚本时也可直接使用——本 Skill 的全部行为都写在 `SKILL.md` 里；你甚至可以把 `SKILL.md` 正文直接作为系统提示喂给任意对话模型来运行。

## 4. 使用方法

1. 对 Agent 说触发语，例如：「用 english-skill 陪我练专四口语」「开始一轮口语思辨」。
2. Agent 输出 `Topic / Pro / Con` 三行后停下，你直接用英文口头作答（打字或粘贴语音转写均可）。
3. 阅读三块反馈后，根据需要输入：
   - `继续` —— 就当前话题深度追问，答新一轮；
   - `重新回答` —— 不换话题，再说一次；
   - `换话题` / `下一题` —— 开启全新话题。
4. 若你不小心用中文作答或答得太短，Agent 会提示你用英文完整说立场，不会强行点评。

## 5. 输入输出示例

**Agent（首轮出题）：**

```
Topic: Should college students do part-time jobs?
Pro: Working part-time helps students earn pocket money and build a real sense of responsibility.
Con: Part-time jobs often take time away from study and leave students exhausted in class.
```

**用户作答：**

> I think part-time job is very good. I can learn knowledge and make money. But if I work too much, I will not have time to study, so I think we should control the time.

**Agent（反馈）：**

【我的原句】
I think part-time job is very good. I can learn knowledge and make money. But if I work too much, I will not have time to study, so I think we should control the time.

【优化句】
I think **having a part-time job is a great experience**: it lets me **earn some pocket money and pick up real-life skills**. **That said**, if I work too many hours, I won't have enough time for my studies, **so the key is to keep my working hours under control**.

【简短点评】
"learn knowledge" 是中式搭配，英语用 acquire / pick up skills 更地道；"very good" 偏弱且受中文语序影响。but...so 连用造成连接词叠用，改成 That said 引出让步、so 一句收束更自然。立场清楚，若补一个具体例子会更有说服力。

【继续】深度追问本话题 / 【重新回答】同一话题再说一次
