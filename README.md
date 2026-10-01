# 🎬 AI Video Generator Workflow

Automated AI-powered short-form video generation and multi-platform publishing workflow for n8n.

## 📋 Overview

This workflow automatically:
1. Takes a topic input via web form
2. Generates video script using AI (Groq/Llama)
3. Creates AI-generated videos (Kling AI via PiAPI)
4. Generates voiceover (ElevenLabs)
5. Merges video + audio (Creatomate)
6. Publishes to TikTok and YouTube Shorts

## 🔧 Required Services

| Service | Purpose | Pricing |
|---------|---------|---------|
| [Groq](https://groq.com) | AI Script Generation | FREE |
| [PiAPI](https://piapi.ai) | Kling AI Video Generation | ~$0.20/video |
| [ElevenLabs](https://elevenlabs.io) | Text-to-Speech | FREE tier available |
| [Creatomate](https://creatomate.com) | Video Merging | FREE tier available |
| [Late](https://getlate.dev) | TikTok Publishing | FREE tier available |
| [YouTube API](https://console.cloud.google.com) | YouTube Publishing | FREE |

## 🚀 Setup

### 1. Import Workflow
- Open n8n
- Go to Workflows → Import
- Select `myVideoGenerator-safe.json`

### 2. Configure API Keys
Copy `.env.example` to `.env` and fill in your API keys:

```bash
cp .env.example .env
```

### 3. Update Nodes
Replace placeholder values in these nodes:
- `groq` → Authorization header
- `PiAPI_Kling_Video` → x-api-key header
- `Get_Kling_Video` → x-api-key header
- `Creatomate_Merge` → Authorization header
- `Get_Render_Status` → Authorization header
- `Generate_Captions` → Authorization header
- `Post_to_TikTok` → Authorization header + connection_id
- `Generate_YouTube_Title` → Authorization header
- `Convert text to speech1` → ElevenLabs credential
- `Upload a video` → YouTube OAuth credential

### 4. Connect Accounts
- **ElevenLabs**: Create credential in n8n with API key
- **YouTube**: Set up OAuth2 in Google Cloud Console, add test user

## 📊 Workflow Structure

```
Form Input
    ↓
Groq (Script Generation)
    ↓
Parse Script
    ↓
┌───────────────────┐
↓                   ↓
Split_Narrations    Split_Video_Prompts
↓                   ↓
ElevenLabs TTS      PiAPI Kling Video
↓                   ↓
└─────────┬─────────┘
          ↓
        Merge
          ↓
   Creatomate (Video+Audio)
          ↓
      Prepare_Post
          ↓
   Generate_Captions (AI)
          ↓
    ┌─────┴─────┐
    ↓           ↓
TikTok      YouTube Shorts
```

## 💰 Cost Estimate

| Component | Cost per Video |
|-----------|----------------|
| Groq | FREE |
| Kling AI (4 scenes) | ~$0.80 |
| ElevenLabs | FREE (limited) |
| Creatomate | FREE (limited) |
| Late/TikTok | FREE |
| YouTube | FREE |
| **TOTAL** | **~$0.80/video** |

## 📝 Form Fields

| Field | Description | Required |
|-------|-------------|----------|
| Topic | Main video topic | ✅ |
| Detailed Description | Visual details | ✅ |
| Visual Style | Cinematic style | ❌ |
| Target Emotion | Desired feeling | ❌ |
| Color Palette | Color scheme | ❌ |
| Duration | Video length (seconds) | ✅ |
| Scenes | Number of scenes | ✅ |

## 🎯 Output

- **TikTok**: Vertical video (9:16) with AI-generated caption
- **YouTube Shorts**: Same video with optimized title/description

## ⚠️ Important Notes

1. **PiAPI Credits**: Make sure to have credits loaded
2. **YouTube OAuth**: Add yourself as test user in Google Cloud Console
3. **TikTok Connection**: Set up Late connection first
4. **Video Duration**: Each scene is ~5 seconds

## 📄 License

MIT License - Feel free to modify and use!

## 🤝 Contributing

Pull requests welcome! Please update documentation for any changes.
# myVideoGenerator

---

Built by [Adem Batur](https://github.com/adembtr) · License: [MIT](LICENSE)
