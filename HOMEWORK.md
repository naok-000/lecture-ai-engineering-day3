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
[^1]: https://blog.google/intl/ja-jp/company-news/technology/gemma-2-2b/
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
  - 1. 高所設置による死角の解消(Elevated viewpoint)
  - 2. 交差点や視界不良箇所を常時監視(Continuous monitoring)
  - 3. 周辺情報をリアルタイムに車両へ共有(Data sharing)
  - 4. 安全性向上と交通流の最適化(Safety and efficiency)
- 質問3，質問4
  1. 相互補完性
    - 1.1. 物体検出: 多視点からの物体認識
    - 1.2. 追跡: 連続性を保ち、遮蔽時でも追い続ける
  2. 効果
    - 2.1. 遮蔽耐性
    - 2.2. センサ障害への強さ
    - 2.3. 認識精度向上
  3. メカニズム
    - 3.1. 特徴マップの共有
    - 3.2. カルマンフィルター
    - 3.3. ハンガリアンアルゴリズム
- 質問5，質問6
  - ROSHAN GEORGE, JOSEPH CLANCY, TIM BROPHY, GANESH SISTU, WILLIAM O’GRADY, SUNIL CHANDRA, FIACHRA COLLINS, DARRAGH MULLINS, EDWARD JONES, BRIAN DEEGAN, MARTIN GLAVIN

なお，質問の考案にはChatGPT（4o）を利用した．以下のプロンプトとPDFの資料を渡し，生成された回答を改変して質問および回答を作成するうえで参考にした．
```
この論文に関する質問を4つ考えてください．以下の指示に従うこと．
- 1つめ：この論文の1箇所から得られる知識を用いて回答するもの．（英語）
- 2つめ：1つ目を日本語訳したもの．
- 3つ目：この論文の複数箇所から得られる知識を総合して回答するもの．（英語）
- 4つ目：3つ目を日本語訳したもの．
```
```
各質問に対する回答を簡潔に生成して
```
```
各回答に含まれるべき要素について教えて
```

## 2. 実験の実施
Google Colab 上で実験を実施した．T4 GPU（無料版）を用いた．モデルはgoogle/gemini-2-2b-jpn-itを用いた．
- プログラム
  - https://github.com/naok-000/lecture-ai-engineering-day3/blob/main/ai_engineering_03_homework.ipynb
- プログラム（実行結果を含む）
  - https://github.com/naok-000/lecture-ai-engineering-day3/blob/main/ai_engineering_03_homework_output.ipynb

### ベースラインモデル評価
演習と同様，RAGを用いない状態で回答を生成させた．以下に結果と正しい回答の要素が含まれているかを示した．
#### 質問1
```
The primary benefit of deploying Fixed Sensor Nodes (FSNs) in Vehicle-to-Infrastructure (V2I) cooperative systems, especially in complex urban scenarios, is **enhanced situational awareness and improved safety**. 

Here's a breakdown:

**1. Comprehensive Coverage:** FSNs can be strategically placed in urban environments to provide a wide-area view of traffic flow, road conditions, and pedestrian activity. This comprehensive coverage helps to fill gaps in the information provided by individual vehicles, leading to a more complete picture of the environment.

**2. Real-Time Data Collection:** FSNs can continuously collect and transmit data about traffic density, speed, road markings, and other relevant information. This real-time data stream provides valuable insights for both vehicles and infrastructure systems.

**3. Improved Traffic Management:**  This data can be used by traffic management systems to:
    * **Optimize traffic flow:** By identifying congestion points and adjusting traffic signals accordingly.
    * **Predict potential accidents:**  FSNs can detect anomalies in traffic patterns and alert authorities to potential hazards.
    * **Respond to emergencies:**  FSNs can help emergency services locate and respond to incidents more efficiently.

**4. Enhanced Safety for Vehicles:** 
    * **Collision avoidance:**  FSNs can provide vehicles with information about nearby vehicles, pedestrians, and road obstacles, enabling them to make better decisions and avoid collisions.
    * **Adaptive cruise control:**  FSNs can help vehicles maintain safe distances from other vehicles, improving overall safety.
    * **Lane departure warnings:**  FSNs can detect lane markings and alert drivers if they are drifting out of their lane.

**5. Improved Infrastructure Management:** 
    * **Road maintenance:**  FSNs can monitor road conditions and alert authorities to potholes, debris, and other issues.
    * **Smart lighting:**  FSNs can help optimize street lighting based on real-time traffic and pedestrian activity.
    * **Traffic enforcement:**  FSNs can assist in traffic enforcement by identifying speeding vehicles and other violations.



**Challenges and Considerations:**

While FSNs offer significant benefits, it's important to consider the challenges:

* **Deployment and maintenance:**  FSNs require careful planning and deployment to ensure optimal coverage and minimize maintenance costs.
* **Cost:**  FSNs can be expensive to deploy and maintain, requiring a significant investment.
* **Data security:**  FSNs collect sensitive data, requiring robust security measures to protect against cyberattacks and data breaches.
* **Interoperability:**  FSNs need to be able to communicate effectively with vehicles and other infrastructure systems.



Despite these challenges, FSNs play a crucial role in the development of V2I cooperative systems, particularly in complex urban environments.  Their ability to provide comprehensive data and enhance situational awareness makes them a key component in improving road safety and traffic management. 
```
- 1. なし
- 2. 部分的にあり
- 3. あり
- 4. 部分的にあり

#### 質問2
```
## FSNをV2Iシステムに導入する主な利点

**複雑な都市環境において、FSNをV2Iシステムに導入することで、以下のメリットが期待できます。**

**1.  交通安全の向上:**

*   **リアルタイムの交通状況把握:**  FSNは、車と道路のリアルタイムな状況を把握できます。これにより、交通状況の予測と最適な走行ルートの提案が可能になります。
*   **事故の予防:**  FSNによるリアルタイム情報に基づいて、危険な状況を早期に検知し、ドライバーに警告を送信できます。
*   **渋滞の抑制:**  FSNによる交通状況のリアルタイム情報に基づいて、渋滞を予測し、ドライバーに適切なルート変更や走行時間の調整を促すことができます。

**2.  交通効率の向上:**

*   **最適な走行ルートの提案:**  FSNによるリアルタイム情報に基づいて、ドライバーに最適な走行ルートを提案できます。
*   **効率的な交通管理:**  FSNによるリアルタイム情報に基づいて、交通管理システムが効率的に操作できます。

**3.  都市環境の効率的な運用:**

*   **道路の管理効率の向上:**  FSNによるリアルタイム情報に基づいて、道路の管理効率が向上します。
*   **エネルギー効率の向上:**  FSNによるリアルタイム情報に基づいて、ドライバーの走行状況を把握し、エネルギー効率を向上させることができます。

**4.  都市のスマート化:**

*   **データ分析による都市の最適化:**  FSNによるリアルタイム情報に基づいて、都市のデータ分析を行い、より効率的な都市運営を実現できます。
*   **市民の生活の質の向上:**  FSNによるリアルタイム情報に基づいて、市民の生活の質を向上させることができます。
```
- 1. なし
- 2. なし
- 3. なし
- 4. あり

#### 質問3
```
Cooperative object detection and cooperative tracking are crucial elements in enhancing safety and reliability in V2I (Vehicle-to-Infrastructure) autonomous driving systems. They work together to create a robust and reliable system that can anticipate and react to potential hazards. 

Here's how they complement each other and the specific mechanisms that enable this synergy:

**1. Object Detection: The Early Warning System**

* **Purpose:**  Identify objects in the environment, like pedestrians, vehicles, traffic lights, and road signs.
* **Mechanism:**  
    * **Shared Data:**  Cooperative object detection systems share information about detected objects with other vehicles and infrastructure. 
    * **Multi-Sensor Fusion:**  Combining data from multiple sensors (cameras, LiDAR, radar) improves accuracy and reduces false positives.
    * **Contextual Awareness:**  Detecting objects in context (e.g., identifying a pedestrian crossing the road vs. a parked car) provides a more accurate understanding of the environment.

**2. Cooperative Tracking: The Action Plan**

* **Purpose:**  Follow and monitor the movement of detected objects, predicting their future trajectory.
* **Mechanism:**
    * **Shared Tracking Data:**  Vehicles and infrastructure exchange information about the tracked objects, including their predicted trajectory and potential risks.
    * **Predictive Modeling:**  Using machine learning and AI, these systems can predict the future movement of objects, allowing for proactive responses.
    * **Dynamic Route Planning:**  Based on shared tracking data, vehicles can adjust their route and speed to avoid potential collisions.

**Synergy and Benefits**

* **Enhanced Safety:**  By combining object detection and tracking, the system can:
    * **Detect and predict potential hazards:**  Early detection of objects and their predicted trajectory allows for proactive avoidance.
    * **Coordinate responses:**  Vehicles can react to shared information about object movement, minimizing the risk of collisions.
    * **Improve situational awareness:**  A shared understanding of the environment allows for more accurate and timely decision-making.
* **Increased Reliability:**
    * **Reduced false positives:**  Combining multiple sensor data and context-aware analysis minimizes false alarms.
    * **Improved object identification:**  Shared data and multi-sensor fusion enhance the accuracy of object detection.
    * **Enhanced communication:**  Reliable communication channels ensure that information is shared accurately and efficiently.


**Specific Mechanisms Enabling Synergy**

* **Communication Protocols:**  Standardized protocols for exchanging object detection and tracking data between vehicles and infrastructure.
* **Data Fusion and Processing:**  Algorithms that combine data from multiple sensors to improve accuracy and reliability.
* **Machine Learning and AI:**  AI-powered systems that can learn from past data and improve their predictions over time.
* **Cooperative Control Systems:**  Systems that allow vehicles to coordinate their actions based on shared information.
* **Real-Time Processing:**  Fast and efficient processing of data to ensure timely responses.



**Examples of Cooperative Systems**

* **Cooperative Adaptive Cruise Control (CACC):**  Vehicles adjust their speed and distance based on shared information about the surrounding environment.
* **Intersection Management Systems:**  Traffic lights and infrastructure communicate with vehicles to optimize traffic flow and safety.
* **Roadside Infrastructure:**  Sensors and cameras on traffic lights, road signs, and other infrastructure can share information with vehicles.



**Challenges and Future Directions**

* **Data Standardization:**  Developing standardized protocols for exchanging data across different systems.
* **Security and Privacy:**  Ensuring secure and private communication channels for sharing sensitive data.
* **Robustness and Reliability:**  Developing systems that can handle noisy or unreliable data.
* **Ethical Considerations:**  Addressing ethical concerns related to decision-making in complex scenarios.
* **Integration with Human Drivers:**  Developing systems that can seamlessly integrate with human drivers.



By combining object detection and cooperative tracking, V2I autonomous driving systems can create a safer and more reliable environment for all road users. 
```
- 1.1 あり
- 1.2 なし
- 2.1 なし
- 2.2 なし
- 2.3 あり
- 3.1 なし
- 3.2 なし
- 3.3 なし

#### 質問4
```
## 協調型物体検出と協調型追跡のV2I型自動運転システムにおける相互補完性

協調型物体検出と協調型追跡は、V2I型自動運転システムにおける安全性と信頼性の向上に、相互補完的に働きます。 

**相互補完性:**

* **物体検出による追跡の精度向上:**  協調型物体検出は、周囲の環境をリアルタイムで認識し、物体位置と特徴を検出します。この情報に基づいて、協調型追跡システムは、より正確な追跡と予測を行うことができます。
* **追跡による物体検出の信頼性の向上:**  協調型追跡システムは、物体位置と速度をリアルタイムで追跡します。この情報に基づいて、協調型物体検出システムは、より正確な物体検出を行うことができます。
* **より複雑な状況への対応:**  協調型物体検出と追跡は、複雑な状況（例えば、道路状況の変化、障害物など）に対応する際に、より正確な判断と行動を可能にします。

**具体的なメカニズム:**

1. **情報共有と連携:**  
    * **物体検出システム:**  周囲の環境をリアルタイムで認識し、物体位置、特徴、速度などを検出します。
    * **追跡システム:**  物体位置と速度をリアルタイムで追跡します。
    * **V2I通信:**  検出された情報と追跡情報が、V2I通信を通じて、自動運転システムと他の車両に共有されます。
2. **信頼性の向上:**  
    * **相互確認:**  検出された情報と追跡情報が、互いに確認され、信頼性を高めます。
    * **情報修正:**  検出された情報と追跡情報が、互いに修正され、より正確な判断と行動を可能にします。
3. **安全性の向上:**  
    * **予測と回避:**  協調型物体検出と追跡システムは、予測と回避を可能にし、衝突を回避します。
    * **緊急時の対応:**  緊急時の状況下でも、より迅速かつ正確な判断と行動が可能になります。

**例:**

* **道路状況の変化:**  道路状況が変化した場合、協調型物体検出と追跡システムは、変化した状況を認識し、自動運転システムが適切な行動をとるように調整します。
* **障害物:**  障害物に遭遇した場合、協調型物体検出と追跡システムは、障害物位置と速度を認識し、自動運転システムが安全な回避行動をとります。
```
- 1.1 なし
- 1.2 なし
- 2.1 なし
- 2.2 なし
- 2.3 あり
- 3.1 なし
- 3.2 なし
- 3.3 なし

#### 質問5
```
The author of "Infrastructure Assisted Autonomous Driving: Research, Challenges, and Opportunities" is **Dr.  Yuheng Wang**.


Let me know if you'd like to know more about this book or Dr. Wang! 
```
- なし

#### 質問6
```
申し訳ありませんが、私はリアルタイムの情報にアクセスできません。 

「Infrastructure Assisted Autonomous Driving: Research, Challenges, and Opportunities」の著者は、インターネット上の情報から特定できません。
```
- なし

### RAG を組み合わせた回答生成

#### RAGの実装

以下のようにRAGを実装した．演習の 4. Rerankによる情報頻出の向上 を参考にした．
1. PDFからテキストのみを抽出した．
2. テキストを'.'で分割した．
3. 分割したテキストと各質問の類似度を計算させた．
4. 類似度が高い上位5つについて，前後2文ずつを含めて1つの参考資料としてまとめ，LLMに質問との関連性をyes/noで判定させた．
5. yesの参考資料と質問をともにLLMに渡し，回答を生成させた．

なお，LLMに指示するプロンプトは日本語をベースとし，資料や質問はテキストの言語をそのまま用いた．



以下に結果と正しい回答の要素が含まれているかを示した．

#### 質問1
```
FSNs の主要なメリットは、**複雑な都市環境でのV2Iシステムの効率的な動作とコスト削減**です。


**具体的には:**

* **オンボードセンサーと処理能力の削減:**  FSNs を導入することで、車両が複雑な状況を検知する際に、より多くの処理をFSNsに委託できます。これにより、車両の複雑なセンサーと処理能力の必要性を減らし、コストを削減できます。
* **より安全な運転:**  FSNs は、車両と道路の相互連携を可能にすることで、より安全な運転を実現します。
```
- 1. なし
- 2. なし
- 3. なし
- 4. 部分的にあり

#### 質問2
```
## FSNをV2Iシステムに導入する主な利点

**複雑な都市環境においては、FSN導入により、以下の利点が期待できます。**

* **物理的Occlusionの克服:**  V2Iシステムは、車とFSNの協調によって、車に物理的に隠れている人体の検知を可能にします。
* **より高い精度:**  複数のセンサーからの情報を融合することで、より正確な環境モデルを構築できます。
* **コスト削減:**  車に搭載するセンサーや処理能力を削減できるため、コスト削減につながります。
* **安全性向上:**  より正確な環境認識により、危険な状況を早期に検知し、安全な運転を支援できます。
* **効率的な道路管理:**  FSNは道路の状況をリアルタイムで監視し、交通の効率性を向上させることができます。



**具体的には、複雑な都市環境では以下のようなメリットが挙げられます。**

* **密集した道路環境:**  FSNは、車と連携して道路の複雑な状況を把握し、安全な走行を支援できます。
* **視認性の制限:**  複雑な都市環境では、視認性の制限が大きい場合があり、FSNは車と連携して視認性の制限を克服できます。
* **人々の移動状況の把握:**  FSNは、人々の移動状況を把握し、安全な道路管理を支援できます。
```
- 1. 部分的にあり
- 2. なし
- 3. 部分的にあり
- 4. あり

#### 質問3
```
##  Cooperative Object Detection & Tracking: Synergy for Enhanced Safety and Reliability in V2I Autonomous Driving

Cooperative object detection and tracking work together to enhance safety and reliability in V2I autonomous driving systems.  Here's how:

**1. Complementing Each Other:**

* **Object Detection:**  Identifies objects in the environment, providing a comprehensive view of the surroundings. This helps the system understand the presence and location of objects, crucial for safe navigation.
* **Object Tracking:**  Follows the movement of detected objects over time, providing a dynamic understanding of their trajectory and potential hazards. This allows the system to anticipate and react to object changes, improving situational awareness.

**2. Specific Mechanisms for Synergy:**

* **Early Fusion:** Combining object detection results from multiple sensors in real-time. This allows for a more robust and accurate understanding of the environment, especially in heterogeneous sensor systems.
* **Feature Flow Prediction:**  Leveraging feature flow information to track objects across different frames. This helps overcome limitations of individual sensor data, providing a more comprehensive and accurate view of object movement.
* **Shared Coordinate System:**  Establishing a common coordinate system for all sensors, enabling consistent object tracking across different viewpoints. This ensures accurate object identification and tracking regardless of sensor perspectives.
* **Communication and Data Sharing:**  Efficiently exchanging information between vehicles, enabling collaborative object detection and tracking. This allows vehicles to share information about detected objects, improving overall situational awareness and safety.
* **Decision Making:**  Integrating object detection and tracking data into the autonomous driving system's decision-making process. This allows the system to make informed decisions about safe navigation, considering the dynamic environment and potential hazards.


**3. Benefits of Combined Approach:**

* **Improved Accuracy:** Combining data from multiple sensors and tracking information enhances the accuracy of object detection and tracking, reducing false positives and negatives.
* **Enhanced Situational Awareness:**  Provides a comprehensive view of the environment, allowing the system to anticipate and react to potential hazards more effectively.
* **Increased Safety:**  Reduces the risk of collisions and accidents by providing a more accurate and reliable understanding of the surrounding environment.
* **Improved Reliability:**  Reduces the impact of sensor failures and data inconsistencies by leveraging multiple sensors and data sources.



**In Conclusion:**

Cooperative object detection and tracking work together to create a robust and reliable system for autonomous driving.  By combining their strengths, they enhance safety and reliability, enabling vehicles to navigate complex and dynamic environments with greater confidence. 
```
- 1.1 部分的にあり
- 1.2 あり
- 2.1 部分的にあり
- 2.2 あり
- 2.3 あり
- 3.1 部分的にあり
- 3.2 なし
- 3.3 なし

#### 質問4
```
## 協調型物体検出と協調型追跡の相互補完性

協調型物体検出と協調型追跡は、V2I型自動運転システムにおける安全性と信頼性の向上に、相互補完的に働きます。 

**具体的なメカニズムは以下の通りです:**

1. **より正確な物体検出:** 複数のセンサーから得られる情報が、協調型物体検出によってより正確に統合されます。これは、個々のセンサーの視点から得られる情報が、より広範囲な視点から得られる情報を補完することで、より正確な物体検出を実現します。
2. **よりリアルタイムな追跡:**  複数のセンサーからの情報が統合され、より正確な位置情報を得ることが可能になります。これにより、追跡のリアルタイム性が向上し、より迅速な判断と行動が可能になります。
3. **より複雑な状況への対応:**  協調型追跡は、個々のセンサーの視点では見逃されやすい状況を、複数のセンサーからの情報に基づいてより正確に捉えることができます。
4. **より安全な運転:**  より正確な物体検出とリアルタイムな追跡により、自動運転システムはより安全な運転を実現できます。


**具体例:**

* **複雑な道路状況:**  複数のセンサーからの情報が統合され、より正確な物体検出が可能となり、自動運転システムは複雑な道路状況をより正確に認識できます。
* **遮蔽物による誤検出:**  複数のセンサーからの情報が統合され、より正確な物体検出が可能となり、自動運転システムは遮蔽物による誤検出を回避できます。
* **複数車との衝突回避:**  協調型追跡により、複数の車との衝突を回避する判断がより迅速かつ正確に行えます。
```
- 1.1 あり
- 1.2 なし
- 2.1 なし
- 2.2 なし
- 2.3 あり
- 3.1 部分的にあり
- 3.2 なし
- 3.3 なし


#### 質問5
```
The authors of 'Infrastructure Assisted Autonomous Driving: Research, Challenges, and Opportunities' are:

* Roshan George
* Joseph Clancy
* Tim Brophy
* Ganesh Sistu
* William O'Grady
* Sunil Chandra
* Fiacha Collins
* Darragh Mullins
* Edward Jones
* Brian Deegan
* Martin Glavin


 
Let me know if you'd like any further information! 😊 
```
- あり

#### 質問6
```
『Infrastructure Assisted Autonomous Driving: Research, Challenges, and Opportunities』の著者は **George**  です。 
```
- 部分的にあり

## 結果分析と考察

- 全体的に，RAGを使用しないときよりもRAGを使用したときのほうが求める回答の要素が多く含まれていた．
- 
