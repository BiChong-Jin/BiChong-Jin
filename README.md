## Hi there 👋

<!--
**BiChong-Jin/BiChong-Jin** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
# 開発経験：

## ＜Stg環境におけるクラウドコスト削減＞　[開発背景]Freee インターンシップ　
[利用技術]Terraform, Kubernetes, Datadog [開発環境]Github, ArgoCD, Kubernetes, Datadog [チーム構成]3人(Tech lead, mentor, 自身) [担当領域]Stg環境インフラ基盤　

[工夫したところ]
当時のタスクとして、Stg環境のコスト削減をして欲しいと言われ、それに向けての原因究明、改善、モニタリングを実施した。まずはなぜStg環境がコストが嵩んでいるかに着目し、分析した。Datadogのmetricsを利用し、Stg環境下の各サービスのグラフを問題のないprod環境と比べた。結果、Stgにおいては、podが過剰に立っているサービスがいくつあった。pod数が多くなっているサービスのTop3を対象とした。Freeeではインフラ管理をTerraformで自動化されているため、各サービスのterraform設定をprod環境の設定を比べた。その結果、HPA(水平pod auto scaling)の設定がstgがprodよりもシビアになっていることがわかった。→ minReplicaとmaxReplicaの範囲が狭かった。その結果、Kubernetesがpodに対して正常なscalingができてなく、pod数が過剰になり、AWSのVMの数の増加に繋がった。

改善策としては、stgとprodの設定を一致させた。これにより、stgにけるpodが正常にauto scalingできて、年間では約33%のコスト削減ができると試算した。

## ＜Kubernetesアラート対応自動化ツール＞　[開発背景]Preferred Networks インターンシップ　
[利用技術]Kubernetes, Prometheus, Vertexai Python SDK, Gemini, MCP [開発環境]Github, Slack, Kubernetes [チーム構成]3人(mentor 2人, 自身) [担当領域]社内機械学習インフラ基盤　

[工夫したところ]
背景としては、PFNの機械学習プラットフォームで日々色んなアラートが発生しており、それらに対して、自分が参加したチームのSREが対応を追われる状況である。生産性や新メンバーのために、このプロセスをLLMを利用し、自動化できるようなツールを作るというタスク。タスクの目標はまずアラート解決策の提案、そして最終目標はLLMによって修正してもらうこと。
前提としてモデルと提供プラットフォームが選定されて、GeminiとGCPのvertexaiに限定された。
このような背景のもと、まず二つの案を考えた。１、prometheus apiを利用し、function call形式でLLMを呼び出し、修正案を提案してもらう　２、MCP serverを利用し、MCP clientを実装し、LLMによる一連の操作の完全自動化。
タスクの最終目標と自分自身に挑戦したいという思いで、プラン２を選択した。
まずはVertexai apiの仕様をdocument参照で熟知し、自由に使えるようにした。そして、mcp serverをred hatによって開発されたkubernetes mcp serverを選択した。

最後に、両者をうまく融合し、ユーザがチャット式でプロンプトを入力し、LLMがリアルタイムで提言から修正まで行うツールを実装できた。

[動画]https://drive.google.com/file/d/13go555k9N9hKO5d4nX2athniJ_PaHZ7j/view?usp=drive_link
