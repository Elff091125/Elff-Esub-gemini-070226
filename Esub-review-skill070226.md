---
name: medical-device-review-generator
description: Generates a comprehensive, 3000-to-4000-word dual-track medical device submission review report in Traditional Chinese. Trigger this skill whenever the user needs a regulatory assessment, gap analysis, or submission strategy for medical devices (especially AI/ML software or ultrasound modifications) targeting both US FDA 510(k) and Taiwan TFDA pathways based on specified guidelines.
---

# Medical Device Submission Review Report Generator

This skill guides the generation of a professional, exhaustive, and technically precise dual-track medical device submission review report in Traditional Chinese ($3000 \sim 4000$ words). It ensures deep alignment with both US FDA 510(k) frameworks and Taiwan TFDA regulations.

## Core Directives
* **Language & Tone:** Professional, formal regulatory tone in Traditional Chinese (Taiwanese regulatory terminology, e.g., 查驗登記, 軟體確效, 實質等同性).
* **Target Length:** Keep the output highly detailed and structurally comprehensive to reach the $3000 \sim 4000$ word threshold. Avoid fluff; expand via deep technical and regulatory explanations.
* **Contextual Integration:** Seamlessly integrate the specific target device data: Philips EPIQ and Affiniti series ultrasound systems modifying/adding the "AI Auto Measure Abdomen" feature.

---

## Required Report Structure & Content Expansion

The generated report MUST strictly follow this 6-chapter structure. Expand each section dynamically using the guidance below:

### 1. 執行摘要 (Executive Summary)
* Summarize the scope of the evaluation: Adding the "AI Auto Measure Abdomen" software modification to existing Philips EPIQ and Affiniti platforms.
* Explain the dual-track strategy (US FDA 510(k) and Taiwan TFDA).
* Define the clinical purpose: automating abdominal and renal organ measurements.
* Highlight the core regulatory pivot points: software validation, risk management (AI misinterpretation), and clinical evaluation.

### 2. 法規路徑分析與分類 (Regulatory Pathway & Classification)
* **2.1 美國 FDA 路徑 (510(k) Pathway)**
  * Detail classification under **21 CFR § 892.1550** (Ultrasonic diagnostic device) and **21 CFR § 892.2050** (Medical image management and processing system). Class II.
  * Justify the **Traditional 510(k)** route as a software modification leveraging a Predicate Device (**K243794**).
  * Elaborate on FDA FDA AI/ML specific mandates: *Predetermined Change Control Plan (PCCP)* and adherence to the *Content of Premarket Submissions for Device Software Functions* guidance.
* **2.2 台灣 TFDA 路徑 (Registration Pathway)**
  * Classify under the 《醫療器材分類分級管理辦法》 as a Class II device.
  * Analyze the execution of the "Simplified Procedure" (簡化程序) leveraging the prior US FDA 510(k) clearance versus the "General Procedure" (一般程序) based on the 《醫療器材查驗登記審查準則》.
  * Address the critical need for **ISO 13485:2016** QMS compliance (Quality System Documentation / QSD) and local 《醫療器材軟體確效指引》 conformity.

### 3. 技術標準與測試要求 (Technical Standards & Testing Requirements)
* **3.1 軟體與 AI 確效 (Software & AI Validation)**
  * Detail lifecycle documentation matching **IEC 62304** (Define and justify Safety Class B or C).
  * Implement *Good Machine Learning Practice (GMLP)* principles: elaborate on training/validation dataset diversity, bias mitigation, and overfitting validation protocols.
* **3.2 機械與生物相容性 (Transducers)**
  * Evaluate the impact on paired hardware transducers (C5-1, C9-2).
  * Detail **ISO 10993-1** requirements (cytotoxicity, sensitization, irritation) for patient-contacting probe surfaces.
  * Detail electrical safety and performance compliance via **IEC 60601-1** and **IEC 60601-2-37**.

### 4. 差距分析 (Gap Analysis)
Construct a comprehensive Markdown table comparing requirements and strategies. Expand upon the following matrix with deep explanatory commentary:

| 項目 | FDA 510(k) 要求 | TFDA 註冊要求 | 差距與對策 |
| :--- | :--- | :--- | :--- |
| **軟體確效** | 強調 AI 演算法之臨床效能與 PCCP | 強調軟體版本控制、繁體中文標籤與本地化指引符合性 | 需編製符合 TFDA 格式之中文說明書，並將 FDA V&V 報告轉譯對齊本地指引。 |
| **風險管理** | 符合 **ISO 14971**，側重演算法異常與網路安全風險 | 符合 **ISO 14971**，審查重點在於本地化使用之風險 | 兩者核心一致；須全面更新風險管理檔案 (RMF) 以涵蓋 AI 自動測量誤判之臨床風險。 |
| **臨床數據** | 著重與前驅器材 (Predicate) 之實質等同性數據比對 | 需提供臨床評估報告 (CER) 或在台臨床試驗評估 | 引用現有 FDA 510(k) 臨床效能數據，補充針對東亞/台灣族群體型適應性之精確度分析。 |

### 5. 三階段法規執行路徑圖 (Three-Phase Regulatory Roadmap)
* **第一階段：準備與測試 (第 1-4 個月)**
  * Actions: Update ISO 14971 risk profile, execute Software V&V including stress testing for AI boundaries.
  * Financials: Estimate USD 50,000 / TWD 1,600,000 (including lab fees).
* **第二階段：提交與審查 (第 5-10 個月)**
  * Actions: Traditional 510(k) submission to FDA; parallel compilation of TFDA registration dossier and Quality System Documentation (QSD) application.
  * Financials: Include FDA standard review fee (~USD 15,000) and TFDA standard review fee (~TWD 100,000).
* **第三階段：上市後監督 (第 11 個月起)**
  * Actions: Establish Post-Market Surveillance (PMS) tracking AI measurement feedback loops and software patches; schedule annual QMS/ISO 13485 audits.

### 6. 結論與建議 (Conclusion & Strategic Recommendations)
* Provide a strategic summary validating the viability of using K243794 for FDA leverage.
* Frame actionable recommendations:
  1. **AI Transparency:** Clear manual statements emphasizing AI as an assistive tool to mitigate legal diagnosis liability.
  2. **Testing Strategy:** "Worst-case" boundary testing using C5-1 and C9-2 probes across varied image qualities.
  3. **Dossier Harmonization:** Alignment with International Medical Device Regulators Forum (IMDRF) TOC structures to streamline parallel tracks.
