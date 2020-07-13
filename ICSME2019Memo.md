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

- Title: Identifying the Within-Statement Changes to Facilitate Change Understanding (Research)
>  
背景： 現在の木差分手法はステートメント内部の粒度になると、その更新を表現できない  
提案手法： ChangeDistiller ステートメント内の変更を識別するための木差分手法 → 編集操作を計算、各操作のメタデータを作成（操作タイプ、エンティティのタイプ、コンテンツなど関連する全参照を包含）  
実装：  
実験： 4つのOSSプロジェクトで条件式の変更を調査 → 状態に影響を与えるかなどを調査 → 20%が重要ではない変更、60%以上が効果的な変更を含む → また、多くの共通パターンを発見

Tag_Presentation, Tag_Code, Tag_Diff  
Tag_S_Change

プログラム表現の一種、だと思う。 そういう意味ではアイデア出しの中で出てきた奴と関連はありそう。
___

- Title: Aiding Code Change Understanding with Semantic Change Impact Analysis (Research)
>  
背景： コードレビューは変更とその影響を手動で調べることになるが、領域外への影響については調べるのが難しい → 差分による影響解析は有望な手法  
提案手法： 構文変更ではなく意味変更の影響を抽出する新手法（JSを対象） → 4つの意味的変化の影響関係の定義、JSプログラムの部分的構造変化を解釈、関係の抽出  
実装：  
実験： 3つのNodeJSアプリケーションの2000コミットで評価 → FPを9-37%削減、変更の影響範囲サイズを19-91%削減

Tag_Diff, Tag_Slice, Tag_Semantics  
Tag_S_Change

差分影響解析において影響範囲をより正確に抽出した、という論文だが、見逃しが発生していないか不安
___

- Title: Why is my code change abandoned? (Journal)
>  
背景： すべてのコード変更がマージされるわけではない → マージされない変更は破棄や再送信が発生するので、コストが嵩む（あるいは無駄が発生する）ことになる  
調査： 4つのOSSプロジェクト（ Eclipse, LibreOffice, OpenStack, Qt ）で変更破棄の理由を調査 → 1459の破棄された変更を手動で分析、ラベル付け、12のカテゴリに分類 → 分布を調査 → 破棄変更の大半は冗長な変更（すでに変更済み）、12のカテゴリの分布は4つのプロジェクトで類似、破棄される場合、1年以内に98.39%が破棄

Tag_Version, Tag_Survey, Tag_Merge  
Tag_S_Change

破棄理由のサーベイ、バージョン管理系の研究をするなら面白そうかも
___

- Title: Towards Generating Transformation Rules without Examples for Android API Replacement (Short)
>  
背景： あるAPIが使えなくなると、そのAPIを利用しているプログラムの開発者は遅かれ早かれAPIを置換せにゃならぬ → 代替APIの使い方が正確に把握できないと、置き換えが困難になる可能性 → API変更の理解が大事  
提案手法： No Example API Transformation (NEAT) Android API について非推奨となったAPIの置換を支援 → 置換ルールを生成  
実装：  
実験： 100の非推奨APIから37について正しい置換ルールを生成

Tag_Android, Tag_API, Tag_Version  
Tag_S_Change

API置換という意味ではYさんのテーマと近い（あるいは読んでいる可能性）。 置換ルールをどう持ってきているのかが気になるところ
___

- Title: How Do Code Changes Evolve in Different Platforms? A Mining-based Investigation (Short)
>  
背景： コードの変更はモバイルプラットフォームか否かで方法が異なる → プラットフォームの違いがコード変更の進化 (evolve) にどう影響するかは未調査  
調査： 変更頻度、ソースコード、ビルド、テストの変更がモバイル/非モバイルでどのように共進化するのかを調査 → 非モバイルでは1月あたりのコミット数が多い、モバイルでは混乱要素を制御する場合にはコミット数が極端に減る

Tag_Code, Tag_Mobile, Tag_Survey, Tag_Co_Evolve  
Tag_S_Change

共進化(Co-Evolution/Co-Evolve)再び。 うーむ。 Abst読む限りだと、コミット数にしか変化がなかったように見えちゃう
___

## Testing and Coding (2 Researches, 1 Industry, 2 Shorts)

- Title: How the Experience of Development Teams Relates to Assertion Density of Test Classes (Research)
>  
背景： ソフトウェアテストでは開発者の経験が活きる（経験が活かされる有望株がテスト）  
調査： 開発チームの経験とアサーション密度（テストクラスのKLOCあたりのアサーション数）との相関を調査 → チームの経験などを12のソフトウェアプロジェクトのテストクラスのアサーション密度と関連付けるモデルを構築 → 57人の開発者への調査と統計モデルを比較 → 関係ありという結果

Tag_Human, Tag_Test, Tag_Assert, Tag_Survey  
Tag_S_Test

なぜアサーション密度？ 経験が多いほうがアサーション密度が高い？低い？ Abstだけでは結果や相関が読み取れず
___

- Title: Automatic Discovery and Cleansing of Numerical Metamorphic Relations (Research)
>  
背景： Metamorphic Relations (MR: 変性関係) → プログラムの入出力の間の Invariant   
提案手法： AutoMR 体系的にMRを推論する新手法 → Particle Swarm Optimization を通じて色んな等式 MR、不等式 MRを検出 → 冗長なMRも削除可能  
実装：  
実験： AutoMRが正確かつ簡潔なMRを効果的に推論 (vs state-of-the-art approach)

Tag_Invariant, Tag_Inferring, Tag_MR  
Tag_S_Test

プログラムの入出力間のInvariantとなると、Invariantをボトムアップ的に（Statement→Method→Class→Program）積み上げていく感じだろうか。 ある意味モデリングと近い分野
___

- Title: Slimming JavaScript Applications: an Approach for Removing Unused Functions from JavaScript Libraries (Journal)
>  
背景： JavaScript開発ではバンドル（アプリと依存ライブラリコード）をリリースするのが一般的 → バンドルの中に使わないライブラリが存在 → サイズの増加、応答性や処理の低下 → 静的解析で未使用コードを削除する研究はまだ改善の余地あり  
提案手法： Unused Foreign Function (UFF) の概念を定義、UFFを識別する動的アプローチ  
実装：  
実験： 22のJSアプリケーションでのケーススタディ → 平均26%のサイズ削減が実現（最大66%）

Tag_Library, Tag_UFF, Tag_Efficiency  
Tag_S_Test

ライブラリ全体をインポートすると使わない関数も一緒に取り込まれちゃうのはよくある。 単純にライブラリ内の関数リストと使用された関数を比較しているだけ感はあるが、意外と盲点だったかも
___

- Title: Automated Identification of Over-Privileged SmartThings Apps (Short)
>  
背景： SmartThings → アプリがデバイスを直接叩かずに提供された関数を介して権限を取得する → この関数内に欠陥があると不正な権限取得へつながる → 時に深刻  
提案手法： SmartThings の過剰権限の脆弱性を自動検出するツール → 一般的なパターンについてのパターンマッチ  
実装：  
実験： 222の公式アプリとTPCに対して評価 → 5.5%のデバイスで計76の過剰権限のインスタンスを検出

Tag_Security, Tag_Debug, Tag_Mobile  
Tag_S_Test

検出数がインスタンスなのが若干気になるところ（同じコンテキストのインスタンスが延べ数でカウントされてない？）
___

- Title: EmoD: An End-to-End Approach for Investigating Emotion Dynamics in Software Development (Short)
>  
背景： ソフトウェア開発において感情認識への関心が高まっている → 既存研究では感情の動的な性質（？）をスルー → あるタイミングでの感情しか抽出していない（連続性がない？）  
提案手法： EmoD チーム内のコミュニケーション記録を自動収集し、その中の感情と強さを識別、感情ダイナミクスをモデル化  
実装：  
実験： 自動データ収集、モデリングなどを通じて、感情認識の実践を提供できていることを確認

Tag_Human, Tag_Dev, Tag_Modeling  
Tag_S_Test

心理学みたいなことやってらっしゃる。 一般論として、汎用的な感情のモデリングなんてできるのかね？と懐疑的
___

## Text Analysis and Empirical Studies (2 Researches, 4 Shorts)

- Title: Know-How in Programming Tasks: From Textual Tutorials to Task-Oriented Knowledge Graph (Research, Award)
>  
背景： タスク解決活動とそれらの関係、属性 → ノウハウ知識 → 一般にプログラミング関係のノウハウは半構造化されたテキスト → 3つの障壁（タスクインテントの非一貫性モデル、チュートリアル情報のオーバーロード、構造化されていないタスクアクティビティの説明） → 既存のナレッジグラフ (Knowledge Graph) はノウハウ情報（API, APIの警告, APIの依存関係など）のみを抽出  
提案手法： Open Information Extraction (OpenIE) 結果として得られるナレッジグラフ TaskKGにアクティビティの階層分類、3種類のアクティビティ関係、5種類のアクティビティ属性が包含  
実装：  
実験： Android Developer Guide に適用 → ユーザ調査で開発者がプログラミングのハウツーの期待通りの回答取得の支援に有望

Tag_Graph, Tag_Natural, Tag_Knowledge, Tag_Dev  
Tag_S_Analysis, Tag_S_Studies

ナレッジグラフがどういうグラフを指すのかは分からないが、共同研究で参考になるかも
___

- Title: An Empirical Study of Abbreviations and Expansions in Software Artifacts (Research)
>  
背景： 略語の展開は開発者の理解を深める → 略語が展開できないと、開発者はコード理解により多くの時間を消費する（もったいない） → 一般的な手法では精度が60%程度行けばいいほう  
調査： 略語とその略語がどこで発生するのかを調査 → 5つのOSSシステムから抽出された略語と展開のペアから、特性を明確にする → 特性から現在の手法を比較・評価

Tag_Natural, Tag_Dev, Tag_Human, Tag_Survey  
Tag_S_Analysis, Tag_S_Studies

略語が何を指しているのかわからないこと、ありますあります。 そういう意味では面白い研究（すでに数件citation付いてた）。
___

- Title: Estimating Software Task Effort in Crowds (Short)
>  
背景： ソフトウェアメンテナンスにおいて、問題の改善と詳細化は重要 → 重要度、担当者、解決への推定コストなどの追加情報も必要  
調査： クラウドワーカーを利用している場合の推定コストをプランニングポーカーを用いて見積もるための調査　→ 見積もりの利点の整理

Tag_Human, Tag_Dev, Tag_Survey, Tag_Crowed_Sourcing
Tag_S_Analysis, Tag_S_Studies

Crowed Worker: クラウドソーシング（一般大衆の知見を利用して問題解決にあたる手法、不特定多数に外注する手法、誰かが解決してくれるだろうという期待）、 Planning Poker: マイクロソフトが出している（？）タスク見積もりのカード（ラフな感じ）  
パッと理解ができなかったが、タスク推定とクラウドソーシングの相性を調査した、でいいのかな
___

- Title: Do as I Do, Not as I Say: Do Contribution Guidelines Match the GitHub Contribution Process? (Short)
>  
背景： GitHubなどでは、開発者に順守してほしい投稿ガイドラインを設定している → 実際にどれだけガイドラインが遵守されているかを体系的に調べられていない  
調査： 53のGitHubプロジェクトについて調査 → プロセスモデルを作成、実際のアクティビティとガイドラインとを比較 → 訳68%が予想されるプロセスと大きく異なる（遵守していない）

Tag_Github, Tag_Human, Tag_Dev, Tag_Survey  
Tag_S_Analysis, Tag_S_Studies

確かにワシGitHubのガイドライン読んでないなぁ
___

- Title: An Analysis of 35+ Million Jobs of Travis CI (Short)
>  
背景： Travis CI → GitHubと提携しているCI支援のためのプラットフォーム  
調査： Travis CI のユーザや利用開始の基準、構成を変更する頻度などを調査 → 利用者にはMicrosoftもいた、Travis上で最も人気の高いPythonはGitHubでは3番目、レポジトリセットアップから平均7日でTravisがセットアップ、Travis内のジョブの60%がテスト

Tag_Github, Tag_CI, Tag_Survey, Tag_Travis_CI  
Tag_S_Analysis, Tag_S_Studies

Travis CI はテスト環境などをTravisサーバ上で構成できるので、環境構築が簡単に。 そうか、Pythonが3番目まで来ちゃったか、という印象
___

- Title: Linguistic Change in Open Source Software (Short)
>  
背景： コード辞書 (code lexicon) は自然言語と同様に進化論の範疇にある（？）   
調査： OSSのコード辞書の進化を統計的に分析 → 2000のOSSで調査 → 時間経過とともに言語的アイデンティティが大幅に変化する、コード辞書の構文構造が異なれば進化方法も異なる、メンテナンスアクティビティがコード辞書へ影響を与える

Tag_Survey, Tag_Co_Evolve, Tag_Natural, Tag_Code  
Tag_S_Analysis, Tag_S_Studies

コード辞書が何なのか調べてもピンと来ない（レシピブックみたいなもん？） そして度々出てくる進化のキーワード
___

## Coding and Repair (1 Research, 1 journal, 4 Shorts)

- Title: Learning How to Mutate Source Code from Bug-Fixes (Research)
>  
背景： Mutant Testing (変異テスト) → テストケース生成を誘導したり、テストスイートの評価に利用 → 実際の障害から変異操作を考案する手法がある → が、コスト高くエラー率が高い → テスターが変異させるかどうかの意思決定には役立たない  
提案手法： 実際の障害から変異を学習する新手法 → 細かい差分、こーどの抽象化、変更のクラスタリングで前処理 → DLを用いて 変異モデルを学習  
実装：  
実験： GitHubからマイニングされたバグ修正のデータセットでトレーニング、評価 → 経験的に、修正されたバグと類似した変異ケースを9-45%で予測、変異後も構文的なエラーは98%で発生しなかった

Tag_Code, Tag_Learning, Tag_Test, Tag_Mutant  
Tag_S_Code, Tag_S_Repair

変異テスト: 小さく（条件分の中など）変えたコードを生成し、失敗することを想定してテストケースを実行する（成功してしまうと、テストや制御構造に問題があることがわかる）
___

- Title: Five recommendations for software evolvability (Journal)
>  
背景： ソフトウェアの進化可能性 (evolvability) は3つの要素（進化するシステムプロパティ、人間的要素、進化の需要）の積  
解説： ソフトウェアの進化可能性を強化する5つの推奨事項について説明 → ソフトウェア変更の定義済みプロセス、コードの進化部分と安定部分の区別、分析可能なコードセグメント、重要な概念のカプセル化、ラッピングの回避

Tag_Co_Evolve, Tag_Code, Tag_Human, Tag_Dev, Tag_Survey  
Tag_S_Code, Tag_S_Repair

Abst短すぎるっぴ。 サーベイよりも解説寄りのジャーナル
___

- Title: Personalized Code Recommendation (Short)
>  
背景： コードのリコメンドについての最先端手法は、ほとんどがcrowd-based → プログラマーが異なればコーディングパターンも異なる、Crowdにやると特定のプログラマー向けのコードリコメンドのパフォーマンスが落ちる可能性  
提案手法： プログラマー個人のコーディングパターンに焦点を当てたコードのリコメンド手法 → 変数宣言と初期化コードのリコメンドモデルを作成 → コーディング履歴に基づいて、個人のコーティングパターンを学習  
実装：  
実験： 効果的であるという結果 → Top1で62%、Top3で70%の精度（ベースライン比大幅改善）

Tag_Recommend, Tag_Code, Tag_Human, Tag_Learning  
Tag_S_Code, Tag_S_Repair

個人向けにコーディングを学習してくれるのはニーズがありそうだが、万人に対して学習ができるのかは不明
___

- Title: Syntax and Stack Overflow: A methodology for source code error and fix extraction (Short)
>  
背景： 構文エラーの修正に役立つ情報の一つは、構文エラーの代表例を取得すること → 実際の構文エラーデータセットは、一般的な開発者の集団を表現できていない（公開されていなかったり、初心者からのデータだったり）  
提案手法： 一般的な構文エラーを抽出するための手法と構文エラーの研究に役立つ対応する修正データセット → 62965の Python Stack Overflow のコードスニペットデータセット  
実装：  
実験：

Tag_Learning, Tag_Syntax, Tag_Code_Fix, Tag_StackOverflow  
Tag_S_Code, Tag_S_Repair

そもそもStackOverflowとかを利用する集団が開発者一般と対応していない気が。
___

- Title: BarrierFinder: Recognizing Ad Hoc Barriers (Short)
>  
背景： アドホック同期はマルチスレッドプログラムで一般的になってきている → 多様かつ複雑なので、同期関係の近いは困難 → が、重要 → 既存手法は基本的なアドホック同期を部分的に検出可能 → 全実装を理解したり、強制同期を推測できない  
提案手法： BarrierFinder 複雑なアド北同期を完全自動で識別する手法 → インターリーブの効率的な探索のためにプログラムスライスや制限付き記号実行を利用 → トレースを利用してアドホックバリアを識別  
実装：  
実験： 効果的かつ効率的という結果

Tag_SymExe, Tag_Slice, Tag_Sync  
Tag_S_Code, Tag_S_Repair

意外と見なかったマルチスレッド関係の論文。 同期の自前実装は実際検証が手間（実装も手間）
___

- Title: Impact Analysis of Syntactic and Semantic Similarities on Patch Prioritization in Automated Program Repair (Short)
>  
背景： パッチの優先順位付け → 正確さの確率に基づいてパッチをソート → バグ修正時間を最小化、自動プログラム修正の精度の最大化に貢献 → 既存文献の手法では、欠陥コードと修正要素間の構文的or意味的な類似性から順位付け  
提案手法： 構文的 and 意味的 な類似性の積で分析する手法 → 変数類似性などを利用して意味的売り自制を測定、正規化された最長共通サブシーケンスを利用して構文類似度を測定  
実装：  
実験： IntroClassJava ベンチマークから22個の置換変異バグを選択、評価 → 22個すべてを修復（精度100%）

Tag_Patch, Tag_Debug, Tag_Learning  
Tag_S_Code, Tag_S_Repair

精度100%？ 俺は騙されんぞ（） インターセクションを取るからには、両方の尺度を正規化せにゃならんだろうけど、どうなんすかね
___

## APIs, Programming, and CI (1 Research, 2 Journals, 2 Shorts)

- Title: Losing Confidence in Quality: Unspoken Evolution of Computer Vision Services (Research)
>  
背景： コンピュータービジョンといったMLの応用先は、アクセシビリティとシンプルさが魅力的 → 複数のベンダがこれらの技術を提供 → メンテナンスと進化のリスクについての調査はない（特に動作の一貫性と機能の透明性）  
調査： 3つの異なるデータセットを使用して11か月の間3つのサービスについてのアウトプットを評価 → サービス動作に一貫性がない、アウトプットの進化リスクが存在、リスク・不整合を文書化する明確なコミュニケーションが存在しない

Tag_Learning, Tag_Survey, Tag_Service  
Tag_S_API, Tag_S_Code, Tag_S_Dev

Computer Vision: コンピュータが画像や動画をいかによく理解できるか、を扱う研究分野  
モデルが時間経過とともに進化（挙動が変わる）していくという結果。ただ、それが精度が向上した結果なのか、本当に出力が異なる（前にできていたことができなくなった）のかで評価が変わりそう
___

- Title: Live Programming in Practice: a Controlled Experiment on State Machines for Robotic Behaviors (Journal)
>  
背景： ライブプログラミングは複数の言語で利用されつつある → 現実的なシナリオや複雑なAPIを使用した場合の利点について未調査  
調査： 機械的な動作を State Machine に落とし込み、ライブプログラミングの利点を分析 → プログラムの理解と作成を分析 → Robotic Behavior のコンテキストでは、プログラムの理解や速度・正確性の…で非ライブ言語を大幅に上回らない（大差ない）

Tag_Live_Programming, Tag_Survey, Tag_State_Machine  
Tag_S_API, Tag_S_Code, Tag_S_Dev

ここでの Robotic Behavior がロボット工学的な意味合いなのか判別できなかった（英語力ェ…） ライブプログラミングは見てる人の属人化が起きちゃう気がして、そんな頻繁には利用できないイメージ

- Title: Source Code Properties of Defective Infrastructure as Code Scripts (Journal)
>  
背景： 継続開発の文脈で、IaC (Infrastructure-as-Code) の欠陥は開発の自動化やパイプラインの信頼性を損ねる可能性 → ハードコードされた文字列などのプロパティが、IaCの欠陥と相関があるのではと仮定  
調査： OSSレポジトリからマイニングされた欠陥関連のコミットに定性分析を適用 → 欠陥のあるIaCと相関のあるプロパティを特定 → 4つのデータセットから2439のスクリプトとそのプロパティを使用して欠陥予測モデルも構築 → 10個の欠陥関連のプロパティを識別 → 欠陥IaCとの相関が認められる

Tag_Learning, Tag_IaC, Tag_Prediction, Tag_Survey  
Tag_S_API, Tag_S_Code, Tag_S_Dev

IaC再び。 ハードコードされると保守性が悪くなる、のか？
___

- Title: Inappropriate Usage Examples in Web API Documentations (Short)
>  
背景： APIの学習にドキュメントが利用されるが、そのドキュメントが信頼できない可能性もある  
調査： 使用例と出力例からOpenAPIの仕様を抽出し、Web APIドキュメントと比較、不適切なドキュメントの特性を調査 → エンドポイントの約65.5%に不適切な使用例が存在 → 4つのカテゴリに分類（ドキュメント化されていない、動的な不一致、リターンしないパターン、型の不一致）

Tag_Learning, Tag_API, Tag_Document, Tag_Survey  
Tag_S_API, Tag_S_Code, Tag_S_Dev

鷲崎先生の論文。 ドキュメント内の矛盾を識別する調査？
___

- Title: What Do Developers Discuss about Biometric APIs? (Short)
>  
背景： 生体認証技術は非常に関心が強くなってきている → が、そのAPIについて使用方法を説明している文書は十分ではない → 利用する開発者の負担大（頻繁にAPIが更新されることも一因）  
調査： Stack Overflow, Neurotechnology などのオンラインメディアから生体認証API関連の投稿500件を手動で分析 → 発生問題のほとんどで正確なドキュメントが欠如が原因、生体認証APIの非互換性が複数の実装環境でまたがっている

Tag_API, Tag_Document, Tag_StackOverflow, Tag_Survey  
Tag_S_API, Tag_S_Code, Tag_S_Dev

生体認証はデバイスも絡んでくるから通常の開発とは経路が違う。 結局はAPIのガイドラインやドキュメントが不十分だぞ、ということを言いたい？
___

## Perspective (1 Research, 4 Industries)

- Title: Teaching Software Maintenance (Research)
>  
実践： アメリカの大学二年生（メンテナンス入門生）のソフトウェアメンテナンスの授業で、扱うプロジェクトの規模を大きくしてみた場合の利点についての実践レポート → ソフトウェアエンジニアリングの主要なトピックについて導入が簡単になった、OSSコミュニティへの有意義な貢献が示された

Tag_Human, Tag_Teaching, Tag_Practice  
Tag_S_Perspective

こんな形式の論文もあるんやなって。 俺プログラミング習ったの大学二年からだったなぁと回顧
___

- Title: Continuous Collateral Privacy Risk Auditing of Evolving Autonomous Driving Software (Industry)
>  
背景： 自動運転の技術では多くのセンサーの情報を収集 → プライバシーとつながる可能性（リスク） → Collateral Privacy Risk  
実践： Apollo プロジェクトでのプライバシーリスクについて分析 → 未解決の問題も残ったが、ソースコードベースの監査手法から予備結果を出力 → 監査の過程でバージョンが3.0から3.5へ → その過程の経験と困難をレポート化

Tag_Hardware, Tag_Practice, Tag_Security  
Tag_S_Perspective

ハードウェア依存のセキュリティについての実践。 ソースコード解析なので、何かしら仕様から抽出したパターンマッチをしているのだろうけど、仕様の見逃しが怖い
___

- Title: Challenges in re-platforming mixed language PL/I and COBOL IS to an open systems platform (Industry)
>  
背景： 再プラットフォーム化 (re-platforming: レガシーシステムを新しいプラットフォームへ移行すること) はレガシーシステム保守のコスト削減の矢面に立つ → 技術的・組織的課題が伴う（コスト削減したいんだけど難しい）  
解説： 再プラットフォーム化の課題と解決策を提示。 40年前のPL/I、COBOLアプリケーションの再プラットフォーム化で得られた教訓について説明

Tag_Practice, Tag_Cost  
Tag_S_Perspective

レガシーシステムをどうするかという点ではGの参考にはなりそう（想定が異なる感は否めないが）
___

- Title: Application of Philosophical Principles in Linux Kernel Customization (Industry)
>  
背景：  
提案手法：  
実装：  
実験：

Tag_Human, Tag_Philosophy, Tag_Linux  
Tag_S_Perspective

Abst長すぎぃ！ ななめ読みするとソフトウェアエンジニアリングと哲学的な原則は共通部分があり、哲学的原則を研究することでSEへ還元できる（応用できる）といいたい？ どちらかというと開発や維持に哲学的思考を使うとベネと言っている、のか？  
SEの概念を日常に見出す（あるいはその逆も）ことはあるけど、ぶっちゃけここまで深くは考えていない
___

- Title: Lessons Learned from Large-Scale Refactoring (Industry)
>  
説明： Googleでは数億行のコードを含む大規模な多言語コードベースを維持 → 過去数年にわたり、所属チームでコードベースを大規模に効率的に更新するプロセスを開発 → 学んだ教訓と未解決の問題について説明

Tag_Practice, Tag_Google  
Tag_S_Perspective
___

## Late Breaking Ideas (5 Ideas)

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

## Testing (2 Researches, 1 Journal, 2 Shorts)

- Title: An Empirical Study of the Relationship between Continuous Integration and Test Code Evolution (Research)
>  
背景： CIはコード統合の頻度を自動化する実践 → 広く利用されてきた → 早期のエラー特定に有用 → CIが新テスト手法の導入を阻害していないかは不明瞭  
調査： CIを採用しているプロジェクトと非採用のプロジェクトをそれぞれ82個ずつ調査 → 全体で3936バージョンに対して、テストコード比率とカバレッジを調査 → CIプロジェクトのほうがテストコード比率が高くなる傾向（カバレッジの改善も見られる） → CIは健全なテストとその進化を後押ししている

Tag_CI, Tag_Dev, Tag_Survey, Tag_Test  
Tag_S_Test

ここまでCIを賛美する論文は中々なさそう（CIと非CIの比較にどれだけの意味があるのかは不明として）？ 82個ずつのプロジェクトが対をなしているなら説得力は高いけどもどうだろ
___

- Title: What Factors Make SQL Test Cases Understandable For Testers? A Human Study of Automatic Test Data Generation Techniques (Research)
>  
背景： RDBのテストに関して、テストケースの自動生成は色々研究されている → テスターがSQL関連のテストを理解してテストできているかは不明瞭   
調査： RDBの自動生成されたテストについてのテスターの理解について調査 → 受理もしくは拒否されるINSERT文の生成器を採用 → INSERTのVALUEはテスターの理解に影響を与える（デフォルト値など）、負数とNULLなどの文字列はテスターの予測を妨げる（テストの結果が正しいか混乱する）

Tag_SQL, Tag_Database, Tag_Test, Tag_Test_Case_Gen, Tag_Survey  
Tag_S_Test

ここでのテストケース自動生成はSQL構文が崩れないようにひな形を作っている、ぐらいの感じ？ 記号実行とかではめんどくさい要素やし
___

- Title: Concrete hyperheuristic framework for test case prioritization (Journal)
>  
背景： テストケースの優先順位付け (Test Case Prioritization: TCP) → 最適化のために色々なアルゴリズムが検討 → 新しいテストシナリオに対して、適切なアルゴリズムの決定は困難  
提案手法： hyperheuristic に基づいた一般的に適用可能な search-based TCP を提案 → 様々なアルゴリズムを包含、シナリオを学習し、適切な戦略を動的に選択  
実装：  
実験： 適切にアルゴリズムを選択できている

Tag_Test, Tag_Learning, Tag_Metrix  
Tag_S_Test

テストケースの実行順を決定する戦略を決定する戦略についての論文。
___

- Title: Systematically Testing and Diagnosing Responsiveness for Android Apps (Short)
>  
背景： アプリの応答性はユーザ視点でのパフォーマンス解釈の最たる例 → CPUの使用率以外にも、デバイスやハードウェアの構成が応答性に影響を与える可能性 → 構成に依存するバグの検出メカニズムはない  
提案手法： AppSPIN 応答性のバグを自動診断、構成依存のバグを体系的に調査 → アプリに対して計装を行う  
実装：  
実験： 30の実際のアプリで評価 → 123の応答性のバグを検出 → 87%について15分のテスト時間内に正常に診断

Tag_Hardware, Tag_Debug, Tag_Response, Tag_Implementation  
Tag_S_Test

計装している以上、AppSPINが応答性に影響を与えている可能性が排除できない（そこについて言及があるかどうか）
___

- Title: DeepEvolution: A Search-based testing approach for Deep Neural Networks (Short)
>  
背景： Deep Learning へのテストケースの自動生成が開発されてきている → Rondom Fuzzingや変換（常に有効な多様性を持つテストケースを生成するわけではない）に依存 → 有効性が阻害  
提案手法： DeepEvolution search-based のDLモデルをテストする新手法  
実装：  
実験： ニューロンカバレッジが大幅に増加（いくつかのコーナーケースも発見） → Tensorfuzzよりも優れていた

Tag_Learning, Tag_Test, Tag_Fuzz, Tag_Test_Case_Gen  
Tag_S_Test

最初勘違いしたが、DLを用いたテストではなくて、DLをテストする手法。 今までそういったテストにBlackbox使われているとは知らなんだ（ホント？）
___

## Systems and Configurations (2 Researches, 1 Industry, 2 Shorts)

- Title: An Exploratory Study of Logging Configuration Practice in Java (Research)
>  
背景： ロギングの構成はロギングの機能、パフォーマンス、信頼性に大きな影響 → ロギングの構成に焦点を当てた調査はない  
調査： 様々なサイズとドメインの10のJavaのOSSプロジェクトと10の産業プロジェクトのロギング構成の実践を調査 → ロギング構成の変更履歴（1213のリビジョン）を分類、分析 → 10個の知見 → 知見から検出器を開発、3つの2年以上未解決のIssueへ取り組み → 2件は解決

Tag_Logging, Tag_Survey, Tag_Version  
Tag_S_Configuration

ここでのログ構成はコーディングのことなのかコンポーネントの構成なのか（多分前者）。 ログ方面に舵を切るなら気になるかも
___

- Title: Performance-Influence Model for Highly Configurable Software with Fourier Learning and Lasso Regression (Research)
>  
背景： システム構成とそのパフォーマンスの推定は大事 → 構成の組み合わせが指数関数的 → 全構成でパフォーマンスを測定するのは非現実的  
提案手法： PerLasso フーリエ学習とLasso Regressionに基づいたパフォーマンスモデリング＆予測手法 → 構成サンプルからパフォーマンスを学習（影響モデルを生成）、フーリエ係数を減らすための新しい次元削除アルゴリズムも提案  
実装：  
実験： 4つの合成データセットと6つの実際のデータセットで評価 → 有効（vs 既存のパフォーマンス影響モデル）

Tag_Learning, Tag_Lasso, Tag_Prediction  
Tag_S_Configuration

構成コストの推定、なんだが、これは構成可能な組み合わせの中で最適な組み合わせを抽出するものなのか？ よくわからんぬ
___

- Title: Microservices Migration in Industry: Intentions, Strategies, and Challenges (Industry)
>  
背景： 環境が移ろう中で、レガシーシステムをマイクロサービスアーキテクチャへ移行が発生 → 大規模な移行では影響と課題の慎重な検討が必要 → 業界内の実践経験がまとまっていない  
調査： 10社のソフトウェア専門家に16回のインタビューを実施、様々なドメイン、サイズの14のシステムの移行プロセスを調査 → 移行では保守性とスケーラビリティが重視、コードベースの分割よりも現代風に書き換えが好まれる（適切な分割手法がないことも要因、技術的課題）

Tag_Survey, Tag_Human, Tag_Practice  
Tag_S_Configuration

移行時の経験・知見についての調査
___

- Title: Comparing Constraints Mined From Execution Logs to Understand Software Evolution (Short)
>  
背景： システム開発で、変更の影響を理解するのは大抵困難 → 変更の影響分析について多く提案されている  
提案手法： 変更前と変更後の実行ログから実行時の制約を比較する手法 → マイニングされた制約を定期的なイベントの予想タイミングと順序、データ要素の値として定義 → 違いを提供することで影響分析をサポート  
実装：  
実験： ソフトウェアの進化の理解に貢献できそう

Tag_Diff, Tag_Learning, Tag_Version  
Tag_S_Configuration

ここでの制約はソルバにとかせるような奴ではない。 差分解析としては参考になるかもしれんがShort
___

- Title: Synthesizing Program Execution Time Discrepancies in Julia Used for Scientific Software (Short)
>  
背景： 科学ソフトウェア（データ分析を用いて知見を得るソフトウェア） → 開発にはJuliaという言語が使われることがあるが、実行時間の見積もりができないのでタスクが効率的に完了できない  
調査： StackOverflowの投稿から実行時間の不一致（想定と違う）についての原因の特定を試みる → 263のJulia関連の投稿について定性分析 → 9つのカテゴリに分類、10個の原因を特定（配列内包の表記で不必要なメモリ割り当てが発生した場合など）

Tag_Julia, Tag_Learning, Tag_StackOverflow, Tag_Survey  
Tag_S_Configuration

ここでの実行時間の不一致は数時間とか数日とかの単位でいいのかね？ Juliaという言語は知らんかった
___

## Comprehension and Empirical Studies (3 Researches, 2 Shorts)

- Title: Comprehending Test Code: An Empirical Study (Research)
>  
背景： 開発者のソースコード理解タスクについての調査はある → テストコード理解の方法についてはあまり調査されていない  
調査： Javaテストコードの理解方法について44人について調査 → テストスイートの読み取りに費やされた合計時間、テストスイートの目的の特定の仕方、テストスイートの拡張の仕方について調査 → 1)事前知識があると読み取り時間が短縮、2)Javaの経験値がAssertなどへの消費時間が短縮、1)2)両方を備えているとテストケース作成に好影響、自動テストの経験は自動テストスイートの理解と拡張に影響

Tag_Human, Tag_Survey, Tag_Test, Tag_Test_Suite  
Tag_S_Comprehension, Tag_S_Human

テストについての理解手法（人間視点）の調査論文。そこまで劇的な内容ではないが、イメージ通りの内容を補強してくれている感。
___

- Title: An Empirical Study Assessing Source Code Readability in Comprehension (Research)
>  
背景： ソースコードの読み取りには時間がかかる → 読み取りやすいコードを書くのがベネ → ネストとループについて2つのコードの可読性ルールを評価  
調査： 4つのカテゴリ（ルールに従うか否か、正しいか否か）、32のJavaメソッドをテスト → オンライン上で275名が実施 → ネストが最小限に抑えるとソースコードの読み取り理解の時間短縮、理解力の向上、do-whileは回避してもそこまで効果なし、英語知識が高いほどネストの最小化に影響

Tag_Human, Tag_Code, Tag_Survey, Tag_Language  
Tag_S_Comprehension, Tag_S_Human

多くのプログラムが英語がベースになっているとはいえ、英語知識が記述に影響を与えるという結果は意外。 ネストが深いと読みづらいのは順当だが、ループ回避（どうやるのかは知らんが）してもそこまで影響しないのは意外
___

- Title: Handling duplicates in Dockerfiles families: Learning from experts (Research)
>  
背景： Dockerfileの管理が単一ではなく複数の Dockerfiles (family) になってきている → 重複処理という（古典的な）課題が発生するのかは未調査  
調査： 128のプロジェクトでの管理者を観察、25人に絞って調査 → 重複は頻繁に発生し、それに対してどうするかは意見が分かれる → 一部の管理者がその場のツールを使用 → 最大85%重複を削除する可能

Tag_Human, Tag_Docker, Tag_Survey  
Tag_S_Comprehension, Tag_S_Human

解読に時間がかかったが、Dockerfile間の重複（冗長）があるのか、あった場合どうするのかについての調査。 Dockerもどこかで習いたいなぁ
___

- Title: Share, But Be Aware: Security Smells in Python Gists (Short)
>  
背景： GitHub Gist上にハードコードされたパスワードなど（Security Smells）を乗せてしまうことがある（危ない） → 脆弱性へ繋がる  
調査： 公開済みの Security Smells 関係の研究を用いて、Gist上のにおいを調査 → 静的分析を通じて13の Security Smells を発見、4403/5822 の公開済み Python Gists で発生が確認 → 1817/5822 で機密性の高いインスタンスを含むコードあり

Tag_Github, Tag_Security, Tag_Survey, Tag_Code_Smell  
Tag_S_Comprehension, Tag_S_Human

セキュリティ上の情報を公開してしまう（コーディングや体制も含め）危険性の議論とその調査。 率が尋常じゃないが、母数の5822は絞っているはず。
___

- Title: Can Automated Impact Analysis Techniques Help Predict Decaying Modules? (Short)
>  
背景： Decaying Modules → 将来的ににおいを発する可能性があるモジュール → 潜在的なにおい → においの予測という観点の手法が提案されてきている → 開発者の変更モジュールの情報（開発者のコンテキスト）が予測パフォーマンスの改善に役立つが、その情報の取得にはコストがかかる  
提案手法： 自動影響分析を用いて、開発者のコンテキストの自動推定の方法を模索  
実装：  
実験： 影響分析の精度とDecaying Modulesの予測精度との相関関係を調査

Tag_Code_Smell, Tag_Version, Tag_Automation, Tag_Prediction  
Tag_S_Comprehension, Tag_S_Human

林先生じゃんか。 においを放つかどうかを予測する、という文脈で自動影響解析が使えないか（情報が使えるのは分かっているので）、という趣旨の論文。
___

## Architecture (3 Researches, 1 Industry)

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
