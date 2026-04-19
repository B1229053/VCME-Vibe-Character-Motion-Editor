# VCME: Vibe Character Motion Editor
### 自然語言驅動之影片人物動作編輯系統
**National Chi Nan University - Dept. of CSIE**

---

## 👥 團隊成員 (Team Members)

* [cite_start]**指導教授：** 陳仁暉 教授 [cite: 3]
* **專題成員：**
    * [cite_start]顏羽婕 (B1229xxx) [cite: 2]
    * [cite_start]黃靖芳 (B1229xxx) [cite: 2]
    * [cite_start]洪碩廷 (B1229xxx) [cite: 2]
    * [cite_start]彭暉紘 (B1229xxx) [cite: 2]
    * [cite_start]王俊傑 (B1229xxx) [cite: 2]

---

## 1. 系統簡介 (System Overview)

[cite_start]本系統 **VCME** 旨在提供一套直覺、低門檻的影片動作編輯平台 [cite: 1, 13][cite_start]。透過自然語言指令與多模態 AI 技術，使用者無需專業動態捕捉設備，即可對影片中特定人物進行精準的動作重塑與編輯 [cite: 7, 9, 13]。

### 1.1 研發目標
* [cite_start]**直覺化操作：** 實現以文字指令驅動的人物動作修改 [cite: 9, 13]。
* [cite_start]**高保真重塑：** 確保編輯後的動作符合人體關節層級與物理邏輯 [cite: 29, 43, 46]。
* [cite_start]**影片穩定性：** 解決 AI 生成影片常見的畫面扭曲與不自然的問題 [cite: 12, 21, 64]。

### 1.2 技術範圍 (Scope)
[cite_start]本系統涵蓋以下核心技術模組 [cite: 17]：
* [cite_start]**目標分離模組：** 利用 **SAM 2** 進行人物 Mask 提取與長效時序追蹤 [cite: 19, 21, 24]。
* [cite_start]**動作重塑模組：** 結合 **AniMo** 與 **MDM**，將骨架視為「樹狀結構」編碼 [cite: 26, 29, 30, 40]。
* [cite_start]**畫面合成模組：** 透過 **ComfyUI** 節點與 **ControlNet** 進行深度感知渲染 [cite: 54, 59, 60]。

---

## 2. 系統架構 (System Architecture)

### Layer 1：感知與分離層 (Perception Layer)
* [cite_start]**SAM 2 Segmentation：** 使用者點選目標，生成精準的人物遮罩與時序記憶 [cite: 20, 22]。
* [cite_start]**Pose Estimation：** 提取原始人物的 3D 骨架資訊作為編輯基準 [cite: 23]。

### Layer 2：核心推論層 (Inference Layer)
* [cite_start]**AniMo Framework：** 提供具備物理層級的關節感知編碼 [cite: 29, 37, 52]。
* [cite_start]**MDM (Diffusion)：** 根據文字 Prompt 生成高質量的動作數據 [cite: 28, 51]。
* [cite_start]**Skeleton Mapping：** 將生成動作映射至原始人物骨架空間 [cite: 30, 49]。

### Layer 3：渲染合成層 (Rendering Layer)
* [cite_start]**Spatial Control：** 利用 Depth Map 確保人物動作與背景物件無穿模 [cite: 57, 62]。
* [cite_start]**Temporal Stability：** 透過時序優化算法，維持幀與幀之間的穩定度 [cite: 64]。

---

## 3. 系統特點 (Key Features)

1. **關節感知時空編碼 (Joint-Aware Encoding)**
   * [cite_start]不同於傳統 1D 向量編輯，我們將骨架視為「樹狀結構」，確保符合人體邏輯（如肩膀帶動手肘） [cite: 29, 40, 43]。
2. **多模態語義對齊**
   * [cite_start]精準對齊文字指令與 3D 動作數據，實現「自然語言驅動」 [cite: 1, 9, 28]。
3. **物理衝突檢測**
   * [cite_start]內建空間幾何判定機制，避免修改後的動作產生穿模或斷裂現象 [cite: 12, 46, 62]。

---

## 4. 系統限制 (Limitations)

* [cite_start]**時長限制：** 目前優化目標為 3 秒內的短影片，以維持生成品質的一致性 [cite: 11]。
* [cite_start]**環境限制：** 極度複雜的背景或短暫遮擋仍需仰賴 SAM 2 的記憶機制穩定度 [cite: 22]。

---

### 📖 參考文獻
1. [cite_start]N. Ravi et al., "SAM 2: Segment Anything in Images and Videos," arXiv preprint arXiv:2408.00714, 2024. [cite: 24]
2. [cite_start]G. Tevet et al., "Human motion diffusion model," arXiv preprint arXiv:2209.14916, 2022. [cite: 51]
3. [cite_start]Wang et al., "AniMo: Species-Aware Model for Text-Driven Animal Motion Generation," CVPR, 2024. [cite: 52]
