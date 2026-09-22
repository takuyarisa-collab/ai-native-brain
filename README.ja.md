# ai-native-brain

[English](README.md)

> 人間とAIが共有する「外部記憶」を育てるための、進行中の実験。

**ai-native-brain** は、人間とAIの両方にとって使いやすい、個人用の知識・記憶システムをどう作るかを試しているリポジトリです。

出発点は、かなり実務的な問題でした。

- 重要な文脈が個別チャットの中に閉じ込められる
- 新しいセッションでは、過去の判断に至った理由が失われやすい
- 異なるAIツール同士で長期文脈を自然に共有しにくい
- 一般的なノートはまず人間向けに作られ、あとからAI利用を足すことが多い

そこで逆向きに考えます。

> **人間とAIの両方が最初から「読む人・書く人」だとしたら、Second Brainはどういう形になるのか？**

今のところ、仕組みは意図的にシンプルです。

- Markdown
- Git履歴
- 明示的な構造
- 必要なものだけを選んで読む運用

完成したフレームワークとして提示するものではありません。
実際に使いながら、構造そのものも変わっていく前提です。

## このリポジトリに置くもの

この公開リポジトリには、**公開可能なアーキテクチャ、運用上の考え方、比較メモ、テンプレート**を置きます。

一方で、元になった実運用環境に含まれる以下は公開しません。

- 個人的な会話
- 非公開のプロジェクト戦略
- 個人プロファイル
- 組織・顧客に関する情報
- 個別の長期記憶

**実際の記憶そのものではなく、記憶を扱う方法を公開する**という境界を意識しています。

## 想定している読者

これは、**「10分で自分のBrainを作るための入門キット」ではありません。**

どちらかというと、すでに次のようなテーマを試している人の参考資料を目指しています。

- AIの永続記憶
- セッションをまたぐAgent Memory
- AI-native PKM / Second Brain
- 複数AI間でのContext共有
- 人間が直接読める長期記憶
- チャットやモデルをまたいだ継続性

狙いは、設計判断、トレードオフ、失敗、構造の変化を公開して、**reference implementation / research notebook** として使える状態にすることです。

テンプレートも「この形が正解」という意味ではなく、現在の実運用から切り出した一例です。

## 中心となる考え方

Brainは巨大な1つのPromptではありません。

役割の違う、小さく長く残る情報を分けて持ちます。

```text
conversation / work
        ↓
   observations
        ↓
      Seeds
        ↓
 repeated evidence
        ↓
 Principles / Decisions
        ↓
 projects and future conversations
```

毎回すべての履歴をAIへ渡すのではなく、その仕事に必要なものだけを辿って読ませます。

## 主なレイヤー

### 1. Principles

個別プロジェクトをまたいで使う、比較的安定した判断基準です。

例：

- 速度と品質をどう両立するか
- 面白い案を実装せずSeedとして残すのはいつか
- 人間とAIで役割をどう分けるか

### 2. Decisions

重要な判断を、その理由と一緒に残します。

最低限、次の4つがあとから分かることを重視します。

1. 何を決めたか
2. なぜそう決めたか
3. 何を採用しなかったか
4. どこに適用する判断か

結論だけでなく、**判断を再現できる程度の理由**を残します。

### 3. Seeds

まだ正解でも方針でもないけれど、失いたくない仮説や違和感です。

Seedはそのまま眠ってもいいし、何度も再登場して育った場合はPrincipleやDecisionへ昇格します。

```text
seed → growing → principle / decision
          ↘
          dormant
```

「面白いから」というだけで、全部を新規プロジェクト化しないための層でもあります。

### 4. Projects

各活動領域の安定した入口です。

人間やAIが短時間で次を理解できることを重視します。

- これは何か
- なぜ存在するか
- 何を扱うか
- 最新情報の正本はどこか

変化の激しい実装状況は、別の場所へ分離します。

### 5. Operating System

Brain全体をどう使うかという運用ルールです。

- 何を残すか
- どこへ残すか
- いつ見直すか
- 複数AI間でどう共有するか
- Knowledge Managementそのものを仕事にしないためにどうするか

## Continuity Memory

もう一つの実験テーマが、**セッションやモデルをまたいだ継続性**です。

記憶を1つのフラットなDBとして扱うのではなく、人間にも扱いやすい概念に分けています。

- **Episode / Bookmark** — 長く持っていきたい出来事
- **Current State / Breath** — 今も生きているもの
- **Handoff** — 次のセッションへ続きを渡すための文脈
- **Dream / Consolidation** — 最近の経験と過去の記憶を見直し、今の視点で再整理する時間

これらはAIに人間の脳があるという主張ではなく、**人間が直感的に理解しやすい操作モデル**として使っています。

人間は「覚える」「忘れる」「寝かせる」「振り返る」「次の日へ持ち越す」という感覚をすでに持っているからです。

詳しくは [docs/continuity-memory.md](docs/continuity-memory.md) を参照してください。

## 設計上の基本姿勢

- **ファイルを正本にする。** Indexや検索層は交換可能である方がよい。
- **人間が読めることを優先する。** 必要なら直接編集できること。
- **AIにも読みやすい構造にする。** 名前、metadata、入口を明示する。
- **結論だけでなく理由を残す。**
- **すべてのアイデアを正解へ昇格させない。**
- **全部を毎回読ませない。** Navigationと選択的参照を優先する。
- **過去の変化を残す。** 現在だけでなく、理解がどう変わったかも価値がある。
- **Private MemoryとPublic Patternは別物。**
- **Brainの仕組み自体も更新してよい。**

## リポジトリ構成

```text
ai-native-brain/
├── README.md
├── README.ja.md
├── docs/
│   ├── architecture.md
│   ├── continuity-memory.md
│   └── landscape.md
└── templates/
    ├── seed.md
    ├── decision.md
    ├── principle.md
    └── project.md
```

大きな実装を配布することより、実運用から出てきた**観察・判断・設計パターン**を残すことを優先しています。

この構造は、そのままコピーするためではなく、比較したり疑ったり、自分の仕組みを考える材料として使うことを想定しています。

## なぜGit + Markdownか

次の性質をできるだけ失いたくないからです。

- portable
- inspectable
- diffable
- versioned
- searchable
- 特定のAIベンダーに依存しにくい
- 人間とAIの両方が直接読める

将来的には、全文検索、Vector Retrieval、Knowledge Graph、自動Consolidation、Agent Toolingなどを足す可能性があります。

ただし、それらはMarkdownの正本を置き換えるのではなく、**周囲から強化するもの**として扱う方針です。

## 関連分野

この実験は、次の領域と重なっています。

- Personal Knowledge Management (PKM)
- Second Brain
- AI-native PKM
- Agent Memory
- Long-term / Persistent AI Memory
- Context Management
- Memory Consolidation
- Personal AI Infrastructure
- External Cognition

ここで使っている概念をすべて独自発明だと主張するものではありません。

実際の人間-AI協働の中で使ってきた仕組みを記録し、近いシステムと比較しながら、似たテーマを扱う人の参考になる形で残すことが目的です。

関連プロジェクトと比較メモは [docs/landscape.md](docs/landscape.md) にまとめています。

## 状態

**Experimental / Living System**

現在の構造を完成形とは考えていません。

Agent MemoryやAI-native Knowledge Management周辺の動きを継続的に観測し、実際に試し、役に立ったものを取り込みながら更新していきます。

その時も、**人間が直接読めるシンプルな外部記憶**という土台を失わないことを重視します。

## Public / Private の境界

このリポジトリが公開するのは、

> **the method, not the memory**

です。

公開しやすいもの：

- architecture
- generic templates
- operating rules
- anonymized examples
- lessons learned
- related-work notes

非公開にするもの：

- personal conversations
- private project strategy
- employer / client information
- personal profiles
- credentials
- identity-specific long-term memory

この境界自体も、Brainの設計の一部として扱います。
