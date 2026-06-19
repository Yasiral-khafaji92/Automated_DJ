# Automated DJ System 🎵

## Overview

This project implements an automated DJ audio analysis pipeline for detecting musical structure and generating smooth transitions between songs.

The system analyzes audio signals to extract rhythm, energy, and structural information, then uses this information to select suitable transition points and create crossfade mixes.

---

## Main Features

### 1. Audio Feature Extraction

The system extracts multiple audio features:

- **Onset Strength**
  - Detects new musical events and sudden changes in the audio.

- **RMS Energy**
  - Represents the loudness and energy variation over time.

- **MFCC**
  - Captures timbral characteristics and sound texture.

- **Spectral Flux**
  - Measures changes in frequency content.

The extracted features are aligned and combined using weighted fusion to create an overall energy representation.

---

## 2. Rhythm Analysis

The system estimates:

- Tempo (BPM)
- Beat positions
- Downbeats positions
- Bar structure


Beat tracking is performed using the onset strength representation instead of the raw signal to improve rhythm detection.

The detected beats and Downbeats are used to estimate bars and musical phrases.

---

## 3. Structural Boundary Detection

The project uses Self-Similarity Matrix (SSM) analysis:

- MFCC similarity captures timbral changes
- RMS similarity captures energy changes

A checkerboard kernel is applied to the SSM to calculate novelty curves

The final novelty curve combines:

- Timbre novelty
- Energy novelty

Peak detection is then applied to identify possible structural changes, define song segments, and detect musical phrase boundaries. 

---

## 4. Phrase Boundary Alignment

Detected structural peaks are aligned with the musical grid.

The algorithm:

- Maps detected peaks to bar positions
- Removes unstable boundaries
- Searches for the dominant 8-bar structure
- Snaps boundaries to valid musical positions

The result is a set of phrase boundaries.

---
#### Transition Testing and Crosfade generation between two songs Based on Bar Energy 

## 5.This module is implemented to test transitions between two songs and verify the alignment of detected downbeats and bars

The system compares bars between two songs:

- Searches transition candidates in the end of the first song and beginning of the second song
- Compares bar energy values
- Selects the pair with the smallest energy difference

If no suitable pair is found, a fallback transition position is used.

---

## 6. Crossfade Generation

After selecting the best transition bars:

- Fade duration is calculated based on tempo and bar length
- Cosine and sine fade curves are generated
- The first song fades out
- The second song fades in
- Both parts are smoothly mixed

The final output is a continuous mixed audio track.

---


