# Story to Video Agent for Claude Code

Transform personal stories, testimonies, and narratives into beautifully illustrated narrated videos — fully automated with AI.

## What It Does

This Claude Code agent takes a story and produces a complete video with:
- Watercolor-style illustrations with consistent characters
- Professional narration (Hebrew or English)
- Ken Burns zoom/pan effects
- Chapter title cards
- Fade transitions

### Three Input Modes

| Mode | Input | What Happens |
|------|-------|-------------|
| **YouTube URL** | A YouTube link | Extracts transcript → summarizes → creates story → illustrates → narrates → video |
| **Paste Text** | Raw transcript or text | Summarizes → creates story → illustrates → narrates → video |
| **Your Story** | Pre-written story | Splits into chapters → illustrates → narrates → video |

### Interactive Process

The agent doesn't just run — it collaborates with you:
1. Asks about target age, language, style, and length
2. **Checkpoint 1**: Shows you the story draft for approval
3. **Checkpoint 2**: Shows image concepts before generating
4. Generates everything and assembles the final video

## Installation

### 1. Copy the agent

```bash
# Clone this repo
git clone https://github.com/elad-refoua/story-to-video-agent.git

# Copy agent to your Claude Code agents directory
cp -r story-to-video-agent/.claude/agents/story-to-video ~/.claude/agents/
```

### 2. Set up your API key

Get a free Gemini API key at [Google AI Studio](https://aistudio.google.com/apikey), then:

```bash
# Add to your shell profile (~/.bashrc, ~/.zshrc, etc.)
export GEMINI_API_KEY=your_key_here
```

### 3. Install dependencies

```bash
# Required
pip install Pillow python-bidi google-genai

# Optional (for YouTube URL mode)
pip install yt-dlp

# ffmpeg must be installed and in PATH
# macOS: brew install ffmpeg
# Ubuntu: sudo apt install ffmpeg
# Windows: download from https://ffmpeg.org/download.html
```

## Usage

Open Claude Code and say:

```
Create a video from this YouTube testimony: https://youtube.com/watch?v=...
```

Or:

```
I have a story I'd like to turn into an illustrated video for children ages 6-9
```

Or:

```
/story-to-video
```

## Examples

### Holocaust Testimony → Children's Video
```
Input: YouTube URL of a Yad Vashem testimony
Settings: Ages 6-9, Hebrew, 5 minutes, emphasis on family and hope
Output: 5-minute watercolor-illustrated video with Hebrew narration
```

### Family Immigration Story
```
Input: Pasted text from grandmother's memoir
Settings: Ages 9-12, English, 3 minutes, emphasis on courage
Output: 3-minute illustrated video with English narration
```

### Pre-Written Children's Story
```
Input: A story you already wrote
Settings: Ages 4-6, Hebrew, 2 minutes
Output: 2-minute picture-book-style video
```

## Technical Details

### Image Generation
- Model: Gemini 3.1 Flash Image (Nano Banana 2)
- Character consistency via reference image technique
- Watercolor children's book style
- 1920x1080 resolution

### Audio Narration
- Model: Gemini 2.5 Pro TTS (storytelling) / Flash TTS (emotional scenes)
- Voice: Kore (best Hebrew female voice)
- Proper names written in English for correct pronunciation
- SPEECH_DIR for natural pacing

### Video Assembly
- ffmpeg with Ken Burns zoom/pan effects
- Fade transitions between chapters
- Hebrew RTL title cards via PIL + python-bidi
- H.264 codec, AAC audio

## Requirements

| Requirement | Details |
|------------|---------|
| Claude Code | With Opus model access |
| GEMINI_API_KEY | Free tier from Google AI Studio |
| ffmpeg | Installed and in PATH |
| Python 3.8+ | With Pillow, python-bidi, google-genai |
| yt-dlp | Optional, for YouTube mode only |

## Limitations

- Character consistency is ~80% similar (AI image generation limitation)
- Hebrew TTS pronunciation is stochastic — same text may sound different each run
- Gemini may refuse to generate certain historical imagery
- Maximum ~10 minutes of video per run (API quotas)

## License

MIT License — use freely for personal and educational projects.

## Credits

Built with Claude Code, Gemini API, and ffmpeg.
Inspired by the mission to preserve and share personal stories across generations.
