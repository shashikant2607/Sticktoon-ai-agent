# Sticktoons AI Shorts Studio

Starter dashboard for the Sticktoons AI Facts & Technology Shorts workflow.

## Current capabilities
- Dashboard and API health check
- English YouTube Shorts script generation through OpenAI
- Google OAuth flow for YouTube upload permission
- Upload an already-rendered MP4 from a direct HTTPS URL

## Important limitation
This is a starter workflow, not a fully autonomous video factory. It does not yet generate voice-over/video footage or automatically publish twice a day. A video generation provider and a tested scheduler are still needed. Test uploads should remain private.

## Deploy
1. Import this repository into Vercel.
2. Add environment variables:
   - `GOOGLE_CLIENT_ID`
   - `GOOGLE_CLIENT_SECRET`
   - `GOOGLE_REDIRECT_URI` (exact URL: `https://YOUR-VERCEL-DOMAIN/api/callback`)
   - `YOUTUBE_REFRESH_TOKEN` (after OAuth consent)
   - `OPENAI_API_KEY` (script generation)
3. In Google Cloud Console, enable YouTube Data API v3, configure OAuth consent, and create an OAuth client of type Web application.
4. Add `https://YOUR-VERCEL-DOMAIN/api/callback` to Authorized redirect URIs.
5. Open `https://YOUR-VERCEL-DOMAIN/api/auth`, approve YouTube access, then save the returned refresh token in Vercel as `YOUTUBE_REFRESH_TOKEN`.
6. Redeploy after changing environment variables.

## Endpoints
- `GET /api/health`
- `GET /api/auth`
- `GET /api/callback`
- `POST /api/generate-script` with JSON `{ "topic": "3 surprising AI facts", "tone": "curious and punchy" }`
- `POST /api/upload-from-url` with JSON `{ "videoUrl": "https://your-host/video.mp4", "title": "Title", "description": "...", "privacyStatus": "private" }`

Never commit API keys, OAuth client secrets, or refresh tokens to GitHub or share them in chat. Use a trusted HTTPS URL for MP4 uploads.
