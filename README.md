CanvasToText v1.10
==================
THIS TOOL IS INTENDED FOR ACCESSIBILITY PURPOSES ONLY AND IS NOT DESIGNED OR INTENDED TO FACILITATE CHEATING, PLAGIARISM, OR ACADEMIC MISCONDUCT.

CanvasToText downloads audio from supported Canvas-hosted videos and sends the audio to Buzz / Faster Whisper for local transcription.

PRIVACY-CLEAN REBUILD
---------------------
- Developer names, aliases, email addresses, usernames, and developer-specific local paths are not embedded in this project.
- The application window, helper window, build scripts, and installer metadata use only the CanvasToText project name.
- The installer does not set a personal publisher/company identity.
- Runtime paths use Windows environment variables and the current user's normal AppData/Downloads folders rather than a hard-coded developer account path.

PRIVACY / SOURCE CHOICE
-----------------------
For the most privacy-preserving and least automated workflow in CanvasToText, use LOCAL MANIFEST mode instead of the automatic Canvas URL fetcher.

Local-manifest mode avoids CanvasToText launching Microsoft Edge with Selenium and therefore avoids the app generating automated browser activity. It is NOT an anonymity mode and does not guarantee that your activity cannot be seen or logged. Canvas/Instructure, your school or SSO provider, your normal browser, your device, or your network may still record normal access to the page or media.

Only download/transcribe media you are authorized to access, download, and use.

HOW TO GET A LOCAL MANIFEST
---------------------------
For a Canvas video you are already authorized to view:

1. Open the Canvas page in your normal browser and start the video.
2. Right-click the video area and choose Inspect, or press F12.
3. In Developer Tools, look for the video's media request. The Network tab is usually the most reliable place. While the video is playing, filter/search for terms such as:
      media_attachments
      redirect
      .mpd
4. Open the matching media/manifest request or link in a new browser tab.
5. Save/download the manifest file. Canvas may download it with a name such as:
      kaltura
   with no file extension. That is okay.
6. Open CanvasToText and, next to Local manifest, click:
      Browse any file...
7. Select the saved file and continue normally.

Do not use these steps to bypass authentication, DRM, paywalls, enrollment restrictions, or other access controls.

CANVAS URL SUPPORT
------------------
1. Paste the full Canvas page URL into CanvasToText.
2. Click Fetch Manifest...
3. Microsoft Edge opens using CanvasToText's dedicated browser profile.
4. Complete Canvas/SSO/MFA normally if prompted.
5. Leave the Edge window open while CanvasToText searches the page for the native Canvas media manifest.
6. When the DASH manifest is found, Edge closes automatically and the local manifest field is populated.

The URL mode is convenient, but it uses automated Edge/Selenium browser activity. Use Local manifest mode when you prefer the least automated workflow.

This feature is designed first for native Canvas media attachments. Third-party integrations such as Panopto, YouTube, external Kaltura LTI, etc. may use different systems. Use the local manifest option as the fallback.

NORMAL RELEASE BUILD
--------------------
On a Windows development PC:

1. Extract the entire CanvasToText_v1.10 folder.
2. Run:
      build_setup.bat
3. Wait for the build to finish.
4. Upload this ONE file to GitHub Releases:
      setup_output\CanvasToText_Setup_v1.10.exe

END USER INSTALLATION
---------------------
The end user only needs to:

1. Download CanvasToText_Setup_v1.10.exe
2. Run the install wizard.
3. The wizard installs/checks:
      - FFmpeg
      - Buzz
      - Microsoft Edge
4. Launch CanvasToText.

The first transcription with a Whisper model can take longer because Buzz must download that model first.

MANUAL SOURCE MODE
------------------
Developer/testing files:
- CanvasToText.py                    Main Tkinter GUI
- CanvasToTextCanvasFetch.py         Authenticated Canvas URL helper using Microsoft Edge + Selenium
- run_python.bat                     Run from Python source
- build_exe.bat                      Build both required application EXEs
- build_setup.bat                    Build the final one-file install wizard
- install_dependencies.bat           Manual FFmpeg/Buzz/Edge installer
- install_dependencies.ps1          Dependency script used by the wizard
- installer\CanvasToText.iss         Inno Setup project

NOTES
-----
- The local manifest picker accepts any file so Windows file associations do not hide oddly named manifest files.
- Audio-only mode creates a temporary MPD containing only the audio AdaptationSet, so FFmpeg avoids downloading video chunks unless Also save full video is enabled.
- Selenium Manager may download a matching Microsoft EdgeDriver the first time the Canvas URL feature is used. Internet access is required.
- Local-manifest mode avoids the automated Canvas browser fetcher but does not make Canvas access invisible or untraceable.
- Only download/transcribe media you are authorized to access and use.

LEGAL / RESPONSIBLE USE
-----------------------
CanvasToText is provided solely as an accessibility and transcription utility for users who are authorized to access the content they process.

Users are solely responsible for ensuring their use complies with applicable laws, copyright restrictions, institutional policies, academic-integrity requirements, contracts, and terms of service. The software is not intended for unauthorized access, circumvention of authentication or DRM, copyright infringement, unauthorized redistribution, cheating, plagiarism, fraud, concealment of unauthorized activity, or other unlawful or unauthorized activity.

To the maximum extent permitted by applicable law, CanvasToText is provided "AS IS" and "AS AVAILABLE," without warranties of any kind. The project contributors are not liable for damages or consequences arising from use, misuse, inability to use, or distribution of the software where such liability may legally be excluded.
