💡 Inspiration

In the chaos of a disaster—like an earthquake or flood—first responders are overwhelmed. Finding a victim is only half the battle; assessing their medical state and keeping them calm until help arrives is critical. We realized that while drones can "see" people, they lack the medical intelligence to triage injuries and the empathy to comfort terrified survivors who might not speak English. We wanted to build a system that turns any camera into an "AI Paramedic."

🚑 What it does

The Paramedic's Eye is an intelligent wearable/device that performs three critical rescue tasks in real-time:

Visual Medical Triage: It analyzes live video feed to identify victims and assess visible injuries (e.g., fractures, bleeding, consciousness) and assigns a Triage Code (Green/Yellow/Red).

Multilingual Empathy: Using context-aware AI, it detects the likely demographic of the victim and speaks a comforting message in their native language (e.g., Urdu or English) using phonetic Roman script to ensure proper pronunciation.

Automated Reporting: It generates structured data logs of the victim's location and status instantly, removing the need for manual paperwork in a crisis.

⚙️ How we built it

We built the system using Python as the core controller.

Vision & Reasoning: We utilized the Google Gemini API (specifically the Flash models for low latency). We stream video frames from a smartphone camera (via IP Webcam) to the Gemini model.

Prompt Engineering: We designed a complex system prompt that forces Gemini to act as a medical expert and a translator simultaneously. It outputs a strict structure containing the Triage Color, Injury Description, and a Phonetic Roman Urdu translation for the voice engine.

Real-Time Performance: To prevent video lag while the AI "thinks," we implemented Python Threading. This allows the video feed to remain smooth (30fps) while the AI processes frames in the background.

Voice Synthesis: We integrated an offline Text-to-Speech engine (pyttsx3) that reads the AI-generated comfort messages aloud to the victim.

🚧 Challenges we ran into

The biggest challenge was latency. Sending high-definition video to the cloud took too long for a "real-time" rescue scenario. We solved this by resizing frames before transmission and using a threaded architecture to decouple the rendering loop from the API inference loop. Another challenge was Language Barriers. Standard TTS engines cannot read Urdu script. We had to engineer the Gemini prompt to output "Roman Urdu" (Urdu written in English letters) so the robot could pronounce "Ghabrayein mat" (Don't worry) correctly.

🏆 Accomplishments that we're proud of

We are proud that we didn't just build a "chatbot." We built a full feedback loop: The AI sees, thinks, and speaks back to the physical world. Getting the system to correctly identify a "broken leg" and immediately switch to a comforting Urdu voice was a huge "Wow" moment for us.

🚀 What's next for The Paramedic's Eye

Drone Integration: Moving the software from a handheld device to an autonomous rescue drone.

Offline Models: Implementing Gemini Nano to run the triage logic entirely on-device without internet.

Vital Sign Detection: Using rPPG (remote photoplethysmography) to detect heart rate via the camera.
