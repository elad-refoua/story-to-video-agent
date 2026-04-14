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

### The easy way (let Claude do it)

1. Install [Claude Code](https://docs.anthropic.com/en/docs/claude-code) or Claude Desktop
2. Tell Claude:

```
Download and install the story-to-video agent from https://github.com/elad-refoua/story-to-video-agent
```

Claude will clone the repo, copy the agent files, and install all dependencies. If you don't have a Gemini API key, the agent will walk you through getting a free one.

### Manual installation

```bash
git clone https://github.com/elad-refoua/story-to-video-agent.git
mkdir -p ~/.claude/agents
cp -r story-to-video-agent/.claude/agents/story-to-video ~/.claude/agents/
pip install Pillow python-bidi google-genai yt-dlp
```

Install ffmpeg:
- **Mac**: `brew install ffmpeg`
- **Linux**: `sudo apt install ffmpeg`
- **Windows**: Download from [gyan.dev/ffmpeg](https://www.gyan.dev/ffmpeg/builds/), extract, and add the `bin` folder to your PATH

Get a free Gemini API key at [Google AI Studio](https://aistudio.google.com/apikey) and set it:
```bash
# Mac/Linux — add to ~/.bashrc or ~/.zshrc to persist
export GEMINI_API_KEY=your_key_here

# Windows CMD
set GEMINI_API_KEY=your_key_here

# Windows PowerShell
$env:GEMINI_API_KEY="your_key_here"
```

## Usage

Just talk to Claude naturally:

```
I have a testimony of my grandfather on Yad Vashem, help me turn it into a children's video
```

```
Create a video from this YouTube testimony: https://youtube.com/watch?v=...
```

```
I wrote a story and I want to illustrate and narrate it as a video for kids ages 6-9
```

The agent will ask you questions, show drafts for approval, and produce the final video.

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
