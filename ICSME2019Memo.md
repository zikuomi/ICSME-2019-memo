# ICSME 2019 memo

<style>
.waku {
  padding: 10px; margin-bottom: 10px; border: 3px solid;
}
</style>

# 7/6 (* absts)

## Bugs I (2 Researches, 2 Journals, 1 Short)

- Title: A Longitudinal Analysis of Bug Handling Across Eclipse Releases (Research)
>  
背景： Eclipseのような大規模OSSは定期的なリリースを行う → 各リリースでバグが報告され、解析・修正 → 既存研究はそのバグ修正などに焦点 → 各リリース間の修正アクティビティそのものを比較（つまり、リリースAとリリースBのバグ修正のどこに差があり、どのような影響があるのか）する研究はない  
調査： Eclipseの15年分のバグ処理プロセス（138Kのバグレポートや年間16+4*2のリリースも含）を調査 → バグの解決率、修正率、 Release Pressure の影響を調査 → 後期ほど修正率などが改善

Tag_CI, Tag_Survey, Tag_Release, Tag_Version  
Tag_S_Debug

継続開発におけるバグ対応の変遷についての調査、ということでいいのだろうか。結論としてはプロジェクト発足当時よりも年数経った時分のほうが優れている（成熟している）とのこと。
___

- Title: Impact of switching bug trackers: a case study on a medium-sized open source project (Research)
>  
背景： Bug Tracker (Bugzilla/GitHub) はソフトウェアプロジェクトにおいて必要不可欠 → ユーザからバグ報告をしてもらう（貢献） → Bug Tracker の各環境が持つバグ報告への影響の比較は困難（比較箇所がないため）  
調査： 中規模OSSプロジェクトのCoqのバグトラッカーを変更（Bugzilla → GitHub）した場合の影響を調査 → IssueをインポートするGitHub APIを利用し 4900のバグレポートを移行  
提案手法： 切り替え前後のデータを比較する新規メトリクス → Regression on Discontinuity を用いた分析  
結果： 主要な開発者自身からバグ報告が増加、開発者のコメント増加、外部から意見を出す人も増加

Tag_Regression, Tag_Github, Tag_Debug, Tag_Dev  
Tag_S_Debug

結論としては、GitHubに切り替えたらバグレポートが活発化したということでいいのか？（だとするとただのGitHub賛美になるだけなんだが） ○○みたいなプロジェクトは××のバグトラッカーが適している（根拠が提案するメトリクス）、みたいなら筋書きは分かるんだが…
___

- Title: Multi-task Defect Prediction (Journal)
>  
背景： 欠陥予測において、ラベル付きデータは十分にあるという仮定や想定が多い → 実際にはラベル付きは限定的 → 未調査の部分が多い  
提案手法： MASK ラベル付きデータが少ないシナリオでも学習できるようにマルチタスク学習を適用した欠陥予測手法 → フェーズを分割（微分進化最適化フェーズ: プロジェクト間の共有情報と非共有情報への重み付け、マルチタスク学習フェーズ: 各プロジェクトの予測モデルを同時に構築）   
実装：  
実験： 18の実世界のソフトウェアプロジェクトで評価（vs STL, SCL, Peters filter, Burak filter） → ラベルデータが全体の10%という状況下で、MASKはF値0.397, AUC 0.608 を達成 → 他の手法を大幅に上回る

Tag_CPDP, Tag_Prediction, Tag_Learning  
Tag_S_Debug

欠陥予測でのラベル付きデータが少ない環境下でどうするか、という問題への取り組みの一。データが少ない中でF値0.397はすごいんだろうけど、実用的かというと微妙なライン？
___

- Title: The Impact of Context Metrics on Just-In-Time Defect Prediction (Journal)
>  
背景： 既存の欠陥予測アプローチでは、変更された行のみに焦点を当てている → その周辺の行の情報は無駄に → 周辺情報が予測結果に影響を与えるのではという直観  
提案手法： 周辺情報を学習へ利用できるようにメトリクスを定義 (Context Metrics) → ここでのContextは変更行の周辺 n 行（ n = 1, 2, ... ）の位置づけ → Metricsの中身はコンテキスト行の単語/キーワードの数  
実装：  
実験： 6つのOSSプロジェクトで評価 → コンテキスト行を考慮したほうが中央値が高い

Tag_Prediction, Tag_Learning, Tag_Metrix  
Tag_S_Debug

周辺を見るというのはアイデアとしてはありだと思う反面、メトリクス化はムズそう（単語数などが最適とも思わない）。 あと地味に学習コストが増えていることが気になる。
___

- Title: The Impact of Rare Failures on Statistical Fault Localization: the Case of the Defects4J Suite (Short)
>  
背景： Statistical Fault Localization (SFL) はテストから得られたカバレッジ情報と統計メトリクスを使用して障害発生位置を推量 → 統計的メトリクスの有効性とテストスイートの失敗率の関連性は不明のまま  
調査： Defects4Jを調査 → テストスイートの失敗率が低いとSFLのパフォーマンスが低下（失敗データが少なくて学習が不十分になるから？） → 各統計メトリクスの精度を調査 → 精度が上昇するとSFLのパフォーマンスが上昇

Tag_Learning, Tag_Localization, Tag_Defect4J, Tag_Statistical  
Tag_S_Debug

メトリクスの評価をしてみた、という位置づけでおｋ？ 失敗率が低いと精度が下がるというジレンマっぽい何かを感じる。
___

## Mobile (4 Researches, 1 Short)

- Title: Do Energy-oriented Changes Hinder Maintainability? (Research)
>  
背景： モバイルアプリにおいてエネルギー効率も重要な品質要件 → が、効率の改善は簡単ではない  
調査： エネルギー効率を改善するための変更とその影響を調査 → 539のエネルギー効率関連のコミットについて Better Code Hub (BCH) を用いて保守性の変化を測定 → エネルギー効率向上の変更によって保守性が低下する（特に省電力モードとウェイクロック追加のエネルギーパターン関連のコード変更で顕著）

Tag_Efficiency, Tag_Physical, Tag_Survey, Tag_Android  
Tag_S_Mobile

モバイルアプリを開発したことないからあまりピンときていないけど、大抵はCPUの使用率を下げる（実行命令数を少なくする）ように実装するとエネルギー消費が低下するのか？ もちろんハードウェアの機能毎に消費量が違うから重み付けはしないといけないけど
___

- Title: Can Everyone use my app? An Empirical Study on Accessibility in Android Apps (Research)
>  
背景： ユニバーサルデザイン（様々なステータスの利用者を想定する）はアクセシビリティの向上を目的とする → アプリケーション開発者はアクセシビリティのサポートをどれだけ利用しているのかは不明瞭  
調査： マイニングベースのパイロット調査を実施 → 開発者はアクセシビリティAPIをほとんど使用していない ＆ APIを補助する説明文の利用は限定的。 StackOverFlowでの投稿を調査 → 開発者視点の整理 → アクセシビリティの困難さ/理解不足を開発者は経験

Tag_Accessibility, Tag_Design_Pattern, Tag_StackOverflow, Tag_Survey  
Tag_S_Mobile

アクセシビリティはアプリケーションだけじゃなくデバイスやら複合的な要素が絡むので難易度は高そう（というかそれこそデバイスが千差万別な以上、アプリ開発側は一般的なユーザしか想定しないのでは？）
___

- Title: Quantifying the Performance Impact of SQL Antipatterns on Mobile Applications (Research)
>  
背景： ローカルデータベースはモバイルアプリの重要なコンポーネント → 使用にはコストが伴う（モバイルの中では最もリソースを消費するコンポーネントの一つ） → 不適切な使用はレスポンス性に深刻な影響  
調査： データベース使用の問題となるプログラミング方法を調査 → 文献レビューとベンチマーク調査

Tag_Database, Tag_Resource, Tag_Survey  
Tag_S_Mobile

ここでのローカルデータベースはアプリケーション内部に組み込まれているデータベースということでいいのか？（なんかめっちゃ改竄できそうな感じがしてやばそう）
___

- Title: An Empirical Study of UI Implementations in Android Applications (Research)
>  
背景： UI のテストも自動化されてきた（Crawlersなど） → UI実装のメカニズムが大幅に変化  
調査： UI実装のための自動化技術が抱えている問題を調査 → 実際のアプリの大規模セットを調査（時間経過に伴う実践の変化も） → 動的分析が完全性（誤検出をしない性質）の面で課題アリ、開発慣行が変化し静的解析による追加解析も使用頻度が増加

Tag_UI, Tag_Test, Tag_Automation, Tag_Survey  
Tag_S_Mobile

記述を見るとUIの分野ではあまり静的解析がメジャーじゃなかったのか？（まあそうか、GUIは静的テストムズイわな）
___

- Title: Same App, Different Countries: A Preliminary User Reviews Study on Most Downloaded iOS Apps (Short)
>  
背景： モバイルアプリのレビューに関する研究では、ユーザレビューには豊富な情報が含まれている、とのことだった → でもそれはアメリカ国内のレビューでしょ？他の国は？  
調査： App Store のダウンロードトップ15のアプリ（2018年）の5か月間、9か国の英語圏の諸国からの300643のレビューを取得 → 3358件のレビューを手動で分類 → アメリカ国内での評価とは矛盾する要因アリ

Tag_Review, Tag_Survey, Tag_iOS, Tag_Nation  
Tag_S_Mobile

レビューはお国柄が出るのは同意（App Storeの日本のレビューってレビューじゃないよな）
___

## Bugs II (2 Researches, 2 Journals)

- Title: Improving Bug Triaging with High Confidence Predictions at Ericsson (Research)
>  
背景： バグのトリアージ（切り分け）はコストがかかる  
提案手法： Logistic Regression Classifier テキスト属性とカテゴリ属性を含む  
実装：  
実験： エリクソンの9つの大規模製品のレポートに対して適用（自動予測の実践） → 最大 Precision 78.09%, 最大 Recall 79.00 % → エリクソンのバグレポにはクラッシュダンプとアラームログが含まれていることがよくある → これを識別子に追加情報として追加 → Precisionが90%に向上したが、予測可能なレポートは62%になった

Tag_Review, Tag_Triaging, Tag_Learning  
Tag_S_Debug

どちらかというと実践についてのレポート？ 文章がコンガラガッテ主張がいまいち分からない
___

- Title: An industrial study on the differences between pre-release and post-release bugs (Research)
>  
背景： バグは開発において頻繁に発生 → バグの早期（リリース前）の発見技術が研究されている  
提案手法： リリース前に見つかるバグとリリース後に見つかるバグの特徴と違いについての産業的な研究を紹介 → 37の産業プロジェクトを分析、リリース前とリリース後に見つかるバグの違いを明文化  
調査結果： リリース後のバグの修正のほうが難度が高そう、複数の言語で記述されたソースコードや構成ファイルの更新も必要になる → リリース後のバグの約82%についてコードの追加が必要

Tag_Release, Tag_Debug, Tag_Survey  
Tag_S_Debug

ある意味リリースを重ねるに連れてバグ修正に手慣れる（もしくはバグが発生しにくいコーディングを実践できるようになる）のだろうとは思う。
___

- Title: Not all bugs are the same: Understanding, characterizing, and classifying bug types (Journal)
>  
背景： GitやSVNなどのバージョン管理システムはバグ追跡メカニズムが存在 → 開発者はバグレポートからバグを認知可能  → トリアージ（分類）補助の研究は色々あるが、報告されたバグの分類を理解を補助する手法の研究は少ない  
調査： 1) Mozilla, Apache, Eclipse などに属する119のプロジェクトの1280のバグレポートを分析 2) 自動分類モデルを考案、評価 → システム全体のバグ原因を9つに分類、モデルは高いF値 64%を達成

Tag_Triaging, Tag_Debug, Tag_Review, Tag_Modeling  
Tag_S_Debug

？最終的にはトリアージしてない？（読み間違えたかな…） 人間視点でもわかりやすい分類方法を考案したということなんだろうか（原因別の分類）
___

- Title: Identifying and Predicting Key Features to Support Bug Reporting (Journal)
>  
背景： バグレポートは開発者がバグ把握に重要 → 提出者が優れたレポートを書けるとは限らない → **提出者がバグレポート提出時に（開発者にとってわかりやすい情報を書く）機能（再現手順など）を見落としている**  
調査： Camel, Derby, Wicket, Firefoxm, Thunderbird のケーススタディでは 再現手順、テストケース、スタックトレースなどの情報が省略されるとバグ修正に影響があることを確認  
提案手法： 提出者へバグレポート内に必要な情報を予測・提供する手法 （分類モデル）
実装：  
実験：

Tag_Debug, Tag_Review, Tag_Recommend, Tag_Prediction  
Tag_S_Debug

バグレポートに必要な情報が全然ないことはままある（どういうバグなのか、どういう設定なのかとか）。 個人的には興味あり
___

## AI Application (2 Researches, 1 Industry, 2 Shorts)

- Title: Tracing with Less Data: Active Learning for Classification-Based Traceability Link Recovery (Research)
>  
背景： 既存研究で、Traceabilityの確立と維持は重要だが困難と判明 → アーティファクト間のトレーサビリティリンクの回復はコストがかかる → 自動化できると嬉しいし、データが豊富な環境下では自動修復が効果的という結果アリ → が、実際にはデータが限定的  
提案手法： 教師付き分類手法で必要なトレーニングデータを大幅に削減する Active Learning に基づく手法  
実装：  
実験：

Tag_Learning, Tag_Traceability, Tag_Limited_Data  
Tag_S_Learning

データが少ないというのが機械学習関連ではよく当たる課題の模様。
___

- Title: Deep Learning Anti-patterns from Code Metrics History (Research)
>  
背景： アンチパターンは再発生する設計問題のジャンルでは不十分（設計問題のアンチパターンが未熟） → 様々な検出技術の動機となるアンチパターンの悪影響が存在 → アンチパターンの検出を主軸とした結果、いくつかの貴重な情報を見逃す可能性  
提案手法： Convolutional Analysis of code Metrics Evolution (CAME) バージョン管理システムからパターンマイニング → アンチパターンの存在を推測  
実装：  
実験： 3つのシステムでの God Class アンチパターンに対するアプローチを評価 → ソースコードメトリクスの履歴を利用すると精度が向上、CAMEが既存の静的機械学習分類子よりも優れている、既存の検出ルールよりも優れている

Tag_Learning, Tag_Design_Pattern, Tag_Metrix  
Tag_S_Learning

英語力の問題で、アンチパターンの立ち位置があいまいになった。 (1) アンチパターンの検出に焦点を当てた結果、精度が下がる (2) アンチパターンの存在が精度を下げている → どうにも(2)っぽい実験結果なんだが、序盤を見ると(1)っぽくも見える…
___

- Title: An Approach to Recommendation of Verbosity Log Levels Based on Logging Intention (Industry)
>  
背景： ログの冗長度は色々なランタイムイベントの識別に有用 → 各ログステートメントに適切に割り当てる必要あり（不適切だと混乱を招く） → ガイドラインがないので達成が難しい → 既存研究では定量的メトリクス（ログの密度など）でロギング特性を明確にしているが、ログ内部まで見ていないのでレベルの決定への貢献は限定的  
提案手法： VerbosityLevelDirector ログレベルの決定を自動化する手法 → ログを行うコードコンテキス関数に基づく  
実装：  
実験： 4つのOSSプロジェクトで効果を測定 → VLDはレベルの識別に高いパフォーマンスを発揮、ベースラインアプローチよりも優れている。 また、不適切なレベルの構成を検出可能

Tag_Logging, Tag_Metrix, Tag_Automation  
Tag_S_Learning

ログのレベル（冗長度）がいまいちまだ理解しきれていない（類似度からログの種類を識別する？重要度を識別する？）
___

- Title: Automated Characterization of Software Vulnerabilities (Short)
>  
背景： 脆弱性を把握するのに、CVEがよく使われる → CVEのレポートには 説明、開示ソース、NIST VDO (Vulnerability Description Ontology: 特性タグ) が付随 → 執筆に専門知識が必要なこともあり、レポートが不正確・不完全になる可能性がある（特にタグ付け）  
提案手法： CVEレポートのテキストからVDOタグを自動識別する手法 → VDOの一つにマッピングされた365の脆弱性のレポートをデータセットとして利用 → 6つの分類アルゴリズムを生成  
実装：  
実験： 6つの分類アルゴリズムのパフォーマンスを評価 → 全部正確な結果を生成 → その中でSVMが一番正確だった

Tag_Learning, Tag_Review, Tag_Natural, Tag_Automation  
Tag_S_Learning

テキストパターンの把握を主眼に据えているっぽい。 実験結果からSVMが最優秀だったみたいだけど、どうなんだろ（2値分類じゃないならSVMだと難しそうな印象だが）
___

- Title: Learning to Identify Security-Related Issues Using Convolutional Neural Networks (Short)
>  
背景： セキュリティは大事なんだが、機能と同時に堅牢なセキュリティを実現しようとするとバランス調整がムズイ（特にアジャイルの文脈で） → セキュリティへの焦点を自動化についての設計と開発  
提案手法： Ergo SecureReqNetという問題追跡システムがセキュリティも見ているかを自動識別する手法を採用 → 2フェーズ（CVEに登録されている数十万の脆弱性の説明とOSSプロジェクトから得られた問題説明で word embedding を学習 → 学習結果からある問題がセキュリティ関連であるかどうかを予測するNNをトレーニング）  
実装：  
実験： GitLabとGitHubのプロジェクトからマイニングされたデータセットで評価 → セキュリティ関連の問題の特定に成功 → OSSでは96%、産業要件では71.6%の精度を達成

Tag_Learning, Tag_Security, Tag_Natural  
Tag_S_Learning

セキュリティ関連のテキストかどうかを識別する学習。 これ識別できると何がうれしいんだろう。
___

## Clones and Refactoring (2 Researches, 1 Industry, 2 Shorts)

- Title: TECCD: A Tree Embedding Approach for Code Clone Detection (Research)
>  
背景： コードクローンの検出技術の歴史は深い → DL技術の登場で検出能力が向上 → 一般にASTから二分木構造への変換をし、 term embedding を行う  
提案手法： TECCD 新規embedding手法 → ASTの各中間ノードのノードベクトルを取得 → ツリーベクトルを生成 → ツリーベクトル間のユークリッド距離を測定（コードクローンの判定）  
実装：  
実験： BigCloneBench (BCB) と他の7つの大規模Javaプロジェクトで評価 → 優れた精度を達成

Tag_Code, Tag_Clone, Tag_Learning  
Tag_S_Refactoring

木構造をベクトル化して、木同士の距離を測定することでコードクローンかの判定をする、というのはおそらく既存手法では？ となるとどこまで embedding が功を奏したかだが…
___

- Title: Investigating Context Adaptation Bugs in Code Clones (Research)
>  
背景： 不適切なコードクローン（コードのコピペ）はバグを誘発するという考えがある → が、詳しく調査はされていない（バグが発生したコード内にコードクローンがあるかの研究はある）  
調査： コードクローン由来のバグ（コンテキスト適応バグ、コンテキストバグ） を2つのパターンを定義して分析 → Java, C, C# で記述された6つのOSSプロジェクトで調査 → 結構バグあるぞよ → クローン関連のバグ修正は50%がコンテキストバグの修正の可能性（特に異なるリビジョン、ファイル間のクローンでは確率が上昇する傾向）

Tag_Code, Tag_Clone, Tag_Debug, Tag_Survey  
Tag_S_Refactoring

ワシもよくコードはコピペしますねぇ（プロジェクト内からもWebからも）。 先輩の研究ではやはりこの手の研究は実装に時間がかかる模様
___

- Title: Decomposing God Classes at Siemens: A Visualization tool and approach (Industry)
>  
背景： God Class への対処などを含めた3年間のレガシーシステムの再構築  
提案手法： ソフトウェアの視覚化ツールとそれに伴うプロセス → 事前知識なしで、God Classの分解が 1、2時間でできるようになった（一般には1週間かかることもある）  
実装：  
実験：

Tag_Design_Pattern, Tag_Restructure, Tag_Visualization  
Tag_S_Refactoring

二件目のGod Class関連論文（Practice）。 God Classって意外とレガシーシステムにも多いのだろうか。 もしレガシーシステムの保守などをするのであれば、気になる論文（God Class限定だとちょい局所的だが）
___

- Title: Tracy: A Business-driven Technical Debt Prioritization Framework (Short)
>  
背景： 技術的負債は開発において蔓延っている状況 → 開発チームは優先順位を付けてる必要がある  
提案手法： Tracy 技術的負債の優先順位付けを行うためのフレームワーク → 探索、エンジニアリング、評価の3フェーズが開発プランとしてあり、現在評価フェーズ  
実装：  
実験： 3社12グループ49人で評価 → 優先順位付けがビジネスの意思決定に貢献できる可能性

Tag_Dev, Tag_Metrix, Tag_Cost, Tag_Technical_Debt  
Tag_S_Refactoring

Technical Debt: 技術的負債。 選択した解決策に付随する追加コストを反映すること。（本当に低コストなのかを調べること？）  
表面上のコストと実際のコストには差があるという前提で、実際のコストを算出して順位付けをしようという試み、だと理解
___

- Title: Self-Admitted Technical Debt Removal and Refactoring Actions: Co-Occurrence or More? (Short)
>  
背景： 技術的負債は適切な解決策を欠如させる可能性がある → Self-Admitted Technical Debt (SATD) コメントやコミットメッセージによる導入（Admittance）  
調査： リファクタリングとSATD削除の関係性を調査 → 4つのOSSプロジェクトでSATDとその削除をデータセットとして利用 → 自動リファクタリング検出ツールとともに関係性を調査 → リファクタリングとSATDの削除には相関がありそう

Tag_Dev, Tag_Learning, Tag_Cost, Tag_Technical_Debt  
Tag_S_Refactoring

結局SATDが何なのか分らぬ…（Admittanceの適当な訳が分からん）。 あくまでリファクタリングとの因果関係までは調査していない模様なので、過信しすぎないよう
___

## Change (2 Researches, 1 journal, 2 Shorts)

- Title:
>  
背景：  
提案手法：  
実装：  
実験：

- Title:
>  
背景：  
提案手法：  
実装：  
実験：

- Title:
>  
背景：  
提案手法：  
実装：  
実験：

- Title:
>  
背景：  
提案手法：  
実装：  
実験：

- Title:
>  
背景：  
提案手法：  
実装：  
実験：

## Testing and Coding (2 Researches, 1 Industry, 2 Shorts)

## Text Analysis and Empirical Studies (2 Researches, 4 Shorts)

## Coding and Repair (1 Research, 1 journal, 4 Shorts)

## APIs, Programming, and CI (1 Research, 2 Journals, 2 Shorts)

## Perspective (1 Research, 4 Industries)

## Late Breaking Ideas (5 Ideas)

## Testing (2 Researches, 1 Journal, 2 Shorts)

## Systems and Configurations (2 Researches, 1 Industry, 2 Shorts)

## Comprehension and Empirical Studies (3 Researches, 2 Shorts)

## Architecture (3 Researches, 1 Industry)
