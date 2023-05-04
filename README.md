Download Link: https://assignmentchef.com/product/solved-csc230-assignment2-hardware-programming
<br>
This assignment covers a wide variety of hardware programming topics, including I/O, polling and interrupt handling. It also covers new assembly programming techniques, like the use of the call stack and interrupt flags. You should start as early as possible; this assignment will be virtually impossible to complete if you leave it to the last minute, especially since you will have to use the lab hardware to test your implementation.

The basic requirement of the assignment is to write an AVR assembly program which, when uploaded to the ATmega2560 board, produces a simple “back and forth” pattern on the 6 blue LED lights connected to pins 42, 44, 46, 48, 50 and 52. Beyond the basic animated pattern, you will also have to include support for simple user input with the 5 black buttons to receive full marks.

Your assignment will be marked during an interactive demo with a member of the CSC 230 teaching team. You will be graded on the function of your implementation, the quality of your code, and your ability to justify the implementation decisions you made.

Section 2 describes the animated pattern. Section 3 describes the required user input features, and Section 4 describes a set of additional enhancements (for 100%, you must implement at least one of these extra enhancements).

<h1>1              Animated Pattern</h1>

The pattern consists of 10 steps which repeat indefinitely. By default, the delay between steps will be 1 second (and your code should strive to achieve timekeeping as accurately as possible). The program may be set to one of two display modes. In ‘Regular Mode’, one LED is lit at each step and the lit LED sweeps back and forth across the shield. In ‘Inverted Mode’, five LEDs are lit, with one LED unlit, and the unlit LED sweeps back and forth across the shield.

To receive the initial set of marks for the ‘basic pattern’ (see Section 7), your implementation must be able to achieve, at minimum, the Regular Mode pattern with a 1 second delay. In the following sections, the term ‘step’ is used to refer to the individual steps of the pattern, and the term ‘transition’ is used to refer to the progression between two adjacent steps in the pattern (with the understanding that the pattern repeats indefinitely and wraps around to step 0 after step 9).

<table width="559">

 <tbody>

  <tr>

   <td width="449">


    <table width="447">

     <tbody>

      <tr>

       <td rowspan="3" width="46">Step</td>

       <td colspan="12" width="372"><strong>LEDs </strong>(by PIN number)</td>

       <td width="28"> </td>

      </tr>

      <tr>

       <td colspan="6" width="171">Regular Mode</td>

       <td width="60"> </td>

       <td colspan="5" width="141">Inverted Mode</td>

       <td width="28"> </td>

      </tr>

      <tr>

       <td width="30">52</td>

       <td width="28">50</td>

       <td width="28">48</td>

       <td width="28">46</td>

       <td width="28">44</td>

       <td width="28">42</td>

       <td width="60"> </td>

       <td width="28">52</td>

       <td width="28">50</td>

       <td width="28">48</td>

       <td width="28">46</td>

       <td width="28">44</td>

       <td width="28">42</td>

      </tr>

      <tr>

       <td width="46">0</td>

       <td width="30">•</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="60"> </td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

      </tr>

      <tr>

       <td width="46">1</td>

       <td width="30">◦</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="60"> </td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

      </tr>

      <tr>

       <td width="46">2</td>

       <td width="30">◦</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="60"> </td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

      </tr>

      <tr>

       <td width="46">3</td>

       <td width="30">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="60"> </td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">•</td>

      </tr>

      <tr>

       <td width="46">4</td>

       <td width="30">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="60"> </td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">•</td>

      </tr>

      <tr>

       <td width="46">5</td>

       <td width="30">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="60"> </td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">◦</td>

      </tr>

      <tr>

       <td width="46">6</td>

       <td width="30">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="60"> </td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">•</td>

      </tr>

      <tr>

       <td width="46">7</td>

       <td width="30">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="60"> </td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">•</td>

      </tr>

      <tr>

       <td width="46">8</td>

       <td width="30">◦</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="60"> </td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

      </tr>

      <tr>

       <td width="46">9</td>

       <td width="30">◦</td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="28">◦</td>

       <td width="60"> </td>

       <td width="28">•</td>

       <td width="28">◦</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

       <td width="28">•</td>

      </tr>

      <tr>

       <td colspan="13" width="418">After step 9, pattern repeats from step 0</td>

       <td width="28"> </td>

      </tr>

     </tbody>

    </table></td>

   <td width="109">


    <table width="107">

     <tbody>

      <tr>

       <td width="27"> </td>

       <td width="79"><strong>Legend</strong></td>

      </tr>

      <tr>

       <td width="27">•</td>

       <td width="79">= LED on</td>

      </tr>

      <tr>

       <td width="27">◦</td>

       <td width="79">= LED off</td>

      </tr>

     </tbody>

    </table></td>

  </tr>

 </tbody>

</table>

<h1>2              Required Inputs</h1>

As you saw in Lab 4, the LCD shield used on the AVR boards in ECS 249 has five general purpose black buttons (plus the RST button which is not easily programmable). You are required to implement the following behaviors for the UP, DOWN, LEFT and RIGHT buttons. Note that this section does not use the SELECT button, since that button is used for the extra features in Section 4.

<table width="561">

 <tbody>

  <tr>

   <td width="68"><strong>Button</strong></td>

   <td width="493"><strong>Behavior</strong></td>

  </tr>

  <tr>

   <td width="68">LEFT</td>

   <td width="493"><strong>Enable Inverted Mode</strong>: When the LEFT button is pressed, the program will <strong>immediately </strong>enter Inverted Mode and the set of lit LEDs will immediately reflect the inverted configuration for the current step of the pattern, as given by the table in Section 2. The change must take effect immediately (not at the beginning of the next step) to be correct<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>. If the button is pressed while Inverted Mode is already active, there is no effect (and the program remains in Inverted Mode).</td>

  </tr>

  <tr>

   <td width="68">RIGHT</td>

   <td width="493"><strong>Enable Regular Mode</strong>: When the RIGHT button is pressed, the program will <strong>immediately </strong>enter Regular Mode and the set of lit LEDs will immediately reflect the non-inverted configuration for the current step of the pattern, as given by the table in Section 2. The change must take effect immediately (not at the beginning of the next step) to be correct. If the button is pressed while Regular Mode is already active, there is no effect (and the program remains in Regular Mode).</td>

  </tr>

  <tr>

   <td width="68">UP</td>

   <td width="493"><strong>Change Delay to 0.25 Seconds</strong>: When the UP button is pressed, the delay between steps will become 0.25 seconds. If the delay is already set to 0.25 seconds, then pressing the UP button will have no effect (and the delay will remain at 0.25 seconds). The new timing must take effect at or before the next pattern transition.</td>

  </tr>

  <tr>

   <td width="68">DOWN</td>

   <td width="493"><strong>Change Delay to 1 Second</strong>: When the DOWN button is pressed, the delay between steps will become 1 second. If the delay is already set to 1 second, then pressing the DOWN button will have no effect (and the delay will remain at 1 second). The new timing must take effect at or before the next pattern transition.</td>

  </tr>

 </tbody>

</table>

<h1>3              Additional Enhancements</h1>

For full marks, you must implement one of the three finishing touches documented in Sections 4.1, 4.2 and 4.3 below. You are welcome to implement more than one (if feasible), but you cannot receive more than 100% on the assignment. If you have your own idea for an extra feature, you may be allowed to implement that instead of one of the items below, but you must get written permission from your instructor before the due date or you will not receive any marks for the feature.

<h2>3.1        Accelerate Mode</h2>

This feature uses the SELECT button to enable a third speed setting, in addition to the standard 1 second delay provided by the DOWN button and the 0.25 second delay provided by the UP button. If this feature is implemented, the behaviors of UP, DOWN and SELECT must follow the table below. The behavior of LEFT and RIGHT are unchanged.

<table width="561">

 <tbody>

  <tr>

   <td width="68"><strong>Button</strong></td>

   <td width="493"><strong>Behavior</strong></td>

  </tr>

  <tr>

   <td width="68">UP</td>

   <td width="493"><strong>Change Delay to 0.25 Seconds</strong>: When the UP button is pressed, accelerate mode will be disabled (if active) and the delay between steps will become 0.25 seconds. If the delay is already set to 0.25 seconds, then pressing the UP button will have no effect (and the delay will remain at 0.25 seconds).The new timing must take effect at or before the next pattern transition.</td>

  </tr>

  <tr>

   <td width="68">DOWN</td>

   <td width="493"><strong>Change Delay to 1 Second</strong>: When the DOWN button is pressed, accelerate mode will be disabled (if active) and the delay between steps will become 1 second. If the delay is already set to 1 second, then pressing the DOWN button will have no effect (and the delay will remain at 1 second). The new timing must take effect at or before the next pattern transition.</td>

  </tr>

  <tr>

   <td width="68">SELECT</td>

   <td width="493"><strong>Enable Accelerate Mode</strong>: When the SELECT button is pressed, accelerate mode will be enabled and the delay between steps will become 1 second. Even if accelerate mode is already active, the delay will be changed to 1 second. The new timing must take effect at or before the next pattern transition.</td>

  </tr>

 </tbody>

</table>

When accelerate mode is active, the delay between steps will be <strong>reduced by half </strong>every time the pattern reaches step 0 until the delay is 1<em>/</em>32 seconds (after which point the delay will remain at 1<em>/</em>32 seconds until the delay is changed by an input. When accelerate mode is started, the delay will be set to 1 second. At each successive iteration of step 0 of the pattern, the delay will progress through  and finally  second intervals. The delay will not change on any other step besides step 0. Note that if the UP or DOWN buttons are pressed, accelerate mode must be disabled. Additionally, accelerate mode must be disabled when the program starts (so the only way to initiate accelerate mode is by pressing SELECT).

<h2>3.2        Variable Speeds</h2>

This feature alters the behavior of the UP and DOWN buttons to cycle through a set of different delays, instead of just switching between two preset speeds. When successfully implemented, this feature will allow delays of 1<em>, </em> and  seconds to be selected by pressing the UP and DOWN buttons. If this feature is implemented, the behaviors of UP and DOWN must follow the table below. The behavior of LEFT and RIGHT are unchanged.

<table width="561">

 <tbody>

  <tr>

   <td width="68"><strong>Button</strong></td>

   <td width="493"><strong>Behavior</strong></td>

  </tr>

  <tr>

   <td width="68">UP</td>

   <td width="493"><strong>Decrease delay by factor of 2</strong>: When the UP button is pressed, the delay between steps will be reduced by a factor of 2, to a minimum delay of seconds. If the active delay is  seconds, pressing the UP button will have no effect (under no circumstances should a delay of less than  seconds be used). The new timing must take effect at or before the next pattern transition.</td>

  </tr>

  <tr>

   <td width="68">DOWN</td>

   <td width="493"><strong>Increase delay by factor of 2</strong>: When the DOWN button is pressed, the delay between steps will be increased by a factor of 2, to a maximum delay of 1 second. If the active delay is 1 second, pressing the DOWN button will have no effect (under no circumstances should a delay of more than 1 second be used). The new timing must take effect at or before the next pattern transition.</td>

  </tr>

 </tbody>

</table>

<h2>3.3        Pause Button</h2>

This feature uses the SELECT button to toggle a “pause” state, in which the pattern is frozen at the current step. When the program begins, pause mode is not active (so the pattern animates as usual). When the SELECT button is pressed, pause mode is toggled (so pressing the button when the program is paused will un-pause it, and pressing the button when the program is un-paused will pause it).

When pause mode is active, the pattern does not transition between steps, and remains fixed at the step that was active when the pause button was pressed. However, all other functionality still behaves as normal: In particular, the entire set of user inputs from Section 3 must continue to work. Specifically, if the display mode (Regular/Inverted) is changed, the new mode must be reflected immediately (even when paused), and if the speed is changed, the new speed must take effect as soon as the program is unpaused (however, changing the speed while pause mode is active does <strong>not </strong>un-pause the program).

<h2>3.4        Avoiding Erroneous Multiple Inputs</h2>

The features described in Sections 4.3 and 4.2 are sensitive to button inputs being read repeatedly. For example, consider the fact that a single press of a button (such as SELECT) might take 0.25 seconds (based on the typical time for a human to press a button). During those 0.25 seconds, your program may poll the buttons thousands of times, and each time read that the button was pressed. This is not a problem when the button has only one behavior, such as enabling Inverted Mode, since the multiple reads will just result in Inverted Mode being enabled repeatedly. However, when the same button has multiple behaviors (such as both pausing and unpausing the program), the multiple read problem can result in incorrect behavior.

You will lose marks if the multiple read problem affects your program’s behavior (for example, if pressing the pause button does not reliably toggle the pause state). You can avert the problem by using a button handling routine like the one given in the pseudocode below, which sets an IGNORE_BUTTON variable whenever a button is pressed and clears it when the button is released.

//Input loop while(1){

Read the button value from the ADC if (no button was pressed){

IGNORE_BUTTON = 0 //Clear the ignore flag }else{

//Handle the button normally

//Set the ignore flag IGNORE_BUTTON = 1

}

}

<h1>4              Implementation Suggestions</h1>

This section contains a general guide for implementing a solution. You are not required to follow this progression, but may find it helpful if you don’t know where to start.

<h2>4.1        The Most Basic Option</h2>

If you can implement the basic pattern with no input, using a delay loop for the time delay, you can receive up to 10<em>/</em>18 (see Section 7 below for details). You are encouraged to start by implementing this variant, and then add other features (timer-based delays, user-inputs, etc.) once you have tested the basic pattern. The simple loop-based delay can be modelled by the C-style pseudocode below.

//Initialization

//Use a variable CURRENT_LED to track the currently lit LED with //an index in the range 0-5.

//You will need to write some conversion code, probably a function, //which converts the LED index to a port and bit number.

CURRENT_LED = 0

DIRECTION = 1 //Use a variable to track the “direction” of the LED while(1){ // The program continues running indefinitely

Clear all LEDs

Set CURRENT_LED to be lit.

CURRENT_LED += DIRECTION

//If we have reached LED 0, set the DIRECTION to be 1 if (CURRENT_LED == 0) DIRECTION = 1

//If we have reached LED 5, set the DIRECTION to be -1 else if (CURRENT_LED == 5) DIRECTION = -1

Wait for one second (using a loop)

}

If you use a loop-based delay, you should ensure that its running time is as close to one second as possible (by counting clock cycles). You may lose marks for inaccurate timing code.

<h2>4.2        Using Timers</h2>

Once you have tested the loop-based delay and verified that the logic for incrementing and lighting the LEDs is correct, add an interrupt service routine (ISR) for one of the on-board timers (you are not required to use a particular timer, but may find it easier to use timer 0 or timer 2 on this assignment). You can then modify your code to use one of the two following patterns.

The first pattern uses a ‘light’ interrupt service routine which only increments the LED number (and leaves all of the other work, such as actually changing the lit LED) to the main loop). In the pseudocode below, C functions are used to model the different program components; note that interrupt service routines do not behave like normal functions since they require the use of the RETI instruction. The variables CURRENT_LED and DIRECTION are assumed to be global variables accessible by all parts of the code.

void interrupt_service_routine(){

Compute whether the correct delay has elapsed

(since the ISR may be called repeatedly before the delay has elapsed)

if (the correct delay has elapsed){

CURRENT_LED += DIRECTION

//If we have reached LED 0, set the DIRECTION to be 1 if (CURRENT_LED == 0) DIRECTION = 1

//If we have reached LED 5, set the DIRECTION to be -1 else if (CURRENT_LED == 5) DIRECTION = -1

} }

void main_program(){ //Initialization

CURRENT_LED = 0

DIRECTION = 1

Set up a timer and enable interrupts (both timer interrupt and the global interrupt flag)

while(1){

Clear all LEDs

Set CURRENT_LED to be lit.

//Add button input handlers here when ready }

}

The second pattern uses a ‘heavy’ interrupt service routine which handles both the incrementation and lighting of the LEDs.

void interrupt_service_routine(){

Compute whether the correct delay has elapsed

(since the ISR may be called repeatedly before the delay has elapsed)

if (the correct delay has elapsed){

CURRENT_LED += DIRECTION

//If we have reached LED 0, set the DIRECTION to be 1 if (CURRENT_LED == 0) DIRECTION = 1

//If we have reached LED 5, set the DIRECTION to be -1 else if (CURRENT_LED == 5)

DIRECTION = -1

Clear all LEDs

Set CURRENT_LED to be lit

} }

void main_program(){ //Initialization

CURRENT_LED = 0

DIRECTION = 1

Set up a timer and enable interrupts (both timer interrupt and the global interrupt flag)

while(1){

//Add button input handlers here when ready }

}

<h1>5              Adding an Input Handler</h1>

Since button input is detected with polling, you will need to use a busy-wait loop to test for button inputs. If you followed one of the patterns in the previous section, you should consider adding the busy-wait loop to the main program in the main loop (as a nested loop inside the while(1) infinite loop). You are strongly encouraged to write a function which reads the ADC and returns an index between 0 and 5 (inclusive) corresponding to the button pressed (for example, with 0 meaning no button was pressed, 1 meaning RIGHT was pressed, etc.), then calling that function from the main loop and handling the result appropriately.

<h1>6              Evaluation</h1>

Submit all .asm and .inc files needed to assemble your assignment electronically via conneX. Your code must assemble, upload and run correctly on the ATmega2560 boards in ECS 249 using the toolchain and methodology described in Lab 3. If your code does not assemble as submitted, you will be allowed to spend some of your demo time attempting to fix it, but the demo will be limited to 10 minutes, and you will lose marks if you miss parts of the evaluation by spending time fixing your code. If your code cannot be assembled during the demo, you will receive a mark of at most

2.

This assignment is worth 9% of your final grade and will be marked out of 18 during an interactive demo with an instructor. Demos must be scheduled in advance (through an electronic system available on conneX). If you do not schedule a demo time, or if you do not attend your scheduled demo, you will receive a mark of zero.

The marks are distributed among the aspects of the assignment as follows.

<table width="561">

 <tbody>

  <tr>

   <td width="59"><strong>Marks</strong></td>

   <td width="502"><strong>Aspect</strong></td>

  </tr>

  <tr>

   <td width="59">8</td>

   <td width="502">The ‘basic pattern’ described in Section 2 (non-inverted with a 1 second interval) functions correctly.</td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="502">The code uses functions where appropriate, with the call stack used instead of global variables where feasible. Functions are expected to be documented with comments indicating the set of parameters and return value. It is acceptable to use registers for parameters and return values instead of the stack, but the stack should be used correctly for pushing and popping register and return values.</td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="502">Timekeeping is achieved with one of the timer peripherals (using interrupts) instead of a delay loop, and is accurate. You may be expected to explain the timekeeping scheme and justify its accuracy.</td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="502">The up/down buttons correctly toggle between 0<em>.</em>25 second and 1 second transition intervals in the manner documented in Section 3.</td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="502">The left/right buttons correctly toggle between the inverted and non-inverted modes of operation in the manner documented in Section 3.</td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="502">One (or more) of the ‘extra features’ described in Section 4 is implemented and functions correctly. If you implement multiple extra features, your total mark is capped at 100% (18/18), but you can make up marks lost in other sections. If your implementation does not <strong>exactly </strong>reflect the requirements in the relevant subsection of Section 4, you will lose marks in this component (even for seemingly minor issues like omitting one of the possible delay values in accelerate mode or variable speed mode). You will not receive any credit for extra features which aren’t described in Section 4 unless you have received prior permission from your instructor.</td>

  </tr>

 </tbody>

</table>

<a href="#_ftnref1" name="_ftn1">[1]</a> . For example, if the delay between steps is 1 second and the button is pressed 0.5 seconds after the last transition, the inverted configuration of the current step should be displayed for 0.5 seconds before the next transition