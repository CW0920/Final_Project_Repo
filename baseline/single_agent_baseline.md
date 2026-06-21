# Single-Agent Baseline Assessment (單一代理人基準評估)

本文件記錄了本專案所建立的 **Single-Agent Baseline (單一代理人基準模型)** 執行輸出結果，並將其與 Multi-Agent Workflow (多代理人工作流程) 進行結構與品質上的對比評估，以作為本自主學習作業之評分證據。

---

## 1. Single-Agent 產生方式與設定

*   **實作邏輯**：使用單一大型語言模型（LLM），在**單次 Prompt（Prompting）**中同時下達影片企劃、腳本撰寫、視覺分鏡、素材規劃與內容審查之所有指令。
*   **核心痛點**：在單次生成中，LLM 必須同時兼顧多種職責（Planner、Script、Visual、Reviewer）[cite: 13, 14, 15, 16]，容易導致細節度不足、時間軸無法精確對齊，且缺乏獨立的客觀審查機制。

---

## 2. Hypothetical Single-Agent Baseline Output (JSON)

以下為單一 Prompt 直接產出的結構化原始 JSON 資料：

```json
{
  "video_plan": {
    "project_title": "NUTN_CSIE_60s_Promo",
    "video_title_suggestion": "國立臺南大學資訊工程學系：啟迪未來",
    "target_audience": ["高中生", "大學新生", "家長"],
    "core_message": "探索知識、激發創新、塑造未來。",
    "video_length_target_seconds": 60,
    "video_length_tolerance_seconds": 5,
    "scene_plan": [
      {
        "scene_id": 1,
        "time_range_suggestion": "0-5",
        "purpose": "開場 Hook",
        "visual_plan_guideline": "快速科技動態畫面",
        "narration_guideline": "「你準備好探索未來看起來是什麼樣子嗎？」",
        "subtitle_guideline": "影片標題"
      },
      {
        "scene_id": 2,
        "time_range_suggestion": "5-15",
        "purpose": "系所介紹",
        "visual_plan_guideline": "校園與系所外觀",
        "narration_guideline": "「國立臺南大學資訊工程學系，你的科技之旅從這裡開始。」",
        "subtitle_guideline": "系所名稱"
      },
      {
        "scene_id": 3,
        "time_range_suggestion": "15-35",
        "purpose": "學習內容",
        "visual_plan_guideline": "程式碼、AI 示意圖、數據流",
        "narration_guideline": "「學習程式、AI、大數據，打造解決未來的能力。」",
        "subtitle_guideline": "關鍵領域"
      },
      {
        "scene_id": 4,
        "time_range_suggestion": "35-50",
        "purpose": "成果與合作",
        "visual_plan_guideline": "學生團隊討論、專題展示示意",
        "narration_guideline": "「透過專題與團隊合作，將想法變成現實。」",
        "subtitle_guideline": "專題、合作"
      },
      {
        "scene_id": 5,
        "time_range_suggestion": "50-58",
        "purpose": "學習氛圍",
        "visual_plan_guideline": "師生互動、校園生活",
        "narration_guideline": "「與優秀的你，共同成長。」",
        "subtitle_guideline": "正面氛圍"
      },
      {
        "scene_id": 6,
        "time_range_suggestion": "58-65",
        "purpose": "結尾 Call-to-Action",
        "visual_plan_guideline": "系所 Logo、校徽、網站資訊",
        "narration_guideline": "「國立臺南大學資訊工程學系，期待你的加入！」",
        "subtitle_guideline": "系所網址、招生資訊"
      }
    ]
  },
  "script_content": {
    "narration_script": "你準備好探索未來看起來是什麼樣子嗎？國立臺南大學資訊工程學系，你的科技之旅從這裡開始。學習程式、AI、大數據，打造解決未來的能力。透過專題與團隊合作，將想法變成現實。與優秀的你，共同成長。國立臺南大學資訊工程學系，期待你的加入！",
    "subtitle_draft": [
      {"scene_id": 1, "start_time_sec": 0.0, "end_time_sec": 5.0, "text": "影片標題"},
      {"scene_id": 2, "start_time_sec": 5.0, "end_time_sec": 15.0, "text": "國立臺南大學資訊工程學系"},
      {"scene_id": 3, "start_time_sec": 15.0, "end_time_sec": 35.0, "text": "程式、AI、大數據、未來"},
      {"scene_id": 4, "start_time_sec": 35.0, "end_time_sec": 50.0, "text": "專題、合作、實現"},
      {"scene_id": 5, "start_time_sec": 50.0, "end_time_sec": 58.0, "text": "共同成長"},
      {"scene_id": 6, "start_time_sec": 58.0, "end_time_sec": 65.0, "text": "國立臺南大學資工系\n期待你！"}
    ],
    "voice_tone_suggestion": "專業、鼓舞人心",
    "compliance_notes": [
      "腳本內容大致符合場景規劃與時長。",
      "內容正面，未明顯虛構。",
      "素材建議待具體化，但原則上假定可找到免費或開放授權。"
    ]
  },
  "visual_plan_asset_suggestions": {
    "visual_style_profile": "科技、簡潔、明亮",
    "shot_list": [
      {"scene_id": 1, "description": "科技動態畫面", "visual_elements": ["數據", "程式碼"]},
      {"scene_id": 2, "description": "校園與系所外觀", "visual_elements": ["建築", "系所招牌"]},
      {"scene_id": 3, "description": "學習場景", "visual_elements": ["程式介面", "AI 示意"]},
      {"scene_id": 4, "description": "學生互動", "visual_elements": ["討論", "專題demo"]},
      {"scene_id": 5, "description": "校園生活", "visual_elements": ["互動", "校園"]},
      {"scene_id": 6, "description": "系所 Logo 與資訊", "visual_elements": ["Logo", "網站"]}
    ],
    "asset_list": [
      {"asset_id": "A001", "type": "graphic", "description": "系所 Logo", "source_suggestion": "搜尋系所官網", "license_required": "Official", "usage_notes": "片頭片尾"},
      {"asset_id": "A002", "type": "video/image", "description": "校園景觀", "source_suggestion": "免費圖庫(Pixabay, Unsplash)", "license_required": "CC0", "usage_notes": "介紹環境"},
      {"asset_id": "A003", "type": "mockup", "description": "科技介面示意", "source_suggestion": "自行設計或線上工具", "license_required": "Self-Made", "usage_notes": "展示學習內容"},
      {"asset_id": "A004", "type": "audio", "description": "背景音樂", "source_suggestion": "YouTube Audio Library", "license_required": "Royalty-Free", "usage_notes": "正面、科技感"},
      {"asset_id": "A005", "type": "graphic", "description": "網站 URL", "source_suggestion": "官方網站", "license_required": "Official", "usage_notes": "結尾"}
    ]
  },
  "preliminary_review_report": {
    "review_summary": "初步審查：內容大致符合要求，但需人工細化。",
    "compliance_checks": {
      "video_length": {"status": "compliant", "notes": "場景建議時間合計約 60 秒"},
      "theme_fit": {"status": "compliant", "notes": "系所形象與核心訊息有涵蓋"},
      "truthfulness": {"status": "compliant", "notes": "無明顯虛構內容"},
      "copyright": {"status": "pending_verification", "notes": "素材來源建議需人工仔細核對授權"},
      "portrait_rights": {"status": "pending_verification", "notes": "建議拍攝學生，需人工確認肖像權"},
      "zero_paid_token_path_viability": {"status": "verified", "notes": "所有元件建議均指向免費或可自行製作的資源"}
    },
    "specific_issues": [
      {
        "agent_source": "SinglePromptLLM",
        "issue_type": "Detail_Level",
        "description": "視覺規劃和素材建議較為籠統，缺乏明確的執行指導。",
        "severity": "Minor",
        "recommendation": "需要人工進一步細化鏡頭描述和素材尋找方向。"
      },
      {
        "agent_source": "SinglePromptLLM",
        "issue_type": "Constraint_Adherence",
        "description": "旁白稿和字幕稿的精確時長匹配度較低，需要人工調整。",
        "severity": "Minor",
        "recommendation": "需人工根據旁白語速細調字幕時間戳。"
      }
    ],
    "potential_risks": [
      "素材授權的最終確認 (人工)",
      "肖像權取得 (人工)",
      "影片剪輯與配音的協調性 (人工)"
    ]
  }
}