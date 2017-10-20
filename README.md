## Introduction  
Codebeat is a javascript library that provides a simple language for music composition.

### Note duration
A note's duration is the relative amount of time it is played, known as a subdivision.
The names of common subdivisions are abbreviated as follows:

* ts = thirty-second  
* s = sixteenth  
* s. = dotted-sixteenth  
* t = triplet  
* e = eighth  
* e. = dotted-eighth    
* q = quarter  
* q. = dotted-quarter  
* h = half  
* h. = dotted-half   
* w = whole
* w. = dotted-whole   

_Note: 3 triplets = 2 eighths_

### Note pitch
A note's pitch is the name for its frequency in Hertz. D in the 5th octave is written as `d5`. Similarly, G-flat in the 3rd octave is `g_3`, and C-sharp in the 6th octave is `c#6`. A pitch can be between `a0` and `g#7`, inclusive.

### Basic notation
General format: `[note_duration][space][note_pitch][comma]`   
In practice: `h d5, q g_3, q c#6` etc.

_Note: any amount of tabs, newlines, or whitespace can appear after the comma, but not between the duration and pitch_  

### Repetition
To simplify the writing process, groups of notes may be assigned to variables (separated with a semicolon) and repeated notes may be multiplied by an integer value.

1) Variable assignment
~~~
motif = h d5, q g_3, q c#6;
t d4, motif,
t a4, motif
~~~
2) Repeat single notes
~~~
h c4 * 8, t b_3 * 3
~~~

### Chords
To play multiple notes simultaneously, Codebeat provides the `+` operator. Doing so produces a chord constituted of the pitches provided for the specified duration. The notes within a chord must be played for the same duration.

~~~
chord = h d3 + a3 + g3;

h d3, chord,
h a3, chord
~~~

### Slides
Like physical instruments, Codebeat can alter the pitch of a note over time until it reaches a second pitch. This is done with the `-` operator. Both notes are independent of each other, which means they may be any of the allowed durations and pitches.

~~~
slide = h e2 - z c3;

e f3, slide,
h b3, slide
~~~

## Usage  
1) Import:
~~~
const Codebeat = require('Codebeat')
~~~
2) Pass in a melody object:  
~~~
const melody = new Codebeat({  
   tempo: 128,                                            //default is 60
   instrument: 'square',                                  //default is 'sine'
   timeSig: '3/4',                                        //default is '4/4'
   notes: 't d4, t d_4, t d4, q a#5, q b5, q rest, w e4', //default is an empty string
   loop: true                                             //default is false  
})
~~~

_Note: Up to six audio contexts can be active on the window object. Each instance of Codebeat creates a new context._

3) Read more about available methods here: https://blmgeo.github.io/Codebeat/out/Codebeat.html
