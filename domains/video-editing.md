# Video Editing

**Problem:** go from raw footage plus a brief (for example *"a 30-second highlight reel with music and captions"*) to a finished, rendered video.

← Back to the [main README](../README.md)

Video editing is not a physical-world problem, but it maps to software just as well. An edit is a sequence of operations (cut, trim, arrange, add transitions, overlay text, mix audio) over media files, and each operation can be written as code. A timeline is data, and rendering it is deterministic.

---

## Recommended tool

The right tool depends on the kind of video:

| Kind of video | Recommended tool | Language | Why |
|---|---|---|---|
| **Editing existing footage** (cutting, trimming, joining, filters, audio, encoding) | [**FFmpeg**](https://ffmpeg.org/) (CLI + filtergraphs) | Command line | The universal backend for video. Fast, available everywhere, and the tool coding agents already reach for in almost every video task. |
| **Generated / motion-graphics video** (templates, animated text, data-driven videos) | [**Remotion**](https://www.remotion.dev/) | TypeScript / React | Each frame is a React render, so layout, animation and data come from ordinary web code that LLMs write well. |
| **Full non-linear edits that a human will keep editing** | [**MLT**](https://www.mltframework.org/) (MLT XML) or [**OpenTimelineIO**](https://opentimeline.io/) | XML / JSON + Python | The edit is stored as a timeline file that opens in a real editor (Shotcut/Kdenlive for MLT; DaVinci Resolve, Premiere and others through OTIO). |

---

## Alternatives

| Tool | Language | When to use it |
|---|---|---|
| [MoviePy](https://zulko.github.io/moviepy/) | Python | Scripted editing and compositing from Python. A high-level layer on top of FFmpeg. |
| [Motion Canvas](https://motioncanvas.io/) | TypeScript | Code-driven animations and explainer videos, with a live editor. |
| [Manim](https://www.manim.community/) | Python | Mathematical and technical animations (community edition of the engine behind 3Blue1Brown). |

---

## Benchmarks

| Benchmark | What it measures | Link |
|---|---|---|
| **Timeline-Bench** | Agents doing realistic editing tasks, from raw footage and a brief to a final cut, in containers with FFmpeg, Python, Node and frameworks like Remotion. | [Paper](https://arxiv.org/abs/2609.35143) |
| VibeVideoBench | Multimodal agents that write code to produce a finished MP4 (with narration and music) within a time limit. Agents call FFmpeg in nearly every run. | [Paper](https://arxiv.org/abs/2610.35864) |
| Code2Video (HeyGen Research) | Agents producing motion-design videos through code that a rendering engine turns into video. | [Announcement](https://www.heygen.com/research/introducing-code2video-benchmark) |
| ELLMPEG | Generating correct FFmpeg commands from natural-language requests. | [Paper](https://arxiv.org/abs/2602.00028) |
