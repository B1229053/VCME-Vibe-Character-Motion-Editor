# VCME: Vibe Character Motion Editor
### 自然語言驅動之影片人物動作編輯系統
**國立暨南國際大學資訊工程學系 - 軟硬體專題**

---

## 👥 團隊成員 (Team Members)

* **指導教授：** 陳仁暉 教授
* **專題成員：**
    * 顏羽婕 (學號)
    * 黃靖芳 (學號)
    * 洪碩廷 (學號)
    * 彭暉紘 (學號)
    * 王俊傑 (學號)

---

## 1. 系統簡介 (System Overview)

本系統 **VCME** 旨在實現「自然語言驅動」的影片動作編輯。使用者只需簡單點選影片中的目標人物並輸入文字指令（如「讓他跳舞」），系統即可在不使用昂貴動態捕捉設備的情況下，精準重塑人物動作。

### 1.1 研發目標
* **直覺化操作：** 點選目標人物並輸入指令，即可完成編輯。
* **高保真動作重塑：** 確保編輯後的骨架符合人體物理邏輯，避免肢體斷裂。
* **影片穩定性：** 解決傳統 AI 編輯時常見的畫面扭曲與不自然現象。

### 1.2 技術範圍 (Scope)
本系統整合以下核心模組：
* **目標分離模組：** 使用 **SAM 2** 提取人物 Mask 並維持長效時序追蹤。
* **動作編輯模組：** 結合 **AniMo** 與 **MDM** 模型，將骨架以「樹狀結構」重塑。
* **畫面合成模組：** 透過 **ComfyUI** 與 **ControlNet** 確保人物與背景完美融合。

---

## 2. 系統架構 (System Architecture)

### Layer 1：感知與分離層 (Perception Layer)
* **SAM 2 Segmentation：** 實現精準的人物分割與記憶機制，應對旋轉或遮擋。
* **Pose Estimation：** 提取原始人物 3D 骨架，作為動作編輯的基礎。

### Layer 2：核心推論層 (Inference Layer)
* **AniMo Framework：** 引入「關節感知時空編碼」，讓動作調整符合人體結構。
* **MDM (Diffusion)：** 根據指令生成流暢且高品質的 3D 動作序列。
* **Skeleton Mapping：** 將新生成的動作精準對應至原始影片人物空間。

### Layer 3：渲染合成層 (Rendering Layer)
* **Spatial Control：** 利用 Depth Map 確保人物動作與背景物件（如沙發）無穿模。
* **Temporal Stability：** 透過時序優化算法維持幀與幀之間的穩定度。

---

## 3. 系統特點 (Key Features)

1. **關節感知時空編碼 (Joint-Aware Encoding)**
   * 不同於傳統 1D 向量編輯，本系統將骨架視為「樹狀結構」，強化關節物理聯繫。
2. **物理衝突檢測**
   * 內建幾何判定機制，避免修改後的動作與背景產生穿模或肢體異常旋轉。
3. **高效渲染整合**
   * 整合 ControlNet (Canny/Depth) 提取細節，保留人物服裝與五官輪廓。

---

## 4. 系統限制 (Limitations)

* **短影片優化：** 目前主要支持 3 秒內的影片動作修改，以維持最高品質。
* **環境依賴：** 極端複雜的背景或持續遮擋可能影響 SAM 2 的追蹤精度。

---

### 📖 參考文獻
1. N. Ravi et al., "SAM 2: Segment Anything in Images and Videos," 2024.
2. G. Tevet et al., "Human motion diffusion model," 2022.
3. Wang et al., "AniMo: Species-Aware Model for Text-Driven Animal Motion Generation," CVPR, 2024.
