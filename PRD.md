**PROJECT REQUIREMENTS DOCUMENT (PRD)**\
**AI--HAM RADIO INTEGRATION:**\
**CALLSIGN RECOGNITION SYSTEM**
==================================================================================================

**1\. Executive Summary**
-------------------------

Operators frequently struggle with accurate callsign recognition due to noise, accents, inconsistent phonetics, and cognitive processing delays. The goal is to build a system that listens to radio audio, extracts possible callsigns in real time, and displays them clearly. The platform may run on a general-purpose computer connected via audio interface (e.g., Signalink) or a dedicated embedded device.

This is not meant to be a "smart assistant"---it's a focused signal-to-text tool engineered for reliability under imperfect conditions.

* * * * *

**2\. Problem Definition**
--------------------------

Current ham radio operation assumes clean audio and perfect human decoding. Reality disagrees:

-   Noise floor and RF interference bury syllables.

-   Operators use inconsistent phonetics or none at all.

-   Accents, speed, mumbling, old microphones, and compression cripple intelligibility.

-   Dyslexia and audio-processing delays extend the cognitive load.

The result: missed callsigns, slower exchanges, higher mental fatigue, and reduced QSO quality.

A system that visually displays probable callsigns removes unnecessary cognitive load and reduces error rates.

* * * * *

**3\. Goals & Non-Goals**
-------------------------

### **Goals**

-   Real-time detection of probable callsigns from audio.

-   Operates with typical ham-radio noise and audio compression.

-   Clear, unambiguous display of recognized callsigns.

-   Continuous listening with minimal operator intervention.

-   Modular enough to run on:

    -   PC + Signalink

    -   Embedded SBC "black box" (e.g., Raspberry Pi, ESP32-S3 with coprocessor)

### **Non-Goals**

-   Not a complete speech-to-text engine.

-   Not meant to violate ham-radio ethics (no unattended operation beyond passive monitoring).

-   Not for decoding encrypted, digital, or prohibited content.

-   Not intended to replace the operator---this is an assistive tool.

* * * * *

**4\. User Stories**
--------------------

1.  **As an operator**, I want the system to highlight detected callsigns so I can respond correctly without guessing.

2.  **As a dyslexic user**, I want the system to reduce my audio-processing burden by presenting text cleanly.

3.  **As a field operator**, I want low-latency recognition so I don't miss a turn in the exchange.

4.  **As a tinkerer**, I want the system to work with existing gear like the Signalink without requiring modifications.

* * * * *

**5\. Use Cases**
-----------------

-   Rapid-fire contesting where accents and speed cripple recognition.

-   Local simplex nets where operators rarely use proper NATO phonetics.

-   HF DXing where weak-signal conditions bury syllables.

-   Mobile operation with high background noise (car, wind, generator).

* * * * *

**6\. System Overview**
-----------------------

The system ingests audio > processes it > extracts probable callsigns > displays them.

Pipeline:

`RF Audio → Audio Interface → AI/STT Engine → Callsign Parser → Display Module`

Modules:

1.  **Audio Capture Layer**

    -   Continuous streaming from audio interface.

    -   Optional noise reduction.

2.  **Speech-to-Text Engine**

    -   Local (Whisper, Vosk) or remote (if allowed).

    -   Tuned for narrowband audio profiles.

3.  **Callsign Extraction Logic**

    -   Regex-based detection for known callsign structures.

    -   Phonetic-mapped dictionary of NATO + non-standard phonetics.

    -   Confidence scoring and ranking.

4.  **Presentation Layer**

    -   Terminal-style display.

    -   Shows top matches + confidence + timestamps.

* * * * *

**7\. Functional Requirements**
-------------------------------

### **Audio Processing**

-   Must accept 600--3000 Hz SSB-style audio.

-   Minimum sampling 8 kHz (16 kHz preferred).

-   Auto-gain or clipping detection.

### **Speech Recognition**

-   Must identify alphanumerics spoken with noise and accents.

-   Must operate at <1.2 seconds end-to-display latency.

-   Should detect known call patterns (e.g., "PJ2XX", "K1ABC").

### **Callsign Parsing**

-   Must use ITU call area patterns.

-   Should handle NATO and non-NATO phonetics.

-   Should recover partial calls (e.g., "Kilo something Alpha").

### **Display**

-   Must list candidates chronologically.

-   Should highlight high-confidence matches.

-   Should allow operator to review last 30--60 seconds.

* * * * *

**8\. Non-Functional Requirements**
-----------------------------------

-   **Performance:** Low latency, real-time operation.

-   **Reliability:** Must tolerate noisy, inconsistent input.

-   **Portability:** Should run on Linux, Windows, or embedded SBCs.

-   **Privacy:** No logging unless enabled.

-   **Offline Capability:** Preferred---especially for field use.

* * * * *

**9\. Architecture Overview**
-----------------------------

### **Option A: PC-Based Architecture**

-   Windows/Linux machine

-   Signalink USB audio interface

-   Whisper/Vosk running locally

-   Python/C++ service + frontend

### **Option B: Embedded Blackbox**

-   Raspberry Pi 4 or similar

-   USB audio interface or direct ADC

-   On-device Whisper Tiny/Small model

-   Minimal terminal or small OLED display

Tradeoffs:

-   PC gives higher accuracy and lower dev friction.

-   SBC gives portability but tighter CPU/memory constraints.

* * * * *

**10\. Dependencies**
---------------------

### **Hardware**

-   Radio (HF/VHF/UHF)

-   Signalink or similar audio interface

-   PC or SBC

-   Optional display (OLED, small LCD)

### **Software**

-   Whisper or Vosk STT models

-   Python/C++ runtime

-   Noise filtering library (RNNoise or similar)

-   Callsign pattern DB (ITU prefixes, DXCC list)

* * * * *

**11\. Risks & Constraints**
----------------------------

-   HF noise and QRM may exceed model tolerance.

-   Whisper accuracy drops with severe noise unless pre-filtered.

-   Callsign formats vary globally---must maintain prefix database.

-   Embedded devices may struggle with Whisper models > Tiny.

-   Legal constraints: no automatic unattended transmitting.

* * * * *

**12\. Milestones / Roadmap**
-----------------------------

**Phase 1 --- Feasibility (1--2 weeks)**

-   Test Whisper and Vosk with actual radio clips.

-   Establish baseline accuracy.

**Phase 2 --- Prototype (2--4 weeks)**

-   Build audio → STT → regex pipeline on PC.

-   Basic terminal display with top callsigns.

**Phase 3 --- Field Testing (2 weeks)**

-   Live monitoring on HF and VHF nets.

-   Gather failure cases (accents, weak signals).

**Phase 4 --- Blackbox Option (4--8 weeks)**

-   Port to Raspberry Pi.

-   Optimize model execution.

**Phase 5 --- UX Refinement (1--2 weeks)**

-   Improve display.

-   Add logs, time markers, operator controls.

* * * * *

**13\. Success Criteria**
-------------------------

-   ≥85% correct detection under typical HF/VHF conditions.

-   <1.2 second recognition latency.

-   Handles non-standard phonetics with >70% accuracy.

-   Minimal operator interaction required.
