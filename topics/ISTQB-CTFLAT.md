# ISTQB-CTFLAT Official Textbook Reading

## 1. Agile Software Development
* 32 pages, 5 questions => 2 days (6/10,11)
* FA-1.1.1 （K1）アジャイルマニフェストに基づくアジャイルソフトウェア開発の基本概念を想起する。
* FA-1.1.2 （K2）チーム全体アプローチの利点を理解する。
* FA-1.1.3 （K2）早期かつ頻繁なフィードバックの利点を理解する。
* FA-1.2.1 （K1）アジャイルソフトウェア開発アプローチを想起する。
* FA-1.2.2 （K3）開発者およびビジネス代表者と協調してテスト可能なユーザストーリーを記述する。
* FA-1.2.3 （K2）アジャイルプロジェクトにおけるプロセス改善のメカニズムとしてふりかえりを使用する方法を理解する。
* FA-1.2.4 （K2）継続的インテグレーションの効用と目的を理解する。
* FA-1.2.5 （K1）イテレーション計画とリリース計画の違いおよびテスト担当者がそれぞれの活動で価値を提供する方法について学習する。

* whole team approach の利点を述べよ
* early and frequent feedback の利点を述べよ
* power of three それぞれにしかできないことは何か？
	- business representatives
	- developers
	- testers
* power of three のある役が別の役に支援できることは何か？
	- business representatives -> developers
	- developers -> business representatives
	- business representatives -> testers
	- testers -> bsuiness representatives
	- developers -> testers
	- testers -> developers
* ユーザーストーリーが望ましい特性の頭文字を合わせると INVEST となる。それぞれの頭文字は何を表すか？
* ユーザーストーリーにおける 3C concept とは何か？
* ユーザーストーリーには要求以外に何が記述されるか？
* 次の活動はリリース計画とイテレーション計画のどちらで行われるか？
	- Breaking down user stories into tasks (particularly testing tasks)
	- Creating acceptance tests for the user stories
	- Defining testable user stories, including acceptance criteria
	- Defining the necessary test levels
	- Determining the testability of the user stories
	- Estimating testing effort for all testing tasks
	- Estimating testing effort associated with the user stories
	- Planning the testing for the release 
	- Participating in the detailed risk analysis of user stories
	- Participating in project and quality risk analyses 
	- Identifying functional and non-functional aspects of the system to be tested
	- Supporting and participating in test automation at multiple levels of testing
* リスクの分析はリリース計画とイテレーション計画のどちらでも行われる。両者の違いは何か？

## 2. Fundamental agile testing principles
* FA-2.1.1 （K2）アジャイルプロジェクトと非アジャイルプロジェクトとの間のテスト活動の違いを説明する。
* FA-2.1.2 （K2）アジャイルプロジェクトでは開発とテストの活動がどのように統合されているのかを説明する。
* FA-2.1.3 （K2）アジャイルプロジェクトでの独立したテストの役割を説明する。
* FA-2.2.1 （K2）アジャイルプロジェクトで、テストの進捗やプロダクト品質を含めて、テストのステータスを伝達するために使用するツールと技法を説明する。
* FA-2.2.2 （K2）複数のイテレーション間でテストが進化するプロセスを説明し、アジャイルプロジェクトで回帰リスクをマネジメントするためにテスト自動化が重要である理由を説明する。
* FA-2.3.1 （K2）アジャイルチームにおけるテスト担当者のスキル（対人、専門領域およびテストに関するスキル）を理解する。
* FA-2.3.2 （K2）アジャイルチームにおけるテスト担当者の役割を理解する。

### 2.1 The differences between testing in traditional...
* 18 pages, 3 questions => 1 day (6/12)

* テスターが開発者やビジネス代表者と協働することはアジャイルでも従来方法でも同じか？
* テスターがフィーチャーの開発完了まで待つことはアジャイルでも従来方法でも同じか？
* チーム全体の現在のステータス（テストのステータスを含む）を一目で詳細に分かるように表現する方法は何か？
* リリースまたはイテレーションに割り当てられている時間に対する、完了すべき残作業の量を表す方法は何か？
* 進捗を妨げる可能性のある、あらゆる問題をチーム全員が認識するための機会は何か？
* 上記3つ以外で、アジャイル開発に欠かせないコミュニケーションを挙げよ

* Q1: B
* Q2: B,D
* Q3: D

### 2.2 Status of testing in Agile projects
* 10 pages, 2 questions => 0.5 day (6/13)

* 以前のイテレーションに作成した回帰テストのテストケースを削除する場合とはいつか？
* 自動受け入れテストをCIで実行するとき、コードのチェックインごとには実行しない。なぜか？
* 重要なシステムの機能と結合箇所をカバーする自動テストの最初のサブセットは、新しいビルドをテスト環境にデプロイした直後に作成する必要がある。このテストを何と呼ぶか？

### 2.3 Role and skills of a tester in an Agile team
* 8 pages, 2 questions => 0.5 day (6/13)

* テストの独立性を維持するための選択肢は、どのようなリスクを軽減するためのものか？

## 3. Agile Testing Methods, Techniques and Tools
* FA-3.1.1 （K1）テスト駆動開発、受け入れテスト駆動開発およびビヘイビア駆動開発の概念を想起する。
* FA-3.1.2 （K1）テストピラミッドの概念を想起する。
* FA-3.1.3 （K2）アジャイルテストの四象限およびそれらのテストレベルとテストタイプとの関係をまとめる。
* FA-3.1.4 （K3）特定のアジャイルプロジェクトに対して、スクラムチームでテスト担当者の役割を実践する。

* FA-3.2.1 （K3）アジャイルプロジェクト内の品質リスクを評価する。
* FA-3.2.2 （K3）イテレーションのコンテンツと品質リスクに基づいてテスト工数を見積もる。

* FA-3.3.1 （K3）テスト活動をサポートするために関連情報を理解する。
* FA-3.3.2 （K2）テスト可能な受け入れ基準を定義する方法をビジネスステークホルダに説明する。
* FA-3.3.3 （K3）特定のユーザストーリーで、受け入れテスト駆動開発のテストケースを記述する。
* FA-3.3.4 （K3）機能および非機能の両方の振る舞いに関して、ブラックボックステスト設計技法を使用して、特定のユーザストーリーに基づくテストケースを記述する。
* FA-3.3.5 （K3）アジャイルプロジェクトのテストをサポートするために、探索的テストを実行する。

* FA-3.4.1 （K1）アジャイルプロジェクトの目的と活動に従って、テスト担当者が使用できるさまざまなツールについて想起する。

### 3.1 Agile testing methods
* 26 pages, 4 questions => 2 days (6/14, 15)

* ATDD
	- ATDDで作成したテストは後の回帰テストに利用できるか？
* BDD
	- なぜBDDだとステークホルダーと議論しやすいのか？
	- なぜBDDは複数のテストレベルに適用できるのか？
* Test Pyramid
	- 関連する7原則は何か？なぜか？
* Agile Testing Quadrants
	- 左右の軸、上下の軸は何を表すか？
	- 第1,2,3,4象限はどこにあり、何を表すか？
	- 静的テストにも適用できる概念か？
* The Role of a Tester
	- ステークホルダーの信頼を得るためにどうするか？信頼を失ったらどうなるか？
	- sprint zero で何をするか？
	- デリバリー済の価値を維持したり、新たな価値のために再定義するためには、`根底にある機能とフィーチャの間のすべての依存関係を識別することが重要`

### 3.2 Assessing quality risks and estimating test effort
* 20 pages, 2 questions => 2 days (6/16, 17)

* Assessing Quality Risks in Agile Projects
	- 品質リスク分析はリリース計画時とイテレーション計画時に行われる。何が異なるか？
	- イテレーション計画時の品質リスク分析プロセスの順番は？ {各品質リスクの評価, テスト技法の選択, アジャイルチームメンバの招集, 品質リスクの識別, テスト範囲の決定, 現イテレーションのバックログアイテムの一覧化}
	- 品質リスクが低いと評価されたバックログアイテムに関連するタスクであるほど、遅くに開始し、より少ないテスト工数を割り当てる。これは真か？なぜか？
* Estimating Testing Effort Based on Content and Risk
	- テスト工数の見積もりにもフィボナッチ数列が推奨される。なぜか？
	- あるユーザーストーリーの見積もりの値が大きいことは一般的に何を意味するか？
	- プランニングポーカーで異なる意見が出ることもある。どのように収束させるか？
	- リスクポーカーでは数値ではない尺度が用いられることがある。それは何か？

### 3.3 Techniaues in Agile projects
* 25 pages, => 2 days (6/18,19)

* Acceptance Criteria, Adequate Coverage, and Other Information for Testing
	- ユーザーストーリー以外に何がテストベースとなりうるか？
	- ユニットテストにおけるdoneの定義として考えられるものを挙げよ
	- 統合テストにおけるdoneの定義として考えられるものを挙げよ
	- システムテストにおけるdoneの定義として考えられるものを挙げよ
	- ユーザーストーリーの作成完了の基準として考えられるものを挙げよ
* Applying Acceptance Test Driven Development
	- ATDD のテストを作成する前に何をするか？
	- ATDD のテストを言い換えられる言葉は何か？
* Functional and Non-Functional Black Box Test Design
	- 開発者がユーザーストーリーと受け入れ基準に基づいてプログラミングするのと同じく、テスト担当者は…
	- 適用できる代表的なテスト技法は？
* Exploratory Testing and Agile Testing
	- チャーターに含まれる情報の種類を挙げよ
	- テスト手順と期待結果はチャーターに含まれるか？
	- テストセッションの種類を挙げよ
	- 探索的テストの過程を示す文書に何を残すべきか？

### 3.4 Tools in Agile projects
* 19 pages => 1 day (6/20)

* 

## 翻訳
* 1.2.5 `リリース計画は、プロダクトのリリースに備えるもので、多くの場合プロジェクトの開始から数カ月後となる。`
	- 数カ月後まで見据えたものである
* 2.2.2 `回帰が取り込まれるリスクが高くなる。`
	- デグレードするリスクが高くなる、という意味である。「回帰するリスクが高くなる」ではどうか。
* 3.3.1 `ユーザストーリーの完了（done）の定義は`
	- 開発完了ではなく作成完了という意味である
* 3.3.2 `正常系のパスのテストが完了したら、`
	- テストを実行したら、ではなく、テストを作成したら、という意味である
* 3.3.4 `テスト担当者は、プロセスについて可能な限り多くを文書化することが重要である。`
	- このプロセスとは **探索的テストの過程** を表す

## 模擬試験 https://istqb.patshala.com/
弱点

* acceptance criteria 3.1
	- definition of done of release
* BDD
* exploratory testing
	- blended with other testing strategies (3.3.4)
* early and frequent feedback
	- highest business value
* regression testing and test levels
	- acceptance testing
	- feature verification testing
	- integration testing
	- unit testing

英語
* collaborate, rely
* represent, indicate, denote
* reduce - eliminate
* selcom

## 模擬試験 参考書

02:35 - 03:32 (57min) 36/40 (90%)

* Q1: B			B
* Q2: C			C
* Q3: B			B
* Q4: D			D
* Q5: D?		D
* Q6: C			C
* Q7: C			C
* Q8: A			A
* Q9: B			D x		ユーザーストーリーが曖昧かどうか。retail, stock code, obsolete
* Q10: B		B
* Q1: D			D
* Q2: B			B
* Q3: B			B
* Q4: A			D x		mandatory <-> highly recommended
* Q5: C			C
* Q6: B			B
* Q7: C			C
* Q8: C?		C
* Q9: C			C
* Q20: B		B
* Q1: D			D
* Q2: B			B
* Q3: A			D x		conduct
* Q4: A,C (E)	A,C
* Q5: C			C
* Q6: B			B
* Q7: C			C
* Q8: B			B
* Q9: C			C
* Q30: D		D
* Q1: A,D		A,D
* Q2: B			B
* Q3: B			B
* Q4: A			A
* Q5: B			B
* Q6: C			C
* Q7: A? (C)	B x
* Q8: C			C
* Q9: A			A
* Q40: A,C		A,C
