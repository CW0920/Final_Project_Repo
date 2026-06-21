# 多代理人影音生成工作流程：國立臺南大學資訊工程學系形象宣傳影片
> **NUTN CSIE 60-second promotional video** (加分主題項目)

本專案為多媒體系統課程之自主學習作業。專案利用 **OpenClaw** 多代理人（Multi-Agent）協作架構，建立了一個受控式、可追蹤且完全符合「零付費 Token」公平性原則的短影片自動化生成與審查工作流程，並最終產出一支高品質的南大資工系形象宣傳短影片。

---

## 1. 專案基本資訊

* **開發團隊**：個人獨立完成（林崇瑋）
* **協作平台**：OpenClaw 多代理人框架
* **多媒體成果規格**：
    * **影片長度**：65 秒（符合 60 秒 ±5 秒之規範）
    * **影片解析度**：1080p
    * **檔案格式**：MP4
* **零付費 Token 完成性正式聲明 (Zero-Paid-Token Declaration)**：
    * 本專案之多代理人規劃、腳本生成、分鏡設計、內容審查以及後續多媒體影音素材獲取、語音合成、影片剪輯，**完全使用免費額度、開源模型或公開/自製授權資源，過程中絕無使用任何付費之商業 LLM API 或付費影音生成服務**，完全符合平台公平性政策。

---

## 2. GitHub Repository 目錄架構導覽

本專案嚴格依據作業規範建構，所有專案成果與評分證據之存放路徑如下：

```text
Final_Project_Repo/
├── README.md                      # 本說明文件（包含組員、免付費聲明與加分項標示）
├── agents/                        # Specialized Agents 角色與 Prompt 設定目錄
│   ├── planner_agent.md           # 企劃代理人設定 (Persona/Prompt 摘要)
│   ├── script_agent.md            # 腳本代理人設定 (負責旁白與字幕生成)
│   ├── visual_agent.md            # 分鏡代理人設定 (負責 Shot List 與 B-roll 規劃)
│   └── reviewer_agent.md          # 審查代理人設定 (負責合規性交叉檢查)
├── handoff/                       # 中間交接資料 (Structured JSON)
│   ├── 01_planner_output.json     # 企劃大綱與受眾目標
│   ├── 02_script_output.json      # 旁白與字幕初稿
│   ├── 03_visual_output.json      # 分鏡描述與素材清單建議
│   └── 04_reviewer_feedback.json  # 獨立審查機制之修正反饋紀錄
├── traces/                        # 執行紀錄目錄
│   └── execution_trace.md         # 完整的系統 Log、對話軌跡與白盒子重現證據
├── baseline/                      # Baseline 比較目錄
│   └── single_agent_baseline.md   # 單一 Prompt 直接產出的 JSON 對照組與深度評估
└── outputs/                       # 最終多媒體成果與授權目錄
    ├── final_video.mp4            # 最終 65 秒 1080p 形象宣傳影片成果
    ├── subtitles.srt              # 影片對應之字幕檔案
    └── asset_sources.md           # 完整素材來源與授權說明（包含 Airvoz 與 Pexels 引用）

3. 多代理人工作流程 (Multi-Agent Workflow) 摘要
專案不依賴單一黑盒子 Prompt 生成，而是透過 OpenClaw 將任務邊界拆分至以下四個專業代理人：

Planner Agent：鎖定高中生、新生與家長，建構 60 秒結構，明定素材合理使用政策。

Script Agent：根據企劃產出正向、熱情的旁白，並計算語速以確保不超出時長限制。

Visual Agent：對照腳本設計高科技感、明亮的分鏡畫面，並給出具體的 B-roll 關鍵字。

Reviewer Agent：站在客觀立場，針對真實性（不虛構系所資訊）、時長（55-65秒）、版權與肖像權進行嚴格過篩。

本流程之中間交接與修正軌跡，皆完整記錄於 handoff/ 與 traces/ 資料夾中，展現了「白盒子（White-box）」系統的可追蹤性與重現性。

4. 合規性與權利聲明 (Compliance & Licensing)
真實性保障：影片內提及之學術領域（人工智慧、大數據、程式開發）與團隊合作特色，均嚴格對照國立臺南大學資訊工程學系官方網站資訊，絕無任何由 AI 虛構或誇大之系所不實內容。

素材與版權說明：

官方識別：影片中出現之南大校徽與資工系徽，均清楚標註來源，且宣告僅用於非商業之教學、學術課程成果發表。

影音素材：全面採用 Pexels Free License 免版權影片，以及 Bensound 創用 CC 規範之免版權音樂。

語音旁白：使用零付費額度工具 Airvoz (Text-to-Speech) 進行語音合成，符合公平性資源路徑。

詳細素材網址與授權條款請參閱：outputs/asset_sources.md。