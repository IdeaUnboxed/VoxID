# VoxID
========

Real-time AI-powered callsign recognition for amateur radio operators.\
Designed for noisy bands, inconsistent phonetics, heavy accents, and operators who benefit from visual decoding support.

* * * * *

**Overview**
------------

Ham radio audio is rarely clean. QRM, QRN, compression artifacts, fast talkers, and regional accents all make callsign recognition harder than it should be.\
**callsign-cather** listens to radio audio, extracts probable callsigns, and displays them with timestamps---live and local.

Feed it audio through a Signalink or any line-in device.\
It runs the speech-to-text engine locally (Whisper or Vosk), parses callsigns, ranks them, and presents them in a clear terminal interface.

No cloud. No guessing. No noise-free expectations.

* * * * *

**Features**
------------

-   Real-time callsign recognition

-   Works with typical SSB/FM/AM narrowband audio

-   NATO + non-NATO phonetic handling

-   Noise-tolerant STT (Whisper/Vosk)

-   Runs on desktop or embedded SBC (Raspberry Pi, etc.)

-   Terminal-style display with timestamps and confidence scores

-   Fully offline operation

* * * * *

**Why It Exists**
-----------------

Operators frequently struggle with callsign comprehension due to:

-   High noise floor

-   Fast exchanges and poor mic discipline

-   Strong accents or inconsistent phonetics

-   Cognitive load, fatigue, or audio-processing delays

-   Weak-signal HF conditions

This tool offloads pattern recognition to software so the operator can focus on the QSO.

* * * * *

**How It Works**
----------------

`[RF Audio] → [Audio Interface] → [STT Engine] → [Callsign Parser] → [Terminal Display]`

### **Audio Ingestion**

Continuous stream from USB audio interface (Signalink or equivalent).

### **Speech-to-Text**

Local Whisper (recommended) or Vosk engine.\
Optimized for narrowband and noisy audio.

### **Callsign Extraction**

-   ITU prefix-aware pattern matching

-   Phonetic mapping

-   Confidence scoring

-   Multiple candidates ranked in real time

### **Display Layer**

-   Terminal-friendly output

-   Time-stamped hits

-   Recent-history scrollback

* * * * *

**Hardware Requirements**
-------------------------

-   HF/VHF/UHF radio

-   Audio interface (Signalink USB or similar)

-   PC (Linux/Windows) or SBC (Raspberry Pi 4+)

-   Optional: dedicated display for standalone "blackbox"

* * * * *

**Software Requirements**
-------------------------

-   Python 3.9+

-   Whisper or Vosk

-   RNNoise (optional noise filtering)

-   ITU prefix database (included in repo)

* * * * *

**Installation**
----------------

(Replace with final commands once directory structure is in place.)

`git clone https://github.com/<yourname>/callsign-cather.git
cd callsign-cather
pip install -r requirements.txt`

Run the prototype:

`python src/cather.py`

* * * * *

**Project Status**
------------------

Active development.\
Desktop prototype functional; embedded SBC build under evaluation.

Contributions, test audio samples, and bug reports are welcome.

* * * * *

**Roadmap**
-----------

1.  **Core Pipeline** -- Audio → STT → callsign extraction

2.  **Noise Handling** -- Integrate RNNoise + tuned Whisper models

3.  **UI Layer** -- Clean terminal view, scrollback buffer

4.  **Embedded Build** -- Raspberry Pi version

5.  **Field Tests** -- Nets, DX, contests, weak-signal

6.  **Performance Tuning** -- Latency, CPU usage, accuracy

Full project details are available in the PRD.

* * * * *

**License**
-----------

MIT (or your preferred license --- update as needed).

* * * * *

**Contributing**
----------------

Pull requests are welcome.\
Audio samples must contain legal amateur-band content only.
