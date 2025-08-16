📢 Multi-Agent Content Distribution System (MVP)
This is an MVP multi-agent system that:
Ingests content (image/video) from your inbox folder or frontend.


Uses an LLM (OpenAI) to generate captions, hashtags, and CTAs.


Publishes content + captions to Instagram, YouTube, TikTok (via APIs or dry-run).


Lets you manage uploads & publishing via a Streamlit frontend dashboard.


Logs activity and saves receipts of published posts.



🚀 Features
Backend (Python agents):


Caption generation with LLM.


Stubs for Instagram/YouTube/TikTok posting (live mode available if you add API keys).


Optional posting to Instagram Stories.


NLP pipeline for handling metadata (title, tone, CTA, audience, keywords).


Frontend (Streamlit):


File uploader for media.


Metadata input form.


Platform selection (Instagram, YouTube, TikTok).


One-click publishing (dry-run or live mode).


View logs and receipts inside the dashboard.



📂 Project Structure
project/
│── content-multi-agent-live.py   # Backend pipeline (multi-agent system)
│── app.py                        # Streamlit frontend
│── requirements.txt               # Dependencies
│── inbox/                        # Upload media + metadata.json here
│── out/
│   ├── logs/                     # Run logs
│   └── published/                # Publishing receipts
│── .env                          # Secrets and API keys (not tracked in git)


⚙️ Setup
1. Clone repo & install dependencies
git clone <your-repo>
cd project
pip install -r requirements.txt

2. Configure environment
Create a .env file in project root:
# LLM
LLM_API_KEY=your-openai-key
LLM_MODEL=gpt-4o-mini

# Instagram (Graph API)
IG_ACCESS_TOKEN=your-instagram-token
IG_USER_ID=your-instagram-user-id

# YouTube & TikTok (placeholders for OAuth/SDK)
YOUTUBE_API_KEY=your-youtube-key
TIKTOK_API_KEY=your-tiktok-key

⚠️ Currently YouTube & TikTok posting are stubs. You’ll need to integrate their official APIs/SDKs for full publishing.

▶️ Usage
Run Backend Directly (CLI)
python content-multi-agent-live.py \
    --inbox ./inbox \
    --out ./out \
    --platforms instagram,youtube,tiktok \
    --also-story \
    --live

Options:
--inbox → Folder with media + metadata.json


--out → Output directory


--platforms → Comma-separated platforms


--also-story → Post to IG Story


--live → Actually publish (omit for dry-run)



Run Frontend (UI)
streamlit run app.py

Open http://localhost:8501
Features:
 ✅ Upload media
 ✅ Save metadata
 ✅ Select platforms
 ✅ Trigger backend pipeline
 ✅ Inspect logs & receipts

📝 Metadata Format
Saved as inbox/metadata.json by frontend:
{
  "title": "My Product Launch",
  "keywords": ["AI", "automation", "startup"],
  "tone": "exciting",
  "cta": "Follow us for more updates!",
  "audience": "tech enthusiasts"
}


📜 Logs & Receipts
Logs are saved in out/logs/run.log


Receipts are JSON reports saved in out/published/


Example:
{
  "timestamp": "2025-08-16T14:05:12Z",
  "platforms": ["instagram", "youtube"],
  "live": false,
  "results": [
    {"platform": "instagram", "status": "dry-run", "caption": "🚀 Exciting news..."},
    {"platform": "youtube", "status": "dry-run", "caption": "🚀 Exciting news..."}
  ]
}


⚠️ Notes
Instagram live posting requires Graph API and a Business Account.


YouTube & TikTok need OAuth setup (placeholders included).


Streamlit frontend is for local testing — deployable to Streamlit Cloud or any Python server.



🛠️ Roadmap
✅ MVP with backend + frontend


🔜 Edit captions before publishing


🔜 Full TikTok/YouTube API integration


🔜 Comment NLP responder agent


🔜 Scheduler for automated posting

