# kbd-audio [![Build Status](https://travis-ci.org/ggerganov/kbd-audio.svg?branch=master)](https://travis-ci.org/ggerganov/kbd-audio?branch=master)

## Description

This is a collection of command-line and GUI tools for capturing and analyzing audio data.

### Keytap

The most interesting tool is called **keytap** - it can guess pressed keyboard keys only by analyzing the audio captured from the computer's microphone.

Check this blog post for more details:

[Keytap: description and some random thoughts](https://ggerganov.github.io/jekyll/update/2018/11/30/keytap-description-and-thoughts.html)

[Video: short demo of Keytap in action](https://www.youtube.com/watch?v=2OjzI9m7W10)

### Keytap2

The **keytap2** tool is another interesting tool for recovering text from audio. It does not require training data - instead it uses statistical information about the frequencies of the letters and n-grams in the English language. The tool is still in development, but you can see a short demonstration here:

[Video: Keytap2 - recovering text from typing sound (7:50)](https://www.youtube.com/watch?v=Y8nWkdWl7Pg)

[CTF: can you guess the text being typed?](https://ggerganov.github.io/keytap-challenge/)

## Build instructions

Dependencies:

 - **SDL2** - used to capture audio and to open GUI windows [libsdl](https://www.libsdl.org)
       
       [Ubuntu]
       $ sudo apt install libsdl2-dev
       
       [Mac OS with brew]
       $ brew install sdl2  
       
 - **FFTW3** *(optional)* - some of the helper tools perform Fourier transformations [fftw](http://www.fftw.org)

**Linux and Mac OS**

    git clone https://github.com/ggerganov/kbd-audio
    cd kbd-audio
    git submodule update --init
    mkdir build && cd build
    cmake ..
    make

**Windows**

    (todo, PRs welcome)

## Tools

Short summary of the available tools. If the status of the tool is not **stable**, expect problems and non-optimal results.

| Name                | Type    | Status      |
| ---                 | ---     | ---         |
| **record**          | text    | **stable**  |
| **record-full**     | text    | **stable**  |
| **play**            | text    | **stable**  |
| **play-full**       | text    | **stable**  |
| **view-gui**        | gui     | **stable**  |
| **view-full-gui**   | gui     | **stable**  |
| **keytap**          | text    | **stable**  |
| **keytap-gui**      | gui     | **stable**  |
| **keytap2**         | text    | development |
| **keytap2-gui**     | gui     | development |
| -                   | *extra* | -           |
| **guess_qp**        | text    | experiment  |
| **guess_qp2**       | text    | experiment  |
| **key_detector**    | text    | experiment  |
| **scale**           | text    | experiment  |
| **subreak**         | text    | experiment  |
| **key_average_gui** | gui     | experiment  |

## Tool details

* **record-full**

  Record audio to a raw binary file on disk

      ./record-full output.kbd [-cN]

  ---

* **play-full**

  Playback a recording captured via the **record-full** tool

      ./play-full input.kbd [-pN]

  ---

* **record**

  Record audio only while typing. Useful for collecting training data for **keytap**

      ./record output.kbd [-cN]

  ---

* **play**

  Playback a recording created via the **record** tool

      ./play input.kbd [-pN]

  ---

* **keytap**

  Detect pressed keys via microphone audio capture in real-time. Uses training data captured via the **record** tool.

      ./keytap input0.kbd [input1.kbd] [input2.kbd] ... [-cN] [-pF] [-tF]

  ---

* **keytap-gui**

  Detect pressed keys via microphone audio capture in real-time. Uses training data captured via the **record** tool. GUI version.

      ./keytap-gui input0.kbd [input1.kbd] [input2.kbd] ... [-cN]

  [**Live demo *(WebAssembly threads required)* **](https://ggerganov.github.io/jekyll/update/2018/11/24/keytap.html)

  <a href="https://i.imgur.com/mnRvT1X.gif" target="_blank">![keytap-gui](https://i.imgur.com/FXa60Pr.gif)</a>

  ---

* **keytap2-gui** *(work in progress)*

  Detect pressed keys via microphone audio capture. Uses statistical information (n-gram frequencies) about the language. **No training data is required**. The *'recording.kbd'* input file has to be generated via the **record-full** tool and contains the audio data that will be analyzed. The *'n-gram.txt'* file has to contain n-gram probabilities for the corresponding language. 

      ./keytap2-gui recording.kbd n-gram.txt

  <a href="https://i.imgur.com/LRnTkPA.jpg" target="_blank">![keytap2-gui](https://i.imgur.com/LRnTkPA.jpg)</a>

  ---

* **view-full-gui**

  Visualize waveforms recorded with the **record-full** tool. Can also playback the audio data.

      ./view-full-gui input.kbd

  <a href="https://i.imgur.com/scjTaXw.png" target="_blank">![view-full-gui](https://i.imgur.com/scjTaXw.png)</a>

  ---

* **view-gui**

  Visualize training data recorded with the **record** tool. Can also playback the audio data.

      ./view-gui input.kbd

  <a href="https://i.imgur.com/2binGaZ.png" target="_blank">![view-full-gui](https://i.imgur.com/2binGaZ.png)</a>

  ---

## Feedback

Any feedback about the performance of the tools is highly appreciated. Please drop a comment [here](https://github.com/ggerganov/kbd-audio/issues/3).
