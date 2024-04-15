# CX Class 16.04.2024 "Experiments with Web-based Audio"
Bela Usabaev, speech synthesis, media art, web-based applications

Eleni-Ira Panourgia, Postdoctoral Researcher, sound and visual art, web art, interactive applications, sound and climate change

## Introduction to the workshop
- What is Web Audio?
- ClimaSynth web application - a case study
- Hands-on experimentation with ClimaSynth and testing: https://ctechfilmuniversity.github.io/project_ClimaSynth/

<img src="https://github.com/xy-grainsynth/xy-prototype/assets/115570643/34b7190e-8a4f-4ede-9a6f-cfd78e3b5bac"  width="200" height="200">

## Practical session: creating a mini web synth
1. create index.html, load p5 and tweakpane library, add css stylesheet, test in VS studio code, check for errors using the console output [Step 1](https://github.com/xy-grainsynth/workshop/tree/3e2b8b6582ee4d3fdd18285555bde1f1e51077b2)
2. set up p5 sketch and web audio
   1. create js/Step2/main.js file in VS Studio Code
   2. in main.js create p5 sketch with setup() and draw()
     ```
     function setup() {

     }

     function draw() {
     
     }
     ```
     setup() is called to initialize the p5 sketch, draw() is called at every frame
   3. in setup() create a p5 canvas the same size as the browser window
     ```
     canvas = createCanvas(windowWidth, windowHeight);
     ```
   4. in setup() tie the canvas to canvasContainer html node
     ```
     canvas.parent("canvasContainer");
     ```
   5. declare audio context at the top of the main script
     ```
     var ctx, master;
     ctx = new (window.AudioContext || window.webkitAudioContext);
     master = ctx.createGain();
     master.connect(ctx.destination);
     ```
   6. in draw() fetch mouse position and define when sound generation is triggered
     ```
     posX = mouseX;
     posY = mouseY;
     if (posX > 0 && posX < windowWidth && posY > 0 && posY < windowHeight) {
        if (mouseIsPressed) {
     
        }
     }
     ```
3. sourcing own recordings .wav format max. duration 1 minute (think of a sound that would be interesting to use for transitions from natural to extreme/unfamiliar state) Search on [BBC Sound Effects](https://sound-effects.bbcrewind.co.uk/search?q=nature&resultSize=30) or other open-access libraries
   1. save at least two recordings in the folder recordings in the project directory
4. setup a tweakpane GUI to load the recordings into the script
   1. create js/gui.js
   2. define tweakpane params and set up tweakpane gui
   3. connect tweakpane param source value to recording
   4. call buffer loading function bufferswitch()
5. load recording into audio buffer
   1. define audiobuffer at the top of main.js
   ```
   var audiobuffer;
   ```
   2. write bufferswitch() buffer loading function in gui.js
   ```
   function bufferSwitch(input) {
    var getSound = new XMLHttpRequest();  // create a new xml http request
    ... // we are expecting an array buffer

     if (input == 0) {
      // getSound.open(name of audio file);
     }

     getSound.onload = function () {
      // upon loading recording by xml http request, load xml http response buffer as web audio context buffer
      ctx.decodeAudioData(getSound.response, function(buffer){
        ... // load buffer into web audio context buffer
        });
     }

     getSound.send(); // send buffer response
   }
   ```
   3. call bufferswitch in setup() in main.js to initialize audiobuffer upon start up
   4. test using the GUI and the console  
6. suspend audio context upon definition and add start/stop button to control audio context in the GUI
   1. in main.js suspend audio context after initialization
   2. in gui.js add tweakpane button to suspend and resume the web audio context
7. grains generator
   1. grains are generated when the mouse is pressed
   ```
   function mousePressed(){
      ... // start generating grains
   }
   ```
   2. dispose of the generated grains when the mouse is released
   ```
   function mouseReleased(){
      ... // delete the grains generated sind the mouse got pressed
   }
   ```
   3. array to hold the generated grains
   ```
   var voice = [];
   ```
   4. generate grains at where the mouse is at position x,y
   ```
   function graingenerator(positionX, positionY){
   this.grain = ctx.createBufferSource();
   this.grain.buffer = audioBuffer;
   this.contour = ctx.createGain();
   this.contour.connect(master);
   }
   ```
   5. define the grain envelope and start and stop grain
   ```
   this.grain.start(ctx.currentTime, Math.max(0.0, this.offset + this.randomoffset));
   this.contour.gain.setValueAtTime(0.0, ctx.currentTime);
   this.contour.gain.linearRampToValueAtTime(this.amp, ctx.currentTime + attack);
   this.contour.gain.linearRampToValueAtTime(0.0, ctx.currentTime + (attack + release));
   this.grain.stop(ctx.currentTime + attack + release + 0.1);
   ```
   6. the offset is obtained from x mouse position, random offset is obtained based on spread
   7. add panner node
   8. amplitude is based on x mouse position
   9. garbage collection: dispose of panner node and gain contour
   10. add feedback delay effect to the grain
8. enhance the GUI to control the granular synth parameters
   - tweakpane library
   - grain param monitors
9. test/play with the built synth, and define a sound that associates with a climate condition, defining associations with climate scenarios
