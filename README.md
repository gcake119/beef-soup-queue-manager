# 牛肉湯店帶位系統 (Beef Soup Queue Manager)

> 🎓 **學習專案**: 基於優先佇列演算法的餐廳帶位系統，靈感來自觀察人工帶位流程的痛點。

## 🎯 專案緣起

在台南某家牛肉湯店排隊等候時，我觀察到店員需要手動協調兩種不同需求的顧客入座：
- **點火鍋的客人**: 需要有電磁爐的專用座位
- **只吃牛肉湯的客人**: 可以坐任意座位

尖峰時段的人工帶位流程常造成等候延遲與座位使用效率低落。這個專案探索如何用**優先佇列演算法**自動化公平且高效的座位分配邏輯。

## ✨ 功能特色

- **優先權佇列**: 火鍋客人優先取得配備電磁爐的座位
- **容量匹配**: 依據人數與剩餘座位數優化桌子使用率
- **併桌規則**: 每張桌子可設定是否允許不同組客人共桌
- **CLI 介面**: 簡易的命令列工具用於測試核心邏輯

## 🛠️ 技術棧

- **程式語言**: JavaScript (ES6+)
- **執行環境**: Node.js
- **測試框架**: Vitest (TDD 開發流程)
- **程式碼風格**: Airbnb JavaScript Style Guide

## 📚 學習重點

本專案實踐以下核心概念：
- 佇列 (Queue) 資料結構實作
- 優先佇列 (Priority Queue) 演算法
- 測試驅動開發 (TDD) 工作流
- Clean Code 原則 (Uncle Bob)
- 模組化架構設計

## 🚀 快速開始

### 安裝相依套件

```bash
npm install
```

### 執行測試

```bash
# 執行所有測試
npm test

# 執行特定測試檔
npm test -- priorityQueue

# 查看測試覆蓋率
npm run test:coverage
```

### 啟動 CLI 介面

```bash
npm start
```

## 📖 使用範例

```bash
$ npm start

=== 牛肉湯店帶位系統 ===
目前等候: 3 組客人
下一位: #1001 (4人，火鍋)
可用座位: H1(4人), H2(6人，已坐2人)
分配至: H1
```

## 🏗️ 專案結構

```
beef-soup-queue-manager/
├── src/
│   ├── core/                 # 核心邏輯層
│   │   ├── priorityQueue.js  # 優先佇列實作
│   │   ├── seating.js        # 帶位邏輯
│   │   └── tableManager.js   # 桌子狀態管理
│   ├── utils/                # 工具函式
│   └── index.js              # CLI 入口點
├── test/                     # 測試檔案
│   ├── priorityQueue.test.js
│   ├── seating.test.js
│   └── tableManager.test.js
├── README.md
├── CHANGELOG.md
└── package.json
```

## 🧪 測試策略

本專案採用 **TDD (測試驅動開發)** 流程：

1. **紅燈**: 先寫會失敗的測試
2. **綠燈**: 寫最少的程式碼讓測試通過
3. **重構**: 改善程式碼品質但保持測試綠燈

範例測試：

```javascript
describe('優先佇列', () => {
  it('火鍋客人應該排在牛肉湯客人前面', () => {
    const queue = createPriorityQueue();
    queue.enqueue({ type: 'soup', name: 'A' });
    queue.enqueue({ type: 'hotpot', name: 'B' });
    
    expect(queue.dequeue().name).toBe('B');
  });
});
```

## 🔄 開發路線圖

- [x] **Phase 1**: Node.js CLI 版本，核心邏輯實作
- [ ] **Phase 2**: HTML/CSS 網頁介面
- [ ] **Phase 3**: Vue.js 前端 + Express 後端
- [ ] **Phase 4**: 進階功能（等候時間預測、數據分析）

## 💡 設計決策

### 為什麼選擇優先佇列？

- **公平性**: FCFS (先到先服務) 為基礎，但有資源限制時優先處理
- **效率**: 避免火鍋客人等太久卻有空的火鍋座位未被使用
- **擴展性**: 未來可以加入更多優先權條件（例如年長者、大型團體）

### 併桌規則設計

每張桌子有獨立的 `allowMerge` 屬性：
- `false`: 不允許併桌，一組客人獨享
- `true`: 允許多組客人共用，直到座位額滿

## 📝 版本記錄

詳見 [CHANGELOG.md](./CHANGELOG.md)

## 🤝 貢獻

這是個人學習專案，但歡迎任何回饋與建議！

如果你發現 bug 或有改進想法：
1. 開 Issue 描述問題
2. Fork 專案後提交 Pull Request
3. 確保所有測試通過 (`npm test`)

## 📄 授權

MIT License - 詳見 [LICENSE](./LICENSE) 檔案

## 🙏 致謝

- 靈感來源：台南在地牛肉湯店的實際觀察
- 測試框架：[Vitest](https://vitest.dev/)
- 程式碼風格：[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- 學習資源：好想工作室 Web Camp 前端培訓
