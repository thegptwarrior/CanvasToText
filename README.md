# CanvasToText

**A local Windows accessibility tool for converting supported Canvas-hosted lecture videos into readable transcripts.**

> **THIS TOOL IS INTENDED FOR ACCESSIBILITY PURPOSES ONLY AND IS NOT DESIGNED OR INTENDED TO FACILITATE CHEATING, PLAGIARISM, OR ACADEMIC MISCONDUCT.**

CanvasToText is designed primarily for students who are deaf, hard of hearing, or otherwise benefit from having video lectures available as text.

The application can locate supported Canvas-hosted media, download the audio, and transcribe it locally on your computer using Whisper-based transcription engines.

No cloud transcription API is required.

---

# Which Version Should I Download?

CanvasToText currently has multiple releases while smaller and faster transcription backends are being tested.

| Version | Best For | Transcription | Approx. Storage | Speed | Status |
|---|---|---|---:|---|---|
| **CanvasToText Full** | Maximum compatibility / proven setup | Buzz + Faster-Whisper | ~8–9+ GB | Fast | ✅ Stable |
| **CanvasToText Lite GPU** | NVIDIA GPU users | Faster-Whisper + CUDA | ~1.3 GB runtime + model | Very Fast | 🧪 Beta |
| **CanvasToText Lite** | Low-storage / CPU-only systems | whisper.cpp | Much smaller | Slower | 🧪 Beta |

## Recommended Version

### Most users

Use **CanvasToText Full** if you want the most tested version and do not mind the large Buzz installation.

### NVIDIA GPU users

Try **CanvasToText Lite GPU** if you have an NVIDIA GTX/RTX GPU and want a substantially smaller installation with GPU-accelerated transcription.

The Lite GPU build can also fall back to CPU transcription if a compatible NVIDIA GPU is unavailable.

### Low-storage computers

Use **CanvasToText Lite** if minimizing storage usage is more important than transcription speed.

CPU transcription can be significantly slower than GPU-accelerated transcription.

---

# Features

CanvasToText currently supports:

- Local Whisper-based transcription
- TXT transcript output
- SRT subtitle output
- Audio-only downloading
- Optional full-video downloading
- Automatic Canvas media detection for supported native Canvas videos
- Manual local-manifest workflow
- Microsoft Edge authentication through the user's normal Canvas login
- Dedicated CanvasToText Edge profile
- Output-folder selection
- Persistent default output directory
- Automatic dependency setup
- Local transcription without a cloud transcription API
- Windows installer
- Windows uninstaller
- NVIDIA CUDA acceleration in the Lite GPU release
- CPU fallback when GPU acceleration is unavailable
- Download and transcription progress reporting

---

# How CanvasToText Works

A typical CanvasToText workflow looks like this:

```text
Canvas lecture page
        ↓
Canvas media manifest
        ↓
FFmpeg downloads audio
        ↓
Local Whisper transcription
        ↓
TXT / SRT transcript
```

The exact transcription engine depends on the release being used.

## Full Release

```text
Canvas
  ↓
FFmpeg
  ↓
Buzz / Faster-Whisper
  ↓
TXT / SRT
```

## Lite GPU Release

```text
Canvas
  ↓
FFmpeg
  ↓
Faster-Whisper
  ↓
NVIDIA CUDA when available
  ↓
TXT / SRT
```

## Lite Release

```text
Canvas
  ↓
FFmpeg
  ↓
whisper.cpp
  ↓
CPU transcription
  ↓
TXT / SRT
```

---

# Supported Operating Systems

CanvasToText currently targets:

**Windows 10 / Windows 11 x64**

The project is not currently packaged for:

- macOS
- Linux
- Windows ARM

Support for additional platforms may be considered later.

---

# Hardware Support

## NVIDIA GPUs

The **Lite GPU** release supports NVIDIA CUDA acceleration through Faster-Whisper.

Examples include many:

- NVIDIA RTX 20-series
- NVIDIA RTX 30-series
- NVIDIA RTX 40-series
- NVIDIA RTX 50-series
- compatible GTX GPUs

A dedicated CUDA Toolkit installation should not normally be required by the current Lite GPU package because the necessary runtime libraries are included with its Faster-Whisper environment.

## AMD GPUs

AMD GPU acceleration is not currently enabled in the public build.

CanvasToText should instead use CPU transcription.

## Intel GPUs

Intel GPU acceleration is not currently enabled in the public build.

CanvasToText should instead use CPU transcription.

## CPU-Only Computers

CanvasToText can operate without a supported NVIDIA GPU.

Transcription will simply be slower.

---

# Whisper Models

Different Whisper models trade speed for accuracy.

Typical choices include:

| Model | Speed | Accuracy | Storage |
|---|---|---|---|
| Tiny | Fastest | Lower | Small |
| Base | Very Fast | Good | Small |
| Small | Fast | Very Good | Moderate |
| Medium | Slower | Higher | Large |
| Large | Slowest | Highest | Very Large |

For most lecture transcription, **Small** provides a good balance of speed and accuracy on capable hardware.

CPU-only systems may benefit from using **Base** or **Tiny** for faster transcription.

Models may need to be downloaded the first time they are selected.

Because models are stored locally after downloading, later transcriptions do not normally need to download the same model again.

---

# Installation

Go to the project's **GitHub Releases** page and download the installer for the version you want.

Normal users should download the installer `.exe`.

You do **not** need:

- Python
- PyInstaller
- Inno Setup
- the source code
- development scripts

to use the normal release.

Run the installer and follow the Windows setup wizard.

---

# Full Release Installation

The Full release automatically checks or installs the dependencies it needs.

These include:

- FFmpeg
- Buzz
- Microsoft Edge

## Important: Buzz Is Large

Buzz currently uses approximately **8–9 GB of installed disk space** on some systems.

This means installation can take several minutes depending on:

- internet speed
- disk speed
- Windows security scanning
- computer performance

If the installer appears to remain on the Buzz download for a while, allow it time to finish.

The smaller Lite releases were created specifically to reduce this storage requirement.

---

# Lite GPU Installation

The Lite GPU release does **not** install the full Buzz application.

Instead, it uses a standalone Faster-Whisper environment.

The Faster-Whisper runtime is approximately **1.3 GB**, with additional storage required for the selected Whisper model.

On a supported NVIDIA computer:

```text
NVIDIA GPU detected
        ↓
CUDA acceleration
        ↓
Fast local transcription
```

On a computer without a supported NVIDIA GPU:

```text
No compatible NVIDIA GPU
        ↓
CPU fallback
        ↓
Local transcription
```

CPU transcription can take considerably longer.

---

# Windows SmartScreen

CanvasToText is currently distributed without a commercial code-signing certificate.

Windows may therefore display a warning such as:

> Windows protected your PC

or:

> Microsoft Defender SmartScreen prevented an unrecognized app from starting.

This does not automatically mean Windows detected malware.

New or unsigned applications frequently lack established SmartScreen reputation.

Only download CanvasToText from the project's official GitHub Releases page.

If you trust the downloaded release and Windows presents an unrecognized-app warning, Windows may provide:

```text
More info
→
Run anyway
```

Use your own judgment before running any unsigned application downloaded from the internet.

---

# Using CanvasToText

CanvasToText provides two primary ways of locating Canvas media.

## Method 1 — Canvas URL

This is the most convenient method.

1. Open CanvasToText.
2. Copy the full URL of the Canvas page containing the video.
3. Paste the URL into the Canvas URL field.
4. Click **Fetch Manifest**.
5. Microsoft Edge opens using CanvasToText's dedicated browser profile.
6. Sign into Canvas normally if requested.
7. Complete SSO or MFA normally if required.
8. Leave Edge open while CanvasToText searches the page.
9. When a supported native Canvas media manifest is found, the manifest field is populated automatically.
10. Choose your output options.
11. Start transcription.

CanvasToText does **not** request that you enter your Canvas password directly into the application.

Authentication occurs through Microsoft Edge and the normal Canvas/SSO website.

---

# Local Manifest Mode

Local Manifest mode is available as a less automated alternative.

This mode avoids CanvasToText launching an automated Edge/Selenium session.

It does **not** make Canvas usage anonymous or invisible.

Canvas, your institution, your SSO provider, your browser, your device, or your network may still log normal access to course pages or media.

---

# How to Get a Local Manifest

Only use this workflow with content that you are already authorized to access.

1. Open the Canvas page containing the video in your normal browser.
2. Start playing the video.
3. Open Developer Tools by pressing:

```text
F12
```

or right-clicking the page and selecting:

```text
Inspect
```

4. Open the **Network** tab.
5. While the video is playing, search for requests containing terms such as:

```text
media_attachments
redirect
.mpd
```

6. Locate the media manifest request associated with the video.
7. Open that request or URL.
8. Save the resulting file.

Canvas may save the file with a name such as:

```text
kaltura
```

with no extension.

That is okay.

9. Open CanvasToText.
10. Next to **Local manifest**, select:

```text
Browse any file...
```

11. Select the saved manifest.
12. Choose the desired output settings.
13. Start transcription.

Do not use these instructions to bypass:

- authentication
- DRM
- paywalls
- course enrollment restrictions
- access controls
- permissions you do not have

---

# Canvas URL Compatibility

The automatic URL mode is designed primarily for **native Canvas-hosted media attachments**.

Some course videos may instead be hosted through third-party systems such as:

- Panopto
- YouTube
- external Kaltura integrations
- other LMS integrations
- external video providers

These services may use completely different delivery systems.

CanvasToText does not claim universal compatibility with every video embedded inside Canvas.

When automatic URL detection does not work, Local Manifest mode may be available for supported media that you are authorized to access.

---

# Output Files

Depending on the selected options, CanvasToText can create:

```text
lecture.txt
lecture.srt
lecture.m4a
lecture.mp4
```

## TXT

Plain-text transcription.

Useful for:

- reading lecture content
- accessibility software
- searching
- studying
- note organization

## SRT

Timestamped subtitle file.

Useful for:

- captions
- video players
- locating where something was said
- accessibility workflows

## M4A

Downloaded lecture audio.

This can optionally be retained after transcription.

## MP4

Optional full-video download.

Downloading the entire video requires significantly more bandwidth and storage than audio-only transcription.

---

# Audio-Only Mode

By default, CanvasToText can create an audio-only version of a DASH media manifest.

This allows FFmpeg to download only the audio portion of supported media rather than downloading every video segment.

This reduces:

- download size
- network usage
- processing time
- storage requirements

The full video is only downloaded when the appropriate option is enabled.

---

# Privacy and Local Processing

CanvasToText was designed to minimize unnecessary external processing.

## Transcription

Transcription happens locally on your computer.

The application does not require a cloud speech-to-text API.

Your downloaded lecture audio is processed using the locally installed transcription engine.

## Canvas Authentication

CanvasToText does not ask users to type their Canvas password directly into CanvasToText.

When automatic URL mode requires authentication, login happens through Microsoft Edge and the normal Canvas/SSO page.

## Local Manifest Mode

For the least automated CanvasToText workflow, use Local Manifest mode.

This avoids the application launching Edge through Selenium.

However:

**Local Manifest mode is not an anonymity feature.**

Normal Canvas access may still be visible to:

- Canvas / Instructure
- your school
- your SSO provider
- Microsoft or another identity provider when applicable
- your normal browser
- your operating system
- your device administrator
- your internet/network administrator

CanvasToText does not claim to make activity invisible or untraceable.

---

# Developer Privacy

Public builds are intended not to contain developer-specific personal information.

The project avoids intentionally embedding:

- developer names
- personal email addresses
- personal Windows usernames
- personal computer paths
- school-specific identifiers
- developer-specific local directories

Runtime paths are generated from normal Windows environment locations such as:

```text
%APPDATA%
%LOCALAPPDATA%
Downloads
```

rather than hard-coded developer paths.

Build logs created on an individual developer's computer may naturally display that computer's local filesystem paths.

Those build-time console messages are not necessarily embedded into the final application.

---

# Application Data

CanvasToText may create application data under a location similar to:

```text
%APPDATA%\CanvasToText
```

Depending on the release, this may contain:

- application settings
- output-folder preferences
- Canvas Edge browser profile
- fetch logs
- local configuration

Some Lite builds may also store runtime or model information in application-specific directories.

---

# Uninstalling CanvasToText

CanvasToText includes a normal Windows uninstaller.

You can uninstall it through:

```text
Windows Settings
→ Apps
→ Installed apps
→ CanvasToText
→ Uninstall
```

or through the CanvasToText Start Menu entry when available.

The uninstaller may ask whether application data should also be removed.

Output files created by the user, such as:

- transcripts
- subtitles
- downloaded audio
- downloaded videos

are not intended to be automatically deleted during normal uninstall.

Independent software installed outside CanvasToText may also remain installed.

For example, the Full release does not automatically remove an existing installation of:

- FFmpeg
- Buzz
- Microsoft Edge

because those applications may be used independently of CanvasToText.

---

# Troubleshooting

## The Installer Seems Stuck

Large dependencies can take time to download and install.

The Full release in particular installs Buzz, which may occupy approximately 8–9 GB.

Check:

- network activity
- disk activity
- installer status text

before closing the installer.

---

## First Transcription Is Slow to Start

The selected Whisper model may need to download the first time it is used.

After the model is stored locally, future transcriptions using that same model should start faster.

---

## Transcription Is Very Slow

Check which transcription backend is being used.

An NVIDIA CUDA-enabled computer can be dramatically faster than CPU-only transcription.

If you are using the Lite GPU build but no compatible NVIDIA GPU is detected, CanvasToText may fall back to CPU mode.

Try a smaller model such as:

```text
Base
```

or:

```text
Tiny
```

if speed is more important than maximum transcription accuracy.

---

## NVIDIA GPU Is Not Being Used

Make sure:

- your NVIDIA graphics driver is installed
- Windows can see the NVIDIA GPU
- you are using the Lite GPU release
- the transcription log reports GPU/CUDA operation

In Windows Task Manager you can also inspect:

```text
Performance
→ GPU
```

and look at CUDA / Compute activity while transcription is running.

---

## Canvas URL Fetch Does Not Work

Possible causes include:

- the video is not native Canvas media
- the course uses Panopto or another external provider
- browser authentication has not completed
- the Canvas page uses a different media system
- Selenium/EdgeDriver needs to update
- the media request is inaccessible

Try Local Manifest mode when appropriate.

---

## Canvas Downloads a File Named `kaltura`

That can be normal.

Some supported manifests may download without a `.mpd` extension.

CanvasToText intentionally allows the Local Manifest file picker to select **any file** so extensionless manifest files can still be used.

---

# Internet Requirements

An internet connection may be required for:

- downloading Canvas media
- installing dependencies
- downloading transcription runtimes
- downloading Whisper models
- Selenium Manager / EdgeDriver setup
- authentication through Canvas / SSO

Once the necessary model and transcription runtime are installed, the actual speech-to-text processing occurs locally.

---

# Build From Source

Normal users do not need to build CanvasToText.

The following section is intended for developers.

A typical source package may contain:

```text
CanvasToText.py
CanvasToTextCanvasFetch.py
CanvasToText.ico

run_python.bat
build_exe.bat
build_setup.bat

install_dependencies.bat
install_dependencies.ps1

installer\
    CanvasToText.iss
```

## CanvasToText.py

Main Tkinter graphical interface.

## CanvasToTextCanvasFetch.py

Canvas URL helper responsible for authenticated media discovery through Microsoft Edge and Selenium.

## install_dependencies.ps1

Handles dependency installation and setup.

Dependencies vary depending on the release.

## build_exe.bat

Builds Windows executables.

## build_setup.bat

Builds the final Windows installer.

## installer/CanvasToText.iss

Inno Setup installer project.

---

# Building the Windows Installer

On a Windows development computer:

1. Install Python.
2. Install the required Python packages.
3. Install PyInstaller.
4. Install Inno Setup.
5. Extract the complete CanvasToText source package.
6. Run:

```text
build_setup.bat
```

7. Wait for the application and installer to build.

The completed installer should appear under a directory similar to:

```text
setup_output\
```

Only the final setup `.exe` needs to be distributed to normal end users.

---

# Accessibility Purpose

CanvasToText exists to help make audiovisual educational material more accessible as readable text.

Potential accessibility uses include:

- deaf and hard-of-hearing students
- users who benefit from captions
- users who process written information more effectively than spoken information
- reviewing inaccessible lecture recordings
- generating searchable local transcripts
- assisting with note-taking from authorized educational material

CanvasToText is not intended to replace official accessibility accommodations.

Students who require formal accommodations should also contact their institution's accessibility/disability services when appropriate.

---

# Responsible Use

CanvasToText should only be used with media that you are authorized to access and process.

Do not use CanvasToText to:

- bypass authentication
- defeat DRM
- defeat paywalls
- bypass enrollment restrictions
- gain access to content you are not authorized to view
- redistribute copyrighted material without permission
- impersonate another user
- commit plagiarism
- cheat
- violate academic-integrity policies
- conceal unauthorized activity

A technical ability to access or download something does not necessarily mean you have legal or contractual permission to do so.

---

# Legal Disclaimer

CanvasToText is provided solely as an accessibility and transcription utility for users who are authorized to access the content they process.

Users are solely responsible for ensuring that their use of CanvasToText complies with all applicable:

- laws
- copyright restrictions
- licenses
- contracts
- institutional policies
- academic-integrity rules
- terms of service
- privacy requirements

CanvasToText is not intended for unauthorized access, circumvention of authentication or DRM, copyright infringement, unauthorized redistribution, cheating, plagiarism, fraud, or other unlawful or unauthorized activity.

To the maximum extent permitted by applicable law, CanvasToText is provided:

> **"AS IS" and "AS AVAILABLE"**

without warranties of any kind.

The project contributors are not liable for damages or consequences arising from use, misuse, inability to use, or distribution of the software where such liability may legally be excluded.

This README is informational and does not constitute legal advice.

---

# Third-Party Software

CanvasToText relies on or interacts with third-party open-source and commercial software depending on the release.

These may include:

- FFmpeg
- Whisper
- whisper.cpp
- Faster-Whisper
- CTranslate2
- Buzz
- Selenium
- Microsoft Edge
- PyInstaller
- Inno Setup

Each third-party component remains subject to its own license and terms.

Where a third-party license requires redistribution of copyright or license notices, those notices should be preserved with distributed builds.

---

# No Affiliation

CanvasToText is an independent project.

It is not affiliated with, endorsed by, sponsored by, or officially supported by:

- Instructure
- Canvas
- Microsoft
- OpenAI
- FFmpeg
- Buzz
- Faster-Whisper
- whisper.cpp
- any university
- any school district
- any educational institution

Product names and trademarks belong to their respective owners.

---

# Project Status

CanvasToText is actively being developed.

Current development priorities include:

- reducing installation size
- improving transcription speed
- improving hardware detection
- improving GPU acceleration
- improving CPU fallback performance
- simplifying installation
- improving compatibility across Windows hardware
- improving accessibility workflows
- improving error reporting

The Lite and Lite GPU versions should currently be considered experimental until they receive broader testing across different computers.

---

# Releases

For normal installation, use the project's GitHub Releases page:

**GitHub → CanvasToText → Releases**

Do not download random copies of CanvasToText from third-party websites.

For security and consistency, use the project's official GitHub repository and official release assets.

---

# Feedback and Bug Reports

If something does not work, useful information to include in a bug report includes:

```text
CanvasToText version:
Windows version:
CPU:
GPU:
RAM:
Selected Whisper model:
Canvas URL mode or Local Manifest mode:
Error message:
Relevant application log:
```

Do **not** publicly post:

- Canvas passwords
- SSO passwords
- authentication cookies
- session tokens
- private course links
- personally identifying school information

when filing bug reports.

---

# Summary

CanvasToText provides a local accessibility-focused workflow for converting supported Canvas lecture videos into readable transcripts.

```text
Authorized Canvas media
        ↓
Local audio download
        ↓
Local Whisper transcription
        ↓
TXT / SRT
```

The Full release prioritizes proven compatibility.

The Lite release prioritizes minimal storage.

The Lite GPU release aims to provide the best balance of:

**smaller installation + fast local GPU transcription.**
