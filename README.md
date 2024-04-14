# CX Class 16.04.2024 "Experiments with Web-based Audio"
Bela Usabaev, speech synthesis, media art, web-based applications

Eleni-Ira Panourgia, Postdoctoral Researcher, sound and visual art, web art, interactive applications, sound and climate change

## Introduction to the workshop
- What is Web Audio?
- ClimaSynth web application - a case study
- Hands-on experimentation with ClimaSynth and testing: https://ctechfilmuniversity.github.io/project_ClimaSynth/

<img src="https://github.com/xy-grainsynth/xy-prototype/assets/115570643/34b7190e-8a4f-4ede-9a6f-cfd78e3b5bac"  width="200" height="200">

## Practical session: creating a mini web synth
1. index.html, loading p5 library [Step 1](https://github.com/xy-grainsynth/xy-prototype/tree/d4e836bfcaada67980dc523e0724686a8003cfb3/js)
2. p5 framework and web audio
   - p5 sketch stub and web audio context definition
3. defining/setting gain, connecting to master output
4. sourcing own recordings .wav format max. duration 1 minute (think of a sound that would be interesting to use for transitions from natural to extreme/unfamiliar state) Search on [BBC Sound Effects](https://sound-effects.bbcrewind.co.uk/search?q=nature&resultSize=30) or other open-access libraries
5. sounds laden/defining and loading buffers
6. connection between web audio und canvas
7. grains generator: how are the granulator work
   - example stub
   - continue adding one effect and exposing the value to test it 
8. setting up a GUI to control the web audio context and expose the granular synth parameters
   - tweakpane library
   - grain param monitors
9. test/play with the built synth, and define a sound that associates with a climate condition, defining associations with climate scenarios