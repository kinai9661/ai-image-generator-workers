# 🎨 AI 圖像生成 API (Cloudflare Workers)

基於 Cloudflare Workers AI 的免費圖像生成 API，支援 Flux 和 Stable Diffusion 模型。

## ✨ 功能特點

- 🆓 每天 100,000 次免費 API 呼叫
- ⚡ 快速的文字轉圖像生成
- 🔒 API 金鑰身份驗證
- 🎯 支援多種 AI 模型

## 🚀 部署步驟

### 1. 建立 Cloudflare 帳號
- 前往 [Cloudflare](https://dash.cloudflare.com/sign-up) 註冊

### 2. 安裝 Wrangler CLI
```bash
npm install -g wrangler
```

### 3. 登入 Cloudflare
```bash
wrangler login
```

### 4. 設定 API 金鑰
```bash
wrangler secret put API_KEY
```

### 5. 部署 Worker
```bash
wrangler deploy
```

## 📖 API 使用方式

### cURL 範例
```bash
curl -X POST https://your-worker.workers.dev \
  -H "Authorization: Bearer your-api-key" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "一隻可愛的機器人在做早餐"}' \
  --output image.png
```

### JavaScript 範例
```javascript
const response = await fetch('https://your-worker.workers.dev', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer your-api-key',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({ 
    prompt: '未來城市的雲端景觀',
    model: '@cf/black-forest-labs/flux-1-schnell' // 可選
  }),
});

const blob = await response.blob();
const img = document.createElement('img');
img.src = URL.createObjectURL(blob);
document.body.appendChild(img);
```

### Python 範例
```python
import requests

url = "https://your-worker.workers.dev"
headers = {
    "Authorization": "Bearer your-api-key",
    "Content-Type": "application/json"
}
data = {"prompt": "一座飛行的城堡"}

response = requests.post(url, headers=headers, json=data)
with open("image.png", "wb") as f:
    f.write(response.content)
```

## 🎯 支援的模型

- `@cf/black-forest-labs/flux-1-schnell` (預設)
- `@cf/stabilityai/stable-diffusion-xl-base-1.0`
- `@cf/lykon/dreamshaper-8-lcm`

## 📝 請求參數

| 參數 | 類型 | 必填 | 說明 |
|------|------|------|------|
| prompt | string | 是 | 圖像描述文字 |
| model | string | 否 | AI 模型名稱 |

## 🔒 安全性

- 使用環境變數儲存 API 金鑰
- 支援 CORS
- Bearer Token 身份驗證

## 📊 免費額度

Cloudflare Workers AI 免費方案:
- 每天 100,000 次請求
- 無需信用卡
- 全球邊緣網路加速

## 🛠️ 開發

```bash
# 本地開發
wrangler dev

# 查看日誌
wrangler tail
```

## 💻 使用教學

1. 註冊 Cloudflare 帳號並啟用 Workers AI
2. Clone 此倉庫: `git clone https://github.com/kinai9661/ai-image-generator-workers.git`
3. 安裝依賴: `npm install`
4. 登入 Cloudflare: `wrangler login`
5. 設定 API 金鑰: `wrangler secret put API_KEY`
6. 部署: `wrangler deploy`

## 📦 部署後設定

在 Cloudflare Dashboard 中:
1. 進入 Workers & Pages
2. 選擇你的 Worker
3. 在 Settings > Variables 中確認 AI 綁定已啟用

## 🌐 線上測試

使用 `examples/index.html` 測試你的 API。只需輸入你的 Worker URL 和 API 金鑰即可開始生成圖像！

## 📝 授權

MIT License

## 🤝 貢獻

歡迎提交 Issue 和 Pull Request！

## 🔗 相關連結

- [Cloudflare Workers AI 文檔](https://developers.cloudflare.com/workers-ai/)
- [Flux 模型說明](https://developers.cloudflare.com/workers-ai/models/)
