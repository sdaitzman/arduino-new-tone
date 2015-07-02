# NewTone Arduino Library #

## Features ##
About 1,200 bytes smaller code size than the standard tone library.
Faster execution time.
Exclusive use of port registers for fastest and smallest code.
Higher quality sound output than tone library.
Plug-in replacement for Tone.
Uses timer 1 which may free up conflicts with the tone library.

## Download ##
**[Download NewTone v1.0](http://code.google.com/p/arduino-new-tone/downloads/list)**

## Show Your Appreciation ##
Help future development by making a small donation (yes, the FreeRingers payee is correct).<br>
<a href='https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MQGEFBJLK2YVU'><img src='https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif' /></a>

<h2>Syntax</h2>
<ul><li><b>NewTone( pin, frequency <code>[, length ]</code> )</b> - Play a note on pin at frequency in Hz.<br>
<ul><li><b>pin</b> - Pin speaker is wired to (other wire to ground, be sure to add an inline 100 ohm resistor).<br>
</li><li><b>frequency</b> - Play the specified frequency indefinitely, turn off with noNewTone().<br>
</li><li><b>length</b> - <code>[optional]</code> Set the length to play in milliseconds. (default: 0 <code>[forever]</code>, range: 0 to 2^32-1)<br>
</li></ul></li><li><b>noNewTone(pin)</b> - Stop playing note (pin is optional, will always stop playing on pin that was last used).</li></ul>

<h2>Example</h2>
<pre><code>#include &lt;NewTone.h&gt;<br>
<br>
#define TONE_PIN 2 // Pin you have speaker/piezo connected to (be sure to include a 100 ohm resistor).<br>
<br>
// Melody (liberated from the toneMelody Arduino example sketch by Tom Igoe).<br>
int melody[] = { 262, 196, 196, 220, 196, 0, 247, 262 };<br>
int noteDurations[] = { 4, 8, 8, 4, 4, 4, 4, 4 };<br>
<br>
void setup() {} // Nothing to setup, just start playing!<br>
<br>
void loop() {<br>
  for (unsigned long freq = 125; freq &lt;= 15000; freq += 10) {  <br>
    NewTone(TONE_PIN, freq); // Play the frequency (125 Hz to 15 kHz sweep in 10 Hz steps).<br>
    delay(1); // Wait 1 ms so you can hear it.<br>
  }<br>
  noNewTone(TONE_PIN); // Turn off the tone.<br>
<br>
  delay(1000); // Wait a second.<br>
<br>
  for (int thisNote = 0; thisNote &lt; 8; thisNote++) { // Loop through the notes in the array.<br>
    int noteDuration = 1000/noteDurations[thisNote];<br>
    NewTone(TONE_PIN, melody[thisNote], noteDuration); // Play thisNote for noteDuration.<br>
    delay(noteDuration * 4 / 3); // Wait while the tone plays in the background, plus another 33% delay between notes.<br>
  }<br>
<br>
  while(1); // Stop (so it doesn't repeat forever driving you crazy--you're welcome).<br>
}<br>
</code></pre>

<h2>History</h2>
<b>01/20/2013 v1.0</b> - Initial release.