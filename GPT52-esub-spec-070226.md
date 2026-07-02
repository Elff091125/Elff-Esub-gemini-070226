醫療器材法規智慧工作坊 2.0
Medical Device Regulatory Intelligence Workspace
雙軌 FDA 510(k) / TFDA 骨科外固定系統技術規格說明書與系統升級白皮書
文件版本： Rev 5.0.0 文件性質： Comprehensive Technical Specification 適用部署： Hugging Face Spaces（建議 Docker Space；可搭配 Streamlit 控制殼層）、agents.yaml、skill.md、OpenAI API、Gemini API 預設語言： 繁體中文，支援 English 預設 LLM： gemini-3.1-flash-lite 原則： 保留原有全部功能，修正已知風險，新增 3 個 WOW AI 功能，並補齊可視化、技能文件、筆記/OCR、主題與部署治理能力

1. 文件目標與升級總覽
本版本是對既有「醫療器材法規智慧工作坊」的系統級設計升級。新版本維持原始產品的核心定位：針對骨科外固定系統，建立一個同時服務 美國 FDA 510(k) 與 台灣 TFDA 查驗登記 的智慧合規工作平台，協助法規、研發、品保、臨床與管理團隊在同一個可稽核、可追溯、可協作的介面中完成技術檔案生產、法規比對、風險評估、臨床與非臨床論證、提交前質量檢查與審查防衛準備。
本次升級重點不只是「加功能」，而是將系統提升為一個更安全、更可視、更可管控、更適合 Hugging Face Spaces 部署的產品級平台。所有原始功能保留，包括：
* 		雙軌法規路徑管理（FDA 510(k) / TFDA）
* 		Worst-case 幾何與力學判定
* 		ISO 10993 / ASTM / ISO 14155 / 21 CFR Part 11 支援
* 		電子申報欄位填寫與 AI 抽取
* 		審計追蹤與數位簽章
* 		14 個原有 WOW 子系統
在此基礎上，本版加入以下關鍵強化：
* 		所有 LLM 功能預設模型統一改為 gemini-3.1-flash-lite 同時允許使用者改選其他 Gemini 或 OpenAI 模型，並可編輯 prompt。
* 		新增 3 個 WOW AI 功能 將總 WOW 模組由 14 擴充至 17。
* 		新增 LLM 執行劇場（Execution Theater） 提供可視化執行特效、互動式狀態燈號、串流式 Live Log。
* 		新增互動儀表板與 5 個 WOW 圖表 讓法規進度、文件完整度、AI 信心、風險熱點、跨模組一致性可即時觀察。
* 		新增 skill.md 智能技能工作室 支援貼上、上傳、編修、下載、AI 修改，並可將 skill 套用到文件分析。
* 		新增 Note Intelligence 模組 可匯入 txt / md / pdf，執行 OCR、整理為 Markdown、關鍵字珊瑚色高亮，並附帶 6 個 Note AI Magic 功能。
* 		新增主題系統 支援 Light / Dark 模式與 10 組基於 Pantone 靈感的高質感配色風格。
* 		補強 API Key、OCR、串流、Markdown 安全、檔案治理與部署風險修正

2. 產品願景與設計原則
本系統應被定義為法規智慧工作平台，而不是單純的文件生成器。其設計原則如下：
2.1 合規優先
任何 AI 生成內容都必須可回溯、可審查、可標記信心區間、可由人覆核。系統不得暗示 AI 內容可直接取代最終法規判斷。
2.2 領域專精
工作流需深度貼合骨科外固定系統的實務：骨針、夾具、連桿、疲勞測試、化學表徵、清潔度、臨床非劣性、QMS、UDI 與 PMS。
2.3 模型中立但預設高效率
預設採用 gemini-3.1-flash-lite，以控制延遲與成本；高風險或長篇生成則可手動升級模型。平台本身不得綁死於單一供應商。
2.4 執行透明
每次 LLM 任務都要有清楚的任務階段、模型、prompt 版本、輸入來源、token/成本估計、結果狀態與 fallback 記錄。
2.5 安全與稽核並重
API key、文件內容、審核意見、簽章、變更日誌與匯出資料必須受到嚴格治理，尤其在 Hugging Face Spaces 這類共享執行環境中更需最小暴露。
2.6 體驗高級化
本系統定位為「內部旗艦級專業工作坊」，UI 不應是單調後台，而需具備高識別度、穩定流暢與高資訊密度的專業儀表風格。

3. 系統範圍與主要模組
本版本建議將平台劃分為九大一級模組：
* 		Regulatory Workspace：主工作區，管理產品、案件、文檔與分析任務
* 		Dual-Pathway Compliance Engine：FDA/TFDA 雙軌比對、差額與提交邏輯
* 		WOW AI Orchestration Hub：17 個 WOW 子系統總控台
* 		Execution Theater：LLM 串流執行可視化、互動指標、Live Log
* 		Interactive Dashboard：全域狀態看板與 5 大圖表
* 		Skill Studio (skill.md)：技能文件編修、AI 協作、文檔套用
* 		Note Intelligence：筆記/文件整理、OCR、Markdown 轉換、AI Magic
* 		e-Submission Form Center：智能填表、核簽、匯出
* 		Audit, Security & Deployment Console：審計、金鑰、設定、部署狀態

4. 多模型 AI 架構與模型治理
4.1 預設模型策略
所有 LLM 功能預設使用：
* 		gemini-3.1-flash-lite：預設模型，適用於大多數生成、抽取、改寫、比較、摘要、OCR、skill 修改、note 整理與 dashboard insights。
使用者可手動切換其他模型，包括：
* 		Gemini 系列其他模型
* 		OpenAI 系列模型
* 		未來擴充之企業內部模型或代理模型
4.2 使用者模型控制能力
每個 AI 任務面板都應允許：
* 		選擇模型供應商
* 		選擇具體模型
* 		調整溫度、最大輸出長度、是否啟用串流
* 		編輯 system prompt / task prompt
* 		儲存 prompt 範本
* 		查看上次執行使用的模型與 prompt 版本
4.3 模型路由建議
* 		低延遲日常任務：gemini-3.1-flash-lite
* 		長文技術說明草擬：Gemini 中階或 OpenAI 中階模型
* 		最終審查草案、矛盾檢測、跨文件綜述：高階模型
* 		OCR with semantics：預設 gemini-3.1-flash-lite，必要時允許升級
* 		高成本任務：需有成本提醒與確認機制
4.4 AI 執行安全邊界
系統必須將 AI 輸出標註為以下層級之一：
* 		Draft
* 		Expert Review Required
* 		Ready for Internal Review
* 		Submission-Prep Only
* 		Non-Binding Analysis
並提供以下防護：
* 		prompt injection 偵測
* 		機密欄位遮罩
* 		結果內部一致性檢查
* 		引用缺失警示
* 		醫療宣稱風險警示
* 		高風險語句自動上色標註

5. 保留原功能並升級的 WOW AI 能力
原有 14 個 WOW 模組全部保留，並建議在資訊架構上以卡片群組、檢索、收藏與結果版本化方式重構。以下為完整 17 模組列表：
原有 14 個保留模組
* 		WOW 1：QMS 雙向追溯
* 		WOW 2：宣稱淨化門
* 		WOW 3：雙語臨床計畫書
* 		WOW 4：SaMD / SBOM 資安掃描
* 		WOW 5：差額查驗橋接器
* 		WOW 6：最劣幾何應力判定儀
* 		WOW 7：FDA 抗辯挑戰沙盒
* 		WOW 8：eSTAR 結構檢校器
* 		WOW 9：生物相容與清潔度審計
* 		WOW 10：性能豁免論證
* 		WOW 11：審查防衛副駕駛
* 		WOW 12：UDI / GUDID 智慧編碼器
* 		WOW 13：CER 文獻智慧合成儀
* 		WOW 14：PMS / PMCF 風險同步器
新增 3 個 WOW AI 模組
WOW 15：Regulatory Delta Sentinel 法規變更雷達
此模組負責追蹤法規、標準與指南版本差異，並分析對現有專案的影響。它的目標不是自動抓網頁，而是讓使用者匯入新版指南或貼上更新內容後，系統自動產生：
* 		舊版 vs 新版條文差異摘要
* 		受影響模組清單
* 		需更新的 skill.md
* 		需調整的 agents.yaml
* 		對既有 510(k) / TFDA 文件的影響矩陣
* 		優先整改建議
這個模組能將法規更新從「被動發現」變成「主動風險管理」。
WOW 16：Cross-Document Contradiction Hunter 跨文件矛盾獵手
此模組專門偵測同一案件不同文件之間的不一致，例如：
* 		IFU 寫 3.5 mm pin，但測試報告用 4.0 mm
* 		CER 宣稱適應症與 TFDA 申請表不一致
* 		風險檔案殘留限值與生物相容報告不一致
* 		行銷宣稱超出 510(k) 預期用途
輸出應包含：
* 		矛盾項目
* 		涉及文檔
* 		風險級別
* 		建議修正順序
* 		自動生成的統一語句草案
這是提交前最有價值的品質閘門之一。
WOW 17：Evidence Confidence Lens 證據信心透鏡
此模組為每份 AI 結果打上「可信度結構化標籤」，結合規則檢查、來源分類、模型自評與跨模型共識結果，呈現：
* 		Evidence Type：法規文本 / 使用者文件 / 推理草案 / 推測
* 		Confidence Score：0–100
* 		Citation Coverage
* 		Contradiction Risk
* 		Human Review Priority
* 		Export Readiness
此模組的核心價值，是讓管理者一眼看出哪些結果可以用、哪些只能當草稿。

6. LLM 執行劇場與 WOW 視覺化設計
為達成「wow visualization effect for llm execution」的需求，系統應提供一個專屬的 Execution Theater。
6.1 視覺設計目標
讓 AI 執行不再是單調 spinner，而是可感知、可追蹤、可診斷的過程。
6.2 執行劇場的主要元素
* 		任務流光軌跡：以粒子流或脈衝線段呈現從「文件載入 → prompt 組裝 → 模型執行 → 結果整理 → 信心評分 → 寫入模組」的流程
* 		階段指示燈：Queued / Parsing / Reasoning / Comparing / Drafting / Finalizing / Fallback
* 		即時串流視窗：顯示 token 串流、摘要進度、警示訊息
* 		互動式計量指標：延遲、成本估計、來源數、字數、矛盾數、信心值
* 		錯誤旁路顯示：若進入 fallback 或 OCR 失敗，清楚顯示原因與替代結果
6.3 Live Log 設計
Live Log 應支援：
* 		使用者操作日誌
* 		AI 任務日誌
* 		OCR 任務日誌
* 		模型切換日誌
* 		API / fallback 狀態
* 		匯出與簽章事件
日誌需支援：
* 		等級過濾（Info / Warning / Error / Audit）
* 		匯出
* 		搜尋
* 		固定追蹤某任務 ID
* 		避免洩漏 API key 與敏感原文

7. 互動儀表板與 5 個 WOW 圖表
首頁應提供高層級決策看板，幫助主管快速了解目前案件健康度。
7.1 核心 KPI 卡片
* 		專案完整度
* 		高風險缺口數
* 		待覆核 AI 結果數
* 		已簽章文檔數
* 		提交就緒度分數
7.2 五大 WOW 圖表
Graph 1：Dual-Pathway Readiness Radar
顯示 FDA / TFDA 兩軌在技術、行政、臨床、QMS、標示、風險與生物相容性的完整度雷達圖。
Graph 2：Regulatory Gap Heatmap
以熱圖顯示各章節的缺口密度、缺失程度、風險權重與截止優先度。
Graph 3：AI Evidence Confidence Trend
呈現各文件或模組的 AI 信心分布、引用覆蓋率與人工覆核負荷趨勢。
Graph 4：Execution Performance Timeline
追蹤模型執行延遲、成功率、fallback 次數、OCR 成功率與高峰時段。
Graph 5：Cross-Document Consistency Network
用節點圖或關聯圖呈現產品規格、風險檔、CER、IFU、申請表、PMS 計畫間的一致性與衝突連結。

8. 主題、語言與設計系統
8.1 語言策略
* 		首次進入預設為繁體中文
* 		提供一鍵切換 English
* 		記憶使用者偏好
* 		所有 UI、系統訊息、審計標籤與 WOW 模組名稱皆支援雙語
8.2 明暗模式
* 		Light Mode
* 		Dark Mode
* 		跟隨系統
* 		高對比模式（建議新增，利於審核與投影）
8.3 十組 Pantone 靈感風格
建議提供 10 組可切換工作坊樣式，例如：
* 		Clinical Coral
* 		Titanium Blue
* 		Compliance Sage
* 		Audit Graphite
* 		Orchid Steel
* 		Glacier Mint
* 		Regulatory Sand
* 		Midnight Indigo
* 		Precision Copper
* 		Executive Pearl
這些風格不只改色，還應帶動：
* 		卡片邊界
* 		狀態燈樣式
* 		圖表主色
* 		Markdown 高亮配色
* 		按鈕層級與 hover 表現
8.4 Coral 高亮規格
關鍵字與法規標準沿用珊瑚色高亮邏輯，但需加強：
* 		在 light/dark 下均具足夠對比
* 		列印模式可轉為底線或框線，避免輸出失真
* 		不依賴顏色作唯一信息載體，需有 icon 或 tooltip

9. Skill Studio：skill.md 智能技能文件模組
此模組是本版升級的重要差異化能力，應作為獨立工作區存在。
9.1 功能範圍
使用者可：
* 		貼上 skill.md
* 		上傳 skill.md
* 		直接編輯內容
* 		下載修改後版本
* 		使用 AI 根據 prompt 修改 skill
* 		套用 skill 到指定文件
* 		以 Markdown 方式編修結果
9.2 AI 修改流程
預設模型為 gemini-3.1-flash-lite，但可切換其他模型。流程如下：
* 		匯入 skill.md
* 		選擇修改目標：風格、法規重點、輸出格式、語氣、章節模板
* 		輸入要求
* 		生成 diff preview
* 		人工核准後覆寫
* 		保存版本歷史
9.3 套用到文件
使用者可貼上 document，要求 agent：
* 		依照 skill.md 的規則分析文件
* 		生成結構化 Markdown
* 		標記缺口、建議與修改痕跡
* 		允許使用者直接在結果中修訂
9.4 治理與版本
skill.md 必須有：
* 		版本號
* 		生效時間
* 		作者
* 		變更摘要
* 		關聯案件
* 		可回滾版本

10. Note Intelligence：筆記整理、OCR 與 AI Magic
此模組面向法規蒐證、會議紀錄、研究摘要、掃描 PDF 與手動便條的整理工作。
10.1 輸入支援
* 		直接貼上文字
* 		上傳 .txt
* 		上傳 .md
* 		上傳 .pdf
10.2 PDF OCR 路徑
若上傳 PDF，使用者可選擇：
Python OCR 套件路徑
建議提供 3 選：
* 		Tesseract OCR
* 		PaddleOCR
* 		EasyOCR
需明示：
* 		支援繁體中文 / English
* 		各自優勢、速度、準確率與資源消耗
LLM OCR 路徑
* 		預設：gemini-3.1-flash-lite
* 		適合版面理解、表格與混合語義修復
* 		需標示成本較高、速度較慢
10.3 輸出目標
將原始筆記轉成：
* 		結構化 Markdown
* 		自動章節
* 		重點摘要
* 		待辦清單
* 		術語表
* 		風險/疑點清單
並將關鍵字以珊瑚色顯示。
10.4 六個 Note AI Magic
* 		Magic Keywords：輸入關鍵字並自訂顏色高亮
* 		Auto Outline：自動整理成章節與層級標題
* 		Action Miner：抽取待辦與責任人
* 		Regulatory Tagger：標記 FDA / TFDA / ISO / ASTM 關聯片段
* 		Glossary Builder：建立中英對照術語表
* 		Insight Merge：將零散會議筆記合併為正式 Markdown 紀錄

11. 電子申報、審計追蹤與簽章治理
既有的 e-Submission Form Center 與 21 CFR Part 11 設計必須保留，但需要更可操作化。
11.1 表單中心升級
* 		支援欄位模板
* 		支援差額比對視圖
* 		支援 AI 抽取填表
* 		支援欄位鎖定與責任指派
* 		支援匯出 JSON / CSV / Markdown / 可列印 PDF 樣式
11.2 電子簽章
* 		簽章前顯示變更摘要
* 		簽章後鎖定內容
* 		任一關鍵欄位變更自動使簽章失效
* 		保留原簽章歷史，不得覆蓋
11.3 審計軌跡
系統應記錄：
* 		誰在何時修改何內容
* 		使用了哪個模型與 prompt 版本
* 		是否有 fallback
* 		是否有 OCR
* 		是否匯出或下載
* 		是否觸發風險警示

12. API Key、隱私與 Hugging Face Spaces 部署要求
12.1 API Key 管理
* 		若環境變數已提供 API key，UI 不得顯示金鑰內容
* 		若環境變數缺失，允許使用者於前端安全輸入
* 		使用者輸入金鑰預設僅保留於當前 session
* 		明確提供「清除金鑰」動作
* 		日誌、錯誤訊息、匯出內容不得回顯 key
12.2 HF Spaces 部署建議
建議採 Docker Space 部署，以便：
* 		支援完整依賴
* 		支援 OCR 套件
* 		支援多模型代理
* 		支援檔案上傳與非同步處理
若需 Streamlit 呈現，建議作為：
* 		輕量入口頁
* 		管理控制面板
* 		嵌入主工作區或啟動後端任務
12.3 檔案與資料治理
* 		暫存檔自動清理
* 		大檔限制與分頁解析
* 		文件上傳前顯示大小與頁數
* 		可選擇不保存原檔，只保存結構化結果
* 		病患資訊或個資應支援人工遮罩與自動敏感詞提醒

13. 已知風險、潛在 Bug 與修正規格
本節是本版最重要的工程品質強化之一。
13.1 模型串流卡死
風險： 串流中斷導致 UI 永久 loading。 修正： 建立 task timeout、重試策略、終止按鈕與 fallback 結果回填。
13.2 Markdown / HTML 注入
風險： LLM 生成內容含惡意 HTML 或 script。 修正： Markdown 渲染前需白名單化、清洗危險標籤、限制 iframe/script。
13.3 OCR 語言混亂
風險： 中英混排 PDF 被誤切段。 修正： OCR 前語言選項明確；結果提供行塊預覽與人工校訂層。
13.4 大型 PDF 記憶體壓力
風險： HF Spaces 容器記憶體不足。 修正： 採分頁處理、逐頁 OCR、延遲載入、預覽抽樣機制。
13.5 API Key 外洩
風險： 錯誤訊息或 debug log 印出密鑰。 修正： 全域遮罩、敏感欄位 redaction、禁止在前端持久化 local storage。
13.6 跨文件一致性誤判
風險： 同義詞造成 false positive。 修正： 引入術語正規化字典、同義映射與人工確認流程。
13.7 繁中顯示與字型錯位
風險： OCR 或 Markdown 在不同主題下行高失衡。 修正： 指定中英混排字體策略、固定標題層級與表格換行規則。
13.8 圖表與資料不同步
風險： 任務完成後 dashboard 未即時刷新。 修正： 統一事件總線與狀態刷新規格，所有任務結束需廣播更新事件。
13.9 prompt 版本失控
風險： 無法重現同一結果。 修正： 對每次任務保存 prompt 版本哈希與模型版本資訊。
13.10 簽章後被部分編輯
風險： 局部欄位仍可改動。 修正： 簽章狀態需驅動完整 UI 鎖定，並在伺服器端再次檢查。
13.11 OCR 與 LLM 成本失控
風險： 使用者誤選高成本路徑。 修正： 執行前顯示成本級別、頁數估算與模型建議。
13.12 多使用者 session 混淆
風險： 共享容器場景下任務串線。 修正： 所有任務、上傳、日誌、key、暫存資料必須綁定 session ID。
13.13 Fallback 品質過低
風險： API 失敗時回傳空泛文本。 修正： fallback 必須按模組提供專用模板，尤其對 worst-case、QMS、CER、申報表與 OCR 整理需維持基本結構品質。

14. 驗證、品質門檻與交付標準
本系統應以「可用」、「可信」、「可稽核」作為驗收核心。
14.1 功能驗收
* 		17 個 WOW 模組皆可獨立執行
* 		gemini-3.1-flash-lite 為所有 LLM 功能預設模型
* 		模型切換可用
* 		prompt 編輯可用
* 		skill.md 上傳、編輯、下載、AI 修改、套用文件皆可用
* 		note 模組支援 txt/md/pdf 與 OCR 路徑選擇
* 		dashboard 5 圖可正常刷新
* 		live log 可追蹤任務
* 		主題與語言切換可持久保存
14.2 安全驗收
* 		API key 不可在 UI 或 log 明文暴露
* 		Markdown 輸出經過清洗
* 		簽章狀態正確鎖定
* 		任務與檔案不跨 session 泄露
14.3 品質驗收
* 		OCR 失敗時有替代流程
* 		AI 任務失敗時有可讀 fallback
* 		長文任務不因單一模型錯誤而整頁崩潰
* 		圖表與主工作區數據一致
14.4 合規驗收
* 		21 CFR Part 11 的審計軌跡、簽章失效、時間戳與版本留存必須完整
* 		法規關鍵術語高亮、標註與引用邏輯應一致
* 		所有 AI 結果都需保留人工覆核入口

15. 結論
Rev 5.0 的目標不是單純把既有工具做得更華麗，而是將它升級為真正可被內部合規團隊長期使用的法規智能平台。此版本保留原始系統對骨科外固定系統的深度法規與工程知識，延續 FDA 510(k) / TFDA 雙軌申報核心能力，並透過以下升級建立明顯產品差異：
* 		預設 LLM 統一為 gemini-3.1-flash-lite
* 		使用者可自由選擇 Gemini / OpenAI 模型與 prompt
* 		擴充到 17 個 WOW AI 模組
* 		增加執行劇場、Live Log、5 大圖表儀表板
* 		加入 skill.md 技能文件協作中樞
* 		加入 Note Intelligence 與 OCR/Markdown 工作流
* 		強化主題、語言與高級感設計系統
* 		大幅改善部署、安全、串流、資料治理與錯誤恢復能力
若按本規格實施，本應用將不只是「AI 幫忙寫文件」，而會成為一個兼具法規智慧、文件工程、知識治理、審計追蹤與管理可視化的高階醫療器材合規工作坊。

20 個後續深度追蹤問題
* 		是否需要為 FDA、TFDA、EU MDR 建立三套可切換的 skill.md 主模板，而不是單一技能檔？
* 		是否應把 agents.yaml 細分為「模型路由、任務權限、主題配置、匯出規則」四個子配置層，以降低維護風險？
* 		對於 Worst-case 力學判定，是否需要納入更多外固定幾何型態，例如環形、半環形與混合構型？
* 		對於 Cross-Document Contradiction Hunter，是否要支援「術語標準化字典」由企業自行維護，以減少誤判？
* 		是否要在 Evidence Confidence Lens 中加入「人工覆核通過率」作為長期校準 AI 信心分數的依據？
* 		Note Intelligence 是否需要支援掃描圖片、手機拍照檔與批次 PDF，而不只限 txt/md/pdf？
* 		OCR 的 Python 路徑是否需要增加自動建議器，根據文件語言、清晰度與版面自動推薦 Tesseract、PaddleOCR 或 EasyOCR？
* 		是否應在 dashboard 中加入提交倒數與關鍵里程碑提醒，讓主管能掌握時程風險？
* 		Skill Studio 是否需要提供「diff 對照模式」，讓使用者清楚看到 AI 對 skill.md 的逐段修改痕跡？
* 		是否應建立一套 skill.md 驗證器，自動檢查技能檔是否有衝突規則、空章節或不一致輸出要求？
* 		是否要讓使用者針對每個 WOW 模組保存專屬 prompt preset，以符合不同公司內部 SOP？
* 		對於 API key 管理，是否需要引入企業版祕密管理器整合，而不是只依賴環境變數與 session 輸入？
* 		在 Hugging Face Spaces 的資源限制下，是否需要為 OCR 與長文分析建立任務佇列與優先級排程？
* 		是否應提供「低資源模式」，在容器性能不足時自動關閉動畫特效，優先確保文檔與模型任務穩定？
* 		對於 21 CFR Part 11 簽章，是否需要未來整合企業 SSO、MFA 或外部憑證機制以強化不可否認性？
* 		是否應為每份輸出報告附帶「生成來源摘要頁」，列出模型、prompt、skill 版本、輸入文件與信心指標？
* 		WOW 15 法規變更雷達是否需要支援影響評估工作流，例如自動建立待辦、指派人員與期限？
* 		是否要在 WOW 16 矛盾獵手中加入「修正後再檢查」迴圈，讓使用者快速驗證矛盾是否已完全消除？
* 		Note Intelligence 的 Magic Keywords 是否需要支援跨文件一致的高亮規則，讓同一專案的所有術語顏色固定？
* 		是否應規劃下一版加入 RAG 知識庫層，讓企業內部歷史 510(k)、TFDA 案件、CAPA、NCR 與 PMS 資料可作為受控檢索來源？
