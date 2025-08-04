# Claude to X

Claude API 兼容层，支持将 Claude API 请求转换为其他厂商 API 格式。目前支持 Gemini, OpenAI

## 特性

- 🚀 一键部署到 Cloudflare Workers
- 🔄 兼容 Claude Code。配合 [One-Balance](https://github.com/glidea/one-balance) 低成本，0 费用使用 Claude Code
- 📡 支持流式和非流式响应
- 🛠️ 支持工具调用
- 🎯 零配置，开箱即用

## 快速部署

```bash
git clone https://github.com/glidea/claude-to-x
cd claude-to-x
npm install
wrangler login # 如果尚未安装：npm i -g wrangler@latest
npm run deploycf
```

## 使用方法

部署完成后，使用你的 Worker URL 替换 Claude API 端点：

```bash
curl -X POST https://your-worker.your-subdomain.workers.dev/gemini/https://generativelanguage.googleapis.com/v1beta/v1/messages \
  -H "x-api-key: YOUR_GEMINI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-2.5-flash",
    "messages": [
      {"role": "user", "content": "Hello"}
    ]
  }'
```

### 参数说明

- URL 格式：`/{type}/{provider_url}/v1/messages`
- `type`: 目标厂商类型，目前支持 `gemini`, `openai`
- `provider_url`: 目标厂商 API 基础地址
- `x-api-key`: 目标厂商的 API Key

### 在 Claude Code 中使用

#### Mac/Linux
```bash
export ANTHROPIC_BASE_URL="https://your-worker.your-subdomain.workers.dev/gemini/https://generativelanguage.googleapis.com/v1beta"
export ANTHROPIC_API_KEY="目标厂商的 API Key"
export ANTHROPIC_MODEL="gemini-2.5-pro"
export ANTHROPIC_SMALL_FAST_MODEL="gemini-2.5-flash" # 也许你并不需要 ccr 那么强大的 route

claude
```

#### Windows PowerShell

```bash
set ANTHROPIC_BASE_URL="https://your-worker.your-subdomain.workers.dev/gemini/https://generativelanguage.googleapis.com/v1beta"
set ANTHROPIC_API_KEY="目标厂商的 API Key"
set ANTHROPIC_MODEL="gemini-2.5-pro"
set ANTHROPIC_SMALL_FAST_MODEL="gemini-2.5-flash"

claude
```

