# Paper Thoughts

# TSE

## MultiPL-E: A Scalable and Polyglot Approach to Benchmarking Neural Code Generation

F. Cassano et al., "MultiPL-E: A Scalable and Polyglot Approach to Benchmarking Neural Code Generation," in IEEE Transactions on Software Engineering, vol. 49, no. 7, pp. 3675-3691, July 2023.

https://ieeexplore.ieee.org/document/10103177


## Today Was a Good Day: The Daily Life of Software Developers

https://ieeexplore.ieee.org/document/8666786

這篇在講述 typical&atypical workday 與 good&bad workday ，主要是因為之前的論文有討論過以下

1. 影響workday performance的factor
2. coding activity

而且之前研究的人數比較少，也比較不會專注在 Job satisfaction ，而這篇就比較專注於  developer 自身的感受

這篇發現 typical workday與 good workday 有高度相關，而 bad workday 通常都是 collaborating day 與 meeting day

不過這篇問卷會被開發者自身的情緒所影響，因此邊緣人可能普遍不會覺得開心，而且提問方式也會讓開發者在問卷一開始就被 bias

## Enhancing Trustability of Android Applications via User-Centric Flexible Permissions

https://ieeexplore.ieee.org/document/8844813

### context
Android 採用兩種 privacy permission 的認證方式：
1. 舊一點的 android 安裝前預先告知所有的 permission 給使用者，使用者只能全部接受或是不安裝
2. 新的 android 會在 app 使用 permission 時詢問使用者，使用者可以選擇接受或是不接受

不過 android 的 permission 粒度較粗，例如聯絡人的 permission 同時包含讀取與寫入聯絡人，而使用者無法選擇更細粒度的 permission。這是因為詢問太多 permission，用戶反而會疲乏。
考慮到 android 不可能去看每個 app 到底會在甚麼時候使用 permission，以及不可能確定每個 permission 到底會用在甚麼功能上，android 也無法使用更細粒度的 permission 控制方式，例如將 permission 限制在特定 feature，以及控制到底要釋出多少 permission(照片只提供一部分等等)。

因此這篇提供了一個第三方 library 解決方式，主要是提供一個公正的第三方來篩選出所有使用 permission 的 component，並且開發者要手動將 feature 對應到 component，如此一來這個 library 就可以確保更細粒度的 permission 只會用在特定 component，以確保使用者明確知道不同 permission 對應到甚麼功能、確保只使用在該功能、以及提供特定 level 的 permission。而對於開發者來說，由於多付出的 effort 只有將功能對應到 component，相較於每次使用 permission 都要使用特殊 library 來說方便許多。

這篇可以管理的 permission 只有三項，也許可以再新增更多。考慮到有些 component 同時提供了許多不同的 feature，因此在 feature 對應到 component 時如果可以更細粒度的控制會更好。

也許之後開發者需要提供更細節的 permission 相關資訊，或是 android, google 可以提供選用的 library 來達成更細粒度的 permission 調控。

# ICSE

## Keeping Pace with Ever-Increasing Data: Towards Continual Learning of Code Intelligence Models

S. Gao, H. Zhang, C. Gao and C. Wang, "Keeping Pace with Ever-Increasing Data: Towards Continual Learning of Code Intelligence Models," 2023 IEEE/ACM 45th International Conference on Software Engineering (ICSE), Melbourne, Australia, 2023, pp. 30-42.

https://ieeexplore.ieee.org/document/10172346

## GenTree: Using Decision Trees to Learn Interactions for Configurable Software

https://arxiv.org/abs/2102.06872

這篇在研究如何自動找出 configurable program 中的 high interaction，
藉此才可以測試出只有在 high interaction 才會出現的 faults。
這篇研究也可以應用在無法靜態分析的 large system 上。 

先前作品與這篇不同的地方在於：
1. 他們以 high coverage 為目標，這篇以 high interaction 為目標
2. 部分先前的研究會認為 interaction 只有特定形式，這篇研究指出 interaction 可以有眾多不同的形式與長短。

### related

1. iGen: dynamic interaction inference for configurable software
https://dl.acm.org/doi/10.1145/2950290.2950311
2. Using symbolic evaluation to understand behavior in configurable software systems
https://dl.acm.org/doi/10.1145/1806799.1806864
3. iTree: Efficiently Discovering High-Coverage Configurations Using Interaction Trees
https://ieeexplore.ieee.org/document/6227129


## Big Code != Big Vocabulary: Open-Vocabulary Models for Source Code

https://ieeexplore.ieee.org/document/9284032

### context
在開發軟體時，可能會發生以下情況：
1. documentation 十分零散，他們之間的關係以及他們與 code 的關係沒有很明確(開會紀錄、mail、問答集等等的零散文件)，這可以由建立 doc 與 code 的連結解決問題
2. 無法取得 documentation ，因為之前沒有留下 comment 而且寫 comment 很花時間，這可以藉由規範 developer 寫 doc 來解決
3. 讀 documentation 十分耗費時間，大家常常會沒有讀完就直接 misuse，這可以藉由改善 documentation 並且提供 code sample 來解決(而且這篇本來也不是用於推薦 API)
4. agile 本來就不會時常更新 documentation，也不會寫很多 documentation，日後如果需要得知 implementation detail 可能就只能透過口耳相傳或是讀 code
5. 第一次撰寫的 code 本來就不會有 implementation detail 相關 documentation
6. 有 bug 的 code 本來就不會記載 documentation(先不用講，畢竟看起來不在 context 裡?)
7. 一開始開發時是用 agile，但後續 maintain 時是另一組團隊，導致當初只留下少數的 documentation(requirement 文件)，而其他需要用來 maintain 的文件(design 文件，comment)都不存在，而且此時也沒辦法跟一開始的開發團隊聯絡時，就會出現狀況

在第四、五種情況中，我們只能透過讀 code 來了解此程式的邏輯。不過由於 code 的 naturalness 特性，NN 可以藉由大量 code 來找出 code 的規律性，進一步幫助 developer 在寫程式時，幫助他們找到自己的邏輯錯誤，也可以在既有的 code 中找出可能出現 bug 的地方。

agile 的 documentation

### related

1. On the Naturalness of Software
https://ieeexplore.ieee.org/document/6227135

## The Art and Practice of Data Science Pipelines, A Comprehensive Study of Data Science Pipelines In Theory, In-The-Small, and In-The-Large

https://ieeexplore.ieee.org/document/9793883

### context
現在有許多 system 都會包含 DS pipeline，不過與一般軟體開發不同的是，DS pipeline 會有以下特性：
1. Data are ever really independent. 不論是 input data 之間的，或是 output 與 input 之間，我們都很難確定只動到一個 data 會不會造成甚麼影響，有些影響是需要時間才能知道的。
2. DS pipeline 同時包含著 research 與 engineering，在 research 的同時就要考慮到 engineering 的特性，但是我們常常無法預測甚麼時候才會 research 結束，因此常常會為了實驗方便就隨便加入程式，而不是根據 engineering principle。

也是因為上述原因，DS pipeline 很難做到真正的每個 stage 分開，而且常常會在每個 stage 內包含許多 experiment code，導致後續 maintanence 困難。大多數的 DS pipeline 並沒有包含 post-processing stage，因為許多 DS pipeline 只專注於當下的 dataset，並沒有考慮到 deploy 後要如何 evolution，也就是說 Art and Practice 還是有一定的差距，許多 state of art model 要 migrate 到現有的 system 後，會有後續 maintanence 上的困難。DS pipeline 比較難使用現有 CI tool，因為 DS pipeline 並不是 build 後就可以 deploy，可能在 build 途中會 overfitting 或是 underfitting，這些都需要進行 evaluation 後才能決定要不要 deploy，但是 evaluation 並不是單純的 true/false 就可以解決。

#### feedback
這兩個問題是之前就出現的嗎？如果以前就出現的話，之前的人是怎麼解決的？這裡的 context 說起來很像是之前的人都沒有套用到任何 solution，但是實際上已經有不少 paper 說明這些問題了，代表之前一定都有一些 solution。

4W1H 要更清楚，不然只看到 why

### 修改後 context
許多公司為了可以幫助決策過程更加透明與持續改進決策過程，會採用 data-driven desicion-making 的方式，而 data science 便是從龐大的資料中產生見解來幫助 desicion-making。

Data science 需要包含了三個領域的專業人才，分別是軟體開發者、利益關係人、數學家。這三個領域分別負責了 data science 中不同的部分，利益關係人負責 feature selection 與 evaluation，數學家負責模型化，軟體開發者則負責建構出 data science pipeline 來自動化上述流程並整合到 desicion-making 流程內。

透過自動化的 data science pipeline，我們便可以幫助公司更有效率的利用 data-driven 帶來的好處。

不過開發這套 data science pipeline 與傳統軟體開發不同的是，data pipeline 難以維護。

第一個問題，整個 data science pipeline 都是與 data 息息相關，一旦動到任何 data 都可能導致 pipeline 中大部分的程式都需要修改。

第二個問題，開發 data science pipeline 會不斷進行開發評估的迴圈，利益關係人會根據自己的見解，讓軟體開發者修改的現有 pipeline，再由利益關係人進行 evaluation 並產生下階段的見解，而在不斷進行這個過程中，pipeline 程式碼會變得髒亂。

如果我們對於 data science pipeline 有完整的認識，我們便可以彌平上述兩個困難點。

第一，我們可以事先預測 pipeline 中每個部分對於 data 改動時會需要進行多少對應修改，以及會需要多少 effort。

第二，我們可以了解 pipeline 中會需要哪些部分並規劃結構，並且在最開始就根據結構進行開發，如此一來就算不斷修改 pipeline 也不會造成程式碼髒亂。

因此如果我們可以了解 DS pipeline 的結構與模式，就可以幫助我們開發的 DS pipeline 更好維護。

## A Controlled Experiment with Novice Developers on the Impact of Task Description Granularity on Software Quality in Test-Driven Development

https://ieeexplore.ieee.org/document/8727972

## How Developers Choose Names

https://ieeexplore.ieee.org/document/9018121

## Reading Answers on Stack Overflow: Not Enough!

https://ieeexplore.ieee.org/document/8906075

## Detecting Incorrect Build Rules

https://ieeexplore.ieee.org/document/8812082

## A Theory of Value for Value-Based Feature Selection in Software Engineering

https://ieeexplore.ieee.org/document/9088281

## Identifying Key Features from App User Reviews

https://ieeexplore.ieee.org/document/9402119
app 開發者通常不能直接接觸到他們的 app user，通常只能透過其他管道，而其中一個可以獲得最多資訊的管道就是 app store 的 review，也因此開發者要藉由 review 上的反應，來了解最近的那些改動是使用者需要的，而這些使用者在意的 feature 也稱為 key feature。

不過要手動看這些評論是不可能的，因此如果可以自動擷取 feature 可以幫助 developer 在有限的時間與成本內了解 key feature。由於直接採用 NLP 的方式會需要 label dataset，對於每個 app 可能都要有自己的 dataset，並且每有新的 feature 可能都要更新 dataset，因此直接採用 NLP 是不可能的。先前的作法是採用 pattern based approach，不過只能了解符合該 pattern 的 review 才會被截取出來，而本篇採用 part-of-speech 與 BERT 來做分類，並且將分類結果對應到 rating，因此就算是不同 pattern 也可以了解。

## DescribeCtx: Context-Aware Description Synthesis for Sensitive Behaviors in Mobile Apps

https://ieeexplore.ieee.org/document/9793913

### context
app 開發者說明 permission 時，常常只有說 what，而沒有說 where, when, why, how，這是因為開發者不一定會每個使用 permission 的地方都寫原因(可能覺得其他地方說明過，覺得沒必要，不是最高優先度)，因此如果可以自動生成原因的候選人，再讓開發者選擇的話，就可以減少寫原因的 effort，進而增加開發者寫原因的意願。對於沒有在 GUI 上面描述功能時，作者也發現同樣類別的 app 使用 permission 通常是因為相同的原因，因此也可以由其他 app 觀察出的 pattern 來自動生成說明文字的候選人

## Recognizing Developers' Emotions while Programming

https://ieeexplore.ieee.org/document/9284015

### context
開發者在面對不同的 task 時會有不同的情緒，進而造成 productivity 下降，如果我們可以了解每個人的情緒，便可以採用一些措施來緩解他們的情緒，以及防止日後會有類似的情況產生。為了可以即時的了解到每個開發者的情緒，我們可以利用每天的 meeting 來確認他們遇到的困難與確認他們自我描述的情緒，不過自我描述的情緒很主觀，很難用相同的標準進行評斷，因此我們可以用生物檢測器來確認開發者當下的情緒，進而得到客觀的成果。因此這篇提出的解決方式可以使用一個手環監測，並且確認此手環可以真正的反映出情緒，並且不會對開發的過程造成影響，方便直接使用在現實開發的環境。

## Exploring, exposing, and exploiting emails to include human factors in software engineering

https://ieeexplore.ieee.org/document/6032593

### context
藉由研究 SCM repositories 等來源來預測 defects、設計不良的部分，與了解 evolution 的過程的研究非常多，不過這類的研究都是使用 sturctured data 來進行研究。然而人在開發軟體時的活動還有許多非 sturctured data 的形式，例如 mail、commit message 等，這些資料包含了人與人間合作等資料，如果我們可以了解這些資料，就可以知道軟體甚麼 component 是討論最多的，進而預測 component 會出現 defects 的機率等，這是先前採用的 sturctured data 所無法取得的資訊。但是我們無法直接使用非 sturctured data 的形式進行研究，因此本篇論文首先將 mail 連結到 code，並擷取出 mail 中的 entities 與 code，進而可以了解到哪個 component 討論度高，嘗試將非 sturctured data 連結到 sturctured data，加入此資訊後可以使得原本預測 defects 的準確度更高。

### 老師 feedback
The conclusion is correct. But I am not sure whether you understand the “effect” of the
results (contribution). To discuss the context is very important. But to get the real contribution
of the paper is to realize the “ reset context” after the results provided of the papers. If you don’t
understand what I mean here, please remind me in the next group meeting. I will explain it
further.

我們的結論是 reset the context 後得到的，並不是全貌。
因此要去重新閱讀這篇 paper 的 context，再思考一次結論後才有可能得到這篇 paper 完整的 conclusion 與 contribution。

# 12 年計畫

## 2009 design modeling
1. social 10
2. debugging 15
3. productivity 1
4. framework 2
5. measurement and analysis 1
6. design modeling 19
7. testing 7
8. coding healper 4
9. non functional 5
10. code smell 2
12. process 2
13. requirement engineering 1
14. recommendation 1
### call
1. component
2. software process
3. software evolution
4. software reuse 2
5. Architectural design
6. system modeling 2
7. software testing
8. service
9. project management
10. Design and implementation
11. Quality management

## 2010 modeling tool
1. performence modeling 3
2. human resource 8
3. process 18
4. modeling tool 7
5. development helping 11
6. integrate old 3
7. requirement 13
8. design modeling 37
9. debugging 7
10. testing 24
11. social 9
12. code smell 3
13. specification 3
14. risk 3


## 2011 code trace and patch
1. testing 25
2. auto patch and refactor 22
3. design modeling 48
4. social 16
5. document generating 10
6. debugging 6
7. conf 1
8. cost 8
9. integrate old 5
10. human resource 3
11. requirement 10
12. specification 2
13. process 10
14. code smell 6

## 2012 auto code patch, API
1. cost 3
2. debugging 6
3. API 6
4. document generating 1
5. auto patch and refactor 11
6. integrate old 5
7. process 4
8. design modeling 4
9. testing 5
10. social 1
11. specification 2
12. cost 1

### call
1. agile
2. system modeling 2
3. process 4
4. component
5. Configuration management 2
6. Dependability and security 2
7. Distributed software engineering 2
8. Quality management 2
9. requirement 3
10. Design and implementation 3
11. software reuse 2
12. Software evolution 5
13. Service-oriented
14. architecture
15. testing 2
16. tool


## 2013 web agile
1. auto patching and refactorin code 8
2. design modeling 8
3. planning 1
4. testing 8
5. API 1
6. cost 3
7. social 3
8. human resource 1
9. code smell 3
10. process 6

## 2014

### call
1. Design and implementation
2. modeling
3. requirement
4. process
5. evolution

## 2015 crowd
1. social 1
2. validating 2
3. social 7
4. testing 4
5. design modeling 8
6. testing 6
7. auto patching and refactorin code 1
8. dependency 2
9. human resource 2
10. specification 1
11. process 1
12. code smell 2
13. cost 1

## 2016 APP security 論文比較少
1. usage data 5
2. privacy 1
3. testing 4
4. auto patching and refactorin code 3
5. performance 2
6. human resource 7
7. research 1
8. document generate 1
9. integrate old 6
10. debugging 2
11. requirement 4
12. porcess 2
13. API 1

### call
1. agile
2. system modeling 9
3. service oriented 1
4. Component-based
5. Configuration management
6. process 4
7. requirement
8. Design and implementation 3
9. Dependability and security 2
10. Embedded
11. evolution 8
12. requirement 2
13. reuse 1
14. testing 6

## 2017 debugging big data and best pratice industrial
1. debugging 3
2. design modeling 2
3. API document 2
4. requirement 1
5. auto patching and refactorin code 5
6. human resource 2
7. usage data 1
8. process 3
9. social 1
10. security 1
11. performance 1
12. testing 2

### call
沒有主題

## 2018 data driven continuous integration
1. auto patching and refactorin code 5
2. testing 5
3. security 1
4. privacy 1
5. usage data 3
6. deploy 1
7. dubugging 8
8. requirement 1
9. design modeling 4
10. human resource 7
11. API 2
12. process 1

### call
1. agile
2. system modeling
3. Component-based
4. process 2
5. Design and implementation 2
6. evolution 
7. Project management
8. reuse

## 2019 defect prediction code analysis GUI testing
1. auto patching and refactorin code 7
2. cost 1
3. human resource 2
4. social 2
5. security 4
6. testing 4
7. API 2
8. desigh modeling 5
9. usage data 4
11. generate doc 4
12. integration 3
13. specification 1
14. process 1
15. doc generate 2

## 2020 testing fault cause big data debugging
1. CI 3
2. testing 9
3. integration 3
4. design modeling 4
5. human resource 2
6. cost 1
7. auto patching and refactorin code 4
8. requirement 1
9. API 4
10. debugging 4
11. doc generate 1

## 2021 open source, covid
1. human resource 5
2. integration 3
3. specification 1
4. Verifying Determinism 1
5. testing 4
6. auto patching and refactorin code 5
7. debugging 3
8. API big data 2
9. security 3
10. design modeling 1
11. fault handleing 1
12. usage data 5
13. social 4

## 2022

## 2023