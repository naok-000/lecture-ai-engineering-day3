# AIエンジニアリング実践講座 第3回課題

## 1. 独自の質問と参照資料の作成

### 参照資料の選定
参照資料として，以下の論文を用いた．

>R. George et al., "Infrastructure Assisted Autonomous Driving: Research, Challenges, and Opportunities," in IEEE Open Journal of Vehicular Technology, vol. 6, pp. 662-716, 2025, doi: 10.1109/OJVT.2025.3542213.
>keywords: {Sensors;Pedestrians;Robot sensing systems;Autonomous vehicles;Roads;Safety;Vehicle-to-infrastructure;Robot kinematics;Accidents;Vehicular ad hoc networks;Cooperative intelligent transportation systems (C-ITS);infrastructure sensing;map fusion;roadside units;V2I;V2X},

[論文のダウンロード元リンク](https://ieeexplore.ieee.org/document/10887285/authors#authors)

以下の理由からこの論文が資料として適していると判断した．
-  この論文は2025年1月21日に投稿されており，google/gemma-2-2b が公開された2024年10月3日[^1]よりも後に公開されたものである．そのため，LLM がこの論文を学習に用いておらず，LLM はこの論文の知識を直接習得していないといえる．
-  この論文は英語で書かれている．そのため，英語の資料を用いて日本語の質問に回答する場合の精度を評価し，言語が複数にわたることによる精度への影響を評価，考察することができる．
-  PDFデータであるためテキストに変換して処理しやすく，また誤字脱字や誤った情報も極めて少ないと考えられるため，回答の精度を評価しやすい．

論文のPDFデータを https://github.com/naok-000/lecture-ai-engineering-day3/blob/main/data/Infrastructure_Assisted_Autonomous_Driving_Research_Challenges_and_Opportunities.pdf に保存した．

### 質問の考案

論文から以下6つの質問を考案した．
1. What is the primary benefit of deploying Fixed Sensor Nodes (FSNs) in Vehicle-to-Infrastructure (V2I) cooperative systems, especially in complex urban scenarios?
2. 固定センサノード（FSN）をVehicle-to-Infrastructure（V2I）協調システムに導入する主な利点は何ですか？特に複雑な都市環境においては？
3. How do cooperative object detection and cooperative tracking complement each other in enhancing safety and reliability in V2I autonomous driving systems, and what specific mechanisms enable this synergy?
4. 協調型物体検出と協調型追跡は、V2I型自動運転システムにおける安全性と信頼性の向上にどのように相互補完的に働きますか？また、この相乗効果を可能にする具体的なメカニズムは何ですか？
5. Who is the author of 'Infrastructure Assisted Autonomous Driving: Research, Challenges, and Opportunities'?
6. 'Infrastructure Assisted Autonomous Driving: Research, Challenges, and Opportunities'の著者は誰ですか？

以下の観点から質問を考案した．
- 言語が異なることによる影響を評価するために，同じ内容の質問を英語，日本語の2つ考案した．
- 質問1と質問2は参考資料の一部分を参照することで答えられるものを考案した．具体的には663ページ後半〜664ページ前半の段落を参照して答えることを想定した．
- 質問3と質問4は参考資料の複数の部分を総合して答えるものを考案した．具体的には685〜688ページの内容を総合的に参照して答えることを想定した．
- 質問5と質問6は参考資料の知識を用いないと正しく回答できないものを考案した．

それぞれ，以下の要素が含まれているものを正しい回答とした．
- 質問1，質問2
  - 高所設置による死角の解消(Elevated viewpoint)
  - 交差点や視界不良箇所を常時監視(Continuous monitoring)
  - 周辺情報をリアルタイムに車両へ共有(Data sharing)
  = 安全性向上と交通流の最適化(Safety and efficiency)
- 質問3，質問4
  - 

[^1]: https://blog.google/intl/ja-jp/company-news/technology/gemma-2-2b/
