# Voice Assistant (Jarvis-style) in Python

A voice-controlled desktop assistant built in Python. Say the wake word, then give a command: it can open websites, play songs from a custom music library, read out the latest news headlines, and answer general questions through an AI chat model.

## Features

- **Wake word activation:** listens in the background and wakes up when it hears the wake word ("Baala").
- **Voice commands:** speech is converted to text with Google's speech recognition.
- **Open websites:** "open Google", "open YouTube", "open Facebook", "open LinkedIn".
- **Play music:** "play skyfall" opens the matching song from your own music library.
- **News headlines:** "news" fetches India's top headlines from NewsAPI and reads them aloud.
- **Conversation:** any other command is sent to an AI chat model, and the short reply is spoken back.
- **Spoken replies:** text-to-speech using gTTS and pygame.

## Tech Stack

| Purpose | Library / Service |
|---|---|
| Speech to text | `SpeechRecognition` (Google Web Speech API), `PyAudio` |
| Text to speech | `gTTS`, `pygame` (`pyttsx3` as an offline option) |
| AI replies | OpenAI API (`gpt-3.5-turbo`) |
| News | NewsAPI + `requests` |
| Browser control | `webbrowser` (standard library) |

## Project Structure

```
voice-assistant/
├── main.py            # main program: wake word, command handling, speech
├── musicLibrary.py    # song names mapped to YouTube links
├── client.py          # small script to test the AI API on its own
└── README.md
```

## Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/netra-p/voice-assistant.git
   cd voice-assistant
   ```

2. **Install the requirements** (Python 3.8 or newer)
   ```bash
   pip install SpeechRecognition pyaudio pyttsx3 gTTS pygame requests openai
   ```
   If `pyaudio` fails to install on Windows, use `pip install pipwin` and then `pipwin install pyaudio`.

3. **Add your API keys**
   - OpenAI key: replace `<Your Key Here>` in `main.py` (and `client.py` if you want to test it).
   - NewsAPI key: get a free key at https://newsapi.org and replace the `newsapi` value in `main.py`.
   - Never upload your real keys to GitHub. Keep them in environment variables or a file that is listed in `.gitignore`.

4. **Run the assistant**
   ```bash
   python main.py
   ```
   You need a working microphone and an internet connection.

## How to Use

1. Run `main.py` and wait for the assistant to greet you.
2. Say the wake word: **"Baala"**. The assistant replies and starts listening.
3. Say a command, for example:
   - "Open YouTube"
   - "Play stealth"
   - "Tell me the news"
   - "Tell me a joke"

## Adding Your Own Songs

Open `musicLibrary.py` and add a new entry with a one-word name and a link:

```python
music = {
    "skyfall": "https://www.youtube.com/watch?v=...",
    "yoursong": "https://www.youtube.com/watch?v=..."
}
```

Then say "play yoursong".

## How It Works

1. A loop listens for short audio clips and checks whether the wake word was spoken.
2. After the wake word, the next phrase is captured as the command.
3. `processCommand()` checks the command for keywords (open, play, news).
4. If no keyword matches, the command goes to the AI model and the reply is spoken aloud.

## Known Limitations and Future Work

- Only one-word song names are supported when playing music.
- The wake word detection needs a quiet room and a clear voice.
- Add calendar reminders (for example with the Google Calendar API).
- Add offline speech recognition and error handling for unknown songs.
- Add a simple GUI.

## Author

**Netra Puranik**
Electronics and Telecommunication Engineering student, Pillai College of Engineering
[LinkedIn](https://www.linkedin.com/in/netra-puranik) | [GitHub](https://github.com/netra-p)
