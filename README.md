Download Link: https://assignmentchef.com/product/solved-cs2261-lab10-sound
<br>
In this lab, you will be modifying the attached project to play sounds correctly. You will be editing the code that pauses, stops, and loops sound. <em>Please make sure to check the recitation video from 4/6 for a tutorial on how to convert .mp3 to .wav files.</em>

<strong>TODO 1 – Convert sound files</strong>

You will need to convert the attached sound files to be the correct .wav format using Audacity. Then, you will convert the .wav files to .c and .h files by building your project with the new Makefile and tasks.json file.

<ul>

 <li><strong>Formating the .wav file</strong></li>

</ul>

<em>Please note that these steps may slightly vary for different versions of Audacity.</em>

<ul>

 <li>Open .wav audio files in Original folder in Audacity</li>

</ul>

<strong>○ </strong>Select the track

<strong>○ </strong>Select Tracks -&gt; Stereo Track to Mono

<strong>○ </strong>Set the Project Rate (Hz) in the lower-left corner of the screen to 11025

<strong>○ </strong>Go to Tracks -&gt; Resample and choose 11025 as the new sample rate

<strong>○ </strong>Select File -&gt; Export Audio

<strong>○ </strong>Be sure to save it in your lab folder where the rest of your .c and .h files are

<strong>○ </strong>Under the “Save as type” dropdown, select Other uncompressed files

<strong>■ </strong>If there is a button for “options,” press the button

<strong>■ </strong>You should see dropdown menus for “Header” and “Encoding”

<strong>■ </strong>Set Header to “WAV (Microsoft)”

<strong>■ </strong>Set Encoding to “Unsigned 8-bit PCM”

<strong>■ </strong>Type “.wav” after your file name (for example, gameSong.wav)

<strong>■ </strong>When the Edit Metadata screen pops up, press the Clear button then hit OK

<ul>

 <li><strong>Converting the .wav file</strong>

  <ul>

   <li>Ensure you’re using the new Makefile and tasks.json provided in the lab zip. <strong>MOVING FORWARD, you will need to use the new Makefile and</strong></li>

  </ul></li>

</ul>

<strong>tasks.json in ALL FUTURE ASSIGNMENTS.</strong>

○ As in Lab00, update your tasks.json on line 9 to include your emulator exact path.

■ This will be the same path you have used for previous projects

○ Given that your .wav files you created from the previous step are in the SAME directory as your Makefile and other .c files, BUILD YOUR PROJECT NOW. It will not actually compile, which is fine, but you should see .c and .h files created for your .wav files once the build command finished.

<ul>

 <li>TODO 1.1

  <ul>

   <li>Include the sound .h files produced in the previous step at the top of main.c.</li>

  </ul></li>

</ul>

○ Build your project. No sound should be playing (since we haven’t implemented that yet), but you should see Rosie from Animal Crossing taking a nap on a bench &#x1f642;

■ If you run into any issues when you build your project, you can

“clean” your project, then build again. To do this in VSCode, go to Terminal &gt; Run Task and select “clean.” Then, build as normal.

<strong>TODO 2 – Complete the playSound functions</strong>

<ul>

 <li>TODO 2.1

  <ul>

   <li>Navigate to the playSoundA function in sound.c. This is the function we will use to tell our game to start playing a sound, so let’s complete it.</li>

  </ul></li>

</ul>

○ Assign all of soundA’s appropriate struct values.

■ soundA is declared in sound.h. You can find the SOUND struct in myLib.h.

■ data, length, and loops are assigned values passed in through the function.

■ isPlaying should be equivalent to “true,” since when we call this function we want a sound to start playing.

■ The duration formula is ((VBLANK_FREQ*length) /

SOUND_FREQ)

■ We can ignore priority, as it is not necessary for this lab. ■ vBlankCount should start at 0.

<ul>

 <li>TODO 2.2

  <ul>

   <li>Complete playSoundB with the same logic as playSoundA (these functions will be almost identical).</li>

  </ul></li>

</ul>

○ At this point, your code should build, but you won’t hear any sound.

<strong>TODO 3: Complete the interrupt handler</strong>

<ul>

 <li>TODO 3.1

  <ul>

   <li>Navigate to the setupInterrupts function in sound.c. Set up the interrupt handler register. The interrupt handler register is a macro that can be found in myLib.h and should point to the interruptHandler <em>function</em>.</li>

  </ul></li>

 <li>TODO 3.2

  <ul>

   <li>Handle soundA playing in the interruptHandler function.</li>

  </ul></li>

</ul>

■ This is where we want to determine if we need to stop playing soundA or not.

■ First, increment the sound’s vBlankCount.

■ Then, if the sound’s vBlankCount is greater than the song’s duration, we know we’ve reached the end of the song. You need to handle two cases here:

<ul>

 <li>If the sound loops, restart the song.</li>

 <li>If the sound does not loop, set the sound playing to false, turn off the DMA channel the sound is using, and turn off the timer the sound is using. Looking at the playSoundA function will be helpful here.</li>

 <li>TODO 3.3

  <ul>

   <li>Handle soundB playing in the interruptHandler function. This will be extremely similar to TODO 3.2.</li>

  </ul></li>

 <li>TODO 3.4

  <ul>

   <li>Call the two setup functions for sounds and interrupts in main.c. At this point, your code should build and start playing and looping music on the start screen! If it does not, take a closer look at your sound and interrupt functions.</li>

  </ul></li>

</ul>

○ Wait for the start song to loop and make sure you do not hear “Cornerface screaming at you”, aka your game playing random bits of memory that will make a screeching noise. This means you are not correctly stopping your sounds in the interruptHandler function.

<strong>TODO 4 – Pausing, unpausing, and stopping music</strong>

We want to be able to control when our music plays and when it doesn’t, so we have three functions to handle this in sound.c.

<ul>

 <li>TODO 4.1

  <ul>

   <li>Complete the pauseSound function. To pause a sound, we want to set soundA</li>

  </ul></li>

</ul>

and soundB playing to false and stop their timers.

<ul>

 <li>TODO 4.2

  <ul>

   <li>Complete the unpauseSound function. To unpause a sound, we want to reverse the changes made in TODO 4.1.</li>

  </ul></li>

</ul>

■ HINT: check out the timer flags in myLib.h.

<ul>

 <li>TODO 4.3

  <ul>

   <li>Complete the stopSound function. Completely stop soundA and soundB. This should be very similar to some of the code you wrote in TODO 3.2 and TODO</li>

  </ul></li>

</ul>

3.3.

○ At this point your code should build, but as we have not called any of these functions yet, you will not notice any changes.

<strong>TODO 5 – Set up more sounds!</strong>

Now that we have everything in place to play sounds, we can add more to our game.

<ul>

 <li>TODO 5.1

  <ul>

   <li>Play the gameSong music when the player presses START to transition from the start to game state.</li>

  </ul></li>

</ul>

■ Call stopSounds first, in case any songs are currently playing. ■ Make sure that the gameSong loops!

<ul>

 <li>TODO 5.2

  <ul>

   <li>Pause the music when transitioning from game to pause screen. ■ HINT: We wrote a function that does exactly this.</li>

  </ul></li>

 <li>TODO 5.3

  <ul>

   <li>Play the sfxSound and loseSong in goToLose</li>

  </ul></li>

</ul>

■ Call stopSounds first, in case any songs are currently playing.

■ Make sure that the loseSong loops and that the sfxSound do NOT loop!

■ Make sure that the sfxSound does not interrupt the loseSong (should play on a different channel)

<ul>

 <li>TODO 5.4

  <ul>

   <li>Unpause the music when transitioning from pause to game screen. ■ Hint: We wrote another function that also does exactly this.</li>

  </ul></li>

</ul>

At this point, you should be done! Check that your lab meets all of the requirements below.

<strong>You will know if it runs correctly if you:</strong>

<ul>

 <li>Have the following behavior in each state:

  <ul>

   <li>START</li>

  </ul></li>

</ul>

■ A looping start song plays

○ GAME

■ A looping game song plays

■ The game song is paused when going to pause screen

■ The game song is stopped sound when going back to the start screen and the start song begins to play

○ PAUSE

■ Sprites from the game state are hidden

■ The game song is unpaused when returning to the game screen

○ LOSE

■ A looping lose song plays

■ A NON-looping sfx sound plays

■ Both sounds are stopped when going back to the start screen and the start song begins playing

<h1>Tips</h1>

<ul>

 <li>Review recitation materials: Canvas &gt; Recitation Materials</li>

 <li>Review the videos on how to convert .mp3 files to .wav files: Canvas &gt; Pages &gt; Lecture/Recitation Recordings (Monday Lecture and Tuesday Recitation)</li>

</ul>